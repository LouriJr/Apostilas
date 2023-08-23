# Programação WEB II

## Introdução ao React

### O que é o React e por que ele é importante

React é uma biblioteca JavaScript para construir interfaces de usuário. Ele foi criado pelo Facebook e é amplamente utilizado em aplicativos web e móveis.

O React é importante porque ele torna a criação de aplicativos complexos muito mais fácil e rápida. Ele permite aos desenvolvedores criar componentes reutilizáveis que podem ser combinados para criar a interface do usuário. Isso significa que é possível escrever código mais enxuto e manter a consistência do design ao longo de um aplicativo inteiro.

Além disso, o React tem uma forte comunidade de desenvolvedores e uma ampla gama de ferramentas e bibliotecas disponíveis, o que significa que é fácil encontrar soluções para problemas comuns e adicionar recursos aos aplicativos.

Outra vantagem do React é sua capacidade de renderizar eficientemente grandes quantidades de dados e manter a interface de usuário atualizada em tempo real. Isso é especialmente importante em aplicativos que exigem muitas atualizações em tempo real, como jogos ou aplicativos de mensagens.

### Diferenças entre React e outras bibliotecas de interface de usuário

Existem algumas diferenças importantes entre o React e outras bibliotecas de interface de usuário, como Angular e Vue:

1. Enfoque em componentes: O React se concentra em componentes, o que significa que os desenvolvedores podem criar componentes reutilizáveis e combiná-los para criar a interface do usuário. Outras bibliotecas, como o Angular, tendem a se concentrar em controladores de visão e modelos.

2. Aprendizado: O React é geralmente considerado mais fácil de aprender do que outras bibliotecas, como o Angular, que possuem uma curva de aprendizado mais inclinada.

3. Performance: O React é conhecido por ser uma das bibliotecas de interface de usuário mais rápidas e eficientes, especialmente quando se trata de renderização de dados em tempo real.

4. Filosofia de desenvolvimento: O React se concentra em permitir aos desenvolvedores escrever código modular e reutilizável, enquanto outras bibliotecas, como o Angular, tendem a oferecer uma abordagem mais direcionada e prescrever certos padrões de projeto.

5. Comunidade: A comunidade do React é muito ativa e oferece uma ampla gama de ferramentas, bibliotecas e recursos para os desenvolvedores.

Em resumo, as diferenças entre o React e outras bibliotecas de interface de usuário dependem do enfoque, da facilidade de aprendizado, da performance, da filosofia de desenvolvimento e da comunidade. O desenvolvedor deve escolher a biblioteca que melhor atenda às suas necessidades e ao projeto em questão.

### Instalação e configuração do ambiente de desenvolvimento

Para instalar e configurar o ambiente para desenvolver em React, é necessário entender o que é o Node.Js.

Node.js é um ambiente de execução JavaScript de código aberto para servidores. Ele foi criado para ajudar os desenvolvedores a construir aplicações escaláveis e de alta performance usando JavaScript no lado do servidor. Com o Node.js, você pode escrever código JavaScript no lado do servidor para manipular solicitações HTTP, manipular banco de dados, gerenciar sessões de usuário, entre outras coisas.

Node.js usa a arquitetura baseada em eventos para lidar com a concorrência e a execução de tarefas assíncronas, tornando-o ideal para aplicativos que precisam lidar com muitas solicitações de rede ao mesmo tempo. Além disso, o Node.js possui uma grande comunidade de desenvolvedores e uma ampla gama de módulos e bibliotecas disponíveis para ajudá-lo a construir aplicativos rapidamente.

Em resumo, o Node.js é uma plataforma poderosa e versátil para construir aplicativos web e outros tipos de aplicativos no lado do servidor, ou seja, o Node.js é necessário para executar o código JavaScript fora do navegador

A instalação e configuração do ambiente de desenvolvimento para o React depende do sistema operacional e das preferências do desenvolvedor. Aqui estão os passos gerais para instalar e configurar o ambiente de desenvolvimento do React:

1. Instale o Node.js

2. Execute no terminal comando create-react-app: O create-react-app é uma ferramenta de linha de comando para criar rapidamente a estrutura básica de um aplicativo React. Para executá-lo, basta seguir o passo a seguir no terminal:

```npx create-react-app nome-do-app```

Instale um editor de código: Você precisará de um editor de código para escrever e editar seu código React. O utilizado em nosso será o Visual Studio Code.

Depois de seguir esses passos, você estará pronto para começar a desenvolver aplicativos React. Você pode criar um projeto com o create-react-app e começar a escrever código imediatamente.

## Fundamentos do React

### Componentes em React

Os componentes são a base da arquitetura do React. Eles representam pequenas partes reutilizáveis de uma aplicação que podem ser combinadas para formar uma interface do usuário completa. Cada componente é responsável por renderizar algum aspecto da interface do usuário e gerenciar seu próprio estado interno.

Os componentes são uma das principais características do React e ajudam a manter a aplicação organizada, facilita a manutenção e torna o desenvolvimento mais eficiente. Ao dividir a interface do usuário em pequenos componentes, é possível escrever código reutilizável e testá-lo de forma independente. Além disso, os componentes podem ser atualizados individualmente sem afetar o resto da aplicação.

#### JSX e sua utilização para criar elementos de interface

