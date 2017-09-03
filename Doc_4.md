- Service is a normal typescript class. No annotation is added to it. Now dont just import the service class to another class and call methods inside that. Thats not the normal service behaviour.

- instead of us creating and using the object of service class, Use the Angular dependency injector to inject the objecct of the service and use it.
For this we declare the object that we want in the constructor of the component,We have to mandatorly give the type or class of the object as well. Now angular can inject the object. But this is not enough. We also have to provide an attribute providers within @component annotation config .Within the providers array we have to give the service class name as well. THis is needed as angular knows who is creating the object, and the type of that is given in the constructor part.


