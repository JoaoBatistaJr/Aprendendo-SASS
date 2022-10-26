# **CSS com Super Poderes**

## **Introdução**
###  O SASS (Syntactically Awesome Style Sheets), é um dos principais pre-processadores para CSS, que serve basicamente para facilitar a codar CSS, com essa linguagem é possível escrever códigos mais limpos, ajudando a escrever menos código e também tornando a leitura mais amigável.

### Para instalar o SASS em sua máquina basta seguir simples o passo a passo do [**Site Oficial**](https://sass-lang.com/install), só copiar e colar.

<br>

### **Exemplo de Código**

### Imagine que você precisa estilizar um botão simples, que mude a sua cor ao passar o cursor do mouse por cima e também altere o icone do curso para a "mãozinha". Em CSS puro ficaria assim:

```css
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

### Já com SASS esse mesmo trecho de código ficaria assim:

```css
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

### A primeira vista não parece ter mudado muito, mas imagine um arquivo CSS com sentenas de linhas e vários blocos de código, para tratar de um mesmo elemento. Com o SASS você faz tada a codificação do elemento dentro de somente um bloco de código.