# 객체 디자인 패턴 DAO, VO, DTO

## 1. VO (Value Object)

- VO는 값 객체를 저장합니다.(예: 금액 주소 값을 저장함)

```java
public class Money {
    private final int amount;

    public Money(int amount) {
        this.amount = amount;
    }

    public int getAmount() {
        return amount;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Money money = (Money) obj;
        return amount == money.amount;
    }

    @Override
    public int hashCode() {
        return Integer.hashCode(amount);
    }
}

```

## 2.DAO(Data Access Object)

- DAO는 데이터 접근을 담당한다. (데이터베이스와의 상호작용을 추상화하는 객체로, 데이터 저장, 조회, 업데이트 등을 담당합니다.)

```java
public class UserDAO {
    private Connection connection;

    public UserDAO() {
        this.connection = DatabaseConnection.getConnection();
    }

    public void save(User user) {
        String query = "INSERT INTO users (id, name) VALUES (?, ?)";
        try (PreparedStatement stmt = connection.prepareStatement(query)) {
            stmt.setInt(1, user.getId());
            stmt.setString(2, user.getName());
            stmt.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public User findById(int id) {
        String query = "SELECT * FROM users WHERE id = ?";
        try (PreparedStatement stmt = connection.prepareStatement(query)) {
            stmt.setInt(1, id);
            ResultSet rs = stmt.executeQuery();
            if (rs.next()) {
                return new User(rs.getInt("id"), rs.getString("name"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return null;
    }
}

```

## 3. DTO (Data Transfer Object)

- DTO는 데이터를 전송하는 데 주로 사용됩니다.(데이터를 전송하기 위한 객체로, 주로 네트워크나 애플리케이션 계층 간 데이터 전달에 사용됩니다)

```java
public class UserDTO {
    private int id;
    private String name;

    // 생성자
    public UserDTO(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // getter 메서드
    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }
}

```