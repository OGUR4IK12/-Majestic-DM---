<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LaimeWorld | Система заявок</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0a0a14;
            color: #e0e0ff;
            min-height: 100vh;
            background-image: 
                radial-gradient(circle at 10% 10%, rgba(100, 0, 255, 0.15) 0%, transparent 20%),
                radial-gradient(circle at 90% 90%, rgba(255, 0, 150, 0.15) 0%, transparent 20%);
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .neon-text {
            color: #8a2be2;
            text-shadow:
                0 0 7px #8a2be2,
                0 0 10px #8a2be2,
                0 0 21px #8a2be2,
                0 0 42px #4b0082,
                0 0 82px #4b0082;
            font-weight: 800;
            letter-spacing: 1px;
        }

        .neon-purple {
            color: #9370db;
            text-shadow:
                0 0 5px #9370db,
                0 0 10px #8a2be2;
        }

        .neon-cyan {
            color: #00ced1;
            text-shadow:
                0 0 5px #00ced1,
                0 0 10px #008b8b;
        }

        /* Шапка */
        header {
            background: rgba(10, 10, 20, 0.95);
            border-bottom: 1px solid #4b0082;
            box-shadow: 0 4px 20px rgba(75, 0, 130, 0.3);
            backdrop-filter: blur(15px);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo h1 {
            font-size: 2.5rem;
            letter-spacing: 3px;
            text-transform: uppercase;
            font-weight: 900;
        }

        .logo-icon {
            font-size: 2.8rem;
            color: #8a2be2;
            filter: drop-shadow(0 0 8px #8a2be2);
        }

        /* Навигация */
        nav {
            display: flex;
            gap: 15px;
        }

        .nav-btn {
            background: rgba(30, 30, 60, 0.7);
            color: #b19cd9;
            border: 1px solid #6a0dad;
            padding: 12px 28px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            text-transform: uppercase;
            letter-spacing: 1px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .nav-btn:hover {
            background: rgba(75, 0, 130, 0.4);
            border-color: #9370db;
            box-shadow: 0 0 15px rgba(138, 43, 226, 0.4);
            transform: translateY(-2px);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4b0082 0%, #8a2be2 100%);
            color: white;
            border-color: #00ced1;
            box-shadow: 0 0 20px rgba(138, 43, 226, 0.6);
        }

        /* Основной контент */
        main {
            padding: 40px 0;
        }

        .page {
            display: none;
        }

        .page.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Карточки */
        .form-card {
            background: rgba(20, 15, 35, 0.85);
            border: 1px solid #4b0082;
            border-radius: 12px;
            padding: 40px;
            box-shadow: 
                0 10px 30px rgba(0, 0, 0, 0.4),
                inset 0 1px 0 rgba(255, 255, 255, 0.1);
            margin-bottom: 30px;
            backdrop-filter: blur(10px);
        }

        .form-title {
            font-size: 2rem;
            margin-bottom: 30px;
            text-align: center;
            color: #9370db;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        /* Форма */
        .form-group {
            margin-bottom: 25px;
        }

        .form-label {
            display: block;
            margin-bottom: 10px;
            color: #b19cd9;
            font-weight: 600;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .form-icon {
            color: #8a2be2;
            font-size: 1.3rem;
            min-width: 30px;
        }

        .form-input, .form-select, .form-textarea {
            width: 100%;
            padding: 14px 18px;
            background: rgba(40, 35, 60, 0.7);
            border: 1px solid #6a0dad;
            border-radius: 8px;
            color: #e0e0ff;
            font-size: 1rem;
            transition: all 0.3s ease;
            font-family: inherit;
        }

        .form-input:focus, .form-select:focus, .form-textarea:focus {
            outline: none;
            border-color: #00ced1;
            box-shadow: 0 0 0 2px rgba(0, 206, 209, 0.2);
            background: rgba(50, 45, 70, 0.9);
        }

        .form-textarea {
            min-height: 100px;
            resize: vertical;
            line-height: 1.5;
        }

        .optional {
            font-size: 0.9rem;
            color: #9370db;
            font-weight: normal;
            margin-left: 5px;
        }

        /* Кнопки */
        .btn {
            background: linear-gradient(135deg, #4b0082 0%, #8a2be2 100%);
            color: white;
            border: none;
            padding: 16px 40px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 700;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: inline-flex;
            align-items: center;
            gap: 12px;
            margin-top: 25px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(138, 43, 226, 0.5);
            background: linear-gradient(135deg, #5a00a3 0%, #9b30ff 100%);
        }

        /* Возрастной барьер */
        .age-warning {
            background: rgba(75, 0, 130, 0.2);
            border: 1px solid #8a2be2;
            border-radius: 8px;
            padding: 15px;
            margin: 15px 0;
            text-align: center;
            color: #b19cd9;
            font-weight: 600;
        }

        /* Скрытые вопросы для ролей */
        .role-specific-questions {
            display: none;
            margin-top: 20px;
            padding: 20px;
            background: rgba(30, 25, 45, 0.7);
            border-radius: 10px;
            border-left: 4px solid #8a2be2;
            animation: slideDown 0.3s ease;
        }

        .role-specific-questions.show {
            display: block;
        }

        @keyframes slideDown {
            from { opacity: 0; max-height: 0; }
            to { opacity: 1; max-height: 2000px; }
        }

        /* Страница проверки статуса */
        .check-status-card {
            background: rgba(20, 15, 35, 0.85);
            border: 1px solid #4b0082;
            border-radius: 12px;
            padding: 40px;
            margin-bottom: 30px;
            text-align: center;
        }

        .id-input-group {
            max-width: 400px;
            margin: 30px auto;
        }

        .id-display {
            font-size: 1.8rem;
            color: #8a2be2;
            background: rgba(40, 35, 60, 0.7);
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
            font-weight: 800;
            letter-spacing: 2px;
            border: 2px solid #6a0dad;
        }

        .copy-btn {
            background: rgba(40, 35, 60, 0.7);
            color: #9370db;
            border: 1px solid #6a0dad;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9rem;
            margin-left: 10px;
            transition: all 0.3s ease;
        }

        .copy-btn:hover {
            background: rgba(138, 43, 226, 0.3);
        }

        .result-card {
            margin-top: 30px;
            padding: 25px;
            border-radius: 10px;
            animation: fadeIn 0.5s ease;
            text-align: left;
        }

        .result-pending {
            background: rgba(255, 165, 0, 0.1);
            border: 1px solid rgba(255, 165, 0, 0.3);
        }

        .result-approved {
            background: rgba(0, 255, 0, 0.1);
            border: 1px solid rgba(0, 255, 0, 0.3);
        }

        .result-rejected {
            background: rgba(255, 0, 0, 0.1);
            border: 1px solid rgba(255, 0, 0, 0.3);
        }

        /* Админ-панель */
        .admin-card {
            background: rgba(20, 15, 35, 0.85);
            border: 1px solid #4b0082;
            border-radius: 12px;
            padding: 35px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
        }

        .application-card {
            background: rgba(40, 35, 60, 0.7);
            border: 1px solid #6a0dad;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
            transition: all 0.3s ease;
            border-left: 4px solid #8a2be2;
        }

        .application-card:hover {
            border-color: #9370db;
            transform: translateX(5px);
            box-shadow: 0 5px 15px rgba(138, 43, 226, 0.3);
        }

        .application-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 12px;
            border-bottom: 1px solid rgba(107, 13, 173, 0.3);
        }

        .application-info {
            flex: 1;
        }

        .application-position {
            color: #9370db;
            font-size: 1.3rem;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .application-user {
            color: #b19cd9;
            font-size: 1.1rem;
            margin-bottom: 5px;
        }

        .application-age {
            color: #00ced1;
            font-size: 1rem;
        }

        .application-status {
            padding: 8px 20px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-left: 15px;
        }

        .status-pending {
            background: rgba(255, 165, 0, 0.15);
            color: #ffa500;
            border: 1px solid rgba(255, 165, 0, 0.3);
        }

        .status-approved {
            background: rgba(0, 255, 0, 0.15);
            color: #00ff00;
            border: 1px solid rgba(0, 255, 0, 0.3);
        }

        .status-rejected {
            background: rgba(255, 0, 0, 0.15);
            color: #ff5555;
            border: 1px solid rgba(255, 0, 0, 0.3);
        }

        .admin-controls {
            display: flex;
            gap: 12px;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .btn-sm {
            padding: 10px 20px;
            font-size: 0.9rem;
            border-radius: 6px;
        }

        .btn-approve {
            background: linear-gradient(135deg, #008000 0%, #00aa00 100%);
        }

        .btn-reject {
            background: linear-gradient(135deg, #8b0000 0%, #cc0000 100%);
        }

        .btn-view {
            background: linear-gradient(135deg, #1e90ff 0%, #4169e1 100%);
        }

        .btn-delete {
            background: linear-gradient(135deg, #4b0082 0%, #6a0dad 100%);
        }

        .btn-contact {
            background: linear-gradient(135deg, #ff69b4 0%, #db7093 100%);
        }

        /* Статистика */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: rgba(40, 35, 60, 0.7);
            border: 1px solid #6a0dad;
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            transition: all 0.3s ease;
        }

        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(138, 43, 226, 0.3);
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 800;
            color: #8a2be2;
            margin-bottom: 10px;
        }

        /* Модальное окно */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            justify-content: center;
            align-items: center;
            z-index: 2000;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: rgba(20, 15, 35, 0.95);
            border: 2px solid #8a2be2;
            border-radius: 12px;
            padding: 40px;
            width: 90%;
            max-width: 450px;
            box-shadow: 0 0 60px rgba(138, 43, 226, 0.4);
        }

        .modal-title {
            color: #9370db;
            margin-bottom: 25px;
            text-align: center;
            font-size: 1.5rem;
            font-weight: 700;
        }

        /* Нотификации */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(20, 15, 35, 0.95);
            border: 1px solid #4b0082;
            border-left: 5px solid #00ced1;
            padding: 15px 25px;
            border-radius: 8px;
            box-shadow: 0 5px 25px rgba(0, 0, 0, 0.5);
            z-index: 3000;
            max-width: 400px;
            animation: slideInRight 0.3s ease;
            display: none;
        }

        .notification.show {
            display: block;
        }

        @keyframes slideInRight {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        /* Позиции */
        .positions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin-top: 40px;
        }

        .position-item {
            background: rgba(30, 25, 45, 0.7);
            border: 1px solid #6a0dad;
            border-radius: 10px;
            padding: 25px;
            transition: all 0.3s ease;
        }

        .position-item:hover {
            border-color: #9370db;
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(138, 43, 226, 0.3);
        }

        /* Футер */
        footer {
            text-align: center;
            padding: 30px;
            color: #888;
            border-top: 1px solid rgba(75, 0, 130, 0.3);
            margin-top: 50px;
            background: rgba(10, 10, 20, 0.8);
        }

        /* Адаптивность */
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                gap: 20px;
            }
            
            nav {
                width: 100%;
                justify-content: center;
                flex-wrap: wrap;
            }
            
            .form-card, .admin-card, .check-status-card {
                padding: 25px;
            }
            
            .admin-controls {
                flex-direction: column;
            }
            
            .logo h1 {
                font-size: 2rem;
            }
            
            .form-title {
                font-size: 1.7rem;
            }
            
            .application-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
            
            .application-status {
                margin-left: 0;
                align-self: flex-start;
            }
        }
    </style>
</head>
<body>
    <div id="app">
        <!-- Шапка -->
        <header>
            <div class="container">
                <div class="header-content">
                    <div class="logo">
                        <div class="logo-icon">✨</div>
                        <h1 class="neon-text">LAIMEWORLD</h1>
                    </div>
                    <nav>
                        <button class="nav-btn active" onclick="showPage('main')">
                            📄 ПОДАТЬ ЗАЯВКУ
                        </button>
                        <button class="nav-btn" onclick="showPage('check')">
                            🔍 ПРОВЕРИТЬ СТАТУС
                        </button>
                        <button class="nav-btn" onclick="showAdminLogin()">
                            🔐 АДМИН ПАНЕЛЬ
                        </button>
                    </nav>
                </div>
            </div>
        </header>

        <!-- Главная страница -->
        <main class="container">
            <div id="mainPage" class="page active">
                <div class="form-card">
                    <h2 class="form-title">ЗАЯВКА В КОМАНДУ LAIMEWORLD</h2>
                    
                    <!-- Возрастной барьер -->
                    <div class="age-warning">
                        <span class="neon-cyan">⚠ ВОЗРАСТ ОТ 13 ЛЕТ</span>
                        <p style="margin-top: 8px; font-size: 0.9rem;">Минимальный возраст: 13 лет</p>
                    </div>
                    
                    <form id="applicationForm">
                        <!-- Основные вопросы -->
                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎯</span>
                                ВЫБЕРИТЕ ДОЛЖНОСТЬ:
                            </label>
                            <select class="form-select" id="position" required onchange="showRoleQuestions()">
                                <option value="">-- ВЫБЕРИТЕ РОЛЬ --</option>
                                <option value="АДМИНИСТРАТОР">👑 АДМИНИСТРАТОР</option>
                                <option value="МОДЕРАТОР">🛡️ МОДЕРАТОР</option>
                                <option value="БИЛДЕР">🏗️ БИЛДЕР</option>
                                <option value="ТЕСТЕР">🔧 ТЕСТЕР</option>
                                <option value="СКРИПТЕР">⚡ СКРИПТЕР</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎂</span>
                                СКОЛЬКО ВАМ ЛЕТ? (ОТ 13):
                            </label>
                            <input type="number" class="form-input" id="age" min="13" required 
                                   oninput="validateAge(this)">
                            <div style="margin-top: 8px; font-size: 0.9rem; color: #9370db;">
                                Минимальный возраст: 13 лет
                            </div>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">👤</span>
                                ВАШ НИКНЕЙМ:
                            </label>
                            <input type="text" class="form-input" id="nickname" required 
                                   placeholder="Например: LaimePlayer">
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">📱</span>
                                TELEGRAM (@username):
                            </label>
                            <input type="text" class="form-input" id="telegram" required 
                                   placeholder="@username или t.me/username">
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">⏰</span>
                                СКОЛЬКО ВРЕМЕНИ МОЖЕТЕ УДЕЛЯТЬ?
                            </label>
                            <select class="form-select" id="time" required>
                                <option value="">-- ВЫБЕРИТЕ --</option>
                                <option value="1-2 часа в день">1-2 часа в день</option>
                                <option value="3-4 часа в день">3-4 часа в день</option>
                                <option value="5+ часов в день">5+ часов в день</option>
                                <option value="Только по выходным">Только по выходным</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">💼</span>
                                ОПЫТ РАБОТЫ НА ПОХОЖИХ ДОЛЖНОСТЯХ:
                                <span class="optional">(не обязательно)</span>
                            </label>
                            <textarea class="form-textarea" id="experience" 
                                      placeholder="Где и кем работали ранее? Какой был опыт? (не обязательно)"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">❓</span>
                                ПОЧЕМУ ИМЕННО МЫ? ЧЕМ ПОНРАВИЛСЯ ПРОЕКТ?
                            </label>
                            <textarea class="form-textarea" id="whyUs" required 
                                      placeholder="Почему выбрали именно наш проект? Что вам в нем нравится?"></textarea>
                        </div>

                        <!-- Вопросы для ролей -->
                        <div id="roleQuestions"></div>

                        <!-- ID заявки -->
                        <div class="form-group" id="applicationIdContainer" style="display: none;">
                            <label class="form-label">
                                <span class="form-icon">🆔</span>
                                ID ВАШЕЙ ЗАЯВКИ:
                            </label>
                            <div class="id-display" id="applicationIdDisplay"></div>
                            <div style="text-align: center; margin-top: 10px;">
                                <button type="button" class="copy-btn" onclick="copyApplicationId()">
                                    📋 КОПИРОВАТЬ ID
                                </button>
                                <div style="margin-top: 10px; color: #9370db; font-size: 0.9rem;">
                                    Сохраните этот ID для проверки статуса заявки
                                </div>
                            </div>
                        </div>

                        <button type="submit" class="btn">
                            <span class="form-icon">🚀</span>
                            ОТПРАВИТЬ ЗАЯВКУ
                        </button>
                    </form>
                </div>

                <!-- Информация о должностях -->
                <div class="positions-grid">
                    <div class="position-item">
                        <h3 class="neon-purple">👑 АДМИНИСТРАТОР</h3>
                        <p>Управление проектом, руководство командой, стратегическое развитие LaimeWorld.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">🛡️ МОДЕРАТОР</h3>
                        <p>Контроль за соблюдением правил, помощь игрокам, решение конфликтов.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">🏗️ БИЛДЕР</h3>
                        <p>Создание построек, дизайн карт, работа с ландшафтом.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">🔧 ТЕСТЕР</h3>
                        <p>Поиск багов, тестирование обновлений, проверка стабильности.</p>
                    </div>
                </div>
            </div>

            <!-- Страница проверки статуса -->
            <div id="checkPage" class="page">
                <div class="check-status-card">
                    <h2 class="form-title">🔍 ПРОВЕРКА СТАТУСА ЗАЯВКИ</h2>
                    
                    <div class="form-group">
                        <label class="form-label">
                            <span class="form-icon">🆔</span>
                            ВВЕДИТЕ ID ЗАЯВКИ:
                        </label>
                        <input type="text" class="form-input" id="checkId" 
                               placeholder="Введите ID заявки (например: LW123456)">
                        <div style="margin-top: 10px; color: #9370db; font-size: 0.9rem;">
                            ID был выдан при отправке заявки
                        </div>
                    </div>
                    
                    <button class="btn" onclick="checkStatus()">
                        <span class="form-icon">🔍</span>
                        ПРОВЕРИТЬ СТАТУС
                    </button>
                    
                    <div id="statusResult"></div>
                </div>
            </div>

            <!-- Админ-панель -->
            <div id="adminPage" class="page">
                <div class="admin-card">
                    <h2 class="form-title">🔐 ПАНЕЛЬ УПРАВЛЕНИЯ LAIMEWORLD</h2>
                    
                    <!-- Статистика -->
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-number" id="totalCount">0</div>
                            <div class="neon-cyan">ВСЕГО ЗАЯВОК</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number" id="pendingCount">0</div>
                            <div class="neon-cyan">НА РАССМОТРЕНИИ</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number" id="approvedCount">0</div>
                            <div class="neon-cyan">ОДОБРЕНО</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number" id="rejectedCount">0</div>
                            <div class="neon-cyan">ОТКЛОНЕНО</div>
                        </div>
                    </div>
                    
                    <!-- Список заявок -->
                    <div id="applicationsList">
                        <!-- Заявки будут загружены здесь -->
                    </div>
                </div>
            </div>
        </main>

        <!-- Модальное окно пароля -->
        <div id="passwordModal" class="modal">
            <div class="modal-content">
                <h3 class="modal-title neon-text">🔒 ВХОД В АДМИН ПАНЕЛЬ</h3>
                <input type="password" id="adminPassword" class="form-input" 
                       placeholder="ВВЕДИТЕ КОД ДОСТУПА"
                       autocomplete="off">
                <div style="display: flex; gap: 15px; margin-top: 25px;">
                    <button class="btn" onclick="checkPassword()">ВОЙТИ</button>
                    <button class="btn btn-delete" onclick="hideModal()">ОТМЕНА</button>
                </div>
                <div style="margin-top: 15px; text-align: center; color: #9370db; font-size: 0.9rem;">
                    Код доступа для администраторов LaimeWorld
                </div>
            </div>
        </div>

        <!-- Нотификация -->
        <div id="notification" class="notification">
            <div class="notification-title"></div>
            <div class="notification-message"></div>
        </div>

        <!-- Футер -->
        <footer>
            <div class="container">
                <p class="neon-purple">LAIMEWORLD © 2024 | СИСТЕМА ЗАЯВОК</p>
                <p style="color: #9370db; margin-top: 15px; font-size: 0.9rem;">
                    Минимальный возраст: 13 лет | Все данные хранятся локально
                </p>
            </div>
        </footer>
    </div>

    <script>
        // Конфигурация
        const STORAGE_KEY = 'laimeworld_applications';
        const ADMIN_PASSWORD = 'Wizixc1LW'; // Пароль для админ панели

        // Генерация ID для заявки
        function generateApplicationId() {
            const prefix = 'LW';
            const timestamp = Date.now().toString().slice(-6);
            const random = Math.floor(Math.random() * 1000).toString().padStart(3, '0');
            return `${prefix}${timestamp}${random}`;
        }

        // Валидация возраста
        function validateAge(input) {
            const age = parseInt(input.value);
            const ageWarning = document.querySelector('.age-warning .neon-cyan');
            
            if (age < 13) {
                input.style.borderColor = '#ff4444';
                input.style.boxShadow = '0 0 10px rgba(255, 68, 68, 0.5)';
                if (ageWarning) {
                    ageWarning.style.color = '#ff4444';
                    ageWarning.textContent = '⚠ МИНИМАЛЬНЫЙ ВОЗРАСТ 13 ЛЕТ!';
                }
            } else {
                input.style.borderColor = '#00ced1';
                input.style.boxShadow = '0 0 10px rgba(0, 206, 209, 0.5)';
                if (ageWarning) {
                    ageWarning.style.color = '#00ced1';
                    ageWarning.textContent = '✅ ВОЗРАСТ ПОДХОДИТ';
                }
            }
        }

        // Показать вопросы для конкретной роли
        function showRoleQuestions() {
            const position = document.getElementById('position').value;
            const roleQuestions = document.getElementById('roleQuestions');
            
            let questionsHTML = '';
            
            switch(position) {
                case 'БИЛДЕР':
                    questionsHTML = `
                        <div class="role-specific-questions show">
                            <h3 style="color: #9370db; margin-bottom: 15px; text-align: center;">🏗️ ВОПРОСЫ ДЛЯ БИЛДЕРА</h3>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🏰</span>
                                    ПРИМЕРЫ ВАШИХ РАБОТ:
                                    <span class="optional">(не обязательно)</span>
                                </label>
                                <textarea class="form-textarea" id="builderPortfolio" 
                                          placeholder="Ссылки на скриншоты или видео ваших построек (не обязательно)"></textarea>
                            </div>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🎨</span>
                                    КАКОЙ СТИЛЬ ПОСТРОЕК ПРЕДПОЧИТАЕТЕ?
                                </label>
                                <textarea class="form-textarea" id="builderStyle" required 
                                          placeholder="Опишите ваш стиль построек, любимые техники"></textarea>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'СКРИПТЕР':
                    questionsHTML = `
                        <div class="role-specific-questions show">
                            <h3 style="color: #9370db; margin-bottom: 15px; text-align: center;">⚡ ВОПРОСЫ ДЛЯ СКРИПТЕРА</h3>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">💻</span>
                                    ЯЗЫКИ ПРОГРАММИРОВАНИЯ КОТОРЫЕ ЗНАЕТЕ:
                                </label>
                                <textarea class="form-textarea" id="scripterSkills" required 
                                          placeholder="Какие языки программирования знаете?"></textarea>
                            </div>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">📁</span>
                                    ПРИМЕРЫ ВАШИХ РАБОТ:
                                    <span class="optional">(не обязательно)</span>
                                </label>
                                <textarea class="form-textarea" id="scripterPortfolio" 
                                          placeholder="Ссылки на ваши проекты или код (не обязательно)"></textarea>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'ТЕСТЕР':
                    questionsHTML = `
                        <div class="role-specific-questions show">
                            <h3 style="color: #9370db; margin-bottom: 15px; text-align: center;">🔧 ВОПРОСЫ ДЛЯ ТЕСТЕРА</h3>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🔍</span>
                                    КАК ВЫ ИЩЕТЕ БАГИ И ОШИБКИ?
                                </label>
                                <textarea class="form-textarea" id="testerMethod" required 
                                          placeholder="Опишите ваш метод поиска багов"></textarea>
                            </div>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">📋</span>
                                    КАК СОСТАВЛЯЕТЕ ОТЧЕТЫ О БАГАХ?
                                    <span class="optional">(не обязательно)</span>
                                </label>
                                <textarea class="form-textarea" id="testerReports" 
                                          placeholder="Как вы оформляете отчеты о найденных багах? (не обязательно)"></textarea>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'МОДЕРАТОР':
                    questionsHTML = `
                        <div class="role-specific-questions show">
                            <h3 style="color: #9370db; margin-bottom: 15px; text-align: center;">🛡️ ВОПРОСЫ ДЛЯ МОДЕРАТОРА</h3>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">⚖️</span>
                                    СИТУАЦИЯ: ИГРОК НАРУШАЕТ ПРАВИЛА. ВАШИ ДЕЙСТВИЯ?
                                </label>
                                <textarea class="form-textarea" id="moderatorScenario" required 
                                          placeholder="Опишите шаг за шагом ваши действия"></textarea>
                            </div>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🤝</span>
                                    КАК РЕШАЕТЕ КОНФЛИКТЫ МЕЖДУ ИГРОКАМИ?
                                </label>
                                <textarea class="form-textarea" id="conflictResolution" required 
                                          placeholder="Опишите ваш подход к решению конфликтов"></textarea>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'АДМИНИСТРАТОР':
                    questionsHTML = `
                        <div class="role-specific-questions show">
                            <h3 style="color: #9370db; margin-bottom: 15px; text-align: center;">👑 ВОПРОСЫ ДЛЯ АДМИНИСТРАТОРА</h3>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🎯</span>
                                    КАКИЕ У ВАС ИДЕИ ДЛЯ РАЗВИТИЯ ПРОЕКТА?
                                    <span class="optional">(не обязательно)</span>
                                </label>
                                <textarea class="form-textarea" id="adminIdeas" 
                                          placeholder="Какие улучшения предлагаете для проекта? (не обязательно)"></textarea>
                            </div>
                            
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">👥</span>
                                    ОПЫТ УПРАВЛЕНИЯ КОМАНДОЙ:
                                </label>
                                <textarea class="form-textarea" id="managementExperience" required 
                                          placeholder="Был ли у вас опыт управления командой?"></textarea>
                            </div>
                        </div>
                    `;
                    break;
                    
                default:
                    roleQuestions.innerHTML = '';
                    return;
            }
            
            roleQuestions.innerHTML = questionsHTML;
        }

        // Показать/скрыть страницы
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            
            const pageElement = document.getElementById(pageId + 'Page');
            if (pageElement) {
                pageElement.classList.add('active');
            }
            
            const navBtn = document.querySelector(`.nav-btn[onclick*="${pageId}"]`);
            if (navBtn) {
                navBtn.classList.add('active');
            }
            
            if (pageId === 'admin') {
                loadApplications();
            }
        }

        // Модальное окно
        function showAdminLogin() {
            document.getElementById('passwordModal').classList.add('active');
            document.getElementById('adminPassword').focus();
        }

        function hideModal() {
            document.getElementById('passwordModal').classList.remove('active');
            document.getElementById('adminPassword').value = '';
        }

        // Проверка пароля
        function checkPassword() {
            const password = document.getElementById('adminPassword').value.trim();
            if (password === ADMIN_PASSWORD) {
                hideModal();
                showPage('admin');
                loadApplications();
            } else {
                const input = document.getElementById('adminPassword');
                input.style.borderColor = '#ff4444';
                input.style.boxShadow = '0 0 10px rgba(255, 68, 68, 0.5)';
                setTimeout(() => {
                    input.style.borderColor = '#6a0dad';
                    input.style.boxShadow = 'none';
                }, 1000);
                input.value = '';
                input.focus();
                showNotification('Ошибка', '❌ Неверный код доступа!');
            }
        }

        // Отправка заявки
        document.getElementById('applicationForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Проверка возраста
            const age = parseInt(document.getElementById('age').value);
            if (age < 13) {
                showNotification('Ошибка', '❌ Минимальный возраст 13 лет!');
                return;
            }

            // Генерация ID
            const appId = generateApplicationId();
            
            // Сбор данных в зависимости от роли
            const position = document.getElementById('position').value;
            let application = {
                id: appId,
                date: new Date().toLocaleString('ru-RU'),
                position: position,
                age: age,
                nickname: document.getElementById('nickname').value.trim(),
                telegram: document.getElementById('telegram').value.trim(),
                time: document.getElementById('time').value,
                experience: document.getElementById('experience').value.trim() || 'Не указано',
                whyUs: document.getElementById('whyUs').value.trim(),
                status: 'pending'
            };

            // Добавляем данные в зависимости от роли
            switch(position) {
                case 'БИЛДЕР':
                    application.builderPortfolio = document.getElementById('builderPortfolio')?.value.trim() || 'Не указано';
                    application.builderStyle = document.getElementById('builderStyle')?.value.trim() || 'Не указано';
                    break;
                case 'СКРИПТЕР':
                    application.scripterSkills = document.getElementById('scripterSkills')?.value.trim() || 'Не указано';
                    application.scripterPortfolio = document.getElementById('scripterPortfolio')?.value.trim() || 'Не указано';
                    break;
                case 'ТЕСТЕР':
                    application.testerMethod = document.getElementById('testerMethod')?.value.trim() || 'Не указано';
                    application.testerReports = document.getElementById('testerReports')?.value.trim() || 'Не указано';
                    break;
                case 'МОДЕРАТОР':
                    application.moderatorScenario = document.getElementById('moderatorScenario')?.value.trim() || 'Не указано';
                    application.conflictResolution = document.getElementById('conflictResolution')?.value.trim() || 'Не указано';
                    break;
                case 'АДМИНИСТРАТОР':
                    application.adminIdeas = document.getElementById('adminIdeas')?.value.trim() || 'Не указано';
                    application.managementExperience = document.getElementById('managementExperience')?.value.trim() || 'Не указано';
                    break;
            }

            // Сохранение в localStorage
            const applications = getApplications();
            applications.push(application);
            localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));

            // Показать ID заявки
            document.getElementById('applicationIdContainer').style.display = 'block';
            document.getElementById('applicationIdDisplay').textContent = appId;
            
            // Прокрутить к ID
            document.getElementById('applicationIdContainer').scrollIntoView({ behavior: 'smooth' });

            showNotification('Успех', `✅ Заявка отправлена! Ваш ID: ${appId}`);
        });

        // Копировать ID заявки
        function copyApplicationId() {
            const id = document.getElementById('applicationIdDisplay').textContent;
            navigator.clipboard.writeText(id).then(() => {
                const btn = document.querySelector('.copy-btn');
                btn.textContent = '✅ СКОПИРОВАНО';
                btn.classList.add('copied');
                setTimeout(() => {
                    btn.textContent = '📋 КОПИРОВАТЬ ID';
                    btn.classList.remove('copied');
                }, 2000);
            });
        }

        // Проверить статус заявки
        function checkStatus() {
            const checkId = document.getElementById('checkId').value.trim().toUpperCase();
            const statusResult = document.getElementById('statusResult');
            
            if (!checkId) {
                statusResult.innerHTML = `
                    <div class="result-card" style="border-color: #ff4444;">
                        <div style="color: #ff4444; text-align: center; font-size: 1.1rem;">
                            ❌ Введите ID заявки
                        </div>
                    </div>
                `;
                return;
            }
            
            const applications = getApplications();
            const application = applications.find(app => app.id === checkId);
            
            if (!application) {
                statusResult.innerHTML = `
                    <div class="result-card" style="border-color: #ff4444;">
                        <div style="color: #ff4444; text-align: center; font-size: 1.1rem;">
                            ❌ Заявка с ID "${checkId}" не найдена
                        </div>
                        <div style="text-align: center; margin-top: 10px; color: #9370db;">
                            Проверьте правильность введенного ID
                        </div>
                    </div>
                `;
                return;
            }
            
            let statusClass, statusText, statusIcon;
            
            switch(application.status) {
                case 'pending':
                    statusClass = 'result-pending';
                    statusText = 'НА РАССМОТРЕНИИ';
                    statusIcon = '🟡';
                    break;
                case 'approved':
                    statusClass = 'result-approved';
                    statusText = 'ОДОБРЕНО';
                    statusIcon = '🟢';
                    break;
                case 'rejected':
                    statusClass = 'result-rejected';
                    statusText = 'ОТКЛОНЕНО';
                    statusIcon = '🔴';
                    break;
            }
            
            statusResult.innerHTML = `
                <div class="result-card ${statusClass}">
                    <div style="text-align: center; margin-bottom: 20px;">
                        <div style="font-size: 2rem; margin-bottom: 10px;">${statusIcon}</div>
                        <div style="font-size: 1.5rem; color: ${application.status === 'approved' ? '#00ff00' : application.status === 'rejected' ? '#ff5555' : '#ffa500'}; font-weight: 700;">
                            ${statusText}
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <div style="color: #9370db; font-weight: 600;">ID заявки:</div>
                        <div style="color: #00ced1; font-size: 1.2rem; font-weight: 700;">${application.id}</div>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <div style="color: #9370db; font-weight: 600;">Должность:</div>
                        <div style="color: #e0e0ff;">${application.position}</div>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <div style="color: #9370db; font-weight: 600;">Никнейм:</div>
                        <div style="color: #e0e0ff;">${application.nickname}</div>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <div style="color: #9370db; font-weight: 600;">Дата подачи:</div>
                        <div style="color: #e0e0ff;">${application.date}</div>
                    </div>
                    
                    ${application.status === 'approved' ? `
                        <div style="margin-top: 20px; padding: 15px; background: rgba(0, 255, 0, 0.1); border-radius: 8px; text-align: center;">
                            <div style="color: #00ff00; font-weight: 700; margin-bottom: 5px;">🎉 ПОЗДРАВЛЯЕМ!</div>
                            <div style="color: #e0e0ff;">С вами свяжется администратор в Telegram</div>
                        </div>
                    ` : ''}
                    
                    ${application.status === 'rejected' ? `
                        <div style="margin-top: 20px; padding: 15px; background: rgba(255, 0, 0, 0.1); border-radius: 8px; text-align: center;">
                            <div style="color: #ff5555; font-weight: 700; margin-bottom: 5px;">😔 ЗАЯВКА ОТКЛОНЕНА</div>
                            <div style="color: #e0e0ff;">Попробуйте подать заявку снова через некоторое время</div>
                        </div>
                    ` : ''}
                </div>
            `;
        }

        // Получить все заявки
        function getApplications() {
            const data = localStorage.getItem(STORAGE_KEY);
            return data ? JSON.parse(data) : [];
        }

        // Загрузка заявок в админ-панель
        function loadApplications() {
            const applications = getApplications();
            const applicationsList = document.getElementById('applicationsList');
            
            // Обновление статистики
            updateStatistics(applications);
            
            if (applications.length === 0) {
                applicationsList.innerHTML = `
                    <div style="text-align: center; padding: 50px; color: #9370db;">
                        <div style="font-size: 3rem; margin-bottom: 20px;">📭</div>
                        <h3 style="margin-bottom: 10px;">НЕТ ЗАЯВОК</h3>
                        <p>Пока никто не отправил заявку</p>
                    </div>
                `;
                return;
            }
            
            // Сортировка: сначала новые
            applications.sort((a, b) => new Date(b.date) - new Date(a.date));
            
            // Отображение заявок
            applicationsList.innerHTML = applications.map(app => `
                <div class="application-card" id="app-${app.id}">
                    <div class="application-header">
                        <div class="application-info">
                            <div class="application-position">${app.position}</div>
                            <div class="application-user">
                                👤 ${app.nickname} | 📱 ${app.telegram} | 🎂 ${app.age} лет
                            </div>
                            <div style="font-size: 0.9rem; color: #888; margin-top: 5px;">
                                🆔 ${app.id} | 📅 ${app.date}
                            </div>
                        </div>
                        <div class="application-status status-${app.status}">
                            ${getStatusText(app.status)}
                        </div>
                    </div>
                    
                    <div class="application-details">
                        <div style="margin-bottom: 10px;">
                            <div style="color: #9370db; font-weight: 600;">⏰ Время:</div>
                            <div style="color: #e0e0ff;">${app.time}</div>
                        </div>
                        <div style="margin-bottom: 10px;">
                            <div style="color: #9370db; font-weight: 600;">❓ Почему выбрал нас:</div>
                            <div style="color: #e0e0ff;">${app.whyUs}</div>
                        </div>
                        ${app.experience !== 'Не указано' ? `
                        <div style="margin-bottom: 10px;">
                            <div style="color: #9370db; font-weight: 600;">💼 Опыт:</div>
                            <div style="color: #e0e0ff;">${app.experience}</div>
                        </div>
                        ` : ''}
                    </div>
                    
                    <div class="admin-controls">
                        ${app.status === 'pending' ? `
                            <button class="btn btn-sm btn-approve" onclick="changeStatus('${app.id}', 'approved')">
                                ✅ ОДОБРИТЬ
                            </button>
                            <button class="btn btn-sm btn-reject" onclick="changeStatus('${app.id}', 'rejected')">
                                ❌ ОТКЛОНИТЬ
                            </button>
                        ` : ''}
                        <button class="btn btn-sm btn-contact" onclick="contactUser('${app.id}')">
                            💬 НАПИСАТЬ В ТГ
                        </button>
                        <button class="btn btn-sm btn-view" onclick="viewApplication('${app.id}')">
                            👁️ ПРОСМОТР
                        </button>
                        <button class="btn btn-sm btn-delete" onclick="deleteApplication('${app.id}')">
                            🗑️ УДАЛИТЬ
                        </button>
                    </div>
                </div>
            `).join('');
        }

        // Получить текст статуса
        function getStatusText(status) {
            switch(status) {
                case 'pending': return 'НА РАССМОТРЕНИИ';
                case 'approved': return 'ОДОБРЕНО';
                case 'rejected': return 'ОТКЛОНЕНО';
                default: return 'НЕИЗВЕСТНО';
            }
        }

        // Изменить статус заявки
        function changeStatus(appId, newStatus) {
            if (!confirm(`Вы уверены, что хотите ${newStatus === 'approved' ? 'одобрить' : 'отклонить'} эту заявку?`)) {
                return;
            }
            
            const applications = getApplications();
            const appIndex = applications.findIndex(app => app.id === appId);
            
            if (appIndex !== -1) {
                applications[appIndex].status = newStatus;
                localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));
                loadApplications();
                
                showNotification('Успех', `✅ Заявка ${newStatus === 'approved' ? 'одобрена' : 'отклонена'}!`);
            }
        }

        // Связаться с пользователем в Telegram
        function contactUser(appId) {
            const applications = getApplications();
            const application = applications.find(app => app.id === appId);
            
            if (!application) return;
            
            // Очищаем telegram от @ и t.me/
            let telegram = application.telegram.trim();
            telegram = telegram.replace('@', '');
            telegram = telegram.replace('t.me/', '');
            telegram = telegram.replace('https://t.me/', '');
            
            // Открываем ссылку в новом окне
            window.open(`https://t.me/${telegram}`, '_blank');
            
            showNotification('Telegram', `💬 Открывается чат с ${application.nickname}`);
        }

        // Просмотр полной заявки
        function viewApplication(appId) {
            const applications = getApplications();
            const app = applications.find(app => app.id === appId);
            
            if (!app) return;
            
            let roleSpecificHTML = '';
            
            switch(app.position) {
                case 'БИЛДЕР':
                    roleSpecificHTML = `
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">🏰 Примеры работ:</div>
                            <div style="color: #e0e0ff;">${app.builderPortfolio || 'Не указано'}</div>
                        </div>
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">🎨 Стиль построек:</div>
                            <div style="color: #e0e0ff;">${app.builderStyle || 'Не указано'}</div>
                        </div>
                    `;
                    break;
                case 'СКРИПТЕР':
                    roleSpecificHTML = `
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">💻 Навыки программирования:</div>
                            <div style="color: #e0e0ff;">${app.scripterSkills || 'Не указано'}</div>
                        </div>
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">📁 Примеры работ:</div>
                            <div style="color: #e0e0ff;">${app.scripterPortfolio || 'Не указано'}</div>
                        </div>
                    `;
                    break;
                case 'ТЕСТЕР':
                    roleSpecificHTML = `
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">🔍 Метод поиска багов:</div>
                            <div style="color: #e0e0ff;">${app.testerMethod || 'Не указано'}</div>
                        </div>
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">📋 Отчеты о багах:</div>
                            <div style="color: #e0e0ff;">${app.testerReports || 'Не указано'}</div>
                        </div>
                    `;
                    break;
                case 'МОДЕРАТОР':
                    roleSpecificHTML = `
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">⚖️ Действия при нарушении:</div>
                            <div style="color: #e0e0ff;">${app.moderatorScenario || 'Не указано'}</div>
                        </div>
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">🤝 Решение конфликтов:</div>
                            <div style="color: #e0e0ff;">${app.conflictResolution || 'Не указано'}</div>
                        </div>
                    `;
                    break;
                case 'АДМИНИСТРАТОР':
                    roleSpecificHTML = `
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">🎯 Идеи для проекта:</div>
                            <div style="color: #e0e0ff;">${app.adminIdeas || 'Не указано'}</div>
                        </div>
                        <div style="margin-bottom: 15px;">
                            <div style="color: #9370db; font-weight: 600;">👥 Опыт управления:</div>
                            <div style="color: #e0e0ff;">${app.managementExperience || 'Не указано'}</div>
                        </div>
                    `;
                    break;
            }
            
            const modal = document.createElement('div');
            modal.className = 'modal active';
            modal.innerHTML = `
                <div class="modal-content" style="max-width: 700px; max-height: 80vh; overflow-y: auto;">
                    <h3 class="modal-title">👁️ ПРОСМОТР ЗАЯВКИ #${app.id}</h3>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                        <div>
                            <div style="color: #9370db; font-weight: 600;">Должность:</div>
                            <div style="color: #e0e0ff; font-size: 1.1rem;">${app.position}</div>
                        </div>
                        <div>
                            <div style="color: #9370db; font-weight: 600;">Статус:</div>
                            <div style="color: ${app.status === 'approved' ? '#00ff00' : app.status === 'rejected' ? '#ff5555' : '#ffa500'}; font-weight: 700;">
                                ${getStatusText(app.status)}
                            </div>
                        </div>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                        <div>
                            <div style="color: #9370db; font-weight: 600;">Никнейм:</div>
                            <div style="color: #e0e0ff;">${app.nickname}</div>
                        </div>
                        <div>
                            <div style="color: #9370db; font-weight: 600;">Telegram:</div>
                            <div style="color: #00ced1;">${app.telegram}</div>
                        </div>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                        <div>
                            <div style="color: #9370db; font-weight: 600;">Возраст:</div>
                            <div style="color: #e0e0ff;">${app.age} лет</div>
                        </div>
                        <div>
                            <div style="color: #9370db; font-weight: 600;">Время в день:</div>
                            <div style="color: #e0e0ff;">${app.time}</div>
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">💼 Опыт работы:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.experience}
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">❓ Почему выбрал нас:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.whyUs}
                        </div>
                    </div>
                    
                    ${roleSpecificHTML}
                    
                    <div style="margin-top: 30px; display: flex; gap: 10px; justify-content: center;">
                        <button class="btn btn-sm" onclick="this.closest('.modal').remove()">ЗАКРЫТЬ</button>
                        <button class="btn btn-sm btn-contact" onclick="contactUser('${app.id}'); this.closest('.modal').remove()">
                            💬 НАПИСАТЬ В ТГ
                        </button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
        }

        // Удаление заявки
        function deleteApplication(appId) {
            if (!confirm('Вы уверены, что хотите удалить эту заявку? Это действие нельзя отменить.')) {
                return;
            }
            
            const applications = getApplications();
            const filteredApplications = applications.filter(app => app.id !== appId);
            localStorage.setItem(STORAGE_KEY, JSON.stringify(filteredApplications));
            loadApplications();
            
            showNotification('Успех', '✅ Заявка удалена!');
        }

        // Обновление статистики
        function updateStatistics(applications) {
            const total = applications.length;
            const pending = applications.filter(app => app.status === 'pending').length;
            const approved = applications.filter(app => app.status === 'approved').length;
            const rejected = applications.filter(app => app.status === 'rejected').length;
            
            document.getElementById('totalCount').textContent = total;
            document.getElementById('pendingCount').textContent = pending;
            document.getElementById('approvedCount').textContent = approved;
            document.getElementById('rejectedCount').textContent = rejected;
        }

        // Показать нотификацию
        function showNotification(title, message) {
            const notification = document.getElementById('notification');
            const titleElement = notification.querySelector('.notification-title');
            const messageElement = notification.querySelector('.notification-message');
            
            titleElement.textContent = title;
            messageElement.textContent = message;
            
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // Слушатель для клавиши Enter в поле пароля
        document.getElementById('adminPassword').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkPassword();
            }
        });

        // Слушатель для клавиши Enter при проверке статуса
        document.getElementById('checkId').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkStatus();
            }
        });

        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', function() {
            // Проверяем, есть ли сохраненные данные
            const applications = getApplications();
            updateStatistics(applications);
            
            // Скрываем админ-панель при загрузке
            document.getElementById('adminPage').classList.remove('active');
            document.getElementById('checkPage').classList.remove('active');
        });
    </script>
</body>
</html>
