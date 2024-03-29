# 10장 | 클래스

### 📃 클래스 체계

**표준 자바 관례**  
순차적으로 내려가는 추상화 단계
1. static, public 상수
2. private 변수
3. private 인스턴스 변수
4. public 함수
5. private 함수

**캡슐화**
- 변수와 유틸리티 함수는 가능한 private으로 하는 것이 낫다.
- 캡슐화를 풀어주는 결정은 언제나 최후의 수단이다.

##

### 📃 클래스는 작아야 한다!

> 클래스를 만들 때 첫 번째 규칙은 '작게'다.  
얼마나 작아야 하는가? '하나'를 책임져야 한다.

- 클래스가 맡은 **책임**을 최소화하라.
- 클래스 이름은 해당 클래스의 책임을 기술해야 한다.  
  → 간결한 이름이 떠오르지 않는다면 클래스 크기가 너무 커서 그렇다.  
  → 클래스 이름이 모호하다면 클래스 책임이 너무 많아서 그렇다.  
  ex) Processor, Manager, Super와 같이 모호한 단어는 여러 책임을 떠안았다는 표시다.  
  ex) 만일(if), 그리고(and), 하며(or), 하지만(but)을 사용하지 않고 가능해야 한다.
- 클래스가 맡은 책임을 클래스 이름에 간결하게 표현할 수 있어야 한다.
- 큰 클래스 몇 개가 아닌 작은 클래스 여럿으로 이루어진 시스템이 더 바람직하다.
- 메소드 개수가 적다고 책임이 적은 것이 아니다.

##

### 📃 **단일 책임 원칙 (SRP: Single Responsibility Principle)**

> 클래스나 모듈을 변경할 이유가 단 하나뿐이어야 한다.  
**책임**, 즉 *변경할 이유* 가 하나여야 한다.

만능 클래스를 **단일 책임 클래스 여럿**으로 분리해야 한다.  
규모가 어느 수준에 이르는 시스템은 논리가 많고도 복잡하다. 이런 복잡성을 다루려면 체계적인 정리가 필수다.  
큼직한 다목적 클래스 몇 개로 이뤄진 시스템은 변경을 가할 때 당장 알 필요가 없는 사실까지 들이민다.

- 큰 클래스 몇 개가 아니라 작은 클래스 여럿으로 이뤄진 시스템이 더 바람직하다.
- 작은 클래스는 각자 맡은 책임이 하나이며, 변경할 이유가 하나이다.
- 작은 클래스는 다른 작은 클래스와 협력해 시스템에 필요한 동작을 수행한다.

##

### 📃 응집도 (Cohesion)

> 몇몇 메서드 만이 사용하는 인스턴스 변수가 많다 → 새로운 클래스로 쪼개야 한다는 신호다.

메서드가 클래스 인스턴스 변수를 더 많이 사용할수록 메서드와 클래스는 응집도가 높다.  
모든 인스턴스 변수를 메서드마다 사용하는 클래스는 응집도가 가장 높다.  
응집도가 높다는 말은 클래스에 속한 메서드와 변수가 서로 의존하며 논리적인 단위로 묶인다는 의미다.

***응집도를 유지하면 작은 클래스 여럿이 나온다***
- 변수가 아주 많은 큰 함수 일부를 작은 함수 하나로 빼내려고 하는데, 빼내려는 코드가 큰 함수에 정의된 변수 넷을 사용한다.  
  잘못된 방법) 변수 넷을 새 함수에 인수로 옮긴다.  
  옳은 방법) 네 변수를 **클래스 인스턴스 변수로 승격한다.** 새 함수는 인수가 필요없다.
- 이렇게 하면 클래스가 응집력을 잃는다. 몇몇 함수만 사용하는 인스턴스 변수가 점점 더 늘어난다.
- 몇몇 함수가 몇몇 변수만 사용한다? → **독자적인 클래스로 분리한다.**

> 클래스가 응집력을 잃는다면 쪼개라!
> 
> ##

### 📃 리팩터링

- 리팩터링한 프로그램은 좀 더 길고 서술적인 변수 이름을 사용한다.
- 리팩터링한 프로그램은 코드에 주석을 추가하는 수단으로 함수 선언과 클래스 선언을 활용한다.
- 가독성을 높이고자 공백을 추가하고 형식을 맞추었다.

**방법**

1. 원래 프로그램의 정확한 동작을 검증하는 테스트 슈트를 작성한다.
2. 한 번에 하나씩 수 차례에 걸쳐 조금씩 코드를 변경한다.
3. 코드를 변경할 때마다 테스트를 수행해 원래 프로그램과 동일하게 동작하는지 확인한다.
4. 조금씩원래 프로그램을 정리해 최종 프로그램을 얻는다.

##

### 📃 변경하기 쉬운 클래스

> 이상적인 시스템이라면 새 기능을 추가할 때 시스템을 확장할 뿐 기존 코드를 변경하지 않는다.

OCP(Open-Closed Principle): 클래스는 확장에 개방적이고 수정에 폐쇄적이어야 한다.  
새 기능을 수정하거나 기존 기능을 변경할 때 건드릴 코드가 최소인 시스템 구조가 바람직하다.

***변경으로부터의 격리***
- 인터페이스와 추상 클래스를 사용해 구현이 미치는 영향을 격리하라.
- 상세한 구현에 의존하지 않도록 시스템 결합도를 낮춰라.
- 추상화된 인터페이스에 의존하도록 해서 실제 작동하는 방식 등의 구체적인 사실을 모두 캡슐화하라.