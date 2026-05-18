## StudentDatabaseManager Class
```Java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class StudentDatabaseManager {

    String url = "jdbc:mysql://localhost:3306/Auto";
    String user = "testuser";
    String pass = "Password";

    public static void main(String[] args) {
        Connection conn = null;
        try {
            conn = DriverManager.getConnection(URL, USER, PASSWORD);
            System.out.println("Connected to the Miramar database successfully.");

            insertStudentRecord(conn);

            updateStudentZip(conn, "111222333", "92126");

        } catch (SQLException e) {
            System.err.println("Database error: " + e.getMessage());
        } finally {
            try {
                if (conn != null) conn.close();
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        }
    }

    private static void insertStudentRecord(Connection conn) throws SQLException {
        String insertSQL = "INSERT INTO Student (SSN, firstName, middleName, lastName, dob, street, phone, zipcode, deptID) " +
                           "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)";

        try (PreparedStatement pstmt = conn.prepareStatement(insertSQL)) {
            pstmt.setString(1, "111222333");
            pstmt.setString(2, "Philip");
            pstmt.setString(3, "David Charles");
            pstmt.setString(4, "Collins");
            pstmt.setString(5, "1951-01-30");
            pstmt.setString(6, "NA");
            pstmt.setString(7, "NA");
            pstmt.setString(8, "NA");
            pstmt.setString(9, "1234");

            int rowsInserted = pstmt.executeUpdate();
            if (rowsInserted > 0) {
                System.out.println("A new student record was inserted successfully!");
            }
        }
    }

    private static void updateStudentZip(Connection conn, String ssn, String newZip) throws SQLException {
        String updateSQL = "UPDATE Student SET zipcode = ? WHERE SSN = ?";

        try (PreparedStatement pstmt = conn.prepareStatement(updateSQL)) {
            pstmt.setString(1, newZip);
            pstmt.setString(2, ssn);

            int rowsUpdated = pstmt.executeUpdate();
            if (rowsUpdated > 0) {
                System.out.println("Student record updated. Zipcode changed to: " + newZip);
            }
        }
    }
}
```
