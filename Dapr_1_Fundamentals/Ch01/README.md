# Getting Started with Dapr

## 목차
- 배경
- Windows Dapr 사전 준비
- Self-Hosted Windows Dapr CLI 설치
- Self-Hosted Windows Dapr CLI 제거

## 배경
- Dapr는 CLI와 Runtime으로 구성되어 있다.
  특히 Runtime을 실행하기 위한 Self-Hosted와 Kubernetes 운영 환경을 제공한다.

## Windows Dapr 사전 준비
- Docker Desktop

## Self-Hosted Windows Dapr CLI 설치
```shell
# 1. CLI 설치
#    - 관리자 권한일 때
powershell -Command "iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1 | iex"

#    - 관리자 권한이 아닐 때
$script=iwr -useb https://raw.githubusercontent.com/dapr/cli/master/install/install.ps1; $block=[ScriptBlock]::Create($script); invoke-command -ScriptBlock $block -ArgumentList "", "$HOME/dapr"

# 2. CLI 설치 검증
#    - 새 Prompt 창 열기
dapr -v
dapr
```
- 참고 자료 : https://docs.dapr.io/getting-started/install-dapr-cli/

## Self-Hosted Windows Dapr CLI 제거
```shell
dapr uninstall --all
```
- 참고 자료 : https://docs.dapr.io/reference/cli/dapr-uninstall/

```shell
dapr init
dapr init --runtime-version 1.0.0
dapr init --from-dir .
docker network create dapr-network
dapr init --network dapr-network

dapr uninstall
dapr uninstall --all
dapr uninstall --network dapr-network

dapr status
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
```