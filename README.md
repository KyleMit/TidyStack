# Tidy Stack

<https://tidystack.netlify.app/>

Turns stack traces that looks like this

```log
System.NullReferenceException: Object reference not set to an instance of an object.
   at MyApp.Services.UserService.GetUserById(Int32 userId) in C:ProjectsMyAppServicesUserService.cs:line 45
   at MyApp.Controllers.UserController.GetDetails(Int32 id) in C:ProjectsMyAppControllersUserController.cs:line 30
   at Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker.InvokeActionMethodAsync()
   at Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker.InvokeNextActionFilterAsync()
   at Microsoft.AspNetCore.Mvc.Internal.ResourceInvoker.InvokeNextResourceFilter()
   at Microsoft.AspNetCore.Routing.EndpointMiddleware.Invoke(HttpContext httpContext)
   at Microsoft.AspNetCore.Hosting.Internal.RequestServicesContainerMiddleware.Invoke(HttpContext httpContext)
   at Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http.HttpProtocol.ProcessRequestsAsync()
```

Into this

```cs
System.NullReferenceException: Object reference not set to an instance of an object.
at GetUserById() in C:ProjectsMyAppServicesUserService.cs:line 45
at GetDetails() in C:ProjectsMyAppControllersUserController.cs:line 30
at InvokeActionMethodAsync()
at InvokeNextActionFilterAsync()
at InvokeNextResourceFilter()
at Invoke()
at Invoke()
at ProcessRequestsAsync()
```

## TODO

* [ ] Copy output button
* [ ] Transform output on content change (don't wait for button click)
* [ ] Share button which shares input as query param
* [ ] Syntax highlight different parts of output
* [ ] Options menu to select which parts you want to strip out
  * [ ] Fully qualified name
  * [ ] Parameters
  * [ ] Type info
  * [ ] File directory
      
