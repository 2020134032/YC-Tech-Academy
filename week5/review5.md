# OAuth

https://charming-kyu.tistory.com/36

Resource Owner

- 리소스 소유자입니다. 본인의 정보에 접근할 수 있는 자격을 승인하는 주체입니다. 예시로 구글 로그인을 할 사용자를 말합니다. Resource Owner는 클라이언트를 인증(Authorize)하는 역할을 수행하고, 인증이 완료되면 동의를 통해 권한 획득 자격(Authorization Grant)을 클라이언트에게 부여합니다.

Client

- Resource Owner의 리소스를 사용하고자 접근 요청을 하는 어플리케이션 입니다.

Resource Server

- Resource Owner의 정보가 저장되어 있는 서버입니다.

Authorization Server

- 권한 서버입니다. 인증/인가를 수행하는 서버로 클라이언트의 접근 자격을 확인하고 Access Token을 발급하여 권한을 부여하는 역할을 수행합니다.

## 1. Authorization Code Grant │ 권한 부여 승인 코드 방식

권한 부여 승인을 위해 자체 생성한 Authorization Code를 전달하는 방식으로 많이 쓰이고 기본이 되는 방식입니다.    
간편 로그인 기능에서 사용되는 방식으로 클라이언트가 사용자를 대신하여 특정 자원에 접근을 요청할 때 사용되는 방식입니다.   
보통 타사의 클라이언트에게 보호된 자원을 제공하기 위한 인증에 사용됩니다. Refresh Token의 사용이 가능한 방식입니다.   

![image](https://github.com/2020134032/YC-Tech-Academy/assets/128214994/a46c80b5-7ba2-4373-a63f-f4343bc74037)   
 
권한 부여 승인 요청 시 response_type을 code로 지정하여 요청합니다.   
이후 클라이언트는 권한 서버에서 제공하는 로그인 페이지를 브라우저를 띄워 출력합니다.   
이 페이지를 통해 사용자가 로그인을 하면 권한 서버는 권한 부여 승인 코드 요청 시 전달받은 redirect_url로 Authorization Code를 전달합니다.    
Authorization Code는 권한 서버에서 제공하는 API를 통해 Access Token으로 교환됩니다.   

## 2. Implicit Grant │ 암묵적 승인 방식
자격증명을 안전하게 저장하기 힘든 클라이언트(ex: JavaScript등의 스크립트 언어를 사용한 브라우저)에게 최적화된 방식입니다.

![image](https://github.com/2020134032/YC-Tech-Academy/assets/128214994/fed4b40b-dd00-4d45-8a36-5c837d9977bf)


암시적 승인 방식에서는 권한 부여 승인 코드 없이 바로 Access Token이 발급 됩니다. Access Token이 바로 전달되므로 누출의 위험을 방지하기 위해 만료기간을 짧게 설정하여 전달됩니다.

Refresh Token 사용이 불가능한 방식이며, 이 방식에서 권한 서버는 client_secret를 사용해 클라이언트를 인증하지 않습니다. Access Token을 획득하기 위한 절차가 간소화되기에 응답성과 효율성은 높아지지만 Access Token이 URL로 전달된다는 단점이 있습니다.

Authorization Grant: Implicit

권한 부여 승인 요청 시 response_type을 token으로 설정하여 요청합니다. 이후 클라이언트는 권한 서버에서 제공하는 로그인 페이지를 브라우저를 띄워 출력하게 되며 로그인이 완료되면 권한 서버는 Authorization Code가 아닌 Access Token를 redirect_url로 바로 전달합니다.

 

## 3. Resource Owner Password Credentials Grant │ 자원 소유자 자격증명 승인 방식

간단하게 username, password로 Access Token을 받는 방식입니다.

![image](https://github.com/2020134032/YC-Tech-Academy/assets/128214994/88fb68c1-ff7a-4338-8d74-200457784be5)


클라이언트가 타사의 외부 프로그램일 경우에는 이 방식을 적용하면 안됩니다. 자신의 서비스에서 제공하는 어플리케이션일 경우에만 사용되는 인증 방식입니다. Refresh Token의 사용도 가능합니다.

Authorization Grant: Password

위와 같이 흐름은 간단합니다. 제공하는 API를 통해 username, password을 전달하여 Access Token을 받는 것입니다. 중요한 점은 이 방식은 권한 서버, 리소스 서버, 클라이언트가 모두 같은 시스템에 속해 있을 때 사용되어야 하는 방식이라는 점입니다.

 

## 4. Client Credentials Grant │ 클라이언트 자격증명 승인 방식
클라이언트의 자격증명만으로 Access Token을 획득하는 방식입니다.

![image](https://github.com/2020134032/YC-Tech-Academy/assets/128214994/4bdf0f15-4bf8-4fbf-baad-89ec5b4844e6)

OAuth2의 권한 부여 방식 중 가장 간단한 방식으로 클라이언트 자신이 관리하는 리소스 혹은 권한 서버에 해당 클라이언트를 위한 제한된 리소스 접근 권한이 설정되어 있는 경우 사용됩니다. 이 방식은 자격증명을 안전하게 보관할 수 있는 클라이언트에서만 사용되어야 하며, Refresh Token은 사용할 수 없습니다.

Authorization Grant: Client Credentials
