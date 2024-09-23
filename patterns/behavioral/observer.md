Паттерн Обсервер (Observer) - это поведенческий паттерн проектирования, который позволяет некоторым объектам (называемым наблюдателями) получать уведомления о состоянии изменении другого объекта (подписчика).

Основные принципы
- Подписчик (Subject) содержит список наблюдателей.
- Наблюдатели реализуют интерфейс для получения уведомлений от подписчика.
- Подписчик может добавлять и удалять наблюдателей.
- Когда состояние подписчика меняется, он уведомляет все свои наблюдатели.

Давайте рассмотрим пример использования паттерна Обсервер в контексте системы оповещений о наличии товара:
```javascript
// Интерфейс подписчика
interface Subject {
    addObserver(observer: Observer): void;
    removeObserver(observer: Observer): void;
    notifyObservers(): void;
}

// Интерфейс наблюдателя
interface Observer {
    update(subject: Subject): void;
}

// Конкретный подписчик (товар)
class Product implements Subject {
    private observers: Observer[] = [];
    private name: string;

    constructor(name: string) {
        this.name = name;
    }

    addObserver(observer: Observer): void {
        this.observers.push(observer);
    }

    removeObserver(observer: Observer): void {
        const index = this.observers.indexOf(observer);
        if (index !== -1) {
            this.observers.splice(index, 1);
        }
    }

    notifyObservers(): void {
        for (const observer of this.observers) {
            observer.update(this);
        }
    }

    restock(): void {
        console.log(`${this.name} возвращен на склад.`);
        this.notifyObservers();
    }
}

// Конкретный наблюдатель (покупатель)
class Customer implements Observer {
    private name: string;

    constructor(name: string) {
        this.name = name;
    }

    update(subject: Subject): void {
        console.log(`${this.name}, ${subject.name} доступен для покупки.`);
    }
}

// Клиентский код
function main() {
    const product = new Product("Продукт А");
    const john = new Customer("Джон");
    const jane = new Customer("Жан");

    product.addObserver(john);
    product.addObserver(jane);

    console.log("Товар отсутствует на складе.");
    product.restock();

    // Удаляем одного из наблюдателей
    product.removeObserver(john);
    console.log("\nУведомляем о новом товаре:");
    product.restock();
}

main();
```

В этом примере:
- Product реализует интерфейс Subject.
- Customer реализует интерфейс Observer.
- Когда товар появляется на складе (restock()), все подписчики получают уведомление.
- Мы можем добавлять и удалять наблюдателей динамически.

Преимущества использования паттерна Обсервер
- Разделение ответственности: подписчик не зависит от конкретных классов наблюдателей.
- Гибкость: легко добавлять новые типы наблюдателей без изменения существующих классов.
- Расширяемость: система может быть легко расширена для поддержки различных сценариев оповещения.
