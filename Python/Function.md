# Function (함수)
## 정의
- 함수는 특정 작업을 수행하도록 짜여진 코드블록으로 input에 대해 연상을 한 뒤 output을 출력하는 기능을 함.
![function schematic diagram](/imgs/function.png)
- 함수를 만든다는 것은 특정 작업을 하는 코드를 작성하고 함수에 이름을 붙여주는 것.
- 개발자는 이름(함수명)을 통해서 필요할 때마다 해당 기능을 빠르고 간편하게 호출할 수 있게 됨.

## 함수의 정의와 호출
```python
# 함수 정의
def 함수이름(매개변수1, 매개변수2, ...,):
    수행할 코드

# 함수 호출
함수이름(인자1, 인자2, ...,)
```
- 예시
```python
def func(x, y):
    return x + y

print(func(3, 4))    # 7
```

## 함수의 종류
1. 매개변수가 없는 경우
    ```python
    # 매개변수가 없는 함수
    def hi(): 
		print('안녕하세요 차은우입니다.')

    hi()  # 안녕하세요 차은우입니다.
    ```
2. 매개변수가 있는 경우
    ```python
    def hello(name):
        print(f'{name}님 안녕하세요. {name}님')

    hello('Jace')  # Jace님 안녕하세요.
    ```
3. 결과값을 반환하지 않는 함수
    ```python
    def plus_x_y(x, y):
        print(x + y)

    sum(3 + 4)  # 7
    ```
4. 결과값을 반환하는 함수
    ```python
    def minus_x_y(x, y):
        return x - y

    print(minus(9, 4))  # 5
    ```

## Arguments (인자)
- 함수가 호출될 때, 전달되는 실제값

### Default Arguments (디폴트 매개변수)
- 함수를 호출할 때, 인자를 제공하지 않아도 기본적으로 사용된 값을 미리 지정해놓은 것.
```python
def plus(a, b = 1):
    return a + x

print(plus(2))  # 3
```

### Positional Arguments (위치 인자)
- 함수에 전달된 인자의 순서랑 함수에 정의된 매개변수의 순서를 매칭해서 동작하는 것.
- 위치인자는 키워드인보다 먼저 전달되어야 함.
```python
def pos_argu(name, age, gender):
    print(f'{name}의 나이는 {age}이고 성별은 {gender}입니다.')

pos_argu('Jace', 28, '남성')
# Jace의 나이는 28이고 성별은 남성입니다.
pos_argu(28, '남성', 'Jace')
# 28의 나이는 남성이고 성별은 Jace입니다.
```

### Variable-length Positional Arguments (가변 위치 인자) (*args)
- 함수에서 여러개의 위치인자를 받고 싶을 때 사용함.
- `*`를 이용해서 정의하고 뒤에 어떤 변수명을 사용해도 상관없지만, 관습적으로 `*args`로 표기해서 사용함.
```python
def get_num(*args):
	return sum(args)

print(get_num(1,2,3,4,5))  # 15
```
- 전달된 인자들은 함수 내부에서 튜플의 형태로 사용됨.
```python
def get_num(*args):  # 가변매개변수
    for i, v in enumerate(args):  # enumerate: 인덱스랑 값을 같이 가져옴
        print(f'index값: {i}, value값; {v}')

get_num('Jung', 'Jace')
# index값: 0, value값; Jung
# index값: 1, value값; Jace
```

### Keyword Arguments (키워드 인자)
- 함수를 호출할 때, 인자의 key와 value를 값이 전달하는 것,
- 인자 순서에 상관없이 인자의 이름을 명시해서 값을 전달할 수 있음.
```python
def key_argu(name, age, gender):
	print(f'{name}의 나이는 {age}이고 성별은 {gender}입니다.')

key_argu(name = 'Jace', age = 18, gender = '남성')
# Jace의 나이는 18이고 성별은 남성입니다.
key_argu(gender = '남성', name = 'Jace', age = 18)
# Jace의 나이는 18이고 성별은 남성입니다.
```

