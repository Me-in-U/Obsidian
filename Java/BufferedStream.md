---
tags: java, input, BufferedStream, BufferedReader, BufferedWriter,
  InputStreamReader, OutputStreamWriter, System
---
```java
import java.io.IOException;

import java.io.BufferedReader;
import java.io.InputStreamReader;

import java.io.BufferedWriter;
import java.io.OutputStreamWriter;

class Main {
  public static void main(String[] args) throws IOException{
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    
    // 사용자 입력 받기
    String[] str = br.readLine().split(" ");
    int age = Integer.parseInt(str[0]);
    String name = str[1];
    
    // 정수 배열 초기화 및 값 할당
    int N = str.length;  // N의 값을 초기화해야 합니다.
    int[] nums = new int[N];
    for(int i = 0; i<N; i++){
      nums[i] = Integer.parseInt(br.readLine());
    }
    
    // 결과 출력
    bw.write(String.valueOf(nums[0]));  // 값을 지정해야 합니다.
    bw.newLine();
    bw.flush();
  }
}
java```


### BufferedReader와 BufferedWriter 클래스 메서드 설명

#### BufferedReader
- **BufferedReader(Reader rd)**: `rd`에 연결된 문자 입력 버퍼 스트림을 생성합니다.
- **int read()**: 스트림에서 한 문자를 읽어 int 형으로 반환합니다.
- **int read(char[] buf)**: 문자 배열 `buf`의 크기만큼 문자를 읽어들입니다. 읽은 문자 수를 반환합니다.
- **int read(char[] buf, int offset, int length)**: `buf`의 `offset` 위치부터 `length` 길이만큼 문자를 스트림에서 읽어들입니다.
- **String readLine()**: 스트림에서 한 줄을 읽어 문자열로 반환합니다.
- **void mark(int readAheadLimit)**: 현재 위치를 마킹하며, 차후 `reset()`을 사용하여 마킹 위치부터 시작할 수 있습니다.
- **void reset()**: 마킹이 있으면 그 위치에서부터 다시 시작하며, 그렇지 않으면 처음부터 다시 시작합니다.
- **long skip(long n)**: `n` 개의 문자를 건너뜁니다.
- **void close()**: 스트림을 닫습니다.

#### BufferedWriter
- **BufferedWriter(Writer wt)**: `wt`에 연결된 문자 출력 버퍼 스트림을 생성합니다.
- **void write(int c)**: int 형으로 문자 데이터를 출력 스트림으로 출력합니다.
- **void write(String s, int offset, int length)**: 문자열 `s`를 `offset` 위치부터 `length` 길이만큼 출력 스트림으로 출력합니다.
- **void write(char[] buf, int offset, int length)**: 문자 배열 `buf`의 `offset` 위치부터 `length` 길이만큼 출력 스트림으로 출력합니다.
- **void newLine()**: 줄 바꿈 문자열을 출력합니다.
- **void flush()**: 남아있는 데이터를 모두 출력시킵니다.
