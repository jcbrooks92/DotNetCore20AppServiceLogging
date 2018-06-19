Welcome to the DotNetCore2.0 Logging with AppServices.

In looking into this further you do not have to do anything special with .Net Core 2.0 for logging to show up within the application logs for Azure Web Apps. I removed all the code mentioned below in the startup.cs and the functionality worked. See this link for more detail: [Azure App Service provider](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging/?tabs=aspnetcore2x&view=aspnetcore-2.1#azure-app-service-provider)

In your .cs file (I used the about.cshtml) should look similar to this:
```
 private ILogger _logger;

        public AboutModel(ILogger<AboutModel> logger)
        {
            _logger = logger;
        }

        public void OnGet()
        {
            _logger.LogInformation("Hello");
            Message = "Your application description page.";
            

        }
```
