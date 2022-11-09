<a name="topo"></a>
# **CSS com Super Poderes**



### Requisitos

- HTML5
- CSS3


## **Sumário**

- [**Introdução**](#intro)
- [**Variáveis**](#variaveis)
- [**Importação**](#importacao)
- [**Mixins**](#mixins)
- [**Funções**](#funcoes)
- [**Estrutura de Arquivos**](#estrutura)
- [**Mini-Projeto**](#projeto)
- [**Referências**](#referencias)

<img aling-itens="center" height="150px" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/sass/sass-original.svg" />

## **Introdução**
Este tutorial tem como objetivo, uma rápida demonstração das principais funcinalidades diponíveis na linguagem Sass, que é um pre-processador para CSS, como também sua estrutura de organização de arquivos. Para um estudo mais aprofundado sobre a linguagem, acesse a **[Documentação Oficial](https://sass-lang.com/guide)**. Ao final criarei um mini-projeto para aprender-mos na prática a utilizar o que foi abordado.

O SASS (Syntactically Awesome Style Sheets), é um dos principais pre-processadores para CSS, ele serve basicamente para facilitar a codificação CSS, com o Sass seus codigos ficam mais bem organizados e faceis de ler e consequentemente mais faceis de dar manutenção em seus projetos.

Para instalar o Sass em sua máquina basta inserir a seguinte linha de comando em seu terminal, pode ser no terminal do VS Code cosa esteja-o usando:

```shell
npm install -g sass
```

Pronto! após a instalação você pode verificar a versão com o comando:
```shell
sass --version
```

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

[Retornar ao topo](#topo)

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

Também podermos adicionar mudanças a esse estilo, para isso usamos os **argumentos** dentro dos mixins. 

Veja no exemplo:
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

Com as Funções **(```@function```)** você pode realizar operações complexas e retornar valores usando a regra **```@return```**, diferente dos mixins, as funções retornam só um valor. 

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
_components.sass - Aqui fica tudo que pode ser reutilizado como botões etc.
main.sass - Repare que neste não usavos o simbolo **_**(soblinhado), esse arquivo será responsável pelas importações dos demais arquivos acima.
```

Além disso, é importante criar uma folha de estilo para cada página de seu site, caso tenha mais de uma, ela deve ser nomeada com o mesmo nome da página seguindo o padrão da estrutura assim: **_pagina.sass**.

> Agora só um adendo importante. Originalmente a extensão usada nos arquivos era a **.SASS** mas atualmente a extensão oficial é a **.SCSS**, o que muda entre as duas? Somente um pouco da sintaxe, **.sass** não possuí chaves nem ponto e vírgula, mas a funcionalidade das duas é a mesma. Vou utilizar a extesão **.SCSS** por ter a sintaxe mais parecida com o CSS, mas fica a seu critério a qual usar.

[Retornar ao topo](#topo)


<a id="projeto"></a>
## **Mini-Projeto**

Antes de começarmos a codar, precisamos fazer uma pequena configuração no nosso VS Code. Na aba de extensões, pesquise por [**Live Sass Compiler**](https://marketplace.visualstudio.com/items?itemName=glenn2223.live-sass), precisamos dessa extensão para compilar o Sass.

Instale também a extensão [**Live Server**](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer), caso não a tenha, essa cria um servidor local para observar-mos as mudanças em tempo real.

Feito isso, podemos começar nosso projeto. Primeiro vamos criar nosso arquivo **index.html** com sua estrutura básica.
> **Dica:** para criar a estrutura básica do HTML5 basta digitar **!** dentro da página vazia, e uma opção aparecerá. Batas teclar Enter e a estrutura básica do HTML5 será criada.


Esse é o código HTML que será criado:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>CSS com Super Poderes</title>
</head>
<body>
		
</body>
</html>
```
Você pode adicionar um titulo de desejar.

Agora iremos criar uma pasta chamada **css**, nela vamos criar as folhas de estilo de nossa estruta de arquivos sass. Crie os seguintes arquivos dentro da pasta:

```
_base.scss 
_componentes.scss 
_layout.scss
main.scss
```
Feito isso, agora vou explicar como a compilação do sass funciona nos arquivos. Mas antes disso primeiro vamos abrir o arquivo **main.scss** e importar as outras folhas de estilo para ele, lembra que ele será o responsavel por juntar tudo.

Veja abaixo e siga a importação na mesma sequência mostrada:

```css
@import 'base';
@import 'components';
@import 'layout';
```
Essa sequência é importante para o que será carregado primeiro em nossa página.

Depois que fazer a importação abrir o no arquivo **_base.scss** e vamos adicionar um estilo qualquer só para verificar se tudo está pronto ao compilar-mos o nosso SASS, vou adicionar um reset simples para nossa página:

```css
*{
  margin: 0;
  padding: 0;
  border: 0;
}
```

Quando executarmos o compilador, o sass criará os arquivos **main.css** esse conterá todos os estilos dos outros arquivos .scss e estarão mimificados ou seja, será removido todos os estaços e tabulações deixando os codigos compactados, isso serve para economizar processamento na hora de carregar a página, e também criará um aquivo **main.css.map**.

Antes de executar o compilador, vamos chamar o arquivo **main.css** dentro do html:

```html
<head>
  <link rel="stylesheet" href="/css/main.css">
</head>
```
Depois feito tudo isso, podemos executar o nosso compilador, não se esqueça de salvar os arquivos e em seguida, na parte inferio do VS Code, na barra de status, você verá o botão da extensao Live Sass Compiler, clique em **Watch Sass** e espere compilar, é rapidinho, se estiver tudo certo aparecerá a saída com **Watching...** e seu sass já está funcionando e pronto para darmos início ao nosso projeto.

Para esse projeto, iremos criar um formulário de login, bem simples que nos ajudará a entender melhor os conceitos apresentados anteriormente.

Vamos iniciar criando nosso formulário na página **index.html**, dentro do corpo do site (**body**), juntamente com cada classe que precisaremos usar pra estilizar nosso formulário.

Veja abaixo:

```html
<body>
	<div class="login-box">
		<h2>Login</h2>
		<form action="">
			<div class="user-box">
				<input type="text" name="user" required="required">
				<label for="">Usuário</label>
			</div>
			<div class="user-box">
				<input type="text" name="password" required="required">
				<label for="">Senha</label>
			</div>
			<a href="">Entrar</a>
		</form>
	</div>
</body>
```

Formulário criado, agora vamos começar a estiliza-lo, primeiro vamos abrir o **_base.scss**, nele vamos adicionar algumas váriaveis, um reset simples para o **body** um **@mixin** para a tipografia.

```scss
$tipografia: font-family: Roboto;
$cor_fundo: #e9e9e9;
$cor_principal: #ed2553;
$cor_secundaria: #666666;

body{
  margin: 0;
  padding: 0;
}

@mixin tipografia($color, $size, $family){
  $family:$tipografia;
  $color:$cor_secundaria;
  $size: font-size: 16px;
}
```
Agora sempre que precisarmos usar uma cor, ou editar o estilo da tipografia do site, poderemos usar as variáveis e o **mixin.**

O próximo que iremos editar será o **_layout.scss**, nele iremos tratar todo o estilo da interface da página, que no nosso caso é o formulário de loguin.

```scss
.login-box {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 400px;
  padding: 40px;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-sizing: border-box;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  border-radius: 6px;
  h2 {
    margin: 70px 50px 30px;
    @include tipografia($size: 38px);
    color: #ed2553;
    padding: 0;
    text-align: center;
  }
}

.login-box .user-box {
  position: relative;
  input {
    width: 100%;
    padding: 10px 0;
    @include tipografia($size: 16px, $color: #000);
    margin-bottom: 30px;
    border: none;
    border-bottom: 1px solid #ed2553;
    outline: none;
    background-color: transparent;
  }
  label {
    position: absolute;
    top: 0;
    left: 0;
    padding: 10px 0;
    @include tipografia($size: 16px, $color: #000);
    pointer-events: none;
    transition: .5s;
  }
}

.login-box .user-box input:focus~label,
.login-box .user-box input:valid~label {
  top: -20px;
  left: 0;
  @include tipografia($size: 12px, $color: #ed2553);
}
```
Agora vamos para a página **_components.scss**, nela iremos estilzar nosso unico componente que é o botão de entrar.

```scss
.login-box form a {
  display: inline-block; 
  padding: 10px 20px; 
  color: #ed2553;
  font-size: 16px;
  text-decoration: none;
  text-transform: uppercase;
  transition: .5s;
  margin-top: 40px;
  border: 1px solid #ed2553;
  border-radius: 6px;
}

.login-box a:hover {
  background: #ed2553;
  color: #fff;
  border-radius: 5px;
}
```

[Retornar ao topo](#topo)

<a id="referencias"></a>

## **Referências**

- Documetação Oficial do Sass: [**Sass-lang.com/documentation**](https://sass-lang.com/documentation/).
- Documentação do Sass em português: [**Introdução ao Sass**](https://devschannel.com/sass/introducao-ao-sass).
- Tutorial sobre Estruturas de aquivos em Sass: [**2 Maneiras mais inteligente de estruturar o Sass**](https://edrodrigues.com.br/blog/2-maneiras-mais-inteligentes-de-estruturar-o-sass/).

[Retornar ao topo](#topo)