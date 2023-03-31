**교육과정 설계**

설명

현수는 1년 과정의 수업계획을 짜야 합니다.

수업중에는 필수과목이 있습니다. 이 필수과목은 반드시 이수해야 하며, 그 순서도 정해져 있습니다.

만약 총 과목이 A, B, C, D, E, F, G가 있고, 여기서 필수과목이 CBA로 주어지면 필수과목은 C, B, A과목이며 이 순서대로 꼭 수업계획을 짜야 합니다.

여기서 순서란 B과목은 C과목을 이수한 후에 들어야 하고, A과목은 C와 B를 이수한 후에 들어야 한다는 것입니다.

현수가 C, B, D, A, G, E로 수업계획을 짜면 제대로 된 설계이지만

C, G, E, A, D, B 순서로 짰다면 잘 못 설계된 수업계획이 됩니다.

수업계획은 그 순서대로 앞에 수업이 이수되면 다음 수업을 시작하다는 것으로 해석합니다.

수업계획서상의 각 과목은 무조건 이수된다고 가정합니다.

필수과목순서가 주어지면 현수가 짠 N개의 수업설계가 잘된 것이면 “YES", 잘못된 것이면 ”NO“를 출력하는 프로그램을 작성하세요.

입력

첫 줄에 한 줄에 필수과목의 순서가 주어집니다. 모든 과목은 영문 대문자입니다.

두 번 째 줄부터 현수가 짠 수업설계가 주어집니다.(수업설계의 길이는 30이하이다)

출력

첫 줄에 수업설계가 잘된 것이면 “YES", 잘못된 것이면 ”NO“를 출력합니다.

예시 입력 1

```
CBA
CBDAGE

```

예시 출력 1

```
YES
```

📌Queue는 링크드리스트 ([https://github.com/wjdrbs96/Today-I-Learn/blob/master/Java/Collection/Queue/Queue가 ArrayList대신 LinkedList 사용하는 이유.md](https://github.com/wjdrbs96/Today-I-Learn/blob/master/Java/Collection/Queue/Queue%EA%B0%80%20ArrayList%EB%8C%80%EC%8B%A0%20LinkedList%20%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%20%EC%9D%B4%EC%9C%A0.md))

why? 큐는 항상 첫번째 저장된 데이터 삭제하므로 어레이리스트같은 배열 기반 자료 구조 사용시

빈공간 채우기 위해 데이터 복사가 발생하므로 매우 비효율적

따라서 추가 삭제가 쉬운 링크드리스트로 구현하는 것

필수값인 String n과 주어진값인 String k해서

큐에 n값을 toCharArray로 담고 

다시 foreach문으로 char k를 포함한다면 poll값(필수의맨앞) 과 같은지 확인. 아니면 No

일단 poll은 꺼내는거니까 이렇게 계속 돌리고

다 돌렸는데 필수값이 비어있지않다면 또 No

그외는 Yes

```java
class Main {

  public String solution(String need, String plan) {

    String answer = "YES";
    Queue<Character> Q = new LinkedList<>();
    for (char x : need.toCharArray()) {
      Q.offer(x);
    }
    //이제 Q에는 필수값들이 들어가있을테니 주어진 배열과 비교
    for (char x : plan.toCharArray()) {
      //x가 주어진 배열 돌면서 맨위 Q에 있는 필수값에 있는 문자인지 확인하고
      if (Q.contains(x)) {
        // 필수값 Q에서 맨 앞에 것 꺼냈는데 그게 x와 같지 않다면
        if (x != Q.poll()) {
          //NO!
          return "NO";
        }
      }
    }
    // 다 돌렸는데 필수값이 비어있지 않다면 !  NO!
    if (!Q.isEmpty()) {
      return "NO";
    }

    return answer;
  }

  public static void main(String[] args) {
    Main T = new Main();
    Scanner sc = new Scanner(System.in);
    String n = sc.next();
    String k = sc.next();
    System.out.println(T.solution(n, k));
  }
}
```
