# [quick start tutorial] 01. Sequential Programming

[Erlang -- Sequential Programming](https://www.erlang.org/doc/getting_started/seq_prog.html)

## atom

erlang의 데이터 유형 

단지 이름일 뿐 

값을 가질 수 있는 변수와는 다르다 

```erlang
-module(tut2).
-export([conver/2]).

convert(M,inch) -> 
		M/2.54;

convert(N, centimeter) ->
		N * 2.54.
```

## tuple

위의 예시는 좋은 코드가 아니다 

inch를 cm로 바꾸어야 하는지, cm를 inch로 변경해야 하는지 명확하지 않다 

이럴 때 튜플로 그룹화하여 인자를 전달하면 좀 더 이해하기 좋은 코드가 된다 

```erlang
-module(tut3).
-export([convert_length/1]).

% {centimeter, X} tuple을 전달 받고 
% {inch, X/2.54} tuple을 return 한다 
convert_length({centimeter, X}) ->
		{inch, X/2.54};

convert_length({inch, Y}) ->
		{centimeter, Y * 2.54}.
```

## list

erlang은 줄바꿈 허용하지 않음 (길어도 어쩔 수 없다)

list는 `|` 를 사용하여 head와 tail로 분리할 수 있다 

→ head: list의 첫 번째 요소, tail: head를 제외한 나머지 요소 

```erlang
% not tail recursive 
-module(tut4).
-export([list_lenght/1]).

list_length([]) ->
		0;

% 빈 list가 아니면 tail 부분을 다시 list_length 함수에 전달 
list_length([First | Rest]) -> 
		1 + list_lenght(Rest).
```

erlang에는 문자여 데이터 유형이 없고, 유니코드 문자 목록으로 표시된다 

```erlang
1> [97,98,99].
"abc"
```

## map

key - value 

```erlang
% 작성 방법 
#{"key" => value}.
```

### map을 사용하여 alpha blending 하는 예시

```erlang
-module(color).

-export([new/4, blend/2]).

-define(is_channel(V), (is_float(V) andalso V >= 0.0 andalso V =< 1.0)).

new(R,G,B,A) when ?is_channel(R), ?is_channel(G),
                  ?is_channel(B), ?is_channel(A) ->
    #{red => R, green => G, blue => B, alpha => A}.

blend(Src,Dst) ->
    blend(Src,Dst,alpha(Src,Dst)).

blend(Src,Dst,Alpha) when Alpha > 0.0 ->
    Dst#{
        red   := red(Src,Dst) / Alpha,
        green := green(Src,Dst) / Alpha,
        blue  := blue(Src,Dst) / Alpha,
        alpha := Alpha
    };
blend(_,Dst,_) ->
    Dst#{
        red   := 0.0,
        green := 0.0,
        blue  := 0.0,
        alpha := 0.0
    }.

alpha(#{alpha := SA}, #{alpha := DA}) ->
    SA + DA*(1.0 - SA).

red(#{red := SV, alpha := SA}, #{red := DV, alpha := DA}) ->
    SV*SA + DV*DA*(1.0 - SA).
green(#{green := SV, alpha := SA}, #{green := DV, alpha := DA}) ->
    SV*SA + DV*DA*(1.0 - SA).
blue(#{blue := SV, alpha := SA}, #{blue := DV, alpha := DA}) ->
    SV*SA + DV*DA*(1.0 - SA).
```

## **A Larger Example**

```erlang
%% This module is in file tut5.erl

-module(tut5).

%% export 되지 않은 함수는 지역 함수가 된다 
-export([format_temps/1]).

%% Only this function is exported
%% 다른 언어의 loop와 유사한 역할 (재귀로 표현)
format_temps([])->                        % No output for an empty list
    ok;
format_temps([City | Rest]) ->
    print_temp(convert_to_celsius(City)),
    format_temps(Rest).

convert_to_celsius({Name, {c, Temp}}) ->  % No conversion needed
    {Name, {c, Temp}};
convert_to_celsius({Name, {f, Temp}}) ->  % Do the conversion
    {Name, {c, (Temp - 32) * 5 / 9}}.

print_temp({Name, {c, Temp}}) ->
    io:format("~-15w ~w c~n", [Name, Temp]).
```

```erlang
% result 

35> c(tut5).
{ok,tut5}
36> tut5:format_temps([{moscow, {c, -10}}, {cape_town, {f, 70}},
{stockholm, {c, -4}}, {paris, {f, 28}}, {london, {f, 36}}]).
moscow          -10 c
cape_town       21.11111111111111 c
stockholm       -4 c
paris           -2.2222222222222223 c
london          2.2222222222222223 c
ok
```

## **Matching, Guards, and Scope of Variables**

```erlang
-module(tut6).
-export([list_max/1]).

% 1개의 parameter가 전달되면 Head와 Rest로 나누어 list_max() 호출
list_max([Head|Rest]) ->
   list_max(Rest, Head).

% 2의 parameter가 들어왔지만 앞 인자가 비어 있으면 Res 반환
% 이미 max 값 판단이 끝난 경우
list_max([], Res) ->
    Res;
% 2개의 parameter가 들어왔고, head 값이 더 크면 
% Result_to_far 값을 버리고 Head 값을 넘김 
% 두번째 인자의 값이 현재까지의 max의 값 
% 계속 재귀함수를 돌며 리스트의 1번째 값을 Result_so_far 값과 비교한다 
%% (erlang list는 1번 인덱스 부터 시작)
list_max([Head|Rest], Result_so_far) when Head > Result_so_far ->
    list_max(Rest, Head);

% Result_so_far 값이 Head보다 클 경우 Head 값을 버린다 
list_max([Head|Rest], Result_so_far)  ->
    list_max(Rest, Result_so_far).
```

```erlang
37> c(tut6).
{ok,tut6}

38> tut6:list_max([1,2,3,4,5,7,4,3,2,1]).
7
```

Erlang에서 인자의 수가 다르면 완전히 다른 함수로 본다 

### list_max 알고리즘 설명

list를 head와 tail로 분리하여 head값과 이전까지의 max값을 비교한다 

비교 후 큰 값을 max 값으로 설정하고 재귀 함수를 돌며 다음 인덱스의 값을 비교한다 

⇒ 재귀적으로 head 부분만 분리하여 비교한다  

## **More About Lists**

`|` operation은 list를 head(가장 앞 요소 1개) 와 tail로 분리한다 

### reversing the order of a list

```erlang
-module(tut8).
-export([reverse/1]).

reverse(List) ->
    reverse(List, []).

% head값을 Reversed_List의 앞 부분으로 붙인다 
reverse([Head | Rest], Reversed_List) ->
    reverse(Rest, [Head | Reversed_List]);
reverse([], Reversed_List) ->
    Reversed_List.
```

```erlang
52> c(tut8).
{ok,tut8}

53> tut8:reverse([1,2,3]).
[3,2,1]
```

STELIB에서 지원되는 함수가 많기에 새로 작성하기 전에 확인해보기 

```erlang
-module(tut7).
-export([format_temps/1]).

format_temps(List_of_cities) ->
    Converted_List = convert_list_to_c(List_of_cities),
    print_temp(Converted_List),
    {Max_city, Min_city} = find_max_and_min(Converted_List),
    print_max_and_min(Max_city, Min_city).

convert_list_to_c([{Name, {f, Temp}} | Rest]) ->
    Converted_City = {Name, {c, (Temp -32)* 5 / 9}},
    [Converted_City | convert_list_to_c(Rest)];

convert_list_to_c([City | Rest]) ->
    [City | convert_list_to_c(Rest)];

convert_list_to_c([]) ->
    [].

print_temp([{Name, {c, Temp}} | Rest]) ->
    io:format("~-15w ~w c~n", [Name, Temp]),
    print_temp(Rest);
print_temp([]) ->
    ok.

find_max_and_min([City | Rest]) ->
    find_max_and_min(Rest, City, City).

find_max_and_min([{Name, {c, Temp}} | Rest], 
         {Max_Name, {c, Max_Temp}}, 
         {Min_Name, {c, Min_Temp}}) ->
    if 
        Temp > Max_Temp ->
            Max_City = {Name, {c, Temp}};           % Change
        true -> 
            Max_City = {Max_Name, {c, Max_Temp}} % Unchanged
    end,
    if
         Temp < Min_Temp ->
            Min_City = {Name, {c, Temp}};           % Change
        true -> 
            Min_City = {Min_Name, {c, Min_Temp}} % Unchanged
    end,
    find_max_and_min(Rest, Max_City, Min_City);

find_max_and_min([], Max_City, Min_City) ->
    {Max_City, Min_City}.

print_max_and_min({Max_name, {c, Max_temp}}, {Min_name, {c, Min_temp}}) ->
    io:format("Max temperature was ~w c in ~w~n", [Max_temp, Max_name]),
    io:format("Min temperature was ~w c in ~w~n", [Min_temp, Min_name]).
```

## if and case

### if

```erlang
if
    Condition 1 ->
        Action 1;
    Condition 2 ->
        Action 2;
    Condition 3 ->
        Action 3;
    Condition 4 ->
        Action 4
end
```

매치 되지 않으면 런타임 에러를 발생시킨다 

success되면 항상 atom `true`를 반환한다

This is often used last in an if, meaning, do the action following the true if all other conditions have failed.

```erlang
60> c(tut9).
{ok,tut9}
61> tut9:test_if(5,33).
A == 5
a_equals_5
62> tut9:test_if(33,6).
B == 6
b_equals_6
63> tut9:test_if(2, 3).
A == 2, B == 3
a_equals_2_b_equals_3
64> tut9:test_if(1, 33).
A == 1 ; B == 7
a_equals_1_or_b_equals_7

%if case에 없는 내용이기에 런타임 에러를 발생시킨다 
66> tut9:test_if(33, 33).
** exception error: no true branch found when evaluating an if expression
     in function  tut9:test_if/2 (tut9.erl, line 5)
```

### case

이전에 작성했던 코드를 case를 사용하여 변경할 수 있다 

```erlang
% 이전에 작성한 코드 
convert_length({centimeter, X}) ->
    {inch, X / 2.54};
convert_length({inch, Y}) ->
    {centimeter, Y * 2.54}.
```

```erlang
% case를 사용한 코드 
-module(tut10).
-export([convert_length/1]).

convert_length(Length) ->
    case Length of
        {centimeter, X} ->
            {inch, X / 2.54};
        {inch, Y} ->
            {centimeter, Y * 2.54}
    end.
```

```erlang
67> c(tut10).
{ok,tut10}
68> tut10:convert_length({inch, 6}).
{centimeter,15.24}
69> tut10:convert_length({centimeter, 2.5}).
{inch,0.984251968503937}
```

## **Built-In Functions (BIFs)**

Erlang virtual machine에 내장된 함수들

```erlang
75> trunc(5.6).
5
76> round(5.6).
6
77> length([a,b,c,d]).
4
78> float(5).
5.0
79> is_atom(hello).
true
80> is_atom("hello").
false
81> is_tuple({paris, {c, 30}}).
true
82> is_tuple([paris, {c, 30}]).
false
```
