<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Majestic DM | Система заявок</title>
    <style>
        /* Основные стили */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', 'Arial', sans-serif;
            background: #0a0a1a;
            color: #fff;
            min-height: 100vh;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(255, 20, 150, 0.1) 0%, transparent 20%),
                radial-gradient(circle at 90% 80%, rgba(255, 20, 150, 0.1) 0%, transparent 20%);
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Неоновый текст */
        .neon-text {
            color: #fff;
            text-shadow:
                0 0 5px #ff00ff,
                0 0 10px #ff00ff,
                0 0 20px #ff00ff,
                0 0 40px #ff1493,
                0 0 80px #ff1493;
            font-weight: bold;
        }

        .neon-pink {
            color: #ff00ff;
            text-shadow:
                0 0 10px #ff00ff,
                0 0 20px #ff1493;
        }

        /* Шапка */
        header {
            background: rgba(10, 10, 26, 0.95);
            border-bottom: 2px solid #ff00ff;
            box-shadow: 0 0 30px rgba(255, 0, 255, 0.3);
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo h1 {
            font-size: 2.2rem;
            letter-spacing: 2px;
        }

        .logo-icon {
            font-size: 2.5rem;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { text-shadow: 0 0 10px #ff00ff; }
            50% { text-shadow: 0 0 20px #ff00ff, 0 0 30px #ff1493; }
        }

        /* Навигация */
        nav {
            display: flex;
            gap: 10px;
        }

        .nav-btn {
            background: transparent;
            color: #ffb6c1;
            border: 2px solid #ff00ff;
            padding: 10px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .nav-btn:hover {
            background: rgba(255, 0, 255, 0.2);
            color: #fff;
            box-shadow: 0 0 15px rgba(255, 0, 255, 0.5);
            transform: translateY(-2px);
        }

        .nav-btn.active {
            background: linear-gradient(45deg, #ff00ff, #ff1493);
            color: white;
            box-shadow: 0 0 20px rgba(255, 0, 255, 0.7);
        }

        /* Главный контент */
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

        /* Карточки форм */
        .form-card {
            background: rgba(20, 10, 30, 0.8);
            border: 2px solid #ff00ff;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 0 40px rgba(255, 0, 255, 0.2);
            margin-bottom: 30px;
        }

        .form-title {
            font-size: 1.8rem;
            margin-bottom: 25px;
            text-align: center;
        }

        /* Форма */
        .form-group {
            margin-bottom: 25px;
            position: relative;
        }

        .form-label {
            display: block;
            margin-bottom: 8px;
            color: #ffb6c1;
            font-weight: 500;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .form-icon {
            color: #ff00ff;
            font-size: 1.2rem;
        }

        .form-input, .form-select, .form-textarea {
            width: 100%;
            padding: 12px 15px;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 0, 255, 0.5);
            border-radius: 10px;
            color: white;
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .form-input:focus, .form-select:focus, .form-textarea:focus {
            outline: none;
            border-color: #ff00ff;
            box-shadow: 0 0 15px rgba(255, 0, 255, 0.3);
            background: rgba(255, 255, 255, 0.1);
        }

        .form-textarea {
            min-height: 100px;
            resize: vertical;
        }

        /* Кнопки */
        .btn {
            background: linear-gradient(45deg, #ff00ff, #ff1493);
            color: white;
            border: none;
            padding: 15px 35px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: bold;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            margin-top: 20px;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(255, 0, 255, 0.4);
        }

        .btn-secondary {
            background: transparent;
            border: 2px solid #ff00ff;
        }

        /* Кнопка просмотра вопросов */
        .toggle-questions-btn {
            background: transparent;
            color: #ff00ff;
            border: 2px dashed #ff00ff;
            padding: 10px 20px;
            border-radius: 15px;
            cursor: pointer;
            font-size: 1rem;
            margin: 10px 0;
            width: 100%;
            transition: all 0.3s ease;
        }

        .toggle-questions-btn:hover {
            background: rgba(255, 0, 255, 0.1);
            border-style: solid;
        }

        /* Скрытые вопросы */
        .hidden-questions {
            display: none;
            margin-top: 20px;
            padding: 20px;
            background: rgba(255, 0, 255, 0.05);
            border-radius: 15px;
            border-left: 4px solid #ff00ff;
        }

        .hidden-questions.show {
            display: block;
            animation: slideDown 0.5s ease;
        }

        @keyframes slideDown {
            from { opacity: 0; max-height: 0; }
            to { opacity: 1; max-height: 1000px; }
        }

        /* Админ-панель */
        .application-card {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 0, 255, 0.3);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            transition: all 0.3s ease;
        }

        .application-card:hover {
            border-color: #ff00ff;
            transform: translateX(5px);
        }

        .application-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid rgba(255, 0, 255, 0.2);
        }

        .application-status {
            padding: 5px 15px;
            border-radius: 15px;
            font-size: 0.9rem;
            font-weight: bold;
        }

        .status-pending {
            background: rgba(255, 165, 0, 0.2);
            color: #ffa500;
        }

        .status-approved {
            background: rgba(0, 255, 0, 0.2);
            color: #00ff00;
        }

        .status-rejected {
            background: rgba(255, 0, 0, 0.2);
            color: #ff5555;
        }

        .admin-controls {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }

        .btn-sm {
            padding: 8px 15px;
            font-size: 0.9rem;
        }

        .btn-approve {
            background: linear-gradient(45deg, #00ff00, #00cc00);
        }

        .btn-reject {
            background: linear-gradient(45deg, #ff0000, #cc0000);
        }

        /* Модальное окно */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
            z-index: 2000;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: rgba(20, 10, 30, 0.95);
            border: 2px solid #ff00ff;
            border-radius: 20px;
            padding: 30px;
            width: 90%;
            max-width: 400px;
            box-shadow: 0 0 50px rgba(255, 0, 255, 0.5);
        }

        .modal-title {
            color: #ff00ff;
            margin-bottom: 20px;
            text-align: center;
        }

        /* Анимации */
        @keyframes glow {
            0%, 100% { box-shadow: 0 0 20px rgba(255, 0, 255, 0.3); }
            50% { box-shadow: 0 0 30px rgba(255, 0, 255, 0.6); }
        }

        .glowing-border {
            animation: glow 3s infinite;
        }

        /* Футер */
        footer {
            text-align: center;
            padding: 20px;
            color: #888;
            border-top: 1px solid rgba(255, 0, 255, 0.2);
            margin-top: 40px;
        }

        /* Информация о должностях */
        .positions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .position-item {
            background: rgba(255, 0, 255, 0.1);
            border: 1px solid rgba(255, 0, 255, 0.3);
            border-radius: 15px;
            padding: 20px;
            transition: all 0.3s ease;
        }

        .position-item:hover {
            transform: translateY(-5px);
            border-color: #ff00ff;
        }

        /* Адаптивность */
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                gap: 15px;
            }
            
            nav {
                width: 100%;
                justify-content: center;
            }
            
            .form-card {
                padding: 20px;
            }
            
            .admin-controls {
                flex-direction: column;
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
                        <div class="logo-icon neon-text">✨</div>
                        <h1 class="neon-text">Majestic DM</h1>
                    </div>
                    <nav>
                        <button class="nav-btn active" onclick="showPage('main')">🎯 Подать заявку</button>
                        <button class="nav-btn" onclick="showAdminLogin()">🔐 Админ-панель</button>
                    </nav>
                </div>
            </div>
        </header>

        <!-- Главная страница -->
        <main class="container">
            <div id="mainPage" class="page active">
                <div class="form-card glowing-border">
                    <h2 class="form-title neon-text">📝 Заявка в команду Majestic DM</h2>
                    
                    <form id="applicationForm">
                        <!-- Основные вопросы -->
                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎭</span>
                                Выберите должность:
                            </label>
                            <select class="form-select" id="position" required>
                                <option value="">-- Выберите вашу роль --</option>
                                <option value="Главный Администратор">👑 Главный Администратор</option>
                                <option value="Старший Модератор">🛡️ Старший Модератор</option>
                                <option value="Куратор Ивентов">🎪 Куратор Ивентов</option>
                                <option value="Ведомый Модератор">👥 Ведомый Модератор</option>
                                <option value="Креативный Билдер">🏗️ Креативный Билдер</option>
                                <option value="Технический Тестер">🔧 Технический Тестер</option>
                                <option value="Дизайнер">🎨 Дизайнер</option>
                                <option value="Скриптер">⚡ Скриптер</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">🎂</span>
                                Сколько вам лет?
                            </label>
                            <input type="number" class="form-input" id="age" min="14" max="70" required>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">👤</span>
                                Ваш уникальный никнейм:
                            </label>
                            <input type="text" class="form-input" id="nickname" required>
                        </div>

                        <div class="form-group">
                            <label class="form-label">
                                <span class="form-icon">💬</span>
                                Discord (username#0000):
                            </label>
                            <input type="text" class="form-input" id="discord" required placeholder="majestic_dm#1234">
                        </div>

                        <!-- Кнопка для дополнительных вопросов -->
                        <button type="button" class="toggle-questions-btn" onclick="toggleQuestions()">
                            📋 Показать дополнительные вопросы (15+)
                        </button>

                        <!-- Скрытые вопросы -->
                        <div id="hiddenQuestions" class="hidden-questions">
                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">⏰</span>
                                    Сколько часов в день готовы уделять проекту?
                                </label>
                                <select class="form-select" id="time">
                                    <option value="">-- Выберите --</option>
                                    <option value="2-3 часа">2-3 часа</option>
                                    <option value="4-5 часов">4-5 часов</option>
                                    <option value="6+ часов">6+ часов</option>
                                    <option value="Весь день">Весь день</option>
                                </select>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">📅</span>
                                    Когда можете приступить к работе?
                                </label>
                                <input type="date" class="form-input" id="startDate">
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🎯</span>
                                    Какой ваш часовой пояс?
                                </label>
                                <input type="text" class="form-input" id="timezone" placeholder="МСК +3">
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">💼</span>
                                    Опыт работы на подобной должности:
                                </label>
                                <textarea class="form-textarea" id="experience" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🔥</span>
                                    Почему именно вы должны получить эту должность?
                                </label>
                                <textarea class="form-textarea" id="motivation" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">💡</span>
                                    Ваши уникальные идеи для проекта:
                                </label>
                                <textarea class="form-textarea" id="ideas" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🎮</span>
                                    Любимые игры/проекты где участвовали:
                                </label>
                                <textarea class="form-textarea" id="favoriteGames" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">⚔️</span>
                                    Ваши сильные стороны:
                                </label>
                                <textarea class="form-textarea" id="strengths" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🎭</span>
                                    Слабости, над которыми работаете:
                                </label>
                                <textarea class="form-textarea" id="weaknesses" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🏆</span>
                                    Ваши достижения в подобных проектах:
                                </label>
                                <textarea class="form-textarea" id="achievements" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🤝</span>
                                    Как решаете конфликты в команде?
                                </label>
                                <textarea class="form-textarea" id="conflictResolution" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">📊</span>
                                    Уровень английского языка:
                                </label>
                                <select class="form-select" id="englishLevel">
                                    <option value="">-- Выберите --</option>
                                    <option value="Начальный">Начальный</option>
                                    <option value="Средний">Средний</option>
                                    <option value="Продвинутый">Продвинутый</option>
                                    <option value="Носитель">Носитель</option>
                                </select>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🔗</span>
                                    Ссылки на портфолио/работы:
                                </label>
                                <textarea class="form-textarea" id="portfolio" rows="2"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">🎯</span>
                                    Чего хотите достичь в нашем проекте?
                                </label>
                                <textarea class="form-textarea" id="goals" rows="3"></textarea>
                            </div>

                            <div class="form-group">
                                <label class="form-label">
                                    <span class="form-icon">💬</span>
                                    Есть ли вопросы к нам?
                                </label>
                                <textarea class="form-textarea" id="questions" rows="3"></textarea>
                            </div>
                        </div>

                        <button type="submit" class="btn">
                            <span class="form-icon">🚀</span>
                            Отправить заявку
                        </button>
                    </form>
                </div>

                <!-- Информация о должностях -->
                <div class="positions-grid">
                    <div class="position-item">
                        <h3 class="neon-pink">👑 Главный Администратор</h3>
                        <p>Полный контроль, управление командой, стратегическое планирование</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-pink">🛡️ Старший Модератор</h3>
                        <p>Контроль модерации, обучение команды, решение сложных ситуаций</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-pink">🎪 Куратор Ивентов</h3>
                        <p>Организация мероприятий, создание уникального контента</p>
                    </div>
                    <div class="position-item">
                        <h3 class="neon-pink">🏗️ Креативный Билдер</h3>
                        <p>Создание миров, дизайн карт, архитектурные решения</p>
                    </div>
                </div>
            </div>

            <!-- Админ-панель -->
            <div id="adminPage" class="page">
                <div class="form-card">
                    <h2 class="form-title neon-text">🔐 Панель управления заявками</h2>
                    
                    <div class="admin-stats" style="margin-bottom: 20px;">
                        <p class="neon-pink">Всего заявок: <span id="totalCount">0</span></p>
                        <p class="neon-pink">На рассмотрении: <span id="pendingCount">0</span></p>
                    </div>
                    
                    <div id="applicationsList">
                        <!-- Заявки будут загружены здесь -->
                    </div>
                </div>
            </div>
        </main>

        <!-- Модальное окно пароля -->
        <div id="passwordModal" class="modal">
            <div class="modal-content glowing-border">
                <h3 class="modal-title neon-text">🔒 Вход в админ-панель</h3>
                <input type="password" id="adminPassword" class="form-input" placeholder="Введите пароль администратора">
                <div style="display: flex; gap: 10px; margin-top: 20px;">
                    <button class="btn" onclick="checkPassword()">Войти</button>
                    <button class="btn btn-secondary" onclick="hideModal()">Отмена</button>
                </div>
            </div>
        </div>

        <!-- Футер -->
        <footer>
            <div class="container">
                <p class="neon-pink">Majestic DM © 2024 | Система заявок v2.0</p>
                <p style="color: #ffb6c1; margin-top: 10px;">Все заявки хранятся в вашем браузере</p>
            </div>
        </footer>
    </div>

    <script>
        // Конфигурация
        const STORAGE_KEY = 'majestic_dm_applications';
        const ADMIN_PASSWORD = 'majestic2024'; // Поменяйте этот пароль!

        // Показать/скрыть страницы
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            
            document.getElementById(pageId + 'Page').classList.add('active');
            document.querySelector(`.nav-btn[onclick*="${pageId}"]`).classList.add('active');
            
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
                toggleBtn.innerHTML = '📋 Скрыть дополнительные вопросы';
            } else {
                questionsDiv.classList.remove('show');
                toggleBtn.innerHTML = '📋 Показать дополнительные вопросы (15+)';
            }
        }

        // Модальное окно
        function showAdminLogin() {
            document.getElementById('passwordModal').classList.add('active');
        }

        function hideModal() {
            document.getElementById('passwordModal').classList.remove('active');
            document.getElementById('adminPassword').value = '';
        }

        // Проверка пароля
        function checkPassword() {
            const password = document.getElementById('adminPassword').value;
            if (password === ADMIN_PASSWORD) {
                hideModal();
                showPage('admin');
            } else {
                alert('❌ Неверный пароль!');
                document.getElementById('adminPassword').value = '';
            }
        }

        // Отправка заявки
        document.getElementById('applicationForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const application = {
                id: Date.now(),
                position: document.getElementById('position').value,
                age: document.getElementById('age').value,
                nickname: document.getElementById('nickname').value,
                discord: document.getElementById('discord').value,
                time: document.getElementById('time').value,
                startDate: document.getElementById('startDate').value,
                timezone: document.getElementById('timezone').value,
                experience: document.getElementById('experience').value,
                motivation: document.getElementById('motivation').value,
                ideas: document.getElementById('ideas').value,
                favoriteGames: document.getElementById('favoriteGames').value,
                strengths: document.getElementById('strengths').value,
                weaknesses: document.getElementById('weaknesses').value,
                achievements: document.getElementById('achievements').value,
                conflictResolution: document.getElementById('conflictResolution').value,
                englishLevel: document.getElementById('englishLevel').value,
                portfolio: document.getElementById('portfolio').value,
                goals: document.getElementById('goals').value,
                questions: document.getElementById('questions').value,
                status: 'pending',
                date: new Date().toLocaleString('ru-RU')
            };

            // Проверка возраста
            if (application.age < 14 || application.age > 70) {
                alert('❌ Возраст должен быть от 14 до 70 лет!');
                return;
            }

            // Сохранение
            let applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            applications.unshift(application); // Добавляем в начало
            localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));
            
            // Очистка формы
            this.reset();
            if (questionsVisible) toggleQuestions();
            
            // Анимация успеха
            const submitBtn = this.querySelector('.btn');
            const originalText = submitBtn.innerHTML;
            submitBtn.innerHTML = '✅ Отправлено!';
            submitBtn.style.background = 'linear-gradient(45deg, #00ff00, #00cc00)';
            
            setTimeout(() => {
                submitBtn.innerHTML = originalText;
                submitBtn.style.background = 'linear-gradient(45deg, #ff00ff, #ff1493)';
            }, 2000);
            
            alert(`✨ Заявка #${application.id} отправлена!`);
        });

        // Загрузка заявок в админке
        function loadApplications() {
            const applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            const container = document.getElementById('applicationsList');
            
            // Статистика
            document.getElementById('totalCount').textContent = applications.length;
            document.getElementById('pendingCount').textContent = 
                applications.filter(app => app.status === 'pending').length;

            if (applications.length === 0) {
                container.innerHTML = '<p class="neon-pink">📭 Нет заявок для рассмотрения</p>';
                return;
            }

            let html = '';
            applications.forEach(app => {
                const statusClass = `status-${app.status}`;
                const statusText = {
                    'pending': '⏳ На рассмотрении',
                    'approved': '✅ Одобрено',
                    'rejected': '❌ Отклонено'
                }[app.status];

                html += `
                    <div class="application-card">
                        <div class="application-header">
                            <h3 class="neon-pink">${app.position} | ${app.nickname} (${app.age})</h3>
                            <span class="application-status ${statusClass}">${statusText}</span>
                        </div>
                        
                        <p><strong>Discord:</strong> ${app.discord}</p>
                        ${app.time ? `<p><strong>Время:</strong> ${app.time}</p>` : ''}
                        ${app.timezone ? `<p><strong>Часовой пояс:</strong> ${app.timezone}</p>` : ''}
                        ${app.experience ? `<p><strong>Опыт:</strong> ${app.experience.substring(0, 100)}...</p>` : ''}
                        ${app.motivation ? `<p><strong>Мотивация:</strong> ${app.motivation.substring(0, 100)}...</p>` : ''}
                        
                        <p><small>📅 ${app.date}</small></p>
                        
                        ${app.status === 'pending' ? `
                            <div class="admin-controls">
                                <button class="btn btn-sm btn-approve" onclick="updateStatus(${app.id}, 'approved')">
                                    ✅ Одобрить
                                </button>
                                <button class="btn btn-sm btn-reject" onclick="updateStatus(${app.id}, 'rejected')">
                                    ❌ Отклонить
                                </button>
                                <button class="btn btn-sm btn-secondary" onclick="viewApplication(${app.id})">
                                    👁️ Просмотр
                                </button>
                                <button class="btn btn-sm" onclick="deleteApplication(${app.id})" style="background: #555;">
                                    🗑️ Удалить
                                </button>
                            </div>
                        ` : ''}
                    </div>
                `;
            });
            
            container.innerHTML = html;
        }

        // Обновление статуса
        function updateStatus(id, status) {
            if (!confirm(`Вы уверены, что хотите ${status === 'approved' ? 'одобрить' : 'отклонить'} эту заявку?`)) {
                return;
            }

            let applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            applications = applications.map(app => app.id === id ? {...app, status} : app);
            localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));
            
            loadApplications();
            alert(`Заявка ${status === 'approved' ? 'одобрена' : 'отклонена'}!`);
        }

        // Просмотр полной заявки
        function viewApplication(id) {
            const applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            const app = applications.find(a => a.id === id);
            
            if (!app) return;
            
            let details = `🎯 Должность: ${app.position}\n`;
            details += `👤 Никнейм: ${app.nickname}\n`;
            details += `🎂 Возраст: ${app.age}\n`;
            details += `💬 Discord: ${app.discord}\n`;
            details += `⏰ Время: ${app.time || 'Не указано'}\n`;
            details += `📅 Начало: ${app.startDate || 'Не указано'}\n`;
            details += `🌍 Часовой пояс: ${app.timezone || 'Не указано'}\n`;
            details += `🏆 Опыт: ${app.experience || 'Не указано'}\n`;
            details += `🔥 Мотивация: ${app.motivation || 'Не указано'}\n`;
            details += `💡 Идеи: ${app.ideas || 'Не указано'}\n`;
            details += `📅 Дата подачи: ${app.date}\n`;
            details += `📊 Статус: ${app.status === 'pending' ? '⏳ На рассмотрении' : app.status === 'approved' ? '✅ Одобрено' : '❌ Отклонено'}`;
            
            alert(details);
        }

        // Удаление заявки
        function deleteApplication(id) {
            if (!confirm('❌ Удалить эту заявку навсегда?')) return;
            
            let applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            applications = applications.filter(app => app.id !== id);
            localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));
            
            loadApplications();
            alert('🗑️ Заявка удалена!');
        }

        // Инициализация
        document.addEventListener('DOMContentLoaded', () => {
            // Проверяем хэш для быстрого доступа к админке
            if (window.location.hash === '#admin') {
                showAdminLogin();
            }
            
            // Загружаем текущие заявки если есть
            const applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            if (applications.length > 0) {
                console.log(`📊 Загружено ${applications.length} заявок`);
            }
        });
    </script>
</body>
</html>
