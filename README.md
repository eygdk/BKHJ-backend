## 👋 안녕하세요! 환영합니다! 저희 프로젝트 관련 설명드리도록 하겠습니다.

#### 대출상품 추천 웹 애플리케이션 프로젝트 입니다.

###### 2023.05.02 ~ 06.26 동안 Spring Boot 와 React 와 Python 를 사용해 구현했습니다.

###### 이 프로젝트를 통해 이루고자 한 목표는 Spring과 react에 연동 방식 및 Python의 라이브러리 및 프레임워크를 직접 사용해 보려고 하였습니다. 

###### 프로젝트 구현 과정 동안 회원 인증/인가, Rest api 연동 및 Python의 Data 수집 및 react와 연결을 고민하며 코드를 작성하였습니다.

## ✨ 접근 방식 

##### 과정1 :  React + java + SpringBoot + JPA + DB [my sql ]기반의 웹어플리케이션 개발

##### 과정2: Python 기반의 데이터분석: 수집(web scraping) + 정제(numpy,pandas) + 분석 + 시각화(ELK)

##### 과정3: Python 기반의 데이터 예측: AI 알고리즘 [ex)선형회귀, 로지스틱 회귀, DNN]을 활용하여 데이터 예측 시스템 구축


###### 언어는 Java를 사용하였으며, 회원과 게시판 기능은 React 및 Springboot를 통해서 구현하였습니다.
###### 또한, 과정2는 Python을 통해서 공공Api에 접근하여 데이터를 수집 및 정제하고, ELk를 통해서 해당 부분을 시각화하여 React로 다시 보여지도록 설정하였습니다  
###### 과정3는 파이썬을 통해서 데이터를 훈련시켜, 회원에 맞는 대출 상품을 추천하게 만들었습니다.



# 📚 목차

##### ● 사용 기술

##### ● 프로젝트 구조

##### ● 구현 기능 

##### ● 구현 설명 및 화면

##### ● Python 기반의 데이터 분석

##### ● Python 기반의 데이터 예측

##### ● ERD 모델


#  🕹 사용 기술 

### Back-end
##### - JAVA (11)
##### - MAVEN 
##### - jjwt (0.9.1)
##### - JPA
##### - React
##### - sts [3]
##### - Pycharm ( Community Edition 2023.1.2 )
##### - Python  (3.11.3)
##### - Flask
##### - ELK
##### - mysql

#  ✴️ 프로젝트 구조




https://github.com/sunyoungads/BKHJ-backend/assets/117277093/95476f79-559b-4f3a-8596-1b76be51ac7d




###### 구현 순서는 회원 기능 구현 => 게시판 기능 구현 => 댓글 기능 구현 => 파일 첨부 기능 구현 으로 진행하였습니다.





# 💲 구현 기능

##### ● 게시판 기능
- 게시글 검색 (제목, 내용, 작성자)
- 게시글 작성,수정,삭제 

##### ● 댓글 기능
- 댓글 작성,수정,삭제
    
##### ● 회원 기능
- JWT 기능, Security기능, 
- 회원가입, 회원정보 수정 , 회원탈퇴
- 로그인/로그아웃

##### ● 파일 첨부 기능
- 파일 추가,수정,삭제


# ✳️ 기능 설명

## ✔ 회원
#### Spring Security

###### ●  WebSecurityConfigurerAdapter**는 보안 구현의 핵심입니다. HttpSecurity 구성을 제공하여 cors, csrf, 세션 관리, 보호된 리소스에 대한 규칙을 구성할 수 있습니다. 또한 기본 구성을 확장하고 사용자 정의할 수도 있습니다.

###### ● UserDetailsService 인터페이스에는 사용자 이름으로 사용자를 로드하고 Spring Security가 인증과 유효성 검사에 사용할 수 있는 UserDetails 개체를 반환하는 메서드가 있습니다.

###### ● UserDetails에는 인증 개체를 구축하는 데 필요한 정보 (사용자 이름, 비밀번호, 권한 등)가 포함되어 있습니다.

###### ● UsernamePasswordAuthenticationToken은 로그인 요청에서 {사용자 이름, 비밀번호}를 가져옵니다. AuthenticationManager는 이를 사용하여 로그인 계정을 인증합니다.

