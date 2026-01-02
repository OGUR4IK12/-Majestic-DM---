<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Заявки на персонал</title>

<style>
body{
    background:#0f0f0f;
    color:white;
    font-family:Arial;
    padding:20px;
}
input, select, textarea, button{
    width:100%;
    padding:8px;
    margin:6px 0;
}
button{
    background:limegreen;
    border:none;
    cursor:pointer;
}
.app{
    border:1px solid #555;
    padding:10px;
    margin-top:10px;
}
</style>
</head>

<body>

<h1>Заявка на должность</h1>

<form id="form">
    Никнейм:
    <input id="nick" required>

    Возраст:
    <input type="number" id="age" required>

    Должность:
    <select id="role">
        <option>Администратор</option>
        <option>Модератор</option>
        <option>Куратор</option>
        <option>Билдер</option>
        <option>Тестер</option>
    </select>

    Почему именно ты?
    <textarea id="text"></textarea>

    <button>Отправить</button>
</form>

<hr>

<button onclick="openAdmin()">Рассмотреть заявки</button>

<div id="admin" style="display:none;">
    <h2>Заявки</h2>
    <div id="list"></div>
</div>

<script>
const PASSWORD = "1234"; // ← СМЕНИ ПАРОЛЬ

let apps = JSON.parse(localStorage.getItem("apps")) || [];

form.onsubmit = e => {
    e.preventDefault();
    apps.push({
        nick:nick.value,
        age:age.value,
        role:role.value,
        text:text.value,
        status:"На рассмотрении"
    });
    localStorage.setItem("apps", JSON.stringify(apps));
    alert("Заявка отправлена");
    form.reset();
};

function openAdmin(){
    if(prompt("Пароль") !== PASSWORD) return alert("Нет доступа");
    admin.style.display="block";
    render();
}

function render(){
    list.innerHTML="";
    apps.forEach((a,i)=>{
        list.innerHTML += `
        <div class="app">
        <b>${a.nick}</b> | ${a.age} лет<br>
        Должность: ${a.role}<br>
        Текст: ${a.text}<br>
        Статус: ${a.status}<br><br>
        <button onclick="ok(${i})">Одобрить</button>
        <button onclick="no(${i})">Отказать</button>
        </div>`;
    });
}

function ok(i){
    apps[i].status="Одобрено";
    save();
}
function no(i){
    apps[i].status="Отказано";
    save();
}
function save(){
    localStorage.setItem("apps", JSON.stringify(apps));
    render();
}
</script>

</body>
</html>
