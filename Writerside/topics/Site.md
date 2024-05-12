# 11. Komunikace v síti - tvorba síťových aplikací, Berkley socket a jeho rozhraní

- **Síťová komunikace** je proces, kdy dva nebo více počítačů sdílí data přes nějakou formu fyzického média (např.
  kabel, Wi-Fi).
- **Síťová aplikace** je aplikace, která komunikuje přes síť s jinými aplikacemi nebo službami.
- **Socket** je koncový bod komunikace mezi dvěma systémy přes síť.

## Sockets

- **Socket** je základní stavební kámen pro vytváření síťových aplikací v Javě.
- **Berkley socket** je implementace socketu, která byla původně vytvořena pro BSD Unix. V Javě je tato implementace
  dostupná prostřednictvím třídy `java.net.Socket`.

### Základní operace pro sockety:

- | Operace | Popis |
          | --- | --- |
  | **Vytvoření socketu** | Vytvoření nového socketu. |
  | **Připojení k serveru** | Připojení socketu k serveru. |
  | **Poslání dat** | Poslání dat přes socket. |
  | **Přijetí dat** | Přijetí dat přes socket. |
  | **Uzavření socketu** | Uzavření socketu. |

### Code example {id="code-example_1"}

```java
import java.net.Socket;
import java.io.OutputStream;
import java.io.DataOutputStream;

public class Client {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 8080);
            OutputStream output = socket.getOutputStream();
            DataOutputStream dos = new DataOutputStream(output);

            dos.writeUTF("Hello Server!");

            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Síťové aplikace

- **Síťová aplikace** je aplikace, která komunikuje přes síť s jinými aplikacemi nebo službami. Můžeme je vytvořit
  pomocí tříd `java.net.ServerSocket` a `java.net.Socket`.
- **ServerSocket** je třída, která naslouchá na určitém portu a přijímá připojení od klientů.
- **Socket** je třída, která reprezentuje koncový bod komunikace mezi dvěma systémy přes síť.

### Základní operace pro síťové aplikace:

- | Operace | Popis |
          | --- | --- |
  | **Vytvoření serveru** | Vytvoření nového serveru. |
  | **Čekání na klienta** | Čekání na připojení klienta. |
  | **Přijetí dat** | Přijetí dat od klienta. |
  | **Odeslání dat** | Odeslání dat klientovi. |
  | **Uzavření serveru** | Uzavření serveru. |

### Code example {id="code-example_2"}

```java
import java.net.ServerSocket;
import java.net.Socket;
import java.io.InputStream;
import java.io.DataInputStream;

public class Server {
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(8080);
            System.out.println("Server is running...");

            Socket socket = serverSocket.accept();
            System.out.println("Client connected!");

            InputStream input = socket.getInputStream();
            DataInputStream dis = new DataInputStream(input);

            String message = dis.readUTF();
            System.out.println("Message from client: " + message);

            serverSocket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Vlastnosti síťových aplikací

- **Komunikace** - síťové aplikace mohou komunikovat přes různé protokoly, jako je TCP, UDP, HTTP, atd.
- **Bezpečnost** - síťové aplikace mohou být zabezpečeny pomocí šifrování a ověřování. Bráníme se tak tím útokům typu
  MITM.
- **Výkon** - síťové aplikace mohou být optimalizovány pro rychlou a efektivní komunikaci mezi klienty a servery a
  zvládat velké množství připojení.