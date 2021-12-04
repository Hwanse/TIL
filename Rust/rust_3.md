# 변수와 가변성 정리

## 변수 선언

### 불변(Immutable) 변수

러스트에서는 기본 변수는 `불변성`이다. 이는 러스트가 안정성, 손쉬운 동시성이라는 장점을 가지게하도록 코드를 작성하게끔 강제하는 요소 중 하나다.

```rust
fn main() {
    let x = 5;  // default 불변성 변수, 변수 선언 시 let 키워드를 사용한다
    println!("The value of x is: {}", x);
    x = 6;
    println!("The value of x is: {}", x);
}
```

위와 같은 코드를 컴파일할 경우 다음과 같은 에러를 발생시킨다.

```
error[E0384]: re-assignment of immutable variable `x`
 --> src/main.rs:4:5
  |
2 |     let x = 5;
  |         - first assignment to `x`
3 |     println!("The value of x is: {}", x);
4 |     x = 6;
  |     ^^^^^ re-assignment of immutable variable
```

에러의 원인은 '불변성 변수'에 값을 재할당하려고 시도했기 때문에 발생한 에러, 러스트는 컴파일러가 변하지 않는 값에 대한 보증을 해주기 때문에, 개발자는 해당 변수의 값이 어떻게 변경되는지 추적할 필요가 없게끔 만들어준다,

### 가변(Mutable) 변수

변수명의 접두어로 `mut`를 추가하면 '가변성 변수'로 선언하게 된다. 이 변수의 값을 변경하는 것을 허용하게 된다.

```rust
fn main() {
    let mut x = 5;  // mut 키워드를 접두어로 붙인다
    println!("The value of x is: {}", x);
    x = 6;
    println!("The value of x is: {}", x);
}
```

x 변수를 가변 변수로 선언한 것을 제외하곤 위 예제 코드와 같은 내용의 프로그램이다. 실행시 다음과 같은 결과를 출력한다.

```
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.30 secs
     Running `target/debug/variables`
The value of x is: 5
The value of x is: 6
```

### 상수

러스트에서는 상수 선언 시 다음과 같은 특징이 있다.

- 상수 변수 선언시 `mut`를 사용하는 것이 허용되지 않는다.
- 상수 선언시 let 키워드 대신 `const`키워드를 사용해야 한다.
- 상수 선언시 값의 유형(자료형, 데이터 타입)을 명시하여 선언해야 한다.
- 상수는 전체 영역을 포함한 어떤 영역에서도 선언될 수 있다.
- 상수는 오직 상수 표현식만 설정될 수 있지만, 함수 호출의 결과값이나 그 외 런타임 시점에 결정되는 값이 설정될 수 없다

```rust
fn main() {
const MAX_POINTS: u32 = 100_000;
}
```

<br>

## Shadowing

러스트에서는 'let'키워드를 사용하여 같은 변수명으로 반복하여 선언하는 것이 가능하며 이를 "변수를 `shadowing`한다"라고 말한다. 러스트 개발자들은 이를 첫 변수가 두 번째 변수에 의해 shadowed 됐다고 표현한다.

기본적으로 let 키워드만 사용하여 변수를 선언하고 불변 변수이기 때문에 해당 변수에 새 값을 대입하려 하면 컴파일시 에러가 발생된다. 하지만 위와 같이 shadowing을 활용하여 똑같은 변수명으로 새로운 값을 대입하는 방식과 이는 'mut'으로 선언하는 것과 2가지 차이가 있다.    

첫째, mut을 사용하는 것과 같은 효과를 볼 수 있지만, 이후 마지막으로 선언된 변수는 불변성의 특징을 가져갈 수 있다.

```rust
fn main() {
    let x = 5;

    let x = x + 1;  // 처음 선언된 x 변수를 let x 구문으로 shadowing

    let x = x * 2;  // 세번째 let x로 두번째 x를 shadowing

    println!("The value of x is: {}", x);
}
```

이 프로그램을 실행하면 다음과 같은 결과를 출력한다.

```
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.31 secs
     Running `target/debug/variables`
The value of x is: 12
```


둘째, mut 사용할 경우에는 변수의 자료형을 변경할 수 없지만, let 키워드를 다시 사용하여 새 변수 선언을 통해 shadowing을 활용하면 변수의 자료형을 변경할 수 있다.

```rust
fn main() {
    let spaces = "   ";
    let spaces = spaces.len();
}
```

다음은 프로그램 실행 결과

```
$ cargo run
   Compiling variables v0.1.0 (/Users/kimhs/study-work/rust-study/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.37s
     Running `target/debug/variables`
spaces length : 3
```
