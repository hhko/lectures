# Part 2. Jwt Token 구현

1. Jwt Token 구현
1. Options 패턴
1. `dotnet user-secrets`
1. Sneak-Peeking(몰래 엿보기) 디버깅

## 1. 의존성
### 1.1 Jwt Token 인터페이스
- Application Layer
  - 인터페이스 정의 : `IJwtTokenGenerator`
  - 인터페이스 사용 : `_jwtTokenGenerator.GenerateToken`
- Presentation Layer : Infrastructure
  - 인터페이스 구현 : `JwtTokenGenerator`
### 1.2 시간 인터페이스
- Application Layer
  - 인터페이스 정의 : `IDateTimeProvider`
  - 인터페이스 사용 : `_dateTimeProvider.UtcNow. ...`
- Presentation Layer : Infrastructure
  - 인터페이스 구현 : `DateTimeProvider

## 2. JWT 구현
dotnet add .\BuberDinner.Infrastructure\ package System.IdentityModel.Tokens.Jwt

```
{
  "id": "95ae91c9-de44-4440-80fb-a216eed75aac",
  "firstName": "Amichai",
  "lastName": "mantinband",
  "email": "amichai@mantinband.com",
  "password": "eyJhbGci ... cUAbxGm1o_E"
}

> Headers
{
    "alg": "HS256",
    "typ": "JWT"
}

> Payload
{
    "sub": "95ae91c9-de44-4440-80fb-a216eed75aac",
    "given_name": "Amichai",
    "family_name": "mantinband",
    "jti": "13fcb573-bb06-4353-abc4-36273be4a54b",
    "exp": 1659493157,
    "iss": "BuberDinner"
}
```

## 3. Options Pattern
```
dotnet add .\BuberDinner.Infrastructure package Microsoft.Extensions.Configuration

dotnet add .\BuberDinner.Infrastructure package Microsoft.Extensions.Options.ConfigurationExtensions
    public static IServiceCollection Configure<[DynamicallyAccessedMembers((DynamicallyAccessedMemberTypes)(-1))] TOptions>(
        this IServiceCollection services,
        IConfiguration config) where TOptions : class;

services.Configure<JwtSettings>(configuration.GetSection(JwtSettings.SectionName));
```

## 4. dotnet user-secrets
```
dotnet user-secrets init --project .\BuberDinner.Api
dotnet user-secrets set --project .\BuberDinner.Api "JwtSettings:Secret" "super-secret-key-from-user-secrets"
dotnet user-secrets list --project .\BuberDinner.Api

  <PropertyGroup>
    <UserSecretsId>20b9b69f-3983-45e1-bc0d-8bb5291de695</UserSecretsId>
  </PropertyGroup>
```