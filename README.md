# CMS_ICS

## Jupyter Notebook:
Pour lancer le script de visualisation de graphe il faut:
1. lancer la commande `%pip install pyvis` dans un kernel à part
2. Ouvrir un nouveau kernel
3. Executer la fonction `Graph(G, s, oriente)`
- G: liste d'adjacence de type ´dict´ ex: ´{0:[1,2,3], 1:[0,2,3], 2:[0,1,3], 3:[0,1,2]}´
- s: sommet de départ de type ´int´
- oriente: graphe orienté ou non de type ´bool´


Exemple:
```python
G2={0:[1,4],1:[2],2:[0,3],3:[],4:[3],5:[],6:[5]}

def Graph(G, s=0, oriente=False):

  from pyvis.network import Network
  import networkx as nx
  from IPython.display import display, HTML

  nodes_id = list(range(0,len(G)))
  nodes_label = [str(i) for i in range(0,len(G))]
  nodes_id.remove(s)
  nodes_label.remove(str(s))
  
  graph = Network(notebook = True,
              directed=oriente,
              cdn_resources='in_line')
  
  
  graph.add_node(s,label=str(s),color="red")
  graph.add_nodes(nodes_id,label=nodes_label)
  for v,es in G.items():
      for e in es:
          graph.add_edge(v,e)
          
  graph.toggle_physics(True)
  graph.show("graph.html")
  
  with open('graph.html', 'r') as file:
      html_content = file.read()
  display(HTML(html_content))
  
Graph(G2,6)
```
