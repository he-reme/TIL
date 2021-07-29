# XML

* Markup Laguage
  * 태그 등을 이용하여 문서나 데이터의 구조를 명기하는 언ㅇ너
  * HTML, SGML, ...
* XML
  * Extnsible Markup Language
* HTML과 차이
  * 필요에 따라서 태그를 확장해서 사용 가능
  * 정확한 문법을 지켜야 동작 : Well formed

<br>

#### 기본 문법

* 문서의 시작
  * `<?xml version="1.0" encoding="UTF-8"?>`
* 반드시 root element가 존재해야 함
  * 나머지 태그들은 Tree 형태로 구성됨
* 시작 태그와 종료 태그는 일치해야 함
* 시작 태그
  * Key-Value 구조의 속성을 가질 수 있음
  * 속성 값은 `""` 또는 `''`로 묶어서 표현
* 대소문자 구별

<br>

#### valid

* xml 태그는 자유롭게 생성하기 때문에 최초 작성자의 의도대로 작성되는지 확인할 필요 있음
  * DTD, Schema를 잘 따른 문서를 valid 하다라고 함

<br>

---

<br>

## XML 파싱

#### 파싱

* 문서에서 필요한 정보를 얻기 위해 태그를 구별하고 내용을 추출하는 과정

  * 전문적인 parser 활용

* SAX parser

  * Simple API for XML parser
  * 문서를 읽으면서 태그의 시작, 종료 등 이벤트 기반으로 처리하는 방식
  * 빠르고 한번에 처리하기 때문에 다양한 탐색이 어려움

* DOM parser

  * Document Object Model

  * 문서를 다 읽고 난 후 문서 구조 전체를 자료구조에 저장하여 탐색하는 방식
  * 다양한 탐색이 가능하지만 느리고 무거우며 큰 문서를 처리하기 어려움

#### SAX Parser

* Simple API for XML
* 동작 방식
  * 문서를 읽다가 발생하는 이벤트 기반으로 문서 처리

1. SAX Parser Factory

   * SAX Parser 생성

2. SAX Parser

   * XML 문서 파싱
   * DefaultHandler 참조
   * 이벤트 발생시 MyHandler 호출

3. DefaultHandler

   * 어떤 기준으로 파싱할 것인지 정보 담음

   * `startDocumenet()`
   * `startElement()`
   * `characters()`
   * `endElement()`
   * `endDocument()`

4. MyHandler

   * 필요한 메서드 재정의

```java
public class BoxOfficeSaxParser extends DefaultHandler {
    private final File xml = new File("/xml/boxoffice.xml");
    // 파싱된 내용을 저장할 List
    private List<BoxOffice> list = new ArrayList<>();
    // 현재 파싱하고 있는 대상 객체
    private BoxOffice current;
    // 방금 읽은 텍스트 내용
    private String content;

    public List<BoxOffice> getBoxOffice() {
        // TODO: SAXParser를 구성하고 boxoffice.xml을 파싱하시오.
        try {
            SAXParserFactory factory = SAXParserFactory.newInstance();
            SAXParser parser = factory.newSAXParser();
            // this : DefaultHandler
            parser.parse(xml, this);
        } catch (IOException | SAXException | ParserConfigurationException e) {
            e.printStackTrace();
        }
        // END:
        return list;
    }
    
    // TODO: 필요한 매서드를 재정의 하여 boxOffice.xml을 파싱하시오.
    @Override
    public void startDocument() throws SAXException {
        System.out.println("문서 시작");
    }

    @Override
    public void endDocument() throws SAXException {
        System.out.println("문서 종료");
    }


    @Override
    public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {
        // 방금 읽은 태그가 student라면 --> 새로운 Student 생성
        if (qName.equals("dailyBoxOffice")) {
            current = new BoxOffice();
        }
    }

    @Override
    public void characters(char[] ch, int start, int length) throws SAXException {
        this.content = new String(ch, start, length);
    }

    @Override
    public void endElement(String uri, String localName, String qName) throws SAXException {
        if (qName.equals("dailyBoxOffice")) {
            list.add(current);
            current = null;
        } else if (qName.equals("rank")) {
            current.setRank(Integer.parseInt(content));
        } else if (qName.equals("movieNm")) {
            current.setMovieNm(this.content);
        } else if (qName.equals("openDt")) {
            current.setOpenDt(current.toDate(this.content));
        } else if (qName.equals("audiAcc")) {
            current.setAudiAcc(Integer.parseInt(content));
        } else if (qName.equals("dailyBoxOffice")) {
        	list.add(current);
        	current=null;
        }
    }
    // END:
}

```

