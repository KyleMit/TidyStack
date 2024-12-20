<script lang="ts">
  let exception = `System.NullReferenceException: Object reference not set to an instance of an object.
   at MyApp.Services.UserService.GetUserById(Int32 userId) in C:\Projects\MyApp\Services\UserService.cs:line 45
   at MyApp.Controllers.UserController.GetDetails(Int32 id) in C:\Projects\MyApp\Controllers\UserController.cs:line 30
   at Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker.InvokeActionMethodAsync()
   at Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker.InvokeNextActionFilterAsync()
   at Microsoft.AspNetCore.Mvc.Internal.ResourceInvoker.InvokeNextResourceFilter()
   at Microsoft.AspNetCore.Routing.EndpointMiddleware.Invoke(HttpContext httpContext)
   at Microsoft.AspNetCore.Hosting.Internal.RequestServicesContainerMiddleware.Invoke(HttpContext httpContext)
   at Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http.HttpProtocol.ProcessRequestsAsync()`
  let output = ""
  transform();


  // TODO setting toggles for what pieces you want to show or not
  // TODO syntax highlighting for sections
  
  function simplifyException(text: string): string {
    return text
      .split("\n")
      .map((line) => {
        var rgx = /at (.+)(<.*>.*)?(\(.*\))( in )?(.+)?/
        var match = rgx.exec(line)
        if (match) {
          var fullyQualifiedName = match[1] || ""
          var fullFilePath = match[5] || ""

          var methodName = fullyQualifiedName.split(".").at(-1)
          var fileName = fullFilePath.split("/").at(-1)

          var fileReference = fileName ? ` in ${fileName}` : ""
          var truncatedLine = `at ${methodName}()${fileReference}`

          return truncatedLine
        }
        return line.trim()
      })
      .join("\n")
  }

  function transform() {
    output = simplifyException(exception)
  }
</script>

<main>
  <h1>Tidy Stack</h1>
  <textarea bind:value={exception} placeholder="Paste your exception here"></textarea>
  <br />
  <button on:click={transform}>Transform</button>
  <pre>{output}</pre>
</main>

<style>
  textarea {
    width: 100%;
    height: 200px;
    margin-bottom: 1rem;
    font-family: monospace;
    font-size: 0.9rem;
  }

  pre {
    background: #f9f9f9;
    padding: 1rem;
    border: 1px solid #ddd;
    font-family: monospace;
    white-space: pre-wrap;
  }
</style>
