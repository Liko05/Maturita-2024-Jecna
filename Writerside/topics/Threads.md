# 22. Vlákna, Paralerní programování, Asynchroní metody, Concurrent design patterns

## Vlákna

### Co je vlastně vlákno?

- Jedná se o jednu instanci třídy Thread
- Umožnuje paralelní běh programu, tj. více částí programu běží současně
- Kdykoliv spustíme program, JVM pro něj vytvoří zásobník na Stacku

### Jak vytvořit vlákno?

- Pomocí třídy Thread, ExecutorService, Runnable...
- Vytvoření vlákna pomocí třídy Thread:

```java
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            System.out.println("Hello from thread!");
        });
        thread.start();
    }
}
```

```Java
public class Main extends Thread {
    public void run() {
        System.out.println("Hello from thread!");
    }
    public static void main(String[] args) {
        Main thread = new Main();
        thread.start();
    }
}
```

```Java
class Test implements Runnable {
    public void run() {
        System.out.println("Hello from thread!");
    }
    public static void main(String[] args) {
        Thread thread = new Thread(new Test());
        thread.start();
    }
}
```

### Jak synchronizovat vlákna?

- Synchronizace je důležitá, pokud pracujeme s nějakými sdílenými daty
- Synchronizace se provádí pomocí klíčového slova `synchronized`

```Java
public class Main {
    private static int count = 0;
    public static synchronized void increment() {
        count++;
    }
    public static void main(String[] args) {
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 10000; i++) {
                increment();
            }
        });
        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 10000; i++) {
                increment();
            }
        });
        thread1.start();
        thread2.start();
        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(count);
    }
}
```

## Paralerní programování

- Paralelní programování je způsob, jak zrychlit běh programu
- Zpracovává více úkolů současně
- V Javě se používá např. třída ExecutorService

```Java
public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        executor.submit(() -> {
            System.out.println("Hello from thread!");
        });
        executor.submit(() -> {
            System.out.println("Hello from thread!");
        });
        executor.shutdown();
    }
}
```

### Note

- Vlákna se pouštějí najednou, program může vracet pokaždé jiný výsledek při třídy Thread

## Asynchroní metody

- Neblokují svým spuštěním chod programu
- Příkladem, kde se hodí, je stahování souborů z internetu

```Java
public class Main {
    public static void main(String[] args) {
        CompletableFuture.runAsync(() -> {
            System.out.println("Hello from thread!");
        });
    }
}
```

- Metoda `runAsync` vytvoří nové vlákno a spustí v něm kód
- CompletableFuture může, ale nemusí, vytvořit nové vlákno pro asynchronní metodu

## Concurrent design patterns

- Vzory, které řeší problémy při kterých program běží na několika vláknech najednou a řeší souběžně operace
  - **Thread Pool** - vytvoření poolu vláken, které se používají pro spouštění úkolů seřazené ve frontě
  - **Read Write Lock** - slouží k umožnění více vláken pro čtení a jednoho pro zápis

### Thread Pool

- Vytvoření poolu vláken, které se používají pro spouštění úkolů seřazené ve frontě

```Java
public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        executor.submit(() -> {
            System.out.println("Hello from thread!");
        });
        executor.submit(() -> {
            System.out.println("Hello from thread!");
        });
        executor.shutdown();
    }
}
```

### Read Write Lock

- Jedná se o synchonizační mechanismus, který umožňuje více vláken pro čtení a jednoho pro zápis
- Funguje to následovně:
  - Vlákno A vstoupí do metody, ihned ji zamkne
  - Vlákno B se pokusí vstoupit do metody, ale je zamčená, takže čeká
  - Vlákno A dokončí čtení a odemkne metodu
  - Vlákno B vstoupí do metody a zamkne ji

```Java
public class Main {
    private static ReadWriteLock lock = new ReentrantReadWriteLock();
    private static Lock readLock = lock.readLock();
    private static Lock writeLock = lock.writeLock();
    private static int count = 0;
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        executor.submit(() -> {
            readLock.lock();
            System.out.println(count);
            readLock.unlock();
        });
        executor.submit(() -> {
            writeLock.lock();
            count++;
            writeLock.unlock();
        });
        executor.shutdown();
    }
}
```

```mermaid
graph LR
    A[Thread A] --> B[Read Lock]
    B --> C[Read Data]
    C --> D[Unlock]
    D --> E[Thread B]
    E --> F[Write Lock]
    F --> G[Write Data]
    G --> H[Unlock]
```