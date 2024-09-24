### Projekt JDBC w Javie z Kompozycją Encji

#### Opis
Celem tego projektu jest stworzenie aplikacji Java, która będzie wykorzystywać JDBC do zarządzania dwoma encjami: `User` i `Profile`. Encja `User` będzie posiadała kompozycję klasy `Profile`, co oznacza, że użytkownik będzie posiadał przypisany profil. Aplikacja będzie zawierała warstwę repozytorium do wykonywania operacji CRUD na bazie danych oraz warstwę Main, gdzie będą uruchamiane operacje.

#### Struktura Projektu
1. **Encje:**
    - `User`: zawiera pola takie jak `id`, `username`, `password` oraz `Profile`.
    - `Profile`: zawiera pola `id`, `email` oraz `phone`.

2. **Baza Danych:**
    - Tabela `users` z kluczami: `id`, `username`, `password`, `profile_id` (klucz obcy do tabeli `profiles`).
    - Tabela `profiles` z kluczami: `id`, `email`, `phone`.

3. **Repozytorium:**
    - Warstwa repozytorium będzie odpowiedzialna za operacje CRUD na obu encjach (`User` i `Profile`), w tym łączenie danych między tabelami przy pomocy klucza obcego.

### Krok po Kroku

#### 1. Struktura Bazy Danych

```sql
CREATE TABLE profiles (
    id SERIAL PRIMARY KEY,
    email VARCHAR(100),
    phone VARCHAR(20)
);

CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50),
    password VARCHAR(50),
    profile_id INT,
    FOREIGN KEY (profile_id) REFERENCES profiles(id)
);
```

#### 2. Encje: `User` i `Profile`

```java
public class Profile {
    private int id;
    private String email;
    private String phone;

    // Gettery i settery
    public int getId() { return id; }
    public void setId(int id) { this.id = id; }

    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }

    public String getPhone() { return phone; }
    public void setPhone(String phone) { this.phone = phone; }
}

public class User {
    private int id;
    private String username;
    private String password;
    private Profile profile;

    // Gettery i settery
    public int getId() { return id; }
    public void setId(int id) { this.id = id; }

    public String getUsername() { return username; }
    public void setUsername(String username) { this.username = username; }

    public String getPassword() { return password; }
    public void setPassword(String password) { this.password = password; }

    public Profile getProfile() { return profile; }
    public void setProfile(Profile profile) { this.profile = profile; }
}
```

#### 3. Warstwa Repozytorium

##### `UserRepository` z JDBC

```java
import java.sql.*;
import java.util.ArrayList;
import java.util.List;

public class UserRepository {

    private static final String URL = "jdbc:postgresql://localhost:5432/mydatabase";
    private static final String USER = "user";
    private static final String PASSWORD = "password";

    public User getUserById(int userId) {
        String sql = "SELECT u.id, u.username, u.password, p.id AS profile_id, p.email, p.phone " +
                     "FROM users u " +
                     "JOIN profiles p ON u.profile_id = p.id " +
                     "WHERE u.id = ?";

        try (Connection connection = DriverManager.getConnection(URL, USER, PASSWORD);
             PreparedStatement preparedStatement = connection.prepareStatement(sql)) {

            preparedStatement.setInt(1, userId);
            try (ResultSet resultSet = preparedStatement.executeQuery()) {
                if (resultSet.next()) {
                    Profile profile = new Profile();
                    profile.setId(resultSet.getInt("profile_id"));
                    profile.setEmail(resultSet.getString("email"));
                    profile.setPhone(resultSet.getString("phone"));

                    User user = new User();
                    user.setId(resultSet.getInt("id"));
                    user.setUsername(resultSet.getString("username"));
                    user.setPassword(resultSet.getString("password"));
                    user.setProfile(profile);

                    return user;
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return null;
    }

    public List<User> getAllUsers() {
        List<User> users = new ArrayList<>();
        String sql = "SELECT u.id, u.username, u.password, p.id AS profile_id, p.email, p.phone " +
                     "FROM users u " +
                     "JOIN profiles p ON u.profile_id = p.id";

        try (Connection connection = DriverManager.getConnection(URL, USER, PASSWORD);
             PreparedStatement preparedStatement = connection.prepareStatement(sql);
             ResultSet resultSet = preparedStatement.executeQuery()) {

            while (resultSet.next()) {
                Profile profile = new Profile();
                profile.setId(resultSet.getInt("profile_id"));
                profile.setEmail(resultSet.getString("email"));
                profile.setPhone(resultSet.getString("phone"));

                User user = new User();
                user.setId(resultSet.getInt("id"));
                user.setUsername(resultSet.getString("username"));
                user.setPassword(resultSet.getString("password"));
                user.setProfile(profile);

                users.add(user);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return users;
    }

    // Metoda do zapisywania użytkownika wraz z profilem
    public void saveUser(User user) {
        String profileSql = "INSERT INTO profiles (email, phone) VALUES (?, ?) RETURNING id";
        String userSql = "INSERT INTO users (username, password, profile_id) VALUES (?, ?, ?)";

        try (Connection connection = DriverManager.getConnection(URL, USER, PASSWORD);
             PreparedStatement profileStatement = connection.prepareStatement(profileSql, Statement.RETURN_GENERATED_KEYS);
             PreparedStatement userStatement = connection.prepareStatement(userSql)) {

            // Zapis profilu
            profileStatement.setString(1, user.getProfile().getEmail());
            profileStatement.setString(2, user.getProfile().getPhone());
            profileStatement.executeUpdate();

            try (ResultSet generatedKeys = profileStatement.getGeneratedKeys()) {
                if (generatedKeys.next()) {
                    int profileId = generatedKeys.getInt(1);

                    // Zapis użytkownika z profilem
                    userStatement.setString(1, user.getUsername());
                    userStatement.setString(2, user.getPassword());
                    userStatement.setInt(3, profileId);
                    userStatement.executeUpdate();
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

#### 4. Warstwa Main

```java
public class Main {
    public static void main(String[] args) {
        UserRepository userRepository = new UserRepository();

        // Tworzenie profilu
        Profile profile = new Profile();
        profile.setEmail("test@test.com");
        profile.setPhone("123456789");

        // Tworzenie użytkownika z profilem
        User user = new User();
        user.setUsername("johndoe");
        user.setPassword("password123");
        user.setProfile(profile);

        // Zapis użytkownika do bazy danych
        userRepository.saveUser(user);

        // Pobieranie użytkownika z bazy danych
        User retrievedUser = userRepository.getUserById(1);
        if (retrievedUser != null) {
            System.out.println("Użytkownik: " + retrievedUser.getUsername() +
                               ", Profil Email: " + retrievedUser.getProfile().getEmail());
        }
    }
}
```

## Testy jednostkowe

```java
import org.h2.jdbcx.JdbcDataSource;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

