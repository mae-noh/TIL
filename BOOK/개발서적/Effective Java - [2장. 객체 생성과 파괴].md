# Effective Java - [2장. 객체 생성과 파괴]

### item 1. `생성자` 대신 `정적 팩터리 메서드`(static factory method)를 고려하라
- 클래스의 인스턴스를 얻는 전통적인 수단은 `public`
- 정적 팩터리 메서드가 생성자보다 좋은 장점 5가지
  1. 이름을 가질 수 있다.
  2. 호출될 때마다 인스턴스를 새로 생성하지 않아도 된다.
  3. `다형성` 메소드의 반환 타입으로 슈퍼클래스를 선언하고, 실제로는 서브클래스의 객체를 반환할 수 있다.*
  4. 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.*
  5. 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.*
- 단점
  1. 상속을 하려면 `public`이나 `protected` 생성자가 필요. 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.
  2. 정적 팩터리 메서드는 프로그래머가 찾기 어렵다.*

### item 2. `생성자`에 매개변수가 많다면 `빌더`를 고려하라
- 점층적 생성자 패턴 < 자바빈즈 패턴 < 빌더 패턴
- build를 호출하여 객체를 얻음. `불변`, `연쇄호출`

### item 3. `private`생성자나 `열거타입`으로 싱글턴임을 보증하라
- `싱글턴` 인스턴스를 오직 하나만 생성
- 3가지 방법의 싱글턴
  - public static final 필드방식
    ```
    public class Elvis {
      public static final Elvis INSTANCE = new Elvis();
      private Elvis() { ... }
      
      public void leaveTheBuilding() { ... }
    }
    ```
  - 정적 팩터리 메서드
    ```
    public class Elvis {
      private static final Elvis INSTANCE = new Elvis();
      private Elvis() { ... }
      public static Elvis get Instancse() { return INSTANCE; }
      
      public void leaveTheBuilding() { ... }
    }
    ```
  - 열거 타입 방식
    ```
    public enum Elvis {
      INSTANCE;
      
      public void leaveTheBuilding() { ... }
    }
    ```
### item 4. 인스턴스화를 막으려거든 `private` 생성자를 사용하라
- 인스턴스를 만들 수 없는 유틸리티 클래스
  ```
  public class UtilityClass {
    private UtilityClass() {
      throw new AssertionError();
    }
  }
  ```
Q. 어떤 경우에 인스턴스화를 막는게 필요할까?

### item 5. 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라
- 의존 객체 주입
  ```
  public class SpellChecker {
    private final Lexicon dictionary;

    public SpellChecker(Lexicon dictionary) {
      this.dictionary = Objects.requireNonNull(dictionary);
    }

    public boolean isValid(String word) { ... }
    public List<String> suggestions(String typo) { ... }
  }
  ```

- Supplier<T> 인터페이스**
- 클래스가 내부적으로 `하나 이상`의 자원에 의존한다면, 싱글턴, 정적 유틸리티 클래스는 지양
  
### item 6. 불필요한 객체 생성을 피하라
- 피해야할 코드
  ```
  String s = new String("swim");
  이 문장은 실행될 떄 마다 String 인스턴스를 새로 만든다. 
  ```
  
  ```
  String s = "swim";
  constant pool, 객체 재사용
  ```
- String.matches는 문자열 형태를 확인하는 가장 쉬운 방법이지만, 성능은 좋지 않아 중요한 상황에서 반복하여 사용하기는 적합하지 않다.
  ```
  public class RomanNumerals {
    private static final Pattern ROMAN = Pattern.compile( - );
    // 패턴을 캐싱해두고, 인스턴스를 재사용한다.
  
    static boolean isRomanNumeral(String s) {
      return ROMAN.matcher(s).matches();
    }
  }
  ```
- 오토박싱, 기본타입과 박싱된 기본타입을 섞어쓸때 자동으로 상호변환해주는 기술
- 박싱된 기본 타입보다는 `기본타입`을 사용 권장  
Q. 왜 박싱된 타입이 아닌, 기본타입을 권장하는걸까?

### item 7. 다 쓴 객체 참조를 해제하라.
- 자바는 메모리 관리를 안해도 된다? 아니요!
  객체 참조 하나를 살려두면, 그 객체뿐만 아니라 그 객체가 참조하는 모든객체를 회수할 수 없다.
- `Stack` 클래스는 자기 메모리를 직접 관리
- `캐시` -> WeakHashMap
- `리스너`, `콜백`*

### item 8. finalize와 cleaner 사용을 피하라.
- finalize와 cleaner로는 제때 실행되어야 하는 작업은 절대 할 수 없다.
- `AutoCloseable` 구현*  
Q. AutoCloseable 그게 뭔데?

### item 9. try-finally 보다는 try-with-resources를 사용하라.
```
try (InputStream in = new FileInputStream(src);
     OutStream out = new FileOutputStream(dst)) {
        byte[] buf = new byte[BUFFER_SIZE];
        int n;
        while((n = in.read(buf)) >= 0)
          out.write(buf, 0, n);
     }
```
