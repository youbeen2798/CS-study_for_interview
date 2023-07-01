<h1> IPC(Inter Process Communication) </h1>

- 프로세스 간에 통신하여 상호 커뮤니케이션 하는 기법
- 프로세스끼리 직접적으로 "대화"하는 방법은 없다.
- 왜냐하면, 프로세스들이 서로 공간을 쉽게 접근하면 프로세스의 데이터나 코드가 다른 프로세스에 의해 쉽게 바뀔 수 있기 때문이다.

<h3> 통신(커뮤니케이션)이 필요한 이유?</h3>

- 성능을 높이기 위해
- 로직을 수행하는 과정에서 필요한 데이터들을 서로 공유하기 위해서

<h3> IPC 종류 </h3>

<b> 1. File 사용 </b>

- 텍스트 파일 txt(혹은 다른 포멧의 파일)을 통해 데이터를 주고 받는 것도 IPC 기법 중 하나
- 그러나 이 방법은 문제가 많다.
- 이 방식은 실시간으로 직접 원하는 프로세스에 데이터를 전달하는게 어렵다.
- 디스크에서 데이터 파일을 읽고 프로세스에 적재(load) 되는 과정에서 Context Switcing(컨텍스트 스위칭), Interrupt(인터럽트) 등 여러 일을 처리해야 하기 때문이다.

<b> 2. 파이프(Pipe) </b>

![image](https://github.com/youbeen2798/CS-study_for_interview/assets/62228401/815fca05-dae0-4bbe-af89-1a237eaaf551)

- 단방향 통신, 즉 부모 프로세스 -> 자식 프로세스에게 일방적으로 통신하는 기법
- fork()를 통해 자식 프로세스를 만들고 나서 부모의 데이터를 자식에게 보낸다.

```
char* msg = "Hello Child Process";
int main()
{
	char buf[255];
	int fd[2], pid, nbytes;
	if(pipe(fd) < 0) 						// pipe(fd)로 파이프 생성
		exit(1);
	pid = fork(); 							// 이 함수 실행 다음 코드부터 부모/자식 프로세스로 나눠짐
	if(pid > 0){ 							// 부모 프로세스는 pid에 실제 프로세스 ID가 들어감
		write(fd[1], msg, MSGSIZE); 		// fd[1]에 씀(write 파일 디스크립터)
	} else{ 								// 자식 프로세스는 pid가 0이 들어감
		nbytes = read(fd[0], buf, MSGSIZE); // fd[0]으로 읽음(read 파일 디스크립터)
		printf("%d %s\n", nbytes, buf);
		exit(0);
	}
	return 0;
}
```

<b> 메시지큐(Message Queue) </b>

- FIFO 정책으로 데이터가 전송되는 기법이다.

```
// A 프로세스
// key는 1234(예), msgflg는 옵션
msqid = msgget(key, msgflg);
msgsnd(msqid, &buf, buf_length, IPC_NOWAIT);

// B 프로세스
// key는 A에서 지정한 것과 동일하게 해야 해당 큐의 msqid를 얻을 수 있어요.
msqid = msgget(key, msgflg);
msgrcv(msqid, &rbuf, MSGSZ, 1, 0);
```

- msgget(key, msgflg) : key 값의 메시지 큐를 가져온다.
- msgsnd(msqid, &buf, buf_length, IPC_NOWAIT) : msgget의 ID를 통해 얻은 메시지 큐 ID에 버퍼를 push한다.
- msgrcv(msqid, &rbuf, MSGSZ, 1, 0) : msgget의 ID를 통해 얻은 메시지 큐 ID에 버퍼를 push한다.

<b> 파이프 VS 메시지 큐 </b>

- 파이프는 부모 - 자식 간 통신만 가능하지만 메시지 큐는 어떤 프로세스 간이라도 통신이 가능하다.
- 즉, 단방향과 양방향의 차이가 있다.

<b> 4. 공유 메모리 </b>
