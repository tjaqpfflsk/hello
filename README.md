# 1.String 클래스 에서 문자열 비교시 equal을 쓰는 이유는?
 - equals 는 원래 주소를 비교하는데 String 클래스는 내용 비교를 하는 형태로 equals 메소드를 오버라이딩 하고 있어서
문자열 비교시 사용한다.

# 2.shall copy, deep copy 의 차이는?
* Shall Copy
 : 복사 받는 객체의 주소 값까지만 복사가 되므로 갗은 객체의 주소를 가지고 있어서 객체 안의 값이 변하면
같이 값이 변하게 되는 것이다.
'''java
@Override
public Object clone() throws CloneNotSupportedException {
return super.clone();
}
'''
* Deep Copy
 : 객체의 주소만 복사하는 것이 아니라 값도 복사하여 따로 저장하기 때문에 복사받은 객체 값이 변하여도 변하지 않는다.
 '''java
public Object clone() throws CloneNotSupportedException {
Rectangle copy = (Rectangle)super.clone();
copy.upperLeft = (Point)upperLeft.clone();
copy.lowerRight = (Point)lowerRight.clone();
return copy;
}
'''
# 3.금일 배운 Rectangle의 shall copy 와 deep copy 일때의 그림을 그리시오.(중요)


# 4.다음 main()이 실행되면 아래 예시와 같이 출력되도록 MyPoint 클래스를 작성하라.
 '''java
public static void main(String [] args) {
	MyPoint p = new MyPoint(3, 50);
	MyPoint q = new MyPoint(4, 50);
	System.out.println(p);
	if(p.equals(q)) System.out.println("같은 점");
	else System.out.println("다른 점");			
}

Point(3,50)
다른점
'''
 '''java
class MyPoint{
	private int x;
	private int y;
	public MyPoint(int x, int y) {
		this.x = x;
		this.y = y;
	}
	public String toString(){
		return "Point(" + x + ","+ y +")";
	}
}
public class PointMain {
	public static void main(String[] args) {
		MyPoint p = new MyPoint(3, 50);
		MyPoint q = new MyPoint(4, 50);
		System.out.println(p);
		if(p.equals(q)) System.out.println("같은 점");
		else System.out.println("다른 점");		
	}
}
'''

# 5.중심을 나타내는 정수 x, y와 반지름 radius 필드를 가지는 Circle 클래스를 작성하고자 한다. 
생성자는 3개의 인자(x, y, raidus)를 받아 해당 필드를 초기화하고, 
equals() 메소드는 두 개의 Circle 객체의 중심이 같으면 같은 것으로 판별하도록 한다.
 '''java
public static void main(String[] args) {
	Circle a = new Circle(2, 3, 5); // 중심 (2, 3)에 반지름 5인 원
	Circle b = new Circle(2, 3, 30); // 중심 (2, 3)에 반지름 30인 원
	System.out.println("원 a : " + a);
	System.out.println("원 b : " + b);
	if(a.equals(b))
		System.out.println("같은 원");
	else 
		System.out.println("서로 다른 원");
}

원 a : Circle(2,3)반지름5
원 b : Circle(2,3)반지름30
같은 원
'''
 '''java
class Circle {
	private int x;
	private int y;
	private int radius;

	public Circle(int x, int y, int radius) {
		this.x = x;
		this.y = y;
		this.radius = radius;
	}

	@Override
	public boolean equals(Object obj) {
		if (this.x == ((Circle) obj).x && this.y == ((Circle) obj).y) {
			return true;
		}
		else
			return false;
	}
	@Override
	public String toString() {
		return "Circle("+x+","+y+")반지름"+radius;
	}
}

public class CircleMain {

	public static void main(String[] args) {
		Circle a = new Circle(2, 3, 5); // 중심 (2, 3)에 반지름 5인 원
		Circle b = new Circle(2, 3, 30); // 중심 (2, 3)에 반지름 30인 원
		System.out.println("원 a : " + a);
		System.out.println("원 b : " + b);
		if (a.equals(b))
			System.out.println("같은 원");
		else
			System.out.println("서로 다른 원");

	}

}
'''

# 6.문자열을 입력받아 한 글자씩 회전시켜 모두 출력하는 프로그램을 작성하라.
(클래스로 작성할 필요없이 메인에서 직접 할것)

문자열을 입력하세요. 빈칸이나 있어도 되고 영어 한글 모두 됩니다.
I Love you
 Love youI
Love youI 
ove youI L
ve youI Lo
e youI Lov
 youI Love
youI Love 
ouI Love y
uI Love yo
I Love you
[Hint] Scanner.nextLine()을 이용하면 빈칸을 포함하여 한 번에 한 줄을 읽을 수 있다.
 '''java
import java.util.Scanner;

public class LoveMain {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("문자열을 입력하세요. 빈칸이나 있어도 되고 영어 한글 모두 됩니다.");
		String words = sc.nextLine();
		String firstWords = words;
		while (true) {
			String first = words.substring(0, 1);
			words = words.substring(1);
			words = words.concat(first);
			System.out.println(words);
			if (firstWords.compareToIgnoreCase(words) == 0) {
				break;
			}
		}
		sc.close();
	}
}
'''

