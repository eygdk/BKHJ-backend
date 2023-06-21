## 👋 안녕하세요! 환영합니다! 저희 프로젝트 관련 설명드리도록 하겠습니다.

##### 대출상품 추천 웹 애플리케이션 프로젝트 입니다.

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

##### ● 트러블슈팅


#  🕹 사용 기술 

### Back-end
- JAVA (11)
- MAVEN 
- jjwt (0.9.1)
- JPA
- React
- sts [3]
- Pycharm ( Community Edition 2023.1.2 )
- Python  (3.11.3)
- Flask
- ELK
- mysql

#  ✴️ 프로젝트 구조




https://github.com/sunyoungads/BKHJ-backend/assets/117277093/95476f79-559b-4f3a-8596-1b76be51ac7d




###### 구현 순서는 회원 기능 구현 => 게시판 기능 구현 => 댓글 기능 구현 => 파일 첨부 기능 구현 으로 진행하였습니다.





# 💲 구현 기능

● 게시판 기능
- 게시글 검색 (제목, 내용, 작성자)
- 게시글 작성,수정,삭제 

● 댓글 기능
- 댓글 작성,수정,삭제
    
● 회원 기능
- JWT 기능, Security기능, 
- 회원가입, 회원정보 수정 , 회원탈퇴
- 로그인/로그아웃

● 파일 첨부 기능
- 파일 추가,수정,삭제


# ✳️ 기능 설명

### 회원
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


## Security: 여기에서 Spring Security를 구성하고 보안 객체를 구현합니다.

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
 리포지토리에는 데이터베이스와 상호 작용하기 위해 Spring Data JPA JpaRepository를 확장하는 인터페이스가 있습니다.

● UserRepository: JpaRepository를 확장합니다.
● RoleRepository: JpaRepository를 확장합니다.
모델은 인증(User) 및 권한(Role)을 위한 두 가지 주요 모델을 정의합니다. 이들은 다대다 관계를 가지고 있습니다.

● User: id, username, email, password, roles
● Role: id, name

● 페이로드는 요청 및 응답 객체를 위한 클래스를 정의합니다.

● 또한, Spring Datasource, Spring Data JPA 및 앱 속성 (예: JWT 비밀 문자열 또는 토큰 만료 시간)을 구성하기 위해 application.properties 파일을 사용합니다.


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


## 지금까지 각 회원 관련 설명이 있었습니다 😄 많이 부족한 설명 들어주셔서 감사합니다.




