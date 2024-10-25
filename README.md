<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Заполнение Google Таблицы</title>
    <style>
        body { font-family: Arial, sans-serif; display: flex; align-items: center; justify-content: center; background-color: #f4f4f9; min-height: 100vh; margin: 0; }
        main { background: #fff; padding: 20px; border-radius: 8px; box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); max-width: 400px; width: 100%; }
        h2 { text-align: center; }
        label, select, input { display: block; width: 100%; margin-bottom: 15px; }
        input, select { padding: 10px; font-size: 16px; border: 1px solid #ccc; border-radius: 5px; }
        button { background-color: #4caf50; color: white; padding: 10px; border: none; border-radius: 5px; cursor: pointer; width: 100%; font-size: 16px; }
        button:hover { background-color: #45a049; }
        .output { text-align: center; font-weight: bold; margin-top: 20px; }
    </style>
</head>
<body>
<main>
    <h2>Форма для записи в Google Таблицу</h2>
    <form id="dataForm">
        <label for="name">Имя:</label>
        <select id="name" required>
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

        <label for="personal">Личное:</label>
        <input type="number" id="personal" required>

        <label for="family">Семья:</label>
        <input type="number" id="family" required>

        <label for="business">Бизнес:</label>
        <input type="number" id="business" required>

        <label for="request">Запрос:</label>
        <input type="text" id="request" placeholder="Нет запроса" required>

        <button type="submit">Отправить</button>
    </form>

    <div class="output" id="responseMessage"></div>
</main>

<script>
    document.getElementById('dataForm').addEventListener('submit', async function(event) {
        event.preventDefault();

        // Получаем значения полей формы
        const name = document.getElementById('name').value;
        const personal = document.getElementById('personal').value;
        const family = document.getElementById('family').value;
        const business = document.getElementById('business').value;
        const request = document.getElementById('request').value || "Нет запроса";

        // ID таблицы и листа
        const spreadsheetId = "1qSya9Mvs9TtyhHAh0EoZebhWlA535QWbEqEePVXDp9w";
        const apiKey = "AIzaSyD0ymAEWCCWBBtsx6C8HWJpmArxSM3CeVQ";
        const sheetName = "Март";

        // URL для отправки данных на Google Sheets
        const url = `https://sheets.googleapis.com/v4/spreadsheets/${spreadsheetId}/values/${sheetName}!A1:E1:append?valueInputOption=USER_ENTERED&key=${apiKey}`;

        // Данные для отправки
        const rowData = [[name, personal, family, business, request]];

        try {
            // Отправка данных через fetch
            const response = await fetch(url, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ values: rowData })
            });

            // Обработка ответа
            const result = await response.json();
            if (response.ok) {
                document.getElementById('responseMessage').textContent = 'Данные успешно отправлены!';
            } else {
                document.getElementById('responseMessage').textContent = `Ошибка: ${result.error.message}`;
            }
        } catch (error) {
            document.getElementById('responseMessage').textContent = `Ошибка: ${error.message}`;
        }
    });
</script>
</body>
</html>
