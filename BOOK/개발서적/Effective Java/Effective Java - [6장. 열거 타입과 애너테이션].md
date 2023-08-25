# Effective Java - [6장. 열거 타입과 애너테이션]

### item 34. int 상수 대신 열거 타입을 사용하라
- 정수 열거 패턴
```
public static final int APPLE_FUJI = 0;
public static final int APPLE_PIPPIN = 1;
public static final int APPLE_GRANNY_SMITH = 2;

public static final int ORANGE_NAVEL = 0;
```

- 열거 타입
```
public enum Apple {FUJI, PIPPIN, GRANNY_SMITH}
public enum Orange {NAVEL, ...}
```

### item 35. ordinal 메서드 대신 인스턴스 필드를 사용하라

### item 36. 비트 필드 대신 EnumSet을 사용하라

### item 37. ordinal 인덱싱 대신 EnumMap을 사용하라

### item 38. 확장할 수 있는 열거타입이 필요하면 인터페이스를 사용하라

### item 39. 명명 패턴보다 애너테이션을 사용하라*

### item 40. @Override 애너테이션을 일관되게 사용하라

### item 41. int 상수 대신 열거 타입을 사용하라
