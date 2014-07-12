# 第七章 JDBC数据库开发接口

----------
### 7.3.1 JDBC的四种类型(page171)
+ JDBC-ODBC桥加ODBC驱动程序
+ 本地API
+ JDBC网络纯Java驱动程序
+ 本地协议纯Java驱动程序

----------
### 7.3.2 数据驱动程序(page172)
+ 加载Oracle的JDBC驱动程序的语句为：
	>**Class.forName("oracle.jdbc.driver.OracleDriver");**

+ 使用JDBC-ODBC桥驱动程序的语句为：
	>**Class.forName("sun.jdbc.odbc.JdbcOdbcDriver");**

+ 加载Sql2005驱动程序的语句为：
	>**Class.forName("com.microsoft.jdbc.sqlserver.SQLServerDriver");**

+ 加载MySQL驱动下次语句为：
	>**Class.forName("com.mysql.jdbc.Driver");**

----------
### 7.3.3 Connection对象(page172)
<pre>
<code>
import java.sql.*;

public class DB {
	public static Connection getConn() {
		Connection conn = null;
		try {
			Class.forName("com.mysql.jdbc.Driver");
			conn = DriverManager.getConnection("jdbc:mysql://localhost/shopping?user=root&password=123456");
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		}
		
		return conn;
	}
	
	public static PreparedStatement prepare(Connection conn,  String sql) {
		PreparedStatement pstmt = null; 
		try {
			if(conn != null) {
				pstmt = conn.prepareStatement(sql);
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return pstmt;
	}
	
	public static PreparedStatement prepare(Connection conn,  String sql, int autoGenereatedKeys) {
		PreparedStatement pstmt = null; 
		try {
			if(conn != null) {
				pstmt = conn.prepareStatement(sql, autoGenereatedKeys);
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return pstmt;
	}
	
	public static Statement getStatement(Connection conn) {
		Statement stmt = null; 
		try {
			if(conn != null) {
				stmt = conn.createStatement();
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return stmt;
	}
	
	/*
	public static ResultSet getResultSet(Connection conn, String sql) {
		Statement stmt = getStatement(conn);
		ResultSet rs = getResultSet(stmt, sql);
		close(stmt);
		return rs;
	}
	*/
	
	public static ResultSet getResultSet(Statement stmt, String sql) {
		ResultSet rs = null;
		try {
			if(stmt != null) {
				rs = stmt.executeQuery(sql);
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return rs;
	}
	
	public static void executeUpdate(Statement stmt, String sql) {
		try {
			if(stmt != null) {
				stmt.executeUpdate(sql);
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	public static void close(Connection conn) {
		try {
			if(conn != null) {
				conn.close();
				conn = null;
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	public static void close(Statement stmt) {
		try {
			if(stmt != null) {
				stmt.close();
				stmt = null;
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
</code>
</pre>