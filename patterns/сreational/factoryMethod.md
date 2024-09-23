Factory Method - это паттерн, который определяет интерфейс для создания объектов, но оставляет подклассам решение о том, какой класс инстанцировать.

Применение:
- Создание семейств взаимосвязанных объектов
- Когда тип создаваемого продукта должен зависеть от клиента

Пример реализации на JavaScript:
```javascript
class Animal {
    speak() {}
}

class Dog extends Animal {
    speak() { console.log("Woof!"); }
}

class Cat extends Animal {
    speak() { console.log("Meow!"); }
}

function createAnimal(type) {
    switch (type) {
        case 'dog':
            return new Dog();
        case 'cat':
            return new Cat();
        default:
            throw new Error('Invalid animal type');
    }
}

const dog = createAnimal('dog');
const cat = createAnimal('cat');

dog.speak(); // Woof!
cat.speak(); // Meow!
```
