# 10. Komunikace s databázovým systémem - Připojení, Ukládání a načítání dat, Mapování entit v OOP

## Připojení k databázi

- V Javě můžeme k databázi připojit pomocí JDBC (Java Database Connectivity) API, které poskytuje metody pro dotazování
  a aktualizaci dat v databázi.
- JDBC podporuje SQL a umožňuje nám pracovat s různými databázovými systémy, jako jsou MySQL, Oracle, PostgreSQL atd.
- Připojení k databázi je první krok při práci s databází. Bez připojení k databázi nemůžeme provádět žádné operace s
  daty.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DatabaseConnection {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/myDatabase";
        String username = "root";
        String password = "password";

        try (Connection connection = DriverManager.getConnection(url, username, password)) {
            System.out.println("Database connected!");
        } catch (SQLException e) {
            throw new IllegalStateException("Cannot connect the database!", e);
        }
    }
}
```

## Ukládání a načítání dat

- Data můžeme ukládat do db pomcí SQL příkazů `INSERT INTO` a načítat pomocí `SELECT`.
- Ukládání a načítání dat jsou jedny ze základních operací, které můžeme provádět s db.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class DatabaseOperations {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/myDatabase";
        String username = "root";
        String password = "password";

        try (Connection connection = DriverManager.getConnection(url, username, password)) {
            String sqlInsert = "INSERT INTO Users (username, password, email) VALUES (?, ?, ?)";
            PreparedStatement statementInsert = connection.prepareStatement(sqlInsert);
            statementInsert.setString(1, "testuser");
            statementInsert.setString(2, "testpass");
            statementInsert.setString(3, "testuser@test.com");
            int rowsInserted = statementInsert.executeUpdate();
            if (rowsInserted > 0) {
                System.out.println("A new user was inserted successfully!");
            }

            String sqlSelect = "SELECT * FROM Users";
            PreparedStatement statementSelect = connection.prepareStatement(sqlSelect);
            ResultSet result = statementSelect.executeQuery(sqlSelect);
            while (result.next()){
                String name = result.getString(2);
                String pass = result.getString(3);
                String email = result.getString("email");
                System.out.println(name + ", " + pass + ", " + email);
            }
        } catch (SQLException e) {
            throw new IllegalStateException("Cannot connect the database!", e);
        }
    }
}
```

## Mapování entit v OOP

- **Mapování entit** OOP (Object-Oriented Programming) je technika, která umožňuje pracovat s db pomocí objektů místo
  sql dotazů.
- V Javě můžeme používat JPA pro ORM (Object-Relational Mapping), které nám umožňuje mapovat objekty na tabulky v db.
- ORM nám umožňuje pracovat s db na výšší úrovní. Místo psání SQL příkazů můžeme pracovat s objekty a nechat ORM
  knihovnu, aby se postarala o převod mezi objektz a databází.

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    private int id;
    private String username;
    private String password;
    private String email;

    // getters and setters
}

import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;

public class App {
    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
        EntityManager em = emf.createEntityManager();

        em.getTransaction().begin();
        User user = new User();
        user.setUsername("testuser");
        user.setPassword("testpass");
        user.setEmail("testuser@test.com");
        em.persist(user);
        em.getTransaction().commit();

        User foundUser = em.find(User.class, user.getId());
        System.out.println(foundUser.getUsername());

        em.close();
        emf.close();
    }
}
```