## Variable-length Keyword Arguments (가변 키워드 인자)
- 함수를 호출할 때, 여러개의 키워드 인자(key = value형태의 인자)를 받고 싶을 떄 사용.
- `**`를 이용해서 정의하고 뒤에 어떤 변수명을 사용해도 상관없지만, 관습적으로 `**kwargs`로 표기해서 사용함.
```python
def get_info(**kwargs):
    for k, v in kwargs.items():
        print(f'Key값: {k}, value값: {v}')

get_info(name='Jace', age= 18, gender = '남성', city = 'Seoul')
# Key값: name, value값: Jace
# Key값: age, value값: 18
# Key값: gender, value값: 남성
# Key값: city, value값: Seoul
```

## 가변 위치 인자와 가변 키워드 인자 함께 쓰기
```python
# 왜 오류가 날까?
def example_args(args1, args2, *args, **kwargs):
	print(args1, args2, *args, **kwargs)

example_args(1, 2, 'Jace', 'John', name1 = 'Kim', name2 = 'Alice')
# TypeError: print() got an unexpected keyword argument 'name1'
```
- 함수 안에서 가변 위치 인자랑 가변 키워드 인자들의 이름을 args, kwarg로 했기 때문에, 매개변수를 `*args`, `**kwargs` 로 쓰는 것이 아니라 `args`, `kwargs`로 사용해야 함.
```python
def example_args(args1, args2, *args, **kwargs):
	print(args1, args2, args, kwargs)

example_args(1, 2, 'Jace', 'John', name1 = 'Kim', name2 = 'Alice')
# 1 2 ('Jace', 'John') {'name1': 'Kim', 'name2': 'Alice'}
```

## Parameter (매개변수)
- 함수가 호출될 때, 입력받은 인수(arguments)를 처리하기 위해서 함수 내부에서 사용되는 변수

### 특수 매개 변수
```python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```
1. pos1, pos2: Positional-only 매개변수
    - 이전에 있는 매개변수들은 위치 인자만으로 전달 가능합니다.
    - f(1, 2)는 가능하지만, f(pos1=1, pos2=2)는 오류 발생.

2. pos_or_kwd: Positional-or-keyword 매개변수
    - 위치 인자 또는 키워드 인자로 모두 전달 가능합니다.
    - f(1, 2, 3) 또는 f(1, 2, pos_or_kwd=3) 둘 다 가능.

3. kwd1, kwd2: Keyword-only 매개변수
    - * 이후에 있는 매개변수들은 반드시 키워드 인자로만 전달해야 합니다.
    - f(1, 2, 3, kwd1=4, kwd2=5)는 가능하지만, f(1, 2, 3, 4, 5)는 오류 발생.

## 반환값 (return)
- 함수가 실행을 끝내고 호출한 곳으로 돌려주는 결과값을 의미
- `return` 으로 반환값을 지정함.
- `return`이 없으면 `None`으로 반환됨.
- 여러 개의 값을 반환하는 경우에는 튜플의 형태로 전달됨.
```python
# 단일 반환값
def add_1(a, b):
    print(a + b) 

result = add_1(3, 5)
print(result)  # add_1() 함수가 반환값 값이 없어서 None

# 반환값이 없을 때
def add_2(a, b):
    return a + b   # 댠일 뱐환값

result = add_2(3, 5)
print(result)  # 8

# 다수의 반환값
def cal(a, b):
    return a + b, a - b, a * b, a / b

result = cal(8, 4)
print(result)  # (12, 4, 32, 2.0)
```

## Lambda expressions (람다 함수)
- `lambda`라는 키워드를 사용해서 생성할 수 있음.
- 함수, 클래스, 다른 수식 안에서 일회성으로 사용하거나 함수의 이름이 필요없을 때 사용.
```python
lambda 매개변수 : 표현식
```

```python
def make_incrementor(n):
    return lambda x: x + n

f = make_incrementor(42)
print(f(1))  # 43
```

```python
print((lambda x,y: x + y)(10, 20))  # 30
```