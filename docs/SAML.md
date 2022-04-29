# SAML 기술소개

### SAML은 Security Assertion Markup Language의 줄임마로써, 같은 네트워크 내의 인증과 권한에 관한 데이타를 서로 교환하기 위한 표준입니다.
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


클라이언트
웹브라우저 또는 단말


Service Provider
클라이언트가 접근하려는 애플리케이션 또는 서비스 (웹엑스 또는 재버)


Identity Provider(IdP)
사용자 크리덴셜 (사용자명과 패스워드)을 인증하고 SAML Assertion을 발행


SAML Assertion
사용자 인증을 위해 IdP로 부터 SP로 전달되는 보안 정보
사용자명, 권한 등의 내용을 적은 XML 문서로 변조를 막기위해 전자서명됨


SAML Request (인증 요청)
Service Provider 가 생성하는 인증 요청으로 IdP로 인증 위임


Circle of Trust (CoT)
하나의 IdP를 공유하는 Service Provider 들로 구성


Metadata
SSO를 활성화하는 Service Provider 및 IdP 가 생성하는 XML 파일
메타데이타의 교환으로 신뢰 관계 설립


Assertion Consumer Service (ACS) URL
ACS URL은 IdP가 특정 URL로 최종 SAML 응답을 포스트하도록 요구한다.



SAML SSO 은 Assertions, 프로토콜, 바인딩 그리고 프로파일의 특별한 결합입니다. 여러가지 Assertion은 프로토콜과 바인딩을 사용하는 애플리케이션과 사이트 사이에서 교환됩니다. 이 Assertion은 사이트간의 사용자들을 인증합니다.




[참고]
https://hooeon.tistory.com/entry/SAML-20
