# Effective Java - [4장. 클래스와 인터페이스]

### item 15. 클래스와 멤버의 접근 권한을 최소화하라.*
- 모든 클래스와 멤버의 접근성을 가능한 좁혀야 한다.
- 멤버 접근자
  - `private` 멤버를 선언한 클래스에서만 접근 가능
  - `package-private` 멤버가 속한 패키지 안의 모든 클래스에서 접근 가능, 접근제한자를 명시하지 않는 경우 기본 접근 수준
  - `protected` package-private + 멤버 하위 클래스에서 접근 가능
  - `public` 모든 곳에서 접근 가능
- public 클래스는 상수용 public static final 필드 외에는 어떠한 public 필드도 가져서는 안된다.

### item 16. public 클래스에서는 public 필드가 아닌 접근자 메서드를 사용하라??
- 멤버변수를 private로 모두 변경하고, public 접근자(getter)를 추가

### item 17. 변경 가능성을 최소화하라. 불변!
- 클래스 불변으로 만드는 다섯가지 규칙
  - 확장하지 못하도록 클래스를 `final`로 선언
  - 모든 필드를 `final`로 선언
  - 모든 필드를 `private`로 선언
  - 자신 외에 내부 가변 컴포넌트에 접근할 수 없도록

### item 18. `상속`보다는 `컴포지션`을 이용하라.
- 메서드 호출과 달리 상속은 캡슐화를 깨뜨린다.

### item 19. 상속을 고려해 설계하고 문서화하라. 그러지 않았다면 상속을 금지하라.

### item 20. `추상` 클래스보다는 `인터페이스`를 우선하라.

### item 21. `인터페이스`는 구현하는 쪽을 생각해 설계하라.

### item 22. `인터페이스`는 타입을 정하는 용도로만 사용하라.

### item 23. 태그 달린 클래스보다는 클래스 계층구조를 활용하라.

### item 24. 멤버 클래스는 되도록 static으로 만들라.

### item 25. 톱레벨 클래스는 한 파일에 하나만 담으라.