JSX é uma sintaxe que permite misturar HTML e JavaScript em uma única declaração. Ele é amplamente utilizado no React para criar elementos da interface de usuário. Ao invés de criar elementos HTML com JavaScript puro, você pode escrever JSX e o React cuidará da renderização desses elementos na tela.

A utilização do JSX torna a criação de elementos da interface muito mais fácil e intuitiva. Além disso, permite a passagem de valores dinâmicos como propriedades, tornando a interface mais flexível e adaptável a diferentes situações.

``` JSX
function CardUsuario() {
  return (
    <div>
      <p>Nome: Lourival Cicero</p>
      <p>Email: lourival@gmail.com</p>
    </div>
  );
}

export default CardUsuario;
```

Ou seja, JSX é uma sintaxe que permite a criação de elementos da interface de usuário de forma mais fácil e intuitiva e torna o desenvolvimento mais eficiente e agradável. Além disso, é uma característica fundamental do React que permite passar valores dinâmicos como propriedades para os componentes.

## Props: Como passar propriedades (props) para os componentes e utilizá-las para renderizar dados dinamicamente

Props são mecanismos para passar informações e ações de um componente pai para um componente filho. São semelhantes aos atributos em elementos HTML. As props são utilizadas para transmitir dados ou configurações específicas de um componente para outro, permitindo que os componentes sejam personalizados e reutilizáveis.

Por exemplo, podemos passar uma prop chamada "nome" para um componente filho e esse componente poderá exibir esse nome em sua renderização. As props são somente leitura e não podem ser modificadas dentro do componente filho, sendo uma forma de comunicação unidirecional.

#### Componente Filho

``` JSX

function ComponenteFilho({ nome }) { // Configuração da Prop
    return (
        <div>
            <h1>{nome}</h1> {/* Utilização da Prop */}
        </div>
    );
}

export default ComponenteFilho;

```

#### Componente Pai

``` JSX

import ComponenteFilho from "./ComponenteFilho"

function ComponentePai() { 
    return (
        <div>
            <ComponenteFilho nome={"Lourival"}></ComponenteFilho>
        </div>
    );
}

export default ComponentePai;

```

Ou seja, por meio do componente pai podemos passar dados dinâmicos para o componente filho, assim nosso componentes podem ser reutilizados com informações diferentes a serem exibidas para os usuários.

#### Utilizando CSS Modules

Agora com nosso CSS importado, precisamos utilizá-lo em nosso componente, seu uso é muito similar ao uso no HTML convencional, com exceção da marcação “class” e do uso do objeto **styles**.

Para utilizar uma classe no CSS como a classe “card” que criamos, você deve utilizar a marcação “className” da seguinte maneira:

```JSX
import styles from "./CardUsuario.module.css";

function CardUsuario() {
  return (
    <div className={styles.card}>
      <p>Nome: Lourival Cicero</p>
      <p>Email: lourival@gmail.com</p>
    </div>
  );
}

export default CardUsuario;

```

Adicionando está classe em nosso arquivo JSX a aparência de nosso site deve ser similar a imagem a seguir:

![Alt text](./Tutoriais/Primeiro%20Aplicativo%20React/AssetsReact/image2-8.png)

Agora com o HTML e CSS em mãos, sua criatividade é ilimitada, teste estilos e componentes diferentes para criar visuais interessantes e chamativos.

## State e gerenciamento de estado

No React, o estado (state) é um conceito fundamental para lidar com dados dinâmicos em um componente. O estado representa as informações que podem ser modificadas e atualizadas ao longo do tempo durante a interação do usuário ou em resposta a eventos. O gerenciamento adequado do estado é crucial para criar componentes interativos e reativos.

### Introdução ao State
O state é uma estrutura de dados que armazena informações mutáveis dentro de um componente. É utilizado para representar dados que podem ser alterados e refletidos na interface do usuário.

O estado é definido no construtor do componente usando a função useState ou em componentes de classe usando a propriedade state.

### Usando a Função useState
A função useState é um hook do React que permite adicionar estado a componentes funcionais. É utilizado para declarar uma variável de estado e uma função para atualizá-la.

A variável de estado e a função de atualização são retornadas em um array. Ao chamar a função de atualização, o React re-renderiza o componente com o novo valor do estado.

### Gerenciando Estado em Componentes de Classe

Em um componente React, o estado é definido usando a propriedade state. O estado é um objeto que contém as informações mutáveis do componente. 

A atualização do estado é feita chamando o método setState, que recebe um novo estado como argumento. ```O React então re-renderiza o componente com o novo estado.```

``` JS
const [state, setState] = useState(initialState);
```

## UseEffect

No React, o useEffect é um dos hooks mais importantes para gerenciar efeitos colaterais e interações com o ciclo de vida dos componentes. 

Ele permite executar código em resposta a mudanças no componente, como manipulação de DOM (manipulação do HTML), chamadas a APIs externas e subscrição/desubscrição de eventos. 

O useEffect é essencial para criar componentes funcionais reativos e interativos.

### Uso básico do UseEffect 

O exemplo mais comum de uso do useEffect é para executar um trecho de código logo ao renderizar o componente, simulando um evento "onLoad" do HTML, ou seja, quando o componente carregar, execute uma função ou código.

Geralmente esse uso pode ser feito para carregar os dados da tela por meio de uma chamada para o backend

``` JS
useEffect(()=> {
  BuscarDadosDoBackend();
}, []);
```

No exemplo anterior, o componente ao carregar vai executar a função chamada ```BuscarDadosDoBackend();```.

