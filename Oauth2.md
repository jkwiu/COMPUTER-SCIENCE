1. OAuth
   1. 개요
      1. ``인가``를 위한 기술이다. ``인증``은 유저가 직접하고, ``권한``은 서비스에게 준다.
   2. 기본적인 개념
      1. 인증(Authentication)
         1. 사용자가 맞는지 진위를 확인한다.
      2. 인가(Authorization)
         1. 권한을 위임해 준다.
      3. Rule
         1. 유저
            1. Resource Owner
               1. 인증을 수행하는 주체
         2. 서비스 
            1. Client Third-party Application
               1. 권한을 위임받는 주체
         3. 구글
            1. Authorization Server
               1. 인증을 검증하고 권한을 부여하는 주체
            2. Resource Server
               1. 인가를 수행하고 리소스를 제공하는 주체
   3. 버전
      1. OAuth1.0
         1. Rule
            1. Resource Owner
            2. OAuth Client
            3. OAuth Server
               1. Resource Owner인증
               2. 인가 토큰 발급
               3. 보호된 리소스 관리
         2. 문제점
            1. Scope개념 없음
            2. 역할이 확실히 나눠지지 않음
            3. 토큰 유효기간 문제
            4. Client 구현 복잡성
            5. 제한적인 사용환경
         3. 웹 환경
            1. 1세대 웹환경
      2. OAuth2.0
         1. Scope기능 추가
            1. 해당 토큰에 대해서 얼마나 접근권한이 있는가
         2. Client 복잡성 간소화
            1. OAuth1.0에서는 인가를 받을 때마다 request param에 매번 값을 채워줘야 하는 등의 번거로움이 있었다.
            2. ``Bearer Token``과 ``TLS``로 해결
               1. Bearer Token
                  1. 해당 토큰을 가지고 있는 것만으로도 인가해줌
                  2. https강제
         3. 토큰 탈취 문제 개선
            1. 기존에 유효기간이 길었음
            2. ``Refresh Token`` 적용
         4. Grant 
            1. 웹브라우저만 아니라 다양한 사용환경에서도 사용 가능
            2. Authorization Code
               1. Server to Server로 인증 후 토큰 발급
            3. Implicit
               1. 웹브라우저의 자바스크립트 기반 클라이언트에서 직접 로그인 후 토큰 발급
            4. Resource owner password credentials
               1. 직접적인 유저정보가 가기 때문에 스마트폰과 같은 기기에서 사용
            5. Client credentials
               1. Resource owner와 OAuth client과 동일할 때 직접 api를 호출해서 토큰 발급
         5. 웹 환경
            1. javascript와 스마트 기기와 더불어 사용
      3. OAuth2.1
         1. 더 보안적으로 민감한 사용처들의 프로토콜 채택
         2. OAuth2.0에서 많은 보안책이 필요했고, 이에 따라 많은 볼트원 방식의 RFC를 숙지하여야 했음. 이를 종합해 스펙화시킨게 OAuth2.1
         3. BCP
         4. Grant
            1. Implicit와 Resource owner password credentials는 spec-out하였다. 보안상 위험하다 판단되어
            2. Device Authoriation Grant
               1. 스마트폰, 애플워치와 같이 기기를 바꿔 인증할 수 있음
            3. PKCE(Proof code Key for Code Exchange)
               1. Authorization code grant에 추가된 PKCE
                  1. 기존에는 인증코드를 탈취할 수 있는 취약점이 있었으나 이를 보안
                  2. 시작 값에 Hash한 값을 보내고 토큰을 받을 때 Hash한 값의 원문을 보내서 시작 client와 끝 client가 같은 것을 확인한다.
                  3. 탈취자는 hash를 역연산할 수 없기 때문에 탈취를 해도 원문을 모른다.
            4. BCP(Best Current Practice)
               1. 기존의 Refresh Token 또한 life cycle을 1회성으로 변경
               2. Refresh Token을 1회 사용하면 없어진다.
         5. 웹 환경
            1. 다양한 IOT환경의 웹환경
      4. Open ID Connet
         1.  개요
             1.  Oauth2.0기반 인증 계층
             2.  Oauth2.0 + OpenID(JWT기반 Token인증) => OpenIDConnect
             3.  Token엔 여러가지 정보가 포함되어 있다.
         2.  웹 환경
             1.  더욱 다양한 서비스 환경 속에서 간단하게 인증을 받을 수 있다.
      5.  GNAP(Grant Negotiation and Authorization Protocol)
          1.  인증/인가의 미래
          2.  Oauth2.0의 ``grant``가 ``interaction``으로 진화
          3.  Interaction
              1.  요청할 때 ``시작``과 ``끝``의 상호작용 방식을 json에 미리 기재해서 맞춘다.
          4.  End user/Resource owner의 분리
              1.  OAuth의 Resouce owner의 Resource접근인가와 Client와 상호작용하는 자연인을 분리
              2.  GNAP Resource owner/GNAP End user
          5.  API의 접근 범위, 정밀 제어 및 여러 토큰 요청 제어 가능
          6.  기존의 Bearer Token + mTLS/DPOP에서 JWK, 인증서 기반 Client 보안 내장으로 변경
          7.  OpenID신기술 연동성
              1.  블록체인의 탈중앙화된 유저의 did적용 등
   4.  요약
       1.  Oauth1.0
           1.  인가 프로토콜 개념제시, 브라우저 환경 동작
       2.  OAuth2.0
           1.  Client간소화, Refresh토큰 등장, 여러가지 Grant 추가
       3.  OAuth2.1`
           1.  보안성 개선, IoT기기지원 및 모범사례의 스펙화
       4.  OpenIDConnect
           1.  인증 계층 추가, API호출 없는 사용자 정보 확인
       5.  GNAP
           1.  Interaction확장, 현/미래 기술들과 호환