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

        /* Страница проверки статуса */
        .check-status-card {
            background: rgba(20, 15, 35, 0.85);
            border: 1px solid #4b0082;
            border-radius: 12px;
            padding: 40px;
            margin-bottom: 30px;
            text-align: center;
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

        .application-details {
            margin-top: 15px;
            padding: 15px;
            background: rgba(30, 25, 45, 0.5);
            border-radius: 8px;
            border-left: 3px solid #9370db;
        }

        .detail-item {
            margin-bottom: 10px;
            padding-bottom: 10px;
            border-bottom: 1px solid rgba(107, 13, 173, 0.2);
        }

        .detail-item:last-child {
            border-bottom: none;
            margin-bottom: 0;
        }

        .detail-label {
            color: #9370db;
            font-weight: 600;
            font-size: 0.95rem;
            margin-bottom: 3px;
        }

        .detail-value {
            color: #e0e0ff;
            font-size: 1rem;
            line-height: 1.4;
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
            border: none;
            cursor: pointer;
            color: white;
            font-weight: 600;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 5px;
        }

        .btn-sm:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
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

        .notification.error {
            border-left: 5px solid #ff4444;
        }

        .notification.success {
            border-left: 5px solid #00ff00;
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

        /* Фильтры */
        .filters {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .filter-btn {
            background: rgba(40, 35, 60, 0.7);
            color: #b19cd9;
            border: 1px solid #6a0dad;
            padding: 8px 16px;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .filter-btn:hover {
            background: rgba(75, 0, 130, 0.3);
        }

        .filter-btn.active {
            background: rgba(138, 43, 226, 0.3);
            border-color: #9370db;
            color: white;
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
            
            .filters {
                justify-content: center;
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
                            <select class="form-select" id="position" required>
                                <option value="">-- ВЫБЕРИТЕ РОЛЬ --</option>
                                <option value="АДМИНИСТРАТОР">👑 АДМИНИСТРАТОР</option>
                                <option value="СТАРШИЙ МОДЕРАТОР">⭐ СТАРШИЙ МОДЕРАТОР</option>
                                <option value="МОДЕРАТОР">🛡️ МОДЕРАТОР</option>
                                <option value="ХЕЛПЕР">💫 ХЕЛПЕР</option>
                                <option value="ТЕСТЕР">🔧 ТЕСТЕР</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎂</span>
                                СКОЛЬКО ВАМ ЛЕТ? (ОТ 13):
                            </label>
                            <input type="number" class="form-input" id="age" min="13" required 
                                   placeholder="Введите ваш возраст">
                            <div style="margin-top: 8px; font-size: 0.9rem; color: #9370db;">
                                Минимальный возраст: 13 лет
                            </div>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">👤</span>
                                ВАШ НИКНЕЙМ В MINECRAFT:
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
                                СКОЛЬКО ЧАСОВ В ДЕНЬ МОЖЕТЕ УДЕЛЯТЬ ПРОЕКТУ?
                            </label>
                            <select class="form-select" id="time" required>
                                <option value="">-- ВЫБЕРИТЕ --</option>
                                <option value="1-2 часа">1-2 часа в день</option>
                                <option value="3-4 часа">3-4 часа в день</option>
                                <option value="5+ часов">5+ часов в день</option>
                                <option value="Только по выходным">Только по выходным</option>
                                <option value="Более 8 часов">Более 8 часов в день</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎮</span>
                                ИГРАЕТЕ ЛИ ВЫ НА НАШЕМ ПРОЕКТЕ В МОМЕНТ ПОДАЧИ ЗАЯВКИ?
                            </label>
                            <select class="form-select" id="playingNow" required>
                                <option value="">-- ВЫБЕРИТЕ --</option>
                                <option value="Да, регулярно играю">Да, регулярно играю</option>
                                <option value="Иногда захожу">Иногда захожу</option>
                                <option value="Только начал(а)">Только начал(а) играть</option>
                                <option value="Нет, но планирую">Нет, но планирую начать</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">📊</span>
                                ОПЫТ РАБОТЫ НА ДРУГИХ ПРОЕКТАХ:
                            </label>
                            <textarea class="form-textarea" id="experience" required rows="3"
                                      placeholder="Был ли у вас опыт работы на других проектах? Если да, опишите его подробно"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">❓</span>
                                ПОЧЕМУ ИМЕННО ВЫ ДОЛЖНЫ ПОЛУЧИТЬ ЭТУ ДОЛЖНОСТЬ?
                            </label>
                            <textarea class="form-textarea" id="whyMe" required rows="3"
                                      placeholder="Почему мы должны выбрать именно вас?"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎯</span>
                                ЧЕГО ВЫ ОЖИДАЕТЕ ОТ РАБОТЫ НА ПРОЕКТЕ?
                            </label>
                            <textarea class="form-textarea" id="expectations" required rows="3"
                                      placeholder="Какие цели вы ставите перед собой?"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🚫</span>
                                КАК ВЫ БУДЕТЕ РЕАГИРОВАТЬ НА ОСКОРБЛЕНИЯ И ПРОВОКАЦИИ?
                            </label>
                            <textarea class="form-textarea" id="reactionToInsults" required rows="3"
                                      placeholder="Опишите вашу реакцию на провокации игроков"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">⚖️</span>
                                СИТУАЦИЯ: ИГРОК НАРУШАЕТ ПРАВИЛА, НО УПОРНО ОТРИЦАЕТ ЭТО. ВАШИ ДЕЙСТВИЯ?
                            </label>
                            <textarea class="form-textarea" id="denialScenario" required rows="3"
                                      placeholder="Как вы будете действовать в такой ситуации?"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">👥</span>
                                КАК ВЫ ОТНОСИТЕСЬ К РАБОТЕ В КОМАНДЕ?
                            </label>
                            <textarea class="form-textarea" id="teamwork" required rows="3"
                                      placeholder="Опишите ваш опыт и отношение к командной работе"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">💡</span>
                                ЕСТЬ ЛИ У ВАС ИДЕИ ДЛЯ УЛУЧШЕНИЯ ПРОЕКТА?
                                <span class="optional">(не обязательно)</span>
                            </label>
                            <textarea class="form-textarea" id="ideas" rows="3"
                                      placeholder="Предложите свои идеи для улучшения проекта (не обязательно)"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">📚</span>
                                ЗНАКОМЫ ЛИ ВЫ С ПРАВИЛАМИ ПРОЕКТА?
                            </label>
                            <select class="form-select" id="rulesKnowledge" required>
                                <option value="">-- ВЫБЕРИТЕ --</option>
                                <option value="Да, знаю все правила">Да, знаю все правила</option>
                                <option value="Знаю основные правила">Знаю основные правила</option>
                                <option value="Ознакомлюсь при необходимости">Ознакомлюсь при необходимости</option>
                                <option value="Требуется повторение">Требуется повторение правил</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🔧</span>
                                ДОПОЛНИТЕЛЬНЫЕ НАВЫКИ (СКРИПТЫ, БИЛД И Т.Д.):
                                <span class="optional">(не обязательно)</span>
                            </label>
                            <textarea class="form-textarea" id="additionalSkills" rows="3"
                                      placeholder="Есть ли у вас дополнительные навыки? (не обязательно)"></textarea>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎤</span>
                                ГОТОВЫ ЛИ ВЫ ОБЩАТЬСЯ В ГОЛОСОВОМ ЧАТЕ ПРИ НЕОБХОДИМОСТИ?
                            </label>
                            <select class="form-select" id="voiceChat" required>
                                <option value="">-- ВЫБЕРИТЕ --</option>
                                <option value="Да, готов общаться">Да, готов общаться</option>
                                <option value="Только в крайнем случае">Только в крайнем случае</option>
                                <option value="Предпочитаю текст">Предпочитаю текстовый чат</option>
                                <option value="Нет, не готов">Нет, не готов</option>
                            </select>
                        </div>

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
                        <p>Полное управление проектом, руководство командой, разработка стратегии, решение глобальных вопросов.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">⭐ СТАРШИЙ МОДЕРАТОР</h3>
                        <p>Руководство модераторами, контроль качества работы, обучение нового персонала.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">🛡️ МОДЕРАТОР</h3>
                        <p>Контроль за соблюдением правил, помощь игрокам, решение конфликтов, выдача наказаний.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">💫 ХЕЛПЕР</h3>
                        <p>Помощь новым игрокам, ответы на вопросы, поддержание дружелюбной атмосферы.</p>
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
                    
                    <!-- Фильтры -->
                    <div class="filters">
                        <button class="filter-btn active" onclick="filterApplications('all')">📋 ВСЕ</button>
                        <button class="filter-btn" onclick="filterApplications('pending')">🟡 НА РАССМОТРЕНИИ</button>
                        <button class="filter-btn" onclick="filterApplications('approved')">🟢 ОДОБРЕНО</button>
                        <button class="filter-btn" onclick="filterApplications('rejected')">🔴 ОТКЛОНЕНО</button>
                    </div>
                    
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
        let currentFilter = 'all';

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
                showNotification('Ошибка', '❌ Неверный код доступа!', 'error');
            }
        }

        // Отправка заявки
        document.getElementById('applicationForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Проверка возраста
            const age = parseInt(document.getElementById('age').value);
            if (age < 13 || isNaN(age)) {
                showNotification('Ошибка', '❌ Минимальный возраст 13 лет!', 'error');
                return;
            }

            // Проверка заполнения обязательных полей
            const requiredFields = ['position', 'nickname', 'telegram', 'time', 'playingNow', 'experience', 'whyMe', 'expectations', 'reactionToInsults', 'denialScenario', 'teamwork', 'rulesKnowledge', 'voiceChat'];
            for (const fieldId of requiredFields) {
                const field = document.getElementById(fieldId);
                if (!field.value.trim()) {
                    showNotification('Ошибка', `❌ Заполните поле: ${field.previousElementSibling.textContent}`, 'error');
                    field.focus();
                    return;
                }
            }

            // Генерация ID
            const appId = generateApplicationId();
            
            // Сбор данных
            const application = {
                id: appId,
                date: new Date().toLocaleString('ru-RU'),
                position: document.getElementById('position').value,
                age: age,
                nickname: document.getElementById('nickname').value.trim(),
                telegram: document.getElementById('telegram').value.trim(),
                time: document.getElementById('time').value,
                playingNow: document.getElementById('playingNow').value,
                experience: document.getElementById('experience').value.trim(),
                whyMe: document.getElementById('whyMe').value.trim(),
                expectations: document.getElementById('expectations').value.trim(),
                reactionToInsults: document.getElementById('reactionToInsults').value.trim(),
                denialScenario: document.getElementById('denialScenario').value.trim(),
                teamwork: document.getElementById('teamwork').value.trim(),
                ideas: document.getElementById('ideas').value.trim() || 'Не указано',
                rulesKnowledge: document.getElementById('rulesKnowledge').value,
                additionalSkills: document.getElementById('additionalSkills').value.trim() || 'Не указано',
                voiceChat: document.getElementById('voiceChat').value,
                status: 'pending',
                adminComment: ''
            };

            // Сохранение в localStorage
            const applications = getApplications();
            applications.push(application);
            localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));

            // Показать ID заявки
            document.getElementById('applicationIdContainer').style.display = 'block';
            document.getElementById('applicationIdDisplay').textContent = appId;
            
            // Прокрутить к ID
            document.getElementById('applicationIdContainer').scrollIntoView({ behavior: 'smooth' });

            showNotification('Успех', `✅ Заявка отправлена! Ваш ID: ${appId}`, 'success');
            
            // Сброс формы через 5 секунд
            setTimeout(() => {
                document.getElementById('applicationForm').reset();
                document.getElementById('applicationIdContainer').style.display = 'none';
            }, 5000);
        });

        // Копировать ID заявки
        function copyApplicationId() {
            const id = document.getElementById('applicationIdDisplay').textContent;
            navigator.clipboard.writeText(id).then(() => {
                const btn = document.querySelector('.copy-btn');
                btn.textContent = '✅ СКОПИРОВАНО';
                btn.style.background = 'rgba(0, 255, 0, 0.2)';
                btn.style.color = '#00ff00';
                btn.style.borderColor = '#00ff00';
                setTimeout(() => {
                    btn.textContent = '📋 КОПИРОВАТЬ ID';
                    btn.style.background = '';
                    btn.style.color = '';
                    btn.style.borderColor = '';
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
                        <div style="margin-top: 5px; color: #9370db; font-size: 0.9rem;">
                            Дата подачи: ${application.date}
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
                    
                    ${application.status === 'approved' ? `
                        <div style="margin-top: 20px; padding: 15px; background: rgba(0, 255, 0, 0.1); border-radius: 8px; text-align: center;">
                            <div style="color: #00ff00; font-weight: 700; margin-bottom: 5px;">🎉 ПОЗДРАВЛЯЕМ!</div>
                            <div style="color: #e0e0ff;">Ваша заявка одобрена! С вами свяжется администратор в Telegram: ${application.telegram}</div>
                            ${application.adminComment ? `
                                <div style="margin-top: 10px; padding: 10px; background: rgba(138, 43, 226, 0.1); border-radius: 5px;">
                                    <div style="color: #9370db; font-weight: 600;">Комментарий администратора:</div>
                                    <div style="color: #e0e0ff;">${application.adminComment}</div>
                                </div>
                            ` : ''}
                        </div>
                    ` : ''}
                    
                    ${application.status === 'rejected' ? `
                        <div style="margin-top: 20px; padding: 15px; background: rgba(255, 0, 0, 0.1); border-radius: 8px; text-align: center;">
                            <div style="color: #ff5555; font-weight: 700; margin-bottom: 5px;">😔 ЗАЯВКА ОТКЛОНЕНА</div>
                            <div style="color: #e0e0ff;">К сожалению, ваша заявка была отклонена.</div>
                            ${application.adminComment ? `
                                <div style="margin-top: 10px; padding: 10px; background: rgba(255, 68, 68, 0.1); border-radius: 5px;">
                                    <div style="color: #ff5555; font-weight: 600;">Причина отказа:</div>
                                    <div style="color: #e0e0ff;">${application.adminComment}</div>
                                </div>
                            ` : ''}
                            <div style="margin-top: 10px; color: #9370db;">
                                Вы можете подать заявку снова через 30 дней
                            </div>
                        </div>
                    ` : ''}
                    
                    ${application.status === 'pending' ? `
                        <div style="margin-top: 20px; padding: 15px; background: rgba(255, 165, 0, 0.1); border-radius: 8px; text-align: center;">
                            <div style="color: #ffa500; font-weight: 700; margin-bottom: 5px;">⏳ ЗАЯВКА НА РАССМОТРЕНИИ</div>
                            <div style="color: #e0e0ff;">Ваша заявка находится на рассмотрении администрацией.</div>
                            <div style="margin-top: 10px; color: #9370db;">
                                Обычно рассмотрение занимает 1-3 дня
                            </div>
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

        // Фильтрация заявок
        function filterApplications(filter) {
            currentFilter = filter;
            document.querySelectorAll('.filter-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            loadApplications();
        }

        // Загрузка заявок в админ-панель
        function loadApplications() {
            let applications = getApplications();
            const applicationsList = document.getElementById('applicationsList');
            
            // Применение фильтра
            if (currentFilter !== 'all') {
                applications = applications.filter(app => app.status === currentFilter);
            }
            
            // Обновление статистики (по всем заявкам)
            updateStatistics(getApplications());
            
            if (applications.length === 0) {
                applicationsList.innerHTML = `
                    <div style="text-align: center; padding: 50px; color: #9370db;">
                        <div style="font-size: 3rem; margin-bottom: 20px;">📭</div>
                        <h3 style="margin-bottom: 10px;">
                            ${currentFilter === 'all' ? 'НЕТ ЗАЯВОК' : 
                              currentFilter === 'pending' ? 'НЕТ ЗАЯВОК НА РАССМОТРЕНИИ' :
                              currentFilter === 'approved' ? 'НЕТ ОДОБРЕННЫХ ЗАЯВОК' :
                              'НЕТ ОТКЛОНЕННЫХ ЗАЯВОК'}
                        </h3>
                        <p>${currentFilter === 'all' ? 'Пока никто не отправил заявку' : 'Нет заявок с таким статусом'}</p>
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
                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 15px;">
                            <div>
                                <div style="color: #9370db; font-weight: 600;">⏰ Время:</div>
                                <div style="color: #e0e0ff;">${app.time}</div>
                            </div>
                            <div>
                                <div style="color: #9370db; font-weight: 600;">🎮 Играет сейчас:</div>
                                <div style="color: #e0e0ff;">${app.playingNow}</div>
                            </div>
                        </div>
                        <div style="margin-bottom: 10px;">
                            <div style="color: #9370db; font-weight: 600;">❓ Почему именно я:</div>
                            <div style="color: #e0e0ff;">${app.whyMe.substring(0, 100)}${app.whyMe.length > 100 ? '...' : ''}</div>
                        </div>
                    </div>
                    
                    <div class="admin-controls">
                        ${app.status === 'pending' ? `
                            <button class="btn-sm btn-approve" onclick="changeStatus('${app.id}', 'approved')">
                                ✅ ОДОБРИТЬ
                            </button>
                            <button class="btn-sm btn-reject" onclick="changeStatus('${app.id}', 'rejected')">
                                ❌ ОТКЛОНИТЬ
                            </button>
                        ` : ''}
                        <button class="btn-sm btn-contact" onclick="contactUser('${app.id}')">
                            💬 НАПИСАТЬ В ТГ
                        </button>
                        <button class="btn-sm btn-view" onclick="viewApplication('${app.id}')">
                            👁️ ПРОСМОТР
                        </button>
                        <button class="btn-sm btn-delete" onclick="deleteApplication('${app.id}')">
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
            const statusText = newStatus === 'approved' ? 'одобрить' : 'отклонить';
            const comment = prompt(`Введите комментарий для пользователя (оставьте пустым, если не нужно):`);
            
            if (comment === null) return; // Если пользователь нажал отмена
            
            const applications = getApplications();
            const appIndex = applications.findIndex(app => app.id === appId);
            
            if (appIndex !== -1) {
                applications[appIndex].status = newStatus;
                applications[appIndex].adminComment = comment || '';
                localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));
                loadApplications();
                
                showNotification('Успех', `✅ Заявка ${statusText}!`, 'success');
                
                // Если одобрено, показываем Telegram
                if (newStatus === 'approved') {
                    setTimeout(() => {
                        if (confirm(`Заявка одобрена! Перейти в Telegram пользователя ${applications[appIndex].nickname}?`)) {
                            contactUser(appId);
                        }
                    }, 500);
                }
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
            
            showNotification('Telegram', `💬 Открывается чат с ${application.nickname}`, 'success');
        }

        // Просмотр полной заявки
        function viewApplication(appId) {
            const applications = getApplications();
            const app = applications.find(app => app.id === appId);
            
            if (!app) return;
            
            const modal = document.createElement('div');
            modal.className = 'modal active';
            modal.innerHTML = `
                <div class="modal-content" style="max-width: 800px; max-height: 80vh; overflow-y: auto;">
                    <h3 class="modal-title">👁️ ПОЛНЫЙ ПРОСМОТР ЗАЯВКИ #${app.id}</h3>
                    
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
                            <div style="color: #9370db; font-weight: 600;">Дата подачи:</div>
                            <div style="color: #e0e0ff;">${app.date}</div>
                        </div>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                        <div>
                            <div style="color: #9370db; font-weight: 600;">⏰ Время в день:</div>
                            <div style="color: #e0e0ff;">${app.time}</div>
                        </div>
                        <div>
                            <div style="color: #9370db; font-weight: 600;">🎮 Играет сейчас:</div>
                            <div style="color: #e0e0ff;">${app.playingNow}</div>
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">💼 Опыт работы:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px; white-space: pre-wrap;">
                            ${app.experience}
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">❓ Почему именно я:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px; white-space: pre-wrap;">
                            ${app.whyMe}
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">🎯 Ожидания от работы:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px; white-space: pre-wrap;">
                            ${app.expectations}
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">🚫 Реакция на оскорбления:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px; white-space: pre-wrap;">
                            ${app.reactionToInsults}
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">⚖️ Ситуация с отрицанием:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px; white-space: pre-wrap;">
                            ${app.denialScenario}
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">👥 Работа в команде:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px; white-space: pre-wrap;">
                            ${app.teamwork}
                        </div>
                    </div>
                    
                    ${app.ideas !== 'Не указано' ? `
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">💡 Идеи для улучшения:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px; white-space: pre-wrap;">
                            ${app.ideas}
                        </div>
                    </div>
                    ` : ''}
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                        <div>
                            <div style="color: #9370db; font-weight: 600;">📚 Знание правил:</div>
                            <div style="color: #e0e0ff;">${app.rulesKnowledge}</div>
                        </div>
                        <div>
                            <div style="color: #9370db; font-weight: 600;">🎤 Голосовой чат:</div>
                            <div style="color: #e0e0ff;">${app.voiceChat}</div>
                        </div>
                    </div>
                    
                    ${app.additionalSkills !== 'Не указано' ? `
                    <div style="margin-bottom: 20px;">
                        <div style="color: #9370db; font-weight: 600;">🔧 Дополнительные навыки:</div>
                        <div style="color: #e0e0ff; background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px; white-space: pre-wrap;">
                            ${app.additionalSkills}
                        </div>
                    </div>
                    ` : ''}
                    
                    ${app.adminComment ? `
                    <div style="margin-bottom: 20px; padding: 15px; background: rgba(138, 43, 226, 0.1); border-radius: 8px;">
                        <div style="color: #9370db; font-weight: 700; margin-bottom: 5px;">💬 Комментарий администратора:</div>
                        <div style="color: #e0e0ff; white-space: pre-wrap;">${app.adminComment}</div>
                    </div>
                    ` : ''}
                    
                    <div style="margin-top: 30px; display: flex; gap: 10px; justify-content: center; flex-wrap: wrap;">
                        <button class="btn-sm btn-contact" onclick="contactUser('${app.id}')">
                            💬 НАПИСАТЬ В ТГ
                        </button>
                        ${app.status === 'pending' ? `
                            <button class="btn-sm btn-approve" onclick="changeStatus('${app.id}', 'approved'); this.closest('.modal').remove()">
                                ✅ ОДОБРИТЬ
                            </button>
                            <button class="btn-sm btn-reject" onclick="changeStatus('${app.id}', 'rejected'); this.closest('.modal').remove()">
                                ❌ ОТКЛОНИТЬ
                            </button>
                        ` : ''}
                        <button class="btn-sm btn-delete" onclick="if(confirm('Удалить заявку?')) { deleteApplication('${app.id}'); this.closest('.modal').remove(); }">
                            🗑️ УДАЛИТЬ
                        </button>
                        <button class="btn-sm" style="background: rgba(40, 35, 60, 0.7);" onclick="this.closest('.modal').remove()">
                            ✖️ ЗАКРЫТЬ
                        </button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
        }

        // Удаление заявки (ИСПРАВЛЕНО)
        function deleteApplication(appId) {
            if (!confirm('Вы уверены, что хотите удалить эту заявку? Это действие нельзя отменить.')) {
                return;
            }
            
            const applications = getApplications();
            const filteredApplications = applications.filter(app => app.id !== appId);
            localStorage.setItem(STORAGE_KEY, JSON.stringify(filteredApplications));
            loadApplications();
            
            showNotification('Успех', '✅ Заявка удалена!', 'success');
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
        function showNotification(title, message, type = '') {
            const notification = document.getElementById('notification');
            const titleElement = notification.querySelector('.notification-title');
            const messageElement = notification.querySelector('.notification-message');
            
            titleElement.textContent = title;
            messageElement.textContent = message;
            
            notification.className = 'notification';
            notification.classList.add('show');
            if (type) {
                notification.classList.add(type);
            }
            
            setTimeout(() => {
                notification.classList.remove('show');
                notification.classList.remove(type);
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
