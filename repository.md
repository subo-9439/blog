```java
@Transient
영속성 처리에서 제외된다. 엔티티 내에서 제외시키고 싶은 속성에 추가해주면 된다. ->DB에는 반영이 되지 않는다는 말이다.
@Enumerated(value = EnumType.STRING)
ENUM 클래스를 
업데이트 하다가 보면 수정이 될때 ORDINAL은 잠재적으로 버그를 일으 킬 수 있다.

```
```
@Notnull vs @Nullable=false;
둘다 널값이 되면 안된다.
다만
@NotNull 어노테이션을 쓰면, 데이터베이스에 SQL 쿼리를 보내기 전에 예외가 발생한다.
JPA의 Repository 인터페이스가 잘못된 Entity를 저장할 때, ConstraintViolationException을 발생시킨다.

(그 때문에, @Valid나 @Validated 없이도 엔티티를 자연스럽게 검증할 수 있다)

물론 값이 검증에 맞지 않아도 객체를 생성하는 것은 가능했다.

또한, Bean Validation의 트리거가 EntityManager가 Flush된 이후이므로,

원하는 타이밍에 맞지 않아 의도치 않은 오류를 맞을 수도 있다.

그러나 nullable=false 로 @Column 어노테이션에 속성을 붙이면,

null을 넣은 엔티티를 생성하면 생성이 된 뒤 Repository에 전달되고,

이 값이 DB에 넘어간 뒤에 예외가 발생해 위험한 오류를 맞을 수 있다.

이렇게 둘의 장단점을 비교해 보았을 때,

@NotNull을 써서 DB와 서버 모두의 안정성을 챙기는 것이 좋겠다고 생각했다.
https://bottom-to-top.tistory.com/14#:~:text=nullable%20%3D%20false%20%EB%8A%94%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%EC%97%90,%EC%95%88%EC%A0%84%ED%95%98%EA%B2%8C%20%EC%82%AC%EC%9A%A9%ED%95%A0%20%EC%88%98%20%EC%9E%88%EC%9D%84%EA%B2%83%20%EA%B0%99%EB%8B%A4.
```

