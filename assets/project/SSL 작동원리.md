### SSL 작동원리

대칭키와 비대칭키(공개키)에 대한 개념을 알고 있어야 함.

![sslHandShake](./SSLhandshake.jpg)

Nonce는 SSL 연결을 시도할 때마다 바뀌는 값임. 통신 내용을 통째로 복사해서 재요청하는 Reply Attack을 막기 위해 설정한다.