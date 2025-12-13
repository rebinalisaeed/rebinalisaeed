<!DOCTYPE html>
<html lang="ku" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Xpay - داهاتووی پارەدان</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Tahoma', 'Geneva', 'Verdana', sans-serif;
        }
        
        :root {
            --mauve-primary: #8B5F8D;
            --mauve-light: #A67FA8;
            --mauve-dark: #6F4C70;
            --mauve-gradient: linear-gradient(135deg, #8B5F8D 0%, #A67FA8 50%, #6F4C70 100%);
            --glossy-effect: linear-gradient(145deg, rgba(255,255,255,0.3) 0%, rgba(255,255,255,0.1) 50%, rgba(0,0,0,0.1) 100%);
            --text-dark: #333333;
            --text-light: #666666;
            --border-color: #E0E0E0;
            --background: #F8F9FA;
        }
        
        body {
            background-color: var(--background);
            color: var(--text-dark);
            overflow-x: hidden;
        }
        
        /* سپلەش سکرین */
        #splash-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            background: var(--mauve-gradient);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            animation: fadeOut 0.8s ease-out 2.5s forwards;
        }
        
        .logo-animation {
            position: relative;
            width: 200px;
            height: 200px;
            margin-bottom: 30px;
        }
        
        .logo-circle {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            animation: pulse 2s infinite;
        }
        
        .logo-circle:nth-child(2) {
            animation-delay: 0.5s;
        }
        
        .logo-circle:nth-child(3) {
            animation-delay: 1s;
        }
        
        .logo-svg {
            position: absolute;
            width: 120px;
            height: 120px;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            filter: drop-shadow(0 5px 15px rgba(0, 0, 0, 0.2));
        }
        
        .app-name {
            color: white;
            font-size: 2.8rem;
            font-weight: 800;
            letter-spacing: 2px;
            text-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            margin-top: 20px;
        }
        
        /* پەڕەی سەرەکی */
        #main-content {
            display: none;
            opacity: 0;
            animation: fadeIn 0.5s ease-out 3s forwards;
        }
        
        .container {
            max-width: 450px;
            margin: 0 auto;
            padding: 20px;
        }
        
        /* سەرەوەی پەڕە */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-top: 10px;
        }
        
        .language-selector {
            position: relative;
            width: 150px;
        }
        
        .language-btn {
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
            padding: 10px 15px;
            background: white;
            border: 2px solid var(--border-color);
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            color: var(--text-dark);
            transition: all 0.3s;
        }
        
        .language-btn:hover {
            border-color: var(--mauve-light);
        }
        
        .language-list {
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            background: white;
            border-radius: 12px;
            border: 2px solid var(--border-color);
            margin-top: 5px;
            overflow: hidden;
            display: none;
            z-index: 100;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
        }
        
        .language-list.show {
            display: block;
        }
        
        .language-option {
            padding: 12px 15px;
            cursor: pointer;
            transition: all 0.2s;
            border-bottom: 1px solid #f0f0f0;
        }
        
        .language-option:last-child {
            border-bottom: none;
        }
        
        .language-option:hover {
            background-color: #f8f8f8;
            color: var(--mauve-primary);
        }
        
        /* ناوەڕاستی پەڕە */
        .logo-section {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .main-logo {
            width: 120px;
            height: 120px;
            margin: 0 auto 20px;
            background: var(--mauve-gradient);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(139, 95, 141, 0.3);
        }
        
        .main-logo::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: var(--glossy-effect);
            transform: rotate(30deg);
        }
        
        .main-logo svg {
            width: 70px;
            height: 70px;
            z-index: 2;
        }
        
        .welcome-text {
            font-size: 1.2rem;
            color: var(--text-light);
            line-height: 1.6;
            margin-bottom: 30px;
        }
        
        /* فۆرم */
        .form-container {
            background: white;
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.05);
            margin-bottom: 25px;
        }
        
        .input-group {
            margin-bottom: 25px;
        }
        
        .input-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--text-dark);
            font-size: 0.95rem;
        }
        
        .phone-input-container {
            display: flex;
            border: 2px solid var(--border-color);
            border-radius: 12px;
            overflow: hidden;
            transition: all 0.3s;
        }
        
        .phone-input-container:focus-within {
            border-color: var(--mauve-primary);
            box-shadow: 0 0 0 3px rgba(139, 95, 141, 0.1);
        }
        
        .country-code-select {
            padding: 15px;
            border: none;
            border-right: 2px solid var(--border-color);
            background: #f8f8f8;
            font-weight: 600;
            color: var(--text-dark);
            outline: none;
            min-width: 120px;
            cursor: pointer;
        }
        
        .phone-input {
            flex: 1;
            padding: 15px;
            border: none;
            outline: none;
            font-size: 1rem;
        }
        
        .password-input-container {
            position: relative;
        }
        
        .password-input {
            width: 100%;
            padding: 15px;
            border: 2px solid var(--border-color);
            border-radius: 12px;
            outline: none;
            font-size: 1rem;
            transition: all 0.3s;
        }
        
        .password-input:focus {
            border-color: var(--mauve-primary);
            box-shadow: 0 0 0 3px rgba(139, 95, 141, 0.1);
        }
        
        .toggle-password {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            color: var(--text-light);
            cursor: pointer;
        }
        
        /* بەستەری لەبیرچوونی پاسوۆرد */
        .forgot-password {
            text-align: left;
            margin-bottom: 25px;
        }
        
        .forgot-password a {
            color: var(--mauve-primary);
            text-decoration: none;
            font-weight: 600;
            font-size: 0.95rem;
            transition: all 0.3s;
        }
        
        .forgot-password a:hover {
            color: var(--mauve-dark);
            text-decoration: underline;
        }
        
        /* دووگمەکان */
        .buttons-container {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .btn {
            flex: 1;
            padding: 18px;
            border: none;
            border-radius: 12px;
            font-size: 1.05rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .btn-primary {
            background: var(--mauve-gradient);
            color: white;
            box-shadow: 0 5px 15px rgba(139, 95, 141, 0.3);
        }
        
        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(139, 95, 141, 0.4);
        }
        
        .btn-fast-login {
            background: white;
            color: var(--mauve-primary);
            border: 2px solid var(--mauve-light);
            max-width: 70px;
        }
        
        .btn-fast-login:hover {
            background: #f9f0fa;
        }
        
        /* بەستەری درووستکردنی هەژمار */
        .signup-link {
            text-align: center;
            padding-top: 20px;
            border-top: 1px solid var(--border-color);
        }
        
        .signup-link a {
            color: var(--mauve-primary);
            text-decoration: none;
            font-weight: 700;
            font-size: 1.05rem;
            transition: all 0.3s;
        }
        
        .signup-link a:hover {
            color: var(--mauve-dark);
            text-decoration: underline;
        }
        
        /* ئەنیمەیشنەکان */
        @keyframes pulse {
            0% {
                transform: scale(1);
                opacity: 1;
            }
            100% {
                transform: scale(1.5);
                opacity: 0;
            }
        }
        
        @keyframes fadeOut {
            0% {
                opacity: 1;
                visibility: visible;
            }
            100% {
                opacity: 0;
                visibility: hidden;
            }
        }
        
        @keyframes fadeIn {
            0% {
                opacity: 0;
            }
            100% {
                opacity: 1;
            }
        }
        
        /* وەڵامدانەوەیی */
        @media (max-width: 480px) {
            .container {
                padding: 15px;
            }
            
            .buttons-container {
                flex-direction: column;
            }
            
            .btn-fast-login {
                max-width: 100%;
                padding: 15px;
            }
            
            .app-name {
                font-size: 2.2rem;
            }
        }
    </style>
</head>
<body>
    <!-- سپلەش سکرین -->
    <div id="splash-screen">
        <div class="logo-animation">
            <div class="logo-circle"></div>
            <div class="logo-circle"></div>
            <div class="logo-circle"></div>
            <div class="logo-svg">
                <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
                    <circle cx="100" cy="100" r="90" fill="#FFFFFF"/>
                    <path d="M60,60 L140,140 M140,60 L60,140" stroke="#8B5F8D" stroke-width="20" stroke-linecap="round"/>
                    <circle cx="100" cy="100" r="80" fill="none" stroke="#8B5F8D" stroke-width="8"/>
                    <circle cx="100" cy="100" r="50" fill="none" stroke="#8B5F8D" stroke-width="5"/>
                </svg>
            </div>
        </div>
        <h1 class="app-name">Xpay</h1>
    </div>
    
    <!-- پەڕەی سەرەکی -->
    <div id="main-content">
        <div class="container">
            <!-- سەرەوە: زمانەکان -->
            <div class="header">
                <div class="language-selector">
                    <button class="language-btn" id="languageBtn">
                        <span id="selectedLanguage">کوردی سۆرانی</span>
                        <i class="fas fa-chevron-down"></i>
                    </button>
                    <div class="language-list" id="languageList">
                        <div class="language-option" data-lang="ckb">کوردی سۆرانی</div>
                        <div class="language-option" data-lang="ckb-bad">کوردی بادینی</div>
                        <div class="language-option" data-lang="ar">عربي</div>
                        <div class="language-option" data-lang="en">English</div>
                        <div class="language-option" data-lang="fa">فارسی</div>
                        <div class="language-option" data-lang="tr">تورکی</div>
                    </div>
                </div>
            </div>
            
            <!-- ناوەڕاست: لۆگۆ و دەربارە -->
            <div class="logo-section">
                <div class="main-logo">
                    <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
                        <circle cx="100" cy="100" r="90" fill="#FFFFFF"/>
                        <path d="M60,60 L140,140 M140,60 L60,140" stroke="#8B5F8D" stroke-width="20" stroke-linecap="round"/>
                        <circle cx="100" cy="100" r="80" fill="none" stroke="#8B5F8D" stroke-width="8"/>
                        <circle cx="100" cy="100" r="50" fill="none" stroke="#8B5F8D" stroke-width="5"/>
                    </svg>
                </div>
                <p class="welcome-text">بەکارهێنەری بەڕێز چوونەژوورەوە ئەنجام بدە تا خزمەت گوزاریەکان ببینی</p>
            </div>
            
            <!-- فۆرمی چوونەژوورەوە -->
            <div class="form-container">
                <!-- ژمارەی تەلەفۆن -->
                <div class="input-group">
                    <label class="input-label">ژمارەی مۆبایل</label>
                    <div class="phone-input-container">
                        <select class="country-code-select" id="countryCode">
                            <option value="+964">عێراق +964</option>
                            <option value="+98">ئێران +98</option>
                            <option value="+90">تورکیا +90</option>
                            <option value="+963">سوریا +963</option>
                            <option value="+966">سعودیا +966</option>
                            <option value="+962">ئوردن +962</option>
                            <option value="+965">کوەیت +965</option>
                            <option value="+961">لوبنان +961</option>
                            <option value="+971">ئیمارات +971</option>
                        </select>
                        <input type="tel" class="phone-input" id="phoneNumber" placeholder="7701234567">
                    </div>
                </div>
                
                <!-- تێپەڕەوشە -->
                <div class="input-group">
                    <label class="input-label">تێپەڕەوشە</label>
                    <div class="password-input-container">
                        <input type="password" class="password-input" id="password" placeholder="••••••••">
                        <button class="toggle-password" id="togglePassword">
                            <i class="far fa-eye"></i>
                        </button>
                    </div>
                </div>
                
                <!-- لەبیرچوونی پاسوۆرد -->
                <div class="forgot-password">
                    <a href="#" id="forgotPasswordLink">ئایا تۆ پاسوۆردەکەت بیرچۆتەوە؟</a>
                </div>
                
                <!-- دووگمەکانی چوونەژوورەوە -->
                <div class="buttons-container">
                    <button class="btn btn-primary" id="loginButton">
                        <i class="fas fa-sign-in-alt"></i>
                        چوونە ژوورەوە
                    </button>
                    <button class="btn btn-fast-login" id="fastLoginButton">
                        <i class="fas fa-fingerprint" id="fastLoginIcon"></i>
                    </button>
                </div>
            </div>
            
            <!-- بەستەری درووستکردنی هەژمار -->
            <div class="signup-link">
                <a href="#" id="signupLink">تۆ هەژمارت نیە؟ ئێستا خۆت تۆمار بکە</a>
            </div>
        </div>
    </div>
    
    <script>
        // دوای 2.5 چرکە سپلەش سکرین دەخرێتەوە
        window.addEventListener('load', function() {
            setTimeout(function() {
                document.getElementById('main-content').style.display = 'block';
            }, 2500);
        });
        
        // کۆنترۆڵکردنی لیستی زمانەکان
        document.getElementById('languageBtn').addEventListener('click', function() {
            document.getElementById('languageList').classList.toggle('show');
        });
        
        // دیاریکردنی زمان
        document.querySelectorAll('.language-option').forEach(option => {
            option.addEventListener('click', function() {
                const selectedLang = this.getAttribute('data-lang');
                const langText = this.textContent;
                
                document.getElementById('selectedLanguage').textContent = langText;
                document.getElementById('languageList').classList.remove('show');
                
                // لەم شوێنەدا دەتوانیت زمان بگۆڕیت
                console.log('زمان گۆڕدرا بۆ: ' + selectedLang);
            });
        });
        
        // کلیککردن لە دەرەوەی لیست بۆ داخستنی
        document.addEventListener('click', function(e) {
            if (!e.target.closest('.language-selector')) {
                document.getElementById('languageList').classList.remove('show');
            }
        });
        
        // نیشاندانی/شاردنەوەی تێپەڕەوشە
        document.getElementById('togglePassword').addEventListener('click', function() {
            const passwordInput = document.getElementById('password');
            const icon = this.querySelector('i');
            
            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                icon.classList.remove('fa-eye');
                icon.classList.add('fa-eye-slash');
            } else {
                passwordInput.type = 'password';
                icon.classList.remove('fa-eye-slash');
                icon.classList.add('fa-eye');
            }
        });
        
        // پشکنینی ئەگەری پەنجەمۆر یان دەنگۆی دەموچاو
        function checkBiometricSupport() {
            // لە کاتی ڕاستیدا پشکنین ڕاستەقینەیە
            // لەم نموونەدا تەنیا وادەزانین کە پەنجەمۆر بەردەستە
            return 'fingerprint';
        }
        
        // دەستکاریکردنی ئایکۆنی چوونەژوورەوەی خێرا
        window.addEventListener('load', function() {
            const biometricType = checkBiometricSupport();
            const fastLoginIcon = document.getElementById('fastLoginIcon');
            const fastLoginButton = document.getElementById('fastLoginButton');
            
            if (biometricType === 'fingerprint') {
                fastLoginIcon.className = 'fas fa-fingerprint';
                fastLoginButton.title = 'چوونەژوورەوە بە پەنجەمۆر';
            } else {
                fastLoginIcon.className = 'fas fa-face-smile';
                fastLoginButton.title = 'چوونەژوورەوە بە دەنگۆی دەموچاو';
            }
        });
        
        // کارکردنی دووگمەی چوونەژوورەوە
        document.getElementById('loginButton').addEventListener('click', function() {
            const countryCode = document.getElementById('countryCode').value;
            const phoneNumber = document.getElementById('phoneNumber').value;
            const password = document.getElementById('password').value;
            
            if (!phoneNumber || !password) {
                alert('تکایە هەموو خانەکان پڕ بکەرەوە!');
                return;
            }
            
            // لەم شوێنەدا دەتوانیت داتاکان بۆ سێرڤەر بنێریت
            console.log('چوونەژوورەوە بەژمارە:', countryCode + phoneNumber);
            alert('چوونەژوورەوە سەرکەوتوو بوو!');
        });
        
        // چوونەژوورەوەی خێرا
        document.getElementById('fastLoginButton').addEventListener('click', function() {
            const biometricType = checkBiometricSupport();
            
            if (biometricType === 'fingerprint') {
                alert('چوونەژوورەوەی خێرا بە پەنجەمۆر');
            } else {
                alert('چوونەژوورەوەی خێرا بە دەنگۆی دەموچاو');
            }
        });
        
        // بەستەری لەبیرچوونی پاسوۆرد
        document.getElementById('forgotPasswordLink').addEventListener('click', function(e) {
            e.preventDefault();
            alert('بەستەری گۆڕینی پاسوۆرد نێردرا بە ژمارەی تەلەفۆنەوە!');
        });
        
        // بەستەری درووستکردنی هەژمار
        document.getElementById('signupLink').addEventListener('click', function(e) {
            e.preventDefault();
            alert('بەستەری درووستکردنی هەژمار!');
        });
    </script>
</body>
</html>
