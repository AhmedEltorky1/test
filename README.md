<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Work Wise - منصة التوظيف الذكية</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Cairo', sans-serif;
        }
        
        :root {
            --primary: #2563eb;
            --secondary: #1e40af;
            --accent: #f59e0b;
            --light: #f8fafc;
            --dark: #1e293b;
            --gray: #64748b;
            --success: #10b981;
            --concentrix: #ff6b6b;
            --hsbc: #4d96ff;
            --volumex: #6bcb77;
            --real-estate: #9b5de5;
            --staff-bg: #f0f7ff;
        }
        
        body {
            background: linear-gradient(135deg, #f0f9ff 0%, #e0f2fe 100%);
            color: var(--dark);
            min-height: 100vh;
            padding: 20px;
            transition: background 0.5s ease;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            position: relative;
        }
        
        /* شريط التنقل */
        .navbar {
            background: white;
            border-radius: 15px;
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            margin-bottom: 30px;
            transition: all 0.3s ease;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo h1 {
            font-size: 1.8rem;
            color: var(--secondary);
            background: linear-gradient(45deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .logo i {
            font-size: 2rem;
            color: var(--accent);
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        
        .nav-links {
            display: flex;
            gap: 25px;
        }
        
        .nav-links a {
            color: var(--dark);
            text-decoration: none;
            font-weight: 600;
            transition: all 0.3s ease;
            padding: 8px 15px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .nav-links a:hover {
            background: var(--light);
        }
        
        .nav-links a.active {
            background: var(--primary);
            color: white;
        }
        
        .staff-login-btn {
            padding: 10px 25px;
            background: var(--accent);
            color: var(--dark);
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 6px rgba(245, 158, 11, 0.3);
        }
        
        .staff-login-btn:hover {
            background: #e69008;
            transform: translateY(-2px);
        }
        
        /* قسم الرئيسية */
        .home-section {
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
            padding: 40px;
            margin-bottom: 40px;
            animation: fadeIn 0.8s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        header {
            text-align: center;
            padding: 30px 0;
            margin-bottom: 40px;
        }
        
        header h1 {
            font-size: 3.5rem;
            color: var(--secondary);
            margin-bottom: 10px;
            position: relative;
            display: inline-block;
            background: linear-gradient(45deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        header h1::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 150px;
            height: 5px;
            background: var(--accent);
            border-radius: 10px;
        }
        
        header p {
            font-size: 1.2rem;
            color: var(--gray);
            max-width: 700px;
            margin: 20px auto;
            line-height: 1.8;
        }
        
        /* تصنيف الوظائف */
        .categories {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 40px;
        }
        
        .category-btn {
            padding: 12px 25px;
            background: white;
            border: 2px solid var(--primary);
            border-radius: 50px;
            font-weight: bold;
            color: var(--primary);
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .category-btn:hover, .category-btn.active {
            background: var(--primary);
            color: white;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(37, 99, 235, 0.3);
        }
        
        /* قائمة الوظائف */
        .jobs-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 30px;
            margin-bottom: 50px;
        }
        
        .job-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 20px rgba(0,0,0,0.08);
            transition: transform 0.3s ease;
            position: relative;
            border-top: 5px solid var(--primary);
        }
        
        .job-card.concentrix {
            border-top-color: var(--concentrix);
        }
        
        .job-card.hsbc {
            border-top-color: var(--hsbc);
        }
        
        .job-card.volumex {
            border-top-color: var(--volumex);
        }
        
        .job-card.real-estate {
            border-top-color: var(--real-estate);
        }
        
        .job-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0,0,0,0.15);
        }
        
        .job-header {
            background: var(--primary);
            color: white;
            padding: 20px;
            position: relative;
        }
        
        .job-header.concentrix {
            background: var(--concentrix);
        }
        
        .job-header.hsbc {
            background: var(--hsbc);
        }
        
        .job-header.volumex {
            background: var(--volumex);
        }
        
        .job-header.real-estate {
            background: var(--real-estate);
        }
        
        .job-header h3 {
            font-size: 1.5rem;
            margin-bottom: 5px;
        }
        
        .job-type {
            background: var(--accent);
            color: var(--dark);
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            position: absolute;
            top: 20px;
            left: 20px;
            font-weight: bold;
        }
        
        .job-body {
            padding: 25px;
        }
        
        .job-details {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            border-bottom: 1px dashed #e2e8f0;
            padding-bottom: 20px;
        }
        
        .detail {
            text-align: center;
            flex: 1;
        }
        
        .detail i {
            font-size: 1.5rem;
            color: var(--primary);
            margin-bottom: 5px;
        }
        
        .detail span {
            display: block;
            font-weight: bold;
            margin-top: 5px;
            font-size: 0.9rem;
        }
        
        .requirements {
            background: #f8fafc;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 3px solid var(--primary);
        }
        
        .requirements h4 {
            margin-bottom: 10px;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .requirements ul {
            padding-right: 20px;
        }
        
        .requirements li {
            margin-bottom: 8px;
            position: relative;
            padding-right: 15px;
        }
        
        .requirements li::before {
            content: "•";
            color: var(--primary);
            font-weight: bold;
            position: absolute;
            right: 0;
        }
        
        .select-btn {
            display: block;
            width: 100%;
            padding: 15px;
            background: var(--success);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s ease;
            box-shadow: 0 4px 6px rgba(16, 185, 129, 0.3);
        }
        
        .select-btn:hover {
            background: #0da271;
            transform: translateY(-2px);
        }
        
        /* قسم التقديم */
        .application-section {
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
            padding: 40px;
            margin: 50px 0;
            display: none;
            animation: fadeIn 0.8s ease;
        }
        
        .application-section h2 {
            text-align: center;
            color: var(--secondary);
            margin-bottom: 30px;
            font-size: 2.2rem;
            background: linear-gradient(45deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .application-form {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group.full {
            grid-column: span 2;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .form-group input, .form-group textarea, .form-group select {
            width: 100%;
            padding: 15px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }
        
        .form-group input:focus, .form-group textarea:focus, .form-group select:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
        }
        
        .voice-recorder {
            background: #f1f5f9;
            border-radius: 15px;
            padding: 25px;
            margin: 20px 0;
            box-shadow: inset 0 0 10px rgba(0,0,0,0.05);
        }
        
        .recorder-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .recorder-title {
            font-size: 1.3rem;
            color: var(--secondary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .recorder-controls {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        .recorder-btn {
            padding: 12px 20px;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: background 0.3s ease;
        }
        
        .recorder-btn:disabled {
            background: var(--gray);
            cursor: not-allowed;
            opacity: 0.7;
        }
        
        .recorder-btn.stop {
            background: #ef4444;
        }
        
        .recorder-btn.delete {
            background: #9ca3af;
        }
        
        .recorder-btn.stop:hover {
            background: #dc2626;
        }
        
        .recorder-btn.delete:hover {
            background: #6b7280;
        }
        
        .recorder-btn:hover {
            background: var(--secondary);
            transform: translateY(-2px);
        }
        
        .timer {
            text-align: center;
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--dark);
            margin: 15px 0;
        }
        
        .recording-visualizer {
            height: 80px;
            background: #e2e8f0;
            border-radius: 10px;
            margin: 20px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
            padding: 0 20px;
            display: none;
        }
        
        .bar {
            width: 8px;
            background: var(--primary);
            border-radius: 10px;
            height: 30px;
            animation: pulse 1.2s infinite ease-in-out;
        }
        
        @keyframes pulse {
            0%, 100% { transform: scaleY(1); }
            50% { transform: scaleY(0.4); }
        }
        
        .audio-playback {
            width: 100%;
            margin: 20px 0;
            display: none;
        }
        
        .submit-btn {
            grid-column: span 2;
            padding: 18px;
            background: var(--secondary);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 1.2rem;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s ease;
            margin-top: 20px;
            box-shadow: 0 4px 6px rgba(30, 64, 175, 0.3);
        }
        
        .submit-btn:hover {
            background: var(--primary);
            transform: translateY(-2px);
        }
        
        /* قسم الموظفين */
        .staff-section {
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
            padding: 40px;
            margin: 50px 0;
            text-align: center;
            display: none;
            animation: fadeIn 0.8s ease;
        }
        
        .staff-section h2 {
            color: var(--secondary);
            margin-bottom: 20px;
            font-size: 2rem;
            background: linear-gradient(45deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .staff-section p {
            color: var(--gray);
            max-width: 600px;
            margin: 0 auto 30px;
            line-height: 1.7;
        }
        
        .login-form {
            max-width: 500px;
            margin: 0 auto;
        }
        
        .password-input {
            position: relative;
            margin-bottom: 25px;
        }
        
        .password-input input {
            width: 100%;
            padding: 16px 50px 16px 20px;
            border: 2px solid #e2e8f0;
            border-radius: 12px;
            font-size: 1.1rem;
            transition: border-color 0.3s ease;
        }
        
        .password-input input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
        }
        
        .password-toggle {
            position: absolute;
            top: 50%;
            right: 15px;
            transform: translateY(-50%);
            cursor: pointer;
            color: var(--gray);
            background: none;
            border: none;
            font-size: 1.2rem;
        }
        
        .staff-btn {
            padding: 16px 40px;
            background: var(--accent);
            color: var(--dark);
            border: none;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s ease;
            box-shadow: 0 4px 6px rgba(245, 158, 11, 0.3);
        }
        
        .staff-btn:hover {
            background: #e69008;
            transform: translateY(-2px);
        }
        
        /* لوحة تحكم الموظفين */
        .dashboard-section {
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
            padding: 40px;
            margin: 50px 0;
            display: none;
            animation: fadeIn 0.8s ease;
        }
        
        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .dashboard-header h2 {
            font-size: 1.8rem;
            color: var(--secondary);
            background: linear-gradient(45deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .stats-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .stat-card {
            background: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            border-top: 4px solid var(--primary);
            transition: transform 0.3s ease;
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.1);
        }
        
        .stat-card.concentrix {
            border-top-color: var(--concentrix);
        }
        
        .stat-card.hsbc {
            border-top-color: var(--hsbc);
        }
        
        .stat-card.volumex {
            border-top-color: var(--volumex);
        }
        
        .stat-card.real-estate {
            border-top-color: var(--real-estate);
        }
        
        .stat-card h3 {
            font-size: 1.1rem;
            color: var(--gray);
            margin-bottom: 15px;
        }
        
        .stat-card .value {
            font-size: 2rem;
            font-weight: bold;
            color: var(--dark);
        }
        
        /* جدول المتقدمين */
        .applicants-section {
            background: white;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.05);
            padding: 25px;
            margin-top: 30px;
        }
        
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }
        
        .section-header h3 {
            font-size: 1.5rem;
            color: var(--secondary);
        }
        
        .controls {
            display: flex;
            gap: 15px;
        }
        
        .filter-btn, .export-btn {
            padding: 10px 20px;
            background: var(--staff-bg);
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: background 0.3s ease;
        }
        
        .filter-btn:hover, .export-btn:hover {
            background: #e2e8f0;
        }
        
        .search-box {
            position: relative;
            width: 300px;
        }
        
        .search-box input {
            width: 100%;
            padding: 12px 20px 12px 45px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
        }
        
        .search-box i {
            position: absolute;
            top: 50%;
            right: 15px;
            transform: translateY(-50%);
            color: var(--gray);
        }
        
        /* جدول المتقدمين */
        .applicants-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .applicants-table th {
            background: var(--staff-bg);
            padding: 15px;
            text-align: right;
            font-weight: 700;
            color: var(--dark);
            border-bottom: 2px solid #e2e8f0;
        }
        
        .applicants-table td {
            padding: 15px;
            border-bottom: 1px solid #e2e8f0;
            color: var(--gray);
        }
        
        .applicants-table tr:hover {
            background: #f8fafc;
        }
        
        .applicant-name {
            display: flex;
            align-items: center;
            gap: 15px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .applicant-name img {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            object-fit: cover;
        }
        
        .status {
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 600;
            display: inline-block;
        }
        
        .status.pending {
            background: #fffbeb;
            color: #f59e0b;
        }
        
        .status.reviewed {
            background: #ecfdf5;
            color: #10b981;
        }
        
        .status.accepted {
            background: #d1fae5;
            color: #065f46;
        }
        
        .status.rejected {
            background: #fef2f2;
            color: #ef4444;
        }
        
        .action-btn {
            padding: 8px 15px;
            background: var(--staff-bg);
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.3s ease;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .action-btn:hover {
            background: #e2e8f0;
        }
        
        /* تفاصيل المتقدم */
        .applicant-detail {
            background: white;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.05);
            padding: 30px;
            margin-top: 30px;
            display: none;
            animation: fadeIn 0.8s ease;
        }
        
        .detail-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            padding-bottom: 20px;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .detail-header h3 {
            font-size: 1.8rem;
            color: var(--secondary);
        }
        
        .close-btn {
            background: var(--staff-bg);
            border: none;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.2rem;
            transition: background 0.3s ease;
        }
        
        .close-btn:hover {
            background: #e2e8f0;
        }
        
        .applicant-info {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }
        
        .info-card {
            background: var(--staff-bg);
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.05);
        }
        
        .info-card h4 {
            margin-bottom: 15px;
            color: var(--secondary);
            padding-bottom: 10px;
            border-bottom: 1px solid #e2e8f0;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .info-row {
            display: flex;
            margin-bottom: 15px;
        }
        
        .info-label {
            font-weight: 600;
            color: var(--dark);
            width: 150px;
        }
        
        .info-value {
            flex: 1;
            color: var(--gray);
        }
        
        /* مشغل الصوت */
        .voice-player {
            background: var(--staff-bg);
            border-radius: 15px;
            padding: 25px;
            margin-top: 20px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.05);
        }
        
        .player-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .player-header h4 {
            font-size: 1.3rem;
            color: var(--secondary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .audio-controls {
            display: flex;
            gap: 15px;
        }
        
        .audio-player {
            width: 100%;
            margin-top: 15px;
        }
        
        .transcript {
            background: white;
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
            border: 1px solid #e2e8f0;
        }
        
        .transcript h5 {
            margin-bottom: 15px;
            color: var(--dark);
        }
        
        .transcript p {
            line-height: 1.8;
            color: var(--gray);
        }
        
        footer {
            text-align: center;
            padding: 30px 0;
            color: var(--gray);
            border-top: 1px solid #e2e8f0;
            margin-top: 50px;
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 25px;
            background: var(--success);
            color: white;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
        }
        
        .about-section {
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
            padding: 40px;
            margin: 50px 0;
            display: none;
            animation: fadeIn 0.8s ease;
        }
        
        .about-content {
            max-width: 800px;
            margin: 0 auto;
        }
        
        .about-content h2 {
            text-align: center;
            margin-bottom: 30px;
            color: var(--secondary);
        }
        
        .ceo-info {
            display: flex;
            align-items: center;
            gap: 30px;
            margin-bottom: 40px;
            background: var(--staff-bg);
            padding: 20px;
            border-radius: 15px;
        }
        
        .ceo-photo {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            background: linear-gradient(45deg, var(--primary), var(--accent));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 3rem;
        }
        
        .ceo-details h3 {
            margin-bottom: 10px;
            font-size: 1.8rem;
        }
        
        .social-links {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }
        
        .social-links a {
            display: inline-block;
            padding: 10px 20px;
            background: var(--primary);
            color: white;
            border-radius: 8px;
            text-decoration: none;
            transition: all 0.3s ease;
        }
        
        .social-links a:hover {
            background: var(--secondary);
            transform: translateY(-3px);
        }
        
        .company-info {
            text-align: center;
            line-height: 1.8;
            margin-bottom: 30px;
        }
        
        /* الرسومات البيانية */
        .chart-container {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-top: 30px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        }
        
        .chart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .chart-header h3 {
            font-size: 1.5rem;
            color: var(--secondary);
        }
        
        .chart-wrapper {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
        }
        
        .chart-box {
            flex: 1;
            min-width: 300px;
            background: #f8fafc;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.05);
        }
        
        .chart-title {
            text-align: center;
            margin-bottom: 15px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .chart {
            height: 250px;
            display: flex;
            align-items: flex-end;
            justify-content: space-around;
            gap: 10px;
            padding: 10px;
        }
        
        .bar-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            height: 100%;
        }
        
        .bar-label {
            margin-top: 5px;
            font-size: 0.9rem;
        }
        
        .chart-bar {
            width: 40px;
            background: var(--primary);
            border-radius: 5px 5px 0 0;
            transition: height 0.5s ease;
        }
        
        .legend {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .legend-color {
            width: 15px;
            height: 15px;
            border-radius: 3px;
        }
        
        /* تصفية الشركات */
        .company-filter {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .filter-option {
            padding: 8px 15px;
            background: #e2e8f0;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .filter-option.active {
            background: var(--primary);
            color: white;
        }
        
        @media (max-width: 768px) {
            .application-form {
                grid-template-columns: 1fr;
            }
            
            .form-group.full {
                grid-column: span 1;
            }
            
            .submit-btn {
                grid-column: span 1;
            }
            
            .jobs-container {
                grid-template-columns: 1fr;
            }
            
            header h1 {
                font-size: 2.5rem;
            }
            
            .navbar {
                flex-direction: column;
                gap: 15px;
            }
            
            .nav-links {
                flex-wrap: wrap;
                justify-content: center;
            }
            
            .dashboard-header {
                flex-direction: column;
                gap: 15px;
                align-items: flex-start;
            }
            
            .section-header {
                flex-direction: column;
                gap: 15px;
                align-items: flex-start;
            }
            
            .controls {
                width: 100%;
                flex-direction: column;
            }
            
            .search-box {
                width: 100%;
            }
            
            .ceo-info {
                flex-direction: column;
                text-align: center;
            }
            
            .social-links {
                justify-content: center;
            }
            
            .chart-wrapper {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- شريط التنقل -->
        <nav class="navbar">
            <div class="logo">
                <i class="fas fa-briefcase"></i>
                <h1>Work Wise</h1>
            </div>
            
            <div class="nav-links">
                <a href="#" class="active" id="homeLink"><i class="fas fa-home"></i> الرئيسية</a>
                <a href="#" id="jobsLink"><i class="fas fa-briefcase"></i> الوظائف</a>
                <a href="#" id="applyLink"><i class="fas fa-file-alt"></i> التقديم</a>
                <a href="#" id="aboutLink"><i class="fas fa-info-circle"></i> عنا</a>
            </div>
            
            <button class="staff-login-btn" id="staffLoginBtn">
                <i class="fas fa-lock"></i> دخول الموظفين
            </button>
        </nav>
        
        <!-- قسم الرئيسية -->
        <section id="homeSection" class="home-section">
            <header>
                <h1><i class="fas fa-briefcase"></i> Work Wise</h1>
                <p>منصة التوظيف الذكية التي تساعدك في العثور على أفضل الفرص الوظيفية. تصفح مئات الوظائف في مختلف المجالات وقدم طلبك بسهولة وأمان.</p>
            </header>
            
            <!-- تصنيف الوظائف -->
            <div class="categories">
                <button class="category-btn active">جميع الوظائف</button>
                <button class="category-btn">وظائف كول سنتر</button>
                <button class="category-btn">وظائف بنوك</button>
                <button class="category-btn">دوام جزئي</button>
                <button class="category-btn">عمل حر</button>
            </div>
            
            <!-- قائمة الوظائف -->
            <div class="jobs-container">
                <!-- وظيفة Concentrix الإنجليزية - المعادي -->
                <div class="job-card concentrix">
                    <div class="job-header concentrix">
                        <div class="job-type">دوام كامل</div>
                        <h3>مندوب خدمة عملاء (الإنجليزية)</h3>
                        <p>Concentrix - المعادي</p>
                    </div>
                    <div class="job-body">
                        <div class="job-details">
                            <div class="detail">
                                <i class="fas fa-map-marker-alt"></i>
                                <span>المعادي</span>
                            </div>
                            <div class="detail">
                                <i class="fas fa-money-bill-wave"></i>
                                <span>14,000 - 19,000 ج.م</span>
                            </div>
                            <div class="detail">
                                <i class="fas fa-clock"></i>
                                <span>9 ساعات</span>
                            </div>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-list-check"></i> المتطلبات:</h4>
                            <ul>
                                <li>إجادة اللغة الإنجليزية (مستوى B2 أو C1)</li>
                                <li>خبرة سابقة</li>
                                <li>مهارات تواصل</li>
                            </ul>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-gift"></i> المميزات:</h4>
                            <ul>
                                <li>راتب ثابت شهري</li>
                                <li>تأمين صحي شامل</li>
                                <li>حوافز شهرية مجزية</li>
                                <li>بدل مواصلات (حسب المسافة)</li>
                            </ul>
                        </div>
                        
                        <button class="select-btn" data-job="مندوب خدمة عملاء (الإنجليزية)" data-company="Concentrix - المعادي">
                            <i class="fas fa-paper-plane"></i> التقديم على الوظيفة
                        </button>
                    </div>
                </div>
                
                <!-- وظيفة Concentrix الفرنسية - 6 أكتوبر -->
                <div class="job-card concentrix">
                    <div class="job-header concentrix">
                        <div class="job-type">دوام كامل</div>
                        <h3>مندوب خدمة عملاء (الفرنسية)</h3>
                        <p>Concentrix - 6 أكتوبر</p>
                    </div>
                    <div class="job-body">
                        <div class="job-details">
                            <div class="detail">
                                <i class="fas fa-map-marker-alt"></i>
                                <span>6 أكتوبر</span>
                            </div>
                            <div class="detail">
                                <i class="fas fa-money-bill-wave"></i>
                                <span>26,000 - 34,000 ج.م</span>
                            </div>
                            <div class="detail">
                                <i class="fas fa-clock"></i>
                                <span>9 ساعات</span>
                            </div>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-list-check"></i> المتطلبات:</h4>
                            <ul>
                                <li>إجادة اللغة الفرنسية (B2 أو C1)</li>
                                <li>خبرة سنة</li>
                                <li>مهارات تواصل - خدمة عملاء</li>
                            </ul>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-gift"></i> المميزات:</h4>
                            <ul>
                                <li>مكافأة شهرية 5,000 جنيه</li>
                                <li>تأمين صحي شامل</li>
                                <li>حوافز شهرية مجزية</li>
                                <li>بدل سكن للمغتربين أو مواصلات</li>
                            </ul>
                        </div>
                        
                        <button class="select-btn" data-job="مندوب خدمة عملاء (الفرنسية)" data-company="Concentrix - 6 أكتوبر">
                            <i class="fas fa-paper-plane"></i> التقديم على الوظيفة
                        </button>
                    </div>
                </div>
                
                <!-- وظيفة HSBC -->
                <div class="job-card hsbc">
                    <div class="job-header hsbc">
                        <div class="job-type">دوام كامل</div>
                        <h3>مندوب خدمة عملاء</h3>
                        <p>HSBC</p>
                    </div>
                    <div class="job-body">
                        <div class="job-details">
                            <div class="detail">
                                <i class="fas fa-map-marker-alt"></i>
                                <span>Smart Village</span>
                            </div>
                            <div class="detail">
                                <i class="fas fa-money-bill-wave"></i>
                                <span>9,000 - 15,700 ج.م</span>
                            </div>
                            <div class="detail">
                                <i class="fas fa-clock"></i>
                                <span>9 ساعات</span>
                            </div>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-list-check"></i> المتطلبات:</h4>
                            <ul>
                                <li>إجادة اللغة الإنجليزية (مستوى B2)</li>
                                <li>سن لا يزيد عن 35 سنة</li>
                                <li>مهارات تواصل - خدمة عملاء</li>
                                <li>لا يشترط خبرة (سيتم تدريب المقبولين)</li>
                            </ul>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-gift"></i> المميزات:</h4>
                            <ul>
                                <li>تأمين صحي شامل</li>
                                <li>بدل مواصلات</li>
                                <li>بونص سنوي</li>
                                <li>بدل سكن</li>
                                <li>تأمين اجتماعي</li>
                            </ul>
                        </div>
                        
                        <button class="select-btn" data-job="مندوب خدمة عملاء" data-company="HSBC">
                            <i class="fas fa-paper-plane"></i> التقديم على الوظيفة
                        </button>
                    </div>
                </div>
                
                <!-- وظيفة Volume X العقارية -->
                <div class="job-card real-estate">
                    <div class="job-header real-estate">
                        <div class="job-type">دوام جزئي</div>
                        <h3>مندوب مبيعات عقارية (Acquisition)</h3>
                        <p>Volume X</p>
                    </div>
                    <div class="job-body">
                        <div class="job-details">
                            <div class="detail">
                                <i class="fas fa-map-marker-alt"></i>
                                <span>أي مكان</span>
                            </div>
                            <div class="detail">
                                <i class="fas fa-money-bill-wave"></i>
                                <span>$4.2/ساعة + عمولة</span>
                            </div>
                            <div class="detail">
                                <i class="fas fa-clock"></i>
                                <span>40 ساعة/أسبوع</span>
                            </div>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-list-check"></i> المتطلبات:</h4>
                            <ul>
                                <li>إجادة اللغة الإنجليزية (مستوى B2)</li>
                                <li>خبرة 6 أشهر في المبيعات (حقلية أو تليفونية)</li>
                                <li>خبرة سابقة في مجال العقارات أو التسويق المباشر</li>
                                <li>القدرة على تحقيق أهداف مبيعات شهرية محددة</li>
                            </ul>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-gift"></i> المميزات:</h4>
                            <ul>
                                <li>عمل عن بعد</li>
                                <li>راتب ثابت + عمولة</li>
                                <li>تدريب مجاني (شهادة معتمدة)</li>
                                <li>بيانات عملاء جاهزة للاتصال</li>
                                <li>فرص ترقية إلى مدير فريق</li>
                            </ul>
                        </div>
                        
                        <div class="requirements">
                            <h4><i class="fas fa-building"></i> عن الشركة:</h4>
                            <ul>
                                <li>شركة عقارية دولية مرخصة</li>
                                <li>مكاتب في دبي وأبو ظبي</li>
                                <li>أكثر من 10 سنوات خبرة</li>
                                <li>تعمل في سوق الإمارات والسعودية</li>
                            </ul>
                        </div>
                        
                        <button class="select-btn" data-job="مندوب مبيعات عقارية (Acquisition)" data-company="Volume X">
                            <i class="fas fa-paper-plane"></i> التقديم على الوظيفة
                        </button>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- قسم التقديم -->
        <section id="applicationSection" class="application-section">
            <h2><i class="fas fa-file-alt"></i> نموذج التقديم للوظيفة</h2>
            <form class="application-form">
                <div class="form-group">
                    <label for="fullName"><i class="fas fa-user"></i> الاسم بالكامل</label>
                    <input type="text" id="fullName" required>
                </div>
                
                <div class="form-group">
                    <label for="phoneNumber"><i class="fas fa-phone"></i> رقم الهاتف</label>
                    <input type="tel" id="phoneNumber" required>
                </div>
                
                <div class="form-group">
                    <label for="email"><i class="fas fa-envelope"></i> البريد الإلكتروني</label>
                    <input type="email" id="email">
                </div>
                
                <div class="form-group">
                    <label for="jobPosition"><i class="fas fa-briefcase"></i> المسمى الوظيفي</label>
                    <input type="text" id="jobPosition" readonly>
                </div>
                
                <div class="form-group">
                    <label for="jobCompany"><i class="fas fa-building"></i> الشركة</label>
                    <input type="text" id="jobCompany" readonly>
                </div>
                
                <div class="form-group full">
                    <label><i class="fas fa-edit"></i> ملاحظات</label>
                    <textarea rows="3" placeholder="أخبرنا عن خبراتك ومؤهلاتك..." id="notes"></textarea>
                </div>
                
                <div class="form-group full">
                    <div class="voice-recorder">
                        <div class="recorder-header">
                            <div class="recorder-title">
                                <i class="fas fa-microphone"></i> رسالة صوتية (اختيارية)
                            </div>
                            <div class="recorder-controls">
                                <button type="button" class="recorder-btn" id="recordBtn">
                                    <i class="fas fa-circle"></i> بدء التسجيل
                                </button>
                                <button type="button" class="recorder-btn stop" id="stopBtn" disabled>
                                    <i class="fas fa-stop"></i> إيقاف التسجيل
                                </button>
                                <button type="button" class="recorder-btn delete" id="deleteBtn" disabled>
                                    <i class="fas fa-trash"></i> حذف التسجيل
                                </button>
                            </div>
                        </div>
                        
                        <div class="timer" id="timer">00:00</div>
                        
                        <div class="recording-visualizer" id="visualizer">
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                            <div class="bar"></div>
                        </div>
                        
                        <audio class="audio-playback" id="audioPlayback" controls></audio>
                    </div>
                </div>
                
                <button type="submit" class="submit-btn">
                    <i class="fas fa-paper-plane"></i> إرسال الطلب
                </button>
            </form>
        </section>
        
        <!-- قسم الموظفين -->
        <section id="staffSection" class="staff-section">
            <h2><i class="fas fa-lock"></i> دخول الموظفين</h2>
            <p>الرجاء إدخال كلمة المرور الخاصة بالموظفين للوصول إلى لوحة التحكم.</p>
            
            <div class="login-form">
                <div class="password-input">
                    <input type="password" id="password" placeholder="أدخل كلمة المرور">
                    <button class="password-toggle" id="passwordToggle">
                        <i class="fas fa-eye"></i>
                    </button>
                </div>
                
                <button class="staff-btn" id="staffLogin">دخول الموظفين</button>
            </div>
        </section>
        
        <!-- لوحة تحكم الموظفين -->
        <section id="dashboardSection" class="dashboard-section">
            <div class="dashboard-header">
                <h2><i class="fas fa-tachometer-alt"></i> لوحة تحكم الموظفين</h2>
                <button class="staff-login-btn" id="logoutBtn">
                    <i class="fas fa-sign-out-alt"></i> تسجيل الخروج
                </button>
            </div>
            
            <!-- إحصائيات المتقدمين -->
            <div class="stats-cards">
                <div class="stat-card">
                    <h3>إجمالي المتقدمين</h3>
                    <div class="value" id="totalApplicants">0</div>
                </div>
                
                <div class="stat-card concentrix">
                    <h3>متقدمين Concentrix</h3>
                    <div class="value" id="concentrixApplicants">0</div>
                </div>
                
                <div class="stat-card hsbc">
                    <h3>متقدمين HSBC</h3>
                    <div class="value" id="hsbcApplicants">0</div>
                </div>
                
                <div class="stat-card volumex">
                    <h3>متقدمين Volume X</h3>
                    <div class="value" id="volumexApplicants">0</div>
                </div>
                
                <div class="stat-card real-estate">
                    <h3>متقدمين العقارات</h3>
                    <div class="value" id="realEstateApplicants">0</div>
                </div>
            </div>
            
            <!-- تصفية الشركات -->
            <div class="company-filter">
                <div class="filter-option active" data-company="all">الكل</div>
                <div class="filter-option" data-company="Concentrix">Concentrix</div>
                <div class="filter-option" data-company="HSBC">HSBC</div>
                <div class="filter-option" data-company="Volume X">Volume X</div>
            </div>
            
            <!-- جدول المتقدمين -->
            <div class="applicants-section">
                <div class="section-header">
                    <h3><i class="fas fa-user-friends"></i> قائمة المتقدمين</h3>
                    
                    <div class="controls">
                        <div class="search-box">
                            <input type="text" id="searchInput" placeholder="ابحث عن متقدم...">
                            <i class="fas fa-search"></i>
                        </div>
                        <button class="filter-btn"><i class="fas fa-filter"></i> تصفية</button>
                        <button class="export-btn"><i class="fas fa-file-export"></i> تصدير</button>
                    </div>
                </div>
                
                <table class="applicants-table">
                    <thead>
                        <tr>
                            <th>المتقدم</th>
                            <th>الوظيفة</th>
                            <th>الشركة</th>
                            <th>رقم الهاتف</th>
                            <th>التاريخ</th>
                            <th>حالة الطلب</th>
                            <th>الإجراءات</th>
                        </tr>
                    </thead>
                    <tbody id="applicantsTableBody">
                        <!-- سيتم ملء الجدول بالمتقدمين -->
                    </tbody>
                </table>
            </div>
            
            <!-- تفاصيل المتقدم -->
            <div class="applicant-detail" id="applicantDetail">
                <div class="detail-header">
                    <h3>تفاصيل المتقدم</h3>
                    <button class="close-btn" id="closeDetail"><i class="fas fa-times"></i></button>
                </div>
                
                <div class="applicant-info">
                    <div class="info-card">
                        <h4><i class="fas fa-user"></i> المعلومات الشخصية</h4>
                        <div class="info-row">
                            <div class="info-label">الاسم الكامل:</div>
                            <div class="info-value" id="detail-fullName">-</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">رقم الهاتف:</div>
                            <div class="info-value" id="detail-phone">-</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">البريد الإلكتروني:</div>
                            <div class="info-value" id="detail-email">-</div>
                        </div>
                    </div>
                    
                    <div class="info-card">
                        <h4><i class="fas fa-briefcase"></i> معلومات الوظيفة</h4>
                        <div class="info-row">
                            <div class="info-label">الوظيفة:</div>
                            <div class="info-value" id="detail-job">-</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">الشركة:</div>
                            <div class="info-value" id="detail-company">-</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">تاريخ التقديم:</div>
                            <div class="info-value" id="detail-date">-</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">الحالة:</div>
                            <div class="info-value" id="detail-status">-</div>
                        </div>
                    </div>
                    
                    <div class="info-card">
                        <h4><i class="fas fa-file-alt"></i> معلومات إضافية</h4>
                        <div class="info-row">
                            <div class="info-label">ملاحظات:</div>
                            <div class="info-value" id="detail-notes">-</div>
                        </div>
                    </div>
                </div>
                
                <!-- مشغل الصوت -->
                <div class="voice-player">
                    <div class="player-header">
                        <h4><i class="fas fa-microphone-alt"></i> الرسالة الصوتية للمتقدم</h4>
                        <div class="audio-controls">
                            <button class="action-btn"><i class="fas fa-download"></i> تحميل</button>
                            <button class="action-btn"><i class="fas fa-share-alt"></i> مشاركة</button>
                        </div>
                    </div>
                    
                    <audio class="audio-player" controls id="detail-audio">
                        <source src="#" type="audio/mpeg">
                        المتصفح لا يدعم تشغيل الصوت.
                    </audio>
                </div>
                
                <!-- إجراءات المتقدم -->
                <div style="display: flex; gap: 15px; margin-top: 30px; flex-wrap: wrap;">
                    <button class="action-btn" style="background: var(--success); color: white;" id="acceptBtn">
                        <i class="fas fa-check"></i> قبول المتقدم
                    </button>
                    <button class="action-btn" style="background: #ef4444; color: white;" id="rejectBtn">
                        <i class="fas fa-times"></i> رفض المتقدم
                    </button>
                    <button class="action-btn" id="emailBtn">
                        <i class="fas fa-envelope"></i> إرسال بريد
                    </button>
                    <button class="action-btn" id="interviewBtn">
                        <i class="fas fa-phone"></i> مقابلة هاتفية
                    </button>
                </div>
            </div>
        </section>
        
        <!-- قسم عنا -->
        <section id="aboutSection" class="about-section">
            <div class="about-content">
                <h2><i class="fas fa-info-circle"></i> عن منصة Work Wise</h2>
                
                <div class="ceo-info">
                    <div class="ceo-photo">
                        <i class="fas fa-user-tie"></i>
                    </div>
                    <div class="ceo-details">
                        <h3>Bishoy - المؤسس والمدير التنفيذي</h3>
                        <p>مرحباً بكم في Work Wise، منصة التوظيف الرائدة في المنطقة منذ أكثر من 10 سنوات في مجال التوظيف.</p>
                        
                        <div class="social-links">
                            <a href="https://www.instagram.com/workwisegy?igsh=Y29uY2g0MmRpaHAx" target="_blank">
                                <i class="fab fa-instagram"></i> Instagram
                            </a>
                            <a href="https://www.facebook.com/share/1FJ4C1asYg/" target="_blank">
                                <i class="fab fa-facebook"></i> Facebook
                            </a>
                        </div>
                    </div>
                </div>
                
                <div class="company-info">
                    <p>Work Wise هي منصة توظيف ذكية تساعد الشركات في العثور على أفضل المواهب والمتقدمين في العثور على فرصهم المثالية. منذ تأسيسها عام 2020، ساعدت أكثر من 5000 شخص في الحصول على وظائف أحلامهم.</p>
                    <p>نحن نؤمن بأن كل شخص يستحق فرصة عادلة للحصول على وظيفة تناسب مهاراته وتطلعاته، ونسعى جاهدين لتحقيق هذه الرؤية.</p>
                </div>
            </div>
        </section>
        
        <footer>
            <p>جميع الحقوق محفوظة &copy; 2023 Work Wise - منصة التوظيف الذكية</p>
            <p>تم الإنشاء بواسطة المهندس أحمد التركي</p>
        </footer>
        
        <div class="notification" id="notification">تم إرسال طلبك بنجاح!</div>
    </div>

    <script>
        // تبديل الأقسام
        const homeSection = document.getElementById('homeSection');
        const applicationSection = document.getElementById('applicationSection');
        const staffSection = document.getElementById('staffSection');
        const dashboardSection = document.getElementById('dashboardSection');
        const aboutSection = document.getElementById('aboutSection');
        const notification = document.getElementById('notification');
        
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
        
        function showSection(section) {
            homeSection.style.display = 'none';
            applicationSection.style.display = 'none';
            staffSection.style.display = 'none';
            dashboardSection.style.display = 'none';
            aboutSection.style.display = 'none';
            section.style.display = 'block';
            window.scrollTo(0, 0);
        }
        
        // اختيار الوظيفة
        const selectBtns = document.querySelectorAll('.select-btn');
        const jobPositionInput = document.getElementById('jobPosition');
        const jobCompanyInput = document.getElementById('jobCompany');
        
        selectBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                const jobTitle = btn.getAttribute('data-job');
                const company = btn.getAttribute('data-company');
                jobPositionInput.value = jobTitle;
                jobCompanyInput.value = company;
                showSection(applicationSection);
                
                // التمرير إلى القسم
                applicationSection.scrollIntoView({ behavior: 'smooth' });
            });
        });
        
        // مسجل الصوت
        const recordBtn = document.getElementById('recordBtn');
        const stopBtn = document.getElementById('stopBtn');
        const deleteBtn = document.getElementById('deleteBtn');
        const timer = document.getElementById('timer');
        const visualizer = document.getElementById('visualizer');
        const audioPlayback = document.getElementById('audioPlayback');
        
        let mediaRecorder;
        let audioChunks = [];
        let recording = false;
        let seconds = 0;
        let timerInterval;
        const maxDuration = 60; // أقصى مدة للتسجيل بالثواني
        
        // بدء التسجيل
        recordBtn.addEventListener('click', async () => {
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
                mediaRecorder = new MediaRecorder(stream);
                
                mediaRecorder.ondataavailable = (e) => {
                    audioChunks.push(e.data);
                };
                
                mediaRecorder.onstop = () => {
                    const audioBlob = new Blob(audioChunks, { type: 'audio/webm' });
                    const audioUrl = URL.createObjectURL(audioBlob);
                    audioPlayback.src = audioUrl;
                    audioPlayback.style.display = 'block';
                    deleteBtn.disabled = false;
                };
                
                mediaRecorder.start();
                recording = true;
                recordBtn.disabled = true;
                stopBtn.disabled = false;
                visualizer.style.display = 'flex';
                
                // تشغيل المؤقت
                seconds = 0;
                timerInterval = setInterval(() => {
                    seconds++;
                    const mins = Math.floor(seconds / 60);
                    const secs = seconds % 60;
                    timer.textContent = `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
                    
                    // إيقاف التسجيل تلقائياً عند الوصول للحد الأقصى
                    if (seconds >= maxDuration) {
                        stopRecording();
                    }
                }, 1000);
            } catch (err) {
                alert('تعذر الوصول إلى الميكروفون. يرجى التحقق من الإعدادات.');
                console.error('Microphone access error:', err);
            }
        });
        
        // إيقاف التسجيل
        stopBtn.addEventListener('click', stopRecording);
        
        function stopRecording() {
            if (mediaRecorder && recording) {
                mediaRecorder.stop();
                recording = false;
                clearInterval(timerInterval);
                recordBtn.disabled = false;
                stopBtn.disabled = true;
                visualizer.style.display = 'none';
            }
        }
        
        // حذف التسجيل
        deleteBtn.addEventListener('click', () => {
            audioPlayback.src = '';
            audioPlayback.style.display = 'none';
            deleteBtn.disabled = true;
            audioChunks = [];
        });
        
        // إظهار/إخفاء كلمة المرور
        const passwordToggle = document.getElementById('passwordToggle');
        const passwordInput = document.getElementById('password');
        
        passwordToggle.addEventListener('click', () => {
            const type = passwordInput.getAttribute('type') === 'password' ? 'text' : 'password';
            passwordInput.setAttribute('type', type);
            passwordToggle.innerHTML = type === 'password' ? 
                '<i class="fas fa-eye"></i>' : 
                '<i class="fas fa-eye-slash"></i>';
        });
        
        // تخزين الطلبات
        let applications = JSON.parse(localStorage.getItem('workwise_applications')) || [];
        let currentApplicationId = null;

        // دالة محسنة لحفظ الطلبات
        function saveApplication(newApplication) {
            // تحميل الطلبات الحالية من localStorage
            const currentApplications = JSON.parse(localStorage.getItem('workwise_applications')) || [];
            
            // إضافة الطلب الجديد
            currentApplications.push(newApplication);
            
            // حفظ الطلبات المحدثة
            localStorage.setItem('workwise_applications', JSON.stringify(currentApplications));
            
            // تحديث المتغير العام
            applications = currentApplications;
        }

        // إرسال الطلب
        const applicationForm = document.querySelector('.application-form');
        applicationForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            // التحقق من وجود تسجيل صوتي
            if (!audioPlayback.src) {
                alert('الرجاء إضافة تسجيل صوتي قبل الإرسال');
                return;
            }
            
            // جمع بيانات الطلب
            const fullName = document.getElementById('fullName').value;
            const phone = document.getElementById('phoneNumber').value;
            const email = document.getElementById('email').value || 'لا يوجد';
            const job = document.getElementById('jobPosition').value;
            const company = document.getElementById('jobCompany').value;
            const notes = document.getElementById('notes').value || 'لا يوجد ملاحظات';
            
            // إنشاء طلب جديد
            const newApplication = {
                id: Date.now(),
                fullName,
                phone,
                email,
                job,
                company,
                notes,
                date: new Date().toLocaleDateString('ar-EG'),
                status: 'pending',
                audioUrl: audioPlayback.src
            };
            
            // حفظ الطلب باستخدام الدالة المحسنة
            saveApplication(newApplication);
            
            // عرض الإشعار
            notification.style.display = 'block';
            notification.textContent = 'تم إرسال طلبك بنجاح! سيتم مراجعة طلبك من قبل فريقنا.';
            
            setTimeout(() => {
                notification.style.display = 'none';
            }, 5000);
            
            // إعادة تعيين النموذج
            setTimeout(() => {
                applicationForm.reset();
                audioPlayback.style.display = 'none';
                timer.textContent = '00:00';
                seconds = 0;
                audioChunks = [];
                deleteBtn.disabled = true;
                showSection(homeSection);
            }, 3000);
        });
        
        // تسجيل دخول الموظفين
        document.getElementById('staffLogin').addEventListener('click', () => {
            const password = passwordInput.value;
            
            // كلمة المرور: workwise123456
            if (password === 'workwise123456') {
                // تحميل أحدث البيانات من localStorage
                applications = JSON.parse(localStorage.getItem('workwise_applications')) || [];
                
                showSection(dashboardSection);
                loadApplications();
                updateStats();
            } else {
                alert('كلمة المرور غير صحيحة. حاول مرة أخرى.');
            }
        });
        
        // تسجيل خروج الموظفين
        document.getElementById('logoutBtn').addEventListener('click', () => {
            if (confirm('هل أنت متأكد من تسجيل الخروج من لوحة التحكم؟')) {
                showSection(homeSection);
            }
        });
        
        // تحديث الإحصائيات
        function updateStats() {
            document.getElementById('totalApplicants').textContent = applications.length;
            
            const concentrix = applications.filter(app => 
                app.company.includes('Concentrix')).length;
            const hsbc = applications.filter(app => 
                app.company === 'HSBC').length;
            const volumex = applications.filter(app => 
                app.company === 'Volume X').length;
            const realEstate = applications.filter(app => 
                app.job.includes('عقارية')).length;
            
            document.getElementById('concentrixApplicants').textContent = concentrix;
            document.getElementById('hsbcApplicants').textContent = hsbc;
            document.getElementById('volumexApplicants').textContent = volumex;
            document.getElementById('realEstateApplicants').textContent = realEstate;
        }
        
        // تصفية الشركات
        const filterOptions = document.querySelectorAll('.filter-option');
        filterOptions.forEach(option => {
            option.addEventListener('click', () => {
                filterOptions.forEach(opt => opt.classList.remove('active'));
                option.classList.add('active');
                
                const company = option.getAttribute('data-company');
                loadApplications(company);
            });
        });
        
        // إغلاق تفاصيل المتقدم
        const applicantDetail = document.getElementById('applicantDetail');
        const closeDetail = document.getElementById('closeDetail');
        
        closeDetail.addEventListener('click', () => {
            applicantDetail.style.display = 'none';
        });
        
        // بحث المتقدمين
        const searchInput = document.getElementById('searchInput');
        searchInput.addEventListener('input', function() {
            const searchTerm = this.value.toLowerCase();
            const rows = document.querySelectorAll('#applicantsTableBody tr');
            
            rows.forEach(row => {
                const name = row.querySelector('.applicant-name span').textContent.toLowerCase();
                const job = row.querySelector('td:nth-child(2)').textContent.toLowerCase();
                
                if (name.includes(searchTerm) || job.includes(searchTerm)) {
                    row.style.display = '';
                } else {
                    row.style.display = 'none';
                }
            });
        });
        
        // تحميل المتقدمين
        function loadApplications(company = 'all') {
            const applicantsTableBody = document.getElementById('applicantsTableBody');
            applicantsTableBody.innerHTML = '';
            
            let filteredApplications = applications;
            if (company !== 'all') {
                filteredApplications = applications.filter(app => 
                    app.company.includes(company) || 
                    app.company.includes('المعادي') || 
                    app.company.includes('6 أكتوبر')
                );
            }
            
            filteredApplications.forEach(app => {
                const row = document.createElement('tr');
                
                // صورة عشوائية للمتقدم
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
                    <td><span class="status ${app.status}">${getStatusText(app.status)}</span></td>
                    <td>${app.date}</td>
                    <td><button class="action-btn view-btn" data-id="${app.id}"><i class="fas fa-eye"></i> عرض</button></td>
                `;
                
                applicantsTableBody.appendChild(row);
                
                // عرض تفاصيل المتقدم عند النقر
                row.querySelector('.view-btn').addEventListener('click', () => {
                    showApplicationDetails(app);
                });
            });
        }
        
        function getStatusText(status) {
            switch(status) {
                case 'pending': return 'قيد المراجعة';
                case 'reviewed': return 'تمت المراجعة';
                case 'accepted': return 'مقبول';
                case 'rejected': return 'مرفوض';
                default: return status;
            }
        }
        
        function showApplicationDetails(application) {
            document.getElementById('detail-fullName').textContent = application.fullName;
            document.getElementById('detail-phone').textContent = application.phone;
            document.getElementById('detail-email').textContent = application.email || 'لا يوجد';
            document.getElementById('detail-job').textContent = application.job;
            document.getElementById('detail-company').textContent = application.company;
            document.getElementById('detail-date').textContent = application.date;
            document.getElementById('detail-status').innerHTML = `<span class="status ${application.status}">${getStatusText(application.status)}</span>`;
            document.getElementById('detail-notes').textContent = application.notes;
            
            if (application.audioUrl) {
                document.getElementById('detail-audio').src = application.audioUrl;
            } else {
                document.getElementById('detail-audio').src = '#';
            }
            
            applicantDetail.style.display = 'block';
            currentApplicationId = application.id;
            
            // التمرير إلى قسم التفاصيل
            applicantDetail.scrollIntoView({ behavior: 'smooth' });
        }
        
        // قبول أو رفض المتقدم
        document.getElementById('acceptBtn').addEventListener('click', () => {
            updateApplicationStatus('accepted');
        });
        
        document.getElementById('rejectBtn').addEventListener('click', () => {
            updateApplicationStatus('rejected');
        });
        
        function updateApplicationStatus(status) {
            if (!currentApplicationId) return;
            
            const index = applications.findIndex(app => app.id === currentApplicationId);
            if (index !== -1) {
                applications[index].status = status;
                localStorage.setItem('workwise_applications', JSON.stringify(applications));
                
                // تحديث الواجهة
                document.getElementById('detail-status').innerHTML = `<span class="status ${status}">${getStatusText(status)}</span>`;
                
                // تحديث الجدول والإحصائيات
                const currentCompany = document.querySelector('.filter-option.active').getAttribute('data-company');
                loadApplications(currentCompany);
                updateStats();
                
                alert(`تم تحديث حالة المتقدم إلى: ${getStatusText(status)}`);
            }
        }
        
        // تهيئة الصفحة
        document.addEventListener('DOMContentLoaded', () => {
            showSection(homeSection);
        });
    </script>
</body>
</html>
