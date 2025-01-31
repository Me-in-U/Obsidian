---
tags: metaspace, stack, heap, java
---
```java
public class SmartPhone {
    static double osVer = 1.0;
    String number;

    void call(String to) { // 파라미터 변수
        String msg = "띠"; // 로컬 변수
        for (int i = 0; i < 3; i++) { // 로컬 변수
            System.out.println(msg);
        }
    }
}

public class SmartPhoneTest {
    public static void main(String[] args) {
        SmartPhone sphone1 = new SmartPhone();
        sphone1.number = "010";
        System.out.println("sphone1.osVer: " + sphone1.osVer + ", " + sphone1.number);
        sphone1.call("011");

        SmartPhone sphone2 = new SmartPhone();
        sphone2.number = "010-111-1111";
        System.out.println("sphone2.osVer: " + sphone2.osVer + ", " + sphone2.number);

        SmartPhone.osVer = 2.0;
        System.out.println("sphone1.osVer: " + sphone1.osVer + ", " + sphone1.number);
        System.out.println("sphone2.osVer: " + sphone2.osVer + ", " + sphone2.number);
    }
}

```

1. 프로그램 시작
	1. Metaspace
	   - `SmartPhone` 클래스 로드: 클래스 정보와 static변수(`osVer`)
	      - osVer의 초기값: 1.0
	2. Heap: 아직 아무 객체도 생성되지 않음.
	3. Stack: 아직 실행 중인 메서드 없음.
2. `main` 메서드 호출
	1. Stack
		- `main` 메서드가 호출되어 스택 프레임이 생성됨.
		- 지역 변수 `sphone1`, `sphone2`가 선언되었지만 초기화되지 않음.
3. `SmartPhone sphone1 = new SmartPhone();`
	1. Heap
		- 첫 번째 `SmartPhone` 객체 생성.
		- `number` 필드는 기본값 `null`로 초기화 됨.
	2. Stack
		- `sphone1` 지역 변수에 생성된 `SmartPhone` 객체의 참조값 저장.
4. `sphone1.number = "010";`
	1. Heap
		- `sphone1`가 참조하는 객체의 `number` 필드가 `"010"`으로 업데이트됨.
5. `sphone1.call("011");`
	1. Stack
		- `call` 메서드 호출 시 새로운 스택 프레임 생성.
		- 매개변수 `to`에 `"011"` 저장.
		- 지역변수 `i`가 for 루프 동안 `0~9` 값을 가짐
6. `SmartPhone sphone2 = new SmartPhone();`
	1. Heap
		- 두 번째 `SmartPhone` 객체 생성.
		- `number` 필드는 기본값 `null`로 초기화됨.
	2. Stack
		- `sphone` 지역 변수에 두 번째 `SmartPhone` 객체의 참조값 저장.
7. `sphone2.number = "010-111-1111";`
	1. Heap
		- `sphone2`가 참조하는 객체의 `number` 필드가 `"010-111-1111"`로 업데이됨.
8. `SmartPhone.osVer = 2.0;`
	1. Metaspave
		- `osVer`의 값이 `1.0`에서 `2.0`으로 변경

---
### 최종 상태

- **Metaspace**: 클래스 정보와 static 변수 `osVer=2.0`.
- **Heap**:
    - 첫 번째 객체: `number="010"`.
    - 두 번째 객체: `number="010-111-1111"`.
- **Stack**:
    - `main` 메서드의 지역 변수 `sphone1`, `sphone2`.
    - `call` 메서드 호출 종료 후 스택 프레임 해제.