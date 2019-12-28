### 팩토리 메소드(factory method) 패턴
- 기본적으로 팩토리는 공장이란 뜻을 내포하고 있습니다. 따라서 팩토리 메소드 패턴도 무언가를 위한 공장이라고 보면 된다.
> 객체를 만들어내는 부분을 서브 클래스Sub-Class에 위임하는 패턴.

*즉, new 키워드를 호출하는 부분을 서브 클래스에 위임하는 거다. 결국 팩토리 메소드 패턴은 객체를 만들어내는 공장(Factory 객체)을 만드는 패턴이라 이해하면 된다*

~~~ java

public class FactoryMain {
	public static void main(String[] args) {

		RobotFactory rf = new SuperRobotFactory();
		Robot r = rf.createRobot("super");
		Robot r2 = rf.createRobot("power");

		System.out.println(r.getName());
		System.out.println(r2.getName());

		RobotFactory mrf = new ModifiedSuperRobotFactory();
		Robot r3 =  mrf.createRobot("pattern.factory.SuperRobot");
		Robot r4 =  mrf.createRobot("pattern.factory.PowerRobot");

		System.out.println(r3.getName());
		System.out.println(r4.getName());
	}
}
~~~