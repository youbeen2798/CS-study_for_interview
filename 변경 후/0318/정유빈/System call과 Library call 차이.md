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

- 대부분의 프로그램은 User Mode에서 실행됩니다.
- 프로그램에 메모리나 하드웨어 리소스가 필요한 경우 System call을 사용하여 커널에 요청을 보냅니다.
- 그런 다음 모드가 User 모드에서 Kernal 모드로 전환되고, 작업이 끝나면 Kernal 모드에서 User 모드로 다시 전환됩니다.
- 이러한 모드 전환을 Context Switcing이라고 합니다.
<br />
UNIX 시스템에서 두 가지 System call 예를 들어 보겠습니다. <br />
- fork()
  - 기존 프로세스를 유지하면서 새 프로세스를 작성하는데 사용됩니다.
  - 특정 프로세스가 fork()를 호출하면 프로세스의 사본이 작성됩니다.
  - 따라서 두 가지 프로세스가 있습니다.
  - 하나는 Parent 프로세스이고, 작성된 새 프로세스는 Child 프로세스입니다.

- exec()
  - 새 프로세스를 작성하고 종료 프로세스를 새 프로레스로 바꿉니다.
  - 
