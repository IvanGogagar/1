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