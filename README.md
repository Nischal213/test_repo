graph_with_heuristics = {
    'A': [("B", 1, 6), ('C', 4, 2)],
    'B': [('C', 2, 2), ('D', 5, 1)],
    'C': [('B', 2, 6), ('D', 1, 1)],
    'D': [('C', 1, 2), ('E', 3, 0)],
    'E': []
}


def a_star_search(graph , start , end):
    previous_distance = 0
    shortest_path = [start]
    unvisited = [i for i in graph.keys() if i != start]
    while True:
      open_set = [i for i in graph[start]]
      smallest_node = None
      smallest_distance = (float("inf") , 0)
      for node , weight , heuristic in open_set:
        if node in unvisited:
          unvisited.remove(node)
          if node == end:
            shortest_path.append(end)
            return "".join([f"{i} -> " if i != end else f"{i}" for i in shortest_path])
          if weight + heuristic + previous_distance < smallest_distance[0]:
              smallest_node = node
              smallest_distance = (weight + heuristic + previous_distance , heuristic)
      start = smallest_node
      if start is None:
        return "".join([f"{i} -> " if i != end else f"{i}" for i in shortest_path])
      shortest_path.append(start)
      previous_distance = smallest_distance[0] - smallest_distance[1]
print(a_star_search(graph_with_heuristics_3 , "A" , "F"))


