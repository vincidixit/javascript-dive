# Ways to create object in Javascript


## Using Object Literal

```javascript
    let user = {
        name: 'Chris',
        greet() {
            console.log(`Hello, My name is ${this.name}`);
        }
    }

    user.greet(); // Hello, My name is Chris

    console.log(Object.getPrototypeOf(user) == Object.prototype); // true
```

## Using Object.create static method

```javascript
    function showMessage() {
        console.log(`Hello, My name is ${this.name}`);
    }

    let user = Object.create(Object.prototype, { name: { value: 'Chris' }, greet: { value: showMessage } });

    user.greet(); // Hello, My name is Chris

    console.log(Object.getPrototypeOf(user) == Object.prototype); // true
```

## Using Function constructor

```javascript
    function User(name) {
        this.name = name;
    }

    // For better memory management, making greet a part of User.prototype and will be shared across all objects of type User.
    User.prototype.greet = function () {
        console.log(`Hello, My name is ${this.name}`);
    }

    let user = new User('Chris');

    user.greet();  // Hello, My name is Chris

    console.log(Object.getPrototypeOf(user) == User.prototype); // true

    console.log(Object.getPrototypeOf(User.prototype) == Object.prototype); // true
```

## Using Class

```javascript
    class User {
        constructor(name) {
            this.name = name;
        }
        greet() {
            console.log(`Hello, My name is ${this.name}`)
        }
    }

    let user = new User('Chris');

    user.greet(); // Hello, My name is Chris

    console.log(Object.getPrototypeOf(user) == User.prototype); // true

    console.log(Object.getPrototypeOf(User.prototype) == Object.prototype); // true

    // BY default, functions declared in class are made part of User.prototype and shared across all object instances of type User. This is done for better memory management.
    console.log(Object.getOwnPropertyNames(user)); // [ name ]
```



