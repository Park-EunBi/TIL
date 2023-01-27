# Tail-recursive

## 꼬리 재귀

재귀함수의 call stack이 깊어질수록 memory overhead가 발생.

이 문제를 해결하기 위한 방법이 꼬리 재귀

재귀함수의 실행 결과가 연산에 사용되지 않고 바로 반환되도록 하여 이전 함수의 상태를 유지할 필요 없도록 작성하는 것

=> 재귀 호출이 끝난 후 현재 함수에서 추가 연산을 요구하지 않도록 구현하는 재귀 (stack을 덮어 씀)

꼬리 재귀를 사용하려면 TCO(Tail Call
Optimization)을 지원해줘야 한다

### <일반 재귀 - direct recursion>

```erlang
% Erlang code

bump([]) ->
	[];
  
bump([H|T]) ->
	[H + 1 | bump(T)]. %% 반환 값에서 추가 연산 진행
```

### <꼬리재귀 - tail-recursion>

1. 반환 값에서 추가 연산 없이 바로 함수 호출
2. Acc변수에 계산한 값을 저장한 후 값을 한번에 반환 

```erlang
% Erlang code

bump([], Acc) ->
	Acc;
  
bump([H|T],Acc) ->
	bump(T, Acc ++ [H + 1]). %% 반환 값에서 추가 연산 없이 바로 함수 호출

%% Acc :accumulator - 누산기
```
