# **CSS com Super Poderes**

<a name="topo"></a>

## **Sumário**
 - [**Variáveis**](#variaveis)
 - [**Importação**](#importacao)
 - [**Mixins**](#mixins)
 - [**Funções**](#funcoes)
 - [**Estrutura de Arquivos**](#estrutura)

<img aling-itens="center" height="150px" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/sass/sass-original.svg" />

## **Introdução**
Este tutorial tem como objetivo uma rápida demonstração das principais funcinalidades diponíveis na linguagem de pre-processamento para CSS, como também sua estrutura e padrão de organização de arquivos. Para um estudo mais aprofundado sobre a linguagem, acesse a **[Documentação Oficial](https://sass-lang.com/guide)**.

O SASS (Syntactically Awesome Style Sheets), é um dos principais pre-processadores para CSS, que serve basicamente para facilitar a codar CSS, com essa linguagem é possível escrever códigos mais limpos, ajudando a escrever menos código e também tornando a leitura mais tranquila.

Para instalar o Sass em sua máquina basta seguir o passo a passo do [**Site Oficial**](https://sass-lang.com/install), só copiar e colar.

### **Exemplo de Código**

Imagine que você precisa estilizar um botão simples, que mude a sua cor ao passar o cursor do mouse por cima e também altere o icone do curso para a "mãozinha". 

Em CSS ficaria assim:

```scss
.botao{
  padding: 15px 40px;
  border-radius: 5px;
  background: #5352ed;
  font-family: Arial;
  font-weight: 600;
  color: #fbfbfb;
}
.botao:hover{
  background-color: #3131ca;
  cursor: pointer;
}
```

Já com Sass esse mesmo trecho de código ficaria assim:

```scss
.botao{
  padding: 15px 40px;
  border-radius: 5px;
  background: #5352ed;
  font-family: Arial;
  font-weight: 600;
  color: #fbfbfb;
  :hover{
    background-color: #3131ca;
    cursor: pointer;
  }
}
```

Essa funcionalidade se chama **Aninhamento**, a primeira vista não parece ter mudado muito, mas imagine um arquivo CSS com sentenas de linhas e vários blocos de código, para tratar de um mesmo elemento. Com o Sass você faz tada a codificação do elemento dentro de somente um bloco de código.

Mas não é só isso que é possível fazer com o Sass, também podemos criar Variáveis, Importações, Mixins e Funções. Tudo isso eu irei mostrar no decorrer da leitura. E ao final criarei um projetinho passo a passo para você aprender na prática a utilizar essa linguagem tão legal.

<a id="variaveis"></a>

## Variáveis

Usar variáveis em Sass é muito simples, a declaração é como em qualquer outra linguagem:

```scss
$cor_principal:#5352ed;
$cor_secundaria:#3131ca;
$tipografia: Arial;
```
No Sass usa-se o caractere especial **$** (Dollar Sign), no inicio de cada variável.

Feito isso, podemos usa-las como desejar, veja ainda no exemplo do botão:

```scss
.botao{
  background: $cor_primaria;
  font-family: $tipografia;
  :hover{
    background-color: $cor_secundaria;
  }
}
```
[Retornar ao topo](#topo)

<a id="importacao"></a>

## **Importação**

A importação (**```@import```**) no Sass funciona igual como nas linguagens de programação, você consegue acesso a outros arquivos Sass e CSS, possibilitando importar **mixins**, **funções**, **variáveis** e também consiliar com o código CSS de outros arquivos de folha de estilo.

A seguir alguns exemplos:
```scss
@import "cor_primaria";
@import "cor_secundaria";
@import "tipografia";
```
Veremos mais detalhadamente sobre a importação quando formos codar nosso projetinho, inclusive a importação de folhas de estilo, que ainda abordei nesse momento.

[Retornar ao topo](#topo)

<a id="mixins"></a>

## **Mixins**

Com os Mixins (**```@mixin```**) é possível declarar grupos de código CSS para serem reutilizados da maneira que você quiser.

Veja o nosso exemplo do botão:

```scss
@mixin botao{
  padding: 15px 40px;
  border-radius: 5px;
  background: $cor_primaria;
  font-family: $tipografia;
  font-weight: 600;
  :hover{
    background-color: $cor_secundaria;
  }
}

body{
  @include botao;
}
```
Fazendo isso, tornamos o estilo, um padrão que pode ser usado a qualquer momento, usamos a diretiva **```@include```** para isso. Mas também podermos adicionar mudanças a esse estilo, para isso usamos os **argumentos** dentro dos mixins. Veja no exemplo:

```scss
@mixin botao($font-color, $font-size: 1em) {
  font-size: $font-size;
  padding: $font-size/2;
  background-color: $cor_primaria;
  color: $font-color;
}

.button{
  @include botao(#fff);
}
```


[Retornar ao topo](#topo)

<a id="funcoes"></a>

## **Funções**

[Retornar ao topo](#topo)

<a id="estrutura"></a>

## **Estrutura de Arquivos**

[Retornar ao topo](#topo)