<script>
const STORAGE_KEY = 'majestic_dm_applications';
const ADMIN_PASSWORD = 'MDM1234';

/* ===== Навигация ===== */
function showPage(page) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    if (page === 'main') document.getElementById('mainPage').classList.add('active');
}

/* ===== Модалка ===== */
function showAdminLogin() {
    document.getElementById('passwordModal').classList.add('active');
}
function hideModal() {
    document.getElementById('passwordModal').classList.remove('active');
    document.getElementById('adminPassword').value = '';
}

/* ===== Проверка пароля ===== */
function checkPassword() {
    const pass = document.getElementById('adminPassword').value;
    if (pass !== ADMIN_PASSWORD) {
        alert('❌ Неверный пароль');
        return;
    }

    hideModal();
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById('adminPage').classList.add('active');
    loadApplications();
}

/* ===== Доп вопросы ===== */
let questionsVisible = false;
function toggleQuestions() {
    questionsVisible = !questionsVisible;
    document.getElementById('hiddenQuestions').classList.toggle('show');
}

/* ===== Возраст ===== */
function validateAge(input) {
    const age = +input.value;
    input.style.borderColor = (age >= 12 && age <= 18) ? '#00ced1' : '#ff4444';
}

/* ===== Отправка заявки ===== */
document.getElementById('applicationForm').addEventListener('submit', e => {
    e.preventDefault();

    const age = +ageInput.value;
    if (age < 12 || age > 18) return alert('Возраст 12–18');

    const app = {
        id: Date.now(),
        position: position.value,
        age,
        nickname: nickname.value,
        telegram: telegram.value,
        time: time.value,
        experience: experience.value,
        whyUs: whyUs.value,
        rulesKnowledge: rulesKnowledge.value,
        cheaterScenario: cheaterScenario.value,
        conflictScenario: conflictScenario.value,
        ideas: ideas.value,
        strengths: strengths.value,
        weaknesses: weaknesses.value,
        teamwork: teamwork.value,
        builderPortfolio: builderPortfolio.value,
        testerMethod: testerMethod.value,
        scripterSkills: scripterSkills.value,
        goals: goals.value,
        status: 'На рассмотрении'
    };

    const data = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
    data.push(app);
    localStorage.setItem(STORAGE_KEY, JSON.stringify(data));

    alert('✅ Заявка отправлена');
    e.target.reset();
});

/* ===== Загрузка заявок ===== */
function loadApplications() {
    const list = document.getElementById('applicationsList');
    const data = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
    list.innerHTML = '';

    document.getElementById('totalCount').textContent = data.length;
    document.getElementById('pendingCount').textContent =
        data.filter(a => a.status === 'На рассмотрении').length;

    data.forEach(app => {
        list.innerHTML += `
        <div class="application-card">
            <div class="application-header">
                <b>${app.nickname}</b>
                <span class="application-status status-pending">${app.status}</span>
            </div>
            <p><b>Должность:</b> ${app.position}</p>
            <p><b>Возраст:</b> ${app.age}</p>
            <p><b>Telegram:</b> ${app.telegram}</p>

            <div class="admin-controls">
                <button class="btn btn-approve btn-sm" onclick="setStatus(${app.id}, 'Одобрено')">Одобрить</button>
                <button class="btn btn-reject btn-sm" onclick="setStatus(${app.id}, 'Отказано')">Отказать</button>
                <button class="btn btn-delete btn-sm" onclick="removeApp(${app.id})">Удалить</button>
            </div>
        </div>`;
    });
}

/* ===== Управление ===== */
function setStatus(id, status) {
    const data = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
    const app = data.find(a => a.id === id);
    if (app) app.status = status;
    localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
    loadApplications();
}

function removeApp(id) {
    let data = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];
    data = data.filter(a => a.id !== id);
    localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
    loadApplications();
}
</script>
