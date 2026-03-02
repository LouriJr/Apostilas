# 🚀 Aula Prática: Criando seu Primeiro Projeto React com Vite

Bem-vindo à parte prática! Siga os passos abaixo para configurar seu ambiente de desenvolvimento e criar o projeto base da nossa aula.

---

## 📂 Passo 1: Localize sua Pasta de Trabalho

1. Abra o **Explorador de Arquivos** do Windows.
2. Vá até a pasta onde você costuma salvar seus projetos (ex: `Documentos/MeusProjetos`).

## 💻 Passo 2: Abrindo o Terminal

1. Dentro da sua pasta de projetos, **segure a tecla SHIFT**.
2. Clique com o **botão direito do mouse** em um espaço vazio.
3. Selecione a opção **"Abrir janela do PowerShell aqui"** (ou "Abrir no Terminal").

## 🛠️ Passo 3: Criando o Projeto e acessando via VS Code

Copie e cole o comando abaixo no terminal e aperte **Enter**:

```bash
npx create-vite@latest aula1 --template react
```

> **Dica:** Esse comando já cria a pasta com o nome `aula1` e configura o React com JavaScript automaticamente para você.

1. Após o comando terminar, você verá uma nova pasta chamada **aula1**.
2. **Segure SHIFT** e clique com o **botão direito** sobre a pasta **aula1**.
3. Selecione a opção **"Abrir com Code"** (ou _Open with Code_).

## ⚡ Passo 4: Rodando o Projeto pela Primeira Vez

Agora, dentro do VS Code, precisamos instalar as bibliotecas do React e iniciar o servidor:

1. Abra o terminal interno do VS Code (Atalho: `Ctrl + '` ou menu **Terminal > New Terminal**).
2. Digite o comando para baixar os arquivos necessários:

    Bash

    ```
    npm install
    ```

3. Após finalizar a instalação, inicie o projeto:

    Bash

    ```
    npm run dev
    ```

4. **Ctrl + Clique** no link que aparecer no terminal (ex: `http://localhost:5173`) para visualizar o site no navegador!

## 📁 Passo 5: Entendendo a Estrutura (Resumo)

Ao abrir o VS Code, você verá várias pastas e arquivos. **Não se assuste!** No começo, focaremos em apenas dois arquivos principais dentro da pasta `src`:

* **main.jsx**: É a porta de entrada. Ele "monta" o React dentro da sua página HTML.
* **App.jsx**: É o componente principal, onde tudo começa a ser desenhado.

## 🧹 Passo 6: Limpando o Terreno

Antes de começar nosso código, vamos limpar o que o Vite trouxe por padrão:

1. Abra o arquivo `src/App.jsx`.
2. Apague todo o conteúdo de dentro do arquivo.
3. Deixe-o completamente vazio e salve (**Ctrl + S**).
4. Verifique no seu navegador: a página deve estar **totalmente branca**.

Ao fim desse ajuste, seu arquivo app.jsx deve se parecer com isso:

``` JSX
function App() {
  return (
    <>
    </>
  );
}

export default App;

```

---

## 🏗️ Passo 7: Criando nosso Primeiro Componente

No React, organizamos o código em pequenos pedaços chamados **Componentes**.

1. Dentro da pasta `src`, crie uma nova pasta chamada `components`.
2. Dentro de `components`, cada componente deve ter sua própria pasta. Crie uma pasta chamada `ProfileCard`.
3. Dentro da pasta `ProfileCard`, crie o arquivo `ProfileCard.jsx`.

---

## ✍️ Passo 8: Escrevendo o Componente

Agora, vamos escrever a estrutura básica do nosso card. No arquivo `ProfileCard.jsx`, adicione o seguinte código:

```jsx
function ProfileCard() {
  return (
    <div>
      <p>Nome: Seu Nome</p>
      <p>Idade: Sua idade</p>
      <p>Profissão: Sua profissão ou profissão desejada</p>
    </div>
  );
}

export default ProfileCard;
````

> **Nota:** Por enquanto, as informações estão "fixas" (hardcoded). Em breve aprenderemos como deixá-las dinâmicas!

* * *

## 📺 Passo 9: Exibindo no Navegador

Para que o card apareça, precisamos chamá-lo no nosso arquivo principal `App.jsx`:

1. Volte ao arquivo `src/App.jsx`.
2. Importe o componente e use-o conforme o exemplo:

JavaScript

```
import ProfileCard from "./components/ProfileCard/ProfileCard";

