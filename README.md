1:52
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Форма записи в Google Таблицу</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #f4f4f9;
            height: 100vh;
            margin: 0;
        }
        .form-container {
            background: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 100%;
        }
        label {
            font-weight: bold;
            display: block;
            margin-bottom: 5px;
        }
        input, select {
            width: 100%;
            padding: 8px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <div class="form-container">
        <h2>Заполните данные</h2>
        <form id="googleSheetForm">
            <label for="name">Имя</label>
            <input type="text" id="name" name="name" required>

            <label for="personal">Личное</label>
            <input type="number" id="personal" name="personal" min="0" required>

            <label for="family">Семья</label>
            <input type="number" id="family" name="family" min="0" required>

            <label for="business">Бизнес</label>
            <input type="number" id="business" name="business" min="0" required>

            <label for="request">Запрос</label>
            <input type="text" id="request" name="request">

            <label for="month">Месяц</label>
            <select id="month" name="month" required>
                <option value="Январь">Январь</option>
                <option value="Февраль">Февраль</option>
                <option value="Март">Март</option>
                <!-- Добавьте остальные месяцы, если необходимо -->
            </select>

            <button type="button" onclick="submitToGoogleSheets()">Отправить</button>
        </form>
    </div>

    <script>
        function submitToGoogleSheets() {
            const data = {
                name: document.getElementById('name').value,
                personal: document.getElementById('personal').value,
                family: document.getElementById('family').value,
                business: document.getElementById('business').value,
                request: document.getElementById('request').value,
                month: document.getElementById('month').value
            };

            fetch('https://script.google.com/macros/s/AKfycbxvUy9qupQcOtNRb5xMo3vgLAEHjizBphzrxd3NjXKxPzM9FpLZKEz9Es8et7qYqqRA/exec', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(data),
            })
            .then(response => response.text())
            .then(result => {
                alert('Данные успешно отправлены!');
                document.getElementById('googleSheetForm').reset(); // Очистка формы после отправки
            })
            .catch(error => alert('Ошибка отправки данных: ' + error));
        }
    </script>
</body>
</html>
