## The ERLANG shell

Can start **erl**

**.** 으로 문장 끝내기

q().으로 종료

## Data Types

### integers

진수#값

2#1010, -16#EA

### Float

17.5, 1.234E-10

### Atoms

Enumeratin types과 같은 역할을 하는 것

소문자로 시작하거나 ' 으로 감싸기

Erlang에는 boolean 없음

January 'January' true false

### Tuples

{1, 2, 3}, {abc, {4, c}}

다른 타입 저장 가능

### Lists

[1, 2, 3], [abc, {4, c}]

### List vs Tuples

Tuple

- 특정 element 뽑아낼 때 주로 사용
- Fixed data set 나타낼 때 사용

List

- split 가능
- 이미 존재하는 리스트에서 수정 가능
- Dynamic data set 만들 때 주로 사용

## Variables

항상 대문자로 시작

'_' 제외하고 다른 문자 사용 가능

한번 값 할당하면 변경 불가능

소문자로 시작하면 atom

## Good to know

Erlang 변수는 모두 call by value (call by reference는 존재하지 않는다)

Erlang 변수는 모두 local variable (global variables 없음)

변수 선언 필요 없음 (dynamic type system)

메모리는 런타임 시스템에 의해 할당되고,

Garbage collector에 의해 반환된다

## Lists operations (cons operator)

Head 와 tail 로 분리 가능

Head는 첫번째 element

Tail은 head를 제외한 나머지 element

```erlang
[Head | Tail] = List
NewList = [Head | Tail]
```

## List operators

1. […|…] : head와 tail을 나누고 합치는 연산자
2. ++: 두 개의 list를 합쳐서 new list 만드는 연산자
3. -: 왼쪽 리스트에서 오른쪽 리스트의 elemet를 제거하는 연산자

```erlang
[1, 2, 2, 3, 4, 4, 5, 6] -- [2, 4]
[1, 2, 3, 4, 5, 6]
```

++와 --는 오른쪽에서부터 연산

```erlang
[1, 2, 3] -- [1, 3] -- [1, 2]

% 위의 코드 실행 결과 
[1, 2]
```

## ++ vs [..|..]

하나의 element를 리스트의 앞부분에 추가하려면

++와 [..|..] 둘 다 사용할 수 있다

그러나 리스트를 사용하는 것은 프로그램을 느리게 할 수 있기에 효율적인 방법이 아니다

```erlang
[1 | [2, 3, 4]]

[1] ++ [2, 3, 4]
```

## Where are the strings?

String 은 list의 한 종류

```erlang
[$H, $e, $l, $l, $o, $ , $W, $o, $r, $l, $d]

“Hello World”
```

Character는 integer로 표현될 수 있기에 string list는 integer list 로 변환될 수 있다

```erlang
“Hello World”

[72,101,108,108,111,32,87,111,114,108,100]
```

## Time to practice

> build a sorted list MyList starting from  A = [4, 5], B = 1, C = [2, 3]
> 

```erlang
[b|c] ++ A
```

> build a complete LDN for a Rcs=1 MO element using: ME = “ManagedElement=1” ENB = “ENodeBFunction=1” RCS = “Rcs=1”
> 

```erlang
ME ++ “,” ++ ENB ++ “,” ++ RCS
“ManagedElement=1,ENodeBFunction=1,Rcs=1”
```

## Built in functions

hd/1

tl/1

length/1

tuple_size/1

element/2

### Example

```erlang
1> List [one, two, three, four, five].

2> hd(List)

One

3> tl(List)

[two, three, four, five]

4> length(List)

5

5> Tuple = { 5, 4, 3, 2, 1}

6> tuple_size(Tuple)

5

7> element(2, Tuple)

4
```

## Type conversion

atom_to_list/1, list_to_atom/1, list_to_existing_atom/1

모든 list와 atom은 변환 가능하다

list_to_tuple/1, tuple_to_list/1

is_float/1, list_to_float/1

float_to_list/1, integer_to_list/1

round/1, trunc/1 (버림), list_to_integer/1

## Pattern matching

변수에 패턴 매칭 방법을 통해 값이 바인딩된다

### Used to

변수에 값 할당할 때

프로그램 실행 흐름 조절할 때

Compound data type 값 추출할 때

Pattern = expression

### Pattern

데이터 구조

지역 변수, 전역 변수, 리터럴 값을 담을 수 있다

### Express

데이터 구조, 지역 변수, 수학 연산자, 함수 호출

### = 연산자 오른쪽에 오는 expression은 먼저 평가 되고, pattern과 비교된다

Pattern과 expression은 같은 모양을 가지고 있어야 한다

Pattern의 literal 값은 expression의 위치에 해당하는 값과 같아야 한다 (무슨소리지)

Pattern 매칭이 성공되면 바운딩 되지 않은 값이 결과 값으로 바인딩 된다

지역 변수는 표현이 위치한 값과 같은 값을 가져야 한다

Sum = 1 + 2

만약 sum이 바운딩 되지 않았다면 패턴 매칭에 성공하고 sum은 3으로 바운딩 된다

만약 sum이 바운드 되었다면 이미 바운드된 3으로만 패턴이 매칭된다

=> 변수에 값을 저장하는 방식이 pattern matching인데

올바른 값만 바운딩 되고, 이미 바운딩 된 값이 있다면 바운딩 되지 않는다는 의미

### 문제

