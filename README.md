<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Система Заявок | GitHub Pages</title>
    <style>
        /* Стили */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        .container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }
        header {
            background: rgba(255, 255, 255, 0.95);
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 1000;
        }
        header .container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
        }
        header h1 { color: #2c3e50; }
        nav a {
            text-decoration: none;
            color: #555;
            padding: 8px 16px;
            border-radius: 20px;
            transition: all 0.3s ease;
            margin-left: 10px;
        }
        nav a:hover { background: #667eea; color: white; }
        nav a.active { background: #667eea; color: white; }
        .form-container, .admin-container {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin: 30px auto;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        }
        .form-group { margin-bottom: 20px; }
        label { display: block; margin-bottom: 5px; color: #2c3e50; }
        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
        }
        button {
            background: #667eea;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover { background: #5a6fd8; }
        .application-card {
            background: #f8f9fa;
            border-left: 4px solid #667eea;
            padding: 20px;
            margin-bottom: 15px;
            border-radius: 8px;
        }
        .admin-controls { display: flex; gap: 10px; margin-top: 10px; }
        .approved { border-left-color: #4CAF50; }
        .rejected { border-left-color: #f44336; }
        .pending { border-left-color: #ff9800; }
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            justify-content: center;
            align-items: center;
            z-index: 1001;
        }
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 10px;
            max-width: 400px;
            width: 90%;
        }
        .password-input {
            width: 100%;
            padding: 10px;
            margin: 15px 0;
            border: 2px solid #667eea;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div id="app">
        <!-- Главная страница с формой -->
        <div id="mainPage" style="display: block;">
            <header>
                <div class="container">
                    <h1>📋 Система Заявок</h1>
                    <nav>
                        <a href="#" class="active" onclick="showPage('mainPage')">📝 Подать заявку</a>
                        <a href="#" onclick="showAdminLogin()">🔐 Админ-панель</a>
                    </nav>
                </div>
            </header>

            <main class="container">
                <div class="form-container">
                    <h2>Подать заявку на должность</h2>
                    <form id="applicationForm" onsubmit="submitApplication(event)">
                        <div class="form-group">
                            <label>Выберите должность:</label>
                            <select id="position" required>
                                <option value="">-- Выберите --</option>
                                <option value="Администратор">Администратор</option>
                                <option value="Модератор">Модератор</option>
                                <option value="Куратор">Куратор</option>
                                <option value="Билдер">Билдер</option>
                                <option value="Тестер">Тестер</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label>Сколько вам лет?</label>
                            <input type="number" id="age" min="14" max="70" required>
                        </div>

                        <div class="form-group">
                            <label>Ваш никнейм:</label>
                            <input type="text" id="nickname" required>
                        </div>

                        <div class="form-group">
                            <label>Discord (username#0000):</label>
                            <input type="text" id="discord" required placeholder="username#0000">
                        </div>

                        <div class="form-group">
                            <label>Опыт работы:</label>
                            <textarea id="experience" rows="3" required></textarea>
                        </div>

                        <div class="form-group">
                            <label>Почему вы хотите эту должность?</label>
                            <textarea id="motivation" rows="3" required></textarea>
                        </div>

                        <button type="submit">📤 Отправить заявку</button>
                    </form>
                </div>
            </main>
        </div>

        <!-- Админ-панель -->
        <div id="adminPage" style="display: none;">
            <header>
                <div class="container">
                    <h1>🔧 Админ-панель</h1>
                    <nav>
                        <a href="#" onclick="showPage('mainPage')">← Назад</a>
                        <a href="#" onclick="loadApplications()">🔄 Обновить</a>
                    </nav>
                </div>
            </header>

            <main class="container">
                <div class="admin-container">
                    <h2>📋 Заявки на рассмотрении</h2>
                    <div id="applicationsList">
                        <!-- Заявки будут здесь -->
                    </div>
                </div>
            </main>
        </div>

        <!-- Модальное окно для пароля -->
        <div id="passwordModal" class="modal">
            <div class="modal-content">
                <h3>🔒 Введите пароль</h3>
                <input type="password" id="adminPassword" class="password-input" placeholder="Пароль администратора">
                <div style="display: flex; gap: 10px; margin-top: 20px;">
                    <button onclick="checkPassword()">Войти</button>
                    <button onclick="hideModal()" style="background: #777;">Отмена</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Данные хранятся в localStorage
        const STORAGE_KEY = 'job_applications';
        const ADMIN_PASSWORD = 'admin123'; // Пароль для доступа

        // Показать/скрыть страницы
        function showPage(pageId) {
            document.getElementById('mainPage').style.display = 'none';
            document.getElementById('adminPage').style.display = 'none';
            document.getElementById(pageId).style.display = 'block';
        }

        // Модальное окно
        function showAdminLogin() {
            document.getElementById('passwordModal').style.display = 'flex';
        }

        function hideModal() {
            document.getElementById('passwordModal').style.display = 'none';
            document.getElementById('adminPassword').value = '';
        }

        // Проверка пароля
        function checkPassword() {
            const password = document.getElementById('adminPassword').value;
            if (password === ADMIN_PASSWORD) {
                hideModal();
                showPage('adminPage');
                loadApplications();
            } else {
                alert('❌ Неверный пароль!');
            }
        }

        // Отправка заявки
        function submitApplication(event) {
            event.preventDefault();
            
            const application = {
                id: Date.now(),
                position: document.getElementById('position').value,
                age: document.getElementById('age').value,
                nickname: document.getElementById('nickname').value,
                discord: document.getElementById('discord').value,
                experience: document.getElementById('experience').value,
                motivation: document.getElementById('motivation').value,
                status: 'pending',
                date: new Date().toLocaleString()
            };

            // Получаем существующие заявки
            let applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            applications.push(application);
            
            // Сохраняем
            localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));
            
            // Очищаем форму
            document.getElementById('applicationForm').reset();
            
            alert('✅ Заявка отправлена! ID: ' + application.id);
        }

        // Загрузка заявок в админ-панели
        function loadApplications() {
            const applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            const container = document.getElementById('applicationsList');
            
            if (applications.length === 0) {
                container.innerHTML = '<p>Нет заявок для рассмотрения</p>';
                return;
            }

            let html = '';
            applications.forEach(app => {
                html += `
                    <div class="application-card ${app.status}">
                        <h3>${app.position} | ${app.nickname} (${app.age} лет)</h3>
                        <p><strong>Discord:</strong> ${app.discord}</p>
                        <p><strong>Опыт:</strong> ${app.experience}</p>
                        <p><strong>Мотивация:</strong> ${app.motivation}</p>
                        <p><small>Подана: ${app.date}</small></p>
                        <div class="admin-controls">
                            <button onclick="updateStatus(${app.id}, 'approved')" style="background: #4CAF50;">
                                ✅ Одобрить
                            </button>
                            <button onclick="updateStatus(${app.id}, 'rejected')" style="background: #f44336;">
                                ❌ Отклонить
                            </button>
                            <button onclick="deleteApplication(${app.id})" style="background: #777;">
                                🗑️ Удалить
                            </button>
                        </div>
                    </div>
                `;
            });
            
            container.innerHTML = html;
        }

        // Обновление статуса заявки
        function updateStatus(id, status) {
            let applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
            applications = applications.map(app => {
                if (app.id === id) {
                    app.status = status;
                }
                return app;
            });
            
            localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));
            loadApplications();
            
            const statusText = status === 'approved' ? 'одобрена' : 'отклонена';
            alert(`Заявка ${statusText}!`);
        }

        // Удаление заявки
        function deleteApplication(id) {
            if (confirm('Удалить эту заявку?')) {
                let applications = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
                applications = applications.filter(app => app.id !== id);
                localStorage.setItem(STORAGE_KEY, JSON.stringify(applications));
                loadApplications();
                alert('Заявка удалена!');
            }
        }

        // Автоматически загружаем заявки при открытии админ-панели
        document.addEventListener('DOMContentLoaded', () => {
            // Проверяем, если кто-то уже в админке
            if (window.location.hash === '#admin') {
                showAdminLogin();
            }
        });
    </script>
</body>
</html>
