
# 1.A星

> 适用矩阵

![[Pasted image 20260220150415.png]]

```cpp
#include<iostream>
#include<vector>
#include<queue>
#include<cmath>
#include<ctime>
#include<random>
#include<chrono>
using namespace std;

//grid[i][j]==0表示障碍
//grid[i][j]==1表示移动

int Dijkstra(vector<vector<int>>&grid,int startX,int startY,int targetX,int targetY){
    if(grid[startX][startY]==0||grid[targetX][targetY]==0)return -1;
    vector<int>move{-1,0,1,0,-1};
    int n=grid.size(),m=grid[0].size();
    vector<vector<int>>distance(n,vector<int>(m,INT_MAX));
    distance[startX][startY]=0;
    vector<vector<bool>>visited(n,vector<bool>(m,false));
    auto cmp=[](const vector<int>&a,const vector<int>&b){return a[2]>b[2];};
    priority_queue<vector<int>,vector<vector<int>>,decltype(cmp)>wait(cmp);
    wait.push({startX,startY,0});
    while(!wait.empty()){
        vector<int>cur=wait.top();
        wait.pop();
        int x=cur[0],y=cur[1];
        if(x==targetX&&y==targetY)return distance[x][y];
        if(visited[x][y])continue;
        visited[x][y]=true;
        for(int i=0;i<4;i++){
            int nx=x+move[i], ny=y+move[i+1];
            if(nx>=0&&nx<n&&ny>=0&&ny<m&&grid[nx][ny]==1
            &&distance[nx][ny]>distance[x][y]+1){
                distance[nx][ny]=1+distance[x][y];
                wait.push({nx,ny,distance[nx][ny]});
            }
        }
    }
    return -1;
}

//曼哈顿距离
int f1(int x,int y,int targetX,int targetY){
    return (int)(fabs(x-targetX)+fabs(y-targetY));
}

//对角线距离
int f2(int x,int y,int targetX,int targetY){
    return (int)max(fabs(x-targetX),fabs(y-targetY));
}

int AStar(vector<vector<int>>&grid,int startX,int startY,int targetX,int targetY){
    if(grid[startX][startY]==0||grid[targetX][targetY]==0)return -1;
    vector<int>move{-1,0,1,0,-1};
    int n=grid.size(),m=grid[0].size();
    vector<vector<int>>distance(n,vector<int>(m,INT_MAX));
    distance[startX][startY]=0;
    vector<vector<bool>>visited(n,vector<bool>(m,false));
    auto cmp=[](const vector<int>&a,const vector<int>&b){return a[2]>b[2];};
    priority_queue<vector<int>,vector<vector<int>>,decltype(cmp)>wait(cmp);
    wait.push({startX,startY,f1(startX,startY,targetX,targetY)});
    while(!wait.empty()){
        vector<int>cur=wait.top();
        wait.pop();
        int x=cur[0],y=cur[1];
        if(x==targetX&&y==targetY)return distance[x][y];
        if(visited[x][y])continue;
        visited[x][y]=true;
        for(int i=0;i<4;i++){
            int nx=x+move[i], ny=y+move[i+1];
            if(nx>=0&&nx<n&&ny>=0&&ny<m&&grid[nx][ny]==1
            &&distance[nx][ny]>distance[x][y]+1){
                distance[nx][ny]=1+distance[x][y];
                wait.push({nx,ny,distance[nx][ny]+f1(nx,ny,targetX,targetY)});
            }
        }
    }
    return -1;
}

vector<vector<int>> createRandomGrid(int n,int m){
    vector<vector<int>>grid(n,vector<int>(m));
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            grid[i][j]=rand()%2;
        }
    }
    return grid;
}

//功能测试 
void FunctionTest(int MAXN,int MAXM,int times){
    cout<<"FunctionTest starts running..."<<endl;
    srand(time(nullptr));
    for(int i=0;i<times;i++){
        int n=rand()%MAXN+1,m=rand()%MAXM+1;
        int targetX=rand()%n,targetY=rand()%m;
        int startX=rand()%n,startY=rand()%m;
        vector<vector<int>>grid=createRandomGrid(n,m);
        int res1=Dijkstra(grid,startX,startY,targetX,targetY);
        int res2=AStar(grid,startX,startY,targetX,targetY);
        if(res1!=res2){
            cout<<"未通过测试样例数据输入："<<endl;
            for(auto&i:grid){
                for(auto&j:i)cout<<j<<" ";
                cout<<endl;
            }
            cout<<"未通过测试样例数据输出："<<endl;
            cout<<"Dijkstra:"<<res1<<endl;
            cout<<"AStar:"<<res2<<endl;
            return;
        }
    }
    cout<<"测试样例都通过"<<endl;
    cout<<"FunctionTest ends..."<<endl;
}

//性能测试
void PerformanceTest(int n,int m){
    cout<<"PerformanceTest starts running..."<<endl;
    int targetX=rand()%n,targetY=rand()%m;
    int startX=rand()%n,startY=rand()%m;
    vector<vector<int>>grid=createRandomGrid(n,m);
    auto start = std::chrono::high_resolution_clock::now();
    int res1=Dijkstra(grid,startX,startY,targetX,targetY);
    auto end = std::chrono::high_resolution_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start);
    cout<<"Dijkstra result:"<<res1<<",cost time:"<<duration.count()<<endl;
    start = std::chrono::high_resolution_clock::now();
    int res2=AStar(grid,startX,startY,targetX,targetY);
    end = std::chrono::high_resolution_clock::now();
    duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start);
    cout<<"AStar result:"<<res2<<",cost time:"<<duration.count()<<endl;
    cout<<"PerformanceTest ends..."<<endl;
}

int main(){
    FunctionTest(10,10,100);
    cout<<endl;
    PerformanceTest(10,10);
    return 0;
}
```

# 2.Floyd

> 有向图和无向图

![[Pasted image 20260220180014.png]]

[记录详情 - 洛谷 | 计算机科学教育新生态](https://www.luogu.com.cn/record/263386037)

```cpp
#include<iostream>
using namespace std;

int n,m;
int path[101];
int grid[101][101];

void Floyd(){
    for(int bridge=1;bridge<=n;bridge++){
        for(int i=1;i<=n;i++){
            for(int j=1;j<=n;j++){
                if(grid[i][bridge]+grid[bridge][j]<grid[i][j]){
                    grid[i][j]=grid[i][bridge]+grid[bridge][j];
                }
            }
        }
    }
}

int main(){
    cin>>n>>m;
    for(int i=1;i<=m;i++)cin>>path[i];
    for(int i=1;i<=n;i++){
        for(int j=1;j<=n;j++){
            cin>>grid[i][j];
        }
    }
    Floyd();
    int ans=0;
    for(int i=1;i<m;i++)ans+=grid[path[i]][path[i+1]];
    cout<<ans<<endl;
    return 0;
}
```

# 3.Bellman-Ford

# 4.SPFA