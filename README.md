# hello-world
Just another repository
#include<stdio.h>
#include<string.h>
int main(void) {
	int i, j, h, n, s, m,T,M,k,c;
	int t[26], d[26], sum[26],b[26];
	int f[26][26], a[26][26];
	while (scanf("%d%d", &n,&h) == 2) {
		if (n == 0)
			return 0;
		for (i = 1; i <= n; i++)
			scanf("%d", &f[i][0]);
		for (i = 1; i <= n; i++)
			scanf("%d", &d[i]);
		for (i = 1; i < n; i++)
			scanf("%d", &t[i]);
		for (i = 1; i <= n; i++)
			for (j = 1; j <= n; j++)
				f[i][j] = f[i][0];
		memset(sum, 0, sizeof(sum));
		memset(a, 0, sizeof(a));
		for (j = 1; j <= n; j++) {
			M = 0;
			for (i = 1; i < j; i++)
				M += 5*t[i];
			while (1) {
				T = 0;
				for (i = 1; i <= j; i++)
					T += a[i][j];
				if (T >= 12 *5 * h - M)
					break;
				m = -1;
				s = -1;
				for (i = 1; i <= j; i++) 
					if (f[i][j] > m) {
						m = f[i][j];
						s = i;
					}
				sum[j] += f[s][j];
				f[s][j] -= d[s];
				if (f[s][j] <= 0)
					f[s][j] = 0;
				a[s][j] += 5;
			}
		}
		m = -1;
		s = -1;
		for (i = 1; i <= n; i++)
			if (sum[i] > m)
				m = sum[i];
		k = 0;
		for (i = 1; i <= n; i++)
			if (sum[i] == m)
				b[++k] = i;
		while (1) {
			j = 1;
			s = b[1];
			c = 0;
			for (i = 2; i <= k; i++) {
				if (a[j][b[i]] > a[j][s])
					s = b[i];
				else if (a[j][b[i]] == a[j][s])
					c = 1;
			}
			if (s != b[1]) break;
			else if (c == 0) break;
			else j++;
		}
		
		for (i = 1; i < n; i++)
			printf("%d, ", a[i][s]);
		printf("%d\n",a[n][s]);
		printf("Number of fish expected: %d\n",sum[s]);
		printf("\n");
	}
	return 0;
}
