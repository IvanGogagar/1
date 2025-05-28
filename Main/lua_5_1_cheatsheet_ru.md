
# 🌀 Lua 5.1 — Краткая выжимка

Полезная шпаргалка и база для Obsidian. Всё самое нужное — компактно и на русском.

---

## 🔹 Переменные и типы

```lua
local a = 10       -- локальная переменная
b = "привет"       -- глобальная переменная (по умолчанию)
print(type(a))     -- number
print(type(b))     -- string
```

- `nil`, `boolean`, `number`, `string`, `table`, `function`, `userdata`, `thread`

---

## 🔹 Управляющие конструкции

```lua
if x > 0 then
  print("Положительное")
elseif x == 0 then
  print("Ноль")
else
  print("Отрицательное")
end

for i = 1, 5 do
  print(i)
end

while a < 10 do
  a = a + 1
end

repeat
  x = x - 1
until x == 0
```

---

## 🔹 Таблицы (основа всего в Lua)

```lua
t = {name = "Олег", age = 18}
print(t.name)        -- Олег
t["country"] = "RU"

arr = {1, 2, 3}
print(arr[1])        -- 1 (индексация с 1)
```

- Таблицы — универсальный тип: и массив, и словарь, и объект.

```lua
for k, v in pairs(t) do
  print(k, v)
end
```

---

## 🔹 Функции

```lua
function say_hi(name)
  print("Привет, " .. name)
end

say_hi("Олег")
```

- Замыкания:

```lua
function make_counter()
  local count = 0
  return function()
    count = count + 1
    return count
  end
end

c = make_counter()
print(c()) -- 1
print(c()) -- 2
```

---

## 🔹 Работа с файлами

```lua
local f = io.open("test.txt", "w")
f:write("Привет, файл!")
f:close()
```

Чтение:

```lua
for line in io.lines("test.txt") do
  print(line)
end
```

---

## 🔹 Модули

```lua
-- mymodule.lua
local M = {}
function M.say_hello()
  print("Привет из модуля!")
end
return M
```

```lua
local m = require("mymodule")
m.say_hello()
```

---

## 🔹 Метатаблицы (продвинутый уровень)

```lua
t = {}
mt = {
  __index = function(table, key)
    return "Нет такого ключа: " .. key
  end
}
setmetatable(t, mt)
print(t.somekey)  --> Нет такого ключа: somekey
```

---

## 🔹 Стандартные библиотеки

- `math`: `math.sin`, `math.random`, `math.floor`
- `string`: `string.len`, `string.sub`, `string.find`, `string.gmatch`
- `table`: `table.insert`, `table.remove`, `table.sort`
- `io`, `os`, `debug`

---

## 🔹 Полезные ссылки

- [Metanit Lua](https://metanit.com/lua/tutorial/)
- [Learn X in Y Minutes (Lua, RU)](https://learnxinyminutes.com/docs/ru-ru/lua/)
- [Lua Manual 5.1 (англ.)](https://www.lua.org/manual/5.1/)
- [Garry’s Mod Lua Wiki](https://wiki.facepunch.com/gmod/)

---

🧠 *Создано с заботой, чтобы ты мог быстро повторять и изучать Lua прямо в Obsidian.*
