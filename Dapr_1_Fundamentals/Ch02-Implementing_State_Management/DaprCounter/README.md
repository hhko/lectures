### DaprCounter 실행
```shell
dapr run --app-id DaprCounter -- dotnet run --project .\DaprCounter\
```

### Redis 컨테이너 값 확인
```shell
# Redis 컨테이너 접속
docker container exec -it dapr_redis redis-cli

# Redis 키 목록 확인
keys *

# Redis 값 확인
# DaprCounter : --app-id DaprCounter
# counter : "key": "counter"
hgetall DaprCounter||counter
```