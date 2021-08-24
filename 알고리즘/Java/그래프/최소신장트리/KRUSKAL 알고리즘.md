# KRUSKAL 알고리즘

> 간선 중심

<br>

#### 간선을 하나씩 선택해서 MST를 찾는 알고리즘

1. 최초, 모든 간선을 가중치에 따라 **오름차순**으로 정렬
2. 가중치가 가장 낮은 간선부터 선택하면서 트리를 증가시킴
   * 사이클이 존재하면 다음으로 가중치가 낮은 간선 선택
3. n-1 개의 간선이 선택될 때까지 **2**를 반복

<br>

#### 서로소 집합을 적용해서 예시를 보여주면..

* 간선을 하나씩 선택하면서 트리를 완성해 나가는 느낌!!

1. Make-Set 으로 정점에 대한 모든 집합 생성

2. 오름차순 정렬한 간선을 하나씩 선택하면서 Union 시도

3. Union을 시도하다가 실패했을 때

   * 같은 집합을 만나게 됐을 때 

   * 사이클 발생
   * 사이클 방생하면 트리가 될 수 없으므로 해당 간선은 사용하지 않음!

4. 계속 나머지 간선에도 Union 시도~

5. 정점의 수가 N이라면, N-1개 Union 성공시 신장트리 완성!

<br>

---

<br>

## 예시 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class MST_KruskalTest {

	static class Edge implements Comparable<Edge>{
		
		int start, end, weight;

		public Edge(int start, int end, int weight) {
			super();
			this.start = start;
			this.end = end;
			this.weight = weight;
		}

		@Override
		public int compareTo(Edge o) {
			return Integer.compare(this.weight, o.weight);
		}	
	}
	
	static int[] parents; // 부모 원소를 관리 (트리처럼 사용)

	// 모든 원소를 자신을 대표자로 만듦
	private static void make() {
		
		parents = new int[V];
		
		for(int i=0; i<V; i++)
			parents[i] = i;
	}
	
	// a가 속한 집합의 대표자 찾기
	private static int find(int a) {
		if(a==parents[a]) return a; // 자신이 대표자

		// 자신이 속한 집합의 대표자를 자신의 부모로 : path compression
		return parents[a] = find(parents[a]);
	}
	
	// 두 원소를 하나의 집합으로 합치기 (대표자를 이용해서 합침)
	private static boolean union(int a, int b) {
		int aRoot = find(a);
		int bRoot = find(b);
		
		// 이미 같은 집합인 경우, 합치지 않음
		if(aRoot == bRoot) return false;
	
		parents[bRoot] = aRoot;
		return true;
	}
	
	static int V, E;
	static Edge[] edgeList;
	public static void main(String[] args) throws IOException {
		BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(in.readLine(), " ");
		V = Integer.parseInt(st.nextToken());
		E = Integer.parseInt(st.nextToken());

		// 간선리스트 작성
		edgeList = new Edge[E];
		
		for(int i=0; i<E; i++) {
			st = new StringTokenizer(in.readLine(), " ");
			int start = Integer.parseInt(st.nextToken());
			int end = Integer.parseInt(st.nextToken());
			int weight = Integer.parseInt(st.nextToken());
			edgeList[i] = new Edge(start, end, weight);
		}
		
		// 1. 오름차순 정렬
		Arrays.sort(edgeList);
		
		// 2. 모든 정점을 각각의 집합으로 만들고 출발
		make(); 
		
		// 3. 간선 하나씩 시도하며 트리 만들어 감.
		int cnt = 0, result = 0;
		for(Edge edge : edgeList) {
			if(union(edge.start, edge.end)) {
				result += edge.weight;
				if(++cnt == V-1) break; // 신장트리 완성
			}
		}
		System.out.println(result);
	}
	
}

```

