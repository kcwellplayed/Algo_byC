# Algo_byC
「C言語で学ぶアルゴリズムとデータ構造」のメモ


## 目次

- [Chapter 1: 基本的なアルゴリズム](#chapter-1-基本的なアルゴリズム)
  - [1-1: アルゴリズムとは](#1-1-アルゴリズムとは)
  - [1-2: 繰り返し](#1-2-繰り返し)
- [Chapter 2: 基本的なデータ構造](#chapter-2-基本的なデータ構造)
  - [2-1: 配列](#2-1-配列)
  - [2-2: テストと検証](#2-2-テストと検証)
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

## Chapter 2: 実装と応用

### 2-1: コードの実装
- 言語とアルゴリズム
- 実装時の工夫や解説
- 関数ごとのコメントや構造整理

### 2-2: テストと検証
- テストケースと実行例
- 結果の考察
- 改善点や最適化案

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
