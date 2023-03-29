Q. 문장 입력 후 가장 길이가 긴 단어 찾기 + 가장 긴 단어가 여러개일 경우 앞쪽에 위치한 단어를 답으로 

📌 1번 .split(); 활용하는 방법

- 조심!!! >= 으로 하면 안됨. why? 같은 길이면 먼저 나온 단어가 답이라고 했으니

```java
import java.util.Scanner;
class Main{
    public String solution(String str) {
        String answer = "";
        int m = Integer.MIN_VALUE;
        //가장 작은 값으로 초기화됨, 최대값으로 계속 갱신할거니까 처음에는 제일 작은 값으로! max 줄임말
        String[] s = str.split(" ");
        //띄어쓰기로 구분할거니까 .split();에서 공백넣어줘서 공백으로 구분
        for(String x : s){
            int len = x.length(); 
            if(len>m){   // 📌조심!!! >= 으로 하면 안됨. why? 같은 길이면 먼저 나온 단어가 답이라고 했으니
                m=len;    //최대값이 m으로 계속 갱신
                answer=x; //최대값이 발견될 때마다 answer 갱신
            }
        }
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner sc = new Scanner(System.in);
        String str = sc.nextLine();  //한줄로 입력 받아야하니 nextLine();
        System.out.print(T.solution(str));
    }
}
```

📌 2번 .indexOf();

같은 연산자(**`==`**)는 두 피연산자의 값이 같으면 반환 **`true`**하고, 그렇지 않으면 반환됩니다 **`false`**

같지 않은 연산자(**`!=`**)는 피연산자에 동일한 값이 없으면 반환 **`true`**
 하고, 그렇지 않으면 반환됩니다 **`false`**

❗❗❗❗❗indexOf() 메서드는 존재하지 않으면 -1을 반환합니다.

📢

 while((pos = str.indexOf(' ')) != -1)

따라서 이런 조건식이 가능한 것. 공백이 있으면 true가 되고  pos에 넣고 

없으면 -1이 되니 조건식 종료

```java
import java.util.Scanner;

//Q. 문장에서 제일 긴 단어 찾기
class Main{
    public String solution(String str) {
        String answer = "";
        int m = Integer.MIN_VALUE, pos;  //int a=5, b; 이런 느낌분리자를 활용해서 a,b를 한번에 선언
        while((pos = str.indexOf(' ')) != -1){
        //공백 위치를 리턴해줌 ! 만약 발견 못하면 -1 리턴하고 while문 종료
				//❗❗indexOf() 메서드는 존재하지 않으면 -1을 반환합니다.
            String tmp = str.substring(0,pos); //pos는 공백 시작점이고, .substirng의 끝부분은 n-1이니 딱임
            int len = tmp.length();  //잘라낸 단어 길이
            if(len > m) {   // 조심!!! >= 으로 하면 안됨. why? 같은 길이면 먼저 나온 단어가 답이라고 했으니
                m = len;
                answer = tmp;  //이렇게 하면 계속 갱신함
            }
            str=str.substring(pos+1);  //다시 앞단어빼고 그 이후부터를 str 설정해서 while문 시작
                                                //마지막 단어로 가면 이제 위로 올라갔을 때 공백이 없으니 -1 돼서 끝나버림
                                                //따라서 마지막 단어일 경우 tmp에 못들어가니 그 처리가 필요함
        }
        if(str.length() > m ) answer = str;  //indexOf(); 쓰려면 이렇게 마지막 단어 처리 꼭 필요함
                                            //공백 없어서 -1리턴하고 while문 끝낸 이 마지막 단어 str이 m보다 크면 answer에 넣어주고 아님 말고
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner sc = new Scanner(System.in);
        String str = sc.nextLine();  //한줄로 입력 받아야하니 nextLine();
        System.out.print(T.solution(str));
    }
}
```
