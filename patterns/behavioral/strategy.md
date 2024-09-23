Паттерн Стратегия (Strategy) - это поведенческий паттерн проектирования, который определяет семейство алгоритмов, инкапсулирует их и делает взаимозаменяемыми.

Основные принципы
- Определяет интерфейс для семейства алгоритмов.
- Создает подклассы для каждого конкретного алгоритма.
- Выбирает и использует алгоритм на лету.

Давайте рассмотрим пример использования паттерна Стратегия в контексте системы оплаты онлайн-магазина:

```typescript
// Интерфейс стратегии
interface PaymentStrategy {
    processPayment(amount: number): void;
}

// Конкретные стратегии
class PayPalStrategy implements PaymentStrategy {
    processPayment(amount: number): void {
        console.log(`Paid ${amount} using PayPal.`);
    }
}

class CreditCardStrategy implements PaymentStrategy {
    processPayment(amount: number): void {
        console.log(`Paid ${amount} using Credit Card.`);
    }
}

class BitcoinStrategy implements PaymentStrategy {
    processPayment(amount: number): void {
        console.log(`Paid ${amount} using Bitcoin.`);
    }
}

// Контекст (OnlineStore)
class OnlineStore {
    private paymentStrategy: PaymentStrategy;

    constructor(paymentStrategy: PaymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    checkout(amount: number): void {
        this.paymentStrategy.processPayment(amount);
    }

    setPaymentStrategy(strategy: PaymentStrategy): void {
        this.paymentStrategy = strategy;
    }
}

// Клиентский код
function main() {
    const paypal = new PayPalStrategy();
    const creditCard = new CreditCardStrategy();
    const bitcoin = new BitcoinStrategy();

    const storeWithPayPal = new OnlineStore(paypal);
    storeWithPayPal.checkout(100); // "Paid 100 using PayPal."

    const storeWithCreditCard = new OnlineStore(creditCard);
    storeWithCreditCard.checkout(200); // "Paid 200 using Credit Card."

    const storeWithBitcoin = new OnlineStore(bitcoin);
    storeWithBitcoin.checkout(300); // "Paid 300 using Bitcoin."

    // Изменение стратегии динамически
    storeWithPayPal.setPaymentStrategy(creditCard);
    storeWithPayPal.checkout(400); // "Paid 400 using Credit Card."
}

main();
```

В этом примере:
- Мы определили интерфейс PaymentStrategy для всех стратегий оплаты.
- Реализовали конкретные стратегии (PayPalStrategy, CreditCardStrategy, BitcoinStrategy).
- OnlineStore является контекстом и использует текущую стратегию оплаты.
- Мы можем легко изменять стратегию оплаты на лету с помощью метода setPaymentStrategy.

Преимущества использования паттерна Стратегия
- Гибкость: можно легко переключаться между различными алгоритмами без изменения кода контекста.
- Расширяемость: легко добавлять новые типы стратегий.
- Открытость расширения: новая стратегия может быть добавлена без изменения существующего кода.
