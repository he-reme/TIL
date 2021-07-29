# Swing

* Java Application에서 사용되는 GUI(Graphic User Interface)를 제공하는 추상적으로 정의된 도구(컴포넌트) 모음

<br>

#### Container

* 다른 컴포넌트들을 배치하기 위한 컴포넌트
* Container는 다른 Container를 포함할 수 있고 나중에 복합적인 Layout을 구성할 수 있게 함
* JFrame: 독립적으로 사용될 수 있으며 타이틀과 사이즈를 조절할 수 있는 버튼을 가짐
* JPanel 
  * 반드시 다른 Container에 포함되어야 하며 복합적인 레이아웃 구성에 사용

<br>

#### 다른 Component

```java
JButton b;
JLabel l;
JTextField tf;
JTable table;
JList list;
```

<br>

---

<br>

## Layout

#### Layout

* Component들을 Container에 어떻게 배치할 것인가

#### LayoutManager

* Container별로 Component의 위치와 크기, 배치 방식을 결정하는 객체

<br>

#### Border Layout

* JFrame의 기본 Layout

* 특별한 영역

  * North, South, West, East, Center에 각각의 컴포넌트를 배치

* 각각의 영역에는 하나의 컴포는트를 담을 수 있고, 중복해서 담을 경우는 마지막에 담은 컴포넌트만 보임

* 크기 조절

  * North와 South는 좌우로
  * East와 West는 상하로만 늘어남. 
  * Center는 양방향

* 생성자에서 수직, 수평 간격을 조절

  `setLayout(new BorderLayout(int hgap, int vgap))`

* 컴포넌트들을 배치할 때는 영역을 지정해줘야 함

  `BorderLayout.CENTER or "Center"`

* 사용하지 않는 공간은 크기가 0*0이 되고 Center가 기본

<br>

---

<br>

## Event Handling

#### 이벤트 처리 모델 (Delegation Model)

* 위임형 모델
* **실제로 이벤트가 일어나는 것은 컴포넌트**이지만
* 거기서 처리되는 것이 아니라 이벤트 리스너를 등록시킨 위임 받은 **handler 클래스 내에서 이벤트 처리**

<br>

#### 이벤트 처리 클래스

* `XX Listener`
  * 이벤트 처리에 대한 메서드들을 정의한 인터페이스로 handler는 이 인터페이스를 구현
* `XX EventAdapter`
  * Listener를 implements 할 경우 사용하지도 않는 이벤트 g핸들러까지 구현해야 하는 단점
    * 필요한 메서드만 구현할 수 있다면??? 밑에!!
  * `-XXXEventAdapter implements XXListener`
    * 해당 메서드들을 모조리 구현해놓은 class. 구현 내용은 비어있는 {}
    * 상속받은 후 필요한 것만 override하면 됨!
  * 

<br>

---

<br>

#### 예시

```java
package com.ssafy.day6.gui;

import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.util.List;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.table.DefaultTableModel;
import com.ssafy.day6.xml.BoxOffice;
import com.ssafy.day6.xml.dom.BoxOfficeDomParser;

/**
 * @since 2021. 7. 11.
 */
public class BoxOfficeUi extends JFrame {
    // 컴포넌트 선언
    JButton button = null;
    JTable table = null;

    // table의 데이터를 관리하는 객체
    DefaultTableModel model = null;

    public static void main(String[] args) {
        BoxOfficeUi ui = new BoxOfficeUi();
        ui.launchUi();
    }

    private void launchUi() {
        button = new JButton("읽기");

        // 테이블 구성
        table = new JTable();
        String[] header = {"랭킹", "제목", "개봉일", "누적관객"};
        model = (DefaultTableModel) table.getModel();
        model.setColumnIdentifiers(header);

        // 이벤트 listener 등록 처리
        addEventListener();

        // 요소 배치
        this.add(new JScrollPane(table), BorderLayout.CENTER);
        this.add(button, BorderLayout.SOUTH);

        this.setTitle("오늘의 영화 랭킹 Top 10");
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setSize(500, 300);
        this.setVisible(true); // 화면에 보여줌
    }

    private void addEventListener() {
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                // 기존 자료 삭제
                model.setRowCount(0);
                // 새로운 자료 조회
                BoxOfficeDomParser parser = new BoxOfficeDomParser();
                List<BoxOffice> list = parser.getBoxOffice();
                for (BoxOffice info : list) {
                    model.addRow(new Object[] {info.getRank(), info.getMovieNm(), info.getOpenDt(), info.getAudiAcc()});
                }
                // model의 데이터가 변경되었음을 알림
                model.fireTableDataChanged();
            }
        });

        // TODO:테이블에서 발생하는 click event 처리를 위한 listener 등록
        table.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                int row = table.getSelectedRow();
                String nm = model.getValueAt(row, 1).toString();
                JOptionPane.showMessageDialog(BoxOfficeUi.this, "선택된 요소: " +
                                                                nm);
            }
        });
        // END:
    }

}

```

