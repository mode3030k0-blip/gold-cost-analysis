
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kingdom Age Calculator - KingShot</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #ff2d55;
            --secondary: #00c7ff;
            --dark: #0a0a14;
            --darker: #05050a;
            --light: #f0f0f0;
            --accent: #ffcc00;
            --success: #34c759;
            --warning: #ff9500;
            --danger: #ff3b30;
            --neon-glow: 0 0 10px rgba(255, 45, 85, 0.7), 0 0 20px rgba(255, 45, 85, 0.5);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
        }

        body {
            background: linear-gradient(135deg, var(--darker) 0%, var(--dark) 100%);
            color: var(--light);
            min-height: 100vh;
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* تصميم شريط التحميل Red Magic Style */
        .loading-bar {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            transform: scaleX(0);
            transform-origin: left;
            z-index: 9999;
            transition: transform 0.3s ease;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        /* الهيدر الرئيسي */
        .main-header {
            text-align: center;
            padding: 30px 20px;
            margin-bottom: 40px;
            position: relative;
            overflow: hidden;
        }

        .main-header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 1px;
            background: linear-gradient(90deg, transparent, var(--primary), transparent);
        }

        .main-header h1 {
            font-size: 3.5rem;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 15px;
            text-shadow: var(--neon-glow);
            letter-spacing: -1px;
        }

        .main-header .subtitle {
            font-size: 1.2rem;
            color: #aaa;
            max-width: 600px;
            margin: 0 auto;
        }

        /* كرت الآلة الحاسبة */
        .calculator-card {
            background: rgba(20, 20, 30, 0.9);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 40px;
            border: 1px solid rgba(255, 45, 85, 0.3);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(10px);
            position: relative;
            overflow: hidden;
        }

        .calculator-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
        }

        .input-group {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .input-field {
            position: relative;
        }

        .input-field label {
            display: block;
            margin-bottom: 10px;
            color: var(--secondary);
            font-weight: 600;
            font-size: 1.1rem;
        }

        .date-input {
            width: 100%;
            padding: 18px 20px;
            background: rgba(10, 10, 20, 0.8);
            border: 2px solid rgba(255, 45, 85, 0.5);
            border-radius: 12px;
            color: var(--light);
            font-size: 1.1rem;
            transition: all 0.3s ease;
        }

        .date-input:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 20px rgba(255, 45, 85, 0.3);
        }

        .calculate-btn {
            background: linear-gradient(45deg, var(--primary), #ff3366);
            color: white;
            border: none;
            padding: 18px 40px;
            font-size: 1.2rem;
            font-weight: 700;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin: 0 auto;
            box-shadow: 0 5px 15px rgba(255, 45, 85, 0.4);
        }

        .calculate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(255, 45, 85, 0.6);
        }

        .calculate-btn:active {
            transform: translateY(-1px);
        }

        /* عرض النتيجة */
        .result-display {
            background: rgba(10, 10, 20, 0.9);
            border-radius: 15px;
            padding: 30px;
            margin-top: 30px;
            border: 1px solid rgba(0, 199, 255, 0.3);
            display: none;
            animation: slideUp 0.5s ease;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .kingdom-age {
            text-align: center;
            margin-bottom: 30px;
        }

        .age-number {
            font-size: 4rem;
            font-weight: 900;
            background: linear-gradient(45deg, var(--accent), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            line-height: 1;
            margin: 10px 0;
        }

        .age-label {
            font-size: 1.5rem;
            color: #aaa;
        }

        .age-details {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .detail-card {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 12px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .detail-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--secondary);
            margin-bottom: 5px;
        }

        .detail-label {
            color: #aaa;
            font-size: 0.9rem;
        }

        /* جدول الأحداث */
        .timeline-section {
            margin-top: 50px;
        }

        .section-title {
            font-size: 2rem;
            margin-bottom: 30px;
            color: var(--light);
            text-align: center;
            position: relative;
            padding-bottom: 15px;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--primary), transparent);
        }

        .events-timeline {
            display: grid;
            gap: 20px;
        }

        .event-card {
            background: rgba(20, 20, 30, 0.8);
            border-radius: 15px;
            padding: 25px;
            border-left: 5px solid;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .event-card:hover {
            transform: translateX(-10px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
        }

        .event-card.past {
            border-left-color: var(--success);
            opacity: 0.9;
        }

        .event-card.present {
            border-left-color: var(--primary);
            border-left-width: 8px;
            box-shadow: 0 0 20px rgba(255, 45, 85, 0.2);
        }

        .event-card.future {
            border-left-color: var(--secondary);
            opacity: 0.7;
        }

        .event-header {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
            gap: 15px;
        }

        .event-day {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white;
            width: 60px;
            height: 60px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: 900;
            flex-shrink: 0;
        }

        .event-title {
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--light);
        }

        .event-description {
            color: #ccc;
            margin-top: 10px;
            line-height: 1.6;
        }

        .event-status {
            position: absolute;
            top: 20px;
            left: 20px;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 700;
            text-transform: uppercase;
        }

        .past .event-status {
            background: rgba(52, 199, 89, 0.2);
            color: var(--success);
        }

        .present .event-status {
            background: rgba(255, 45, 85, 0.2);
            color: var(--primary);
        }

        .future .event-status {
            background: rgba(0, 199, 255, 0.2);
            color: var(--secondary);
        }

        /* فلاتر الأحداث */
        .event-filters {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .filter-btn {
            padding: 12px 25px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: white;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
        }

        .filter-btn:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        .filter-btn.active {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            border-color: transparent;
        }

        /* تصميم للهواتف */
        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }

            .main-header h1 {
                font-size: 2.5rem;
            }

            .input-group {
                grid-template-columns: 1fr;
            }

            .age-number {
                font-size: 3rem;
            }

            .event-card {
                padding: 20px;
            }

            .event-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }

            .event-day {
                width: 50px;
                height: 50px;
                font-size: 1.2rem;
            }

            .event-title {
                font-size: 1.2rem;
            }

            .event-filters {
                gap: 10px;
            }

            .filter-btn {
                padding: 10px 20px;
                font-size: 0.9rem;
            }
        }

        @media (max-width: 480px) {
            .main-header h1 {
                font-size: 2rem;
            }

            .age-number {
                font-size: 2.5rem;
            }

            .calculate-btn {
                width: 100%;
                padding: 16px;
            }

            .event-card {
                padding: 15px;
            }
        }

        /* تأثيرات إضافية */
        .neon-text {
            text-shadow: 0 0 10px currentColor;
        }

        .pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.7; }
            100% { opacity: 1; }
        }

        /* شريط التقدم */
        .progress-container {
            width: 100%;
            height: 6px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 3px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            width: 0%;
            border-radius: 3px;
            transition: width 0.5s ease;
        }

        /* كود التنبيهات */
        .notification {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: rgba(20, 20, 30, 0.95);
            padding: 15px 25px;
            border-radius: 10px;
            border-left: 5px solid var(--primary);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            transform: translateX(150%);
            transition: transform 0.3s ease;
            z-index: 1000;
            max-width: 300px;
        }

        .notification.show {
            transform: translateX(0);
        }

        /* زر العودة للأعلى */
        .scroll-top {
            position: fixed;
            bottom: 30px;
            left: 30px;
            width: 50px;
            height: 50px;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
            z-index: 999;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        .scroll-top.show {
            opacity: 1;
            visibility: visible;
        }
    </style>
</head>
<body>
    <!-- شريط التحميل -->
    <div class="loading-bar" id="loadingBar"></div>

    <!-- زر العودة للأعلى -->
    <div class="scroll-top" id="scrollTop">
        <i class="fas fa-chevron-up"></i>
    </div>

    <!-- تنبيه -->
    <div class="notification" id="notification"></div>

    <div class="container">
        <!-- الهيدر الرئيسي -->
        <header class="main-header">
            <h1 class="neon-text">KINGSHOT</h1>
            <p class="subtitle">حاسبة عمر المملكة | تتبع الأحداث التاريخية والاستراتيجية لمملكتك</p>
        </header>

        <!-- الآلة الحاسبة -->
        <section class="calculator-card">
            <h2 style="color: var(--secondary); margin-bottom: 25px; font-size: 1.8rem;">
                <i class="fas fa-calculator"></i> حساب عمر المملكة
            </h2>
            
            <div class="input-group">
                <div class="input-field">
                    <label for="startDate"><i class="fas fa-calendar-plus"></i> تاريخ بداية المملكة</label>
                    <input type="date" id="startDate" class="date-input" value="2025-01-21">
                </div>
                
                <div class="input-field">
                    <label for="currentDate"><i class="fas fa-calendar-day"></i> التاريخ الحالي (اختياري)</label>
                    <input type="date" id="currentDate" class="date-input">
                </div>
            </div>

            <button class="calculate-btn" id="calculateBtn">
                <i class="fas fa-crown"></i> حساب عمر المملكة
            </button>

            <!-- عرض النتيجة -->
            <div class="result-display" id="resultDisplay">
                <div class="kingdom-age">
                    <div class="age-label">عمر مملكتك</div>
                    <div class="age-number" id="ageDays">0</div>
                    <div class="age-label">يوم</div>
                </div>

                <!-- شريط التقدم -->
                <div class="progress-container">
                    <div class="progress-bar" id="progressBar"></div>
                </div>

                <div class="age-details">
                    <div class="detail-card">
                        <div class="detail-value" id="ageYears">0</div>
                        <div class="detail-label">سنوات</div>
                    </div>
                    <div class="detail-card">
                        <div class="detail-value" id="ageMonths">0</div>
                        <div class="detail-label">أشهر</div>
                    </div>
                    <div class="detail-card">
                        <div class="detail-value" id="ageWeeks">0</div>
                        <div class="detail-label">أسابيع</div>
                    </div>
                    <div class="detail-card">
                        <div class="detail-value" id="completion">0%</div>
                        <div class="detail-label">إكمال الجدول الزمني</div>
                    </div>
                </div>
            </div>
        </section>

        <!-- جدول الأحداث -->
        <section class="timeline-section">
            <h2 class="section-title">الجدول الزمني للأحداث</h2>
            
            <!-- فلاتر الأحداث -->
            <div class="event-filters">
                <button class="filter-btn active" data-filter="all">جميع الأحداث</button>
                <button class="filter-btn" data-filter="past">الأحداث الماضية</button>
                <button class="filter-btn" data-filter="present">الأحدث الحالية</button>
                <button class="filter-btn" data-filter="future">الأحداث القادمة</button>
            </div>

            <!-- قائمة الأحداث -->
            <div class="events-timeline" id="eventsTimeline">
                <!-- سيتم تعبئة الأحداث هنا عبر JavaScript -->
            </div>
        </section>
    </div>

    <script>
        // بيانات الأحداث
        const timelineEvents = [
            { day: 1, title: "أبطال الجيل الأول", description: "بداية رحلتك مع أول مجموعة من الأبطال", category: "hero" },
            { day: 14, title: "ارتفاع الضباب عن السهول", description: "تتكشف السهول لتصبح صالحة للبناء والتوسع", category: "terrain" },
            { day: 38, title: "ارتفاع الضباب عن الأراضي الخصبة", description: "أراضي زراعية خصبة تصبح متاحة للمملكة", category: "terrain" },
            { day: 40, title: "أبطال الجيل الثاني", description: "جيل جديد من الأبطال الأقوى ينضم للمملكة", category: "hero" },
            { day: 45, title: "تبادل الموارد بين الحلفاء", description: "فتح أنظمة التجارة والتعاون بين الممالك", category: "alliance" },
            { day: 54, title: "المعركة الأولى للقلعة", description: "اختبار دفاعاتك في أول معركة حقيقية", category: "battle" },
            { day: 55, title: "الحيوانات الأليفة الجيل الأول", description: "الذئاب الرمادية، الوشق، الثيران", category: "animal" },
            { day: 70, title: "الذهب الحقيقي من المستوى 1 إلى 3", description: "تحسين الاقتصاد والإنتاج", category: "economy" },
            { day: 75, title: "حيوانات الجيل الثاني الأليفة", description: "رفاق أقوى للمعارك والمهام", category: "animal" },
            { day: 80, title: "أهلية مملكة القوة/أقوى حاكم", description: "تصبح مؤهلاً للمنافسة على لقب أقوى حاكم", category: "rank" },
            { day: 110, title: "حيوانات الجيل الثالث الأليفة", description: "الأسود والدببة الرمادية", category: "animal" },
            { day: 120, title: "أبطال الجيل الثالث", description: "أبطال ذوو مهارات متخصصة", category: "hero" },
            { day: 143, title: "حيوانات الجيل الثالث الكاملة", description: "اكتمال مجموعة الحيوانات المتقدمة", category: "animal" },
            { day: 150, title: "الذهب مستوى 4-5", description: "قفزة اقتصادية كبيرة", category: "economy" },
            { day: 180, title: "معدات الحاكم T3-3", description: "معدات متقدمة لتعزيز قدرات الحاكم", category: "gear" },
            { day: 195, title: "أبطال الجيل الرابع", description: "أبطال أسطوريون بقدرات فريدة", category: "hero" },
            { day: 200, title: "حيوانات الجيل الرابع والخامس", description: "مخلوقات أسطورية وغريبة", category: "animal" },
            { day: 220, title: "فتح أكاديمية جنود T11", description: "جنود النخبة الأقوى يصبحون متاحين", category: "military" },
            { day: 270, title: "أبطال الجيل الخامس", description: "أبطال بمستوى السادة ذوو مهارات قتالية لا مثيل لها", category: "hero" },
            { day: 280, title: "حيوانات الجيل السادس والسابع", description: "مخلوقات قديمة ونادرة", category: "animal" },
            { day: 315, title: "الذهب مستوى 6-7-8", description: "ثروة هائلة لتوسيع المملكة", category: "economy" },
            { day: 360, title: "أبطال الجيل السادس", description: "أبطال سماويون بقدرات إلهية", category: "hero" },
            { day: 370, title: "حيوانات الجيل الثامن", description: "وحوش أسطورية من الأساطير", category: "animal" },
            { day: 440, title: "أبطال الجيل السابع", description: "أبطال شبيهة بالآلهة بقدرات تغيير مصير الحروب", category: "hero" },
            { day: 500, title: "الذهب مستوى 9-10", description: "ذروة الإنجاز الاقتصادي - موارد غير محدودة", category: "economy" },
            { day: 520, title: "أبطال الجيل الثامن", description: "أبطال أسطوريون من النبوءات القديمة", category: "hero" },
            { day: 600, title: "أبطال الجيل التاسع", description: "أبطال متعالون أتقنوا جميع أشكال القتال والاستراتيجية", category: "hero" },
            { day: 700, title: "أبطال الجيل العاشر", description: "الأبطال النهائيون - كائنات من القوة والحكمة الخالصة", category: "hero" }
        ];

        // عناصر DOM
        const startDateInput = document.getElementById('startDate');
        const currentDateInput = document.getElementById('currentDate');
        const calculateBtn = document.getElementById('calculateBtn');
        const resultDisplay = document.getElementById('resultDisplay');
        const ageDaysElement = document.getElementById('ageDays');
        const ageYearsElement = document.getElementById('ageYears');
        const ageMonthsElement = document.getElementById('ageMonths');
        const ageWeeksElement = document.getElementById('ageWeeks');
        const completionElement = document.getElementById('completion');
        const progressBar = document.getElementById('progressBar');
        const eventsTimeline = document.getElementById('eventsTimeline');
        const filterButtons = document.querySelectorAll('.filter-btn');
        const loadingBar = document.getElementById('loadingBar');
        const notification = document.getElementById('notification');
        const scrollTopBtn = document.getElementById('scrollTop');

        // تعيين التاريخ الحالي افتراضيًا
        function setCurrentDate() {
            const today = new Date();
            const formattedDate = today.toISOString().split('T')[0];
            currentDateInput.value = formattedDate;
        }

        // حساب الفرق بين تاريخين بالأيام
        function calculateDateDifference(startDate, endDate) {
            const start = new Date(startDate);
            const end = new Date(endDate);
            const differenceMs = end - start;
            return Math.floor(differenceMs / (1000 * 60 * 60 * 24));
        }

        // تنسيق الأرقام
        function formatNumber(num) {
            return num.toLocaleString('ar-EG');
        }

        // إظهار الإشعار
        function showNotification(message, type = 'info') {
            notification.textContent = message;
            notification.style.borderLeftColor = getNotificationColor(type);
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // الحصول على لون الإشعار حسب النوع
        function getNotificationColor(type) {
            const colors = {
                'info': 'var(--secondary)',
                'success': 'var(--success)',
                'warning': 'var(--warning)',
                'error': 'var(--danger)'
            };
            return colors[type] || colors.info;
        }

        // تحديث شريط التحميل
        function updateLoadingBar(progress) {
            loadingBar.style.transform = `scaleX(${progress})`;
        }

        // إنشاء بطاقة الحدث
        function createEventCard(event, kingdomAge) {
            const isPast = kingdomAge >= event.day;
            const isPresent = kingdomAge === event.day;
            const isFuture = kingdomAge < event.day;
            
            let statusClass = 'future';
            let statusText = 'قادم';
            
            if (isPast && !isPresent) {
                statusClass = 'past';
                statusText = 'مكتمل';
            } else if (isPresent) {
                statusClass = 'present';
                statusText = 'جاري الآن';
            }
            
            const card = document.createElement('div');
            card.className = `event-card ${statusClass}`;
            card.dataset.category = event.category;
            card.dataset.day = event.day;
            
            card.innerHTML = `
                <div class="event-status">${statusText}</div>
                <div class="event-header">
                    <div class="event-day">${event.day}</div>
                    <div>
                        <h3 class="event-title">${event.title}</h3>
                        <p class="event-description">${event.description}</p>
                    </div>
                </div>
            `;
            
            return card;
        }

        // تحديث الجدول الزمني
        function updateTimeline(kingdomAge) {
            eventsTimeline.innerHTML = '';
            
            // ترتيب الأحداث حسب اليوم
            const sortedEvents = [...timelineEvents].sort((a, b) => a.day - b.day);
            
            sortedEvents.forEach(event => {
                const eventCard = createEventCard(event, kingdomAge);
                eventsTimeline.appendChild(eventCard);
            });
            
            // تحديث نسبة الإكمال
            const totalEvents = timelineEvents.length;
            const completedEvents = timelineEvents.filter(e => kingdomAge >= e.day).length;
            const completionPercentage = Math.round((completedEvents / totalEvents) * 100);
            
            completionElement.textContent = `${completionPercentage}%`;
            progressBar.style.width = `${completionPercentage}%`;
        }

        // تصفية الأحداث
        function filterEvents(filter) {
            const allEvents = document.querySelectorAll('.event-card');
            
            allEvents.forEach(event => {
                if (filter === 'all') {
                    event.style.display = 'block';
                } else if (filter === 'past') {
                    event.style.display = event.classList.contains('past') ? 'block' : 'none';
                } else if (filter === 'present') {
                    event.style.display = event.classList.contains('present') ? 'block' : 'none';
                } else if (filter === 'future') {
                    event.style.display = event.classList.contains('future') ? 'block' : 'none';
                }
            });
        }

        // حساب عمر المملكة
        function calculateKingdomAge() {
            updateLoadingBar(0.3);
            
            const startDate = startDateInput.value;
            const currentDate = currentDateInput.value || new Date().toISOString().split('T')[0];
            
            if (!startDate) {
                showNotification('الرجاء اختيار تاريخ بداية المملكة', 'error');
                updateLoadingBar(0);
                return;
            }
            
            const kingdomAge = calculateDateDifference(startDate, currentDate);
            
            if (kingdomAge < 0) {
                showNotification('تاريخ البداية يجب أن يكون قبل التاريخ الحالي', 'error');
                updateLoadingBar(0);
                return;
            }
            
            // تحديث النتائج
            ageDaysElement.textContent = formatNumber(kingdomAge);
            ageYearsElement.textContent = formatNumber(Math.floor(kingdomAge / 365));
            ageMonthsElement.textContent = formatNumber(Math.floor(kingdomAge / 30));
            ageWeeksElement.textContent = formatNumber(Math.floor(kingdomAge / 7));
            
            // إظهار النتائج
            resultDisplay.style.display = 'block';
            
            // تحديث الجدول الزمني
            updateTimeline(kingdomAge);
            
            // إظهار الإشعار
            showNotification(`تم حساب عمر المملكة بنجاح: ${kingdomAge} يوم`, 'success');
            
            // إكمال شريط التحميل
            setTimeout(() => updateLoadingBar(1), 300);
            setTimeout(() => updateLoadingBar(0), 800);
            
            // التمرير إلى النتائج
            resultDisplay.scrollIntoView({ behavior: 'smooth' });
        }

        // تهيئة الصفحة
        function init() {
            // تعيين التاريخ الحالي
            setCurrentDate();
            
            // إضافة مستمعي الأحداث
            calculateBtn.addEventListener('click', calculateKingdomAge);
            
            // فلاتر الأحداث
            filterButtons.forEach(button => {
                button.addEventListener('click', function() {
                    filterButtons.forEach(btn => btn.classList.remove('active'));
                    this.classList.add('active');
                    filterEvents(this.dataset.filter);
                });
            });
            
            // زر العودة للأعلى
            window.addEventListener('scroll', () => {
                if (window.scrollY > 300) {
                    scrollTopBtn.classList.add('show');
                } else {
                    scrollTopBtn.classList.remove('show');
                }
            });
            
            scrollTopBtn.addEventListener('click', () => {
                window.scrollTo({ top: 0, behavior: 'smooth' });
            });
            
            // حساب تلقائي عند تحميل الصفحة
            setTimeout(() => {
                calculateKingdomAge();
            }, 1000);
            
            // تأثيرات عند التمرير
            const observerOptions = {
                threshold: 0.1,
                rootMargin: '0px 0px -50px 0px'
            };
            
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.style.opacity = '1';
                        entry.target.style.transform = 'translateY(0)';
                    }
                });
            }, observerOptions);
            
            // مراقبة الأحداث
            document.querySelectorAll('.event-card').forEach(card => {
                observer.observe(card);
            });
            
            // إضافة تأثيرات CSS للأحداث
            const style = document.createElement('style');
            style.textContent = `
                .event-card {
                    opacity: 0;
                    transform: translateX(20px);
                    transition: opacity 0.5s ease, transform 0.5s ease;
                }
                
                .event-card.visible {
                    opacity: 1;
                    transform: translateX(0);
                }
            `;
            document.head.appendChild(style);
        }

        // تشغيل التهيئة عند تحميل الصفحة
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
