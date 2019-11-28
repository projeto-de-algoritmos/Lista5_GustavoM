# Canibais

## Origem 

A questão foi aplicada na IV Maratona de programação do IFB.
[Caderno de problemas](https://danielsaad.com/maratona/assets/4-mdp-ifb/Maratona.pdf)

## Descrição 

A trilha Nunca-Mais é bastante popular na cidade de Estranhópolis, possuindo diversos atrativos em seu percurso, como cavernas, cachoeiras, riachos etc. Um grupo de canibais que peregrinam entre cidades percebeu o trânsito de pessoas na trilha e resolveu se aproveitar da situação.

Um andarilho solitário seria um lanche fácil para os famintos antropófagos, mas fornece poucos nutrientes para o grupo todo. Uma excursão seria um banquete, mas o esforço para lidar com muitas pessoas pode ser demais para os antropófagos debilitados pela fome. Além disso, eles sabem que, ao capturarem e devorarem andarilhos, a cidade ficará em alerta e as pessoas deixarão de percorrer a trilha Nunca-Mais, forçando-os a retomar a peregrinação. Por questões de sobrevivência, a ideia dos canibais é simplesmente obter o máximo de energia, capturando as pessoas que oferecem menos resistência, para então preparar o melhor banquete possível antes de migrarem para outra localidade.

Sabendo que, em um determinado período de tempo, N pessoas percorrem a trilha Nunca-Mais, calcule a quantidade máxima de energia que os canibais conseguirão obter ao capturar os andarilhos, considerando que este processo não pode exceder o custo máximo M aos canibais.

### Input
A primeira linha é dada por pelos inteiros N (1≤N≤104), indicando a quantidade de pessoas que foram aventurar na trilha Nunca-Mais durante o referido período, e M (1≤M≤104), indicando o custo máximo que os canibais pretendem gastar no processo de captura de pessoas, separados por um espaço em branco.

A segunda linha contém N inteiros e1, e2, ... , eN, separados por um espaço em branco, descrevendo a energia que cada pessoa forneceria se for devorada pelos canibais, onde 1≤ei≤104.

A terceira linha também contém N inteiros c1, c2, ..., cN, separados por um espaço em branco, representando o custo de capturar cada pessoa, com 1≤ci≤104.

### Output
Imprima um único inteiro indicando a quantidade máxima de energia que os canibais podem obter após devorar as pessoas que eles conseguem capturar.


## Como resolver

A questão é uma clássica questão de knapsack sem modificações, o método de resolução é simplismente aplicar o algorítimo e resgatar a resposta. Porém o tempo limite da questão é de apenas 1 segundo,
portanto uma solução recursiva acarreta em TLE. A resposta deve ser feita usando uma solução iterativa.


### Solução Recursiva (TLE)
```c++
#include<bits/stdc++.h>
using namespace std;
const int MAX=10001;
int val[MAX], wt[MAX] ;
 
int knapsack(int n, int w){
	if(n==0 || w==0) return 0;
 
	if(wt[n-1]>w)
		return knapsack(n-1, w);
	else
		return max( val[n-1]+knapsack(n-1, w-wt[n-1]),
				knapsack(n-1, w));
}
int main(){
	ios::sync_with_stdio(0);
	int n, w;
	cin >> n >> w;
	for(int i=0; i<n; ++i) cin >> val[i];
	for(int i=0; i<n; ++i) cin >> wt[i];
	int ans = knapsack(n, w);
	cout << ans << endl;
}
```

### Solução Iterativa (AC) 202ms
```c++
#include <bits/stdc++.h>
using namespace std;
int mt[10010][10010]; // Matríz global é iniciada com zeros

int knapSack(int w, int wt[], int val[], int n){
    for(int i=1; i<=n; i++){
        for(int j=1; j<=w; j++){
            if(wt[i-1]<=j)
                mt[i][j] = max(val[i-1]+mt[i-1][j-wt[i-1]], mt[i-1][j]);
            else
                mt[i][j] = mt[i-1][j];
        }
    }
    return mt[n][w];
}

int main(){
	ios_base::sync_with_stdio(0);
	int n, w;
	cin >> n >> w;
	int wt[n], val[n];
	for(int i=0; i<n; i++) cin >> val[i];
	for(int i=0; i<n; i++) cin >> wt[i];
	cout << knapSack(w, wt, val, n) << endl;
}
```
