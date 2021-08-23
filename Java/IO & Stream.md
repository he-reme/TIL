# I/O & Stream

#### I/O와 Stream

* I/O
  * 데이터의 입력과 출력
* 데이터는 한쪽에서 주고 한쪽에서 받는 구조
  * 입력과 출력의 끝단 : 노드
  * 두 노드를 연결하고 데이터를 전송할 수 있는 개념 : 스트림(Stream)
    * 물과 전기의 흐름과 같은 개념
  * 스트림은 단방향으로만 통신이 가능하며 하나의 스트림으로 입력과 출력을 같이 처리할 수 없음

<br>

#### Node Stream의 종류와 naming

* Node Stream
  * node에 연결되는 스트림

* 종류 및 naming
  * 데이터 타입에 따라 : byte or char?
    * byte : `XXStream`
    * char : `XXer`
  * 방향에 따라 (입력 또는 출력)
    * `XXStream`
      * 입력 : InputStream
      * 츨력 : OutputStream
    * `XXer`
      * 입력 : Reader
      * 출력 : Writer
  * 노드 타입에 따라
  * 최종 노드 스트림

<br>

---

<br>

## InputStream & Reader

#### InputStream의 주요 메서드 (오버로딩)

* read()

  * `public abstract int read() throws IOException`

    * 바이트 한 개씩 읽음
    * byte 하나를 읽어서 int로 반환
    * 더 이상 읽을 값이 없으면 `-1`을 리턴

    ```java
    String data = "hi java world";
    
    try ( InputStream input = new ByteArrayInputStream(data.getBytes()) ) {
    	int read = -1;
    	while ((read = input.read()) != -1) {
    		System.out.print("읽은 값 %d, 문자로: %c%n", read, read);
    	} 
    } catch (IOException e) {
    		e.printStackTrace();
    }
    
    ```

    

  * `public int read(byte b[]) throws IOException`

    * Buffer 만큼 씩 읽음
    * 데이터를 읽어서 b를 채우고 읽은 바이트의 개수를 리턴
    * `0`이 리턴되면 더 이상 읽을 값이 없는 상황

    ```java
    String data = "hi java world";
    
    byte[] buffer = new byte[10];
    try ( InputStream input = new ByteArrayInputStream(data.getBytes()) ) {
    	int read = -1;    
    	while ((read = input.read(buffer))>0){ 
    		System.out.print("읽은 개수 %d, 문자열: %s%n", read, new String(buffer));    
    	} 
    }catch (IOException e) {
    	e.printStackTrace();
    }
    ```

    * UTF-8 한글은 한 글자가 3byte

  * `public int read(byte b[], int offset) int len) throws IOException`

    * 최대 len 만큼 데이터를 읽어서 b의 offset부터 b에 저장하고 읽은 바이트 개수를 리턴
    * 따라서 len + offset은 b의 크기 이하여야 함

* close()

  * `public void close() throws IOException`
    * 스트림을 종료해서 자원을 반납

<br>

#### Reader의 주요 메서드

> 유니코드(한글) 안전

* read()

  * `public abstract int read() throws IOException`

  * `public int read(char c[]) throws IOException`

  * `public int read(char c[], int offset) int len) throws IOException`

    ```java
    char[] buffer = new char[10];
    
    try ( Reader input = new CharReader(data.toCharArray(), data.length()) ) {
    	int read = -1;    
    	while ((read = input.read(buffer))>0){ 
    		System.out.print("읽은 개수 %d, 문자열: %s%n", read, new String(buffer, 0, read));    
    	} 
    }catch (IOException e) {
    	e.printStackTrace();
    }
    ```

* close()
  * `public void close() throws IOException`

<br>

---

<br>

## OutStream & Writer

#### OuputStream

* write()
  * `public abstract void write(int b) throws IOException`
  * `public void write(byte b[]) throws IOException`
  * `public void write(byte b[], int off, int len) throws IOEception`
* close()
  * `public void close() throws IOException`
    * 내부적으로 flush()를 호출
