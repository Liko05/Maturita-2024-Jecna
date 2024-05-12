# 9. Integrita dat, bezpečnost, logování, kontrola vstupů, zpracování chyb

## Integrita dat

- **Integrita dat** je zajištění konzistence a validity dat v databázi.
- V Javě můžeme integritu dat zajistit například pomocí konstruktorů, getterů a setterů, které kontrolují validitu dat
  při jejich nastavování.

```java
public class Data {
    private int number;

    public Data(int number) {
        if (number >= 0) {
            this.number = number;
        } else {
            throw new IllegalArgumentException("Number must be positive");
        }
    }

    public int getNumber() {
        return number;
    }

    public void setNumber(int number) {
        if (number >= 0) {
            this.number = number;
        } else {
            throw new IllegalArgumentException("Number must be positive");
        }
    }
}
```

## Bezpečnost

- **Bezpečnost** v Javě zahrnuje různé aspekty, tj. bezpečnost dat, aplikace a uživatlů. Existují různé nástroje na
  zajištění bezpečnosti.
- **Příklady:**
    - **Šifrování** - zabezpečení dat pomocí šifrování
    - **Autentizace** - ověření identity uživatele
    - **Autorizace** - kontrola oprávnění uživatele
    - **Firewall** - zabezpečení sítě
    - **Antivirový software** - ochrana před škodlivým softwarem

```Java
// Příklad šifrování
public class Encryption {
    public static String encrypt(String data) {
        return Base64.getEncoder().encodeToString(data.getBytes());
    }

    public static String decrypt(String data) {
        return new String(Base64.getDecoder().decode(data));
    }
}

// Příklad autentizace
public class Authentication {
    public static boolean authenticate(String username, String password) {
        return username.equals("admin") && password.equals("admin");
    }
}
```

## Logování

- **Logování** je proces zaznamenávání událostí v aplikaci. V Javě můžeme používat například
  logger `java.util.logging.Logger`.

- **Proč logovat:**
    - **Debugging** - zjištění chyb
    - **Monitoring** - sledování aplikace
    - **Audit** - záznam událostí

```Java
import java.util.logging.Logger;

public class Main {
    private final static Logger LOGGER = Logger.getLogger(Main.class.getName());

    public static void main(String[] args) {
        LOGGER.info("This is an info message");
        LOGGER.warning("This is a warning message");
        LOGGER.severe("This is a severe message");
    }
}
```

## Kontrola vstupů

- **Kontrola vstupů** je proces ověřování, zda jsou vstupy do aplikace validní a bezpečné. Můžeme používat například
  validátory, výjimky. Každá metoda, která má nějaké vstupy, by měla kontrolovat jejich validitu.

```Java
public class Validator {
    public static boolean isNumber(String input) {
        return input.matches("\\d+");
    }

    public static boolean isEmail(String input) {
        return input.matches("^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$");
    }
}

public class Main {
    public static void main(String[] args) {
        String number = "123";
        if (Validator.isNumber(number)) {
            System.out.println("Valid number");
        } else {
            System.out.println("Invalid number");
        }
    }
}
```

## Zpracování chyb

- **Zpracování chyb** je proces řešení problémů,které se vyskytnou během běhu aplikace. V Javě můžeme používat
  výjimky, které nám umožňují zachytit a zpracovat chyby, try-catch bloky.

```Java
public class Main {
    public static void main(String[] args) {
        try {
            int result = divide(10, 0);
            System.out.println(result);
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero");
        }
    }

    public static int divide(int a, int b) {
        return a / b;
    }
}
```