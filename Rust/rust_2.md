# Cargo 입문

## Cargo란

Cargo(카고)는 러스트의 빌드 시스템 및 패키지 매니저이다. 대부분의 러스트 프로그램들이 이 툴을 사용하여 프로젝트가 관리되고 있으며, Cargo가 코드를 빌드하고, 코드가 의존하고 있는 라이브러리들을 다운로드해주고, 그 라이브러리들을 빌드하는 등의 많은 작업을 대신 수행해준다.

### Cargo 설치
Cargo는 초기에 공식 홈페이지 안내대로 공식 인스톨러를 사용했을 경우 rust 언어와 함께 이미 설치되어 있다. 다른 수단을 통해 러스트를 설치했다면 Cargo가 설치되었는지 확인 필요

```
$ cargo --version
```

## Cargo를 이용한 프로젝트 생성

Cargo를 사용하여 프로젝트 폴더 생성하기

```
$ cargo new hello_cargo --bin
$ cd hello_cargo
```

위 커맨드를 실행하면 hello_cargo라고 불리는 실행 가능한 바이너리를 생성한다(실행 파일을 뜻함). `cargo new` 에게 넘겨지는 `--bin` 인자가 라이브러리가 아닌 실행 가능한 애플리케이션으로 만들어준다. cargo가 동일한 이름의 폴더와 그 하위 경로에 프로젝트의 파일들이 생성된 것을 확인할 수 있다.

```
# 프로젝트 트리
hello_cargo
\ - src
  - .gitignore (Cargo는 default로 Git을 VCS로 사용하며 해당 프로젝트 폴더를 새로운 git 저장소로 초기화한다)
  - Cargo.toml
```

<br>

TOML파일(Tom's Obvious, Minimal Language)포맷으로 작성된 Cargo.toml 파일은 Cargo의 환경설정 포맷이다.

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]

[dependencies]

```

- [package]는 이후 나열되는 문장들이 패키지 환경설정이라는 것을 나타내기 위한 섹션의 시작 지점
- [dependencies]는 프로젝트의 의존성들의 리스트를 적을 수 있는 섹션의 시작 지점이다. 러스트에서는 코드의 패키지를 크레이트(crate)라고 부른다.

### src 폴더
해당 폴더 하위에 main.rs 파일이 있으며 처음으로 배웠던 Hello, world를 출력하는 프로그램이다. 이 파일은 Cargo가 자동으로 src폴더와 함께 생성하여 src폴더 하위에 위치시킨다.
Cargo는 기본적으로 개발자가 작성한 소스 파일들이 src 폴더 안에 있을거라고 가정하며, 최상위 프로젝트 디렉토리는 README 파일, 라이센스 정보, 환경 파일 등등 코드와는 관련 없는 다른 파일들이 위치하여 프로젝트를 조직화하는 데에 도움을 준다.

## Cargo 프로젝트 빌드 및 실행

- cargo build: 프로젝트를 빌드하는 명렁어. 프로젝트 빌드 완료 시 `target/debug/[프로젝트명]` 와 같은 형식의 경로로 실행 파일을 생성한다. 따라서 해당 파일을 명령어를 통해 바로 실행이 가능하다
- cargo run: 프로젝트를 한번의 커맨드로 컴파일하고 만들어진 실행 파일을 바로 실행시켜주는 명령어.
- cargo check: 해당 프로젝트가 컴파일이 되는지 빠르게 확인하기 위해 사용되는 명령어이며 실행 파일을 생성하지 않는다.
- cargo build --release: 해당 명령어를 통해 '최적화'와 함께 프로젝트를 컴파일할 수 있다. `target/debug`대신 `target/release`폴더 아래에 실행파일을 생성하며, '최적화'는 러스트 코드를 더 빠르게 만들어주지만, '최적화'를 키는 것은 프로그램을 컴파일하는데 드는 시간이 길어지게 만든다. 따라서 목적에 따라 두 빌드 명령어를 사용하게 된다.
  - `cargo build`는 주로 개발하는 당시 환경에서 확인하기 위한 용도
  - `cargo build --release`는 배포할 때 사용되는 최종 프로그램을 빌드하기 위한 용도
    

### 참조
- https://rinthel.github.io/rust-lang-book-ko/ch01-03-hello-cargo.html
