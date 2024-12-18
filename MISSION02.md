# MISSION: 예시 만들기

본인이 잘 이해했는지 확인하는 가장 정확한 방법은 가르쳐 보는 것!
클린코드 읽으며 뼈맞았던 내용 중 **`3가지 원칙`** 을 고르고, 원칙 따르는 예시 총 3가지를 만들어보세요.

클린코드 읽을 때 분명 참고하라고 적어준 예시인데 자바로 되어있어서 공감이 잘 안됐죠? 이제 본인이 가장 잘하는 언어로(JS, Python 등등) 더러운 코드를 깨끗한 코드로 리팩토링하는 예시를 만들어보세요.

## QUIZ 01

```python
# 본인이 가장 잘하는 언어로(JS, Python 등등) 더러운 코드를 깨끗한 코드로
# 리팩토링하는 예시를 만들어보세요. 현재 파일은 JS 로 되어있지만. 자유롭게 다른 언어로 변경해주세요.

# 원칙 1. 의미있게 구분하라

# Before 😣
import sys
s=input("16진수를 입력 하시오")
result = 0 # 계산 결과 저장
v = 0 # 변환된 숫자 저장
for c in s:
    if (c>='0' and c<='9') :
        v = ord(c) - ord('0')   # 해당되는 숫자 (10진수) 또는 v= int(c)
    elif (c>='A' and c<='F') :
        v = ord(c) - ord('A') + 10  # 해당되는 숫자 (16진수)
    elif (c>='a' and c<='f') :
        v = ord(c) - ord('a') + 10  # 해당되는 숫자 (16진수)
    else:
        print('16진수가 아닙니다.')
        sys.exit(0)
    result = result * 16 + v

print('16진수 {0} 는 10진수 {1} 입니다'.format(s, result))

# 무엇을 고치려고 하는지, 고치려는 문제가 무엇인지 알려주세요.
# 변수가 무엇을 말하는지 모르겠다.
# 덤으로 주석이 불필요하다.

# After 😎
import sys

hexadecimal = input("16진수를 입력 하시오")
result = 0
decimal = 0
for char in hexadecimal:
    if char >= "0" and char <= "9":
        value = ord(char) - ord("0")
    elif char >= "A" and char <= "F":
        value = ord(char) - ord("A") + 10
    elif char >= "a" and char <= "f":
        value = ord(char) - ord("a") + 10
    else:
        print("16진수가 아닙니다.")
        sys.exit(0)
    result = result * 16 + value

print("16진수 {0} 는 10진수 {1} 입니다".format(hexadecimal, result))


# 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.

# 먼저 변수들의 이름을 모두 의미 있는 이름으로 바꿨다.
# 그리고 불필요한 주석들을 모두 지웠다.
```

## QUIZ 02

```python
# 본인이 가장 잘하는 언어로(JS, Python 등등) 더러운 코드를 깨끗한 코드로
# 리팩토링하는 예시를 만들어보세요. 현재 파일은 JS 로 되어있지만. 자유롭게 다른 언어로 변경해주세요.

# 원칙 2. try-except 블록 뽑아내기

# Before 😣
class PerkDetail(APIView):

    def get(self, request, pk):
        try:
            perk = Perk.objects.get(pk=pk)
        except:
            raise NotFound
        serializer = PerkSerializer(perk)
        return Response(serializer.data)

# 무엇을 고치려고 하는지, 고치려는 문제가 무엇인지 알려주세요.

# get 메소드 내에 있는 try-except 블록은 정상 동작과 오류 처리 동작을 뒤섞는다.
# 따라서 이를 별도의 함수로 뽑아낸다.


# After 😎
class PerkDetail(APIView):

    def get_object(self, pk):
        try:
            return Perk.objects.get(pk=pk)
        except:
            raise NotFound

    def get(self, request, pk):
        perk = self.get_object(pk)
        serializer = PerkSerializer(perk)
        return Response(serializer.data)


# 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.

# get 메소드에서 try-except 블록을 뽑아서 get_object 함수에서 이를 따로 수행하게 했다.

```

## QUIZ 03

```python
# 본인이 가장 잘하는 언어로(JS, Python 등등) 더러운 코드를 깨끗한 코드로
# 리팩토링하는 예시를 만들어보세요. 현재 파일은 JS 로 되어있지만. 자유롭게 다른 언어로 변경해주세요.

# 원칙 3. 인수가 2~3개 필요하다면 독자적인 클래스 변수로 선언해보자.

# Before 😣
def calculateEchelonArea(top: float, bottom: float, height: float):
    return (top + bottom) * height / 2

# 무엇을 고치려고 하는지, 고치려는 문제가 무엇인지 알려주세요.

# 위 함수는 사다리꼴의 넓이를 구하는 함수로, 밑변, 윗변, 높이를 함수로 받고 있다.
# 즉, 총 3개의 인수를 받고 있는데, 이를 1개로 줄일 것이다.


# After 😎
class Echelon:
    top: float
    bottom: float
    height: float

def calculateEchelonArea(echelon: Echelon):
    top = echelon.top
    bottom = echelon.bottom
    height = echelon.height
    return (top + bottom) * height / 2


# 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.

# 윗변, 밑변, 높이를 가지는 Echelon 클래스를 새로 만들었다. 그리고 Echelon의 인스턴스를 calculateEchelonArea 함수에서 대신 받게 했다. 이제 인수가 1개로 줄어들었다.
# 물론 클래스가 추상화나 변수 비공개같은 것을 어기고 있지만 아무튼 인수 1개로 줄였으니 좋았으!

```
