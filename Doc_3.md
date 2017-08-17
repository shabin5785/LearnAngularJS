**Diretictive  

- There are two types of Directives: Attribute and structural.
Attribute is like normal html ones, which affects the element it is added to, like data or event binding. Structural one affects the DOM so have a * to point this to angular.

- We cannot have more than one structural directive on an element.

- ngClass to change the class dynamically and ngStyle to change style dynamically. Both can be attribute bound using []

- @Directive is used to create our own directives. We define directive like a component, gives it a selector to use.We can wrap the selector tag in [], so that it will be recognized when we use it without square brackts, like we use ngFor.
Now for a directive to affect a component, we need access to the component, For that we inject the component to our custom directive. For that we use the constructor of the directive and pass an elementRef to that. This is the refernce to that component that uses this directive.

We can change the component in construtor itself or use life cycle methods like onInit to affect the component. its upto us ..

- After creatin directive we need to add it to angular module, as angular is not aware of it. Angular doesnt scan all files or we have to tell it to include new one we created. We add it under declarations
