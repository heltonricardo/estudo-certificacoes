# 1Z0-808 - Oracle Certified Associate, Java SE 8 Programmer

<img src="assets/badge.png" alt="1Z0-808 - Oracle Certified Associate, Java SE 8 Programmer" width="200"/>

## Blocos de construção do Java

### Comentários

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

### Estrutura de uma classe

Uma classe em Java é um `modelo` ou um plano para criar objetos. Os membros que a compõe incluem:

- `Atributos` (variáveis de instância): para armazenar dados;
- `Métodos` (funções/procedimentos de instância): para definir o comportamento dos objetos.

```java
public class Animal {
    String nome;
}
```

### Arquivos e classes

Quando uma classe é declarada como pública em Java, `o nome do arquivo que a contém deve ser obrigatoriamente o mesmo nome da classe pública`.

Se a classe não é declarada como pública, ou seja, pertence ao "pacote" (**package**) padrão, então o nome do arquivo não precisa ser o mesmo que o nome da classe. No entanto, é uma boa prática manter a correspondência entre o nome da classe e o nome do arquivo mesmo para classes não públicas, para tornar o código mais organizado e legível.
