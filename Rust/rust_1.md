# 러스트 입문

## 러스트 특징 정리
- 컴파일 언어
- 다중 패러다임 언어(함수형,절차지향,객체지향,병렬형 등등)
- LLVM(Low Lever Virtual Machine: 저레벨 가상머신) 사용
- 러스트는 안전하고, 빠르고, 병렬성에 초점을 둔 시스템 프로그래밍 언어

<br>

## Rust 설치
러스트 공식 홈페이지 설치 가이드 참조
- https://www.rust-lang.org/learn/get-started

<br>

## Hello World 실행해보기

1. 러스트 프로젝트용 폴더 생성
2. 해당 폴더 하위에 hello_world 폴더 생성(여러 단어 사용시 언더스코어`_`를 구분자로 사용할 것을 권장)
3. main.rs 파일 생성
4. 다음 내용 입력

```rust
fn main() {
    println!("Hello, world!");
}
```
5. Hello, World 출력
```
$ rustc main.rs (컴파일)
$ ./main
Hello, world!
```

## Hello, World 출력 해석

1. main이라는 함수가 첫번째로 실행되는 코드이다.
2. `println!`는 러스트 매크로(macro)라고 불린다. 만약에 함수라고 부르기 위해선 `!`println으로 입력되었어야 한다. 매크로에 대한 자세한 사항은 나중에 알아보도록 하며,
   지금은 `!`가 붙으면 보통의 함수 대신 매크로를 호출하고 있음을 의미
3. "Hello, world" 는 스트링 타입이며 해당 문자열이 화면에 출력되는 것
4. 라인을 마칠 때 세미콜론`;`으로 끝난다
5. 러스트는 컴파일 언어이기때문에 프로그램을 실행하기 위해선 먼저 rust 파일을 컴파일하는 과정이 필요하다
6. 컴파일이 완료되면 실행 파일이 생성된다
7. 러스트는 ahead-of-time compiled 언어로, 이는 프로그램을 컴파일하여 만들어진 실행파일이 다른 환경의 컴퓨터에서 러스트가 설치되어 있지 않아도 바로 실행될 수 있다는 것을 말한다.

<br>

### 참조
- https://rinthel.github.io/rust-lang-book-ko/