* flush()
  * `public void flush() throws IOEception`
    * 버ㅠㅓ가 있는 스트림에서 버퍼의 내용을 출력하고 버퍼를 지운다

<br>

#### Writer

* write()
  * `public abstract void write(int b) throws IOException`
  * `public void write(char c[]) throws IOException`
  * `public void write(char c[], int off, int len) throws IOEception`
  * `public void write(String str) throws IOException`
  * `public void write(String str, int off, int len) throws IOException`
* append()
  * `public Writer append(CharSequence csq) throws IOException`
    * csq 출력하고 Writer 반환
  * `public Writer append(CharSequence csq, int start, int end) throws IOException`
* close()
  * `public void close() throws IOException`
    * 내부적으로 flush()를 호출
* flush()
  * `public void flush() throws IOEception`
    * 버퍼가 있는 스트림에서 버퍼의 내용을 출력하고 버퍼를 지운다

<br>

---

<br>

## File

* 가장 기본적인 입출력 장치 중 하나
* 파일과 디렉터리를 다루는 클래스
* 내용은 관여 못함

<br>

#### 메서드

* File()
  * 파일 객체 생성
  * `public File(String pathname)`
    * pathname에 해당하는 파일 생성
    * 경로 없이 파일을 생성하면 애플리케이션을 시작한 경로가 됨
  * `public File(String parent, String child)`
    * parent 경로 아래 child 생성
  * `public File(File parent, String child)`
    * parent 경로 아래 child 생성
  * `public File(URI uri)`
    * file로 생성하는 URI 객체를 이용해 파일 생성
* createNewFile()
  * `public boolean createNewFile() throws IOException`
  * 새로운 물리적인 파일 생성
* mkdir()
  * `public boolean mkdir()`
    * 새로운 디렉토리 생성
* mkdirs()
  * `public boolean mkdirs()`
    * 경로상에 없는 모든 디렉토리 생성
* delete()
  * `public boolean delete()`
    * 파일 또는 디렉토리 삭제

* getName()
  * public String getName()
    * 파일의 이름을 리턴
* getPath()
  * 파일의 경로 리턴
* getAbsolutePath()
  * 파일의 절대 경로 리턴
* getCanonicalPath()
  * 파일의 정식 경로 리턴 (절대경로)
  * `.`
* isDirectory()
  * 파일의 디렉토리인지 확인
* isFile()
  * 파일인지 리턴
* length()
  * 파일의 길이 리턴
* listFile()
  * 파일이 디렉토리인 경우 자식 파일들을 File[] 형태로 리턴

<br>

#### FileStream

* `FileInputStream(String name)`
  * name 경로의 파일을 읽는 FileInputStream을 생성

* FileOutputStream
  * `FileOutputStream(string name)`
    * name 경로의 파일에 출력하는 FileOutputStream 생성
  * `FileOutputStream(String name, boolean append)`
    * name 경로의 파일에 출력하는 FileOutputStream 생성
    * 기존에 파일이 있다면 뒤에 이어 쓴다.

<br>

#### File Move

```java
public long fileMove(int bufferSize) {
        long start = System.currentTimeMillis();
        File src = new File("c:\\ssafy\\eclipse-jee-2018-09-win32-x86_64.zip");
        File target = new File("c:\\Temp\\eclipse.zip");
        
        try (FileInputStream fin = new FileInputStream(src);
                FileOutputStream fout = new FileOutputStream(target)) {
                
            byte[] buffer = new byte[bufferSize];
            int read = 0;
            
            while ((read = fin.read(buffer)) > 0) {
                fout.write(buffer, 0, read);
            }
            
        } catch (IOException e) {
            e.printStackTrace();
        }

        return System.currentTimeMillis() - start;
    }
```

#### FileReader, FileWriter

<br>

---

<br>

## 보조 스트림

>  Filter Stream, Processing Stream

* 다른 스트림에 부가적인 기능을 제공
  * 문자 set 변환
  * Buffering
  * 기본 데이터 형의 전송
  * 객체 입출력
