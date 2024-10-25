2:26
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
    <form id="dataForm">
        <!-- Выбор месяца -->
        <label for="month">Выберите месяц:</label>
        <select id="month" required>
            <option value="Январь">Январь</option>
            <option value="Февраль">Февраль</option>
            <option value="Март">Март</option>
            <option value="Апрель">Апрель</option>
            <option value="Май">Май</option>
            <option value="Июнь">Июнь</option>
            <option value="Июль">Июль</option>
            <option value="Август">Август</option>
            <option value="Сентябрь">Сентябрь</option>
            <option value="Октябрь">Октябрь</option>
            <option value="Ноябрь">Ноябрь</option>
            <option value="Декабрь">Декабрь</option>
        </select>

        <!-- Выбор пользователя -->
        <label for="user">Выберите пользователя:</label>
        <select id="user" required>
            <option value="Александр">Александр</option>
            <option value="Ирина">Ирина</option>
            <option value="Константин">Константин</option>
            <option value="Виктор">Виктор</option>
            <option value="Елена">Елена</option>
            <option value="Сергей">Сергей</option>
            <option value="Андрей">Андрей</option>
            <option value="Варвара">Варвара</option>
            <option value="Дмитрий">Дмитрий</option>
            <option value="Виталий">Виталий</option>
            <option value="Антон">Антон</option>
        </select>

        <!-- Поля для ввода данных -->
        <label for="personal">Личное:</label>
        <input type="number" id="personal" placeholder="Введите значение для Личного" required>

        <label for="family">Семья:</label>
        <input type="number" id="family" placeholder="Введите значение для Семьи" required>

        <label for="business">Бизнес:</label>
        <input type="number" id="business" placeholder="Введите значение для Бизнеса" required>

        <label for="request">Запрос:</label>
        <input type="text" id="request" placeholder="Введите запрос" required>

        <button type="button" onclick="submitData()">Отправить данные</button>
    </form>

    <div id="responseMessage"></div>

    <script>
        // Функция для отправки данных на сервер
        async function submitData() {
            const month = document.getElementById("month").value;
            const user = document.getElementById("user").value;
            const personal = document.getElementById("personal").value;
            const family = document.getElementById("family").value;
            const business = document.getElementById("business").value;
            const request = document.getElementById("request").value;

            const url = "https://script.google.com/macros/s/AKfycbycIe3CC5ME84JjTyWF8zmtIn6fNUMSHwLHaP_qRUubj0DApLkVzAT3Ai2c0qGGLf_r/exec";

            try {
                const response = await fetch(url, {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({
                        month: month,
                        user: user,
                        personal: personal,
                        family: family,
                        business: business,
                        request: request
                    })
                });

                // Проверка статуса ответа
                if (!response.ok) {
                    throw new Error(`Ошибка: ${response.status} ${response.statusText}`);
                }

                const result = await response.json();
                document.getElementById("responseMessage").innerText = result.message || "Данные успешно отправлены!";
            } catch (error) {
                document.getElementById("responseMessage").innerText = "Произошла ошибка: " + error.message;
            }
        }
    </script>
</body>
</html>
