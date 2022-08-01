- [동영상](https://www.youtube.com/watch?v=fhM0V2N1GpY&list=PLzYkqgWkHPKBcDIP5gzLfASkQyTdy0t4k)
- [소스](https://github.com/amantinband?tab=repositories)

```shell
dotnet new sln -o BuberDinner

Presentation Layer
	dotnet new classlib -o BuberDinner.Contracts
	dotnet new webapi -o BuberDinner.Api 
		dotnet add .\BuberDinner.Api reference .\BuberDinner.Contracts .\BuberDinner\Application .\BuberDinner.Infrastructure
	
Infrastructure Layer
	dotnet new classlib -o BuberDinner.Infrastructure
		dotnet add .\BuberDinner.Infrastructure reference .\BuberDinner\Application
	
Application Lyaer	
	dotnet new classlib -o BuberDinner.Application
		dotnet add .\BuberDinner.Application reference .\BuberDinner\Domain
	
Domain Layer
	dotnet new classlib -o BuberDinner.Domain 
	
dotnet sln add (ls -r **\*.csproj)
dotnet sln list
dotnet build
dotnet run --project .\BuberDinner.Api

Requests > Weather > GetForecasts.http
GET http:// ... /WeatherForecast
```
