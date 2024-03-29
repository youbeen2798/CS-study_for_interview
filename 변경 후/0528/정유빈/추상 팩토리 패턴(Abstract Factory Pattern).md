<h1> 추상 팩토리 패턴(Abstract Factory Pattern) </h1>

- 추상 팩토리 패턴은 이름만 봐서는 팩토리 메소드 패턴과 비슷해보이지만, 명확한 차이가 있다.

<h3> 팩토리 메소드 패턴 </h3>

 - 조건에 따른 객체 생성은 팩토리 클래스로 위임하여, 팩토리 클래스에서 객체를 생성하는 패턴

<h3> 추상 팩토리 패턴 </h3>

- 서로 관련이 있는 객체들을 통째로 묶어서 팩토리 클래스 만들고, 이들 팩토리를 조건에 따라 생성하도록 다시 팩토리를 만들어서 객체를 생성하는 패턴
- 즉, 서로 관련 있는 여러 객체를 만들어주는 인터페이스를 제공하는 패턴
- 추상 팩토리 패턴은, 팩토리 메소드 패턴을 좀 더 캡슐화한 방식

- 예를 들어, 컴퓨터를 생산하는 공장이 있을 때, 마우스, 키보드, 모니터의 제조사로 Samsung과 LG가 있다고 가정
- 컴퓨터를 생산할 때, 전부 삼성으로 만들거나, LG로 만들어야 한다.
- 즉, 객체를 일관적으로 생산할 필요가 있다.
- 코드 레벨에서 본다면, SamsungComputer인지 LGComputer인지 조건에 따라 분기될 것이기 때문에 팩토리 메소드 패턴과 같이, 조건에 따라 객체를 생성할 부분을 Factory 클래스로 정의한다.

<h1> 추상 팩토리 패턴 이유 - 팩토리 메소드 패턴을 사용할 경우 문제 </h1>

![image](https://github.com/youbeen2798/CS-study_for_interview/assets/62228401/76e752f3-2174-469e-b880-8c24ff2d87a0)

1) 먼저 키보드 관련 클래스를 정의한다.

- LGKeyboard와 SamsungKeyboard 클래스를 정의하고, 이를 캡슐화하는 keyboard 인터페이스를 정의한다.
- 그리고 KeyboardFactory 클래스에서 입력값에 따라 LGKeyboard를 생성할지, SamsungKeyboard를 생성할지 결정합니다.

```
public class LGKeyboard implements Keyboard {
    public LGKeyboard(){
        System.out.println("LG 키보드 생성");
    }
}
```

```
public class SamsungKeyboard implements Keyboard {
    public SamsungKeyboard(){
        System.out.println("Samsung 키보드 생성");
    }
}
```

```
public interface Keyboard {
}
```

```
public class KeyboardFactory {
    public Keyboard createKeyboard(String type){
        Keyboard keyboard = null;
        switch (type){
            case "LG":
                keyboard = new LGKeyboard();
                break;

            case "Samsung":
                keyboard = new SamsungKeyboard();
                break;
        }

        return keyboard;
    }
}
```

2) Keyboard와 동일하게 Mouse 관련 클래스들을 정의한다.

```
public class LGMouse implements Mouse {
    public LGMouse(){
        System.out.println("LG 마우스 생성");
    }
}
```

```
public class SamsungMouse implements Mouse {
    public SamsungMouse(){
        System.out.println("Samsung 마우스 생성");
    }
}
```

```
public class MouseFactory {
    public Mouse createMouse(String type){
        Mouse mouse = null;
        switch (type){
            case "LG":
                mouse = new LGMouse();
                break;

            case "Samsung":
                mouse = new SamsungMouse();
                break;
        }

        return mouse;
    }
}
```

3) 다음으로 ComputerFactory 클래스를 구현한다.
- ComputerFactory 클래스는 keybaordFactory와 MouseFactory 객체를 생성해서 어떤 제조사의 키보드 마우스를 생산할 것인지 결정합니다.

```
public class ComputerFactory {
    public void createComputer(String type){
        KeyboardFactory keyboardFactory = new KeyboardFactory();
        MouseFactory mouseFactory = new MouseFactory();

        keyboardFactory.createKeyboard(type);
        mouseFactory.createMouse(type);
        System.out.println("--- " + type + " 컴퓨터 완성 ---");
    }
}
```

4) 마지막으로 컴퓨터를 생산하기 위한 Client 클래스를 구현한다.

```
public class Client {
    public static void main(String args[]){
        ComputerFactory computerFactory = new ComputerFactory();
        computerFactory.createComputer("LG");
    }
}
```

- 팩토리 메소드 패턴을 사용하여 컴퓨터를 생산해보았다.
- 그런데 컴퓨터 구성품은 키보드, 마우스, 모니터 등 여러 가지가 있다.

