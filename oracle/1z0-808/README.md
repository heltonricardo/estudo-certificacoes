# 1Z0-808 - Oracle Certified Associate, Java SE 8 Programmer

<img src="assets/badge.png" alt="1Z0-808 - Oracle Certified Associate, Java SE 8 Programmer" width="200"/>

<!-- TOC tocDepth:2..3 chapterDepth:2..6 -->

- [1. Blocos de construção do Java](#1-blocos-de-construção-do-java)
  - [1.1. Comentários](#11-comentários)
  - [1.2. Estrutura de uma classe](#12-estrutura-de-uma-classe)
  - [1.3. Arquivos e classes](#13-arquivos-e-classes)
  - [1.4. Método main](#14-método-main)
  - [1.5. Compilação e execução](#15-compilação-e-execução)
  - [1.6. Pacotes](#16-pacotes)

<!-- /TOC -->

## 1. Blocos de construção do Java

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

Se a classe não é declarada como pública, ou seja, pertence ao "pacote" (**package**) padrão, então o nome do arquivo não precisa ser o mesmo que o nome da classe. No entanto, é uma boa prática manter a correspondência entre o nome da classe e o nome do arquivo mesmo para classes não públicas, para tornar o código mais organizado e legível.

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

Também é possível usar wildcards (\*) para importar todas as classes de um pacote: `import outropacote.*;`. Pode-se usar wildcard somente no nome do pacote mais externo e não em subpacotes ou classes individuais dentro desse pacote. Além disso, é permitido apenas um wildcard por declaração de importação.

> Usar wildcard pode resultar em ambiguidade no código. Isso ocorre quando dois ou mais pacotes contêm classes ou interfaces com nomes idênticos ou conflitantes. Nesse cenário, o compilador pode não saber qual classe específica deve ser usada em um contexto particular, resultando em um erro de ambiguidade.
>
> Para resolver ambiguidades ao usar wildcards pode-se **importar classes específicas**, **utilizar o nome completo da classe** ou **renomear classes localmente** usando `import ... as`.

O pacote `java.lang` é automaticamente importado, não sendo necessária sua importação manual.
