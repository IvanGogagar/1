## Подключение node.js

```bash
npm init -y
npm i grammy dotenv nodemon
```

Create .env
```javascript
BOT_API_KEY=
```

Main.js
```javascript
require{'dotenv'}.config();
const { Bot } require{'grammy'};

const bot = new Bot(process.env.BOT_API_KEY);
```

## Типы данных
typeof

**boolean** — true, false
**string** — 'text'
**number** — 131
**object** — { a: 31 }
**undefined**
**null**
**symbol** — Symbol('a')
**Bigint** — BigInt(10)

## if else

```js
if (myStatus === 'ready') {
console.log('hello')
} else if (myStatus === 'notReady') {
console.log('goodbye')
} else {
console.log('failed')
}
```

## Функции
Конструктор.метод

```js
function calcAge(year) {
const date = new Date().getFullYear() - year

if (date <= 0) {
    return 'youre loh'
    }
return date
}

console.log(calcAge(2025))
```

### Стрелочные функции

```js
const a = () => {
    console.log('ya gey')
}
```
## Массивы

``` js
const cars = []

console.log(cars.lenght) 
//Сколько в массиве
console.log(cars[0])
//Первый в массиве

for (let = i; i < cars.lenght; i++) {
    console.log(cars[i])
}

for (let car of cars) {
    console.log(car)
}

//Добавить вначало массива/конец
cars.push('gey')
cars.unshift('neGey')

//Удалить/достать
const lastCar = cars.pop()
const firstCar = cars.shift()
console.log(lastCar, firstCar)

// cars.toSorted
// cars.toReversed
```

## Объекты

```js
const person = {
    name: 'dmitriy',
    langs: ['ru', 'eng'],
    isProgrammer: true,
    greet() {
    console.log('hello ddd')
    },
}

console.log(person.name)
person.greet
```

### Delete

```js
delete person.langs
```
## Замыкание

```js
function createMember(firstName) {
	return function (lastName) {
		console.log(firstName + " " + lastName)
	}
}

const logWithLastName = createMember('John')
logWithLastName('Doe')
logWithLastName('Smith')

``` 

## Асинхронность

```js
setTimeout(() => {
	console.log('hihi')
}, 2000)
```
Очистка:
```js
const timeout =
clearTimeout(timeout)
```

```js
setInterval(() => {
	console.log('hihi')
}, 2000)
```

```js
const delay = (wait = 1500) => {
    const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve()
    }, wait)
    })
    return promise
}

delay(2500).then(() => {
    console.log('yep')
})
```

# Страницы
```js
async function allUsers(ctx, page = 0) {
  const currentPage = Number(page) || 0; 
  const limit = 20;
  const offset = currentPage * limit;

  try {
    const users = db.prepare('SELECT id, firstName FROM users LIMIT ? OFFSET ?')
                    .all(limit, offset);

    const totalCountObj = db.prepare('SELECT COUNT(*) as count FROM users').get();
    const totalUsers = totalCountObj ? totalCountObj.count : 0;

    const messageText = users.length > 0 
      ? `<b>Список пользователей (Страница ${currentPage + 1}):</b>\n\n` + 
        users.map(u => `<code>${u.id}</code>: ${u.firstName}`).join('\n')
      : "Пользователей пока нет.";

    const keyboard = new InlineKeyboard();
    
    if (currentPage > 0) {
      keyboard.text('⬅️ Назад', `page_${currentPage - 1}`);
    }
    
    if (offset + limit < totalUsers) {
      keyboard.text('Вперед ➡️', `page_${currentPage + 1}`);
    }

    await ctx.editMessageText(messageText, { 
      reply_markup: keyboard,
      parse_mode: 'HTML' 
    });

    await ctx.answerCallbackQuery().catch(() => {}); 
  } catch (err) {
    console.error("Ошибка в showUsers:", err);
    await ctx.reply("Произошла ошибка при загрузке списка.");
  }
}
```

1. Объявление функции
```js
async function allUsers(ctx, page = 0) { ... }
```

`async`: Говорит, что функция асинхронная (внутри будет await).

`ctx`: Объект контекста Telegram. В нем всё: кто нажал кнопку, какой текст сообщения и т.д.

`page = 0`: Аргумент «номер страницы». По умолчанию равен 0 (первая страница), если ничего не передали.


2. Подготовка цифр (Математика пагинации)

`Number(page) || 0`: Гарантируем, что в currentPage будет число. Если в page прилетел мусор или undefined, запишется 0.

`limit = 20`: Сколько юзеров мы хотим видеть на одном «экране».

`offset = currentPage * limit`: Отступ. Если страница 0, отступ 0. Если страница 1, отступ 20 (пропускаем первых 20 и показываем следующих).


3. Работа с базой данных (Блок try)
`const users = db.prepare('... LIMIT ? OFFSET ?').all(limit, offset);`

`SELECT id, firstName FROM users`: Выбрать поля ID и Имя.

`LIMIT ?`: Возьми только столько строк (в нашем случае 20).

`OFFSET ?`: Пропусти столько-то строк от начала.

`.all(limit, offset)`: Подставляет наши цифры вместо знаков ? и выполняет запрос.

`const totalCountObj = db.prepare('SELECT COUNT(*) as count FROM users').get();`

`COUNT(*)`: Считает, сколько всего людей в таблице. Это нужно, чтобы бот понял, есть ли смысл рисовать кнопку «Вперед».

`.get()`: Возвращает одну строку (объект), а не массив.


4. Формирование текста

`${currentPage + 1}`: Для программиста страницы начинаются с 0, но пользователю мы пишем «Страница 1», поэтому прибавляем единицу.

`users.map(...)`: Превращаем объекты из базы в красивые строчки.

`<code>${u.id}</code>`: Тег HTML, который делает текст ID «моноширинным» (как код), его удобно копировать в Telegram одним нажатием.


5. Логика кнопок (Клавиатура)
`if (currentPage > 0)`

Если мы не на самой первой странице, рисуем кнопку «Назад». В данные кнопки (callback_data) записываем page_ и номер предыдущей страницы.

`if (offset + limit < totalUsers)`

Если текущий отступ + 20 всё еще меньше, чем общее кол-во людей в базе — значит, впереди есть еще кто-то. Рисуем кнопку «Вперед».


6. Отправка в Telegram

`ctx.editMessageText`: Не присылает новое сообщение, а меняет старое (чтобы чат не превращался в помойку из списков).

`parse_mode: 'HTML'`: Обязательный параметр, чтобы Telegram понял теги `<b>` и `<code>`.

`ctx.answerCallbackQuery()`: Убирает «часики» или анимацию загрузки на кнопке после нажатия.

```js
bot.callbackQuery(/^page_(\d+)$/, async (ctx) => {
  const pageToOpen = parseInt(ctx.match[1], 10);
  await allUsers(ctx, pageToOpen, db);
});
```

7. Обработчик нажатия `(bot.callbackQuery)`
`bot.callbackQuery(/^page_(\d+)$/, ...)`

`/^page_(\d+)$/`: Регулярное выражение. Ловит все нажатия кнопок, которые начинаются на page_ и заканчиваются цифрами.

`ctx.match[1]`: Это та самая цифра, которую мы вытащили из названия кнопки.

`parseInt(..., 10)`: Превращаем строку "1" в реальное число 1 для базы данных.
# code-server --auth none