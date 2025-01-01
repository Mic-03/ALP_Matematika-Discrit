# Proyek: Implementasi Teori Graf Menggunakan Python
## Deskripsi
Proyek ini bertujuan untuk membuat sistem berbasis Python untuk mempelajari teori graf menggunakan Library NetworkX. Kalian akan membuat kelas dengan metode-metode dasar yang membantu dalam analisis graf, seperti menambah node dan edge, mengecek keterhubungan, menghitung jalur terpendek, dan menampilkan visualisasi graf.
```
import networkx as nx
import matplotlib.pyplot as plt

class Graf:
    def __init__(self):
        self.graph = nx.Graph()

    def add_node(self, node):
        self.graph.add_node(node)

    def add_edge(self, node1, node2, weight=1):
        self.graph.add_edge(node1, node2, weight=weight)

    def visualize_graph(self):
        pos = nx.spring_layout(self.graph)
        weights = nx.get_edge_attributes(self.graph, 'weight')
        nx.draw(self.graph, pos, with_labels=True, node_color='lightblue', node_size=500, font_size=10, font_weight='bold')
        nx.draw_networkx_edge_labels(self.graph, pos, edge_labels=weights)
        plt.show()

    def shortest_path(self, source, target):
        try:
            path = nx.shortest_path(self.graph, source=source, target=target, weight='weight')
            return path
        except nx.NetworkXNoPath:
            return f"No path exists between {source} and {target}."

    def visual_shortest_path(self, source, target):
        try:
            path = self.shortest_path(source, target)
            if isinstance(path, str):
                print(path)
                return

            subgraph = self.graph.subgraph(path)
            pos = nx.spring_layout(self.graph)
            nx.draw(self.graph, pos, with_labels=True, node_color='lightblue', node_size=500, font_size=10, font_weight='bold')
            nx.draw(subgraph, pos, with_labels=True, edge_color='red', node_color='orange', width=2, node_size=600)
            plt.show()
        except nx.NetworkXNoPath:
            print(f"No path exists between {source} and {target}.")

    # Metode tambahan:

    def is_connected(self):
        """Cek apakah graf terhubung."""
        return nx.is_connected(self.graph)

    def node_degree(self, node):
        """Kembalikan derajat node tertentu."""
        if node in self.graph:
            return self.graph.degree[node]
        else:
            return f"Node {node} tidak ada dalam graf."

    def clustering_coefficient(self):
        """Menghitung koefisien clustering untuk setiap node."""
        return nx.clustering(self.graph)

    def find_bridges(self):
        """Mencari edge yang merupakan bridge (penghubung kritis)."""
        return list(nx.bridges(self.graph))

    def find_articulation_points(self):
        """Mencari articulation points (node kritis)."""
        return list(nx.articulation_points(self.graph))
```
## Implementasi
Membuat Object
```
graph = Graf()
```
Menambah Node (Titik)
```
graph.add_node(1)
graph.add_node(2)
graph.add_node(3)
graph.add_node(4)
graph.add_node(5)
```
Menambah Sisi (Edge)
```
graph.add_edge(1, 2, weight=4.5)
graph.add_edge(1, 3, weight=3.2)
graph.add_edge(2, 4, weight=2.7)
graph.add_edge(3, 4, weight=1.8)
graph.add_edge(1, 4, weight=6.7)
graph.add_edge(3, 5, weight=2.7)
```
Visualisasi Graf
```
graph.visualize_graph()
```
Jalur Terpendek
```
path = graph.shortest_path(1, 5)
print(path)
```
Hasil:
```
[1, 3, 5]
```
Visualisasi Jalur Terpendek
```
graph.visual_shortest_path(1, 5)
```
## Instruksi Tambahan

Tambahkan 5 metode tambahan yang dapat membantu dalam manipulasi dan analisis graf, seperti:

- Cek apakah graf terhubung.

- Menghitung derajat node tertentu.

- Menghitung koefisien clustering.

- Menemukan bridge.

- Menemukan articulation points.
