# Effective Java - [7장. 람다와 스트림]

### item 42. 익명 클래스보다는 람다를 사용하라
- 코드 자체로 동작이 명확히 설명 되지 않거나 코드 줄 수가 많아지면 람다를 쓰지말자.(MAX 3줄)
- 람다는 함수형 인터페이스에서만 사용된다.
- 추상클래스의 인스턴스를 만들때 람다를 쓸 수 없어 익명 클래스를 써야한다.  
  Q.왜 쓸 수 없나요?
- 람다의 this는 밖의 인스턴스를 가리킴  
- 익명클래스의 this는 자기자신을 가리킴  
Q. 익명 클래스?
Q. 람다?

### item 43. 람다보다는 메서드 참조를 사용하라
Q. 메서드 참조?
  ```
  // 람다
  map.merge(key, 1, (count,incr) -> count + incr);
  // 메서드 참조
  map.merge(key, 1, Integer::sum);
  ```

### item 44. 표준 함수형 인터페이스를 사용하라
- 입력값과 반환값에 함수형 인터페이스 타입을 활용하라
- 기본 함수형 인터페이스  

  |인터페이스|함수 시그니처|예시|
  |------|---|---|
  | UnaryOperator<T> | T apply(T t) | String::toLowerCase |
  | BinaryOperator<T> | T apply(T t1, T t2) | BigInteger::add |
  | Predicate<T> | boolean test(T t) | Collection::isEmpty |
  | Function<T> | R apply(T t) | Arrays::asList |
  | Supplier<T> | T get() | Instant::now |
  | Consumer<T> | void accept(T t) | System.out.println |

Q. 표준 함수형 인터페이스? java.util.function

### item 45. 스트림은 주의해서 사용하라
- 스트림을 과용하면 읽거나 유지보수하기 어려워짐.
Q. 스트림?
### item 46. 스트림에서는 부작용 없는 함수를 사용하라
- forEach는 스트림이 수행한 계산 결과를 보고할때만 이용
Q. 종단 연산? 

### item 47. 반환 타입으로는 스트림보다 컬렉션이 낫다
Q. 컬렉션?
### item 48. 스트림 병렬화는 주의해서 적용하라 

