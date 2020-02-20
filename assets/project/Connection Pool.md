## Connection Pool

Connection Pool이란 동시에 서버에 접속할 수 있는 Connection을 모아 놓은 것이다. 유저가 서버에 접속할 때마다 새롭게 Connection 객체를 만드는 것이 아니라 미리 Connection 개체를 만들어 놓고 Connection pool에 저장해 놓은 뒤 서버에 접속하려는 유저에게 하나씩 꺼내어 주는 방식이다. Connection 객체를 받은 유저는 Connection을 다 사용하고 나면 Connection Pool에 다시 반납한다.

![connectionpool](ConnectionPool.jpg)

이렇게 하면 좋은 점은 connection 객체를 새로 생성하는 비용을 절약할 수 있고  사용가능한 Connection이 없을 경우에는 에러를 내는 대신에 유저를 대기상태로 둘 수 있다. 원한다면 유동적으로 새로운 Connection 객체를 생성하는 것도 가능하다.



### 우리 서버가 자꾸 죽었던 이유

- Connection을 가져가 놓고 반납(Release)을 안해서
- Connection pool이 작아서(10개가 디폴트로 되어있음)
- 코드가 이상해서(분명 어딘가에 Connection을 너무 일찍 가져오거나 너무 늦게 반납하는 코드가 있을 거임 혹은 중간에 에러를 던지지 못하고 멈추는 코드가 있다.)



### 커넥션 몇개로 해야됨?

커넥션을 많이 하면 메모리 소비가 많아짐(미리 객체를 만드는 것이므로) 너무 적으면 대기시간때매 서버가 기다리게됨. 적절하게(제일 어려움) 정하는 게 중요함. TypeORM에서는 아래 처럼 설정할 수 있다.

```json
// ormconifg.json
{
   ...
   "extra": {"connectionLimit": 10, ...}
}
```



### 참고

- https://brownbears.tistory.com/289