```
public class ComputerFactory {
    public void createComputer(String type){
        KeyboardFactory keyboardFactory = new KeyboardFactory();
        MouseFactory mouseFactory = new MouseFactory();
        BodyFactory bodyFactory = new BodyFactory();
        MonitorFactory monitorFactory = new MonitorFactory();
        SpeakerFactory speakerFactory = new SpeakerFactory();
        PrinterFactory printerFactory = new PrinterFactory();

        keyboardFactory.createKeyboard(type);
      
      mouseFactory.createMouse(type);
        bodyFactory.createBody(type);
        monitorFactory.createMonitor(type);
        speakerFactory.createSpeaker(type);
        printerFactory.createPrinter(type);
        System.out.println("--- " + type + " 컴퓨터 완성 ---");
    }
}
```

- 그런데 사실 Samsung 컴퓨터라면 모든 구성품이 Samsung이어야 하고, LG라면 모든 구성품이 LG여야 한다.
- 따라서, 추상 팩토리를 사용하여 구성품이 모두 동일한 제조사가 되기 위해서는, "추상 팩토리 패턴"을 사용해야 한다.


2) 추상 팩토리 패턴 적용

![image](https://github.com/youbeen2798/CS-study_for_interview/assets/62228401/c1c7176e-c38f-41c9-b987-8c30adad78e1)

- 패턴 적용 전과 비교했을 때 차이점은 다음과 같다.

- 어떤 제조사의 부품을 선택할지 결정하는 팩토리 클래스(KeyboardFactory, MouseFactory)가 제거되고, Computer Factory 클래스가 추가되었습니다.(SamsungComputerFactory, LGComputerFactory)
- SamsungComputerFactory, LGComputerFactory는 ComputerFactory 인터페이스로 캡슐화하고, 어떤 제조사의 부품을 생성할지 명확하므로, 각각의 제조사 부품을 생성한다.
- FactoryOfComputerFactory 클래스에서 컴퓨터를 생산하는 createComputer() 메소드를 호출한다.

- 먼저 SamsungComputerFactory, SamsungKeyboard, Mouse, LGMouse, SamsungMouse 클래스는 이전 코드와 동일하다.

1) 먼저 SamsungComputerFactory, LGComputerFactory 클래스를 정의하고, 이들을 캡슐화하는 ComputerFactory 인터페이스를 정의한다.
- 각 클래스는 자신의 제조사 부품 객체를 생성한다.
- 예를 들어, SamsungComputerFactory 클래스는 삼성 키보드, 마우스를 가지므로 SamsungKeyboard, SamsungMouse 객체를 생성한다.

```
public class SamsungComputerFactory implements ComputerFactory {
    public SamsungKeyboard createKeyboard() {
        return new SamsungKeyboard();
    }

    public SamsungMouse createMouse() {
        return new SamsungMouse();
    }
}
```

```
public class LGComputerFactory implements ComputerFactory {
    public LGKeyboard createKeyboard() {
        return new LGKeyboard();
    }

    public LGMouse createMouse() {
        return new LGMouse();
    }
}
```
```
public interface ComputerFactory {
    public Keyboard createKeyboard();
    public Mouse createMouse();
}
```

2) 다음으로 FactoryOfComputerFactory 클래스를 정의한다.
- 이 클래스는 패턴 적용 전 ComputerFactory 클래스와 하는 일이 같다.
- 입력 값에 따라 객체 생성을 분기하며, 이 때 어떤 제조사 객체를 생성할지 결정한다.
- 즉, 부품이 아니라 컴퓨터 객체를 생성한다는 점에서 차이점이 있다.

```
public class FactoryOfComputerFactory {
    public void createComputer(String type){
        ComputerFactory computerFactory= null;
        switch (type){
            case "LG":
                computerFactory = new LGComputerFactory();
                break;

            case "Samsung":
                computerFactory = new SamsungComputerFactory();
                break;
        }

        computerFactory.createKeyboard();
        computerFactory.createMouse();
    }
}
```

3) 마지막으로 컴퓨터를 생산하기 위한 Client 클래스를 정의한다.

```
public class Client {
    public static void main(String args[]){
        FactoryOfComputerFactory factoryOfComputerFactory = new FactoryOfComputerFactory();
        factoryOfComputerFactory.createComputer("LG");
    }
}
```


<h1> 정리 </h1>

- 팩토리 메소드 패턴은 구성품마다 팩토리를 만들어서 어떤 객체를 형성했는데, 그 객체의 구성품은 일정하므로, 추상 팩토리 패턴을 적용하여 관련된 객체들을 한 꺼번에 캡슐화하여 팩토리로 만들어서 일관되게 객체를 생성하도록 한다.














