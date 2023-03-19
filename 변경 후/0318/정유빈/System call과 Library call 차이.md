<h1> System call과 Library call의 차이 </h1>

- System call과 Library call의 주요 차이점은 System call은 커널에 대한 Resource Acess 요청이고, Library call은 프로그래밍 라이브러리에 정의 된 함수를 사용하라는 요청입니다. <br />

- 응용 프로그램은 시스템 콜이나 라이브러리 함수를 통해 커널의 모듈을 사용해 특정 기능을 발휘할 수 있습니다.
- 여기서 바로 시스템 콜을 사용하느냐 라이브러리 함수를 사용하느냐 두 가지로 나뉠 수 있는데 라이브러리 함수를 사용한다면 함수 내에 사용된 시스템 콜을 사용합니다.
- 반대로 응용 프로그램 내에서 바로 시스템 콜을 사용한다면 라이브러리 함수를 거치지 않고 커널의 기능을 사용할 수 있습니다.
<br />

<h1> 시스템 콜(System Call) </h1>

- 커널(Kernel)에 직접 서비스를 요청하는 것을 말한다.
- 주로 하드웨어, 프로세스, 파일 등의 I/O 등을 처리하며 프로그램은 사용자(User) 모드가 아닌 커널 모드로 실행된다.
- 시스템에 직접 접근하기 때문에 프로그래머가 로우레벨(Low-Level)까지 제어할 수 있지만, 커널에 직접 접근하는 만큼 남용하면 성능 손실이 일어난다.
- 대표적인 시스템 콜 함수로는 open, read, write가 있다.

<h1> 라이브러리 함수 </h1>

- 시스템 콜 함수를(Wrapping) 한 것이다.
- 함수 내부에서 메모리 할당/해제가 일어나고, 잦은 커널 호출로 인한 성능 손실을 줄이기 위해 입력을 모았다가 한  번에 커널에 요청하기도 한다.
- 대표적인 라이브러리 함수로는 fopen, fread, fprint가 있다.

<br />
- 시스템 콜인 open은 파일 디스크립터(File Descriptor)를 반환하고, 라이브러리 함수인 fopen은 파일 포인터(FILE*)를 반환한다.

<h1> File Descriptor </h1>

- 파일 디스크립터는 아래와 같이 가져올 수 있다.
- 사용한 파일 디스크립터는 close를 이용해 닫아주어야 한다.

```
#include <fcntl.h>

int main() {
    int fd = open("hello.txt", O_RDONLY);
    close(fd);
    return 0;
}
```

- 파일을 읽고 수정할 때는 <b> read </b> 와 <b> write </b> 를 이용하면 된다.
- read와 write는 unistd.h에 정의되어 있다.

```
#include <fcntl.h>
#include <unistd.h>

int main() {
    int fd = open("hello.txt", O_RDWR);
    char buf[101];
    read(fd, buf, 100);
    write(fd, buf, 100);
    close(fd);
    return 0;
}
```

- 시스템 콜 함수는 메모리를 직접 할당하지 못하기 때문에 파일을 읽어올 때도 프로그래머가 buf를 넣어줘야 한다.

<h1> FILE* </h1>

- 파일 포인터는 아래와 같이 가져올 수 있다.
- 사용한 파일 스트림은(Stream)은 fclose를 이용해 닫아주어야 한다.

```
#include <stdio.h>

int main() {
    FILE* stream = fopen("hello.txt", "r+");
    fclose(stream);
    return 0;
}
```

- 파일을 읽고 수정할 때는 fscanf와 fprintf를 이용하면 된다.

```
#include <stdio.h>

int main() {
    FILE* stream = fopen("hello.txt", "r+");
    char buf[101];
    fscanf(stream, "%s", buf);
    fprintf(stream, "%s", buf);
    fprintf(stream, "%s", buf);
    fprintf(stream, "%s", buf);
    fprintf(stream, "%s", buf);
    fclose(stream);
    return 0;
}
```
- 라이브러리 함수는 여러 번 함수를 호출해도 파일 구조체 내부 버퍼에 수정 사항을 담아 두었다가 한 번에 시스템 함수를 호출한다.
- 따라서, 잦은 함수 호출에는 시스템 함수보다 빠르다.