###### ● AuthenticationManager에는 DaoAuthenticationProvider (UserDetailsService 및 PasswordEncoder의 도움을 받아)가 있어 UsernamePasswordAuthenticationToken 개체를 유효성 검사합니다. 성공하면 AuthenticationManager는 권한이 부여된 권한을 포함한 완전히 채워진 인증 개체를 반환합니다.

###### ● OncePerRequestFilter는 API에 대한 각 요청에 대해 단일 실행을 수행합니다. 우리는 JWT를 구문 분석하고 유효성을 검사하며 (UserDetailsService를 사용하여) 사용자 세부 정보를 로드하고 (UsernamePasswordAuthenticationToken을 사용하여) 권한을 확인하는 doFilterInternal() 메서드를 제공합니다.

###### ● AuthenticationEntryPoint는 클라이언트가 인증 없이 보호된 리소스에 액세스하는 경우 권한 없음 오류를 감지하고 401을 반환합니다.

###### ● Repository에는 Database와 작업하기 위한 UserRepository 및 RoleRepository가 있으며, Controller에 가져올 것입니다.

###### ● Controller는 OncePerRequestFilter에 의해 필터링된 요청을 받고 처리합니다.

###### ● AuthController는 회원 가입/로그인 요청을 처리합니다.

###### ● TestController에는 역할 기반 검증이 있는 보호된 리소스에 액세스하는 메서드가 있습니다.

★ 코드는 Git에서 확인 및 참고 부탁드립니다.


#### Security: 여기에서 Spring Security를 구성하고 보안 객체를 구현합니다.

###### ● WebSecurityConfig은 SecurityFilterChain filterChain 를 확장합니다.[주의 WebSecurityConfigurerAdapter(deprecated)] 
###### ● UserDetailsServiceImpl은 UserDetailsService를 구현합니다.
###### ● UserDetailsImpl은 UserDetails를 구현합니다.
###### ● AuthEntryPointJwt는 AuthenticationEntryPoint를 구현합니다.
###### ● AuthTokenFilter는 OncePerRequestFilter를 확장합니다.
###### ● JwtUtils는 JWT 생성, 구문 분석, 유효성 검사를 위한 메서드를 제공합니다.
###### ● 컨트롤러는 회원 가입/로그인 요청 및 인증된 요청을 처리합니다.
###### ●  @RequestMapping("/api/auth") 
###### ● AuthController: @PostMapping('/signin'), @PostMapping('/signup')
###### ● TestController: @GetMapping('/api/test/all'), @GetMapping('/api/test/[role]')
###### ● 리포지토리에는 데이터베이스와 상호 작용하기 위해 Spring Data JPA JpaRepository를 확장하는 인터페이스가 있습니다.

###### ● UserRepository: JpaRepository를 확장합니다.
###### ● RoleRepository: JpaRepository를 확장합니다.
###### 모델은 인증(User) 및 권한(Role)을 위한 두 가지 주요 모델을 정의합니다. 이들은 다대다 관계를 가지고 있습니다.

###### ● User: id, username, email, password, roles
###### ● Role: id, name

###### ● 페이로드는 요청 및 응답 객체를 위한 클래스를 정의합니다.

###### ● 또한, Spring Datasource, Spring Data JPA 및 앱 속성 (예: JWT 비밀 문자열 또는 토큰 만료 시간)을 구성하기 위해 application.properties 파일을 사용합니다.


