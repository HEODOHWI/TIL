# SAML 기술소개 :grinning:

### SAML은 Security Assertion Markup Language의 줄임마로써, 같은 네트워크 내의 인증과 권한에 관한 데이터를 서로 교환하기 위한 표준입니다.
주로 아래 4가지 사항을 위해 이용되는데, 제일 중점적으로 쓰이는 곳은 웹기반은 SSO 인증을 위한 경우 입니다.

**Internet SSO/Security/Accesss/Admin**

많은 기업에서 SAML 2.0 기반의 SSO를 구현하는 이유는 다음과 같은 이점이 있기 때문입니다.

1. 암호 피로 (Password fatigue) 감소
  - 사용자가 여러 개의 비밀번호와 유저 네임의 쌍을 외워야 하는 정신적인 피로도를 의미하는 암호피로의 감소

2. 인증 위임
  - 다수의 Service Provider 와 단 하나의 IdP 간의 CoT를 생성하여 IdP로 인증 위임되므로 사용자는 단 한번의 로그인으로 다수의 Service Provider를 사용할 수 있음

3. 안전한 인증 정보의 보호
  - IdP, SP, 사용자 사이에서 교환되는 인증정보를 암호화

4. 개인 생산성 향상
  - 지속적으로 패스워드를 재입력하는 과정이 생략되고, 패스워드 재설정 및 복구에 따른 과정이 필요없음

## SAML 기반의 SSO 주요 요소
SAML 의 동작 방식을 이해하기 위해서 먼저 몇가지 구성 요소를 살펴보겠습니다.

![This is an image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbCGBxm%2FbtqDw4ebkOY%2FQLtJKyfnRL7w7dRKv0jSdK%2Fimg.png)

- 클라이언트 : 웹브라우저 또는 단말

- Service Provider : 클라이언트가 접근하려는 애플리케이션 또는 서비스 (웹엑스 또는 재버)

- Identity Provider(IdP) : 사용자 크리덴셜 (사용자명과 패스워드)을 인증하고 SAML Assertion을 발행

- SAML Assertion : 사용자 인증을 위해 IdP로 부터 SP로 전달되는 보안 정보
  - 사용자명, 권한 등의 내용을 적은 XML 문서로 변조를 막기위해 전자서명됨

- SAML Request (인증 요청) : Service Provider 가 생성하는 인증 요청으로 IdP로 인증 위임

- Circle of Trust (CoT) : 하나의 IdP를 공유하는 Service Provider 들로 구성

- Metadata : SSO를 활성화하는 Service Provider 및 IdP 가 생성하는 XML 파일.
  - 메타데이타의 교환으로 신뢰 관계 설립

- Assertion Consumer Service (ACS) URL : ACS URL은 IdP가 특정 URL로 최종 SAML 응답을 포스트하도록 요구한다.


SAML SSO 은 Assertions, 프로토콜, 바인딩 그리고 프로파일의 특별한 결합입니다. 여러가지 Assertion은 프로토콜과 바인딩을 사용하는 애플리케이션과 사이트 사이에서 교환됩니다. 이 Assertion은 사이트간의 사용자들을 인증합니다.

## SAML 2.0 기반의 인증 과정
IdP와 Service Providor 간에 메타데이타를 교환하여 신뢰 관계 설립한 후 SAML 2.0 은 다음과 같이 동작합니다.

![This is an image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FW9IQ8%2FbtqDzDsthki%2F1dV3sJtkzXKfGTgxNuGbg1%2Fimg.png)

Access Resource (애플리케이션 접속)
사용자가 웹브라우저에서 최초로 Service Provider 로 접속합니다. 아직 웹브라우저가 세션을 활성화한 상태는 아닙니다.


Redirect with SAML Authentication Request (인증 요청)
Service Provider 는 인증요청(Authentication Request)를 생성하여 클라이언트로 전송합니다.
IdP URL은 SAML 메타데이타 교환 과정에서 사전 구성됩니다. SP는 iDP와 직접 통신하지는 않고, 사용자의 웹브라우저가 iDP로 인증 요청을 redirect 하도록 합니다.

인증 요청은 다음과 같이 보입니다.

HTTP/1.1 302 Found

Location: https://pingsso.home.org:9031/idp/SSO.saml2?SAMLRequest=nZLNbtswEITveQqCd1m0pKoWYRlwYxQ1kDZK5OaQG02tYwISqXLJtH37kkra%2FBjwodflcPab3V2iGPqRr7076lv44QEdIb%2BGXiOfXmrqreZGoEKuxQDIneTt%2BusVz2aMj9Y4I01PL7abmmJWVCxnku07sYCqFAu2KGWVdaycV1AWRbnPPjJZlDkld2BRGV3TYEPJFtHDVqMT2oUSm%2BcJq5Ks2LGK5x84K%2B8p2QQ0pYWbfh2dG5Gn6aj0A6KZHc0AM2MfeACYp6ob07a9nsUEGSWfjZUwJazpQfQIsWEjENUj%2FKs0z1E%2BKd0F0%2FO5908i5F92uyZprtsdJWtEsJHu0mj0A9gW7KOS8P326oVXejkk4F94F0WRpyEBjmmkjdip6JXAEyldXSyjhE%2FDsq%2BWdJ5V%2FOWiq%2FeWy%2FSV4bP9yL8Fi%2B2mMb2Sv%2F%2FnFuK8B%2BHOq2NFdclhknJnhUYF2lHSNrH%2FjQ9DOCiwNT2ZA1n3vfl5aUG4sD5nPdDVU5K37CFQenrdqz8%3D&RelayState=s249030c0bda8e96a8086c92d0619e6446b270c463

인증 요청을 아래와 같이 디코딩하였습니다.


ID="s249030c0bda8e96a8086c92d0619e6446b270c463"

Version="2.0"

IssueInstant="2013-09-19T09:35:06Z"

Destination="https://pingsso.home.org:9031/idp/SSO.saml2"

ForceAuthn="false"

IsPassive="false"

ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"

AssertionConsumerServiceURL="https://cucm-eu.home.org:8443/ssosp/saml/SSO/alias/cucm-eu.home.org">

cucm-eu.home.org

 

Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"

SPNameQualifier="cucm-eu.home.org"

AllowCreate="true"

/>

 





GET with SAML Authentication Request (인증 요청 획득)
클라이언트는 인증 요청을 그대로 IdP로 전송합니다. 아직 사용자의 브라우저는 IdP와 세션이 활성화되지 않았습니다.

Challenge for Credential (로그인 요청)
IdP는 사용자 웹브라우저에게 로그인을 요청합니다. 인증방식은 사용자명과 패스워드, PKI 등 다양하게 사용할 수 있습니다.


Credential (로그인 성공)
클라이언트는 요구되는 인증방식으로 인증을 시도합니다. 이과정에서 Service Provider는 개입하지 않습니다. IdP가 LDAP 서버로 인증을 다시 위힘할 경우에는 LDAP으로 경로가 증가하지만 여기서는 생략합니다.


Signed response in hidden HTML form
IdP는 SP를 위해 SAML response를 생성하여 사용자의 웹브라우저로 전송합니다. SAML Response는 SAML assertion이 포함됩니다. iDP는 웹브라우저에 Session cookie (세션 쿠키)를 설정하고, 이정보는 웹브라우저에 캐싱됩니다.


POTS signed response
클라이언트는 Service Provider 의 ACS URL에 Assertion을 포스팅합니다.


Supply Resoures (자원 접속)
SP는 POST로 부터 SAML assertion을 추출합니다.



[참고]
https://hooeon.tistory.com/entry/SAML-20
