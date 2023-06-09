---
layout: post
title: xcpc模板积累
author: Ranok
tag: [算法]
color: brown
permalink: algorithm
feature-img: assets/img/feature-img/algorithm.jpg # 这是一个会出现在博客文章内部的图片
thumbnail: assets/img/thumbnails/feature-img/algorithm.jpg # 文件路径在github还是只支持正斜杠'/'
---

&emsp;&emsp;这是一个竞赛算法模板博客，用于应对xcpc等算法竞赛。此模板不一定是符合大众的模板，我会带有自己的风格。模板我会不断地更新，内容仅供参考。

---
# 目录

- [目录](#目录)
- [算法模板积累](#算法模板积累)
  - [图论](#图论)
    - [单源最短路](#单源最短路)
      - [dijiestal](#dijiestal)
      - [SPFA](#spfa)
    - [多源最短路](#多源最短路)
      - [Floyd](#floyd)
    - [最小生成树](#最小生成树)
      - [prim](#prim)
      - [Kruskar](#kruskar)
    - [spfa负环判断](#spfa负环判断)
    - [差分约束](#差分约束)
    - [最近公共祖先lca](#最近公共祖先lca)
    - [有向图的强连通分量](#有向图的强连通分量)
    - [无向图的强连通分量](#无向图的强连通分量)
      - [e-dcc缩点](#e-dcc缩点)
      - [v-dcc缩边](#v-dcc缩边)
    - [二分图](#二分图)
      - [染色法判断二分图是否合理](#染色法判断二分图是否合理)
      - [匈牙利算法 解 二分图的最大匹配数](#匈牙利算法-解-二分图的最大匹配数)
  - [dp](#dp)
    - [背包问题](#背包问题)
      - [完全背包](#完全背包)
      - [多重背包的二进制优化](#多重背包的二进制优化)
    - [数位dp](#数位dp)
  - [数据结构](#数据结构)
    - [树状数组](#树状数组)
    - [线段树](#线段树)
  - [数学](#数学)
    - [pow](#pow)
    - [矩阵快速幂](#矩阵快速幂)
    - [逆元计算](#逆元计算)
    - [欧拉筛](#欧拉筛)

---
# 算法模板积累

---

## 图论

---

### 单源最短路

---

#### dijiestal
```c++
int head[N],edge[N],Next[N],val[N],tt=0;
void add(int x,int y,int z){
    edge[++tt]=y;
    val[tt]=z;
    Next[tt]=head[x];
    head[x]=tt;
}

int d[N];

struct node{
    int i,d;
    node(int i=0,int d=0):i(i),d(d){}
    bool friend operator<(const node &a,const node &b){
        return a.d>b.d;
    }
};

void dijiestal(int u){
    memset(d,0x3f,sizeof d);
    d[u]=0;

    bool mp[N]={0};
    priority_queue<node>q;
    q.push(node(u,0));
    
    while(!q.empty()){
        node e=q.top();
        q.pop();
        int x=e.i;
        if(mp[x]) continue;
        mp[x]=true;

        for(int i=head[x];i;i=Next[i]){
            int y=edge[i],y_val=val[i];
            if(d[y]>d[x]+y_val){
                d[y]=d[x]+y_val;
                q.push(node(y,d[y]));
            }
        }
    }
}

```

---
#### SPFA

```c++
struct node{
    int val,y;
    node(int y=0,int val=0):val(val),y(y){}
};

vector<node>a[M];
int d[M],b[M];   // b[i]记录在牧场i处有多少只奶牛
int n,p,c;

int spfa(int u){
    memset(d,0x3f,sizeof d);
    d[u]=0;
    queue<int> q;
    q.push(u);
    bool mp[M]={};
    while(!q.empty()){
        int x=q.front();
        q.pop();
        
        mp[x]=false;
        
        for(node &e:a[x]){
            int y=e.y,val=e.val;
            if(d[y]>d[x]+val){
                d[y]=d[x]+val;
                if(!mp[y]){
                    mp[y]=true;
                    q.push(y);
                }
            }
        }
    }
    int res=0;
    for(int i=1;i<=p;i++){
        if(b[i]){
            if(d[i]==MAX) return MAX;
            res+=b[i]*d[i];
        }
    }
    return res;
}
```

---

### 多源最短路

---

#### Floyd

```c++
memeset(d,0x3f,sizeof d);
for(int i=1,x,y,z;i<=m;i++){
    cin>>x>>y>>z;
    d[x][y]=d[y][x]=min(d[x][y],z);
}
for(int k=1;k<=n;i++){
    for(int i=1;i<=n;i++){
        for(int j=1;j<=n;j++)
            d[i][j]=min(d[i][j],d[i][k]+d[k][j]);
    }
}
```

---

### 最小生成树
---

#### prim

```c++
int d[N],n;
int res;    // 最小生成树的总路程长度
int a[N][N];
struct node{
    int i,d;
    bool friend operator<(const node &a,const node &b){
        return a.d>b.d;
    }
};

void prim(int u=1){
    bool mp[N]={0};

    priority_queue<node>q;
    q.push({u,0});

    memset(d,0x3f,sizeof d);
    d[u]=0;

    while(!q.empty()){
        node e=q.top();
        q.pop();
        int x=e.i;

        if(mp[x]) continue;
        mp[x]=true;
        res+=e.d;

        for(int y=1;y<=n;y++){
            if(!mp[y]&&d[y]>a[x][y]){
                d[y]=a[x][y];
                q.push({y,d[y]});
            }
        }
    }
}

```
---
#### Kruskar

```c++
int n,k,sum=0;
int edge[M],head[M],Next[M],val[M],top=0;
int d[N];

int f[N];
int Hash[N]={0};
int get(int x){
    return f[x]==x?x:f[x]=get(f[x]);
}

void mange(int x,int y){
    x=get(x);
    y=get(y);
    if(x!=y){
        f[x]=y;
        Hash[x]=1;
    }
}

void add(int x,int y,int z){
    edge[++top]=y;
    val[top]=z;
    Next[top]=head[x];
    head[x]=top;
}

struct node{
    int i,d;
    node(int i=0,int d=0):i(i),d(d){}
    friend bool operator<(const node &a,const node &b){
        return a.d>b.d;
    }
};

void pirm(int u){
    bool Hash[N]={0};
    memset(d,0x3f,sizeof d);
    priority_queue<node>q;
    q.push(node(u,0));
    d[u]=0;
    while(!q.empty()){
        int x=q.top().i;
        q.pop();
        if(Hash[x]) continue;
        Hash[x]=true;
        sum-=d[x];
        for(int i=head[x];i;i=Next[i]){
            int y=edge[i],z=val[i];
            if(!Hash[y]&&z<d[y]){
                d[y]=z;
                q.push(node(y,d[y]));
            }
        }
    }
}
```
---
### spfa负环判断

输入的第一行是两个整数 N,K。
接下来 K 行，表示分配糖果时需要满足的关系，每行 3 个数字 X,A,B。

1. 如果 X=1．表示第 A 个小朋友分到的糖果必须和第 B个小朋友分到的糖果一样多。
2. 如果 X=2，表示第 A 个小朋友分到的糖果必须少于第 B个小朋友分到的糖果。
3. 如果 X=3，表示第 A 个小朋友分到的糖果必须不少于第 B个小朋友分到的糖果。
4. 如果 X=4，表示第 A 个小朋友分到的糖果必须多于第 B个小朋友分到的糖果。
5. 如果 X=5，表示第 A 个小朋友分到的糖果必须不多于第 B 个小朋友分到的糖果。

小朋友编号从1到 N。
```c++
bool spfa(){
    int d[N],cnt[N]={0};
    bool mp[N];
    queue<int>q;
    for(int i=1;i<=n;i++){
        q.push(i);
        d[i]=INF;
        mp[i]=true;
    }
    while(!q.empty()){
        int x=q.front();
        q.pop();
        mp[x]=false;
        for(int i=head[x];i;i=Next[i]){
            int y=ver[i],z=edge[i];
            if(d[y]>d[x]+z){
                d[y]=d[x]+z;
                cnt[y]=cnt[x]+1;
                if(cnt[y]>=n) return true;
                if(!mp[y]){
                    mp[y]=true;
                    q.push(y);
                }
            }
        }
    }
    return false;
}

```
---
### 差分约束
实质上也是判断负环
```c++
#include<cstring>
#include<iostream>
using namespace std;
typedef long long ll;
const int N=1e5+10;
const int K=3e5+10;
int head[N],Next[K],edge[K],ver[K],tot=0;

void add(int x,int y,int z){
    edge[++tot]=z;
    ver[tot]=y;
    Next[tot]=head[x];
    head[x]=tot;
}

ll d[N]={0};
bool mp[N];
int stc[N]={0},top=0;
int cnt[N]={0};
int n,k;
bool spfa(){
    memset(d,-1,sizeof d);
    d[0]=0;
    stc[top++]=0;
    while(top){
        int x=stc[--top];
        mp[x]=false;
        for(int i=head[x];i;i=Next[i]){
            int y=ver[i],z=edge[i];
            if(d[y]<d[x]+z){
                d[y]=d[x]+z;
                cnt[y]=cnt[x]+1;
                if(cnt[y]>=n+1) return true;
                if(!mp[y]){
                    mp[y]=true;
                    stc[top++]=y;
                }
            }
        }
    }
    return false;
}
int main(){
    int x,y,t;
    scanf("%d %d",&n,&k);
    for(int i=1;i<=k;i++){
        scanf("%d %d %d",&t,&x,&y);
        if(t==1){
            add(x,y,0);
            add(y,x,0);
        }
        else if(t==2){
            add(x,y,1);
        }
        else if(t==3){
            add(y,x,0);
        }
        else if(t==4){
            add(y,x,1);
        }
        else{
            add(x,y,0);
        }
    }
    for(int i=1;i<=n;i++) add(0,i,1);
    if(spfa()){
        puts("-1");
    }
    else{
        ll sum=0;
        for(int i=1;i<=n;i++)
            sum+=d[i];
        printf("%lld\n",sum);
    }
    return 0;
}

```
---
### 最近公共祖先lca
```c++
const int N = 4e4 + 5, M = N << 1;
struct E {
    int v, next;
} e[M];
int n, m, t, len, root, u, v, dep[N], f[N][17], h[N];
void add(int u, int v) {
    e[++len].v = v; e[len].next = h[u]; h[u] = len;
}
void bfs() {        // 初始化
    int q[N],tt=0,hh=0;
    q[tt++]=root;   // 进入一个根节点
    dep[root] = 1, dep[0] = 0;
    while (tt!=hh) {
        int u = q[hh++];
        for (int j = h[u]; j; j = e[j].next) {
            int v = e[j].v;
            if (dep[v]) continue;
            dep[v] = dep[u] + 1;
            q[tt++]=v;
            f[v][0] = u;
            for (int k = 1; k <= t; k++) f[v][k] = f[f[v][k - 1]][k - 1];
        }
    }
}
int lca(int x, int y) { // 返回x，y的最近公共祖先
    if (dep[y] > dep[x]) x=x+y-(y=x);
    for (int i = t; i >= 0; i--) {
        if (dep[f[x][i]] >= dep[y]) x = f[x][i];
    }
    if (x == y) return x;
    for (int i = t; i >= 0; i--) {
        if (f[x][i] != f[y][i]) x = f[x][i], y = f[y][i];
    }
    return f[x][0];
}
```
---
### 有向图的强连通分量
```c++
void tarjan(int x){
    low[x]=dfn[x]=++ti;
    dic[++top]=x;
    mp[x]=true;
    for(int i=head[x];~i;i=Next[i]){
        int y=edge[i];
        if(!dfn[y]){
            tarjan(y);
            low[x]=min(low[x],low[y]);
        }else if(mp[y]) low[x]=min(low[x],dfn[y]);
    }
    if(low[x]==dfn[x]){     // 联通块缩点
        int y;
        ecc_cnt++;
        do{
            y=dic[top--];
            id[y]=ecc_cnt;
            ecc[ecc_cnt].push_back(y);
            mp[y]=false;
        }while(x!=y);
    }
}
```
---
### 无向图的强连通分量
#### e-dcc缩点
```c++
int n,m,dcc_cnt;
int dfn[N],low[N],ti;
int dic[N],top=0;   // 用于记录边

void tarjan(int x,int pre){  // 用于计算桥的算法,pre是边不是点
    dfn[x]=low[x]=++ti;
    dic[top++]=x;

    for(int i=head[x];~i;i=Next[i]){    // 注意这里的i表示head要初始化为-1
        int y=edge[i];
        if(!dfn[y]){    // 这个点没走过
            tarjan(y,i);
            low[x]=min(low[x],low[y]);
            if(dfn[x]<low[y]){  //这里有桥
                mp[i]=mp[i^1]=true;
            }
        }else if(i!=(pre^1)){   // 这个点走过了，但不是父节点
            low[x]=min(low[x],dfn[y]);
        }
    }
    if(dfn[x]==low[x]){ // 说明这个是一个连通域的根结点
        id[x]=++sign;   // 这里将联通域中所有的点压缩为一个点
        for(int y=dic[--top];y!=x;y=dic[--top]) id[y]=sign;
    }
}
```
---

#### v-dcc缩边
```c++
void tarjan(int x){
    low[x]=dfn[x]=++ti;
    dic[++top]=x;
    if(x==root&&head[x]==-1){   // 孤立点
        dcc_cnt++;
        dcc[dcc_cnt].push_back(x);
        return;
    }
    int sign=0;
    for(int i=head[x];~i;i=Next[i]){    // 不是孤立点
        // 注意这里的i表示head要初始化为-1
        int y=edge[i];
        if(!dfn[y]){
            tarjan(y);
            low[x]=min(low[x],low[y]);
            if(dfn[x]<=low[y]){
                sign++;
                if(sign>1||x!=root) mp[x]=true;
                dcc_cnt++;
                int z;
                do{
                    z=dic[top--];
                    dcc[dcc_cnt].push_back(z);
                }while(z!=y);
                dcc[dcc_cnt].push_back(x);
            }
        }
        else low[x]=min(low[x],dfn[y]);
    }
}
```
---
### 二分图
---
#### 染色法判断二分图是否合理
```c++
bool dfs(int x,int c){  // 结点，颜色，阈值
    color[x]=c;
    for(int i=head[x];i;i=Next[i]){
        int y=edge[i],val_y=val[i];
        if(color[y]==color[x]) return false;
        if(!color[y]&&!dfs(y,3-c,mid)) return false;
    }
    return true;
}

bool check(){
    memset(color,0,sizeof color);
    for(int i=1;i<=n;i++){
        if(!color[i]){
            if(!dfs(i,1)) return false;     // 出现矛盾就返回
        }
    }
    return true;
}
```
---
#### 匈牙利算法 解 二分图的最大匹配数
二分图的：
最小覆盖点的数量可以用匈牙利算法求解
最小覆盖点的数量 = 最大匹配数
最大独立集 = 总点数 - 最小覆盖点的数量

```c++
bool mp[M];  // 表示i是否被访问过
int match[M];   // 表示i的配对对象是match[i],0表示还没有配对上
bool dfs(int x){
    for(int i=head[x];i;i=Next[i]){ // 递归的寻找可以与x配对的点
        int y=ver[i];
        if(!mp[y]){  // 这个点没有访问过
            mp[y]=true; // 标记一下表示访问过了
            if(!match[y]||dfs(match[y])){   // 找到一个没有配对过的点，或者一个可以让出y的方案
                match[y]=x; // 回溯的标注与其配对的点
                return true;
            }
        }
    }
    return false;   // 没找到可以增广的点
}


int main(){
    *
    *
    *
    int res=0;  // 表示二分图的最大匹配数
    for(int i=1;i<=n;i++){  // 注意！！这里枚举的是二分图的左部（右部也可以）
        memset(mp,0,sizeof mp);  // 这一步不能少
        if(dfs(i)) 
    }
    return 0;
}
```

## dp
### 背包问题
#### 完全背包
```c++
for(int i = 1 ; i<=n ;i++){
    for(int j = v[i] ; j<=m ;j++)
        f[j] = max(f[j],f[j-v[i]]+w[i]);
}
```
---
#### 多重背包的二进制优化
```c++
while(n--){
    scanf("%d %d %d",&v,&w,&s);
    int k;
    for(k=1;k<=s;k<<=1){
        s-=k;
        for(int i=m;i>=v*k;i--)
        dp[i]=max(dp[i],dp[i-k*v]+k*w);
    }
    if(s>0){
        for(int i=m;i>=s*v;i--)
        dp[i]=max(dp[i],dp[i-s*v]+w*s);
    }
}

```
### 数位dp
这个板子不具有一般性，请结合题目来理解：

如果一个正整数每一个数位都是 互不相同 的，我们称它是 特殊整数 。

给你一个正整数 $$ n $$ ，请你返回区间 $$[1, n]$$ 之间特殊整数的数目。

示例：<br>
输入:
```py
    20
```

输出
```py
    19
```


```c++
int f[15][1<<10];   // 合法情况下（第一个数字允许是0），这里存储的是一般情况下（不受限制）的情况
int n;
string s;   // 字符串表示的数字

// is_limt表示是否受到了前面数字的约束
// is_num第i个数前面是否填了数字
int dfs(int i,int mask,bool is_limt,bool is_num){
    if(i==n) return is_num; // 合法返回1
        
    if(!is_limt&&is_num&&f[i][mask]!=-1) return f[i][mask];
        
    int res=0;
    if(!is_num) res=dfs(i+1,mask,false,false);  // 前面全是0的状态是可以传导的，且前面是0那就对后面的数字不存在约束

    // 如果受到限制，那么就必须要设置最大值为s[i]，否则最大值可以到9
    int up=is_limt?s[i]-'0':9;

    // is_sum==false表示前面没有填写数字，那么这一位需要从1开始，否则可以从0开始
    for(int d=1-is_num;d<=up;d++)   // 遍历选择的数字
        if(!(mask >> d & 1))    // 这个数字没有填写过
            res+=dfs(i+1,mask|(1<<d),d==up&&is_limt,true);
    if(!is_limt&&is_num) f[i][mask]=res;
    return res;

}
```
---
## 数据结构
---
### 树状数组 
点修改，区间查询
```c++
void add(int i,ll d){
    for(;i<N;i+=i&-i) b[i]+=d;
}

ll ask(int i){
    ll res=0;
    for(;i;i-=i&-i) res+=b[i];
    return res;
}
```

---
### 线段树

区间修改，区间查询

```c++
const int N=2e5+10;
int n,m;
int a[N];

struct node{
    int l,r;
    ll sum,add;
    #define l(p) tree[p].l
    #define r(p) tree[p].r
    #define add(p) tree[p].add
    #define sum(p) tree[p].sum
}tree[N*4];

void build(int p,int l,int r){
    l(p)=l,r(p)=r;
    if(l==r){
        sum(p)=a[l];
        return;
    }
    int mid=(l+r)/2;
    build(p*2,l,mid);
    build(p*2+1,mid+1,r);
    sum(p)=sum(p*2)+sum(p*2+1);
};

void spead(int p){
    if(add(p)){
        sum(p*2)+=add(p)*(r(p*2)-l(p*2)+1);
        sum(p*2+1)+=add(p)*(r(p*2+1)-l(p*2+1)+1);
        add(p*2)+=add(p);
        add(p*2+1)+=add(p);
        add(p)=0;
    }
}

void change(int p,int l,int r,int d){
    if(l<=l(p)&&r(p)<=r){
        sum(p)+=d*(r(p)-l(p)+1);
        add(p)+=d;
        return;
    }
    spead(p);
    int mid=(l(p)+r(p))/2;
    if(l<=mid) change(p*2,l,r,d);
    if(mid<r) change(p*2+1,l,r,d);
    sum(p)=sum(p*2)+sum(p*2+1);
}

ll ask(int p,int l,int r){
    spead(p);
    if(l<=l(p)&&r(p)<=r) return sum(p);
    int mid=(l(p)+r(p))/2;
    ll res=0;
    if(l<=mid) res+=ask(p*2,l,r);
    if(mid<r) res+=ask(p*2+1,l,r);
    return res;
}


```
---

## 数学
---
### pow
---

```c++
ll pow(ll p,int n){
    ll res=1;
    while(n){
        if(n&1) res*=p;
        p*=p;
        res%=mod;
        p%=mod;
        n>>=1;
    }
    return res;
}
```
---
### 矩阵快速幂

斐波那契前 n 项**和**

```c++
#include<iostream>
#include<cstring>
using namespace std;
typedef long long ll;
ll n,mod;
ll res[3]={1,2,4};
ll a[3][3]={ {0,0,-1},
             {1,0,0},
             {0,1,2} };

void mul(){
    ll c[4]={0};
    for(int j=0;j<3;j++){
        for(int k=0;k<3;k++)
            c[j]=(c[j]+res[k]*a[k][j])%mod;
    }
    memcpy(res,c,sizeof c);
}

void mulself(){
    ll c[3][3]={{0}};
    for(int i=0;i<3;i++)
        for(int j=0;j<3;j++)
            for(int k=0;k<3;k++)
                c[i][j]=(c[i][j]+a[i][k]*a[k][j])%mod;
    memcpy(a,c,sizeof a);
}

int main(){
    cin>>n>>mod;
    n--;
    
    while(n){
        if(n&1) mul();
        mulself();
        n>>=1;
    }
    cout<<res[0];
    return 0;
}
```
---
### 逆元计算
```c++
int exgcd(int a,int b,int &x,int &y){
    if(b==0){x=1,y=0;return a;}
    int d=exgcd(b,a%b,x,y);
    int z=x;
    x=y;
    y=z-a/b*y;
    return d;
}
```
---
### 欧拉筛
```c++
int prime[N],m; // 存放素数
bool mp[N];     // 判断是否为素数
int v[N]={0};

void primes(){
    for(int i=2;i<=N;i++){
        if(v[i]==0) prime[m++]=i,v[i]=i,mp[i]=true;
        for(int j=0;j<m;j++){
            if(prime[j]>v[i]||prime[j]>N/i) break;
            v[i*prime[j]]=prime[j];
        }
    }
}
```