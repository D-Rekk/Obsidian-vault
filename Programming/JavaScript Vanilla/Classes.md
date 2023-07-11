# JavaScript 03: Classes

Created: June 30, 2022 11:28 AM
Status: Open
Updated: June 30, 2022 2:28 PM

# Classes

Classes are template to create Objects. They are coded so we can work with the data incapsulated  in. Classes are in fact “special functions”.

### **SYNTAX**

You name the class with a capital letter to differ it from other variables. To invoke a class, use the  `new` keywork and the name of the class. Invoking the class execute the constructor function

```jsx
class User {
	constructor (_name, _surname){
		this.name = _name;
		this.surname = _surname;
	}
}
let userOne = new User('Mario', 'Bros');
```

This creates a new empty object

### Inheritance

Classes have the chance to pass on different methods to other classes. This is possible by calling the `extends` function during the declaring of the parent class. `super` collects the information from the inherited class and defines them in the new class.

```jsx
class VideoCharacter extends User{
	constructor (_name, _surname, _gameOrigin){
		super (_name, _surname);
		this.gameOrigin= _gameOrigin;
	}
}

```

---

Something

---

<aside>
💡

</aside>

 Something

---