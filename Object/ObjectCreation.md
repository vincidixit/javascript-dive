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