# Sweets Eating

## Origem 

Essa questão foi aplicada no round [#600](https://codeforces.com/contest/1253) do juiz online codeforces

[Link para questão](https://codeforces.com/contest/1253/problem/C)

## Descrição (Inglês)

Tsumugi brought n delicious sweets to the Light Music Club. They are numbered from 1 to n, where the i-th sweet has a sugar concentration described by an integer ai.

Yui loves sweets, but she can eat at most m sweets each day for health reasons.

Days are 1-indexed (numbered 1,2,3,…). Eating the sweet i at the d-th day will cause a sugar penalty of (d⋅ai), as sweets become more sugary with time. A sweet can be eaten at most once.

The total sugar penalty will be the sum of the individual penalties of each sweet eaten.

Suppose that Yui chooses exactly k sweets, and eats them in any order she wants. What is the minimum total sugar penalty she can get?

Since Yui is an undecided girl, she wants you to answer this question for every value of k between 1 and n.

### Input
The first line contains two integers n and m (1≤m≤n≤200 000).

The second line contains n integers a1,a2,…,an (1≤ai≤200 000).

### Output
You have to output n integers x1,x2,…,xn on a single line, separed by spaces, where xk is the minimum total sugar penalty Yui can get if she eats exactly k sweets.

## Solução 


```c++
#include<bits/stdc++.h>
using namespace std;
using ll = long long;
const int MAXN =  200010; 
ll dp[MAXN];

int main(){
	ios::sync_with_stdio(0);
	ll n, m;
	cin >> n >> m;
	vector<ll> vs(n);
	for(auto &x:vs) cin >> x;
	sort(vs.begin(), vs.end());
	ll sum = vs[0];
	cout << sum;
	for(ll i=1; i<n; ++i){
		ll acc=0;
		for(ll j=i; j>=0; j-=m){
			if(dp[j]){
				acc+=dp[j];
				break;
			}
			else acc+=vs[j];
		}
		dp[i]=acc;
		sum += dp[i];
		cout << " " << sum;
	}
	cout << endl;
}
```
