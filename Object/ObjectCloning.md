# Ways of cloning an object

## Using Spread Operator

Points to be considered:
- Performs only shallow copy - The cloning of nested objects is not performed.
- Prototype object is not copied - An empty object is created based on Object.prototype before spread operator copies the content.

```javascript
let userPrototype = {
    greet() {
        console.log(`Hello, My name is ${this.name}`);
    }
}

let user = {
    name: 'Miguel',
    address: {
        city: 'Pune',
        country: 'India'
    },
    __proto__: userPrototype
}

let userClone = { ...user };

console.log(user === userClone); // false (Shallow Copy)

console.log(user.address === userClone.address); // true (No Deep Copy)

console.log(Object.getPrototypeOf(user) === Object.getPrototypeOf(userClone)); // false (Default Prototype by Object Literal)
```



## Using Object.assign

Points to be considered:
- Performs only shallow copy - The cloning of nested objects is not performed.
- Prototype of the object depends on the target object. In given example, the target object is created using Object Literal which creates an empty object based on Object.prototype.

```javascript
let userPrototype = {
    greet() {
        console.log(`Hello, My name is ${this.name}`);
    }
}

let user = {
    name: 'Miguel',
    address: {
        city: 'Pune',
        country: 'India'
    },
    __proto__: userPrototype
}

let userClone = Object.assign({}, user);

console.log(user === userClone); // false (Shallow Copy)

console.log(user.address === userClone.address); // true (No Deep Copy)

console.log(Object.getPrototypeOf(user) === Object.getPrototypeOf(userClone)); // false (Default Prototype by Object Literal)

```


## Using Object.create


Points to be considered:
- Performs only shallow copy - The cloning of nested objects is not performed.
- Below example contains usage of Object.getPrototype to get the prototype and Object.getOwnPropertyDescriptors to retrieve information about properties.

```javascript
// Using Object.create, Object.getPrototype and Object.getOwnPropertyDescriptors

let userPrototype = {
    greet() {
        console.log(`Hello, My name is ${this.name}`);
    }
}

let user = {
    name: 'Miguel',
    address: {
        city: 'Pune',
        country: 'India'
    },
    __proto__: userPrototype
}

let userClone = Object.create(Object.getPrototypeOf(user), Object.getOwnPropertyDescriptors(user));

console.log(user === userClone); // false

console.log(user.address === userClone.address); // true

console.log(Object.getPrototypeOf(user) === Object.getPrototypeOf(userClone)); // true
```


## Using for..in loop


```javascript
function CloneObject(obj) {
    let clone = {};
    for (let prop in obj) {
        if (typeof (obj[prop]) === 'object') {
            clone[prop] = CloneObject(obj[prop]);
        }
        else {
            clone[prop] = obj[prop];
        }
    };
    return clone;
}

let userPrototype = {
    greet() {
        console.log(`Hello, My name is ${this.name}`);
    }
}

let user = {
    name: 'Miguel',
    address: {
        city: 'Pune',
        country: 'India'
    },
    __proto__: userPrototype
}

let userClone = CloneObject(user);

console.log(user === userClone); // false

console.log(user.address === userClone.address); // false

console.log(Object.getPrototypeOf(user) === Object.getPrototypeOf(userClone)); // false

console.log(typeof (userClone.greet) === 'function'); // true
```
