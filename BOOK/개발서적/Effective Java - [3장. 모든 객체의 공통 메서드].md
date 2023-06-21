# Effective Java - [3장. 모든 객체의 공통 메서드]

### item 10. `equals`는 일반규약을 지켜 재정의 하라.
- 꼭 필요한 경우가 아니라면, equals를 재정의하지 말아라. 많은 경우, Object의 equals가 비교를 정확히 수행한다.
- 만약 equals를 정의해야한다면, 다섯 가지 규약을 지켜가며 비교해야 한다.

### item 11. `equals`를 재정의하려거든, `hashCode`도 재정의하라.
- 논리적으로 같은 객체는 같은 해시코드를 반환해야한다.

### item 12. `toString`을 항상 재정의하라.
- toString을 잘 구현한 클래스는 사용하기 훨씬 즐겁고, 디버깅하기 쉽다.  
  map 객체를 출력했을때 `{Jenny=PhoneNumber@adbbd}` 보다는 `{Jenny=707-867-5309}`가 더 반갑다.  
 - 명확하고, 유용한 정보를 읽기 좋은 형태로 반환하자.

### item 13. `clone` 재정의는 주의해서 진행하라.
- 실무에서 Cloneable을 구현한 클래스는 clone메서드를 public으로 제공하며, 사용자는 복제가 제대로 이뤄지리라 기대한다.
- 배열 복사시, 원본과 같은 연결리스트를 참조하여 원본과 복제본 모두 예기치 않게 동작할 가능성이 생김
- 복사 생성자
  ```
  public Yum(Yum yum) { ... };
  ```
- 복사 팩터리
  ```
  public static Yum newInstance(Yum yum) { ... };  
  ```

### item 14. Comparable을 구현할지 고려하라.
- Comparable은 인터페이스, Comparable 내의 compareTo 메서드
- compareTo는 동치성 비교 + 순서 비교 가능
- compareTo 메서드로 수행한 동치성 테스트의 결과가 equals와 같아야 한다. `일관성`
- 정적 compare 메서드
  ```
  static Comparator<Object> hashCodeOrder = new Comparator<>() {
    public int compare(Object o1, Object o2) {
      return Integer.compare(o1.hashcode(), o2.hashCode());
    }
  }
  ```
- 비교자 생성 메서드
  ```
  static Comparator<Object> hashCodeOrder = Comparator.comparingInt(o -> o.hashCode());
  ```
Q. hashCode로 비교하면 어떤 정렬이 이루어지는거지?
