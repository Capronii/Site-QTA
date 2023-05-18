Knuth–Morris–Pratt algorithm
======

Problema
---------
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Imagine que você tem um texto de 1000 caracteres e quer saber se ele contém a palavra *touro*. Como você faria? Uma solução simples seria percorrer o texto, caractere por caractere, e verificar se o caractere atual é igual ao primeiro caractere da palavra. Se for, você verifica se o próximo caractere é igual ao segundo caractere da palavra, e assim por diante. Se todos os caracteres forem iguais, você encontrou a palavra. Caso contrário, você volta para o inicio e continua a busca a partir do próximo caractere.

**Entradas:**
* Texto Inteiro;

* Palavra a ser buscada;

**Saída:**
* Posição da palavra no texto;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Esse algoritmo é chamado de *força bruta* (**brute force**). Ele é simples e funciona, mas não é muito eficiente. Por exemplo, se o texto for MUITO grande, você vai ter que percorrer todos os caracteres até encontrar a palavra. Tendo uma complexidade **O(n*m)**, onde **n** é o tamanho do texto e **m** é o tamanho da palavra, sendo as vezes inviavél.



Ideia
---------

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Nas aulas de Desafios de Programação, você aprendeu alguns algoritmos de ordenação, como o *quicksort* e o *mergesort*. Neste exercício, você vai aprender um algoritmo de busca de texto, o *Knuth–Morris–Pratt algorithm* (KMP). Ele é um algoritmo de busca de padrões, ou seja, ele busca uma palavra dentro de um texto. A ideia é criar uma tabela de *falhas*, que nos indica quantos caracteres podemos pular quando encontramos uma falha. Assim não precisamos voltar para o proximo caracter e podemos continuar a busca a partir do próximo caractere na tabela de falhas. 

Sei que parece confuso, mas vamos ver um exemplo para ficar mais claro.

Tabela de Falha
---------

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Supondo que queremos buscar a palavra ***"touro"*** no texto ***"o touro fugiu"***. A tabela de falhas para essa palavra é a seguinte:

!!!colocar tabela
Colocar exemplo com imagens e setinhas
!!!


??? Exercício 1 - Agora é com você!

Utilizando a função ***cria_tabela_falha***, crie a tabela de falha para a seguintes entradas:

* Texto: ***""A casa caiu"***

* Palavra: ***"asa"***

::: Gabarito
!!!colocar Gabarito
Colocar gabarito bonitinho
!!!
:::

???
_______


O Algoritmo
---------

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Agora que temos a tabela de falhas, podemos usar ela para buscar a palavra **touro** no texto **o touro fugiu**. A ideia é percorrer o texto  e comparar caractere por caractere com a palavra. Se o caractere for igual, continuamos a busca. Se o caractere for diferente, pulamos para o próximo caractere de acordo com a tabela de falhas.




Implementação Em C
---------

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Segue abaixo uma implementação exemplo do algoritmo KMP em C para facilitar a compreensão do algoritmo.

``` c
void cria_tabela_falha(char* pat, int M, int* pps) {
   int length = 0;
   pps[0] = 0;
   int i = 1;
   while (i < M) {
      if (pat[i] == pat[length]) {
         length++;
         pps[i] = length;
         i++;
      } else {
         if (length != 0)
         length = pps[length - 1];
         else {
            pps[i] = 0;
            i++;
         }
      }
   }
}
void KMPAlgorithm(char* text, char* pattern) {
   int M = strlen(pattern);
   int N = strlen(text);
   int pps[M];
   cria_tabela_falha(pattern, M, pps);
   int i = 0;
   int j = 0;
   while (i < N) {
      if (pattern[j] == text[i]) {
         j++;
         i++;
      }
      if (j == M) {
         printf("Found pattern at index %d", i - j);
         j = pps[j - 1];
      }
      else if (i < N && pattern[j] != text[i]) {
         if (j != 0)
         j = pps[j - 1];
         else
         i = i + 1;
      }
   }
}
```

^Retirado de: https://www.tutorialspoint.com/c-program-for-kmp-algorithm-for-pattern-searching#

^^^
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; No começo a função ***cria_tabela_falha*** cria a tabela de suporte. Ela recebe como parâmetro a palavra que queremos buscar, o tamanho da palavra e um vetor de inteiros que vai guardar a tabela de falhas. A função ***kmp_search*** recebe como parâmetro a palavra que queremos buscar e o texto onde queremos buscar a palavra. Ela percorre o texto e compara caractere por caractere com a palavra. Se o caractere for igual, continuamos a busca. Se o caractere for diferente, pulamos para o próximo caractere de acordo com a tabela de falhas. 


!!!colocar exemplo de execução
Colocar exemplo com imagens e setinhas 
!!!
^^^

---------

??? Exercício 2 - Denovo é com você!

Utilizando o algoritimo KMP, agora mostre o valor do index para cada passo da busca da palavra ***"asa"*** no texto ***""A casa caiu"***.


Dica:
Utilize a tabela de falha criada no exercício anterior.


::: Gabarito
!!!colocar Gabarito
Colocar gabarito bonitinho
!!!
:::

???

??? Exercício 3 - Tudo junto e misturado
Utilizando o algoritimo KMP, crie a tabela de falha e mostre o valor do index para cada passo da busca com as entradas:

* Texto:  ***"O genero mais popular é pop!"***

* Palavra: ***"pop"***

::: Gabarito
!!!colocar Gabarito
Colocar gabarito bonitinho
!!!
:::

???


??? Desafio - O poder da tabela de falha

Utilizando o algoritimo KMP, crie a tabela de falha e mostre o valor do index para cada passo da busca com as entradas:

* Texto: ***"ABBABABBBABBAB"***

* Palavra: ***"ABAB"***

::: Gabarito
!!!colocar Gabarito
Colocar gabarito bonitinho
!!!
:::

???


Faça você mesmo
---------



Você também pode criar

1. listas;

2. ordenadas,

assim como

* listas;

* não-ordenadas

e imagens. Lembre que todas as imagens devem estar em uma subpasta *img*.

![](logo.png)

Para tabelas, usa-se a [notação do
MultiMarkdown](https://fletcher.github.io/MultiMarkdown-6/syntax/tables.html),
que é muito flexível. Vale a pena abrir esse link para saber todas as
possibilidades.

| coluna a | coluna b |
|----------|----------|
| 1        | 2        |

Ao longo de um texto, você pode usar *itálico*, **negrito**, {red}(vermelho) e
[[tecla]]. Também pode usar uma equação LaTeX: $f(n) \leq g(n)$. Se for muito
grande, você pode isolá-la em um parágrafo.

$$\lim_{n \rightarrow \infty} \frac{f(n)}{g(n)} \leq 1$$

Para inserir uma animação, use `md :` seguido do nome de uma pasta onde as
imagens estão. Essa pasta também deve estar em *img*.

:bubble

Você também pode inserir código, inclusive especificando a linguagem.

``` py
def f():
    print('hello world')
```

``` c
void f() {
    printf("hello world\n");
}
```

Se não especificar nenhuma, o código fica com colorização de terminal.

```
hello world
```


!!! Aviso
Este é um exemplo de aviso, entre `md !!!`.
!!!


??? Exercício

Este é um exemplo de exercício, entre `md ???`.

::: Gabarito
Este é um exemplo de gabarito, entre `md :::`.
:::

???
