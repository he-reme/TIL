# PRIM 알고리즘

> 정점 중심 → 인접행렬, 인접리스트로 해결

* KRUSKAL 알고리즘보다 시간이 덜 걸림
  * 정점 중심의 해결이므로

<br>

#### 하나의 정점에서 연결된 간선들 중에 하나씩 선택하면서 MST를 만들어 가는 방식

1. 임의 정점을 하나 선택해서 시작
2. 선택한 정점과 인접한 정점들 중의 최소 비용의 간선이 존재하는 정점을 선택 ★
3. 모든 정점이 선택될 때까지 **1, 2** 과정을 반복 (V개)

<br>

#### 서로소인 2개의 집합(2 disjoint-sets) 정보를 유지

* 트리 정점들(tree vertices) - MST를 만들기 위해 선택된 정점들
* 비트리 정점들(non-tree vertices) - 선택되지 않은 정점들

<br>

---

<br>

## 예시 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class MST_PrimTest {

	public static void main(String[] args) throws Exception {
		BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
		
		int N = Integer.parseInt(in.readLine());
		int[][] adjMatrix = new int[N][N];
		boolean[] visited = new boolean[N];
		int[] minEdge = new int[N];
		
		StringTokenizer st = null;
		for(int i=0; i<N; i++) {
			st = new StringTokenizer(in.readLine(), " ");
			for(int j=0; j<N; j++) {
				adjMatrix[i][j] = Integer.parseInt(st.nextToken());
			}
			minEdge[i] = Integer.MAX_VALUE;
		}

		int result = 0; // 최소신장트리 비용
		minEdge[0] = 0; // 임의의 시작점 0 의 간선비용을 0으로 세팅
		
		for(int i=0; i<N; i++) {
			
			// 1. 신장트리에 포함되지 않은 정점 중 최소 간선 비용의 정점 찾기
			int min = Integer.MAX_VALUE;
			int minVertex = -1; // 최소 간선 비용의 정점번호
			for(int j=0; j<N; j++) {
				if(!visited[j] && min>minEdge[j]) {
					min = minEdge[j];
					minVertex = j;
				}
			}
			
			visited[minVertex] = true; // 신장트리에 포함시킴
			result += min; // 간선비용 누적
			
			
			// 2. 선택된 정점 기준으로 신장트리에 연결되지 않은 타 정점과의 간선 비용 최소로 업데이트
			for(int j=0; j<N; j++) {
				
				// 아직 신장트리에 포함되어있지 않은 정점, 연결되어있는 정점, 
				// 이전 간선비용보다 현재 간선 비용이 더 적은 경우
				if(!visited[j] && adjMatrix[minVertex][j]!=0 
						&& minEdge[j]>adjMatrix[minVertex][j]) {
					minEdge[j] = adjMatrix[minVertex][j];
				}
			}
			
		}
		System.out.println(result);
		
	}

}

```

