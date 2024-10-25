2:17
<html lang="ru">
<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>Форма для заполнения таблицы Google</title>
    <style>
        * {
            -webkit-user-select: none;
            user-select: none;
            box-sizing: border-box;
        }
        body {
            margin: 0;
            color: black;
            background-color: #f4f4f9;
            display: flex;
            flex-direction: column;
            align-items: center;
            font-family: Arial, sans-serif;
        }
        main {
            max-width: 600px;
            width: 100%;
            padding: 20px;
            margin: 20px;
            background: white;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        label {
            font-weight: bold;
            margin-bottom: 5px;
            display: block;
        }
        input, select {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background-color: #4caf50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
        }
        button:hover {
            background-color: #45a049;
        }
        .output {
            margin-top: 20px;
            padding: 20px;
            background-color: #eaeaea;
            border-radius: 8px;
            width: 100%;
        }
    </style>
</head>
<body>
<main>
    <h2>Форма для заполнения таблицы Google</h2>
    
    <label for="user">Введите имя:</label>
    <input type="text" id="user" placeholder="Имя" required />

    <label for="month">Выберите месяц:</label>
    <select id="month" required>
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
        <option value="Январь">Январь</option>
        <option value="Февраль">Февраль</option>
    </select>

    <label for="personal">Личное:</label>
    <input type="number" id="personal" placeholder="Введите значение" required />

    <label for="family">Семья:</label>
    <input type="number" id="family" placeholder="Введите значение" required />

    <label for="business">Бизнес:</label>
    <input type="number" id="business" placeholder="Введите значение" required />

    <label for="request">Запрос:</label>
    <input type="text" id="request" placeholder="Введите запрос" required />

    <button onclick="submitForm()">Отправить</button>

    <div class="output" id="output"></div>
</main>

<script>
    const apiUrl = 'https://script.google.com/macros/s/AKfycbxvUy9qupQcOtNRb5xMo3vgLAEHjizBphzrxd3NjXKxPzM9FpLZKEz9Es8et7qYqqRA/exec';

    const submitForm = async () => {
        const user = document.getElementById('user').value;
        const month = document.getElementById('month').value;
        const personal = document.getElementById('personal').value;
        const family = document.getElementById('family').value;
        const business = document.getElementById('business').value;
        const request = document.getElementById('request').value;

        const data = {
            user: user,
            month: month,
            personal: personal,
            family: family,
            business: business,
            request: request
        };

        try {
            const response = await fetch(apiUrl, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            });

            const result = await response.json();
            document.getElementById('output').innerHTML = result.message;
        } catch (error) {
            console.error('Ошибка:', error);
            document.getElementById('output').innerHTML = 'Произошла ошибка: ' + error.message;
        }
    };
</script>
</body>
</html>
