## [Docker 명령어 요약] 

`docker run`과 `docker start`는 모두 Docker 컨테이너를 실행하는 명령어이지만, **용도와 동작 방식**에 차이가 있습니다. 

---

## 🚀 **1. `docker run`**  
### ✅ **설명:**  
- **새로운 컨테이너를 생성하고 실행**합니다.  
- 지정한 이미지로부터 컨테이너를 **처음부터** 시작합니다.  
- 이미지가 로컬에 없으면, **자동으로 다운로드**한 후 실행합니다.  
- `docker run`은 내부적으로 다음과 같은 과정을 수행합니다:
  1. `docker create` (컨테이너 생성)  
  2. `docker start` (컨테이너 시작)  
  3. `docker attach` (필요할 경우 표준 입출력 연결)

### 📝 **기본 사용법:**
```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### 💡 **예제:**
```bash
docker run -d -p 8080:80 nginx
```
> 위 명령어는 `nginx` 이미지로부터 새로운 컨테이너를 생성하고, 포트를 매핑하여 백그라운드(`-d`)에서 실행합니다.

### ⚡ **주요 옵션:**
- `-d`: 백그라운드에서 실행 (detached mode)  
- `-p`: 포트 매핑 (`호스트:컨테이너`)  
- `--name`: 컨테이너 이름 지정  
- `-v`: 볼륨 마운트  
- `-e`: 환경 변수 설정  

---

## 🔄 **2. `docker start`**  
### ✅ **설명:**  
- **이미 생성된 컨테이너를 시작**합니다.  
- 컨테이너가 **중지(`stopped`) 상태**일 때 사용합니다.  
- 컨테이너가 처음 실행되었을 때의 **설정 및 옵션을 재사용**합니다.  
- `docker run`과 달리 새로 이미지를 다운로드하거나 컨테이너를 생성하지 않습니다.

### 📝 **기본 사용법:**
```bash
docker start [OPTIONS] CONTAINER
```

### 💡 **예제:**
```bash
docker start mycontainer
```
> 이름이 `mycontainer`인 기존 컨테이너를 시작합니다.

### ⚡ **주요 옵션:**
- `-a`: 컨테이너의 표준 출력과 연결 (attach)  
- `-i`: 입력을 활성화 (interactive)

---

## 🔍 **3. 주요 차이점 비교**

| 🏷️ **기능**           | 🚀 **`docker run`**                      | 🔄 **`docker start`**                 |
|-------------------|--------------------------------------|-----------------------------------|
| 🛠️ **용도**         | 새 컨테이너 생성 후 실행                 | 기존에 생성된 컨테이너를 재실행        |
| 💾 **이미지 다운로드** | 로컬에 이미지가 없으면 다운로드           | 다운로드 없음 (이미 생성된 컨테이너 사용) |
| ⚙️ **설정 재정의**    | 새로운 옵션 및 설정 적용 가능              | 초기 설정을 그대로 사용               |
| 🔄 **컨테이너 상태**  | **항상 새 컨테이너** 생성                | **중지된 컨테이너**를 재시작           |
| 🖇️ **명령어 실행**   | 새로운 명령어 전달 가능                  | 기존 시작 명령어만 사용 (`CMD`, `ENTRYPOINT`) |
| 🔄 **중지된 컨테이너 재실행** | ❌ 새로운 컨테이너 생성 필요            | ✅ 한 줄로 간단하게 재실행 가능        |

---

## 🧪 **4. 예제 시나리오로 이해하기**  

### 🎬 **Step 1: `docker run`으로 새 컨테이너 생성**
```bash
docker run --name webserver -d -p 8080:80 nginx
```
- `nginx` 이미지를 기반으로 `webserver`라는 이름의 컨테이너를 생성하고 실행합니다.

---

### 🛑 **Step 2: 컨테이너 중지**
```bash
docker stop webserver
```
- `webserver` 컨테이너를 중지합니다.

---

### 🔄 **Step 3: `docker start`로 동일 컨테이너 재시작**
```bash
docker start webserver
```
- **동일한 설정과 상태로 컨테이너를 다시 시작**합니다.  
- `docker run`을 다시 사용할 필요 없이 간단히 재실행됩니다.

---

## ⚡ **5. 실전 활용 팁**  

| 🌟 **요구사항**                  | 🏃 **추천 명령어**          |
|------------------------------|----------------------|
| 새로운 앱 컨테이너 실행           | `docker run`         |
| 한 번 중지한 컨테이너 재시작       | `docker start`       |
| 옵션 변경 후 새 컨테이너 실행      | `docker run` (옵션 수정) |
| 재부팅 후 이전 컨테이너 복구 실행   | `docker start`       |

---

## 📝 **6. 한 눈에 정리: 핵심 요약**  
- ⚡ `docker run`: **처음부터 새 컨테이너 생성** + 실행  
- 🔄 `docker start`: **기존 컨테이너 재시작** (빠르고 설정 유지)  
- 🚀 새 기능 추가나 설정 변경 시 `run` 사용  
- 🔄 단순한 재시작은 `start` 사용  

---


```
# Docker 이미지 Pull
docker pull [이미지 이름]

# Docker 이미지 확인
- docker image ls

# 새로운 이미지 태그 지정 (alpine:3.10 -> alpine:custom_3.10)
docker image tag alpine:3.10 alpine:custom_3.10

# 실행중인 컨테이너 확인
docker ps

# 종료된 컨테이너까지 확인
docker ps -a

```

## docker prune 커맨드
- docker container prune : 중지된 모든 컨테이너를 삭제
- docker image prune : 이름 없는 모든 이미지를 삭제
- docker network prune : 사용되지 않는 도커 네트워크를 모두 삭제
- docker volume prune : 도커 컨테이너에서 사용하지 않는 모든 도커 볼륨을 삭제

## docker 컨테이너 로그 확인
```
docker logs -f --tail --it $container-ps-id

docker logs --follow --tail --it $container-ps-id
```

