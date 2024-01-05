# 자바의 정석 - Part04 - Chapter18 데이터 입출력

## 18.1 입출력 스트림

- 자바는 입력 스트림과 출력 스트림을 통해 데이터를 입출력한다.
- 스트림 : 데이터가 단방향으로 흐르는 것을 말한다.
- 데이터는 출발지에서 나와 도착지로 흘러 들어간다.
  - `입력 스트림` : 출발지 (키보드, 파일, 프로그램) -> 도착지 (프로그램)
  - `출력 스트림` : 도착지 (모니터, 파일, 프로그램) -> 도착지 (프로그램)
  - 프로그램 기준으로 데이터가 들어오면 `입력 스트림`, 나가면 `출력 스트림`
  - 프로그램이 다른 프로그램과 데이터를 교환하기 위해서는 양쪽 모두 입력 스트림과 출력 스트림이 필요하다.
- 어떤 데이터를 입출력하는지에 따라
  - `바이트 스트림` : 그림, 멀티미디어, 문자 등 모든 종류의 데이터를 입출력할 때 사용
  - `문자 스트림` : 문자만 입출력할 때 사용
- 자바는 데이터 입출력과 관련된 라이브러리를 `java.io` 에서 제공하며 바이트 스트림과 문자 스트림을 다음과 같이 이름으로 구분해서 제공
  - `바이트 스트림`
    - 최상위 클래스
      - `입력 스트림` : InputStream
      - `출력 스트림` : OutputStream
    - 하위 클래스
      - `입력 스트림` : XXXInputStream (ex: FileInputStream)
      - `출력 스트림` : XXXOutputStream (ex: FileOutputStream)
  - `문자 스트림`
    - 최상위 클래스
      - `입력 스트림` : Reader
      - `출력 스트림` : Writer
    - 하위 클래스
      - `입력 스트림` : XXXReader (ex: FileReader)
      - `출력 스트림` : XXXWriter (ex: FileWriter)

## 18.2 바이트 출력 스트림
- `OutputStream은 바이트 출력 스트림의 최상위 클래스로 추상클래스 이다.`
  - 모든 바이트 출력 스트림 클래스는 이 OutputStream 클래스를 상속받아서 만들어진다.
  - `OutputStream` <- (FileOutputStream, PrintStream, BufferedOutputStream, DataOutputStream)
- 메소드
  - void write(int b) : 1byte 출력
  - void write(byte[] b) : 배열 b의 모든 바이트 출력
  - void write(byte[] b, int off, int len) : off부터 len개의 바이트를 출력
  - void flush() : 출력 버퍼에 잔류하는 모든 바이트 출력
  - void close() : 출력 스트림을 닫고 사용 메모리 해제
```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;

public class Main {
    public static void main(String[] args) throws IOException {
        OutputStream os = new FileOutputStream("./test.txt");

        byte a = 'a';
        byte b = 'b';
        byte c = 'c';

        os.write(a);
        os.write(b);
        os.write(c);

        os.flush();
        os.close();
    }
}
```
> 1바이트를 출력하는 경우는 드물고, 보통 바이트 배열을 통째로 출력하는 경우가 많다.
```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;

public class Main {
    public static void main(String[] args) throws IOException {
        OutputStream os = new FileOutputStream("./test.txt");

        byte[] array = {10, 20, 30};

        os.write(array);

        os.flush();
        os.close();
    }
}
```

## 18.2 바이트 입력 스트림
- InputStream <- (FileInputStream, BufferedInputStream, DataInputStream)
- 메소드
  - int read() : 1byte를 읽은 후 읽은 바이트를 리턴
  - int read(byte[] b) : 읽은 바이트를 매개값으로 주어진 배열에 저장 후 읽은 바이트 수를 리턴
  - void close() : 입력 스트림 닫고 사용 메모리 해제
```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;

public class Main {
    public static void main(String[] args) throws IOException {
        InputStream is = new FileInputStream("./test.txt");

        while(true){
            int data = is.read();
            if (data == -1) break;;
            System.out.println((char) data);
        }

        is.close();
    }
}
```
> 이것도 주로 배열 로 읽음
```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;

public class Main {
    public static void main(String[] args) throws IOException {
        InputStream is = new FileInputStream("./test.txt");
        byte[] data = new byte[100];

        while(true){
            int num = is.read(data);
            if (num == -1) break;

            for(int i=0; i<num; i++){
                System.out.println((char) data[i]);
            }
        }

        is.close();
    }
}

```

- 파일 복사 에제
```java
import java.io.*;

public class P001 {
    public static void main(String[] args) throws IOException {
        String originalFileName = "./test.txt";
        String targetFileName = "./test1.txt";

        //입출력 스트림 생성
        InputStream is = new FileInputStream(originalFileName);
        OutputStream os = new FileOutputStream(targetFileName);

//        byte[] data = new byte[1024];
//        while(true){
//            int num = is.read(data);    //최대 1024 바이트를 읽고 배열에 저장, 읽은 바이트는 리턴
//            if (num == -1) break;
//            os.write(data,0,num);
//        }
        is.transferTo(os); // Java9 부터는 위의 코드를 대체하는 메소드 추가

        os.flush();
        os.close();
        is.close();

        System.out.println("파일 복사완료");
    }
}
```

## 18.4 문자 입출력 스트림

