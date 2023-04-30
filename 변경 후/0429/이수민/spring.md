# Spring VS SpringBoot

- 자바 생태계에서 가장 대중적인 응용프로그램 개발 프레임워크
- 의존성 주입(DI, Dependency Injection)과 제어의 역전(IOC, Inversion Of Control)은 스프링의 가장 중요한 특징
- 이들로 인해 결합도를 낮추는 방식으로 어플리케이션을 개발할 수 있음

@Component

스프링의 BeanFactory라는 팩토리 패턴의 구현체에서 bean이라는 스프링프레임워크가 관리하는 객체가 있는데 해당 클래스를 그러한 bean 객체로 두어 스프링 관리하에 두겠다는 어노테이션

@Autowired

스프링 프레임워크에서 관리하는 bean 객체와 같은 타입의 객체를 찾아서 자동으로 주입해주는 것

해당 객체를 bean으로 등록하지 않으면 주입해줄 수 없음

즉 필요한 의존 객체의 “타입”에 해당하는 빈을 찾아 주입

- 생성자
- setter
- 필드

이 3가지 경우에 Autowired 사용 

Autowired는 기본값이 true이기 때문에 의존성 주입을 할 대상을 차지 못한다면 애플리케이션 구동에 실패한다.

Spring 프레임워크는 웹 어플리케이션을 개발하는데 결합도를 낮추는 방향의 개발방법을 제공 

→ Spring 의 컨셉(Dispatcher Servlet, ModelAndView, Vier Resolver) 덕에 쉬운 개발 함

—> Spring은 많은 기능을 제공하지만 설정하는데 많은 시간이 든다. 심지어 최소한의 기능으로 mvc를 사용하여 기본 프로젝트 셋팅하는데 많은 시간이 걸림

SpringBoot는 자동설정(AutoConfiguration)을 이용하였고 어플리케이션 개발에 필요한 모든 내부 디펜던시를 관리 

→ 개발자가 해야하는건 단지 어플리케이션 실행 

→ 스프링부트는 미리설정된 스타터 프로젝트를 제공
