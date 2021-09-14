# JDBC

> Java DataBase Connectivity

<br>

#### JDBC 작업 순서

1. Driver Loading

2. DB 연결 (Connection 생성)

3. SQL 실행 준비

   3-1. SQL 작성.

   3-2. Statement 생성 (Statement, PreparedStatement)

4. SQL 실행

   4-1. I, U, D

   ```
   int x = stmt.execteUpdate(sql);
   int x = pstmt.executeUpdate();
   ```

   4-2. S

   ```
   ResultSet rs = pstmt.executeQuery();
   rs.next() [단독, if, while]
   rs.getString() // 값 얻기
   rs.getInt() 등등등....
   ```

5. DB 연결 종료 : 연결 역순으로 종료, finally, AutoCloseable, try-with-resource (JDK7이상)

   ```
   if(rs != null)
   	rs.close()
   if(pstmt != null)
   	pstmt.close();
   if(conn != null)
   	conn.close();
   ```

<br>

#### Driver download

https://dev.mysql.com/downloads/connector/j/

