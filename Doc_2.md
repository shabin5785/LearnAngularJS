- While creating component using cl1, ng g c <> --spec false, prevents creation of test file.
Also ng g c aaa/<> creates teh component within aaa folder and not the defaut app folder.

- to store data we can use a model. Here model is a vanilla TS class. we can use it like an object in oops langauges.
these classes can be instantiated. 
Fields in TS classes can have access specifiers like public..  public name :string;

- source maps allow us to map TS files to correspoding js files

-to pass data between components : create a property in receiving component of the type of data it should recieve. Then from teh calling or invoking component pass data as attribute to the second component. All attributes are by default accessible within the component. so make it a property and expose to outside using @input 

<app-server-comp *ngFor="let c of students" [elements]="c"></ app-server-comp>
Above create an attribute named "elements" in the app-server-comp. append @Input (), decorator before the attribute as well.

This can done only when parent needs to send data to child components..

for @Input('abcd'), abcd is an alias. Now we can bind the attribute using 'abcd' only.

- The reverse of above process is to send event from child to parent component. Like we do an operation in child component and we want to inform the parent of the event so that parent can handle the event. If this was to be done in child itself, we could have binded the event to child component. For parent, we need to create custom events, and include the data to be send to parent as well in the event.

First we need to define events in child. 
@Output() serverCreated = new EventEmitter<{ name: string, content: string }>();
Here the type given to EventEmitter is the data or the type of event we will generate. This data can be passed to parent. @output is used as we are emitting events out of the component.(like @input to receive data)

Now bind normal event listeners in child.   
<button class="btn btn-primary" (click)="onAddServer()">Add Server</ button>

In the onAddServer() method, we can now emit the custom event.
onAddServer() {
    this.serverCreated.emit({ name: this.newServerName, content: this.newServerContent });
  }
 
Now wherever we use this child component we can listen for this event and bind to it to handle it.
	  <app-cockpit (serverCreated)="onServerAdded($event)"></app-cockpit>
Here we are using the childcomponent. The child emits a custom event called ServerCreated on click of a button. We are listening to that in the place where we use it and then handling it in our custom method. Also the event has data passed to it, which we can capturing.. this is the custom object which we created. Use it like below

  onServerAdded(serverData: { name: string, content: string }) {
      name: serverData.name,
      content: serverData.content
  }
  
The type of object here, and the object type in event definition are the same.

Like input we can create alias names for output event tags..

- Now the case where two child components need to talk to each other, we need to emit custom event from one child, parent listens for that, then emits data to the second child. This can get longer and messy. Like call back hell.
Need to be careful with this long pipelines of emits and data( output and input)...

- the styles in a css files applies only to the component they belogns to. It doesnt apply hierarchially. angular internally adds attributes to elements and then applies styles based on these. So Angular uses Style encapsualtion. FOr this angular applies unique attributes to all elements. This is like Shadow dom, a dom behind original dom. Angular then applues sytles to these elements.

- We can add encapsulation attribute to component. We can set value to it from ViewEncapsulation, which has three values. Defautl is Emulated, which results in above shadow dom thing. If we choose none, the elements in dom does nto have attributes added to it by angular. So styles can be applied across components. Now we add this encapsualtion attribute to a component. So only this will not use the shadow dom concept while other components will continue using it, unless turned off. Third option Native is same as Emulated .But uses Shadow DOM concept of browser without angular intervention. So it is browser support based, So better use ANgualr suported one whihc will work in all browsers.

- Instead of using a two way binding like below
  <.input type="text" class="form-control" [(ngModel)]="newServerName">
  we can use a reference to the input and pass it to the TS method.
    < input type="text" class="form-control" #servername>
    
  Reference can be kept anywhere within tempaltes. But cannot be put in TS. so we need to pass it to TS from template. Also the refernce is the reference to the whole element, nt just the value.. So servername.value will give the value.
  
- There is another way to bind TS attribute to DOM. decalre attribute in TS and add @ViewChild to it. Now this qualifier needs to knwo which component to bind to. So we can give it the reference we defined for the component as value or the selector , or like that
@ViewChild('servername');
The type of attribute is now ElementRef, and not the element itself like above. We can get the nativeElement of this ref, which is the underlyng element and then proceeed normally,.
now with this, we have actual reference to DOM and we can change the value and attributes.. But Dont do this.Use the Angular Way


- by default all data between opening and closing tags are lost. To keep this data, add ng-content place holder in template of a component and angualr will pass data between tags to it.

**Life Cylce Methods**
- ngOnChanges - called after a bound property changes. Its also executed when the component is intialized and after that for changes

-ngOnInit - Once the component initalized. It will run after constructor

-ngDoCheck - This will run whenever change detector runs. SO can run multipe times as angular runs changedetector to check on all properties and components. So it can run even if there is no change. It runs while checking for change.

-ngAfterContentInit - called when ng-content was projected to the component

-ngAfterContentChecked - after change detector runs for ng-content 

-ngAfterViewInit - called after the components view (and child views) are initialized

-ngAfterViewChecked - after change detector for ngAfterViewInit

-ngOnDestory - called once component is to be destroyed by angular
