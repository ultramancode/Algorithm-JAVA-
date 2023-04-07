**후위식 연산(postfix)**

설명

후위연산식이 주어지면 연산한 결과를 출력하는 프로그램을 작성하세요.

만약 3*(5+2)-9 을 후위연산식으로 표현하면 352+*9- 로 표현되며 그 결과는 12입니다.

입력

첫 줄에 후위연산식이 주어집니다. 연산식의 길이는 50을 넘지 않습니다.

식은 1~9의 숫자와 +, -, *, / 연산자로만 이루어진다.

출력

연산한 결과를 출력합니다.

예시 입력 1

```
352+*9-

```

예시 출력 1

```
12
```

📌 .isDigit → char값이 숫자인지 여부 판단하여 true false 리턴

lt rt활용. 먼저 뺀걸rt 나중에 뺀걸 lt로해서 나중에 뺀거로 후위연산

else if로 일일히 연산자들 지정.. for문내에서 돌돌돌

```java
import java.util.Scanner;
import java.util.Stack;

class Main {

  public int solution(String str) {
    int answer = 0;
    Stack<Integer> stack = new Stack<>();
    for (char x : str.toCharArray()) {
      //char 값이 숫자인지 여부 판단하여 true false 리턴
      if (Character.isDigit(x)) {
        stack.push(x - 48); //뒤에서 연산할거니까 숫자로 넣어줘야하는데 48을 빼줘야 숫자화 가능
      } else {
        int rt = stack.pop();
        int lt = stack.pop();
        //'임
        if (x == '+') {
          stack.push(lt + rt);
        }
        //lt에서 rt빼는거임. 나중에 pop한거에서 먼저 pop한걸 빼줌. 후위연산
        else if (x == '-') {
          stack.push(lt - rt);
        } else if (x == '*') {
          stack.push(lt * rt);
        } else if (x == '/') {
          stack.push(lt / rt);
        }
      }
    }
    answer = stack.get(0);
    return answer;
  }

  public static void main(String[] args) {
    Main T = new Main();
    Scanner sc = new Scanner(System.in);
    String str = sc.next();
    System.out.println(T.solution(str));
  }
}
```
