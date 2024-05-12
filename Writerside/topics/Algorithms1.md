# 2. Algoritmizace - Grafy, Prohlédávání stavového prostoru, Řazení

- Algoritmy jsou postupy řešení problémů pro jednotlivé problémy. 
- Každý algoritmus má svou složitost, která se dá vyjádřit časovou a paměťovou složitostí.
- Zásadně je tvořen jednoznačným postupem, zaručuje že pro správný vstup vrátí správný výstup.

## Vlastnosti algoritmů

- **Hromadnost** - Měnitelná vstupní data.
- **Determinovanost** - Každý krok je jednoznačně definován.
- **Konečnost a resultativnost** - Pro správný vstup vrátí správný výstup.

## Grafy

- **[G]raf** je množina vrcholů a hran, které spojují vrcholy. Slouží k reprezentaci vztahů mezi objekty. Značíme G(V,E)
  - **[V]rchol** - Objekt, který je reprezentován v grafu.
  - **Hrana/[E]dge** - Relace mezi dvěma vrcholy.
  - **Využití** - Například pro hledání nejkratší cesty, detekci cyklů, nebo pro reprezentaci dat.

### Znázornění grafu:

#### Ilustrace 
![Graf](https://media.geeksforgeeks.org/wp-content/uploads/undirectedgraph.png)
#### Matrix 
![Matice](https://media.geeksforgeeks.org/wp-content/uploads/adjacencymatrix.png)

### Základní operace pro grafy:

- | Operace | Popis |
  | --- | --- |
  | **Vložení vrcholu** | Vložení nového vrcholu do grafu. |
  | **Vložení hrany** | Vložení nové hrany mezi vrcholy. |
  | **Smazání vrcholu** | Smazání vrcholu z grafu. |
  | **Smazání hrany** | Smazání hrany mezi vrcholy. |
  | **Výpis grafu** | Výpis grafu. |
  | **Prohledávání grafu** | Prohledávání grafu. |
  
### Code example {id="code-example_1"}

```Java
class Graph<T> {
    private Map<T, List<T>> map = new HashMap<>();
    
    public void addVertex(T s) {
        map.put(s, new LinkedList<T>());
    }
    
    public void addEdge(T source, T destination, boolean bidirectional) {
        if (!map.containsKey(source)) addVertex(source);
        if (!map.containsKey(destination)) addVertex(destination);
        map.get(source).add(destination);
        if (bidirectional) map.get(destination).add(source);
    }
    
    public void getVertexCount() {
        System.out.println("The graph has " + map.keySet().size() + " vertex");
    }
    
    public void hasVertex(T s)
    {
        if (map.containsKey(s)) {
            System.out.println("The graph contains " + s
                               + " as a vertex.");
        }
        else {
            System.out.println("The graph does not contain "
                               + s + " as a vertex.");
        }
    }
    
    public void hasEdge(T s, T d)
    {
        if (map.get(s).contains(d)) {
            System.out.println(
                "The graph has an edge between " + s
                + " and " + d + ".");
        }
        else {
            System.out.println(
                "The graph has no edge between " + s
                + " and " + d + ".");
        }
    }
}
```

## Prohlédávání stavového prostoru

- **Stavový prostor** - Množina všech možných stavů, S.
- **Počáteční stav** - Stav, ve kterém se nacházíme, s0 ∈ S
- **Cílové stavy** - Stavy, které chceme dosáhnout, T ⊆ S
- **Akce** - Operace, kterou můžeme provést, A
- **Přechodová funkce** - Funkce, která nám říká, jak se můžeme dostat z jednoho stavu do druhého, f : S × A → S

### Vlastnosti prohlédávání stavového prostoru

- **Úplnost** - Algoritmus najde cílový stav, pokud existuje.
- **Optimalita** - Algoritmus najde nejlepší cestu.
- **Využití** - Plánování cesty, bludiště, řešení hlavolamů.

### Algoritmy pro prohlédávání stavového prostoru

- **[DFS](https://en.wikipedia.org/wiki/Depth-first_search) (Depth First Search)**
  - Prohledávání do hloubky.
  - Funguje následovně: V každém stavu zkusím něco udělat. Když už to nejde, tak se
    vrátím a zkusím něco jiného.
  - Vlastnosti: Cíl => hotovo, ozančuje si prozkoumané uzly.

#### DFS 
![DFS](https://he-s3.s3.amazonaws.com/media/uploads/9fa1119.jpg)

#### DFS Code example

```Java
class Graph {
  private LinkedList<Integer> adjLists[];
  private boolean visited[];

  Graph(int vertices) {
    adjLists = new LinkedList[vertices];
    visited = new boolean[vertices];

    for (int i = 0; i < vertices; i++)
      adjLists[i] = new LinkedList<Integer>();
  }

  void addEdge(int src, int dest) {
    adjLists[src].add(dest);
  }

  void DFS(int vertex) {
    visited[vertex] = true;
    System.out.print(vertex + " ");

    Iterator<Integer> ite = adjLists[vertex].listIterator();
    while (ite.hasNext()) {
      int adj = ite.next();
      if (!visited[adj])
        DFS(adj);
    }
  }
}
```

- **[BFS](https://en.wikipedia.org/wiki/Breadth-first_search) (Breadth First Search)**
  - Prohledávání do šířky.
  - Funguje následovně: Hledáme v pořadí délky sekvence akcí. Nejprve prozkoumáme všechny sousedy, pak jejich sousedy, atd.
  - Vlastnosti: Vždy najde nejkratší cestu, využívá frontu.

#### BFS 
![BFS](https://velog.velcdn.com/images%2Fseongwon97%2Fpost%2F32e4165b-b98a-41d6-8daf-0506528cb07b%2Fimage.png)

#### BFS Code example

```Java
class Graph {

    private int V;

    private LinkedList<Integer> adj[];

    Graph(int v)
    {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList();
    }

    void addEdge(int v, int w) { adj[v].add(w); }

    void BFS(int s)
    {
        boolean visited[] = new boolean[V];

        LinkedList<Integer> queue
            = new LinkedList<Integer>();

        visited[s] = true;
        queue.add(s);

        while (queue.size() != 0) {

            s = queue.poll();
            System.out.print(s + " ");

            Iterator<Integer> i = adj[s].listIterator();
            while (i.hasNext()) {
                int n = i.next();
                if (!visited[n]) {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }
    }
}
```

## Řazení

- **Řazení** - Proces, kdy se prvky v poli uspořádají podle určité vlastnosti.
- **Algoritmy** - Bubble sort, Selection sort, Insertion sort, Merge sort, Quick sort, Heap sort, Radix sort.
- **Využití** - Vyhledávání, statistika, databáze.

### Bubble sort

- **Princip** - Porovnává dva sousední prvky a prohodí je, pokud nejsou ve správném pořadí.
- **Využití** - Malé pole, kde je třeba jednoduchý algoritmus.

![Bubble sort](https://media.geeksforgeeks.org/wp-content/uploads/20230526103842/1.webp)

#### Bubble sort Code example

```Java
class BubbleSort {
    void bubbleSort(int arr[]) {
        int n = arr.length;
        for (int i = 0; i < n-1; i++)
            for (int j = 0; j < n-i-1; j++)
                if (arr[j] > arr[j+1]) {
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
    }
}
```

### Selection sort 

- **Princip** - Najde nejmenší prvek a prohodí ho s prvním prvkem. Poté najde druhý nejmenší prvek a prohodí ho s druhým prvkem, atd.
- **Využití** - Malé pole, kde je třeba jednoduchý algoritmus.

![Selection sort](https://media.geeksforgeeks.org/wp-content/uploads/20240110164310/Selection-Sort-in-Java-660.png)

#### Selection sort Code example

```Java
class SelectionSort {
    void sort(int arr[]) {
        int n = arr.length;
        for (int i = 0; i < n-1; i++) {
            int min_idx = i;
            for (int j = i+1; j < n; j++)
                if (arr[j] < arr[min_idx])
                    min_idx = j;
            int temp = arr[min_idx];
            arr[min_idx] = arr[i];
            arr[i] = temp;
        }
    }
}
```

### Merge sort

- **Princip** - Rozdělí pole na poloviny, dokud nezůstane jednoprvkové pole. Poté se pole spojují a řadí.
- **Využití** - Velké pole, kde je třeba rychlý algoritmus.

![Merge sort](https://media.geeksforgeeks.org/wp-content/uploads/20230713125040/Merge-Sort-in-Java-2-(1)-660.png)

### Quick sort

- **Princip** - Vybere prvek jako pivot a rozdělí pole na dvě části. Pravá část obsahuje prvky větší než pivot, levá část obsahuje prvky menší než pivot.
- **Využití** - Velké pole, kde je třeba rychlý algoritmus.

![Quick sort](https://inprogrammer.com/wp-content/uploads/2023/02/image-48.png)

#### Quick sort Code example

```Java
class GFG {

    static void swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    static int partition(int[] arr, int low, int high)
    {
        int pivot = arr[high];

        int i = (low - 1);

        for (int j = low; j <= high - 1; j++) {

            if (arr[j] < pivot) {

                i++;
                swap(arr, i, j);
            }
        }
        swap(arr, i + 1, high);
        return (i + 1);
    }

    static void quickSort(int[] arr, int low, int high)
    {
        if (low < high) {

            int pi = partition(arr, low, high);

            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }
}
```