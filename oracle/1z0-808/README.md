# 1Z0-808 - Oracle Certified Associate, Java SE 8 Programmer

<img src="assets/badge.png" alt="1Z0-808 - Oracle Certified Associate, Java SE 8 Programmer" width="200"/>

<!-- TOC tocDepth:2..3 chapterDepth:2..6 -->

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
  - [2.3. Operadores Aritméticos](#23-operadores-aritméticos)
  - [2.4. Operadores Relacionais](#24-operadores-relacionais)
  - [2.5. Operadores Lógicos](#25-operadores-lógicos)
  - [2.6. Operadores de Atribuição](#26-operadores-de-atribuição)
  - [2.7. Operadores de Incremento/Decremento](#27-operadores-de-incrementodecremento)
  - [2.8. Operadores Bitwise](#28-operadores-bitwise)
  - [2.9. Operadores Condicionais (ternários)](#29-operadores-condicionais-ternários)
  - [2.10. Operador instanceof](#210-operador-instanceof)
  - [2.11. Promoção numérica](#211-promoção-numérica)
  - [2.12. Comandos de decisão](#212-comandos-de-decisão)
  - [2.13. Switch](#213-switch)

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

### 2.3. Operadores Aritméticos

- Adição: `+`
- Subtração: `-`
- Multiplicação: `*`
- Divisão: `/`
- Módulo: `%`

### 2.4. Operadores Relacionais

- Igual a: `==`
- Diferente de: `!=`
- Maior que: `>`
- Menor que: `<`
- Maior ou igual a: `>=`
- Menor ou igual a: `<=`

### 2.5. Operadores Lógicos

- E lógico: `&&`
- OU lógico: `||`
- NÃO lógico: `!`

### 2.6. Operadores de Atribuição

- Atribuição: `=`
- Adição e atribuição: `+=`
- Subtração e atribuição: `-=`
- Multiplicação e atribuição: `*=`
- Divisão e atribuição: `/=`
- Módulo e atribuição: `%=`

### 2.7. Operadores de Incremento/Decremento

- Incremento: `++`
- Decremento: `--`

### 2.8. Operadores Bitwise

- E bitwise: `&`
- OU bitwise: `|`
- OU exclusivo bitwise: `^`
- Complemento bitwise: `~`
- Deslocamento à esquerda: `<<`
- Deslocamento à direita com sinal: `>>`
- Deslocamento à direita sem sinal: `>>>`

> Quando usamos os operadores bitwise entre **expressões**, ambas são sempre avaliadas, independentemente do valor da primeira expressão.

### 2.9. Operadores Condicionais (ternários)

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

### 2.12. Comandos de decisão

O bloco `if-else` é uma estrutura de controle de fluxo que permite a execução condicional de código. Se a condição especificada no `if` é verdadeira, o bloco de código dentro do `if` é executado; caso contrário, o bloco dentro do `else` é executado. Por exemplo, considerando a variável idade:

```java
int idade = 20;

if (idade >= 18) {
    System.out.println("Maior de idade");
} else {
    System.out.println("Menor de idade");
}
```

Já o operador ternário é uma forma concisa de expressar uma estrutura condicional em uma única linha. Ele avalia uma condição e retorna um valor com base nessa condição. Por exemplo, ao verificar se um número é par ou ímpar:

```java
int numero = 7;
String resultado = (numero % 2 == 0) ? "Par" : "Ímpar";
```

### 2.13. Switch

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
