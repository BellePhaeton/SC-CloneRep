<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Генератор BBCode</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            color: #333;
        }
        .container {
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        input, textarea {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        input.error, textarea.error {
            border-color: red;
        }
        button {
            padding: 10px 15px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:disabled {
            background-color: gray;
        }
    </style>
</head>
<body>
  <div class="container">
    <h1>Генератор HTML сообщений</h1>
    <h4>Все поля обязательны к заполнению, если в поле не указано иное. </h4>
    <form id="messageForm">
        <label>Фандом (англ.): <input type="text" id="fandomEn" placeholder="Фандом на англ" required></label><br>
        <label>Ссылка на анкету: <input type="url" id="profileLink" placeholder="Ссылка на вашу опубликованную анкету" required></label><br>
        <label>Имя Фамилия (рус.): <input type="text" id="nameRu" placeholder="Имя Фамилия вашего персонажа на русском" required></label><br>
        <label>Ваш текст личного звания: <textarea id="personalTitle" maxlength="300" placeholder="Оставьте здесь некоторое высказывание(не более 300 символов)"></textarea></label><br>
        <label>Ссылка на пару: <input type="url" id="coupleLink" placeholder="Ссылка на профиль вашей пары(Если она у вас есть. Поле необязательное)"></label><br>
        <label>Имя пары: <input type="text" id="coupleName" placeholder="Имя вашей пары как как в её профиле (По наличию и необходимости, поле необязательное)" ></label><br>
<label>Лучей (Поставьте галочку, если пришли по заявке в "Жди меня): <input type="number" id="rays" value="100" min="100" readonly></label>
        <label><input type="checkbox" id="waitingCheckbox" style="Margin-top: -85px; margin-left: 200px"></label><br>
        <label>Фандом (капсом): <input type="text" id="fandomCaps" required placeholder="Фандом на англ"></label><br>
        <label>Фандом (рус.): <input type="text" id="fandomRu" required placeholder="Фандом на русском"></label><br>
        <label>Ссылка на профиль: <input type="url" id="profileLink2" placeholder="Ссылка на ваш профиль(не анкету)" required></label><br>
        <label>Имя Фамилия (англ.): <input type="text" id="nameEn" placeholder="Имя Фамилия вашего персонажа на английском" required></label>
        <label>Имя Фамилия (рус.): <input type="text" id="nameRu2" placeholder="Имя Фамилия вашего персонажа на русском" required></label><br>
        <button type="button" id="generateButton">Сгенерировать HTML</button>
    </form>
    <div id="outputTags"></div>

    <script>
        document.getElementById('waitingCheckbox').addEventListener('change', function() {
            document.getElementById('rays').value = this.checked ? 700 : 100;
        });

        document.getElementById('generateButton').addEventListener('click', function() {
            try {
                const fandomEn = document.getElementById('fandomEn').value.trim().toLowerCase();
                const profileLink = document.getElementById('profileLink').value.trim();
                const nameRu = document.getElementById('nameRu').value.trim();
                const personalTitle = document.getElementById('personalTitle').value.trim();
                const coupleLink = document.getElementById('coupleLink').value.trim();
                const coupleName = document.getElementById('coupleName').value.trim();
                const rays = document.getElementById('rays').value;
                const fandomCaps = document.getElementById('fandomCaps').value.trim().toUpperCase();
                const fandomRu = document.getElementById('fandomRu').value.trim().toLowerCase();
                const profileLink2 = document.getElementById('profileLink2').value.trim();
                const nameEn = document.getElementById('nameEn').value.trim().toLowerCase();
                const nameRu2 = document.getElementById('nameRu2').value.trim().toLowerCase();

                // Проверка обязательных полей
                if (!fandomEn || !profileLink.startsWith('https://sunnycross.ru') || !nameRu || !fandomCaps || !fandomRu || !profileLink2) {
                    throw new Error('Пожалуйста, заполните все обязательные поля корректно.');
                }

                const outputHTML = `
<div class="fandom">${fandomEn}</div>
<div class="name"><a href="${profileLink}">${nameRu}</a></div>
<div class="lz">${personalTitle}</div>
<a href="${coupleLink}"><b>${coupleName}</b></a>
<div class="shine">лучей: <br>${rays}</div>
<tr>
<td><div class="role">• ${fandomCaps}</div>
<div class="subrole">${fandomRu}</div></td>
<td><div class="subrole"><br><a href="${profileLink2}">${nameEn} • ${nameRu2}</a></div></td>
</tr>
<br><a href="${profileLink2}">${nameEn} • ${nameRu2}</a>`;

                document.getElementById('outputTags').innerText = outputHTML;

                // Копирование в буфер обмена
                navigator.clipboard.writeText(outputHTML).then(() => {
                    const button = document.getElementById('generateButton');
                    button.innerText = 'Скопировано';
                    button.classList.add('button-disabled');
                    setTimeout(() => {
                        button.innerText = 'Сгенерировать HTML';
                        button.classList.remove('button-disabled');
                    }, 4000);
                });
            } catch (error) {
                alert(error.message);
            }
        });
    </script>
    </div>
<div class="container">
    <h1>Генератор BBCode</h1>
    <input type="text" id="imgLink1" placeholder="Ссылка на изображение с внешностью (1)" required>
    <input type="text" id="imgLink2" placeholder="Ссылка на изображение с внешностью (2)" required>
    <input type="text" id="fandomEng" placeholder="Фандом на англ" required>
    <input type="text" id="fandomRus" placeholder="Фандом на русск." required>
    <input type="text" id="appearanceEng" placeholder="внешность на англ." required>
    <input type="text" id="nameEng" placeholder="Имя Фамилия на англ." required>
    <input type="text" id="nameRus" placeholder="Имя Фамилия на русск." required>
    <input type="text" id="applicationLink" placeholder="Ссылка на заявку:" required>
    <textarea id="bioExcerpt" placeholder="Выдержка из досье" required></textarea>
    <input type="text" id="contact" placeholder="Связь:" required>
    <input type="text" id="twinks" placeholder="Твинки:" required>
    <textarea id="roleplay" placeholder="Отыгрыш вашего персонажа в альте другим игроком: Согласны/Не согласны/при уведомлении. 

Помните, что отыгрыш, начатый до вашего прихода, в расчет не берется." required style="max-width: 600px"></textarea>
    <textarea id="trialPost" placeholder="Пробный пост:" required></textarea>
    <button id="generateBtn">Сгенерировать</button>
    <textarea id="outputBBCode" placeholder="Сгенерированный BBCode" readonly></textarea>
</div>
<script>
    document.getElementById('generateBtn').addEventListener('click', function() {
        const fields = [
            'fandomEng', 'fandomRus', 'appearanceEng', 
            'nameEng', 'nameRus', 'applicationLink', 
            'bioExcerpt', 'contact', 'twinks', 
            'roleplay', 'trialPost', 'imgLink1',
            'imgLink2'
        ];
        
        let isValid = true;
        fields.forEach(field => {
            const input = document.getElementById(field);
            if (!input.value.trim()) {
                input.classList.add('error');
                isValid = false;
            } else {
                input.classList.remove('error');
            }
        });

        if (!isValid) {
            alert('Пожалуйста, заполните все обязательные поля.');
            return;
        }

        try {
            const bbCode = `
[align=center][size=23][font=Palatino Lynotipe][i]${document.getElementById('fandomEng').value} // ${document.getElementById('fandomRus').value}[/i][/font][/size][/align]
[align=center][img]${document.getElementById('imgLink1').value}[/img] [img]${document.getElementById('imgLink2').value}[/img]
[font=Book Antiqua][size=12]${document.getElementById('appearanceEng').value}[/size][/font][/align]
[align=center][size=20][b][font=Georgia]${document.getElementById('nameEng').value}[/font][/b][/size]
[size=16][b][font=Book Antiqua]${document.getElementById('nameRus').value}[/font][/b][/size][/align]
[table layout=fixed width=100%]
[tr]
[td][/td]
[td width=470px]
[hr]
[font=Georgia][b][size=15]Ссылка на заявку: [/size][/b][/font] ${document.getElementById('applicationLink').value} [/td]
[td][/td]
[/tr]
[/table]
[hr]
[align=center][b][size=20][font=Georgia]Выдержка из досье[/font][/size][/b][/align]

${document.getElementById('bioExcerpt').value}

[hr]
[font=Georgia][b][size=15]Связь: [/size][/b][/font] [hide=999999]${document.getElementById('contact').value}[/hide]
[font=Georgia][b][size=15]Твинки: [/size][/b][/font] [hide=9999999]${document.getElementById('twinks').value}[/hide]
[font=Georgia][b][size=15]Отыгрыш вашего персонажа в альте другим игроком: [/size][/b][/font] ${document.getElementById('roleplay').value}
[spoiler="[font=Georgia][size=17][align=center]Пробный пост[/align][/size][/font]"]${document.getElementById('trialPost').value}[/spoiler]
            `;
            document.getElementById('outputBBCode').value = bbCode;
            copyToClipboard(bbCode);
        } catch (error) {
            console.error('Ошибка при генерации BBCode:', error);
            alert('Произошла ошибка при генерации BBCode. Пожалуйста, попробуйте еще раз.');
        }
    });

    function copyToClipboard(text) {
        navigator.clipboard.writeText(text).then(() => {
            const button = document.getElementById('generateBtn');
            button.disabled = true;
            button.textContent = 'Скопировано';
            setTimeout(() => {
                button.disabled = false;
                button.textContent = 'Сгенерировать';
            }, 4000);
        }).catch(err => {
            console.error('Ошибка при копировании в буфер обмена:', err);
            alert('Не удалось скопировать текст. Пожалуйста, попробуйте вручную.');
        });
    }
</script>

</body>
</html>
