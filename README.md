# Todo-list2
Обновленный Тодо-лист 

Данный код на JavaScript представляет собой простой список дел (todo list), который может добавлять новые задачи, помечать их как выполненные или важные, а также сохранять состояние списка в локальном хранилище браузера.

Давайте разберем код по частям:

Определение переменных:
let addMessage = document.querySelector('.message'),
    addButton = document.querySelector('.add'),
    todo = document.querySelector('.todo')

let todoList = []

Здесь объявляются переменные addMessage, addButton и todo, которые будут использоваться для работы с элементами на странице. Переменная todoList представляет собой массив, в котором будут храниться объекты задач.

1. Загрузка данных из локального хранилища:
if(localStorage.getItem('todo')) {
    todoList = JSON.parse(localStorage.getItem('todo'))
    displayMessages()
}

При загрузке страницы проверяется, есть ли данные в локальном хранилище с ключом 'todo'. Если такие данные существуют, они извлекаются, парсятся из JSON и сохраняются в переменной todoList. Затем вызывается функция displayMessages(), чтобы отобразить задачи на странице.

2. Добавление задачи по нажатию кнопки:
   addButton.addEventListener('click', function(){
    let newTodo = {
        todo: addMessage.value,
        checked: false,
        important: false,
    }
    todoList.push(newTodo)
    displayMessages()

    localStorage.setItem('todo', JSON.stringify(todoList))
})

По клику на кнопку с классом .add, создается новый объект newTodo, представляющий задачу. Этот объект содержит текст задачи, а также два булевых свойства checked (показывает, выполнена ли задача) и important (показывает, является ли задача важной). Затем этот объект добавляется в массив todoList, вызывается функция displayMessages() для обновления отображения и список задач сохраняется в локальное хранилище.

3. Отображение задач:
 function displayMessages() {
    let displayMessage = ''
    todoList.forEach(function(item, i){
        displayMessage += `
        <li>
        <input type='checkbox' id='item_${i}' ${item.checked ? 'checked' : ''}>
        <label for='item_${i}'>${item.todo}</label>
        </li>
        `;
        todo.innerHTML = displayMessage;
    });
}
Функция displayMessages() обходит массив todoList и для каждого элемента создает HTML-разметку, представляющую задачу. Если задача отмечена как выполненная (checked равно true), соответствующий чекбокс будет отмечен. Затем весь сформированный HTML добавляется внутрь контейнера todo.

4. Обработка изменения состояния задачи:
   todo.addEventListener('change', function(event){
    let valueLabel = todo.querySelector('[for='+ event.target.getAttribute('id') +']').innerHTML
    
    todoList.forEach(function(item){
        if(item.todo === valueLabel){
            item.checked = !item.checked
            localStorage.setItem('todo', JSON.stringify(todoList))
        }
    })
})

При изменении состояния чекбокса (по клику на него) вызывается обработчик события. Этот обработчик ищет соответствующую метку (label) по атрибуту for у чекбокса. Затем он находит задачу в todoList, которая соответствует этой метке, меняет её состояние выполнения на противоположное и обновляет данные в локальном хранилище.

Этот код создает функциональность простого списка задач с возможностью добавления, отметки выполнения и сохранения данных в локальном хранилище браузера.
