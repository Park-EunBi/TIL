# How_to_write_code

## 1. Erlang shell

`erl` 입력해서 시작하고, 코드 작성

## 2. Escript 사용하여 실행

Escript는 컴파일 없이 실행할 수 있다

파일명.erl

```erlang
#!/usr/bin/env escript
main(_Args) ->
	io:format("Hello World").
```

### 실행 방법

escript hello_world.erl

## 3. `.beam` 파일로 컴파일 후 실행하기

```erlang
- module(hello_world). % module의 이름은 파일이름과 동일해야 한다 
- export([start/0]). % 함수를 외부에서 호출 할 수 있도록 

start() ->
	hello_world(),
	init:stop().
hello_world() ->
	io:format("Hello World\n").
```

얼랭 소스코드 컴파일 -> beam 파일 생성

BEAM이라는 얼랭 가상 머신에서 얼랭 프로그램을 실행하는 방법

.erl 파일 작성 -> 컴파일 -> beam 파일 생성 -> 컴파일된 파일 실행

### [컴파일]

erlc hello_world.erl

### [실행]

`erl -noshell -run hello_world`

컴파일하고, erl 실행하고 모듈명:함수명(파라미터). 로 실행

+) 얼랭에서 함수를 표현하는 방법

`함수명/파라미터_수`  `[main/1]`
