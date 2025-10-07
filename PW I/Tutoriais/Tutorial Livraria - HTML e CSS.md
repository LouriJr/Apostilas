# Tutorial Completo: Criando a Página "Etec Book Store" com HTML e CSS

## 🎯 Introdução

Neste exercício, você vai construir uma **vitrine de livros online**
usando HTML e CSS.\
O objetivo é praticar: - A estruturação de conteúdo com **HTML**\

- A estilização e layout com **CSS**\
- Conceitos de **flexbox**, **cores**, **fontes** e **sombreamento**

------------------------------------------------------------------------

## 🧱 Passo 1 -- Estrutura inicial do HTML

Crie o arquivo `index.html` com o conteúdo básico do documento.

``` html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Etec Book Store</title>
    <link rel="stylesheet" href="index.css" />
    <link
      href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100..900;1,100..900&display=swap"
      rel="stylesheet"
    />
  </head>
  <body></body>
</html>
```

🧩 **Explicação:**\
Aqui definimos o tipo de documento (`<!DOCTYPE html>`), idioma,
codificação e título.\
Também conectamos o arquivo `index.css` (que criaremos a seguir) e a
fonte **Roboto**, que deixará o texto mais moderno.

------------------------------------------------------------------------

## 🎨 Passo 2 -- Reset e base de estilos

Crie o arquivo `index.css` e adicione:

``` css
* {
  box-sizing: border-box;
}
html,
body {
  width: 100%;
  height: 100%;
  margin: 0;
  background-color: #eee;
  overflow-x: hidden;
}
```

🧩 **Explicação:**\

- O seletor `*` faz um reset para todos os elementos terem
`box-sizing: border-box`, facilitando cálculos de espaçamento.\
- O `html` e `body` ocupam 100% da tela e têm fundo cinza-claro
(`#eee`).\
- `overflow-x: hidden` impede o aparecimento de barras de rolagem
laterais.

------------------------------------------------------------------------

## 🧱 Passo 3 -- Estrutura principal da página

Adicione dentro do `<body>` do `index.html`:

``` html
<div class="container">
  <div class="header">
    <img src="logo.png" alt="Logo da livraria" />
    <span>Lourival Cicero</span>
  </div>

  <div class="content"></div>
</div>
```

🧩 **Explicação:**
O `.container` agrupa tudo.
Dentro dele, o `.header` é o **cabeçalho** e `.content` será a **área
dos livros**.

------------------------------------------------------------------------

## 🎨 Passo 4 -- Estilizando o container e o cabeçalho

No `index.css`, adicione:

``` css
.container {
  width: 100vw;
  height: 100vh;
  background-color: #eee;
}

.header {
  height: 20%;
  background-color: #efe5da;
  border-radius: 0 0 16px 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 32px;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.35);
}

.header img {
  height: 75%;
  width: auto;
}

.header span {
  font-family: "Roboto", sans-serif;
  font-size: 1.5rem;
}
```

🧩 **Explicação:**\
O cabeçalho usa **flexbox** para alinhar a logo e o nome.\
Tem **cantos arredondados**, **sombra leve** e ocupa 20% da altura da
tela.

------------------------------------------------------------------------

## 🧱 Passo 5 -- Área de livros (estrutura no HTML)

Agora vamos adicionar os livros dentro da `<div class="content">`:

``` html
<div class="content">
  <div class="book-container">
    <div class="book">
      <img
        class="book-image"
        src="https://m.media-amazon.com/images/I/51rsg74x7-L._SY445_.jpg"
        alt="O Mundo Assombrado Pelos Demônios"
      />
      <div class="book-info">
        <span class="book-title">O Mundo Assombrado Pelos Demônios</span>
        <span class="book-author">Carl Sagan</span>
      </div>
    </div>
    <div class="price">
      <span>R$ 39,90</span>
    </div>
  </div>
</div>
```

🧩 **Explicação:**
Cada **book-container** tem o **card do livro** e o **preço** logo
abaixo.

**Importante sobre a imagem:** O `src` da imagem está usando uma URL externa (da Amazon), mas na prática você também poderia usar uma imagem local. Por exemplo, se você tivesse uma imagem salva na pasta do projeto, poderia usar `src="imagens/livro1.jpg"` em vez da URL completa.

**📝 Dica importante:** Para adicionar mais livros ao seu site, você precisará duplicar a estrutura `<div class="book-container">` e personalizar cada elemento:

- **Título do livro:** Altere o texto dentro de `<span class="book-title">`
- **Autor:** Modifique o conteúdo de `<span class="book-author">`
- **Imagem:** Substitua o `src` da imagem pela capa do novo livro
- **Preço:** Atualize o valor em `<span>` dentro de `.price`

Desta forma, você pode criar uma vitrine completa com vários livros!

------------------------------------------------------------------------

## 🎨 Passo 6 -- Layout dos livros

Adicione ao `index.css`:

``` css
.content {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  gap: 32px;
  padding: 32px;
}

.book-container {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
```

🧩 **Explicação:**
A `.content` organiza os cards lado a lado e quebra linha
automaticamente.
Cada `.book-container` empilha o card e o preço verticalmente.

------------------------------------------------------------------------

## 🧱 Passo 7 -- Card do livro

HTML já está pronto; agora estilize o card.

``` css
.book {
  height: 425px;
  width: 250px;
  border-radius: 16px;
  background-color: #fcf8f5;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.35);
  transition: box-shadow 0.2s ease-in-out;
}

.book:hover {
  cursor: pointer;
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.35);
}
```

🧩 **Explicação:**
Define o tamanho e o estilo do card com um **efeito de sombra suave**
que aumenta ao passar o mouse.

------------------------------------------------------------------------

## 🎨 Passo 8 -- Imagem e informações do livro

Adicione:

``` css
.book-image {
  width: 100%;
  height: 75%;
  border-radius: 16px 16px 0 0;
}

.book-info {
  width: 100%;
  height: 25%;
  padding: 8px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
```

🧩 **Explicação:**
A imagem ocupa 75% do card e tem bordas arredondadas no topo.
As informações (título e autor) ficam abaixo, com espaçamento interno.

------------------------------------------------------------------------

## 🧱 Passo 9 -- Tipografia do título e autor

``` css
.book-title {
  font-family: "Roboto", sans-serif;
  font-size: 1.2rem;
}

.book-author {
  font-family: "Roboto", sans-serif;
  font-size: 1rem;
  color: #888;
}
```

🧩 **Explicação:**
O título é maior e o autor tem cor cinza mais clara, criando contraste
visual.

------------------------------------------------------------------------

## 🎨 Passo 10 -- Preço

``` css
.price {
  display: flex;
  justify-content: center;
  width: 250px;
}

.price span {
  font-family: "Roboto", sans-serif;
  font-size: 1.8rem;
  font-weight: bold;
  color: #72b074;
}
```

🧩 **Explicação:**
Centraliza o valor e o destaca com verde e fonte grande.

------------------------------------------------------------------------

## 🧩 Passo 11 -- Resultado final

Ao abrir o `index.html` no navegador, você verá:

- Um **cabeçalho** com fundo bege, logo e nome.
- Uma **vitrine de livros** organizada em colunas.
- Cada card com capa, título, autor e preço.
- Efeito de sombra quando o mouse passa sobre os cards.
