# ASP .NET Core - Deploy e Hospedagem no IIS

- Adicionar no arquivo **Startup.cs** a seguinte instrução:

  ```c#
  webBuilder.UseIISIntegration();
  ```

  Exemplo:

  ```c#
  using System;
  using System.Collections.Generic;
  using System.Linq;
  using System.Threading.Tasks;
  using Microsoft.AspNetCore.Hosting;
  using Microsoft.Extensions.Configuration;
  using Microsoft.Extensions.Hosting;
  using Microsoft.Extensions.Logging;
  
  namespace teste_core_IIS
  {
      public class Program
      {
          public static void Main(string[] args)
          {
              CreateHostBuilder(args).Build().Run();
          }
  
          public static IHostBuilder CreateHostBuilder(string[] args) =>
              Host.CreateDefaultBuilder(args)
                  .ConfigureWebHostDefaults(webBuilder =>
                  {
                      webBuilder.UseStartup<Startup>();
                      webBuilder.UseIISIntegration();
                  });
      }
  }
  ```

  

- Em seguida criar o arquivo **web.config** e inserir os seguintes códigos:

  ```c#
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <location path="." inheritInChildApplications="false">
      <system.webServer>
        <handlers>
          <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
        </handlers>
        <aspNetCore processPath="dotnet"
                    arguments=".\MyApp.dll"
                    stdoutLogEnabled="false"
                    stdoutLogFile=".\logs\stdout"
                    hostingModel="inprocess" />
      </system.webServer>
    </location>
  </configuration>
      
  <!-- fonte: https://docs.microsoft.com/pt-br/aspnet/core/host-and-deploy/iis/web-config?view=aspnetcore-5.0 -->
  ```

  

