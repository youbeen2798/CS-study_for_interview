<h1> System call과 Library call의 차이 </h1>

- System call과 Library call의 주요 차이점은 System call은 커널에 대한 Resource Acess 요청이고, Library call은 프로그래밍 라이브러리에 정의 된 함수를 사용하라는 요청입니다.
- 운영체제는 응용 프로그램이 하드웨어 리소스에 접근할 수 있도록 하는 Interface입니다.
- 운영체제는 메모리 관리, 프로세스 관리, 데이터 보안 등과 같은 컴퓨터 시스템의 주요 작업을 수행합니다.
- 커널은 이러한 운영 체제의 핵심입니다.
- System call 및 Libaray call은 운영 체제와 관련된 두 가지 용어입니다.
- 커널은 System call을 제공하는 반면 프로그래밍 라이브러리는 Library call을 제공합니다.

<h3> System call </h3>

- 컴퓨터 시스템에는 Kernal 모드와 User 모드 2가지 모드가 있습니다.
- Kernal 모드에서 프로그램은 메모리 및 하드웨어 리소스에 직접 액세스 할 수 있습니다.
- User 모드에서 프로그램은 메모리 및 하드웨어 리소스에 직접 액세스 할 수 없습니다.
