
### 메일 프로토콜 이해하기

SMTP

POP3

IMAP

다양한 협업툴과 실시간 통신 기술의 발달에도 불구하고 이메일은 여전히 업무의 대부분을 차지하는 커뮤니케이션 수단이다. 왜냐하면,

다른 시각(시차), 다른 장소(원격) 에서의 통신을 가능하게 해주기 때문이다.

### 관련 이메일 프로그램

아웃룩(Outlook)

윈도우즈메일(Windows Mail)

### 이메일 시스템 구조

![이미지](https://github.com/JaeHyukSim/projects/blob/jaehyuk/hands/jaehyuk/hands/data/img/email-system-structure.PNG)

1.  메일 서버
    -   A,B,C로 표시된 메일서버는 각각의 메일 주소에 대응하는 사서함 ( Mail Box )가 존재한다
        
        → 이러한 사서함을 바탕으로 한 메일 서버간의 통신 덕분에 원격지에서 시차를 두고 메일을 주고받을 수 있는 것이다.
        
    -   발신자(Sunny)가 이메일을 보내면, Sunny의 이메일 서버(A)에 도착한다.
        
    -   발신자의 이메일 서버(A)에서 보내고자 하는 상대방 Sally의 이메일 서버(B)로 연결된 인터넷을 통해 메일을 전달한다.
        
    -   서버 B에 도착한 메일은 수신자 Sally에게 전달된다.
        
2.  메일 클라이언트
    -   메일 서버의 사서함에 저장된 이메일을 가져와 보여주거나, 서버로 전달하는 역할을 수행
    -   보낼때 : 서버에게 send
    -   받을 때 서버의 사서함에서 가져온다

### 프로토콜이란

통신 규약

### SMTP(Simple Mail Transfer Protocol) - port 25

1.  클라이언트가 작성한 메일을 서버로 전송할 때
2.  인터넷을 통해 서버 간 메일을 전송할 때

### POP3(Post Office Protocol 3) - port 110

-   이메일을 수신할 때 사용하는 프로토콜
-   이메일 서버에 도착한 메일을 클라이언트로 가져올 때 사용.
-   3의 의미는 버전
-   서버의 사서함으로부터 클라이언트 PC로 메일을 직접 다운로드 하는 형식
-   다운로드 할 때 헤더 부분(발신자의 정보, 수신 서버의 호스트 주소, 해당 메일의 고유한 식별자, 메일이 수신된 날짜 등의 정보가 담김), 본문(첨부파일, 메일내용)을 모두 다운로드
-   다운로드가 되면, 메일 서버의 사서함에서 해당 메일 삭제.(삭제되지 않도록 설정 가능)
-   따라서 POP3방식을 사용하면, 로컬 PC에만 해당 메일이 남아있어서 다른 PC나 모바일 등의 기기로 동일한 메일을 확인할 수 없다.

### IMAP(Internet Message Access Protocol) - port 143

-   이메일을 수신할 때 사용되는 또 다른 프로토콜
-   메일 서버와 클라이언트를 동기화
-   받은 편지함, 보낸 편지함 등을 확인할 수 있다.
-   POP3보다 빠르다 - 수신자가 해당 메일을 클릭해야만 메일 내용과 첨부파일 등의 본문을 다운로드하기 때문
-   오프라인 상태에서는 메일을 열람할 수 없다.
-   메일 서버의 주기적인 용량 관리가 필요

### 결론

용량이 큰 메일을 자주 주고받아 주기적인 용량 관리가 필요하고, 오프라인 상태에서도 메일 확인이 필요한 경우라면 POP3가 적합

다양한 단말기에서 메일 확인이 필요하고, 불필요한 메일 다운로드 없이 빠르게 필요한 메일만 확인하고 싶으면 IMAP이 적합하다.

### 메일 전송의 원리

1.  mail cloent에서 mail을 작성한 후 SMTP을 사용해 mail deamon으로 메시지를 전송.
2.  mail deamon은 종단간 client를 분석하고, 가장 가까운 mail server(송신자측)로 메시지와 정보를 보낸다
    -   mail deamon이란, 일종의 프로세스로 송신자의 메일과 정보를 메일 서버가 해석 가능하도록 재가공. 반대의 경우 또한 같은 방법으로 수신자의 정확한 메시지 수신과 릴레이를 지원한다.
3.  mail server는 수신자의 전자우편 주소를 분석해서 최단 경로를 찾아 mail server에 편지를 전달한다
4.  최종 수신자측의 mail server에 도착하기까지 연속적으로 전달하는 중계작업이 계속된다.
5.  서로 근접한 Mail Server들 간에 전자우편을 계속해서 중개해 나가는 방법을 통해 메일을 저장 후 전송 ( Store and forward)하는 서비스를 한다.
6.  송수신자는 정확히 메일 교환에 성공한다.

### 전자 우편의 주소 체계와 전송

[zenome@email.com](mailto:zenome@email.com)

-   @ 구분자로 앞 : ID, 뒤는 소속 서버의 주소.
-   메일 헤더 + 메일 본체로 구성
-   전자우편은 7비트 아스키 문자 전송이 표준 (한글은 깨진다)
-   이진 파일의 경우 MIME 방식을 이용해 전자우편에 첨부하여 발송

### 암호화

SHA-256 + Salt 사용.

### SHA

Secure Hash Algorithm - 안전한 해시 알고리즘

NSA(미국 국가안보국)이 1993년에 처음으로 설계 - 미국 국가 표준

최초의 함수는 SHA-0

SHA-1

SHA-2 : SHA-224, SHA-256, SHA-384, SHA-512

SHA-1은 가장 많이 쓰인다 - TLS, SSL, PGP, SSH, IPSec 등 많은 보안 프로토콜과 프로그램에서 사용된다.

하지만 더 중요한 기술에는 SHA-256이나 그 이상의 알고리즘을 사용할 것을 권장.

왜냐하면 SHA-0, SHA-1에 대한 공격은 이미 발견되었기 떄문. (SHA-256도 SHA-1과 비슷한 방법을 사용하기 때문에 공격이 발견될 가능성이 있다)

SHA-0, SHA-1 : 최대 2^64비트의 메시지로부터 160비트의 해시값을 만들어 낸다. (충돌 발견됨)

SHA-256 : 256비트의 해시값을 만들어 낸다.

### 암호화 강화시키기

Salt : 문자열 추가

키 스트레칭 : 해시 함수를 여러번 사용

→ 브루트포스 공격을 최대한 무력화 시킬 수 있다
