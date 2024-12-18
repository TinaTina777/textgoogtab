2:48
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Форма для отправки данных в Google Таблицу</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #f4f4f9;
            padding: 20px;
        }
        form {
            max-width: 500px;
            width: 100%;
            padding: 20px;
            background: white;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            display: flex;
            flex-direction: column;
        }
        label {
            margin-bottom: 8px;
            font-weight: bold;
        }
        select, input, button {
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
            width: 100%;
        }
        button {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h2>Форма для отправки данных в Google Таблицу</h2>
    <form name="submit-to-google-sheet" id="dataForm">
        <label for="month">Выберите месяц:</label>
        <select name="month" id="month" required>
            <option value="Январь">Январь</option>
            <option value="Февраль">Февраль</option>
            <option value="Март">Март</option>
            <!-- другие месяцы -->
            <option value="Декабрь">Декабрь</option>
        </select>

        <label for="user">Выберите пользователя:</label>
        <select name="user" id="user" required>
            <option value="Александр">Александр</option>
            <!-- другие пользователи -->
        </select>

        <label for="personal">Личное:</label>
        <input type="number" name="personal" id="personal" placeholder="Введите значение для Личного" required>

        <label for="family">Семья:</label>
        <input type="number" name="family" id="family" placeholder="Введите значение для Семьи" required>

        <label for="business">Бизнес:</label>
        <input type="number" name="business" id="business" placeholder="Введите значение для Бизнеса" required>

        <label for="request">Запрос:</label>
        <input type="text" name="request" id="request" placeholder="Введите запрос" required>

        <button type="submit">Отправить данные</button>
    </form>

    <div id="responseMessage"></div>

    <script>
        const scriptURL = 'https://script.google.com/macros/s/AKfycbwr7ldAP1HSSyIJDlBsbd3aoyhzPnQuVXYxKbXqBWn8I3lC6UuQCywq_ioWlDuoyZZt/exec';
        const form = document.forms['submit-to-google-sheet'];

        form.addEventListener('submit', e => {
            e.preventDefault();

            fetch(scriptURL, { method: 'POST', body: new FormData(form) })
                .then(response => {
                    document.getElementById("responseMessage").innerText = "Данные успешно отправлены!";
                    form.reset();
                })
                .catch(error => {
                    document.getElementById("responseMessage").innerText = "Произошла ошибка: " + error.message;
                });
        });
    </script>
</body>
</html>
