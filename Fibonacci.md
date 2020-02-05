# 피보나치 수열

피보나치 수열은 전형적으로 재귀함수를 사용가능하다.

> ```python
> def fibo(n):
>     if n<3:
>         return 1
>     return fibo(n-1) + fibo(n-2)
> ```

하지만, 재귀 함수를 쓸 때, 일정 이상 연산에서 현저히 느리게 되는 경우가 있다.

> ```python
> def fibonacci(n):
>     a, b = 1, 0
>     for i in range(n):
>         a, b = b, a + b
>     return b
> ```
>
> 