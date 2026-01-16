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

        /* Темный неон */
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
            min-height: 120px;
            resize: vertical;
            line-height: 1.5;
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

        /* Кнопка просмотра вопросов */
        .toggle-questions-btn {
            background: rgba(40, 35, 60, 0.7);
            color: #9370db;
            border: 1px dashed #6a0dad;
            padding: 14px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            margin: 20px 0;
            width: 100%;
            transition: all 0.3s ease;
            font-weight: 600;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .toggle-questions-btn:hover {
            background: rgba(75, 0, 130, 0.2);
            border-style: solid;
            border-color: #9370db;
        }

        /* Скрытые вопросы */
        .hidden-questions {
            display: none;
            margin-top: 25px;
            padding: 25px;
            background: rgba(30, 25, 45, 0.7);
            border-radius: 10px;
            border-left: 4px solid #8a2be2;
            animation: slideDown 0.5s ease;
        }

        @keyframes slideDown {
            from { opacity: 0; max-height: 0; }
            to { opacity: 1; max-height: 2000px; }
        }

        .hidden-questions.show {
            display: block;
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

        .age-warning .neon-cyan {
            font-size: 1.2rem;
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
            animation: modalFadeIn 0.3s ease;
        }

        @keyframes modalFadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal-content {
            background: rgba(20, 15, 35, 0.95);
            border: 2px solid #8a2be2;
            border-radius: 12px;
            padding: 40px;
            width: 90%;
            max-width: 450px;
            box-shadow: 0 0 60px rgba(138, 43, 226, 0.4);
            transform: scale(1);
            animation: modalScaleIn 0.3s ease;
        }

        @keyframes modalScaleIn {
            from { transform: scale(0.9); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }

        .modal-title {
            color: #9370db;
            margin-bottom: 25px;
            text-align: center;
            font-size: 1.5rem;
            font-weight: 700;
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

        .position-item h3 {
            color: #9370db;
            margin-bottom: 15px;
            font-size: 1.3rem;
            font-weight: 700;
        }

        .position-item p {
            color: #b19cd9;
            line-height: 1.6;
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
            
            .form-card, .admin-card {
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
                        <button class="nav-btn active" onclick="showPage('main')">📄 ПОДАТЬ ЗАЯВКУ</button>
                        <button class="nav-btn" onclick="showAdminLogin()">🔐 АДМИН ПАНЕЛЬ</button>
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
                        <span class="neon-cyan">⚠ ВОЗРАСТ ОТ 12 ДО 18 ЛЕТ</span>
                        <p style="margin-top: 8px; font-size: 0.9rem;">Только для участников 12-18 лет</p>
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
                                <option value="МОДЕРАТОР">🛡️ МОДЕРАТОР</option>
                                <option value="БИЛДЕР">🏗️ БИЛДЕР</option>
                                <option value="ТЕСТЕР">🔧 ТЕСТЕР</option>
                                <option value="СКРИПТЕР">⚡ СКРИПТЕР</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎂</span>
                                СКОЛЬКО ВАМ ЛЕТ? (12-18):
                            </label>
                            <input type="number" class="form-input" id="age" min="12" max="18" required 
                                   oninput="validateAge(this)">
                            <div style="margin-top: 8px; font-size: 0.9rem; color: #9370db;">
                                Только для участников от 12 до 18 лет включительно
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

                        <!-- Кнопка для дополнительных вопросов -->
                        <button type="button" class="toggle-questions-btn" onclick="toggleQuestions()">
                            📋 ПОКАЗАТЬ ДОПОЛНИТЕЛЬНЫЕ ВОПРОСЫ
                        </button>

                        <!-- Скрытые вопросы -->
                        <div id="hiddenQuestions" class="hidden-questions">
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">⏰</span>
                                    СКОЛЬКО ВРЕМЕНИ МОЖЕТЕ УДЕЛЯТЬ?
                                </label>
                                <select class="form-select" id="time">
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
                                </label>
                                <textarea class="form-textarea" id="experience" rows="3" 
                                          placeholder="Где и кем работали ранее? Какой был опыт?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">❓</span>
                                    ПОЧЕМУ ИМЕННО МЫ? ЧЕМ ПОНРАВИЛСЯ ПРОЕКТ?
                                </label>
                                <textarea class="form-textarea" id="whyUs" rows="3" 
                                          placeholder="Почему выбрали именно наш проект? Что вам в нем нравится?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">📜</span>
                                    ЗНАНИЕ ПРАВИЛ ПРОЕКТА:
                                </label>
                                <textarea class="form-textarea" id="rulesKnowledge" rows="3" 
                                          placeholder="Знакомы ли с правилами? Какие основные правила знаете?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🚫</span>
                                    СИТУАЦИЯ: ВИДИТЕ ЧИТЕРА. ВАШИ ДЕЙСТВИЯ?
                                </label>
                                <textarea class="form-textarea" id="cheaterScenario" rows="3" 
                                          placeholder="Опишите шаг за шагом ваши действия при обнаружении читера"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">⚠️</span>
                                    КОНФЛИКТ С ИГРОКОМ. КАК РЕШИТЕ?
                                </label>
                                <textarea class="form-textarea" id="conflictScenario" rows="3" 
                                          placeholder="Игрок нарушает правила и грубит. Ваши действия?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">💡</span>
                                    ИДЕИ ДЛЯ УЛУЧШЕНИЯ ПРОЕКТА:
                                </label>
                                <textarea class="form-textarea" id="ideas" rows="3" 
                                          placeholder="Какие улучшения вы бы предложили для проекта?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">⚔️</span>
                                    ВАШИ СИЛЬНЫЕ СТОРОНЫ:
                                </label>
                                <textarea class="form-textarea" id="strengths" rows="3" 
                                          placeholder="В чем вы особенно хороши? Какие навыки выделяют вас?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🎭</span>
                                    СЛАБЫЕ СТОРОНЫ:
                                </label>
                                <textarea class="form-textarea" id="weaknesses" rows="3" 
                                          placeholder="Над чем вам нужно работать? Какие трудности испытываете?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🤝</span>
                                    РАБОТА В КОМАНДЕ:
                                </label>
                                <textarea class="form-textarea" id="teamwork" rows="3" 
                                          placeholder="Как вы работаете в команде? Легко ли находите общий язык?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🏗️</span>
                                    ЕСЛИ БИЛДЕР: ПРИМЕРЫ РАБОТ (ССЫЛКИ):
                                </label>
                                <textarea class="form-textarea" id="builderPortfolio" rows="3" 
                                          placeholder="Ссылки на скриншоты или видео ваших построек"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🔧</span>
                                    ЕСЛИ ТЕСТЕР: КАК ИЩЕТЕ БАГИ?
                                </label>
                                <textarea class="form-textarea" id="testerMethod" rows="3" 
                                          placeholder="Опишите ваш метод поиска и тестирования багов"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">⚡</span>
                                    ЕСЛИ СКРИПТЕР: ЯЗЫКИ И НАВЫКИ:
                                </label>
                                <textarea class="form-textarea" id="scripterSkills" rows="3" 
                                          placeholder="Какие языки программирования знаете? Примеры работ?"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🎯</span>
                                    ЦЕЛИ В ПРОЕКТЕ:
                                </label>
                                <textarea class="form-textarea" id="goals" rows="3" 
                                          placeholder="Чего хотите достичь в нашем проекте?"></textarea>
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
                        <p>Полный контроль над проектом, управление командой, стратегическое планирование и развитие LaimeWorld.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">🛡️ МОДЕРАТОР</h3>
                        <p>Контроль за соблюдением правил, помощь игрокам, решение конфликтов, поддержание порядка в LaimeWorld.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">🏗️ БИЛДЕР</h3>
                        <p>Создание построек, дизайн карт, работа с ландшафтом, строительство структур для LaimeWorld.</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-purple">🔧 ТЕСТЕР</h3>
                        <p>Поиск багов, тестирование обновлений, проверка стабильности, составление отчетов для LaimeWorld.</p>
                    </div>
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

        <!-- Футер -->
        <footer>
            <div class="container">
                <p class="neon-purple">LAIMEWORLD © 2024 | СИСТЕМА ЗАЯВОК</p>
                <p style="color: #9370db; margin-top: 15px; font-size: 0.9rem;">
                    Для участников 12-18 лет | Все данные хранятся локально
                </p>
            </div>
        </footer>
    </div>

    <script>
        // Конфигурация
        const STORAGE_KEY = 'laimeworld_applications';
        const ADMIN_PASSWORD = 'LAIME2024'; // Измените этот код на свой!

        // Валидация возраста
        function validateAge(input) {
            const age = parseInt(input.value);
            const ageWarning = document.querySelector('.age-warning .neon-cyan');
            
            if (age < 12 || age > 18) {
                input.style.borderColor = '#ff4444';
                input.style.boxShadow = '0 0 10px rgba(255, 68, 68, 0.5)';
                if (ageWarning) {
                    ageWarning.style.color = '#ff4444';
                    ageWarning.textContent = '⚠ ВОЗРАСТ ДОЛЖЕН БЫТЬ 12-18!';
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

        // Показать/скрыть дополнительные вопросы
        let questionsVisible = false;
        function toggleQuestions() {
            const questionsDiv = document.getElementById('hiddenQuestions');
            const toggleBtn = document.querySelector('.toggle-questions-btn');
            
            questionsVisible = !questionsVisible;
            
            if (questionsVisible) {
                questionsDiv.classList.add('show');
                toggleBtn.innerHTML = '📋 СКРЫТЬ ДОПОЛНИТЕЛЬНЫЕ ВОПРОСЫ';
            } else {
                questionsDiv.classList.remove('show');
                toggleBtn.innerHTML = '📋 ПОКАЗАТЬ ДОПОЛНИТЕЛЬНЫЕ ВОПРОСЫ';
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
            }
        }

        // Отправка заявки
        document.getElementById('applicationForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Проверка возраста
            const age = parseInt(document.getElementById('age').value);
            if (age < 12 || age > 18) {
                alert('❌ Возраст должен быть от 12 до 18 лет!');
                return;
            }

            // Сбор данных
            const application = {
                id: Date.now(),
                date: new Date().toLocaleString('ru-RU'),
                position: document.getElementById('position').value,
                age: age,
                nickname: document.getElementById('nickname').value.trim(),
                telegram: document.getElementById('telegram').value.trim(),
                time: document.getElementById('time').value,
                experience: document.getElementById('experience').value.trim(),
                whyUs: document.getElementById('whyUs').value.trim(),
                rulesKnowledge: document.getElementById('rulesKnowledge').value.trim(),
                cheaterScenario: document.getElementById('cheaterScenario').value.trim(),
                conflictScenario: document.getElementById('conflictScenario').value.trim(),
                ideas: document.getElementById('ideas').value.trim(),
                strengths: document.getElementById('strengths').value.trim(),
                weaknesses: document.getElementById('weaknesses').value.trim(),
                teamwork: document.getElementById('teamwork').value.trim(),
                builderPortfolio: document.getElementById('builderPortfolio').value.trim(),
                testerMethod: document.getElementById('testerMethod').value.trim(),
                scripterSkills: document.getElementById('scripterSkills').value.trim(),
                goals: document.getElementById('goals').value.trim(),
                status: 'pending' // Статус по умолчанию: на рассмотрении
            };

            // Сохранение в localStorage
            const applications = getApplications();
            applications.push(application);
            localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));

            // Очистка формы
            document.getElementById('applicationForm').reset();
            const hiddenQuestions = document.getElementById('hiddenQuestions');
            if (hiddenQuestions.classList.contains('show')) {
                toggleQuestions();
            }

            // Показать уведомление
            alert('✅ Заявка успешно отправлена!');
            
            // Сброс возраста
            document.getElementById('age').style.borderColor = '#6a0dad';
            document.getElementById('age').style.boxShadow = 'none';
            const ageWarning = document.querySelector('.age-warning .neon-cyan');
            if (ageWarning) {
                ageWarning.style.color = '#00ced1';
                ageWarning.textContent = '⚠ ВОЗРАСТ ОТ 12 ДО 18 ЛЕТ';
            }
        });

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
            applications.sort((a, b) => b.id - a.id);
            
            // Отображение заявок
            applicationsList.innerHTML = applications.map(app => `
                <div class="application-card" id="app-${app.id}">
                    <div class="application-header">
                        <div class="application-info">
                            <div class="application-position">${app.position}</div>
                            <div class="application-user">${app.nickname} | ${app.telegram}</div>
                            <div class="application-age">${app.age} лет | ${app.time || 'Не указано'}</div>
                            <div style="font-size: 0.9rem; color: #888; margin-top: 5px;">
                                ${app.date}
                            </div>
                        </div>
                        <div class="application-status status-${app.status}">
                            ${getStatusText(app.status)}
                        </div>
                    </div>
                    
                    <div class="application-details">
                        <div class="detail-item">
                            <div class="detail-label">Опыт работы:</div>
                            <div class="detail-value">${app.experience || 'Не указано'}</div>
                        </div>
                        <div class="detail-item">
                            <div class="detail-label">Почему выбрал нас:</div>
                            <div class="detail-value">${app.whyUs || 'Не указано'}</div>
                        </div>
                        <div class="detail-item">
                            <div class="detail-label">Знание правил:</div>
                            <div class="detail-value">${app.rulesKnowledge || 'Не указано'}</div>
                        </div>
                        ${app.ideas ? `
                        <div class="detail-item">
                            <div class="detail-label">Идеи для улучшения:</div>
                            <div class="detail-value">${app.ideas}</div>
                        </div>
                        ` : ''}
                    </div>
                    
                    <div class="admin-controls">
                        ${app.status === 'pending' ? `
                            <button class="btn btn-sm btn-approve" onclick="changeStatus(${app.id}, 'approved')">
                                ✅ ОДОБРИТЬ
                            </button>
                            <button class="btn btn-sm btn-reject" onclick="changeStatus(${app.id}, 'rejected')">
                                ❌ ОТКЛОНИТЬ
                            </button>
                        ` : ''}
                        <button class="btn btn-sm btn-view" onclick="viewApplication(${app.id})">
                            👁️ ПРОСМОТР
                        </button>
                        <button class="btn btn-sm btn-delete" onclick="deleteApplication(${app.id})">
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
                
                alert(`✅ Заявка ${newStatus === 'approved' ? 'одобрена' : 'отклонена'}!`);
            }
        }

        // Просмотр полной заявки
        function viewApplication(appId) {
            const applications = getApplications();
            const app = applications.find(app => app.id === appId);
            
            if (!app) return;
            
            const details = `
                <div style="max-height: 70vh; overflow-y: auto; padding-right: 10px;">
                    <h3 style="color: #9370db; margin-bottom: 20px; text-align: center;">
                        ПОЛНАЯ ИНФОРМАЦИЯ О ЗАЯВКЕ
                    </h3>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                        <div>
                            <div class="detail-label">Должность:</div>
                            <div class="detail-value">${app.position}</div>
                        </div>
                        <div>
                            <div class="detail-label">Статус:</div>
                            <div class="detail-value" style="color: ${app.status === 'approved' ? '#00ff00' : app.status === 'rejected' ? '#ff5555' : '#ffa500'}">
                                ${getStatusText(app.status)}
                            </div>
                        </div>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                        <div>
                            <div class="detail-label">Никнейм:</div>
                            <div class="detail-value">${app.nickname}</div>
                        </div>
                        <div>
                            <div class="detail-label">Telegram:</div>
                            <div class="detail-value">${app.telegram}</div>
                        </div>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                        <div>
                            <div class="detail-label">Возраст:</div>
                            <div class="detail-value">${app.age} лет</div>
                        </div>
                        <div>
                            <div class="detail-label">Время в день:</div>
                            <div class="detail-value">${app.time || 'Не указано'}</div>
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Опыт работы:</div>
                        <div class="detail-value" style="background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.experience || 'Не указано'}
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Почему выбрал нас:</div>
                        <div class="detail-value" style="background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.whyUs || 'Не указано'}
                        </div>
                    </div>
                    
                    ${app.cheaterScenario ? `
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Действия при читере:</div>
                        <div class="detail-value" style="background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.cheaterScenario}
                        </div>
                    </div>
                    ` : ''}
                    
                    ${app.conflictScenario ? `
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Решение конфликтов:</div>
                        <div class="detail-value" style="background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.conflictScenario}
                        </div>
                    </div>
                    ` : ''}
                    
                    ${app.ideas ? `
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Идеи для улучшения:</div>
                        <div class="detail-value" style="background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.ideas}
                        </div>
                    </div>
                    ` : ''}
                    
                    ${app.strengths ? `
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Сильные стороны:</div>
                        <div class="detail-value" style="background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.strengths}
                        </div>
                    </div>
                    ` : ''}
                    
                    ${app.builderPortfolio ? `
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Примеры работ (билдер):</div>
                        <div class="detail-value" style="background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.builderPortfolio}
                        </div>
                    </div>
                    ` : ''}
                    
                    ${app.scripterSkills ? `
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Навыки (скриптер):</div>
                        <div class="detail-value" style="background: rgba(40, 35, 60, 0.5); padding: 10px; border-radius: 5px;">
                            ${app.scripterSkills}
                        </div>
                    </div>
                    ` : ''}
                    
                    <div style="margin-bottom: 20px;">
                        <div class="detail-label">Дата подачи:</div>
                        <div class="detail-value">${app.date}</div>
                    </div>
                </div>
            `;
            
            alertWithHTML(details, 'Просмотр заявки');
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
            
            alert('✅ Заявка удалена!');
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

        // Вспомогательная функция для алерта с HTML
        function alertWithHTML(content, title = '') {
            const modal = document.createElement('div');
            modal.className = 'modal active';
            modal.innerHTML = `
                <div class="modal-content" style="max-width: 700px;">
                    ${title ? `<h3 class="modal-title">${title}</h3>` : ''}
                    ${content}
                    <div style="text-align: center; margin-top: 30px;">
                        <button class="btn" onclick="this.closest('.modal').remove()">ЗАКРЫТЬ</button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
        }

        // Слушатель для клавиши Enter в поле пароля
        document.getElementById('adminPassword').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkPassword();
            }
        });

        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', function() {
            // Проверяем, есть ли сохраненные данные
            const applications = getApplications();
            updateStatistics(applications);
            
            // Скрываем админ-панель при загрузке
            document.getElementById('adminPage').classList.remove('active');
        });
    </script>
</body>
</html>
