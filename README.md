# DotNetCore20AppServiceLogging

Welcome to the DotNet (.Net) Core 2.0 Logging with AppServices.

Since there isn't a full project example that I could I find I decided to create one. This should just be used as a reference to get started. Thanks to the StackOverflow user Lars for his reference : [Stackoverflowpost](https://stackoverflow.com/questions/49111671/where-does-the-asp-net-core-logging-api-as-default-store-logs)

Startup.cs should look similar to this, note the important parts are surrounded by ** **:
```
     public void Configure(IApplicationBuilder app, IHostingEnvironment env, **ILoggerFactory loggerFactory**)
        {
            if (env.IsDevelopment())
            {
                app.UseBrowserLink();
                app.UseDeveloperExceptionPage();
            }
            else
            {
                app.UseExceptionHandler("/Error");
            }

            loggerFactory.AddDebug();
            **loggerFactory.AddAzureWebAppDiagnostics();**

            app.UseStaticFiles();

            app.UseMvc();
        }
```

The appsettings.json should reflect the log level you are wanting to use:
```
{
  "Logging": {
    "IncludeScopes": false,
    "LogLevel": {
      "Default": "Information"
    }
  }
}
```

Finally your .cs file (I used the about.cshtml) should look similar to this:
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

Tags : .net core 2.0 app service logging ILogger ILoggerFactory Diagnostic Logging 
