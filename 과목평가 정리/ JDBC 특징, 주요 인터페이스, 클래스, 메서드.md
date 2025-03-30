- 특정 : 
	- 데이터베이스 독립성
		- DB 벤더별로 JDBC 드라이버를 구현
		- 애플리케이션은 JDBC API만 사용하면 되므로, DB를 교체해도 코드 변경을 최소화
- 주요 인터페이스:
	- DriverManager
		- Class.forName("com.mysql.jdbc.Driver")
		- DriverManager.getConnection(url, user, password)
			- 지정한 URL, 계정 정보로 DB 연결을 시도하고 `Connection` 객체를 반환합니다.
	- Connection
		- DB와의 연결(세션)을 나타내는 객체입니다.
		- 트랜잭션 제어(커밋, 롤백)나 `Statement`, `PreparedStatement` 객체를 생성가능
		- createStatement()
			- SQL 실행을 위한 `Statement` 객체를 생성합니다.
		- prepareStatement(String sql)
			- 미리 컴파일된 SQL을 실행하기 위한 `PreparedStatement` 객체를 생성합니다.
		- setAutoCommit(boolean autoCommit)
			- 트랜잭션 자동 커밋 여부를 설정합니다. false로 설정하면 수동 커밋/롤백이 가능합니다.
		- `commit()` / `rollback()`
			- 수동 트랜잭션 모드에서 쿼리 실행 결과를 커밋하거나 롤백합니다.
		- close()
	- Statement
		- SQL 쿼리를 실행하기 위한 객체
		- 가장 기본이 되는 STATEMENT
		- 생성시 실행할 SQL이 정해지지않음
		- SQL INJECTION 취약
		- executeQuery(String sql)
			- SELECT 쿼리를 실행하고, 결과로 `ResultSet`을 반환합니다.
		- executeUpdate(String sql)
			- INSERT, UPDATE, DELETE 쿼리를 실행하며, 적용된 레코드 수(정수)를 반환합니다.
		- execute(String sql)
			- 쿼리 종류와 무관하게 실행 가능하며, 결과 여부에 따라 boolean을 반환합니다.
		- close()
	- PreparedStatement
		- `Statement`를 상속받은 서브 인터페이스
		- 쿼리에 파라미터(“?”)를 사용하여 값을 동적 바인딩 실행 가능
		- SQL INJECTION 대비 가능
		- setXxx(int parameterIndex, Xxx value)
			- SQL에 바인딩될 변수값을 세팅합니다.
			- 예: `setString(1, "Hello")`, `setInt(2, 100)` 등
		- executeQuery()
			- 바인딩된 SQL을 실행하고, `ResultSet`을 반환합니다.
		- executeUpdate()
			- 바인딩된 SQL(INSERT, UPDATE, DELETE 등)을 실행하고 적용된 레코드 수를 반환합니다.
		- `addBatch()` / `executeBatch()`
			- 여러 SQL을 배치로 모아 일괄 실행하여 성능을 높일 때 사용합니다.
		- clearParameters()
			- PreparedStatement에 설정된 모든 파라미터를 초기화합니다.
	- CallableStatement
		- DB 내의 Stored Procedure를 호출하는 SQL을 실행하기 위한 Statement
		- DMBS에 종속적
	- ResultSet
		- SQL 쿼리 실행 결과를 담는 인터페이스
		- 커서(Cursor) 방식으로 데이터를 순회
		- `next()`, `previous()` 등의 메서드로 레코드를 이동해가며 탐색
		- next()
			- 커서를 다음 레코드로 이동하고, 결과가 있으면 `true`를 반환합니다.
		- getXxx(String columnLabel)
			- 현재 커서가 가리키는 레코드에서 컬럼(columnLabel)의 값을 가져옵니다.
			- 예: `getString("name")`, `getInt("age")` 등
		- close()
	- SQLException
		- JDBC를 사용하면서 발생하는 예외를 처리하기 위한 예외 클래스

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class JdbcExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydb";
        String user = "root";
        String password = "root";

        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;

        try {
            // 1. 드라이버 로드 (필요시)
            Class.forName("com.mysql.jdbc.Driver");  
            
            // 2. Connection 객체 생성
            conn = DriverManager.getConnection(url, user, password);
            
            // 3. 쿼리 준비 (PreparedStatement)
            String sql = "SELECT id, name FROM user WHERE age > ?";
            pstmt = conn.prepareStatement(sql);
            pstmt.setInt(1, 20);
            
            // 4. 쿼리 실행
            rs = pstmt.executeQuery();
            
            // 5. 결과 처리
            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                System.out.println("ID: " + id + ", Name: " + name);
            }
            
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
            // 6. 자원 정리 (반드시 try-catch로 감싸서 에러 방지)
            try {
                if (rs != null) rs.close();
                if (pstmt != null) pstmt.close();
                if (conn != null) conn.close();
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        }
    }
}

```