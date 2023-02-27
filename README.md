# Finding-the-Minimum-Cost
# pyhon
첫째줄에 도시의 개수 n개, 두번째줄에 버스의 개수 m개, 그다음줄부터 m개의 버스의 출발지점,도착지점,비용을 각각 입력하고 마지막줄에 시작지점과 도착지점을 입력하고 입력한 지점까지 가는데 걸리는 버스비용중에서 가장 적은 비용을 출력하는 프로그램을 작성해보자!


다익스트라 알고리즘==> 최단경로 알고리즘
1-출발 노드와, 도착 노드를 설정한다.
2-알고 있는 모든 거리 값을 부여한다.
3-출발 노드부터 시작하여 방문하지 않은 인접 노드를 방문 거리를 계산한 다음 현재 알고있는 거리보다 짧으면 해당 값으로 갱신한다.
4-현재 노드에 인접한 모든 미방문 노드까지의 거리를 계산했다면 현재 노드는 방문한 것이므로 미방문 집합에서 제거한다.
5-도착 노드가 미방문 노드 집합에서 벗어나면 알고리즘을 종료한다.


import sys
import heapq
from sys import maxsize
input=sys.stdin.readline
n=int(input())
m=int(input())
place=[[] for _ in range(n+1)]
distance=[maxsize]*(n+1)
for _ in range(m):
  starts,ends,money=map(int,input().split()) #출발,도착,비용
  place[starts].append((money,ends))
start,end=map(int,input().split())
def check(x): #다익스트라 알고리즘 
  distance[x]=0
  array=[]
  heapq.heappush(array,(0,x))
  while array:
    a,b=heapq.heappop(array) #a=총가격 b=출발지점 
    if distance[b] < a: #기존최소비용보다 크다면 무시 
      continue
    for i,j in place[b]: #i=가격 j=도착지점
      d=a+i #가격을 더해나감 
      if distance[j] > d:
        heapq.heappush(array,(d,j))
        distance[j]=d       
check(start)
print(distance[end])
