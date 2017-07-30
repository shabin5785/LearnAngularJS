- Angular is a JS framework. It helps mainly to build single page applications.

**## Angular 1 vs 2 vs 4**
 angular 2 is a complete rewrite of angualr 1. Angular 4 is an update on angular 2, compatable with angular 2. From version 4, the name is just Angular
 
 - Angular CLI is a set of tools that helps with creating, managaing and building Angular projects. We can also avoid CLI and do the manual way of importing to html. But using CLI takes care of a lots of things for us.
 
 - @angular/cli. '@'  is a new feature of NPM called 'scoped packages'. They effectively allow NPM packages to be namespaced - any package that starts with @angular/ will get grouped into a @angular folder in your node_modules.
The reason that scoped packages don't show up in public search is because a lot of them are private packages created by organizations using NPM's paid services, and they're not comfortable opening the search up until they can be totally certain they're not going to make anything public that shouldn't be public - from a legal perspective, this is pretty understandable.

- ng new < app name> to create new app in angular cli
ng-serve to build and run the code. This command will covnert type script to JS, build and deploy it. Also start a development server.
e2e folder: End to end testing scripts

**### Typescript**
Its a super set to JS. Features like classes, interfaces, types etc. So we can have type of variable here instead of dynamic variables in js. So code gets checked in compile time and not at run time. CLI takes care of converting ts to js that browser can understand

- Behing the scene, CLI uses webpack to bring ts, js, css etc together. We can add our custom style to ang4 project, by changing the config file angular-cli.json. So to use bootstrap, we install it using npm and then add to the json style section

-CSS @import is relative to the current working directory.
So using the prefix ~ at the start of the path tells the Webpack loader to resolve the import "like a module".

- Usually the starting file, like index.html has an ang tag that points to teh root component. This custom component or tag is declared in the ts file for a component say xyz.ts. Inside that we define the component  with selector name same as the component, and also give it template and style urls to be used.all of has .component in its name( is this needed?). 
So a component has atleast 3 associated files: component.ts, style and template. Additionlay we can have the spec file for testing as well

the serve process bundles all the files and builds them. For the process the first file to be executed is the main.ts file. Inside that we bootstraps the angular app by passing the module file for the component that we created above. So the component has one more file, the module file, named as app.module.ts
in the module file we define the components that it needs to start, like inject components to it. THis is the base component that we defined earlier. All of them are referred by their exported class name so can be anything. Now the component has the selector or tag used inside index.html and angular knows about it now.

All this is triggered by the build process that runs on index.html and starts with main.ts

So the flow is like this:
Build starts on index.html through main.ts. Main.ts has an import for a module defined by us, say AppMod. This is given to the bootstrap contsructor of angular. In AppMod,  we define the components that it needs to bootstrap. This components are again defined by us. Say one is AppComponent. Inside the Appcomponet, we define the selector (or a tag). Now this tag, thru this flow is known to angular and can be used inside html files. When we use this tag or selector, the associated tempalte and style for the tag is invoked to render the page. This is how we get the date.
As all these modules, components etc are TS file, we export classes that is used across file by importing them.

The above given is the startup that happens when we first load the page. Triggered by the scripts inside index.html, added by the build process

- So angular in effect changes the DOM at runtime by parsing and executing angualr tags
- Components are the base for angular. We inject modules, and modules in turn refer to components. Its the componetns that has the tempalte and style. We usually define a root component that holds all other components together. this root component is given to the bootstrap array to start up.

- An angular app is composed of components. We can have many that makes up an application. Better keep each component in separate folder. Also add component to names of files for ease.

- A component is a TS class that angular is able to instantiate. We define a normal TS class and add angular code to make it a component. For this we use TS feature called decorators. Decorators allows us to enhance classes. So here make the normal TS class a component. We add @component annotation and then give meta data to it like the selectore, tempalte etc

- After creating a component we have to register it in the module. We dont use the components other than the root component in index.html. We use the new components in the other componetns html, starting from root component.

- In module: boostrap to startup, declaration for components and imports for importing other modules.

- we can also create componetns using CLI. ng generate is the command. ng g c is a short cut for same.

- in a component instead of using an external tempalte file, we can define the html within TS itself. Inline style. We use template of inline and templateurl for external file. One of them should be present. Need to use tilde for multi line template code.

- we can  link and use bootstrap for styling. Can also override the styling with ours by writing in css file for component

- styleurls can be used to refer multipe styel sheets. We can also using styles, an inline styling.  Cant use both at once.

- the selector in component can be an attribute style one instead of normal tag one 
eg: 'app-server' , we have to use it like <app-server>
we can put it in attribute style like :['app-server'] and then use it as attribute
< div app-server></div>

also can use class style selectors like '.app-server' and use it like below
< div class="app-server"></div>

- Databinding is done two ways. From TS backend (business logic) to the template (front end). also the other way around, taking user interactions to backend (event bindings). We can combine both using two way bindings

- String interpolatin operator can be used with anyting that returns a string, ternary operator or a fn or hard coded string etc. It can also take types that can be converted to string like number.
We can also use a method in string interpolation. Now if we dont use the function braces to call the method,(), then the function name is taken as a string and the return value will be the fn definition.Means fn name points to the definition

-[] brackets indicate to angular that we are using property binding. So when we use a normal html attribute within [] ,like [disabled] then its binded to the class property that we specify. The dom property is binded to the backend.So the property updates dynamically. Update dom dynamically ...

- similary we can bind dom events to backend methods. Use () here, similar to square brackets above. So the event is now bound to a backend method.

- we can pass dom event to backend by sending $event as argument to the backend method. So we can get the input string or form input or like that.

- in TS we can set type of object to any like, event : any or specific like event: Event