* 스트림 체이닝
  * 필요에 따라 여러 보조 스트림 연결해서 사용 가능

<br>

#### 종류

* byte 스트림을 char 스트림으로 변환
  * byte 기반
    * InputStreamReader
    * OutputStreamWriter
* 버퍼링을 통한 속도 향상
  * byte 기반
    * BufferedInputStream
    * BufferedOutputStream
  * char 기반
    * BufferedReader
    *  BufferedWriter
* 객체 전송
  * ObjectInputStream
  * ObjectOutputStream

<br>

#### 생성

* 이전 스트림을 생성자의 파라미터에 연결

```
new BufferedInputStream(System.in);
new DataInputStream(new BufferedInputStream(new FileInputStream()));
```

* 노드 스트림은 언제나 필요!!

<br>

#### 종료

* 보조 스트림의 close()를 호출하면 노드 스트림의 close() 까지 호출 됨

<br>

#### 사용할 스트림의 결정 과정

1. 노드가 무엇인가?
2. 타입은 문자열인가? 바이트인가?
3. 방향이 무엇인가? 
4. 추가 기능이 필요한가? 
   * 1, 2, 3 : 노드 스트림 구성
   * 4 : 보조 스트림 구성

**[예시]**

* 어떤 파일을 빠른 속도로 이동시키고 싶다면?
  * 노드 : File
  * 타입 : byte
  * 방향 : 읽기, 쓰기
  * 노드 스트림 : FileInputStream, FileOutputStream
  * 기능 : BufferedInputStream, BufferedOutputStream
* 키보드에서 유니코드 문자를 안전하고 빠르게 읽고 싶다면?
  * 노드 : Keyboard
  * 타입 : byte
  * 방향 : 읽기
  * 노드 스트림 : InputStream, System.in → InputStreamReader
  * 기능 : BufferedReader
* 메모리의 객체를 파일로 저장하고 싶다면?
  * 노드 : File
  * 타입 : byte
  * 방향 : Tmrl
  * 노드 스트림 : FileOutputStream
  * 기능 : ObjectOutputStream

<br>

---

<br>

#### InputStreamReader & OutputStreamWriter

* byte기반 스트림을 char 기반으로 변경해주는 스트림
  * 문자열을 관리하기 위해서는 byte 단위보다 char 단위가 유리
  * 키보드에 입력받은 데이터를 처리할 경우
* 변환시 encoding 지정

<br>

---

<br>

#### Buffered 계열

* 버퍼 역할
* 스트림의 입/출력 효울을 높이기 위해 버퍼를 사용하는 스트림
  * BufferedInputStream()
  * BufferedOutputStream()

<br>

---

<br>

#### 객체 직렬화 (serialization)

* **객체를 저장**하거나 네트워크로 전송하기 위해 연속적인 데이터로 변환하는 것

* 반대의 경우 역 직렬화

* 직렬화 되기 위한 조건

  * serializable 인터페이스를 구현할 것
  * 클래스의 모든 멤버가 Serializable 인터페이스를 구현해야 함
  * 직렬화에서 제외하려는 멤버는 transient 선언

  ```java
  class Person implements Serializable {
  
  	// private static final long serialVersionUID = -8445421888691427769L;
  	
  	private String name;
  	private int age;
  	
  	private transient String ssn;
  	private LoginInfo lInfo;
  }
  ```

  * `implements Serializable`
    * 직렬화 필수 조건
  * `transient`
    * 직렬화 제외 (민감한 정보)
  * `LoginInfo lInfo`
    * 직렬화 필요

* **serialVersionUID**

  * 클래스의 변경 여부를 파악하기 위한 유일 키
  * 직렬화 할 때의 UID와 역 직렬화 할 때의 UID가 다를 경우 예외 발생
  * 직렬화되는 UID가 설정되지 않았을 경우 컴파일러가 자동 생성
    * 멤버 변경으로 인한 컴파일 시마다 변경 → InvalidClassException 초개