# 7.래퍼 클래스란 무엇인가?
 자바는 객체 지향 언어이므로 자료형을 객체로 다루기 위해서 사용되는 것을 말하며
 기본 자료형의 값을 인스턴스로 감싼다고 하여 래퍼 클래스라 한다 .
- java.lang.Number
 : 모든 래퍼 클래스가 상속하는 클래스

- 래퍼 클래스의 종류와 생성자
 '''java
Boolean public Boolean(boolean value)
Character public Character(char value)
Byte public Byte(byte value)
Short public Short(short value)
Integer public Integer(int value)
Long public Long(long value)
Float public Float(float value), public Float(double value)
Double public Double(double value)
'''

# 8.auto unboxing 이란?
객체에 기본 자료형 값을 대입하는 것이 오토 박싱인데 컴파일러가 찾아서 자동으로 new 해서 객체를 생성해준다. 
이 반대로 기본형 변수에다가 객체의 값을 넣어주는 것을 말한다. 
Integer iObj = 10;// 오토 박싱 진행
int num1 = iObj; // 오토 언박싱 진행

# 9. 다음 조건을 만족하는 클래스 Person을 구현하여 테스트하는 프로그램을 작성하시오.(필수)

- 클래스 Person은 이름을 저장하는 필드 구성

- 클래스 Person은 상위 클래스 Object의 메소드 equals()를 오버라이딩하여 이름이 같으면 true를 반환하는 메소드 구현

- 다음과 같은 소스로 클래스 Person을 점검

Person p1 = new Person("홍길동");
System.out.println(p1.equals(new Person("홍길동")));
System.out.println(p1.equals(new Person("최명태")));

 '''java
class Person {
	String name;

	public Person(String name) {
		this.name = name;
	}

	@Override
	public boolean equals(Object obj) {
		if (this.name == (((Person) obj).name))
			return true;
		else
			return false;
	}
}

public class PersonMain {

	public static void main(String[] args) {
		Person p1 = new Person("홍길동");
		System.out.println(p1.equals(new Person("홍길동")));
		System.out.println(p1.equals(new Person("최명태")));

	}

}
'''

# 10. 다음 조건을 만족하는 클래스 String의 객체 이용 프로그램을 작성하여
 메소드 equals()와 연산자 ==의 차이를 비교 설명하시오.(필수) 

- 메소드 equals()와 비교 연산자 ==의 차이를 다음 소스로 점검
 '''java
String s1 = new String("java");
String s2 = new String("java");
String s3 = s2;

System.out.println(s1 == s2);
System.out.println(s1.equals(s2));
System.out.println(s2 == s3);
System.out.println(s2.equals(s3));

이 코딩의 결과 값 : 
false
true
true
true
'''
== 둘이 같냐는 의미의 연산자인데 String은 안에 주소 값을 가지고 있으므로 둘의 주소 값을 비교하게 된다.
하지만  equals 는 원래 주소를 비교하는데 String 클래스에서 내용 비교를 하는 형태로 equals 메소드를 오버라이딩 하고 있어서
문자열이 비교된다.


# 11. 다음 조건을 만족하도록 오늘의 정보를 출력하는 프로그램을 작성하시오.

- 클래스 Calendar의 객체의 다음 메소드를 사용하며

 * get(Calendar.DAY_OF_WEEK_IN_MONTH) : 달에서 요일의 횟수 반환
 * get(Calendar.DAY_OF_WEEK) : 요일을 반환, 1이 일요일
 * get(Calendar.WEEK_OF_MONTH) : 월의 주 횟수를 반환
 * get(Calendar.DAY_OF_YEAR) : 해의 날짜를 반환
 * get(Calendar.WEEK_OF_YEAR) : 해의 주 횟수를 반환

- 다음과 같이 출력되도록 한다.

오늘은 2012년 6월 17일 일요일입니다.
이 달의 3번째 일요일입니다.
이 달의 4번째 주입니다.
이 해의 169일입니다.
이 해의 25번째 주입니다. 
 '''java
import java.util.Calendar;

public class CalendarMain {
	public static void main(String[] args) {

		Calendar cal = Calendar.getInstance();
		// 왜 이렇게 되는지 모르겠다. 캘린더를 상속 받는 클래스를 만들려고 했으나 실패!!
		String day = "";
		int a = cal.get(Calendar.DAY_OF_WEEK);
		switch (a) {
		case (1):
			day = "일";
			break;
		case (2):
			day = "월";
			break;
		case (3):
			day = "화";
			break;
		case (4):
			day = "수";
			break;
		case (5):
			day = "목";
			break;
		case (6):
			day = "금";
			break;
		case (7):
			day = "토";
			break;
		}

		int year = cal.get(Calendar.YEAR);
		int month = cal.get(Calendar.MONTH);
		int date = cal.get(Calendar.DATE);
		System.out.println("오늘은 " + year + "년 " + month + "월 " + date + "일 " + day + "입니다.");
		System.out.println("이 달의 "+cal.get(Calendar.DAY_OF_WEEK_IN_MONTH)+"번째 "+day+"입니다.");
		System.out.println("이 달의 "+cal.get(Calendar.WEEK_OF_MONTH)+"번째 주입니다.");
		System.out.println("이 해의 "+cal.get(Calendar.DAY_OF_YEAR)+"일입니다.");
		System.out.println("이 해의 "+cal.get(Calendar.WEEK_OF_YEAR)+"번째 주입니다." );

	}
}
'''
