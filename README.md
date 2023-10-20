![Untitled](https://github.com/Kernel360/hackerthon1-doitfor/assets/103917282/3ba325ba-2c80-4220-a173-cebc879a7e78)



# 프로젝트 개요

이 프로젝트는 Spring Boot를 사용하여 개발된 웹 애플리케이션입니다. 이 애플리케이션은 다음과 같은 주요 특징을 갖고 있습니다:

- **Spring Boot 2.7.16**: Spring Boot의 최신 버전을 사용하여 개발되었습니다.
- **Spring Data JPA**: 데이터베이스 액세스 및 관리를 위한 Spring Data JPA를 사용합니다.
- **Thymeleaf**: Thymeleaf 템플릿 엔진을 사용하여 웹 페이지를 동적으로 생성합니다.
- **Lombok**: Lombok을 사용하여 코드를 간결하게 작성합니다.
- **MySQL Connector**: MySQL 데이터베이스와의 연결을 위해 MySQL Connector를 사용합니다.

## hackerthon1-doitfor
shortURL을 만들어주는 서비스입니다.

이 Java Spring Boot 애플리케이션인 "Doitforme"은 URL 단축 서비스를 제공합니다. 사용자는 긴 URL을 짧게 변환하고 변환된 URL을 사용하여 쉽게 원본 URL에 액세스할 수 있습니다. 이 애플리케이션은 다음과 같이 구성되어 있습니다.

- **컨트롤러**: `UrlController` 클래스는 URL 경로 설정 및 사용자 인터페이스와 상호 작용을 담당합니다.

- **DTO (데이터 전송 객체)**: 애플리케이션은 데이터를 프런트엔드와 백엔드 간에 전송하기 위해 `UrlRequest` 및 `UrlResponse`와 같은 DTO를 사용합니다.

- **엔티티**: `Url` 엔티티는 URL 레코드를 나타내며 원본 및 변환된 URL에 대한 정보를 저장합니다.

- **리포지토리**: `UrlRepository`는 엔티티의 데이터 저장 및 검색에 대한 데이터베이스 상호 작용 및 CRUD 작업을 처리합니다.

- **서비스**: `UrlService` 클래스에는 URL 단축에 대한 핵심 비즈니스 로직이 포함되어 있으며 데이터 저장 및 검색을 위해 리포지토리와 상호 작용합니다.

- **Audit**: 애플리케이션은 엔티티의 생성 및 수정 타임스탬프를 자동으로 캡처 및 관리하기 위해 JPA Audit을 활용합니다.

## 사용법

- 주 메인 페이지를 확인하려면 루트 URL (예: `http://localhost:8080/`)에 액세스합니다.
- 제공된 입력 필드에 긴 URL을 입력하고 "단축" 버튼을 클릭하여 단축 URL로 변환합니다.
- 단축 URL이 표시된 페이지로 리디렉션됩니다.
- 단축 URL에 액세스하면 원본 URL로 리디렉션됩니다.

## 애플리케이션 구성요소

### UrlController

- `GET /`: 주 메인 페이지를 표시합니다.
- `GET /result`: 쿼리 매개변수로 변환된 URL이 포함된 주 메인 페이지를 표시합니다.
- `POST /api/v1/shoutUrl`: 긴 URL을 단축 URL로 변환하고 `/result` 페이지로 리디렉션합니다.
- `GET /{convertUrl}`: 변환된 URL을 기반으로 원본 URL로 리디렉션합니다.

### DTOs

- `UrlRequest`: URL 단축 요청의 데이터를 나타냅니다. 원본 및 변환된 URL이 포함됩니다.
- `UrlResponse`: URL 단축 응답의 데이터를 나타냅니다. 변환된 URL이 포함됩니다.

### 엔티티

- `Url`: 원본 URL, 변환된 URL 및 감사 타임스탬프에 대한 필드를 포함하는 URL 엔티티를 나타냅니다.

### 리포지토리

- `UrlRepository`: `Url` 엔티티의 데이터 액세스 메서드를 제공하며 변환된 URL을 기반으로 URL 레코드를 찾는 메서드를 포함합니다.

### 서비스

- `UrlService`: URL 단축을 위한 핵심 비즈니스 로직을 포함하며 단축 URL을 생성하고 원본 URL을 검색합니다.

## 애플리케이션 실행

1. 시스템에 Java와 Gradle이 설치되어 있는지 확인합니다.
2. 저장소에서 프로젝트를 복제합니다.
3. Gradle을 사용하여 프로젝트를 빌드합니다
4. 애플리케이션을 실행합니다

애플리케이션은 `http://localhost:8080/`에서 실행됩니다.

## 데이터베이스 구성

이 애플리케이션은 데이터 저장을 위해 MySQL 데이터베이스와 Spring Data JPA를 사용합니다. 데이터베이스 설정을 `application.yml` 파일에서 구성할 수 있습니다.

## 참고

이 README는 "Doitforme" URL 단축 애플리케이션의 개요를 제공합니다. 필요에 따라 자세한 문서 및 사용 지침을 제공할 수 있습니다.

<br>

# 개발 문서 일람

  ## 개발 목표
- 최소한의 기능을 수행하는 프로그램을 완성한다.
- 시연이 가능하도록 서버를 구축한다.
- DB 저장시 키 무결성을 항상 유지하도록 로직 수정 후 적용한다.
- 개선사항이 완료된 후 서비스를 오픈한다.

## 성능 목표
- 1일 1억건 (100M / 24H / 3600s, 초당 약 1천개)을 감내 할 수 있을 정도의 로직을 구성한다.
- 해시 생성 후 해시 충돌 회피 전략 구성을 고려한다.
- 분산 처리 시스템 도입시 PK값 유일성을 보장하는 방안을 고려한다.
- 배포서비스를 구축한다.

## 기술 스택
- 타임리프
- 스프링부트 2.8
- Spring Data JPA
- MYSQL 5.7
- Gradle
- 구름IDE

## API 명세서

| NO | 메서드 | 도메인 | URI | 쿼리 | 설명 | 응답 | 버전 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | POST | /{구름io 아이피} | /shoutUrl |  | 단축URL 생성 | 200: 성공     500 : 내부에러 | v.0.0.1 |
| 2 | GET | /{구름io 아이피} | /{shortUrl} |  | 원본URL 조회 | 3xx : redirect://[원본URL]             404: 만료or없음500: 내부에러 | v.0.0.1 |

## 요구사항 명세서

- 사용자가 입력한 원본url을 단축url로 변환하여 제공한다.
- 사용자가 브라우저에서 단축url을 입력하여 이동했을 경우 원본url 경로로 리다이렉트 시킨다.
- 잘못된 URL 형식의 원본url을 입력할 경우 사용자에게 오류 표시한다.
- 단축된 URL은 7자리로 생성한다.

## 테이블 명세서
![Untitled](https://github.com/Kernel360/hackerthon1-doitfor/assets/103917282/992ae026-cbe4-4a09-86c2-ec90ecff68d1)

## 커밋 메세지 컨벤션 

**feat** : 새로운 기능 추가

**fix** : 버그 수정

**docs**: 문서 변경

**style** : 코드 스타일 변경 (포매팅 수정, 세미콜론 추가 등)

**refactor** : 코드 리팩토링

**test** : 테스트 코드 추가, 수정

**chore** : 빌드 프로세스, 도구 설정 변경 등 기타 작업

예시는 다음과 같다.

```bash
feat: place CRUD 기능 추가 # <scope> <title>

플레이스에 대한 CRUD 기능을 추가하였습니다. # <body>
```

## 성능테스트 방향
- junit 및 mock 데이터, nGrinder 통한 성능 측정
- 고려사항
    - 디스크 시간 - 요청을 작성하거나 읽기를 실행하는데 소요되는 시간
    - 대역폭 사용량 - 네트워크 인터페이스에서 사용되는 bit/s
    - 처리량 - 초당 수신 된 요청 비율
    - 스레드 수 - 활성 스레드 수
    - 메모리 사용 - 가상 메모리 사용 패턴
  시스템 로드 시간, 사용자 입력에 대한 응답 시간, 많은 수의 사용자를 수용하는 양 등을 고려
    
- 로컬 환경에서의 측정 방법
    - 테스트 영역에서 수행한다.
    - 1000rows 생성 된 mock 파일을 입력받아 파일 내용 1줄당 1요청으로 반복
      또는 임의의 http 주소를 정규표현식을 이용해 만들어 for문을 통해 반복 요청
        
    
- nGrinder를 이용한 성능 측정
    - 시나리오를 설정하여 하위의 값을 설정 후 테스트 진행, 결과에 따라 조율
        agent (프로세스 및 스레드),
        vuser per agent (사용자), 
        duration (수행시간) ,
        ramp-up(점진적 부하 증가량) 
    - ex) agent : 1대, 유저 : 1000, 테스트 시간 : 10분, ramp-up : 2

- 테스트 완료 후 결과를 통해 성능 분석 및 테스트 성공/실패 판정, 애메 할 경우 조정 후 재 실행

## 배포 정책
- 초기 컨테이너에 구축 환경 테스트 수행 시, 빠른 동작 판단을 위하여 jar를 사용한다.
- 실질적 배포 환경이 수립되었다면 nginx web과 tomcat was를 연동하여 오픈한다.
- 긴급사항 발생시 빠른 수정이 필요 할 경우 커밋 컨벤션 fix의 규격을 따라 동일하게 수행하고, 핫라인을 통해 연락 및 검수 받은 후 배포한다.




## 보완 및 개선 필요사항, 미비된점
- 사용자가 url 단축을 요청시 url의 perfix를 확인하여 누락되어 있으면 추가해주는 작업 필요
- 사용자가 url 단축을 요청하는 원본 url의 대한 validation 기능을 추가 했으나, 너무 긴 문자의 경우엔 정확하지 못하여 보완 필요
- 동일 주소에 대해 지속적으로 url단축 요청시, 키 생성 및 데이터 등록 과정에서 충돌이 발생하는 경우 이의 대한 재귀 처리 및 재시도, 실패의 대한 예외처리 및 안내하는 뷰 처리
- db의 축적된 데이터가 많을 때, 특정 도메인을 포함한 url을 요청 할 경우 도메인과 QueryString을 분리하여 각자 해싱, 저장하여 조회 속도 개선
- 프로그램에서 서버의 ip를 자동으로 perfix 하는 부분을 추가 했었는데, goorm.io의 내부 ip주소가 나와 도메인 지정 부분의 대한 환경변수 처리 등을 통해 수정 필요
  
- 설계시 만들어진 단축 url 값의 대한 보존 정책 미흡으로 인한 개발 방향 방황 (퀄리티와 별개로 알게되는 지식, 생각해야 할 범위들은 매우 뜻깊음)
- 테스트 시나리오를 작성하지 못하여 테스트 부족
- web - was까지 연동을 하고자 했는데, goorm.io 환경에서 설치 후 연동 실패
- 성능 측정 계획을 세웠지만 수행하지 못함..
- 해시 알고리즘으로 가공 된 값을 자른 후, db에 넣었을 때 충돌 회피 전략 또는 유일키 생성의 대한 방법이 많았으나 이해 부족으로 프로그램에 담지를 못하였음

