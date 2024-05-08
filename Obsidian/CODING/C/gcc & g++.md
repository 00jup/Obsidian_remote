![](https://velog.velcdn.com/images/00jup/post/7e2c54fc-02d6-4e1e-af42-cc72c8f28498/image.png)
[[gcc option]]

# mkdir touch로 파일 생성하기
## mkdir
```
mkdir {$directory_filename}
```

## touch
```
cd {$directory_filename}
touch {$filename}.c {$filename2}.c
```
근데 여기서 궁금한 점(20230602)이 생겼다.
만약 20230602폴더로 이동하지 않고 외부에서 파일을 생성해보자.
```
touch 20230602/{$filename}.c {$filename2}.c
```
이렇게 하면 가능할 줄 알았는데 작동하지 않는다.
```
# 1번
touch 20230602/{{$filename}.c {$filename2}.c}
# 2번
touch 20230602/{$filename}.c 20230602/{$filename2}.c
```
구글링도 해보고 chatGPT에게 얻은 답은 위와 같았다.
실행 결과는..? 2번은 가능했지만 1번은 되지 않았다. terminal에서는 다음과 같이 알려줬다.
```
zsh: parse error near `}'
```
실패였다. 계속 찾아보려고 한다!

# 1️⃣ gcc && g++
 ## 1️⃣-1️⃣ gcc랑 g++로 compile만 하기
 ```
 gcc {$filename}.c
 
 g++ {$filename}.cpp
 ```
 > 이렇게 되면 컴파일 되고 a.out이 생긴다.
 ```
 ./a.out
 ```
 으로 실행하면 끝
 
## 1️⃣-2️⃣ gcc랑 g++로 원하는 이름으로 compile하기
```
gcc -o {$filename} {$filename}.c

g++ -o {$filename} {$filename}.cpp
```
이렇게 하면 {$filename}으로 compile이 된다.
```
gcc {$filename}.c -o {$filename}

g++ {$filename}.cpp -o {$filename}
```
이것도 가능하다
`-o`가 어떤 기능을 하는지 몰라서 `g++ -help`를 통해서 찾아봤다.
기능은 아래와 같다.
> -o `<file>` Write output to `<file>`

실행은 
```
./{$filename}
```
으로 진행한다.

## 1️⃣-3️⃣ warning을 잡으면서 compile하는 방법
```
gcc -Wall -Wextra -Werror {$filename}.c

g++ -Wall -Wextra -Werror {$filename}.cpp
```
컴파일 후에
```
./a.out
```
으로 실행한다.

이름은 변경하고 싶으면 `1️⃣-2️⃣ gcc랑 g++로 원하는 이름으로 compile하기`처럼 -0를 사용한다.

## 참고 1️⃣-4️⃣ gcc -o -c option 같이 사용하기
```
gcc