<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <!-- باقي الهيدر كما هو -->
</head>
<body>
    <div class="container">
        <!-- باقي الهيكل كما هو -->
    </div>

    <!-- إضافة Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-firestore-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-storage-compat.js"></script>

    <script>
    // ========== تهيئة Firebase ==========
    const firebaseConfig = {
        apiKey: "AIzaSyYourApiKeyHere",
        authDomain: "your-project.firebaseapp.com",
        projectId: "your-project-id",
        storageBucket: "your-bucket.appspot.com",
        messagingSenderId: "1234567890",
        appId: "1:1234567890:web:abcdef123456"
    };

    // Initialize Firebase
    const app = firebase.initializeApp(firebaseConfig);
    const db = firebase.firestore();
    const auth = firebase.auth();
    const storage = firebase.storage();

    // ========== متغيرات التطبيق ==========
    let currentUser = null;
    let applications = [];
    let jobs = [];
    let mediaRecorder;
    let audioChunks = [];
    let recording = false;
    let seconds = 0;
    let timerInterval;
    let currentApplicationId = null;

    // ========== تهيئة الصفحة ==========
    document.addEventListener('DOMContentLoaded', async () => {
        try {
            // إعداد مستمعي الأحداث
            setupEventListeners();
            
            // تحميل البيانات الأولية
            await loadInitialData();
            
            // التحقق من حالة المصادقة
            auth.onAuthStateChanged(user => {
                currentUser = user;
                if (user) {
                    showSection(dashboardSection);
                    loadApplications();
                } else {
                    showSection(homeSection);
                }
            });
            
        } catch (error) {
            console.error("Error initializing app:", error);
            showNotification("حدث خطأ أثناء تحميل التطبيق", "error");
        }
    });

    // ========== دوال إدارة البيانات ==========
    async function loadInitialData() {
        try {
            // تحميل الوظائف
            const jobsSnapshot = await db.collection("jobs").get();
            jobs = jobsSnapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
            
            // تحميل المتقدمين إذا كان المستخدم موظفاً
            if (currentUser) {
                await loadApplications();
            }
            
        } catch (error) {
            console.error("Error loading initial data:", error);
            throw error;
        }
    }

    async function loadApplications(company = 'all') {
        try {
            showLoading(true);
            
            let query = db.collection("applications");
            
            if (company !== 'all') {
                query = query.where("company", "==", company);
            }
            
            const snapshot = await query.get();
            applications = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
            
            updateApplicantsTable();
            updateStats();
            
        } catch (error) {
            console.error("Error loading applications:", error);
            showNotification("حدث خطأ أثناء تحميل بيانات المتقدمين", "error");
        } finally {
            showLoading(false);
        }
    }

    async function saveApplication(newApplication) {
        try {
            showLoading(true);
            
            // رفع الملف الصوتي إذا موجود
            if (newApplication.audioFile) {
                const audioUrl = await uploadFile(newApplication.audioFile);
                newApplication.audioUrl = audioUrl;
            }
            
            // حفظ بيانات المتقدم
            const docRef = await db.collection("applications").add({
                ...newApplication,
                createdAt: firebase.firestore.FieldValue.serverTimestamp(),
                status: 'pending'
            });
            
            showNotification("تم إرسال طلبك بنجاح!");
            return docRef.id;
            
        } catch (error) {
            console.error("Error saving application:", error);
            showNotification("حدث خطأ أثناء حفظ الطلب", "error");
            throw error;
        } finally {
            showLoading(false);
        }
    }

    async function uploadFile(file) {
        try {
            const storageRef = storage.ref();
            const fileRef = storageRef.child(`applications/${Date.now()}_${file.name}`);
            await fileRef.put(file);
            return await fileRef.getDownloadURL();
        } catch (error) {
            console.error("Error uploading file:", error);
            throw error;
        }
    }

    // ========== دوال واجهة المستخدم ==========
    function setupEventListeners() {
        // أحداث التنقل
        document.getElementById('homeLink').addEventListener('click', (e) => {
            e.preventDefault();
            showSection(homeSection);
        });
        
        document.getElementById('jobsLink').addEventListener('click', (e) => {
            e.preventDefault();
            showSection(homeSection);
            window.scrollTo(0, document.querySelector('.jobs-container').offsetTop - 100);
        });
        
        document.getElementById('applyLink').addEventListener('click', (e) => {
            e.preventDefault();
            showSection(applicationSection);
        });
        
        document.getElementById('staffLoginBtn').addEventListener('click', (e) => {
            e.preventDefault();
            showSection(staffSection);
        });
        
        document.getElementById('aboutLink').addEventListener('click', (e) => {
            e.preventDefault();
            showSection(aboutSection);
        });
        
        // أحداث التقديم على الوظائف
        const selectBtns = document.querySelectorAll('.select-btn');
        selectBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                const jobTitle = btn.getAttribute('data-job');
                const company = btn.getAttribute('data-company');
                document.getElementById('jobPosition').value = jobTitle;
                document.getElementById('jobCompany').value = company;
                showSection(applicationSection);
                applicationSection.scrollIntoView({ behavior: 'smooth' });
            });
        });
        
        // أحداث التسجيل الصوتي
        document.getElementById('recordBtn').addEventListener('click', startRecording);
        document.getElementById('stopBtn').addEventListener('click', stopRecording);
        document.getElementById('deleteBtn').addEventListener('click', deleteRecording);
        
        // أحداث تسجيل الدخول
        document.getElementById('staffLogin').addEventListener('click', staffLogin);
        document.getElementById('logoutBtn').addEventListener('click', logout);
        
        // أحداث لوحة التحكم
        document.querySelectorAll('.filter-option').forEach(option => {
            option.addEventListener('click', () => {
                document.querySelectorAll('.filter-option').forEach(opt => opt.classList.remove('active'));
                option.classList.add('active');
                loadApplications(option.getAttribute('data-company'));
            });
        });
        
        document.getElementById('searchInput').addEventListener('input', searchApplicants);
        document.getElementById('closeDetail').addEventListener('click', () => {
            document.getElementById('applicantDetail').style.display = 'none';
        });
        
        document.getElementById('acceptBtn').addEventListener('click', () => updateApplicationStatus('accepted'));
        document.getElementById('rejectBtn').addEventListener('click', () => updateApplicationStatus('rejected'));
        
        // إرسال النموذج
        document.querySelector('.application-form').addEventListener('submit', submitApplication);
    }

    async function startRecording() {
        try {
            const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
            mediaRecorder = new MediaRecorder(stream);
            
            mediaRecorder.ondataavailable = (e) => {
                audioChunks.push(e.data);
            };
            
            mediaRecorder.onstop = () => {
                const audioBlob = new Blob(audioChunks, { type: 'audio/webm' });
                const audioUrl = URL.createObjectURL(audioBlob);
                document.getElementById('audioPlayback').src = audioUrl;
                document.getElementById('audioPlayback').style.display = 'block';
                document.getElementById('deleteBtn').disabled = false;
            };
            
            mediaRecorder.start();
            recording = true;
            document.getElementById('recordBtn').disabled = true;
            document.getElementById('stopBtn').disabled = false;
            document.getElementById('visualizer').style.display = 'flex';
            
            seconds = 0;
            timerInterval = setInterval(() => {
                seconds++;
                const mins = Math.floor(seconds / 60);
                const secs = seconds % 60;
                document.getElementById('timer').textContent = `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
                
                if (seconds >= 60) {
                    stopRecording();
                }
            }, 1000);
        } catch (err) {
            console.error('Microphone access error:', err);
            showNotification('تعذر الوصول إلى الميكروفون. يرجى التحقق من الإعدادات.', 'error');
        }
    }

    function stopRecording() {
        if (mediaRecorder && recording) {
            mediaRecorder.stop();
            recording = false;
            clearInterval(timerInterval);
            document.getElementById('recordBtn').disabled = false;
            document.getElementById('stopBtn').disabled = true;
            document.getElementById('visualizer').style.display = 'none';
        }
    }

    function deleteRecording() {
        document.getElementById('audioPlayback').src = '';
        document.getElementById('audioPlayback').style.display = 'none';
        document.getElementById('deleteBtn').disabled = true;
        audioChunks = [];
    }

    async function staffLogin() {
        try {
            showLoading(true);
            const password = document.getElementById('password').value;
            
            // في تطبيق حقيقي، استخدم auth.signInWithEmailAndPassword()
            if (password === 'workwise123456') {
                showSection(dashboardSection);
                await loadApplications();
            } else {
                throw new Error('كلمة المرور غير صحيحة');
            }
        } catch (error) {
            console.error('Login error:', error);
            showNotification(error.message || 'حدث خطأ أثناء تسجيل الدخول', 'error');
        } finally {
            showLoading(false);
        }
    }

    function logout() {
        if (confirm('هل أنت متأكد من تسجيل الخروج من لوحة التحكم؟')) {
            showSection(homeSection);
        }
    }

    async function submitApplication(e) {
        e.preventDefault();
        
        try {
            showLoading(true);
            
            const fullName = document.getElementById('fullName').value;
            const phone = document.getElementById('phoneNumber').value;
            const email = document.getElementById('email').value || 'لا يوجد';
            const job = document.getElementById('jobPosition').value;
            const company = document.getElementById('jobCompany').value;
            const notes = document.getElementById('notes').value || 'لا يوجد ملاحظات';
            const audioUrl = document.getElementById('audioPlayback').src;
            
            if (!audioUrl) {
                throw new Error('الرجاء إضافة تسجيل صوتي قبل الإرسال');
            }
            
            await saveApplication({
                fullName,
                phone,
                email,
                job,
                company,
                notes,
                audioUrl,
                date: new Date().toLocaleDateString('ar-EG')
            });
            
            // إعادة تعيين النموذج
            document.querySelector('.application-form').reset();
            document.getElementById('audioPlayback').style.display = 'none';
            document.getElementById('timer').textContent = '00:00';
            seconds = 0;
            audioChunks = [];
            document.getElementById('deleteBtn').disabled = true;
            
            showSection(homeSection);
            
        } catch (error) {
            console.error('Submit error:', error);
            showNotification(error.message || 'حدث خطأ أثناء إرسال الطلب', 'error');
        } finally {
            showLoading(false);
        }
    }

    function updateApplicantsTable() {
        const tableBody = document.getElementById('applicantsTableBody');
        tableBody.innerHTML = '';
        
        applications.forEach(app => {
            const row = document.createElement('tr');
            const randomId = Math.floor(Math.random() * 100);
            const gender = Math.random() > 0.5 ? 'men' : 'women';
            
            row.innerHTML = `
                <td>
                    <div class="applicant-name">
                        <img src="https://randomuser.me/api/portraits/${gender}/${randomId}.jpg" alt="صورة المتقدم">
                        <span>${app.fullName}</span>
                    </div>
                </td>
                <td>${app.job}</td>
                <td>${app.company}</td>
                <td>${app.phone}</td>
                <td>${app.date}</td>
                <td><span class="status ${app.status}">${getStatusText(app.status)}</span></td>
                <td><button class="action-btn view-btn" data-id="${app.id}"><i class="fas fa-eye"></i> عرض</button></td>
            `;
            
            tableBody.appendChild(row);
            
            row.querySelector('.view-btn').addEventListener('click', () => showApplicationDetails(app));
        });
    }

    function showApplicationDetails(app) {
        document.getElementById('detail-fullName').textContent = app.fullName;
        document.getElementById('detail-phone').textContent = app.phone;
        document.getElementById('detail-email').textContent = app.email || 'لا يوجد';
        document.getElementById('detail-job').textContent = app.job;
        document.getElementById('detail-company').textContent = app.company;
        document.getElementById('detail-date').textContent = app.date;
        document.getElementById('detail-status').innerHTML = `<span class="status ${app.status}">${getStatusText(app.status)}</span>`;
        document.getElementById('detail-notes').textContent = app.notes;
        
        if (app.audioUrl) {
            document.getElementById('detail-audio').src = app.audioUrl;
        }
        
        document.getElementById('applicantDetail').style.display = 'block';
        currentApplicationId = app.id;
    }

    async function updateApplicationStatus(status) {
        try {
            if (!currentApplicationId) return;
            
            showLoading(true);
            
            await db.collection("applications").doc(currentApplicationId).update({
                status,
                updatedAt: firebase.firestore.FieldValue.serverTimestamp()
            });
            
            const currentCompany = document.querySelector('.filter-option.active').getAttribute('data-company');
            await loadApplications(currentCompany);
            
            showNotification(`تم تحديث حالة المتقدم إلى: ${getStatusText(status)}`);
            
        } catch (error) {
            console.error("Error updating status:", error);
            showNotification("حدث خطأ أثناء تحديث حالة المتقدم", "error");
        } finally {
            showLoading(false);
        }
    }

    function searchApplicants() {
        const searchTerm = this.value.toLowerCase();
        const rows = document.querySelectorAll('#applicantsTableBody tr');
        
        rows.forEach(row => {
            const name = row.querySelector('.applicant-name span').textContent.toLowerCase();
            const job = row.querySelector('td:nth-child(2)').textContent.toLowerCase();
            row.style.display = (name.includes(searchTerm) || job.includes(searchTerm)) ? '' : 'none';
        });
    }

    function updateStats() {
        document.getElementById('totalApplicants').textContent = applications.length;
        
        const concentrix = applications.filter(app => app.company === 'Concentrix').length;
        const hsbc = applications.filter(app => app.company === 'HSBC').length;
        const volumex = applications.filter(app => app.company === 'Volume X').length;
        const realEstate = applications.filter(app => app.job.includes('عقارية')).length;
        
        document.getElementById('concentrixApplicants').textContent = concentrix;
        document.getElementById('hsbcApplicants').textContent = hsbc;
        document.getElementById('volumexApplicants').textContent = volumex;
        document.getElementById('realEstateApplicants').textContent = realEstate;
    }

    function showSection(section) {
        document.querySelectorAll('section').forEach(sec => {
            sec.style.display = 'none';
        });
        section.style.display = 'block';
        window.scrollTo(0, 0);
    }

    function showNotification(message, type = 'success') {
        const notification = document.getElementById('notification');
        notification.textContent = message;
        notification.style.backgroundColor = type === 'success' ? '#10b981' : '#ef4444';
        notification.style.display = 'block';
        
        setTimeout(() => {
            notification.style.display = 'none';
        }, 5000);
    }

    function showLoading(show) {
        const loader = document.getElementById('loader') || createLoader();
        loader.style.display = show ? 'block' : 'none';
    }

    function createLoader() {
        const loader = document.createElement('div');
        loader.id = 'loader';
        loader.style.position = 'fixed';
        loader.style.top = '0';
        loader.style.left = '0';
        loader.style.width = '100%';
        loader.style.height = '100%';
        loader.style.backgroundColor = 'rgba(0,0,0,0.5)';
        loader.style.zIndex = '1000';
        loader.style.display = 'flex';
        loader.style.justifyContent = 'center';
        loader.style.alignItems = 'center';
        loader.innerHTML = '<div class="spinner"></div>';
        document.body.appendChild(loader);
        return loader;
    }

    function getStatusText(status) {
        const statusMap = {
            pending: 'قيد المراجعة',
            reviewed: 'تمت المراجعة',
            accepted: 'مقبول',
            rejected: 'مرفوض'
        };
        return statusMap[status] || status;
    }
    </script>
</body>
</html>
