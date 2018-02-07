# Hello-world
#x小z的袜子
=======
莫队算法
------
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int MAXN =51000;
int a[MAXN],pos[MAXN];
ll ans,s[MAXN];
struct node{
    ll a,b;
    int l,r,id;
}N[MAXN];
bool cmp(node a, node b)
{
    if(pos[a.l]==pos[b.l]) return a.r<b.r;
    return pos[a.l]<pos[b.l];
}
bool cmp1(node a, node b)
{
    return a.id<b.id;
}
void update(int p,int val)
{
    ans-=s[a[p]]*s[a[p]];
    s[a[p]]+=val;
    ans+=s[a[p]]*s[a[p]];
}
ll gcd(ll x,ll y)
{
    return x%y==0?y:gcd(y,x%y);
}
int main ()
{
   // freopen("1.in","r",stdin);
    int n,m; scanf("%d%d",&n,&m);
    for(int i=1;i<=n;i++) scanf("%d",&a[i]);
    int block=(int)sqrt(n);
    for(int i=1;i<=n;i++) pos[i]=(i-1)/block+1;
    for(int i=1;i<=m;i++){
        scanf("%d%d",&N[i].l,&N[i].r);
        N[i].id=i;
    }
    sort(N+1,N+m+1,cmp);
  //  for (int i=1;i<=m;i++) printf("ans1 =%d/%d\n",N[i].l,N[i].r);
    int l=1,r=0;
    for(int i=1;i<=m;i++){
        for(;r<N[i].r;r++) update(r+1,1);
        for(;r>N[i].r;r--) update(r,-1);
        for(;l<N[i].l;l++) update(l,-1);
        for(;l>N[i].l;l--) update(l-1,1);
        if(N[i].l==N[i].r) {N[i].a=0,N[i].b=1;continue;}
        N[i].a=ans-(N[i].r-N[i].l+1);
        N[i].b=(ll)(N[i].r-N[i].l+1)*(N[i].r-N[i].l);
        ll g=gcd(N[i].a,N[i].b);
        N[i].a/=g, N[i].b/=g;
     }
     sort(N+1,N+1+m,cmp1);
     for(int i=1;i<=m;i++){
        printf("%lld/%lld\n",N[i].a,N[i].b);
     }
     return 0;

}
