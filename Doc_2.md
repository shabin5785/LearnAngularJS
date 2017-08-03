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

