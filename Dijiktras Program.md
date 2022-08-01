```java
    private int[] dijiktras(ArrayList<Edge> adj[], int i, int n) {
        int distance[] = new int[n];
        Arrays.fill(distance, Integer.MAX_VALUE);
        PriorityQueue<Edge> pq = new PriorityQueue<>();
        distance[i] = 0;
        pq.add(new Edge(-1, i, 0));
        boolean vis[] = new boolean[n];
        while(!pq.isEmpty()) {
            Edge e = pq.poll();
            vis[e.to] = true;
            for(Edge p : adj[e.to]) {
                if(distance[p.to] > e.distance + p.distance) {
                    distance[p.to] = e.distance + p.distance;
                }
                if(!vis[p.to]) {
                    pq.add(new Edge(e.to, p.to, distance[p.to]));
                }
            }
        }
        return distance;
    }

    class Edge implements Comparable<Edge>{
        int from , to;
        int distance;
        Edge(int from, int to, int distance) {
            this.from=from;
            this.to=to;
            this.distance=distance;
        }
        public int compareTo(Edge e) {
            return Integer.compare(e.distance, distance);
        }
    }
```