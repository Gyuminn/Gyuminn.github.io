---
layout: default
title: Docker 기본 명령어
parent: Docker
grand_parent: Cloud
nav_order: 1
---

# **Docker 기본 명령어**

{: .bg-purple-000}

---

## Docker run 명령어

```
docker run [옵션] [이미지이름 or 이미지Id] [실행할 파일]
```

### [옵션]

- -i: 사용자가 입출력할 수 있는 상태
- -t: 가상 터미널 환경을 에뮬레이션 하겠다.
- -d: 컨테이너를 일반 프로세스가 아닌 데몬 프로세스로 실행하여 프로세스가 끝나도 유지되도록 한다.
- -e: 환경변수 설정, 옵션을 사용하면 Dockerfile의 ENV 설정도 덮어씌어지게 된다.
- -p: 호스트 컴퓨터에서 설정한 포트
- -h: 컨테이너의 호스트 이름을 설정한다.
- --link: Docker 컨테이너끼리 연결할 때는 `docker run` 명령에서 `--link` 옵션을 사용
- --rm: 컨테이너를 일회성으로 실행할 때 주로 쓰이고, 컨테이너가 종료될 떄 컨테이너와 관련된 리소스(파일 시스템, 볼륨)까지 꺠끗이 제거해준다.
