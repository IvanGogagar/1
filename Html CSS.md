[[Шаблонство]]
## Head
Подключение файла со стилями:
```css
<head>
	<link rel="stylesheet" href="style.css">
</head>
```


## FlexBox CSS

``` css
display: inline-flex;
```

``` css
justify-content: space-between;
```
Растягивает элементы по всей ширине

``` css
justify-content: space-around; 
```
Растягивает, но отступы по бокам


``` css
align-items: flex-start;
```
К верху
```css
align-items: fles-end;
```
К низу

``` css
align-content: center;
```
Тоже центрирование контента чи шо

``` css
colum-gap
row-gap
```
Расстояние между колонками


## Переменные

Переменные пишутся так:
```css
--variable-name:
```

Используется:
```css
Color: var(--name);
```

Пример:
```css
:root {
	--primary: #FF00AA
}
```

## Позиционирование

```css
position: relative;
```
top, left, right, bottom.
```css
position: absolute;
```
```css
z-index
```

## Медиатеги
```css
<img src="" alt"Cannot find imege">
```

Надпись под изображение:
```css
<figure>
	<img src="meme.png"/>
	<figcaption>text</figcaption>
<figure>
```

Оптимизация качества изображения:
```css
<picture>
	<img src="small"/>
	<source
		media="(min-width: 700px)"
		srcset="big.png"
	>
</picture>
```

### Видео
```css
<video>
	<source src="wow.mp4"
	type="video/mp4">
	Ваш браузер не поддерживает такой формат видео
</video>
```
**Атрибуты:**
whidth
height

Превью:
```css
<video poster="thumb.png">
```

### Аудио
```css
<audio>
	<source src="voice.mp3"
	type="audio/mpeg"
	>
	Гг не загрузило у тебя брат
</audio>
```

### Видио аудио атрибуты
1. controls - управление
```css
<audio controls>
```

2. controlslist
```css
controlslist="nodownload", "nofullscreen"
```

3. autoplay

4. preload="auto"
preload="metadata"

5. muted








## CSS Transform
```css
transform:
Translate(10px 10px)
;
```

## Анимации

```css
button {
	transition-property: background;
	transition-duration: 0.3s;
	transition-timing-function: ease;
	transition-timing-function: cubic-bezier(0, 0, 0, 0);
}
```

```css
@keyframes first {
	from {
		transform: translateX(0px);
	}
	
	to {
		transform: translateX(200px);
	}
}

button {
	animation-name: first;
	animation-duration: 3s;
	animation-timing-function: ease-in;
	animation-delay: 2s;
	animation-iteration-count: infinite;
	animation-direction: alternative-reverse;
}
```






[[JavaScript]]