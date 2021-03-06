
# WARMUP NOTES

* TODO : `warmup-oop`

Encapsulation
- the practice of bundling related properties and behaviors into
  one class
- each class has a purpose and is responsible for keeping track of 
  properties related to that purpose and providing the methods 
  necessary to manage those properties



Inheritance
- mechanism that passes traits of a parent class to its descendants
- prevents duplication of code
- the Cat and Dog classes both have a name and age property so we can
  group these shared properties into a parent class that the Cat
  and Dog classes can inherit from



Polymorphism
- provides a way to perform a single action in different forms by
  calling the same method on different objects
- we can create a speak method in both Cat and Dog classes that
  has the same purpose, but differs in execution and utilizes the 
	functionality of the parent classes method



Abstraction
- implemented to hide unnecessary data and withdraw relevant data
- the Shelter class only cares about whether or not an application
  is valid, it doesnt need to know how the Application class checks
  for validity



* TODO: REFACTOR USING COMMON JS MODULES


# LAW OF DEMETER

* TODO : `coupling-demo`

Coupling
- the degree of interdependence betweeen two or more classes
- the fewer the connections, less chance for ripple effect
	- one small change causes other changes and so on
- changing one class should not require a change of another class
	- if it does, the class is too "coupled" or interdependent
- to reduce coupling, reduce num of clases a given class must know to operate



The Law Of Demeter
- a method of an object can only invoke methods or use props of the following
	- methods on object itself
	- any of objects passed in as params to the method
	- an object created in the method
	- any values stored in instance vars of the object
	- any values stored in global vars
- guideline: dont use more than one dot (not counting one after "this")



```JS

// THE BAD SOLUTION

class User {
	constructor(name, age, address, imageUrl) {
		this.name = name;
		this.age = age;
		this.profile = new Profile(address, imageUrl)
	}

	updateAddress(address) {
		// this violates the law of demeter
		// 1. we've chained two dots (excluding the dot after `this`)
		// 2. the user class must be aware of the inner workings
		//    of the Address class
		// 3. if there was a change to the Address class
		//    (such as renaming the method `update`)
		//    we would have to update both the Profile
		//    and User classes
		this.profile.address.update(address)
	}

}

// THE GOOD SOLUTION

class User {
  constructor(name, age, address, imageUrl) {
    this.name = name;
    this.age = age;
    this.profile = new Profile(address, imageUrl);
  }

  updateAddress(newAddress) {
		// this fixes the issue 
		// - only chaining one dot (excluding the dot after `this`)
		// - a change to the Address class wouldnt require
		//   a change to the Profile or User classes
		// - the only thing that might change is the value
		//   passed as the argument
    this.profile.updateAddress(newAddress);
  }
}

```



# ES6 MODULES

* TODO : `commonJS-vs-es6-demo`

Browser Support for ES6 Modules
- ES6 modules can only be used when file is specified as a `module`
- can use HTTP server to serve HTML file with <script type="module">
	- `python3 -m http.server`
- running local web server gives you access to browser support for ES6 syntax


Modules in Browser Before ES6 Support
1. third party technology to load javascript files
2. individual script tags for each module


* TODO : `practice-es6-modules`