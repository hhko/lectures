# Part 1. 솔루션 구성

1. 솔루션 구성
1. Authentication API 구현
1. 의존성 구현

## 솔루션 & 프로젝트 생성
```shell
dotnet new sln -o BuberDinner
cd BuberDinner

dotnet new webapi -o BuberDinner.Api					// Presentation layer
dotnet new classlib -o BuberDinner.Contracts			// Presentation layer
dotnet new classlib -o BuberDinner.Infrastructure		// Infrastructure layer
dotnet new classlib -o BuberDinner.Application			// Application layer
dotnet new classlib -o BuberDinner.Domain				// Domain layer

more BuberDinner.sln
dotnet sln add(ls -r **\*.csproj)
```

## 프로젝트 참조
```shell
dotnet add .\BuberDinner.Api reference .\BuberDinner.Contracts .\BuberDinner.Application .\BuberDinner.Infrastructure
dotnet add .\BuberDinner.Infrastructure reference .\BuberDinner.Application
dotnet add .\BuberDinner.Application reference .\BuberDinner.Domain

dotnet build
dotnet run --project .\BuberDinner.Api
```

### VSCode 확장 도구
- REST Client 확장 도구 설치
- Request > Weather > GetForecast.http
  ```
  dotnet run --project ./BuberDinner.Api
  info: Microsoft.Hosting.Lifetime[14]
        Now listening on: http://localhost:5024
  ```
  ```
  GET http://localhost:5024/WeatherForecast
  ```

### BuberDinner.Api 프로젝트 수정
- `Program.cs` 파일 수정
  ```cs
  var builder = WebApplication.CreateBuilder(args);
  {
      // Add services to the container.
      builder.Services.AddControllers();

      // // Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
      // builder.Services.AddEndpointsApiExplorer();
      // builder.Services.AddSwaggerGen();
  }

  var app = builder.Build();
  {
      // // Configure the HTTP request pipeline.
      // if (app.Environment.IsDevelopment())
      // {
      //     app.UseSwagger();
      //     app.UseSwaggerUI();
      // }

      app.UseHttpsRedirection();
      // app.UseAuthorization();
      app.MapControllers();
      app.Run();
  }
  ```
- `BuberDinner.Api.csproj` 불필요한 패키지 제거
  ```xml
  <ItemGroup>
    <PackageReference Include="Swashbuckle.AspNetCore" Version="6.2.3" />
  </ItemGroup>
  ```