```erlang
%% (1)에서는 오류가 나고, (2)에서는 오류가 나지 않는 이유 ********%%******** 

>List = [1, 2, 3, 4].
>[Head|Tail] = List.
>Head.
1
>Tail
[2, 3, 4]

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

>[Head|Tail] = 1. --------(1)

Exception error 발생

>[Head|Tail] = [1, 2, 3, 4].  -------(2)

[1, 2, 3, 4]
```

### 정답

: 이미 Head = 1, Tail = [2, 3, 4]로 바인딩 되어서 다른 값으로 바인딩이 안됨

Head = 1, Tail = [ ]으로 바인딩을 하려 해서 안되는 것

+) head 와 tail 을 나눌 때 [Head|Tail]으로만 작성하지 않아도 된다

안에 들어가는 값은 변수라 원하는 이름으로 작성하면 된다

[Headtest|Tailtest] 가능

## The wildcard symbol "_"

변수를 할당하지 않고 wildcard symbol을 사용하여 패턴을 나타낼 수 있다

바인딩 하려는 어떤 것이라도 매칭이 된다

{Element1, Element2, _} = {1, 2, 3}

변수명을 "_"으로 시작한다면 익명 또는 don't care 변수가 된다

이러한 변수는 문법상으로는 필요하나 프로그램 상에서 필요 없을 때 사용된다

Don't care 변수는 일반 변수 처럼 사용 된다

검사, 사용, 비교에 사용될 수 있다

"_"는 변수에서 독립적으로 사용되거나, don't care 변수가 된다.

하지만 이러한 변수는 아무것에도 access 할 수 없다 (값이 무시되고, 절대 바운딩 되지 않는다)

## 문제

```erlang
This works:

{A,_,[B|_],{B}} = {abc,23,[22,23],{22}}

This fails:

{A,_I,[B|_I],{B}} = {abc,23,[22,23],{22}}
```

### 정답

첫 번째 문장에서는

"_"는 바인딩이 되지 않는 기호라 앞의 _에는 23, 뒤의 _에는 [23]이 들어갈 수 있다 

근데 두 번째 문장에서는

같은 변수 "_I"에 23과 [23]을 바인딩 하고자 해서 에러가 발생하는 것이다

23과 [22, 23] 속 23은 다르다

## Function

함수 이름은 atom이고, 괄호 뒤에 0개 혹은 여러개의 파라미터를 괄호로 감싸 넣는다

매개변수의 수를 arity라고 부른다

화살표는 함수이름(파라미터) 와 body를 분리한다

```erlang
function/2

Function(Param1, Param2) -> Body.
```

함수는 모듈로 정의되어야 하고, 각각 컴파일 되어야 한다

함수의 바디에는 적어도 하나의 comma(,)로 끝나는 표현이 있어야 한다

Return value는 마지막 표현의 실행 결과이다

함수는 세미콜론으로 분리된 문장(조항)들의 집합, 모든게 끝나야 끝난다 (?)

함수가 불리면, 호출에서 불린 각 절들은 순차적으로 패턴 매칭에 의해 체크된다

- 성공하면, 변수들은 바운딩되고, 바디는 실행된다
- 실패하면, 다음절이 선택되고, 매치된다

함수를 정의할 때, 각 절의 모든 요소들에 대해 하나의 절이 성공하는지를 확인하는 것이 좋다

- This is done by making the final clause a catch-all clause that matches all the remaining clauses.

## Modules

함수는 모듈 안에서 그룹을 이룬다

확장자가 .erl일 파일들

모듈 이름은 -module(Name)으로 지정한다

모듈 이름과 파일 이름은 같아야 한다

module(Hello_world), Hello_world.erl

export 에는 내보낼 함수의 리스트가 포함된다

이 함수들은 전역함수이며, 모듈 밖에서 불릴 수 있다

전역함수는 모둘이름:함수이름(파라미터) 형식으로 사용할 수 있다

```erlang
demo:double(2).
```

## exercise

1. erl 파일 작성
2. module 추가
3. 컴파일 (erlc 파일명.erl)
4. 사용 (모듈명:함수명(파라미터))

### [문제]

- Type the demo:double example into a file called demo.erl. Use your favorite text editor. Start Erlang.
- Give the command c(demo). to compile the file.
- Try running the query:

demo:double(12).

- This is just to test if you can get the system started and can use the editor together with the Erlang system.
1. Write functions temp:f2c(F) and temp:c2f(C) which convert between centigrade and Fahrenheit scales. (*hint 5(F-32) = 9C*)
2. Write a function temp:convert(Temperature) which combines the functionality of f2c and c2f. Example:

temp:1> temp:convert({c,100}).

{f,212}

2> temp:convert({f,32}).

{c,0}

### [정답]

```erlang
- module(temp).
- export([f2c/1, c2f/1, convert/1]).

f2c(Temp) ->
	5 * (Temp - 32) / 9.

c2f(Temp) ->
	((9 * Temp) / 5) + 32.

convert({c, Temp}) ->
	{f, c2f(Temp)};
convert({f, Temp}) ->
	{c, f2c(Temp)};
convert(_Other) ->
	error(input_format_unknown).
```

### [문제]

1. Write a function shapes:perimeter(Form) which computes the perimeter of different forms. Form can be one of:

{square,Side} {circle,Radius} {triangle,A,B,C}

### [정답]

```erlang
- module(shapes).
- export([perimeter/1]).

perimeter({square, Side}) ->
	Side * 4;
perimeter({circle, Radius}) ->
	2 * 3.14 * Radius;
perimeter({triangle, A, B, C}) ->
	A + B + C;
perimeter(Other) ->
	error(unknown_shape).
```
