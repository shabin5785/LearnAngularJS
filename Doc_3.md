**Diretictive  

- There are two types of Directives: Attribute and structural.
Attribute is like normal html ones, which affects the element it is added to, like data or event binding. Structural one affects the DOM so have a * to point this to angular.

- We cannot have more than one structural directive on an element.

- ngClass to change the class dynamically and ngStyle to change style dynamically. Both can be attribute bound using []

- @Directive is used to create our own directives. We define directive like a component, gives it a selector to use.We can wrap the selector tag in [], so that it will be recognized when we use it without square brackts, like we use ngFor.
Now for a directive to affect a component, we need access to the component, For that we inject the component to our custom directive. For that we use the constructor of the directive and pass an elementRef to that. This is the refernce to that component that uses this directive.

We can change the component in construtor itself or use life cycle methods like onInit to affect the component. its upto us ..

- After creatin directive we need to add it to angular module, as angular is not aware of it. Angular doesnt scan all files or we have to tell it to include new one we created. We add it under declarations
< p appBasicHighlight> Style Me</p>
Example of how to use customdirective .but this direct changing of DOM is not the angular way. So dont directly use the elementRef.

- use ng g d to generate a directive.. similar to ng g c.
If we directly access the dom , we might get errors as not all elements will be present or dom is not built completely. So use the renderer and accress the componenet through it to be on safer side. This is better as well.

- we might want our directives to responds to dom events. For that we bind the event to the directive class using hostlistner and then work on it.

@HostListener('mouseenter') onmouseenter(eventRef: Event){
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color','blue');
  } 
  
  above we are listening to the mousenter event on the component having our custom directive and the changing the color.
  
  - we can also use the @HostBinding to bind a property of the component to the directive and change it. Like 
  @HostProperty('style.backgroundColor') bc= 'blue';
  above we have bound the background color property and can now change it. This is an optional way of doing thigs.Renderer shouod work fine.
  
 - Above examples the value that directive sets is fixed. We may want to pass this value from DOM to the new directive. For this we can bind custom attributes to the directive and use it in the dom
  @Input() highlightColor : string ='transparent';
  
  and the use it with customdirective like this:
   < p appBetterHighlight [highlightColor]="'yellow'"> Style Better</p>
   
   above we have changed the value set inside the directive to the user provided one.
  
 - How does adding the attribue bidning in directive work? It can be attribute of p tag or the directive. Answer is angular figures this out by checking the components and the directives.
 
 [highlightColor]="'yellow'"  and highlightColor="yellow"  shoudl work the same. With [] and '' and second with neither of them. But this type of property binding can be confused with real attribute of the component . so be careful using it.
 
- A structural directive, like the one starting with *, will in backend, create a ng-template, and inject the code within that and then display it. We can choose not use the structural directive with * and use our own template. Both works the same way.