class UserRepositoryTest {

    private UserRepository userRepository;
    private Connection mockConnection;
    private PreparedStatement mockPreparedStatement;
    private ResultSet mockResultSet;

    @BeforeEach
    void setUp() throws Exception {
        // Mockowanie JDBC
        mockConnection = Mockito.mock(Connection.class);
        mockPreparedStatement = Mockito.mock(PreparedStatement.class);
        mockResultSet = Mockito.mock(ResultSet.class);

        userRepository = new UserRepository();
    }

    @Test
    void testGetUserById() throws Exception {
        // Mockowanie zwracanych danych z ResultSet
        when(mockConnection.prepareStatement(anyString())).thenReturn(mockPreparedStatement);
        when(mockPreparedStatement.executeQuery()).thenReturn(mockResultSet);

        when(mockResultSet.next()).thenReturn(true);
        when(mockResultSet.getInt("id")).thenReturn(1);
        when(mockResultSet.getString("username")).thenReturn("johndoe");
        when(mockResultSet.getString("password")).thenReturn("password123");
        when(mockResultSet.getInt("profile_id")).thenReturn(2);
        when(mockResultSet.getString("email")).thenReturn("test@test.com");
        when(mockResultSet.getString("phone")).thenReturn("123456789");

        // Wywołanie metody
        User user = userRepository.getUserById(1);

        // Sprawdzenie czy wartości są poprawnie przypisane
        assertNotNull(user);
        assertEquals(1, user.getId());
        assertEquals("johndoe", user.getUsername());
        assertEquals("password123", user.getPassword());

        Profile profile = user.getProfile();
        assertNotNull(profile);
        assertEquals(2, profile.getId());
        assertEquals("test@test.com", profile.getEmail());
        assertEquals("123456789", profile.getPhone());
    }

    @Test
    void testSaveUser() throws Exception {
        // Mockowanie Generated Keys dla profilu
        Statement mockStatement = mock(Statement.class);
        when(mockConnection.prepareStatement(anyString(), eq(Statement.RETURN_GENERATED_KEYS)))
            .thenReturn(mockPreparedStatement);
        when(mockPreparedStatement.getGeneratedKeys()).thenReturn(mockResultSet);
        when(mockResultSet.next()).thenReturn(true);
        when(mockResultSet.getInt(1)).thenReturn(1); // Profile ID

        // Mockowanie zapisu użytkownika
        User user = new User();
        user.setUsername("johndoe");
        user.setPassword("password123");

        Profile profile = new Profile();
        profile.setEmail("test@test.com");
        profile.setPhone("123456789");

        user.setProfile(profile);

        // Wywołanie metody
        userRepository.saveUser(user);

        // Weryfikacja czy metoda insert była wywoływana
        verify(mockPreparedStatement, times(2)).executeUpdate();
    }

    @Test
    void testGetAllUsers() throws Exception {
        // Mockowanie danych
        when(mockConnection.prepareStatement(anyString())).thenReturn(mockPreparedStatement);
        when(mockPreparedStatement.executeQuery()).thenReturn(mockResultSet);

        // Mockowanie danych dla wielu użytkowników
        when(mockResultSet.next()).thenReturn(true, true, false); // 2 Users
        when(mockResultSet.getInt("id")).thenReturn(1, 2);
        when(mockResultSet.getString("username")).thenReturn("johndoe", "janedoe");
        when(mockResultSet.getString("password")).thenReturn("password123", "password456");
        when(mockResultSet.getInt("profile_id")).thenReturn(1, 2);
        when(mockResultSet.getString("email")).thenReturn("test@test.com", "jane@test.com");
        when(mockResultSet.getString("phone")).thenReturn("123456789", "987654321");

        // Wywołanie metody
        List<User> users = userRepository.getAllUsers();

        // Sprawdzenie wyniku
        assertEquals(2, users.size());

        User user1 = users.get(0);
        assertEquals("johndoe", user1.getUsername());
        assertEquals("password123", user1.getPassword());
        assertEquals("test@test.com", user1.getProfile().getEmail());

        User user2 = users.get(1);
        assertEquals("janedoe", user2.getUsername());
        assertEquals("password456", user2.getPassword());
        assertEquals("jane@test.com", user2.getProfile().getEmail());
    }
}
```