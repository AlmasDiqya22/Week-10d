# Week-10d
Tugas Artificial Intelligent and Aplication Week 10

Nama		: Almas Diqya Wafa’
NIM		: 5311421005
Prodi		: Teknik Elektro
Mata Kuliah            	: Artificial Intellegent and Aplication
Rombel	            : Senin 09.00

MODUL 4
“Teknik Pencarian Blind Search”

4.	Ubahlah kode program di atas sehingga bentuk tree seperti Gambar 4.7 dapat dibentuk. Kemudian tentukan bagaimana algoritma BFS dapat menemukan node C.
Program:
import java.util.ArrayDeque; 
import java.util.ArrayList; 
import java.util.HashMap; 
import java.util.List; 
import java.util.Map; 
import java.util.Queue; 
import java.util.Set; 

public class AdjacencyList 
{ 
public enum NodeColour { WHITE, GRAY, BLACK } 
public static class Node 
{ 
char data; 
int distance; 
NodeColour colour; 
public Node(int data) 
{ 
            this.data = (char) data; 
        } 
        
    /**
     *
     * @return
     */
    @Override
        public String toString() 
        { 
         return "(" + data + ",d=" + distance + ")"; 
        } 
    } 
    
    Map<Node, List<Node>> nodes; 
 
    public AdjacencyList() 
    { 
        nodes = new HashMap<>(); 
    } 
    
    public void addEdge(Node n1, Node n2) 
    { 
        if (nodes.containsKey(n1)) { 
            nodes.get(n1).add(n2); 
        } else { 
       ArrayList<Node> list = new ArrayList<>(); 
            list.add(n2); 
            nodes.put(n1, list); 
        } 
    } 
    
    public void bfs(Node s) 
    { 
        Set<Node> keys = nodes.keySet(); 
        for (Node u : keys) { 
            if (u != s) { 
                u.colour = NodeColour.WHITE; 
                u.distance = Integer.MAX_VALUE; 
            } 
        } 
        s.colour = NodeColour.GRAY; 
        s.distance = 0; 
        Queue<Node> q = new ArrayDeque<>(); 
        q.add(s); 
        while (!q.isEmpty()) { 
            Node u = q.remove(); 
            List<Node> adj_u = nodes.get(u); 
            if (adj_u != null) { 
                for (Node v : adj_u) { 
                    if(v.colour == NodeColour.WHITE) { 
                        v.colour = NodeColour.GRAY; 
                        v.distance = u.distance + 1; 
                        q.add(v); 
                    } 
                } 
            } 
            u.colour = NodeColour.BLACK; 
            System.out.print(u + " "); 
        } 
    } 
    public static void main(String[] args) { 
    AdjacencyList graph = new AdjacencyList(); 
    Node n1 = new Node('A'); 
    Node n2 = new Node('B'); 
    Node n3 = new Node('C'); 
    Node n4 = new Node('D'); 
    Node n5 = new Node('E'); 
    Node n6 = new Node('F'); 
    Node n7 = new Node('G'); 
    Node n8 = new Node('H'); 
    Node n9 = new Node('I'); 
    
    
    graph.addEdge(n1, n2); 
    graph.addEdge(n1, n4); 
    graph.addEdge(n2, n6); 
    graph.addEdge(n2, n1); 
    graph.addEdge(n2, n4); 
    graph.addEdge(n3, n4); 
    graph.addEdge(n3, n5);
    graph.addEdge(n4, n2); 
    graph.addEdge(n4, n3);
    graph.addEdge(n4, n5); 
    graph.addEdge(n5, n4);
    graph.addEdge(n5, n3); 
    graph.addEdge(n6, n2);
    graph.addEdge(n6, n7); 
    graph.addEdge(n7, n6);
    graph.addEdge(n7, n9); 
    graph.addEdge(n8, n9); 
    graph.addEdge(n9, n8); 
      
    
    graph.bfs(n6); 
    }
}

Hasil:
Setelah melakukan praktikum menggunakan software Netbeans dan melakukan uji coba pada Modul 4 (nomor 4) ditemukan hasil sebagai berikut.
(F,d=0) (B,d=1) (G,d=1) (A,d=2) (D,d=2) (I,d=2) (C,d=3) (E,d=3) (H,d=3) BUILD SUCCESSFUL (total time: 0 seconds)

Penjelasan:
Dalam algoritma BFS yang dijalankan pada graf yang diberikan, pencarian dimulai dari simpul 'F' (n6) sebagai simpul awal. Berikut adalah langkah-langkah algoritma BFS dalam menemukan node 'C':

1. *Node F (d=0):* BFS dimulai dari simpul n6 dengan jarak 0.
2. *Node B (d=1):* n6 memiliki dua anak, yaitu n2 dan n7. BFS melanjutkan ke n2 dengan jarak 1.
3. *Node G (d=1):* n6 juga memiliki anak n7. Namun, n7 sudah diwarnai GRAY dalam proses BFS, sehingga BFS tidak melanjutkan ke n7.
4. *Node A (d=2):* n2 memiliki dua anak, yaitu n1 dan n4. BFS melanjutkan ke n1 dengan jarak 2.
5. *Node D (d=2):* n2 juga memiliki anak n4. Namun, n4 sudah diwarnai GRAY, jadi BFS tidak melanjutkan ke n4.
6. *Node I (d=2):* n7 memiliki satu anak, yaitu n9. BFS melanjutkan ke n9 dengan jarak 2.
7. *Node C (d=3):* n3 adalah tetangga dari n4. BFS melanjutkan ke n3 dengan jarak 3.

Dengan demikian, algoritma BFS pada graf di atas menemukan node C dengan jarak 3 dari node awal, note F.


