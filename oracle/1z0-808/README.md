# 1Z0-808 - Oracle Certified Associate, Java SE 8 Programmer

<img src="assets/badge.png" alt="1Z0-808 - Oracle Certified Associate, Java SE 8 Programmer" width="200"/>

<!-- TOC tocDepth:2..4 chapterDepth:2..4 -->

- [1. Blocos de construção](#1-blocos-de-construção)
  - [1.1. Comentários](#11-comentários)
  - [1.2. Estrutura de uma classe](#12-estrutura-de-uma-classe)
  - [1.3. Arquivos e classes](#13-arquivos-e-classes)
  - [1.4. Método main](#14-método-main)
  - [1.5. Compilação e execução](#15-compilação-e-execução)
  - [1.6. Pacotes](#16-pacotes)
  - [1.7. Criação de objetos](#17-criação-de-objetos)
  - [1.8. Blocos inicializadores de instância](#18-blocos-inicializadores-de-instância)
  - [1.9. Tipos primitivos x referências](#19-tipos-primitivos-x-referências)
  - [1.10. Declaração e inicialização de variáveis](#110-declaração-e-inicialização-de-variáveis)
  - [1.11. Ordem dos elementos na classe](#111-ordem-dos-elementos-na-classe)
  - [1.12. Destruindo objetos](#112-destruindo-objetos)
- [2. Operadores e instruções](#2-operadores-e-instruções)
  - [2.1. Tipos de operadores](#21-tipos-de-operadores)
  - [2.2. Precedência](#22-precedência)
  - [2.3. Operadores aritméticos](#23-operadores-aritméticos)
  - [2.4. Operadores relacionais](#24-operadores-relacionais)
  - [2.5. Operadores lógicos](#25-operadores-lógicos)
  - [2.6. Operadores de atribuição](#26-operadores-de-atribuição)
  - [2.7. Operadores de incremento e decremento](#27-operadores-de-incremento-e-decremento)
  - [2.8. Operadores bitwise](#28-operadores-bitwise)
  - [2.9. Operadores condicionais (ternários)](#29-operadores-condicionais-ternários)
  - [2.10. Operador instanceof](#210-operador-instanceof)
  - [2.11. Promoção numérica](#211-promoção-numérica)
  - [2.12. Estruturas de decisão](#212-estruturas-de-decisão)
    - [2.12.1. If-else](#2121-if-else)
    - [2.12.2. Ternário](#2122-ternário)
    - [2.12.3. Switch](#2123-switch)
  - [2.13. Estruturas de repetição](#213-estruturas-de-repetição)
    - [2.13.1. While](#2131-while)
    - [2.13.2. Do-while](#2132-do-while)
    - [2.13.3. For](#2133-for)
    - [2.13.4. Foreach](#2134-foreach)
    - [2.13.5. Break, continue e label](#2135-break-continue-e-label)
- [3. Core API](#3-core-api)
  - [3.1. String](#31-string)
    - [3.1.1. Concatenação](#311-concatenação)
    - [3.1.2. Métodos importantes](#312-métodos-importantes)
  - [3.2. StringBuilder](#32-stringbuilder)
    - [3.2.1. Métodos importantes](#321-métodos-importantes)
    - [3.2.2. StringBuilder x StringBuffer](#322-stringbuilder-x-stringbuffer)
  - [3.3. Comparação de objetos](#33-comparação-de-objetos)

<!-- /TOC -->

## 1. Blocos de construção

### 1.1. Comentários

```java
// Comentários de linha única: adicionar notas ou descrições breves.

/*
Comentários de bloco: podem abranger várias linhas.
São úteis para comentar seções maiores de código.
*/

/**
 * Documentação de comentários: usados para gerar documentação automática para o código usando a ferramenta javadoc.
 * Podem incluir informações sobre classes, métodos, parâmetros, retornos e mais.
 */
```

### 1.2. Estrutura de uma classe

Uma classe em Java é um `modelo` ou um plano para criar objetos. Os membros que a compõe incluem:

- `Atributos` (variáveis de instância): para armazenar dados;
- `Métodos` (funções/procedimentos de instância): para definir o comportamento dos objetos.

```java
public class Animal {
    String nome;
}
```

### 1.3. Arquivos e classes

Quando uma classe é declarada como pública em Java, `o nome do arquivo que a contém deve ser obrigatoriamente o mesmo nome da classe pública`.

Se a classe não é declarada como pública, ou seja, seu modificador de acesso é **package** (padrão), então o nome do arquivo não precisa ser o mesmo que o nome da classe. No entanto, é uma boa prática manter a correspondência entre o nome da classe e o nome do arquivo mesmo para classes não públicas, para tornar o código mais organizado e legível.

### 1.4. Método main

Serve como o ponto de entrada para a execução do programa.

```java
public class Programa {
    public static void main(String[] args) {
        System.out.println("Olá, mundo!");
    }
}
```

É declarado como `public` para que possa ser acessado de fora da classe e como `static` para que possa ser chamado sem criar uma instância da classe. Isso é necessário porque a execução do programa começa antes que qualquer objeto seja criado.

Pode receber argumentos de linha de comando como um array de strings (`String[] args`). Esses argumentos podem ser usados para passar informações ou configurações para o programa quando ele é executado. Também é possível usar `String ...args` (**varargs**).

### 1.5. Compilação e execução

Para compilar, usamos: `javac Programa.java` e para executar, usamos `java Programa`.

Para usar os argumentos, basta enviar após o nome do programa:

```sh
java Programa argumento1 "argumento dois" argumento3
```

```java
public class Programa {
    public static void main(String[] args) {
        System.out.println(args[0]); // argumento1
        System.out.println(args[1]); // argumento dois
        System.out.println(args[2]); // argumento3
    }
}
```

É necessário compilar todas as classes do projeto, indicando seu diretório:

```sh
javac dir1/ClasseA.java dir2/ClasseB.java
```

E para executar, use a anotação de ponto:

```java
java dir2.ClasseB
```

> Supondo que a classe B possui o método main.

### 1.6. Pacotes

Um pacote (`package`) é um mecanismo de organização de classes e interfaces em grupos relacionados. Ele ajuda a evitar conflitos de nomes entre classes, permite a modularização do código e facilita a organização de projetos de software em hierarquias lógicas. Os pacotes são representados como diretórios no sistema de arquivos.

- **Declaração de Pacote**: No início de um arquivo Java, você pode declarar a qual pacote a classe pertence usando a instrução package. Por exemplo:
  `package com.example.minhaplicacao;`

- **Importação de Classes**: Para usar classes de outros pacotes em seu código, você pode importá-las usando a instrução _import_. Por exemplo, se você quiser usar a classe MinhaClasse de um pacote chamado outropacote, você pode importá-la assim:
  `import outropacote.MinhaClasse;`

Se uma classe não tem uma declaração de pacote no início do arquivo, ela pertence ao pacote padrão. Classes no pacote padrão podem ser usadas diretamente sem importações, desde que estejam no mesmo pacote que as classes que as estão referenciando.

Também é possível usar wildcards () para importar todas as classes de um pacote: `import outropacote._;`. Pode-se usar wildcard somente no nome do pacote mais externo e não em subpacotes ou classes individuais dentro desse pacote. Além disso, é permitido apenas um wildcard por declaração de importação.

> Usar wildcard pode resultar em ambiguidade no código. Isso ocorre quando dois ou mais pacotes contêm classes ou interfaces com nomes idênticos ou conflitantes. Nesse cenário, o compilador pode não saber qual classe específica deve ser usada em um contexto particular, resultando em um erro de ambiguidade.
>
> Para resolver ambiguidades ao usar wildcards pode-se **importar classes específicas**, **utilizar o nome completo da classe** ou **renomear classes localmente** usando `import ... as`.

O pacote `java.lang` é automaticamente importado, não sendo necessária sua importação manual.

### 1.7. Criação de objetos

Em Java, a criação de objetos envolve o uso da palavra-chave "new" seguida pelo construtor da classe. Os passos básicos para criar um objeto são:

```java
// Declaração da Variável de Referência:
TipoObjeto nomeObjeto;

// Alocação de Memória e Inicialização:
nomeObjeto = new TipoObjeto();
```

O construtor é um método especial na classe responsável por configurar o estado inicial do objeto e é chamado sempre que um objeto é criado.

Depois de criado, você pode acessar os membros (atributos e métodos) do objeto usando a notação de ponto.

### 1.8. Blocos inicializadores de instância

É um bloco de código que é executado quando uma instância da classe é criada. Ele é usado para realizar a inicialização de instâncias ou execução de código `antes da execução dos construtores`. Existem dois tipos de blocos inicializadores de instância em Java: o bloco de inicialização de instância e o bloco de inicialização de instância estático:

```java
public class Exemplo {

    // Bloco de inicialização estático
    static {
        System.out.println("Bloco de inicialização estático executado");
    }

    // Bloco de inicialização de instância
    {
        System.out.println("Bloco de inicialização de instância executado");
    }

    int valor; // A variável de instância

    // Construtor
    public Exemplo() {
        valor = 10;
        System.out.println("Construtor executado");
    }

    public static void main(String[] args) {
        System.out.println("Início do programa");
        Exemplo exemplo1 = new Exemplo();
        Exemplo exemplo2 = new Exemplo();
        System.out.println("Fim do programa");
    }
}

/* Resultado:
   Bloco de inicialização estático executado
   Início do programa
   Bloco de inicialização de instância executado
   Construtor executado
   Bloco de inicialização de instância executado
   Construtor executado
   Fim do programa
*/
```

O bloco de inicialização estático, ele é declarado com a palavra-chave `static` e é executado uma única vez quando a classe é carregada, antes da criação de qualquer instância.

O bloco de inicialização de instância é executado cada vez que uma nova instância da classe é criada, antes do construtor.

> Atributos e blocos inicializadores de instância são executados na ordem em que aparecem no arquivo, só depois o construtor é executado. Portanto, o código abaixo gera erro:
>
> ```java
> {
>   System.out.println(valor);
> }
> int valor = 10;
> ```

### 1.9. Tipos primitivos x referências

O Java possui 8 tipos primitivos:

![](assets/2023-11-13-20-38-19.png) \
Para que um valor inteiro seja interpretado como `long`, é necessário acrescentar o `L` no final, caso contrário, será interpretado como `int`. O mesmo acontece para diferenciar `float` e `double`, mas agora usando a letra `f`.

**Bases numéricas**
![](assets/2023-11-13-20-54-35.png)

- Começa com `0b`: binário
- Começa com `0`: octal
- Começa com `0x`: hexadecimal

Também podemos usar `_` para facilitar a leitura de números grandes **no código**: \
![](assets/2023-11-13-20-51-05.png) \
Não usar no começo, no fim dos valores, e antes ou depois do `.`.

As referências são variáveis que referenciam um objeto. Não guardam valor, mas sim o `endereço` do espaço de memória no qual o valor está.

Somente o tipo referência pode receber `null` e pode possuir métodos e atributos.

### 1.10. Declaração e inicialização de variáveis

**Declarando múltiplas variáveis**
![](assets/2023-11-13-21-25-58.png)

`Regras para identificadores`:

- Deve começar com **letra**, `$` ou `_`
- Pode conter **letras**, **números**, `$` ou `_`
- Não pode ser uma palavra reservada (Java é case-sensitive)

As variáveis locais (localizadas nos métodos) `não são inicializadas`. Gerarão erro caso tente usar antes de atribuir um valor a elas.

As variáveis de instância (atributos) ou classe (estáticas) têm valores padrão quando criadas: \
![](assets/2023-11-13-21-41-05.png)

As `variáveis de classe` são declaradas usando a palavra-chave `static`. Essas variáveis pertencem à classe, em vez de a uma instância específica da classe. Portanto, elas **são compartilhadas por todas as instâncias da classe**.

Quanto ao escopo das variáveis:

- `Variáveis Locais`: escopo desde a declaração até o fim do bloco
- `Variáveis de Instância`: da declaração até o objeto ser coletado
- `Variáveis de Classe`: da declaração até o fim do programa

### 1.11. Ordem dos elementos na classe

![](assets/2023-11-13-22-03-21.png)

### 1.12. Destruindo objetos

O `Garbage Collector` em Java é um mecanismo automático de gerenciamento de memória que remove objetos não referenciados, **liberando espaço na memória**. Ele opera de forma automática, identificando objetos que não têm mais referências no escopo de execução do programa. Embora seja possível chamar `System.gc()` para sugerir a execução do Garbage Collector, a efetiva coleta de objetos não é garantida nesse momento.

O método `finalize()` é chamado pelo Garbage Collector antes de liberar a memória ocupada por um objeto que está prestes a ser coletado. No entanto, sua execução não é garantida pois depende se um objeto é ou não coletado - nem todo objeto é necessariamente coletado.

## 2. Operadores e instruções

### 2.1. Tipos de operadores

- `Operadores Unários`: Atuam em um único operando. Exemplo: `-x`, `x++`

- `Operadores Binários`: Atuam em dois operandos.
  Exemplo: `a + b`

- `Operadores Ternários`: Atuam em três operandos.
  Exemplo: `x > 0 ? "Positivo" : "Negativo"`

### 2.2. Precedência

![](assets/2023-11-13-22-46-39.png) \
De cima para baixo: da maior para a menor precedência.

### 2.3. Operadores aritméticos

- Adição: `+`
- Subtração: `-`
- Multiplicação: `*`
- Divisão: `/`
- Módulo: `%`

### 2.4. Operadores relacionais

- Igual a: `==`
- Diferente de: `!=`
- Maior que: `>`
- Menor que: `<`
- Maior ou igual a: `>=`
- Menor ou igual a: `<=`

### 2.5. Operadores lógicos

- E lógico: `&&`
- OU lógico: `||`
- NÃO lógico: `!`

### 2.6. Operadores de atribuição

- Atribuição: `=`
- Adição e atribuição: `+=`
- Subtração e atribuição: `-=`
- Multiplicação e atribuição: `*=`
- Divisão e atribuição: `/=`
- Módulo e atribuição: `%=`

### 2.7. Operadores de incremento e decremento

- Incremento: `++`
- Decremento: `--`

### 2.8. Operadores bitwise

- E bitwise: `&`
- OU bitwise: `|`
- OU exclusivo bitwise: `^`
- Complemento bitwise: `~`
- Deslocamento à esquerda: `<<`
- Deslocamento à direita com sinal: `>>`
- Deslocamento à direita sem sinal: `>>>`

> Quando usamos os operadores bitwise entre **expressões**, ambas são sempre avaliadas, independentemente do valor da primeira expressão.

### 2.9. Operadores condicionais (ternários)

- Operador ternário: `? `

### 2.10. Operador instanceof

- instanceof: `instanceof`

### 2.11. Promoção numérica

Quando operações são realizadas entre tipos numéricos menores e um tipo numérico maior, `o tipo menor é promovido ao tipo maior automaticamente` antes da operação ser realizada. Isso garante a precisão dos cálculos e evita a perda de dados.

> Ao tentarmos atribuir tipos maiores para menores implicitamente, geramos um erro:
>
> ```java
> int x;
> long y;
>
> x = x * y; // Erro pois o resultado é long
>
> x *= y; // Funciona pois esse tipo de operação tem cast automático
> ```

### 2.12. Estruturas de decisão

#### 2.12.1. If-else

O bloco `if-else` é uma estrutura de controle de fluxo que permite a execução condicional de código. Se a condição especificada no `if` é verdadeira, o bloco de código dentro do `if` é executado; caso contrário, o bloco dentro do `else` é executado. Por exemplo, considerando a variável idade:

```java
int idade = 20;

if (idade >= 18) {
    System.out.println("Maior de idade");
} else {
    System.out.println("Menor de idade");
}
```

#### 2.12.2. Ternário

Já o operador ternário é uma forma concisa de expressar uma estrutura condicional em uma única linha. Ele avalia uma condição e retorna um valor com base nessa condição. Por exemplo, ao verificar se um número é par ou ímpar:

```java
int numero = 7;
String resultado = (numero % 2 == 0) ? "Par" : "Ímpar";
```

#### 2.12.3. Switch

É uma estrutura de controle usada para `direcionar a execução do código com base no valor de uma expressão`. Cada caso no bloco switch representa um valor possível da expressão, e o código correspondente é executado quando um caso coincide:

```java
int numeroDia = 5;
String diaSemana;

switch (numeroDia) {
    case 1:
        diaSemana = "Domingo";
        break;
    case 2:
        diaSemana = "Segunda-feira";
        break;
    case 3:
        diaSemana = "Terça-feira";
        break;
    default:
        diaSemana = "Outro dia";
}
```

### 2.13. Estruturas de repetição

#### 2.13.1. While

O loop while é uma estrutura de controle de fluxo que `executa repetidamente um bloco de código enquanto uma condição é verdadeira`. Por exemplo, para imprimir os números de 1 a 5:

```java
int contador = 1;

while (contador <= 5) {
    System.out.println(contador);
    contador++;
}
```

#### 2.13.2. Do-while

O loop do-while é uma estrutura semelhante ao while, mas `garante que o bloco de código seja executado pelo menos uma vez`, pois a condição é verificada após a execução do bloco. Por exemplo, para imprimir os números de 1 a 5:

```java
int contador = 1;

do {
    System.out.println(contador);
    contador++;
} while (contador <= 5);
```

#### 2.13.3. For

O loop for é uma estrutura de controle de fluxo que simplifica a iteração sobre uma sequência de elementos. É composto por uma `inicialização, condição de continuação e expressão de iteração`. Por exemplo, para imprimir os números de 1 a 5:

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

> `for ( ; ; ) {}` gera um loop infinito, pois os componentes do `for` são opcionais.

> É possível ter mais de uma inicialização e iteração. Basta separar por vírgula:
>
> ```java
> for (int i = 0, j = 10; i < 5 && j > 5; i++, j--) {
>     System.out.println("i: " + i + ", j: " + j);
> }
> ```

#### 2.13.4. Foreach

O loop foreach (também conhecido como **enhanced for loop**) é usado para iterar sobre elementos em uma coleção ou array. Ele simplifica o processo de iteração, `eliminando a necessidade de controlar índices manualmente`. Por exemplo, para percorrer os elementos de um array:

```java
int[] numeros = {1, 2, 3, 4, 5};

for (int numero : numeros) {
    System.out.println(numero);
}
```

#### 2.13.5. Break, continue e label

A palavra-chave `break` é usada para **interromper a execução** de **loops ou switch statements**. Por exemplo, para sair de um loop for quando i atinge 3:

```java
for (int i = 0; i < 5; i++) {
    if (i == 3) {
        break; // Sai do loop quando i é 3
    }
    System.out.println(i);
}
```

A palavra-chave `continue` é usada para **pular a iteração** atual de um loop e continuar com a próxima. Com labels, pode ser direcionado para qual loop deve pular. Exemplo, pulando a iteração quando i é 3:

```java
outerLoop:
for (int i = 0; i < 3; i++) {
    innerLoop:
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            continue outerLoop; // Pula a iteração quando i é 1 e j é 1
        }
        System.out.println(i + " " + j);
    }
}
```

> O `break` também pode ser usado com labels para especificar de qual loop ou switch deve sair.

## 3. Core API

### 3.1. String

Sequência **imutável** de caracteres que pode ser criada de duas formas:

```java
String nome1 = "Nome";
String nome2 = new String("Nome");
```

#### 3.1.1. Concatenação

A concatenação de strings com o operador `+` segue a regra da **esquerda para a direita**. Por exemplo, ao concatenar inteiros e strings:

```java
int numero1 = 5;
int numero2 = 10;
String resultado = numero1 + numero2 + " é o resultado.";

System.out.println(resultado); // "15 é o resultado"
```

Note que, mesmo sendo imutável, é possível concatenar uma string com outros caracteres:

```java
String nome = "Meu";

nome += " Nome";

System.out.println(nome); // "Meu nome"
```

Porém, internamente ainda existe um lugar na memória apenas com o conteúdo `"Meu"`. O conteúdo impresso na tela é resultado da criação de outra string com valor concatenado, e a variável `nome` apenas mudou o endereço referenciado. Assim, podemos observar a imutabilidade.

#### 3.1.2. Métodos importantes

- `length`: Retorna o número de caracteres na string;
- `charAt`: Retorna o caractere na posição especificada;
- `indexOf`: Retorna a posição do primeiro caractere especificado;
- `substring`: Retorna uma substring com base nos índices fornecidos;
- `toLowerCase`: Converte a string para minúsculas;
- `toUpperCase`: Converte a string para maiúsculas;
- `equals`: Verifica se duas strings são iguais;
- `equalsIgnoreCase`: Verifica se duas strings são iguais, ignorando maiúsculas e minúsculas;
- `startsWith`: Verifica se a string começa com um determinado prefixo;
- `endsWith`: Verifica se a string termina com um determinado sufixo;
- `contains`: Verifica se a string contém uma determinada sequência de caracteres;
- `replace`: Substitui caracteres ou sequências de caracteres por outros;
- `trim`: Remove espaços em branco do início e do final da string.

### 3.2. StringBuilder

Diferente de `String`, a **StringBuilder** é mutável. Logo, é ideal para casos em que é necessário fazer concatenações e mudanças em uma string, pois essas mudanças não ocasionam a criação de valores intermediários em memória.

```java
StringBuilder sb = new StringBuilder("Olá, ");
sb.append("mundo!");
System.out.println(sb);  // Saída: Olá, mundo!
```

#### 3.2.1. Métodos importantes

Para StringBuilder **podemos usar os [métodos da classe String](#312-métodos-importantes)**, e outros métodos específicos:

- `append`: Adiciona dados ao final do StringBuilder.
- `insert`: Insere dados em uma posição específica.
- `delete`: Remove uma sequência de caracteres.
- `deleteCharAt`: Remove o caractere na posição especificada.
- `reverse`: Inverte a sequência de caracteres.
- `toString`: Converte o StringBuilder para uma string.

#### 3.2.2. StringBuilder x StringBuffer

A classe `StringBuffer` possui os mesmos métodos de `StringBuilder`. A principal diferença entre elas é a sincronização.

`StringBuffer` é sincronizado e, portanto, seguro para operações concorrentes, mas pode ser menos eficiente em cenários onde a concorrência não é um problema.

`StringBuilder` não é sincronizado, tornando-o mais eficiente em operações não concorrentes.

Por exemplo, em um aplicativo onde várias **threads** estão manipulando e modificando uma string compartilhada, é crucial **garantir que as operações sejam sincronizadas para evitar problemas de concorrência e inconsistências nos resultados**. Nesses casos, usar `StringBuffer` (que é **thread-safe** devido à sincronização) é mais apropriado para garantir a consistência dos dados compartilhados entre as **threads**.

### 3.3. Comparação de objetos

O operador `==` em Java compara referências de objetos, não os valores.

No entanto, para objetos String criados sem o uso do operador new, o Java usa um **pool de strings** interno, o que significa que strings idênticas compartilham a mesma referência na memória, tornando a comparação com `==` válida para verificar igualdade de valor.

No entanto, para garantir a comparação de conteúdo, é preferível usar o método `equals()`, que compara os valores das strings, não apenas as referências.

```java
public class ComparacaoDeObjetos {

    public static void main(String[] args) {
        // Criando strings usando o pool de strings
        String str1 = "Hello";
        String str2 = "Hello";
        // Criando string no HEAP
        String str3 = new String("Hello");

        // Usando == para comparar referências
        System.out.println(str1 == str2);  // true (mesma referência no pool)
        System.out.println(str1 == str3);  // false (referências diferentes)

        // Usando equals para comparar valores
        System.out.println(str1.equals(str2));  // true (mesmo valor)
        System.out.println(str1.equals(str3));  // true (mesmo valor, embora referências sejam diferentes)
    }
}
```
