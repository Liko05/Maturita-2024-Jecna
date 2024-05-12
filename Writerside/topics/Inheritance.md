# 8. Dědičnost, method overriding, function overloading

## Dědičnost

- **Dědičnost** je základním prvkem objektově orientovaného programování.
    - Umožňuje vytvářet nové třídy na základě již existujících tříd.
-  **Typy dědičnosti:**
  - **Single inheritance** - třída může dědit pouze od jedné třídy
  - **Multiple inheritance** - třída může dědit od více tříd (Java nepodporuje)
  - **Multilevel inheritance** - třída může dědit od jiné třídy, která dědí od jiné třídy
  - **Hierarchical inheritance** - více tříd může dědit od jedné třídy
  - **Hybrid inheritance** - kombinace více typů dědičnosti

    - **Příklad:**
      ```Java
      public class Vehicle {
          protected String brand;
          protected int year;
      }
  
      public class Car extends Vehicle {
          private int doors;
      }
      ```
- **Výhody:**
    - **Znovupoužitelnost kódu**
    - **Snížení redundance**
    - **Zvýšení čitelnosti kódu**
    - **Zvýšení rozšiřitelnosti**
- **Nevýhody:**
    - **Zvýšení složitosti**
    - **Zvýšení náročnosti na paměť**

## Method overriding

- **Method overriding** je proces, kdy potomek přepíše metodu svého rodiče.
- **Příklad:**
  ```Java
  public class Vehicle {
      public void drive() {
          System.out.println("Driving...");
      }
  }

  public class Car extends Vehicle {
      @Override
      public void drive() {
          System.out.println("Driving a car...");
      }
  }
  ```

## Function overloading

- **Function overloading** je proces, kdy třída obsahuje více metod se stejným názvem, ale různými parametry.
- **Příklad:**
  ```Java
  public class Math {
      public int add(int a, int b) {
          return a + b;
      }

      public double add(double a, double b) {
          return a + b;
      }
  }
  ```
  
- **Proč se používá**
  - **Zvýšení čitelnosti kódu** - stejná metoda s různými parametry
  - **Zvýšení flexibility** - různé typy parametrů
  - **Zvýšení efektivity** - různé návratové typy
  - **Zvýšení rozšiřitelnosti** - podporuje polymorfismus