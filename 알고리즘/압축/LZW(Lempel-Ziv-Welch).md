---
tags: algorithm, image, compress, LZW
---
### 작동 방법
1. 초기 사전 생성: 알파벳이나 기호 등으로 이루어진 초기 사전을 만듭니다.
2. 데이터 스캔: 입력 데이터를 스캔하면서 새로운 문자열을 찾습니다.
3. 사전 업데이트: 새로운 문자열을 사전에 추가하고, 고유한 인덱스를 부여합니다.
4. 출력: 기존 문자열이 사전에 있을 경우, 해당 인덱스를 출력합니다.
5. 반복: 입력 데이터가 끝날 때까지 2-4단계를 반복합니다.
6. 압축 완료: 모든 입력 데이터를 처리하고 압축을 완료합니다.

### 예제 
- 입력: "ABABA"
1. 초기 사전 생성:
	- 사전: {'A': 65, 'B': 66}
	- 다음 인덱스: 67
2. 첫 번째 문자 'A':
	- 사전에 있음 (인덱스: 65)
	- w = 'A'
3. 두 번째 문자 'B':
	- 'AB'는 사전에 없음
	- 출력: 65 (w = 'A'의 인덱스)
	- 사전 업데이트: {'AB': 67}
	- w = 'B'
4. 세 번째 문자 'A':
	- 'BA'는 사전에 없음
	- 출력: 66 (w = 'B'의 인덱스)
	- 사전 업데이트: {'BA': 68}
	- w = 'A'
5. 네 번째 문자 'B':
	- 'AB'는 사전에 있음 (인덱스: 67)
	- w = 'AB'
6. 다섯 번째 문자 'A':
	- 'ABA'는 사전에 없음
	- 출력: 67 (w = 'AB'의 인덱스)
	- 사전 업데이트: {'ABA': 69}
	- w = 'A'
7. 끝:
	- 출력: 65 (w = 'A'의 인덱스)

최종 출력: [65, 66, 67, 65]

``` python
def LZW_compress(input_str):
    dictionary = {chr(i): i for i in range(256)}  # 초기 사전 생성
    next_index = 256
    output = []
    w = ""
    
    for c in input_str:  # 데이터 스캔
        wc = w + c
        if wc in dictionary:  # 사전에 있으면
            w = wc
        else:
            output.append(dictionary[w])  # 출력
            dictionary[wc] = next_index  # 사전 업데이트
            next_index += 1
            w = c
    
    if w:
        output.append(dictionary[w])
    
    return output  # 압축 완료

# 사용 예
input_str = "ABABABA"
compressed = LZW_compress(input_str)
print("Compressed:", compressed)
```