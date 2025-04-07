**주의 사항**
- 모든 날짜 클래스는 **불변**
- 변경이 발생하는 경우 새로운 객체를 생성해서 반환 필수

## LocalDate
- 날짜만 표현할 때 사용

```java
import java.time.LocalDate;

public class LocalDateMain {
    public static void main(String[] args) {
        LocalDate nowDate = LocalDate.now();
        LocalDate ofDate = LocalDate.of(2025,11,11);
        System.out.println("오늘 날짜 = " + nowDate);
        System.out.println("지정 날짜 = " + ofDate);

        //계산(불변)
        ofDate = ofDate.plusDays(10);
        System.out.println("지정 날짜 +10 = " + ofDate);
    }
}
```
- `now()`: 현재 시간을 기준으로 생성
- `of(...)`: 특정 날짜를 기준으로 생성(년, 월, 일 기입 가능)
- `plusDays()`: 특정 일을 더함(다양한 `plusXxx()` 메서드가 존재)

## LocalTime
- 시간만을 표현할 때 사용
  
```java
import java.time.LocalTime;

public class LocalTimeMain {
    public static void main(String[] args) {
        LocalTime nowTime = LocalTime.now();
        LocalTime ofTime = LocalTime.of(9, 10, 30);

        System.out.println("현재 시간 = " + nowTime);
        System.out.println("지정 시간 = " + ofTime);

        //계산(불변)
        LocalTime ofTimePlus = ofTime.plusSeconds(30);
        System.out.println("지정 시간 + 30s = " + ofTimePlus);
    }
}
```
- `of(...)`: 시, 분, 초, 나노초 입력 가능


## LocalDateTime
- LocalDate와 LocalTime을 합한 개념
```java
public class LocalDateTime {
  private final LocalDate date;
  private final LocalTime time;
  ...
}
```

```java
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.LocalDateTime;

public class LocalDateTimeMain {
    public static void main(String[] args) {
        LocalDateTime nowDt = LocalDateTime.now();
        LocalDateTime ofDt = LocalDateTime.of(2016,8,16,8,10,1);
        System.out.println("현재 날짜시간 = " + nowDt);
        System.out.println("지정 날짜시간 = " + ofDt);

        //날짜와 시간 분리
        LocalDate localDate = ofDt.toLocalDate();
        LocalTime localtime = ofDt.toLocalTime();
        System.out.println("localtime = " + localtime);
        System.out.println("localDate = " + localDate);

        //날짜와 시간 합체
        LocalDateTime localDateTime = LocalDateTime.of(localDate, localtime);
        System.out.println("localDateTime = " + localDateTime);

        //계산(불변)
        LocalDateTime ofDtPlus = ofDt.plusDays(1000);
        System.out.println("지정 날짜시간 + 1000d = " + ofDtPlus);
        LocalDateTime ofDtPlus1Year = ofDt.plusYears(1);
        System.out.println("지정 날짜시간 + 1y = " + ofDtPlus1Year);

        //비교
        System.out.println("현재 날짜시간이 지정 날짜시간보다 이전인가? " + nowDt.isBefore(ofDt));
        System.out.println("현재 날짜시간이 지정 날짜시간보다 이후인가? " + nowDt.isAfter(ofDt));
        System.out.println("현재 날짜와 지정 날짜시간이 같은가? " + nowDt.isEqual(ofDt));
    }
}
```
- `LocalDate`와 `LocalTime`을 `toXxx()` 메서드로 분리 가능

**isEqual() vs equals()**
- **`isEquals()`**: 객체, 타임존이 달라도 시간적으로 같은면 `true` 반환
- **`equals()`**: 객체의 타입, 타임존 등등 내부 데이터의 모든 구성요소가 같아야 `true` 반환

