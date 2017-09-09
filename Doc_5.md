**FORMS**
--------------------
- Angular has two approaches for forms: Template driven, where we define a template and angular will infer the form elements and controls from that template. Other one is Reactive approach, where we define the elements, link them up and control the finer elements of the form.

- We want angular to handle the forms. Not sent a http request on form submit. So we should not submit forms like normal http ones, but use angular to handle them

Template Approach
-----------------------

- Here we start with a form or a template defined within a component html. Then we use that template to drive everything. the form submit, data etc

- Now the template driven appraoches, restricts our control of form witin the template of html file. We cannot control it from ts file. We interact of configure the template and angular takes care of implementing it. In reactive approach, we have the complete control, so we can submit form and then interact or control it from ts file.

- Make use to import the FormsModule in module.ts and add it to imports array. The formsmodule has a lot of inbuilt functions.
One being, angular will automatically create a JS object when it detecs a form tag within a component. But the individual components are not autmatically as we may choose not to use all elements in form in the object. We have to do this manually
To do this add ngModel to the form elements we want to be part of the form object. Make sure to add the name attribute to the element.

- Use ngSubmit to submit the form. This will hook into the defautl form submit and trigger the angular method we added to the listener.

- We can set #f="ngForm" in the form element. Now the reference f is pointing to the angular created form object for the template. THe object will be of type ngForm. 

- The form object has a lot of controls or info about the form. Tons of.

- We can access the form by using ViewChild annotation to get access to the local reference object we created, instead of passing it. This can be useful if we want to refer an earlier submitted form while submittign another form.


