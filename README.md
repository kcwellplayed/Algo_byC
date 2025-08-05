# Algo_byC
「C言語で学ぶアルゴリズムとデータ構造(柴田望洋)」のメモ


## 目次

- [Chapter 1: 基本的なアルゴリズム](#chapter-1-基本的なアルゴリズム)
  - [1-1: アルゴリズムとは](#1-1-アルゴリズムとは)
  - [1-2: 繰り返し](#1-2-繰り返し)
- [Chapter 2: 基本的なデータ構造](#chapter-2-基本的なデータ構造)
  - [2-1: 配列](#2-1-配列)
- [Chapter 3: ドキュメントと資産化](#chapter-3-ドキュメントと資産化)
  - [3-1: 学びの整理](#3-1-学びの整理)
  - [3-2: 再利用可能なアウトプット](#3-2-再利用可能なアウトプット)
- [Appendix（付録）](#appendix付録)

---

## Chapter 1: 基本的なアルゴリズム

### 1-1: アルゴリズムとは
最大最小を求めるアルゴリズムは数が増えても方法は変わらないため、面倒ではあるが同じように書ける。  
しかし中央値は数によってプログラムが大きく変わることが推測される。  
中央値を求めるプログラムは様々な書き方があるが、  
余分な分岐判定を含んでいたりすると効率が悪くなるので注意。  
数が大きくなった時に、どのようにして効率の良い、書きやすいプログラムになるかが楽しみ。  

```C
#include<stdio.h>

/*3値の最大値を求める関数*/
int max3(int a, int b, int c) {
	int max;
	max = a;
	if (b > max)
		max = b;
	if (c > max)
		max = c;
	return max;
}

/*3値の最小値を求める関数*/
int min3(int a, int b, int c) {
	int min;
	min = a;
	if (b < min)
		min = b;
	if (c < min)
		min = c;
	return min;
}

/*3値の中央値*/
int med3(int a, int b, int c) {
	if (a >= b)
		if (c >= a)
			return a;
		else if (b >= c)
			return b;
		else
			return c;
	else
		if (a >= c)
			return a;
		else if (b >= c)
			return c;
		else
			return b;
}

/*正負判定する関数*/
void det(int d) {
	if (d > 0)
		printf("その値は正です。\n");
	else if (d < 0)
		printf("その値は負です。\n");
	else
		printf("その値は0です。\n");
}

int main() {

	int a, b, c, d;
	int max, min, med;

	printf("3つの値を入力");
	printf("a="); scanf_s("%d", &a);
	printf("b="); scanf_s("%d", &b);
	printf("c="); scanf_s("%d", &c);

	/*3値の最大値*/
	printf("最大値は%dです。\n", max3(a, b, c));
	/*3値の最小値*/
	printf("最小値は%dです。\n", min3(a, b, c));
	/*3値の中央値*/
	printf("中央値は%dです。\n", med3(a, b, c));
	/*正負判定*/
	printf("1つの値を入力"); scanf_s("%d", &d);
	det(d);

	return 0;
}
```

### 1-2: 繰り返し
繰り返し処理を大きく分けると前判定繰り返しと後判定繰り返しがある。  
フローチャートを見ると違いがよくわかりやすい。  
前者はループ内の処理が１度も実行されない可能性があるが、後者は少なくとも  
１度は必ず実行される。この点で使い分けられることが多い。 
ちなみに`%3d`で整数型の数を3桁分のスペースに右づめに表示できる。
```C
#include<stdio.h>

/*1~nまでの和を計算(while文)する関数*/
int sum1(int n) {
	int i, sum;
	i = 1;
	sum = 0;
	while (i <= n) {
		sum += i;
		i++;
	}
	return sum;
}

/*同じ計算を1+2+...のように式を明示(for文)する関数*/
void sum2(int n) {
	int i, sum=0;
	for (i = 1; i <= n; i++) {
		printf("%d + ", i);
		sum += i;
	}
	printf("\b\b= %d\n", sum);
}

/*等差数列の和の公式を用いて計算する関数*/
int sum3(int n) {
	return (n*(1 + n))/2;
}

/*a~bの間の整数の和を計算する関数*/
int sum4(int a, int b) {
	return ((b-a)*(a + b))/2;
}

/*正の値を読み込んでその桁数を出力*/
int digits(int n) {
	int i = 1;
	while (n >= 10) {
		n /= 10;
		i++;
	}
	return i;
}

/*九九の表を表示（かける数も表示）する関数*/
void kuku(void) {
	int i, j, k;
	printf("   |");
	for (i = 1; i <= 9; i++) {
		printf("%3d", i);
	}
	printf("\n---+");
	for (i = 1; i <= 9; i++) {
		printf("---");
	}
	printf("\n");
	for (j = 1; j <= 9; j++) {
		printf(" %d |", j);
		for (k = 1; k <= 9; k++) {
				printf("%3d", j * k);
		}
		printf("\n");
	}
}


int main() {
	int n1, n2, n3, a, b, n4;

	/*1~nまでの和を計算(while文)*/
	do {
		printf("①和を計算します。nを入力："); scanf_s("%d", &n1);
	} while (n1 <= 0);
	printf("1から%dまでの和は%dです。\n", n1, sum1(n1));

	/*同じ計算を1+2+...のように式を明示(for文)*/
	do {
		printf("②和を計算します。nを入力："); scanf_s("%d", &n2);
	} while (n2 <= 0);
	sum2(n2);

	/*等差数列の和の公式を用いて計算*/
	do {
		printf("③和を計算します。nを入力："); scanf_s("%d", &n3);
	} while (n3 <= 0);
	printf("等差数列の和の公式を使うと和は%dです。\n", sum3(n3));

	/*a~bの間の整数の和を計算*/
	printf("２数の和を計算します。aを入力："); scanf_s("%d", &a);
	do {
		printf("b>aを入力："); scanf_s("%d", &b);
	} while (b <= a);
	printf("その２数の和は%dです。\n", sum4(a, b));

	/*正の値を読み込んでその桁数を出力*/
	do {
		printf("桁数を計算します。nを入力："); scanf_s("%d", &n4);
	} while (n4 <= 0);
	printf("桁数は%dです。\n", digits(n4));

	/*九九の表を表示（かける数も表示）*/
	kuku();

	return 0;
}
```
---

## Chapter 2: 基本的なデータ構造

### 2-1: 配列
データ構造とは要素同士に何らかの関係があるもの。  
そのひとつとしてここでは配列を扱う。  
C言語では配列の宣言時に要素数を変数にすることはできない。  
そのため要素数を標準入力から得た値にする場合は記憶域を動的に確保する必要がある。  
関数に配列を渡すときは配列名のみ、すなわち先頭要素のポインタと要素数を渡せばよい。  
`const`をつけると読み込みのみ可能で書き込み不可となる。  

```C
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

#define N 5 /*配列の要素数*/

/*要素数nの配列の最大値を返す関数*/
int maxn(const int a[], int n) {
	int max, i;
	max = a[0];
	for (i = 1; i < n; i++) {
		if (max < a[i]) max = a[i];
	}
	return max;
}

int main() {

	/*要素数５の配列に入力・表示*/
	int i;
	int a[N];
	for (i = 0; i < N; i++) {
		printf("a[%d]：", i); scanf_s("%d", &a[i]);
	}
	for (i = 0; i < N; i++) {
		printf("a[%d]=%d\n", i, a[i]);
	}

	/*配列を初期化して表示*/
	int b[] = { 0,2,4,6,8,10 };
	int s = sizeof(b) / sizeof(b[0]); /*要素数*/
	for (i = 0; i < s; i++) {
		printf("b[%d]=%d\n", i, b[i]);
	}

	/*int型のオブジェクトを動的に生成して表示したのち破棄*/
	int* x;
	x = calloc(1, sizeof(int));
	if (x == NULL)
		puts("記憶域の確保に失敗しました。");
	else {
		*x = 57;
		printf("%d\n", *x);
		free(x);
	}

	/*int型の配列を動的に生成して表示したのち破棄*/
	int na;
	printf("確保する配列の要素数："); scanf_s("%d", &na);
	int* y;
	y = calloc(na, sizeof(int));
	if (y == NULL)
		puts("記憶域の確保に失敗しました。");
	else {
		for (i = 0; i < na; i++) {
			printf("y[%d]:", i); scanf_s("%d", &y[i]);
		}
		for (i = 0; i < na; i++) {
			printf("y[%d]=%d\n", i, y[i]);
		}
		free(y);
	}

	/*n人の身長を入力し最大値を返す(関数で)*/
	int n;
	printf("何人の身長を入力しますか？"); scanf_s("%d", &n);
	int* height;
	height = calloc(n, sizeof(int));
	if (height == NULL)
		puts("記憶域の確保に失敗しました。");
	else {
		for (i = 0; i < n; i++) {
			printf("%d人目の身長：", i + 1);
			scanf_s("%d", &height[i]);
		}
		printf("身長の最大値は%dです。\n", maxn(height, n));
		free(height);
	}

	/*乱数で身長をを作成し最大値を求める*/
	int n2;
	int* height2;
	printf("何人の身長を入力しますか？："); scanf_s("%d", &n2);
	height2 = calloc(n2, sizeof(int));
	if (height2 == NULL)
		puts("記憶域の確保に失敗しました。");
	else {
		srand(time(NULL));
		for (i = 0; i < n2; i++) {
			height2[i] = 100 + rand() % 100;
			printf("%d人目の身長：%d\n", i + 1, height2[i]);
		}
		printf("最大値は%dです。\n", maxn(height2, n2));
		free(height2);
	}
	return 0;
}
```
**関数名の由来**  
`malloc`：memory allocation(メモリ割り当て)  
`calloc`：contiguous allocation(連続メモリ割り当て)  


続いて配列要素を反転するアルゴリズム。  
左右の端からスワップしていけばよい。  
スワップの実行回数はn/2である。これはnの偶奇によらない。  
プログラムをかけるよりも図を書いてこの操作で条件を満足することを確認する方が重要な気がする。   
関数形式マクロを用いるとプログラムが短くなり読みやすい。  
コンパイル時に呼び出した部分がマクロに書いた処理に展開される。  
`do{} while(0)`ではループの条件を満たさないので中の処理が1度のみ実行される。  
普通に書いてmain関数内で展開されるとifとelseの間に空文；ができてifとelseがつながっていないことになる。

```C
#include<stdio.h>
#include<stdlib.h>

/*関数内で一次保存用のtmpを確保する必要があるがその型は不明→引数に*/
/*関数形式マクロ*/
#define swap(type,x,y) do{type tmp; tmp=x; x=y; y=tmp;} while(0)

/*配列の要素を反転する関数*/
void ary_reverse(int a[], int n) {
	int i;
	for (i = 0; i < (n / 2); i++) {
		swap(int, a[i], a[n - i - 1]);
	}
}

int main() {
	/*配列の要素を反転*/
	int n3;
	printf("配列の要素数："); scanf_s("%d", &n3);
	int* c;
	c = calloc(n3, sizeof(int));
	for (i = 0; i < n3; i++) {
		printf("c[%d]=", i); scanf_s("%d", &c[i]);
	}
	puts("反転しました。");
	ary_reverse(c, n3);
	for (i = 0; i < n3; i++) {
		printf("c[%d]=%d\n", i, c[i]);
	}
	return 0;
}
```

---

## Chapter 3: ドキュメントと資産化

### 3-1: 学びの整理
- 学習ノートやまとめ
- メモ、気付き、重要事項

### 3-2: 再利用可能なアウトプット
- テンプレートコード
- 自作関数やツール
- 応用可能な設計パターン

---

## Appendix（付録）

- 参考リンク／資料
- 使用ライブラリ一覧
- 備考、その他メモ
