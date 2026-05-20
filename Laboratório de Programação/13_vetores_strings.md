
# Introdução a Vetores em C

## O problema: muitas variáveis para a mesma informação

Imagine que você precisa armazenar as notas de 5 alunos:

```c
float nota1;
float nota2;
float nota3;
float nota4;
float nota5;
```

Funciona para poucos dados. Mas imagine armazenar as notas de 100 alunos:

```c
float nota1;
float nota2;
float nota3;
...
float nota100;
```

Além de trabalhoso, o código fica difícil de manter. Se for necessário calcular a média ou percorrer todos os valores, precisaríamos acessar cada variável manualmente.

Para resolver esse problema, utilizamos **vetores**.

---

# O que é um vetor?

Um vetor é uma estrutura que permite armazenar vários valores do mesmo tipo dentro de uma única variável.

Também podemos pensar em um vetor como várias posições de memória organizadas em sequência.

**O livro aborda o tema de vetores como matrizes de uma única dimensão.**

Representação:

```
Notas:

+-----+-----+-----+-----+-----+
| 7.5 | 8.0 | 6.0 | 9.5 | 7.0 |
+-----+-----+-----+-----+-----+
   0     1     2     3     4
```

Cada posição possui um **índice**.

Importante:

Em C, os índices sempre começam em **0**.

---

# Declarando um vetor

Sintaxe:

```c
tipo nome[tamanho];
```

Exemplo:

```c
float notas[5];
```

Neste caso:

- `float` → tipo dos dados armazenados
- `notas` → nome do vetor
- `5` → quantidade fixa de posições

O vetor possui posições:

```c
notas[0]
notas[1]
notas[2]
notas[3]
notas[4]
```

---

# Atribuindo valores

Podemos atribuir valores individualmente:

```c
notas[0] = 7.5;
notas[1] = 8.0;
notas[2] = 6.0;
notas[3] = 9.5;
notas[4] = 7.0;
```

Também podemos declarar já inicializando:

```c
float notas[5] = {7.5, 8.0, 6.0, 9.5, 7.0};
```

---

# Acessando valores

Para acessar um elemento usamos seu índice:

```c
#include <stdio.h>

int main(){

    float notas[5] = {7.5, 8.0, 6.0, 9.5, 7.0};

    printf("%.1f\n", notas[0]);
    printf("%.1f\n", notas[3]);

    return 0;
}
```

Saída:

```
7.5
9.5
```

---

# Utilizando repetição com vetores

Uma das grandes vantagens dos vetores é permitir percorrer os dados facilmente.

Exemplo:

```c
#include <stdio.h>

int main(){

    int numeros[5] = {10,20,30,40,50};

    for(int i = 0; i < 5; i++){

        printf("%d\n", numeros[i]);

    }

    return 0;
}
```

Saída:

```
10
20
30
40
50
```

---

# Cuidados com vetores

O tamanho do vetor é fixo.

Exemplo:

```c
int numeros[5];
```

Esse vetor possui apenas posições:

```c
numeros[0]
numeros[1]
numeros[2]
numeros[3]
numeros[4]
```

Tentar acessar uma posição inexistente pode gerar comportamento inesperado:

```c
numeros[8] = 100;
```

Esse acesso é inválido.

---

# O tipo char

Antes de entender strings, precisamos conhecer o tipo `char`.

O tipo `char` é utilizado para armazenar **um único caractere**.

Exemplos:

```c
char letra = 'A';
char simbolo = '#';
char numero = '8';
```

Observe que caracteres utilizam **aspas simples**:

```c
'A'
'B'
'@'
```

Um `char` armazena apenas um caractere por vez.

---

# Vetores de char

Assim como podemos criar vetores de inteiros ou reais, também podemos criar vetores de caracteres.

Exemplo:

```c
char letras[5] = {'H','E','L','L','O'};
```

Representação:

```
+-----+-----+-----+-----+-----+
|  H  |  E  |  L  |  L  |  O  |
+-----+-----+-----+-----+-----+
   0     1     2     3     4
```

---

# Strings em C

Em C, uma string não é um tipo próprio da linguagem.

Uma string é simplesmente um **vetor de caracteres (`char`)**.

Exemplo:

```c
char nome[6] = {'M','A','R','I','A','\0'};
```

Representação:

```
+-----+-----+-----+-----+-----+------+
|  M  |  A  |  R  |  I  |  A  | \0   |
+-----+-----+-----+-----+-----+------+
   0     1     2     3     4     5
```

O caractere `\0` é chamado de **caractere nulo** e indica o final da string.

Sem ele, o computador não saberá onde o texto termina.

Existe uma forma simplificada de declarar:

```c
char nome[] = "MARIA";
```

ou

```c
char nome[6] = "MARIA";
```

A linguagem adiciona automaticamente o `\0`.

---

# Exemplo completo

```c
#include <stdio.h>

int main(){

    char nome[20] = "Joao";

    printf("%s\n", nome);

    return 0;
}
```

Saída:

```
Joao
```

O `%s` é usado no `printf` para exibir strings.

---

# Extra

## Passagem de vetores para funções

Quando passamos uma variável comum para uma função, normalmente uma cópia do valor é enviada.

Exemplo:

```c
void alterar(int numero){

    numero = 100;

}
```

Nesse caso, alterar `numero` dentro da função não modifica a variável original.

Com vetores ocorre algo diferente.

Quando um vetor é enviado para uma função, a função recebe uma referência para os dados armazenados em memória. Isso significa que alterações feitas dentro da função afetam diretamente o vetor original.

Por isso, não é criada uma cópia completa do vetor.

Sintaxe:

```c
tipo nomeFuncao(tipo vetor[], tamanho);
```

ou

```c
tipo nomeFuncao(tipo vetor[tamanho], tamanho);
```

---

## Exemplo modificando valores de um vetor

Neste exemplo vamos criar uma função que dobra todos os valores de uma lista.

```c
#include <stdio.h>

void dobrarValores(int numeros[], int tamanho){

    for(int i = 0; i < tamanho; i++){

        numeros[i] = numeros[i] * 2;

    }

}

int main(){

    int lista[5] = {1,2,3,4,5};

    dobrarValores(lista, 5);

    for(int i = 0; i < 5; i++){

        printf("%d ", lista[i]);

    }

    return 0;
}
```

Saída:

```
2 4 6 8 10
```

Observe que a função não retornou um novo vetor.

Mesmo assim, os valores da lista original foram modificados, porque a função recebeu uma referência para o vetor armazenado na memória.