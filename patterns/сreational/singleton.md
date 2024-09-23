
Singleton - это паттерн, который гарантирует, что класс имеет только один экземпляр, и предоставляет глобальную точку доступа к этому экземпляру.

Применение:
- Логирование
- Настройки приложения
- Кэширование данных

```javascript
class Logger {
    static instance;
    
    constructor() {
        if (!Logger.instance) {
            this.logs = [];
            Logger.instance = this;
        }
        return Logger.instance;
    }

    log(message) {
        this.logs.push(message);
    }

    getLogs() {
        return this.logs;
    }
}

const logger1 = new Logger();
const logger2 = new Logger();

console.log(logger1 === logger2); // true
```
