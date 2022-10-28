# **CSS com Super Poderes**

<a name="topo"></a>

### Requisitos:
- HTML5
- CSS3


## **Sumário**
 - [**Introdução**](#intro)
 - [**Variáveis**](#variaveis)
 - [**Importação**](#importacao)
 - [**Mixins**](#mixins)
 - [**Funções**](#funcoes)
 - [**Estrutura de Arquivos**](#estrutura)
 - [**Projeto**](#projeto)
 - [**Referencias**](#referencias)

<img aling-itens="center" height="150px" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/sass/sass-original.svg" />

## **Introdução**
Este tutorial tem como objetivo, uma rápida demonstração das principais funcinalidades diponíveis na linguagem Sass, que é um pre-processador para CSS, como também sua estrutura de organização de arquivos. Para um estudo mais aprofundado sobre a linguagem, acesse a **[Documentação Oficial](https://sass-lang.com/guide)**. Ao final criarei um mini-projeto para aprender-mos na prática a utilizar o que foi abordado.

O SASS (Syntactically Awesome Style Sheets), é um dos principais pre-processadores para CSS, ele serve basicamente para facilitar a codificação CSS, com o Sass seus codigos ficam mais bem organizados e faceis de ler e consequentemente mais faceis de dar manutenção em seus projetos.

Para instalar o Sass em sua máquina basta seguir o passo a passo do [**Site Oficial**](https://sass-lang.com/install), é bem simples, é só copiar e colar comandos no seu terminal.

### **Exemplo de Código**

Imagine que você precisa estilizar um botão simples, que mude de cor ao passar o cursor do mouse por cima e também altere o icone do curso para aquela "mãozinha". 

Fazer isso usando CSS ficaria assim:

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

Agora usando Sass esse mesmo trecho de código fica assim:

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

Essa funcionalidade se chama **Aninhamento**, onde em vez de criar vários blocos de código, um para cada alteração, com o Sass você faz toda a codificação do elemento dentro de somente um bloco de código. A primeira vista não parece ter mudado muito, mas imagine um arquivo CSS com centenas de linhas e vários blocos de código, ler e dar manutenção a cada bloco de codigo individualmente se torna bem mais trabalhoso sem o Sass.

Mas não é só isso que é possível fazer com o Sass, também podemos criar **Variáveis**, **Importações**, **Mixins** e **Funções**. Tudo isso você irá ver no decorrer da leitura. E no final quando estivermos codando o mini-projeto, você irá entender melhor tudo isso.

<a id="variaveis"></a>

## Variáveis

Usar variáveis em Sass é muito simples, a declaração é como em qualquer outra linguagem:

```scss
$cor_principal:#5352ed;
$cor_secundaria:#3131ca;
$tipografia: Arial;
```
No Sass, usa-se o caractere especial **$** (Dollar Sign), no inicio de cada variável.

Feito isso, podemos usa-las como desejar, veja ainda no exemplo do botão:

```scss
.botao{
  background: $cor_primaria;
  font-family: $tipografia;
  :hover{
    background-color: $cor_secundaria;
    cursor: pointer;
  }
}
```
[Retornar ao topo](#topo)

<a id="importacao"></a>

## **Importação**

A importação (**```@import```**) no Sass funciona igual como nas linguagens de programação, você consegue acesso a outros arquivos Sass, possibilitando importar **mixins**, **funções**, **variáveis** e também consiliar com o código CSS de outros arquivos de folha de estilo.

A seguir alguns exemplos:
```scss
@import "cor_primaria";
@import "cor_secundaria";
@import "tipografia";
```
Veremos mais detalhadamente sobre a importação quando formos implementar nosso projeto, inclusive a importação de folhas de estilo, que ainda não citei até esse momento.

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
    cursor: pointer;
  }
}

body{
  @include botao;
}
```
Fazendo isso, tornamos o estilo, um padrão que pode ser usado a qualquer momento, usamos a diretiva **```@include```** para isso.

Também podermos adicionar mudanças a esse estilo, para isso usamos os **argumentos** dentro dos mixins. Veja no exemplo:

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

Com as Funções **(```@function```)** você pode realizar operações complexas e retornar valores usando a regra **(```@return```)**, diferente dos mixins, as funções retornam só um valor. 

Veja o exemplo:

```scss
@function pow($base, $exponent) {
  $result: 1;
  @for $_ from 1 through $exponent {
    $result: $result * $base;
  }
  @return $result;
}

.sidebar {
  float: left;
  margin-left: pow(4, 3) * 1px;
}
```

E claro, também é possível adicionar argumentos às funções:

```scss
@function invert($color, $amount: 100%) {
  $inverse: change-color($color, $hue: hue($color) + 180);
  @return mix($inverse, $color, $amount);
}

$primary-color: #036;
.header {
  background-color: invert($primary-color, 80%);
}
```

[Retornar ao topo](#topo)

<a id="estrutura"></a>

## **Estrutura de Arquivos**

A medida que o projeto vai crescendo e ficando mais complexo, a quantidade de arquivos vai aumentando, e ter uma boa organização se torna algo essencial para a qualidade do projeto.

Neste tutorial introdutorio, irei utilizar uma estrutura simples por ser um projeto pequeno, para se aprofundar melhor no assunto, veja esse tutorial completo sobre [**madeiras de estruturar o SASS**](https://edrodrigues.com.br/blog/2-maneiras-mais-inteligentes-de-estruturar-o-sass/).

### **Estrutura Simples**

Melhor para projetos pequenos, essa estrutura divide a codificação dos estilos site em partes, dessa forma fica mais simples para fazer alterações e buscar blocos de código mais facilmente, melhor para codar e dar manutenção.

A estrutura que vou utilizar é a seguinte:

```
_base.sass - Aqui é onde ficará as variáveis, os mixins e classes.
_layout.sass - Aqui fica todo código que trata do layout da página.
_componentes.sass - Aqui fica tudo que pode ser reutilizado como botões etc.
_main.sass - Esse arquivo será responsável pelas importações dos demais arquivos acima.
```
[Retornar ao topo](#topo)


<a id="projeto"></a>
## **Mini-Projeto**

[Retornar ao topo](#topo)

<a id="referencias"></a>

# Referências:

- Documetação Oficial do Sass: [**Sass-lang.com/documentation**](https://sass-lang.com/documentation/).
- Documentação do Sass em português: [**Introdução ao Sass**](https://devschannel.com/sass/introducao-ao-sass).
- Tutorial sobre Estruturas de aquivos em Sass: [**2 Maneiras mais inteligente de estruturar o Sass**](https://edrodrigues.com.br/blog/2-maneiras-mais-inteligentes-de-estruturar-o-sass/).

[Retornar ao topo](#topo)