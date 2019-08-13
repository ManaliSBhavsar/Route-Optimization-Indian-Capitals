# basicrepo
import googlemaps 
 
#Class to represent a graph 
class Graph: 
  
    '''To find the  
     vertex with minimum distance from 
     the set of vertices still present in the queue''' 
    def minDistance(self,dist,queue): 
        # Initialize min value and min_index as -1 
        minimum = float("Inf") 
        min_index = -1
          
        # from the dist array,pick one which 
        # has min value and is till in queue 
        for i in range(len(dist)): 
            if dist[i] < minimum and i in queue: 
                minimum = dist[i] 
                min_index = i 
        return min_index 
  
  
    '''To print shortest path from source to vertex j using parent array
       Parent array has the shortest path'''
    def printPath(self, parent, j): 
          
        #If j is source 
        if parent[j] == -1 :  
            print (my_list[j]) 
            return
        self.printPath(parent , parent[j]) 
        print (my_list[j])
          
  
    '''To print source, destination and the distance from source'''
    def printSolution(self, dist, parent): 
        src = p
        print("Source-->Destination\tDistance from Source") 
        for i in range(0, len(dist)): 
            if(i!=src):
                print("\n%s --> %s \t\t%d" % (my_list[src], my_list[i], dist[i]),"\nPath:"),
                self.printPath(parent,i)
            
  
  
    '''Function for Dijkstra's single source shortest path 
    algorithm using given matrix'''
    def dijkstra(self, graph, src): 
  
        row = len(graph) 
        col = len(graph[0]) 
  
        '''The output array. dist[i] will hold the shortest distance from src to i '''
        '''Initialize all distances as INFINITE ''' 
        dist = [float("Inf")] * row 
  
        '''Parent array stores shortest path'''
        parent = [-1] * row 
  
        '''Distance of source vertex from itself is always 0'''
        dist[src] = 0
      
        '''Add all vertices in queue'''
        queue = [] 
        for i in range(row): 
            queue.append(i) 
              
        '''To find shortest path for all vertices''' 
        while queue: 
  
            '''Pick the minimum dist vertex from the set of vertices still in queue''' 
            u = self.minDistance(dist,queue)  
  
            '''remove min element'''    
            queue.remove(u) 
  
            '''Update dist value and parent index of the adjacent vertices of the picked vertex. Consider only those vertices which are still in queue '''
            for i in range(col): 
                '''Update dist[i] only if the vertex is in queue and there is 
                an edge from u to i, and total weight of path from 
                src to i through u is smaller than current value of 
                dist[i]'''
                if graph[u][i] and i in queue: 
                    if dist[u] + graph[u][i] < dist[i]: 
                        dist[i] = dist[u] + graph[u][i] 
                        parent[i] = u 
  
  
        '''print the distance array '''
        self.printSolution(dist,parent) 


print("\n")

graph=[]
my_list=['Mumbai','Hyderabad','Itanagar','Dispur','Patna','Raipur','Panaji','Gandhinagar','Chandigarh',
 'Shimla','Ranchi','Bengaluru','Thiruvananthapuram','Bhopal','Imphal','Shillong','Aizawl',
 'Kohima','Bhubaneswar','Jaipur','Gangtok','Chennai','Hyderabad','Agartala','Lucknow','Dehradun',
 'Kolkata']

print("\n\n")
gmaps = googlemaps.Client(key='AIzaSyDBEl7ncacJKadv_lzHs_HI6z_nKmn5bTs') 
g=Graph()

distance1=[]

for i in range (len(my_list)):
    for j in range (len(my_list)):
        distance1.append(gmaps.distance_matrix(my_list[i],my_list[j])['rows'][0]['elements'][0]['distance']['value'])
        
for l in range(len(distance1)):
    print(distance1[l])

print("\n\n")
    
    
m=0
for i in range (len(my_list)):
    a=[]
    for j in range(len(my_list)):
        a.append(distance1[m]/1000)
        m=m+1
    graph.append(a)
        
for i in range(len(my_list)): 
    for j in range(len(my_list)): 
        print(graph[i][j], end = "   ") 
    print() 

print("\nEnter source:")
s=input()
for i in range(len(my_list)):
    if(my_list[i]==s):
        p=i
        break

g.dijkstra(graph,p)









