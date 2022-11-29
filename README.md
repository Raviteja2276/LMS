import java.sql.*;

public class JDBCDemo1 {
    public static void main(String[] args) {
        Connection c = null;
        Statement stmt = null;

        try {
            Class.forName("oracle.jdbc.driver.OracleDriver");
            c= DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe","system","123456");

            System.out.println("database successfully opened");
            stmt = c.createStatement();
//            String sql = "INSERT INTO COMPANY15 " +
//                    "VALUES (103, 'PJ', 23, 'AP', 5000)";
//
//
//            sql = "INSERT INTO COMPANY15 " +
//                    "VALUES (108, 'SRI', 22, 'ANDHRA', 60000)";
//            sql = "INSERT INTO COMPANY15 " +
//                    "VALUES (107, 'SAM', 22, 'AP', 60000)";

            String sql = "SELECT * FROM COMPANY15 ";
            ResultSet r = stmt.executeQuery(sql);
            while(r.next()){
             int id=   r.getInt("ID");
              String name =  r.getString("NAME");
              int age= r.getInt("AGE");
               String address= r.getString("ADDRESS");
             int salary = r.getInt("SALARY");
                System.out.println(id+" " +name +" "+age+" "+address+" "+salary);
            }


            stmt.executeUpdate(sql);
            stmt.close();

            c.close();

        } catch (Exception e) {
            System.err.println(e.getClass().getName()+":"+e.getMessage());
            System.exit(0);

        }
        System.out.println("values inserted successfully");

    }
}

