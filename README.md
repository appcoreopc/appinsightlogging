WebApp

To setup appsights logging quickl :-

create a dotnet project 

next, 

dotnet add package Microsoft.Extensions.Logging.ApplicationInsights --version 2.10.0

add the following codes and remember to provide your application insights guid id :-




public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
      WebHost.CreateDefaultBuilder(args)
        .UseStartup<Startup>()
      .ConfigureLogging(
            builder =>
            {
                // Providing an instrumentation key here is required if you're using
                // standalone package Microsoft.Extensions.Logging.ApplicationInsights
                // or if you want to capture logs from early in the application startup
                // pipeline from Startup.cs or Program.cs itself.
                builder.AddApplicationInsights("aikey");

                // Optional: Apply filters to control what logs are sent to Application Insights.
                // The following configures LogLevel Information or above to be sent to
                // Application Insights for all categories.
                builder.AddFilter<Microsoft.Extensions.Logging.ApplicationInsights.ApplicationInsightsLoggerProvider>
                                 ("", LogLevel.Information);
            }
        );


Place this as part of your constructor 


 private readonly `ILogger` _logger;

    public ValuesController(ILogger<ValuesController> logger)
    {
        _logger = logger;
    }




And finally log your data :-


        logger.LogInformation("Getting weather data.");




To check, goto Azure web portal, application insights and search 



That's it! :)