![image](https://github.com/sunyoungads/BKHJ-backend/assets/117277093/d47b1764-deda-4e8f-9132-d244c656aa68)

###### ● datasource.url = DB Tool로 연결 (mysql)
###### ● hibernate.ddl -auto = update [sts 실행 시, 자동으로 DB로 데이터를 넘기는 역할]
###### ● jwtSecret, jwtExpirationMs = 각 토큰 값 설정 [중요]
###### ● file-size = 각 파일 크기 지정


## OverView

  Methods |  Urls |  Actions
   ----- | --- | ---
POST	| /api/auth/signin	| 로그인 

POST	| /api/auth/sign up	| 회원가입

Delete	| /api/auth/delete/{id}	| 회원탈퇴

PUT| 	/api/auth/update/{id}	| 회원수정


### 회원관련 CRUD 화면 설명은 넘어가도록 하겠습니다.[코드로 봐도 다들 아시죠?!] 🤩

#####  그래도, 간략하게 작성 순서만 말씀드리도록 하겠습니다.

models(.java) =>  Repository(인터페이스 생성) => Service 및 ServiceImpl-> Controller 

## 구현 화면

https://github.com/sunyoungads/BKHJ-backend/assets/117277093/29dad353-26da-4190-925a-2ab73163ad02


##### 지금까지 각 회원 관련 설명이 있었습니다 😄 많이 부족한 설명 들어주셔서 감사합니다.
##### 다음으로는 게시판 관련 설명이 있습니다.

## ✔ 게시판 기능

#### 게시판도 동일하게 아래에 순서로 작성해주시면 문제 없습니다!!

models(.java) =>  Repository(인터페이스 생성) => Service 및 ServiceImpl-> Controller 

CRUD 기능만 설정되어 있기에, 따로 설명은 하지 않도록 하겠습니다!



## 게시판 구현 화면


https://github.com/sunyoungads/BKHJ-backend/assets/117277093/e7e03773-bd9a-4b01-b1a7-bc57fd081fb6



## OverView

  Methods |  Urls |  Actions
   ----- | --- | ---
POST	| /api/auth/saveBoard	| 게시판 작성 

POST	| /api/auth/listBoard	| 전체 게시판 

GET	| /api/auth/{id}	| 각 게시판 불러오기

GET| 	/api/auth/deleteBoard/{id}	| 게시판 삭제

Post| 	/api/auth/editBoard/{id}	| 게시판 수정



## ✔ 댓글 기능


##### 댓글 기능은 중요한 포인트가 존재합니다.

① comment.java[model] 에 게시판에 PK를 가져와야 합니다. 
![image](https://github.com/sunyoungads/BKHJ-backend/assets/117277093/a6c69768-94b2-4ddf-ac85-533df05016ed)

② 마찬가지로 각각, Controller , Repository ,Serivce에도 해당 board ID를 추가하셔야 합니다.

###### 해당 부분만 조심하시면 댓글을 구현하기에 어려움이 없을 것 같습니다.




## ✔ 첨부 파일 기능

#### 첨푸 파일 기능에도 중요한 포인트가 있습니다.


① 댓글과 마찬가지로 Board_id[Pk] 값을 속성으로 가져와야 합니다.
![image](https://github.com/sunyoungads/BKHJ-backend/assets/117277093/73f8b951-9f63-46cd-8f78-26bda2685ac5)

② 댓글 구성과 다른점은, 게시판 등록 시 파일과 게시판이 같이 저장되는 것을 염두해두어야합니다. [중요]

③ 파일 부분에 대해서 예외처리가 꼭 필요합니다.
![image](https://github.com/sunyoungads/BKHJ-backend/assets/117277093/7c940b8c-85bd-4e4d-9b91-e3bdb1ab8375)

④ 간략 설명


###### – FileInfo업로드된 파일의 정보를 포함합니다.

###### – FilesStorageService저장소 초기화, 새 파일 저장, 파일 로드, 파일 정보 목록 가져오기, 모든 파일 삭제를 도와줍니다.

###### – Rest API 내보내기에 FilesController사용 FilesStorageService: 파일 게시, 모든 파일 정보 가져오기, 파일 다운로드.

###### – FileUploadExceptionAdvice컨트롤러가 파일 업로드를 처리할 때 예외를 처리합니다.

###### – application.properties 에는 Servlet Multipart에 대한 구성이 포함되어 있습니다.

###### – uploads 는 파일을 저장하기 위한 정적 폴더입니다.

###### – Spring Boot 의존성을 위한 pom.xml.


## OverView

  Methods |  Urls |  Actions
   ----- | --- | ---
POST	| /api/comments	| 댓글 작성 

POST	| /board/{boardId}	| 댓글에 게시판 id 연결 

Put	| /{commentId}	| 각 댓글 불러오기

Delete|  /{commentId}}	| 댓글 삭제

Post| 	/api/auth/upload	| 파일 첨부

GET| 	/api/auth/files	| 전체 파일 보기 

GET| 	/api/auth//files/{id}	| 각 파일 아이디 추출

GET| 	/api/auth//files/board/{boardId}	| 첨푸파일에 게시판 아이디 생성



## 댓글 및 파일 첨부 화면



https://github.com/sunyoungads/BKHJ-backend/assets/117277093/29ffe622-22e0-4caa-bcc8-25af952623dd



## 🌟 여기까지가, 스프링으로에 구현 입니다. 나머지는 Front에서의 리액트를 확인해주시면 됩니다. Link[https://github.com/Hooddduck/BKHJ-frontend]
### 다음으로는, Python 관련해서 설명 드리도록 하겠습니다.


## ✔ Data 수집 

##### 일단 저희가 목표로 한 부분은 대출상품을 가져와서 비교하려는 부분입니다.   

##### 그래서 해당 데이터는 공공데이터포탈사이트: [https://www.data.go.kr/data/15074500/openapi.do] 에서 다운받았습니다.

## ✔ Data 정제 및 분석 [Python]

##### ★ Tool은 Pycharm

##### ★ Json형태로 파싱

##### ★ 사용 가능한 column 파싱 [ 공공 data 에서 원하는 부분만 뽑아낸다 ]

##### ★ CSV파일로 다운로드 변환 시키기[ ELk에 파일 자체를 등록하기 위해서 필요하다]

### 코드 확인 [Python]
[분석code.txt](https://github.com/sunyoungads/BKHJ-backend/files/11816779/code.txt)


## ✔ Data 시각화

##### ★ 해당 부분은 그래프로 표현하려고 했지만, 저희 프로젝트에 목표와 맞지 않아서, Python => ELk => Rest Api로 데이터 호출하여 React에서 대출상품을 비교하는 형태로 변경하였습니다.
##### 이 부분이 필요하다면, Front에서 확인하기를 바랍니다. Link[https://github.com/Hooddduck/BKHJ-frontend]


## ✨ AI 예측

##### ★ 프로젝트에 최종 목표는 고객에게 많은 빅데이터에서 많은 사람들이 선호하는 상품을 자동으로 추천하는 것이였습니다.

##### 하지만, 고객 Data는 개인정보 보호법으로 인해서 다운로드 어려워, 저희는 임의의 DummyData를 생성해서  어떤 고객들이 어떤 상품을 구매했다고 가정하여, 가상으로 Data를 생성하였습니다.

##### ★ 같은 나이, 성별에서 가장 많이 산 상품을 추천해주는 프로그램을 생성했습니다. [AI 예측] 단, 더 많은 컬럼을 사용하려고 했지만, 데이터 수집에 어려움이 있었습니다. [preditmodel.xls] , [회원가입과 동시에 예측 가능] 

##### ★ 대출한도, 대출기간을 통해서 금리를 예측하는 AI프로그램을 만들었습니다.[LoanProudct.5.xlsx]
        [대출한도, 대출기간 입력을 통한 예측]
        
##### 아래는 RawData입니다.
[LoanProduct 5.xlsx](https://github.com/sunyoungads/BKHJ-backend/files/11816923/LoanProduct.5.xlsx)


[preditmodel.xls](https://github.com/sunyoungads/BKHJ-backend/files/11816919/preditmodel.xls)



##### 아래는 AI Python 코드 입니다.
##### 간단한, 설명은 코드안에 설정하였습니다. 
##### Python을 Flask를 통해서 서버를 만들어 진행하였고, mysql에 직접적으로 들어가서, 회원정보를 가져와서 리액트로 뿌려주는 형태로 만들었습니다.

[AI예측.txt](https://github.com/sunyoungads/BKHJ-backend/files/11817090/AI.txt)




## ✔ 대출 상품 예측 시각화 화면

###### 단, 이 전에 React 화면이 다른 부분은 [UI]을 따로 예쁘게 수정하였습니다.




https://github.com/sunyoungads/BKHJ-backend/assets/117277093/fe18b477-9a17-4f4d-b8be-e376a1d811b8




## ERD,화면


![image](https://github.com/sunyoungads/BKHJ-backend/assets/117277093/98aeaa55-833a-4a63-9af9-4e513910fe72)




# 지금까지 저의 글을 읽어주셔서 정말 감사합니다 🙋‍♀️ 
















