Паттерн Адаптер (Adapter) - это порождающий паттерн проектирования, который позволяет объектам с несоответствующими интерфейсами работать вместе. Он решает проблему совместимости между несовместимыми системами или компонентами.

Основные принципы
- Адаптер создается для адаптации одного интерфейса к другому.
- Адаптер не изменяет существующие классы.
- Адаптер предоставляет новый интерфейс, совместимый с требуемым.

Давайте рассмотрим пример использования паттерна Адаптер в TypeScript:
```javascript
// Интерфейс старой системы
interface OldSystem {
    oldMethod(): void;
}

// Класс, реализующий интерфейс старой системы
class OldClass implements OldSystem {
    oldMethod() {
        console.log("Старая система работает");
    }
}

// Новый интерфейс, требуемый современной системой
interface NewSystem {
    modernMethod(): void;
}

// Адаптер для адаптации старой системы к новой
class Adapter implements NewSystem {
    private oldSystem: OldSystem;

    constructor(oldSystem: OldSystem) {
        this.oldSystem = oldSystem;
    }

    modernMethod(): void {
        this.oldSystem.oldMethod();
        console.log("Адаптер адаптирует метод");
    }
}

// Использование адаптера
function useNewSystem(newSystem: NewSystem): void {
    newSystem.modernMethod();
}

// Пример использования
const oldSystem = new OldClass();
const adapter = new Adapter(oldSystem);

useNewSystem(adapter);
```

В этом примере:
- Мы имеем OldClass, который реализует интерфейс OldSystem.
- Нам нужно адаптировать этот класс к новому интерфейсу NewSystem.
- Мы создаем класс Adapter, который реализует NewSystem и содержит ссылку на OldClass.
- В методе modernMethod() адаптер вызывает соответствующий метод из OldClass.

Преимущества использования паттерна Адаптер
- Сохранение существующего кода без изменений.
- Улучшение совместимости между различными системами или компонентами.
- Повышение гибкости и расширяемости системы.