function App() {
  return (
    <div>
      <h1>Minha Turma de React</h1>
      <ProfileCard />
    </div>
  );
}

export default App;
```

1. Salve o arquivo e veja a mágica acontecer no navegador! 🚀

## 👥 Passo 10: O Problema da Repetição (Hardcoded)

Agora que nosso componente funciona, vamos testar sua principal vantagem: a **reutilização**.

1. No seu arquivo `App.jsx`, duplique a tag `<ProfileCard />`:

   ```jsx
   function App() {
     return (
       <div>
         <ProfileCard />
         <ProfileCard />
       </div>
     );
   }


2. Olhe para o navegador. Você verá dois cartões, mas **exatamente com as mesmas informações**.
3. **Reflexão:** Se tivermos 100 usuários, não faz sentido criar 100 arquivos diferentes, certo? Precisamos que o componente seja um "molde" que aceita informações diferentes.

* * *

## 🎁 Passo 11: O que são Props?

As **Props** (abreviação de _properties_) são como "encomendas" que enviamos para dentro de um componente.

> **Analogia de Professor:** Pense nas Props como os **parâmetros de uma função** na programação. No JavaScript comum, você faz: `soma(2, 5)`. No React, você faz: `<ProfileCard nome="João" />`.

É exatamente como o atributo `src` da tag `<img>`. A tag é a mesma, mas a imagem muda dependendo do que você passa no "parâmetro" `src`.

* * *

## 🛠️ Passo 12: Preparando o "Envio" (no App.jsx)

Antes de mexer no componente, vamos dizer quais informações queremos enviar. Ajuste o seu `App.jsx` para passar esses atributos (como se fossem atributos HTML):

JavaScript

```
function App() {
  return (
    <div>
      <h1>Lista de Perfis</h1>
      <ProfileCard nome="Erick" idade="28" profissao="Professor" />
      <ProfileCard nome="Ana" idade="22" profissao="Designer" />
    </div>
  );
}
```

* * *

## 📥 Passo 13: Recebendo as Props (no ProfileCard.jsx)

Agora precisamos avisar ao componente que ele vai receber um objeto chamado `props`.

1. Vá ao arquivo `src/components/ProfileCard/ProfileCard.jsx`.
2. Adicione o parâmetro `props` na função.
3. Use as chaves `{ }` para exibir o conteúdo JavaScript dentro do HTML:

JavaScript

```
// Recebemos o objeto 'props' como argumento da função
function ProfileCard(props) {
  return (
    <div style={{ border: '1px solid #ccc', margin: '10px', padding: '10px' }}>
      <p>Nome: {props.nome}</p>
      <p>Idade: {props.idade} anos</p>
      <p>Profissão: {props.profissao}</p>
    </div>
  );
}

export default ProfileCard;
```

* * *

## ✅ Passo 14: O Teste Final

1. Salve todos os arquivos (**Ctrl + K + S** salva tudo de uma vez).
2. Verifique o navegador: Agora você deve ver dois cards com **nomes e profissões diferentes!**
3. **Desafio Rápido:** Tente mudar a idade ou o nome de um dos perfis lá no `App.jsx` e veja o navegador atualizar instantaneamente.

## 🏆 DESAFIO FINAL: O Toque de Mestre

Agora que você entendeu como passar textos via **Props**, vamos elevar o nível. O seu componente `ProfileCard` está funcional, mas visualmente incompleto.

### 🎯 O Objetivo

Sua missão é adicionar uma foto de perfil para cada card.

### 📋 Requisitos

1. O componente `ProfileCard` deve exibir uma imagem acima das informações de texto.
2. A imagem **não pode ser fixa** (não pode estar hardcoded no componente).
3. Cada tag `<ProfileCard />` que você chamou no seu `App.jsx` deve enviar uma imagem diferente.
4. Utilize links de imagens `.jpg` encontradas no Google Imagens (clique com o botão direito na imagem e selecione "Copiar endereço da imagem").

### 💡 O Pensamento

Pense no que aprendemos sobre a tag `<img>` e como passamos as informações de `nome`, `idade` e `profissao`. O caminho é exatamente o mesmo!

Boa sorte, desenvolvedor(a)! 🚀
