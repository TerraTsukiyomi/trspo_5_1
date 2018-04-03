# trspo_5_1
LR_5

#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <locale.h>

using namespace std;

int main()
{
	#define N 5 /* Число строк матрицы A*/
	#define M 3 /* Число столбцов матрицы A*/
	#define N2 3 /* Число строк матрицы B*/
	#define M2 4 /* Число столбцов матрицы B*/

	setlocale(0, "Russian");


	// Динамически выделяем память под матрицы A, B, C:
	// выделяем память для указателя на указатель
	int *A = (int*)malloc(N * sizeof(int*));
	int *B = (int*)malloc(N2 * sizeof(int*));
	int *C = (int*)malloc(N * sizeof(int*));

	// выделяем для каждой строки память
	for (int i = 0; i < N; i++) {
		A[i] = (int*)malloc(M * sizeof(int));
	}
	for (int i = 0; i < N2; i++) {
		B[i] = (int*)malloc(M2 * sizeof(int));
	}
	for (int i = 0; i < N; i++) {
		C[i] = (int*)malloc(M2 * sizeof(int));
	}

	/* Для генерации псевдослучайных чисел используется функция rand().
	* Она генерирует числа на основе базы. Если базу не менять, последовательность псевдослучайных чисел будет одна и та же. 
	* установки базы генератора псевдослучайных чисел служит функция srand(). 
	* Ее аргумент — и есть значение базы. Сочетание srand(time(NULL)) устанавливает в качестве базы текущее время. 
	* Этот прием часто используется для того, чтобы при разных запусках генератора псевдослучайных чисел была всякий раз разная база
	* и, соответственно, разный ряд получаемых значений.*/

	for (int i = 0; i < N; i++)
		for (int j = 0; j < M; j++) {
			A[i][j] = rand() % 10;
		}
	for (int i = 0; i < N2; i++)
		for (int j = 0; j < M2; j++) {
			B[i][j] = rand() % 10;
		}

	// Выполняем умножение матриц:
	for (int i = 0; i < N; i++)
		for (int j = 0; j < M2; j++) {
			C[i][j] = 0;
			for (int k = 0; k < M; k++)
				C[i][j] += A[i][k] * B[k][j];
		}

	// Выводим произведение на экран:
	printf("Матрица A\n");
	for (int i = 0; i < N; i++) {
		for (int j = 0; j < M; j++) {
			printf("%d ", A[i][j]);
		}
		printf("\n");
	}
	printf("\nМатрица B\n");
	for (int i = 0; i < N2; i++) {
		for (int j = 0; j < M2; j++) {
			printf("%d ", B[i][j]);
		}
		printf("\n");
	}
	printf("\nРезультат умножения: \n");
	for (int i = 0; i < N; i++) {
		for (int j = 0; j < M2; j++) {
			printf("%3d ", C[i][j]);
		}
		printf("\n");
	}



	//Не забываем освобождать память:

	for (int i = 0; i < N; i++) {
		free(A[i]);
	}
	for (int i = 0; i < N2; i++) {
		free(B[i]);
	}
	for (int i = 0; i < N; i++) {
		free(C[i]);
	}
	free(A);
	free(B);
	free(C);


	//Добавим проверку на возможность умножения матриц:
	if (M != N2) {
		printf("Нельзя умножать такие матрицы");
		system("pouse");
		return 0;
	}

}
