---
layout: default
title: ps -ef | grep 명령어
parent: Linux
grand_parent: Language
nav_order: 2
---

# **ps -ef | grep 명령어**

{: .bg-purple-000}

---

```
ps -ef | grep (찾을 단어)
```

{: .text-purple-100}

### ps(Process Stataus)

현재 실행중인 프로세스 목록을 보여주는 명령어이다.

- -e: 모든 프로세스를 출력한다.
- -f: 풀 포맷으로 보여준다. (UID, PID) 등

{: .text-purple-100}

### grep

특정 문자열을 찾는 명령어이다.

- -i: 대소문자 구분하지 않고 검색한다.
- -n: 줄 번호를 함께 출력한다.
- -x: 패턴과 단어 자체가 일치하는 라인을 출력한다.

{: .text-purple-100}

### 파이프라인(|)은 왜 사용하는 것인가?

`명령어 1 | 명령어 2`와 같은 형태에서는 명령어 1의 처리 결과를 명령어 2로 전달한다. 즉 결과를 바로 넘겨서 다음 명령에 사용할 수 있다.
