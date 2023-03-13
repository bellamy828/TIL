# HTTP API 설계 예시

## Document

### 설계 예시

- /members/100
- files/star.jpg

### 특징

- 단일 개념
    - a file
    - Object instance
    - Database row

## Collection

### 설계 예시

- 회원 관리 시스템
    - 회원 목록 조회 → GET /members
    - 회원 등록→ POST /members
    - 회원 조회 → GET /members/{id}
    - 회원 수정 → PATCH /members/{id}
    - 회원 삭제 → DELETE /members/{id}

### 특징

- Server가 관리하는 Resource directory이며, 위 예시에서 Collection은 /members 이다.
- POST 기반으로 등록한다.
- Client는 등록될 Resource의 URI를 모른다.
- Server가 새로 등록된 Resource URI를 생성해준다.
    
    > HTTP/1.1 201 Created
    Location: /members/100
    > 
- 대부분의 경우 POST 기반으로 등록하는 Collection 형태이다.

## Store

### 설계 예시

- 파일 관리 시스템
    - 파일 목록 조회 → GET /files
    - 파일 조회→ GET /files/{filename}
    - 파일 등록 → PUT /files/{filename}
    - 파일 삭제 → DELETE /files/{filename}
    - 파일 대량 등록 → POST /files

### 특징

- Client가 관리하는 Resource Store이며, Resource의 URI를 알고 있어야 한다.
    - ex. PUT /files/star.jpg

## Controller(Control URI)

### 설계 예시

- /members/{id}/delete

### 특징

- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스를 실행하기 위해 동사를 직접 사용한다.
- HTML FORM과 같이 methods 사용 제약이 있을 때 뿐만 아니라 HTTP API를 설계할 때도 빈번하게 사용한다.
    - ex. 주문 pocess 처리

## HTML FORM Usage

### 설계 예시

- 회원 목록 조회 → GET /members
- 회원 등록 form → GET /members/new
- 회원 등록 → POST /members/new, /members
- 회원 조회 → GET /members/{id}
- 회원 수정 form → GET /members/{id}/edit
- **회원 수정** → **POST** /members/{id}/edit, /members/{id}
- **회원 삭제** → **POST** /members/{id}/**delete**

### 특징

- GET / POST만 지원한다.
    - 컨트롤 URI를 사용한다.
        - 동사로 된 Resource 경로를 사용하여 제약을 해결한다.
        - POST /members/new, POST /members/edit, POST members/delete…
