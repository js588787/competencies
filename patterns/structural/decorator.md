Паттерн Декоратор (Decorator) - это структурный паттерн проектирования, который позволяет динамически добавлять новые обязанности объекту без изменения его структуры. Вот подробное объяснение этого паттерна и пример его реализации на TypeScript:

Основные принципы
- Декоратор создается для добавления новых обязанностей к объекту.
- Декоратор не изменяет существующий класс.
- Декоратор предоставляет новый интерфейс, совместимый с требуемым.

Давайте рассмотрим пример использования паттерна Декоратор в TypeScript:
```javascript
// Интерфейс компонента
interface Component {
    operation(): string;
}

// Конкретный компонент
class ConcreteComponent implements Component {
    operation(): string {
        return 'Конкретный компонент';
    }
}

// Базовый декоратор
abstract class Decorator implements Component {
    protected component: Component;

    constructor(component: Component) {
        this.component = component;
    }

    abstract operation(): string;
}

// Конкретный декоратор
class ConcreteDecoratorA extends Decorator {
    constructor(component: Component) {
        super(component);
    }

    operation(): string {
        return `Декоратор A: ${this.component.operation()}`;
    }
}

// Еще один декоратор
class ConcreteDecoratorB extends Decorator {
    constructor(component: Component) {
        super(component);
    }

    operation(): string {
        return `Декоратор B: ${this.component.operation()}`;
    }
}

// Клиентский код
function clientCode(component: Component) {
    console.log(`Результат: ${component.operation()}`);
}

// Пример использования
const component = new ConcreteComponent();
console.log('Клиент: Используем простой компонент:');
clientCode(component);

const decorator1 = new ConcreteDecoratorA(component);
console.log('\nКлиент: Используем компонент с декоратором A:');
clientCode(decorator1);

const decorator2 = new ConcreteDecoratorB(decorator1);
console.log('\nКлиент: Используем компонент с декораторами A и B:');
clientCode(decorator2);
```

В этом примере:
- Мы определили интерфейс Component для всех компонентов и декораторов.
- ConcreteComponent реализует базовый компонент.
- Decorator - это абстрактный класс для всех декораторов.
- ConcreteDecoratorA и ConcreteDecoratorB реализуют конкретные декораторы.
- Клиентский код использует все эти компоненты и декораторы.

Преимущества использования паттерна Декоратор
- Гибкость: можно добавлять новые обязанности к объекту динамически.
- Расширяемость: легко создавать различные комбинации декораторов.
- Сохранение существующего кода: не требуется изменять исходные классы.