* 직렬화되는 객체에 대해서 serialVersionUID 설정 권장

<br>

#### ObjectInputStream, ObjectOutputStream

* `ObjectOutputStream(OutputStream out)`
  * out을 이용해 ObjectOutputStream 객체를 생성
* `writeObject(Object obj)`
  * obj를 직렬화해서 출력
* `ObjectInputStream(InputStream in)`
  * in을 이용해 ObjectInputStream 객체를 생성
* `readObject()`
  * 직렬화된 데이터를 역직렬화해서 Object로 리턴한다 obj를 직렬화해서 출력

```java
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

/**
 * @since 2021. 7. 9.
 */
public class ObjectStreamTest {
    public static void main(String[] args) {
        write();
        read();
    }
    
    private static File target = new File("c:/Temp/objPerson.dat");
    
    private static void write() {
        Person person = new Person("홍길동2", "pass1234", "123-456", "seoul");
        // TODO: person을 target에 저장하시오. 
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(target))) {
            // 객체 저장
            oos.writeObject(person);
            System.out.println("저정 완료!!");
        } catch (IOException e) {
            e.printStackTrace();
        }
        // END:
    }
    
    private static void read() {
        // TODO: target에서 person을 읽어서 내용을 출력하시오.
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream(target));) {
            // 객체 로딩
            Object readed = ois.readObject();

            if (readed != null && readed instanceof Person) {
                Person casted = (Person) readed;
                System.out.println("로딩 완료: "+casted);
            }
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
        // END:
    }
}

```



<br>

---

<br>

#### BufferedReader & BufferedWriter

* BufferedReader
  * readLine()
  * 줄 단위로 데이터를 읽어 들임

* `BufferedReader(Reader in)`
* `BufferedReader(Reader in, int sz)`
* `BufferedWriter(Writer out)`
* `BufferedWriter(Writer out, int sz)`

<br>

#### Scanner와 BufferedReader

* char 형태의 데이터를 읽기위한 클래스들

* Scanner

  * 자동 형변환을 지원하는 등 사용이 간편하지만 속도가 느림

  ```java
   private void useScanner() throws FileNotFoundException {
          
          try(Scanner s = new Scanner(file)){
              long start = System.nanoTime();
              String line = null;
              while(s.hasNextLine()) {
                  line = s.nextLine();
              }
              System.out.printf("sc: %10d%n", System.nanoTime() - start);
          }
      }
  ```

  * 속도 : 130100

* BufferedReader

  * 직접 스트림을 구성해야하는 등 번거롭지만 속도가 빠름

  ```java
  private void useBufferedReader() throws IOException {
          
          try(BufferedReader br = new BufferedReader(new FileReader(file))){
              long start = System.nanoTime();
              String line = null;
              while((line = br.readLine())!=null) {
  				int num = Integer.parseInt(line);
              }
              System.out.printf("br: %10d%n",System.nanoTime() - start);
          }
      }
  ```

  * 속도 : 2286700
  
    * 예시
  
      ```java
      import java.io.BufferedReader;
      import java.io.FileInputStream;
      import java.io.InputStreamReader;
      import java.util.StringTokenizer;
      
      public class Test {
      
      	public static void main(String[] args) throws Exception {
      		// System.in : InputStream - byte - 키보드
      	
      		System.setIn(new FileInputStream("c:/ssafy/data/input.txt"));
      	
      		
      		//  InputStreamReader : InputStream으로 받은 입력값 Reader로 변환해주는.. 
      		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      		
      		int count = Integer.parseInt(br.readLine());
      
      		for(int i=0; i<count; i++) {
      			String msg = br.readLine();
      			if(msg == null)
      				continue;
      			System.out.println(msg);
      			
      			StringTokenizer st = new StringTokenizer(msg);
      			while(st.hasMoreTokens()) {
      				String data = st.nextToken();
      				System.out.printf("%s, ", data);
      			}
      			System.out.println();
      		}
      
      	}
      
      }
      
      ```
  
      