<br>

---

<br>

## DOM Parser

#### 동작 방식

* 문서를 완전히 메모리에 로딩 후 필요한 내용 찾기

* DOM Tree
  * 문서를 구성하는 모든 요소를 Node(태그, 속성, 값)로 구성
  * 태그들은 root 노드(주소록)을 시작으로 부모-자식의 관계 구성

1. Document Builder Factory
   * Document Builder 생성
2. Document Builder
   * XML 문서 파싱
3. business logic
   * DOM Tree

#### 유용한 API들

* Node
  * 타입
    * ELEMENT_NODE
    * ATTRIBUTE_NODE : key-value
    * TEXT_NODE
  * 메서드
    * `public String getNodeName();`
    * `public String getNodeValue() throws DOMException;`
    * `public short getNodeType();`
    * `public Node getParentNode();`
    * `public NodeList getChildNodes();`
    * `public Node getPreviousSibling();`
    * `public Node getNextSibing();`
    * `public String getTextContent() throws DOMException;`
* Element extends Node
  * 메서드
    * `public NodeList getElementsByTagName(String na	me);`
    * `public String getAttribute(String name);`
    * `public String getTagName();`

```java
public class BoxOfficeDomParser {
    private final File xml = new File("/xml/boxoffice.xml");
    private List<BoxOffice> list = new ArrayList<>();
    
    public List<BoxOffice> getBoxOffice() {
        try {
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            DocumentBuilder builder = factory.newDocumentBuilder();
            // 문서 로딩 완료 --> 원하는 요소들 골라내기
            Document doc = builder.parse(xml);
            // 최 상위 element
            Element root = doc.getDocumentElement();
            parse(root);
        } catch (IOException | ParserConfigurationException | SAXException e) {
            e.printStackTrace();
        }
        return list;
    }

    private void parse(Element root) {
        // TODO: root에서 dailyBoxOffice를 추출한 후 BoxOffice를 생성해 list에 저장하시오.
        NodeList boxOffices = root.getElementsByTagName("dailyBoxOffice");
        for (int i = 0; i < boxOffices.getLength(); i++) {
            Node child = boxOffices.item(i);
            list.add(getBoxOffice(child));
        }
        // END:
    }

    private static BoxOffice getBoxOffice(Node node) {
        BoxOffice boxOffice = new BoxOffice();
        // TODO: node 정보를 이용해서 BoxOffice를 구성하고 반환하시오.

        NodeList subNodes = node.getChildNodes();
        for (int j = 0; j < subNodes.getLength(); j++) {
            Node sub = subNodes.item(j);
            if (sub.getNodeName().equals("rank")) {
                boxOffice.setRank(Integer.parseInt(sub.getTextContent()));
            } else if (sub.getNodeName().equals("movieNm")) {
                boxOffice.setMovieNm(sub.getTextContent());
            } else if (sub.getNodeName().equals("openDt")) {
                boxOffice.setOpenDt(boxOffice.toDate(sub.getTextContent()));
            } else if (sub.getNodeName().equals("audiAcc")) {
                boxOffice.setAudiAcc(Integer.parseInt(sub.getTextContent()));
            }
        }
        // END:
        return boxOffice;
    }
}
```

