# Breadth-First-Search Algorithm
## Tujuan
1. Mahasiswa mampu memahami konsep blind search dan dapat mengimplementasikan program
salah satu algoritma blind search pada kasus tree.
## Dasar Teori
Breadth first search (BFS) adalah algoritma pencarian yang dimulai dari satu node dan menyelidiki semua node yang dapat dicapai dari node tersebut sebelum menyelidiki node yang lebih jauh. BFS sering digunakan untuk menemukan jalur terpendek antara dua node dalam sebuah graph.
BFS menggunakan queue untuk menyimpan node-node yang belum dieksplorasi. Node akar dimasukkan ke dalam queue, dan kemudian node yang paling depan dalam queue dieksplorasi. Setelah node dieksplorasi, semua node yang berdekatan dengan node tersebut dimasukkan ke dalam queue. Proses ini diulangi hingga semua node dalam graph telah dieksplorasi.
## Code
Pada code di bawah "addEdge(Node n1, Node n2)" adalah method untuk menghubungkan dua buah edge sedangkan method "bfs(Node s)" adalah method untuk menentukan titik dimulai teknik pencarian menggunakan algoritma Breadth First Search.

    package JavaApplication1;
            
    public class JavaApplication1
    {  
      public static void main(String[] args) 
      {
      }         
    }

code di atas adalah main file pada code java. Untuk code algoritma BFS ditunjukkan oleh code di bawah.

    package JavaApplication1;
    import java.util.ArrayDeque;
    import java.util.ArrayList;
    import java.util.HashMap;
    import java.util.List;
    import java.util.Map;
    import java.util.Queue;
    import java.util.Set;
    
    public class AdjacencyList {
        public enum NodeColour 
        {
            WHITE, GRAY, BLACK
    }
    
    public static class Node {
        int data;
        int distance;
        Node predecessor;
        NodeColour colour;
    
    public Node(int data)
    
    {
          this.data = data;
    }
    
        public String toString() {
            return "(" + data + ",d=" + distance + ")";
        }
    }
    
    Map<Node, List<Node>> nodes;
    
    public AdjacencyList()
    {
    nodes = new HashMap<Node, List<Node>>();
    }
    
    public void addEdge(Node n1, Node n2) {
        if (nodes.containsKey(n1)) {
            nodes.get(n1).add(n2);
        } else {
            ArrayList<Node> list = new ArrayList<Node>();
            list.add(n2);
            nodes.put(n1, list);
        }
    }
    
    public void bfs(Node s) {
        Set<Node> keys = nodes.keySet();
        for (Node u : keys) {
            if (u != s) {
                u.colour = NodeColour.WHITE;
                u.distance = Integer.MAX_VALUE;
                u.predecessor = null;
            }
        }
        s.colour = NodeColour.GRAY;
        s.distance = 0;
        s.predecessor = null;
        Queue<Node> q = new ArrayDeque<Node>();
        q.add(s);
        while (!q.isEmpty()) {
            Node u = q.remove();
            List<Node> adj_u = nodes.get(u);
            if (adj_u != null) {
                for (Node v : adj_u) {
                    if (v.colour == NodeColour.WHITE) {
                        v.colour = NodeColour.GRAY;
                        v.distance = u.distance + 1;
                        v.predecessor = u;
                        q.add(v);
                    }
                }
            }
            u.colour = NodeColour.BLACK;
            System.out.print(u + " ");
        }
    }
    
    public static void main(String[] args)
    
    {
        AdjacencyList graph = new AdjacencyList();
        Node n1 = new Node(1);
        Node n2 = new Node(2);
        Node n3 = new Node(3);
        Node n4 = new Node(4);
        Node n5 = new Node(5);
        Node n6 = new Node(6);
        Node n7 = new Node(7);
        Node n8 = new Node(8);
        
        graph.addEdge(n1, n2);
        
        graph.addEdge(n2, n1);
        graph.addEdge(n2, n3);
        
        graph.addEdge(n3, n4);
        graph.addEdge(n3, n2);
        
        graph.addEdge(n4, n3);
        graph.addEdge(n4, n5);
        graph.addEdge(n4, n6);
        
        graph.addEdge(n5, n4);
        graph.addEdge(n5, n6);
        graph.addEdge(n5, n7);
        
        graph.addEdge(n6, n4);
        graph.addEdge(n6, n5);
        graph.addEdge(n6, n7);
        graph.addEdge(n6, n8);
        
        graph.addEdge(n7, n5);
        graph.addEdge(n7, n6);
        graph.addEdge(n7, n8);
        
        graph.addEdge(n8, n6);
        graph.addEdge(n8, n7);
        
        graph.bfs(n3);
      }
    }

## Tugas
1. Tentukan bagaimana algoritma BFS di atas dapat menentukan node ke 8, 6, dan 7.
2. Ubahlah method static void main sehingga bentuk tree seperti Gambar 4.5 dapat dibentuk.
Kemudian tentukan bagaimana algoritma BFS dapat menemukan node 5.

4. Ubahlah method static void main sehingga bentuk tree seperti Gambar 4.6 dapat dibentuk.
Kemudian tentukan bagaimana algoritma BFS dapat menemukan node 9.

6. Ubahlah kode program di atas sehingga bentuk tree seperti Gambar 4.7 dapat dibentuk. Kemudian
tentukan bagaimana algoritma BFS dapat menemukan node C.

## Jawaban
1. Pada code yang diberikan di hasilkan output

   (3,d=0) (4,d=1) (2,d=1) (5,d=2) (6,d=2) (1,d=2) (7,d=3) (8,d=3)

   Hasil di atas di dapatkan di karenakan code "graph.bfs(n3);" yang berarti mulai melakukan algoritma BFS dari node 3 sehingga node 3 merupakan tingkat atau di kedalaman palinga atas maka node 3 depth 0. node ke 8, 6, dan 7 ditentukan mempunyai depth (6,d=2), (7,d=3), (8,d=3) dengan menggunakan array queue dan visited. Pertama dimulai dari node 3 disimpan dalam queue setelah sudah di datangi makan di simpan kedalam array visited lalu akan pindah ke depth ke-1 dari depth ke-0 karena tetangga 3 adalah 4 dan 2 maka node 4 dan 2 masuk ke queue ketika node 4 sudah di datangi maka node 4 di simpan dalam array visited dengan depth ke-1 setelah node 4 queue selanjutnya adalah 2 ketika dua sudah di datangi maka node 2 akan dimasukkan ke dalam array visited dengan depth 1. Dari node 2 pencarian berlanjut ke depth 2 dimulai dari tetangga 4 yaitu 3, 5, dan 6 karena 3 sudah pernah di datangi maka queue akan berisi 5 dan 6 di tambah dengan tetangga dari 2 yaitu 1 dan 3 karena 3 sudah di datangi maka queue dari tetangga 2 hanya node 1. Queue dari depth 2 adalah 5, 6, dan 1 setelah semua di datangi maka node 5, 6, dan 1 akan di masukkan kedalam array visited. Selanjutnya pencarian dilakukan di depth ke 3 dengan tetangga dari node 5 adalah 4, 6, dan 7. Tetangga dari node 6 adalah 4, 5, 7, 8. Tengga dari node 1 adalah 2 maka queue pada depth 3 adalah 7 dan 8 saja karena node lain sudah pernh di datangi ketika 7 dan 8 sudah di datangi maka node 7 dan 8 akan di masukkan kedalam array visited dengan depth 3.

2. 