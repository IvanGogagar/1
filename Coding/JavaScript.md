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