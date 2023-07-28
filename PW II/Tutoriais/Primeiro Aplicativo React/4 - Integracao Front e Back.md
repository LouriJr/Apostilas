# Tutorial - Primeiro aplicativo React

Com os tutoriais anteriores realizados, precisamos unir nosso front-end com o back-end e exibir os dados do banco de dados direto para o usuário.

Vamos voltar a nosso projeto React e fazer os ajustes necessários, mas é importante que ao realizar as chamadas HTTP para o backend, seu projeto C# esteja executando.

## Adicionando Biblioteca

Para realizar as requisições HTTP do frontend para o backend, utilizaremos uma biblioteca chamada Axios. O Axios é uma biblioteca que oferece uma interface fácil de usar para enviar requisições assíncronas e lidar com respostas, simplificando o processo de obtenção de dados de APIs ou serviços backend em aplicações React.

Para instalar basta executar o comando no terminal do seu projeto React:

```
npm install axios
```

Agora vamos voltar ao código da nossa página de listagem de usuários.

## Criando a integração

No código JSX, podemos juntar a parte lógica à parte visual de um componente, logo, a responsabilidade de criar a lógica de buscar os dados e gerar um componente fica a cargo da nossa página de listagem de usuários.

Esse é o nosso código deste componente atualmente:

```JSX
import React from "react";
import CardUsuario from "../../Components/CardUsuario/CardUsuario";

function ListaDeUsuarios() {
  return (
    <div>
      <CardUsuario nome="Lourival Cicero" idade="24"></CardUsuario>
      <CardUsuario nome="João" idade="32"></CardUsuario>
      <CardUsuario nome="Maria" idade="30"></CardUsuario>
    </div>
  );
}

export default ListaDeUsuarios;
```

Vamos adicionar agora uma função chamada BuscarUsuarios, para poder realizar a requisição HTTP, é importante que essa função seja assíncrona.

```JSX
import React from "react";
import CardUsuario from "../../Components/CardUsuario/CardUsuario";

function ListaDeUsuarios() {

  async function BuscarUsuarios() {
    
  }

  return (
    <div>
      <CardUsuario nome="Lourival Cicero" idade="24"></CardUsuario>
      <CardUsuario nome="João" idade="32"></CardUsuario>
      <CardUsuario nome="Maria" idade="30"></CardUsuario>
    </div>
  );
}

export default ListaDeUsuarios;


```

Um método assíncrono é uma função que permite executar tarefas de forma assíncrona, sem bloquear a execução do restante do código. Ele utiliza a sintaxe async/await para lidar com operações que podem levar tempo, como chamadas de API ou acesso a banco de dados.

Esses métodos permitem que o código continue a execução enquanto aguarda a conclusão da operação assíncrona, garantindo uma melhor eficiência e responsividade do programa. Ao usar métodos assíncronos, podemos escrever um código mais conciso e legível, evitando o bloqueio de threads e permitindo a execução de várias tarefas simultaneamente.

### Utilizando o Axios

Para utilizar o Axios, precisamos realizar sua importação

```import axios from 'axios';```

Precisamos fazer agora a requisição utilizando a biblioteca, a sintaxe da biblioteca axios é muito simples, basta chama-la, seguido do verbo HTTP desejado, em nosso caso é o HTTP Get. Além do verbo, precisamos também da rota que criamos em nossa API, no meu caso foi <https://localhost:44342/api/usuarios/listar>.

``` JSX
const response = await axios.get("https://localhost:44397/api/usuarios/listar");
```

O marcador await antes da biblioteca axios indica que nosso código vai esperar o resultado de uma chamada assíncrona antes de prosseguir com a sua execução.

### Validando resposta da requisição

Agora que o conseguimos realizar a requisição, precisamos checar se houve sucesso ou erro no processo de chamada para o backend, para isso, basta verificarmos o **Status Code** da nossa resposta. Caso o status seja diferente de 200 (sucesso) temos que exibir uma mensagem de erro para o usuário.

```JSX
  async function BuscarUsuarios() {
    const response = await axios.get("https://localhost:44397/api/usuarios/listar");

    if(response.status != 200){
        alert("Erro ao listar usuários");
        return;
    }
  }
```

O ```return``` após a mensagem indica que o código dessa função termina naquele momento, assim evitando que o restante do código seja executado.

### Armazenando resultado da requisição

Realizamos a requisição e validamos seu resultado, precisamos então exibir os dados do JSON da resposta na tela para o usuário, portanto, vamos utilizar os ```States```.

Para relembrar, state em React é um objeto que representa o estado atual de um componente. Ele é utilizado para armazenar e controlar dados dinâmicos que podem ser atualizados ao longo do tempo.

O state é uma parte fundamental da arquitetura do React, permitindo que os componentes reajam a eventos, alterações de propriedades e interações do usuário. Ao atualizar o state de um componente, o React re-renderiza o componente e atualiza automaticamente a interface do usuário para refletir as mudanças.

Podemos pensar no state como uma variável especial, onde o componente react reage (por isso o nome react 🤔) à essa variável.

Para criar um state, vamos para o nosso JSX e utilizaremos o seguinte código:

``` JSX
  const [usuarios, setUsuarios] = useState([]);
```

Esse state será o responsável por armazenar o JSON com os dados do usuário. Os colchetes (```[]```) dentro do hook useState indica que nossa lista começará como uma lista vazia.

Não esqueça também de importar o useState

```JS
import { useState } from "react";
```

Nesse momento o código do componente deve ser o seguinte:

```JSX
import { useState } from "react";
import CardUsuario from "../../Components/CardUsuario/CardUsuario";
import axios from "axios";

function ListaDeUsuarios() {
  const [usuarios, setUsuarios] = useState([]);

  async function BuscarUsuarios() {
    const response = await axios.get(
      "https://localhost:44397/api/usuarios/listar"
    );

    if (response.status != 200) {
      alert("Erro ao listar usuários");
      return;
    }
  }

  return (
    <div>
      <CardUsuario nome="Lourival Cicero" idade="24"></CardUsuario>
      <CardUsuario nome="João" idade="32"></CardUsuario>
      <CardUsuario nome="Maria" idade="30"></CardUsuario>
    </div>
  );
}

export default ListaDeUsuarios;

```

Agora, precisamos armazenar o resultado da requisição dentro de nosso State, para isso, basta adicionarmos o seguinte código após a validação da requisição HTTP.

```JS
setUsuarios(response.data);
```

Pronto, assim nossa requisição está validada e devidamente armazenada, precisamos somente exibi-lá para o usuário.

```JSX
  async function BuscarUsuarios() {
    const response = await axios.get(
      "https://localhost:44342/api/usuarios/listar"
    );

    if (response.status != 200) {
      alert("Erro ao listar usuários");
      return;
    }

    setUsuarios(response.data);
  }
```

## Renderizando dados do State

Para renderizar os dados que armazenamos no state anteriormente, precisamos entender primeiro o processo que vamos seguir. Nosso JSON nesse momento é uma lista com alguns itens representando usuários, para cada item nessa lista, precisamos renderizar um componente de usuário, passando seus dados para ele via **props**.

Vamos então remover toda a parte visual de nosso componente, deixando somente uma div:

### Antes

``` HTML
    <div>
      <CardUsuario nome="Lourival Cicero" idade="24"></CardUsuario>
      <CardUsuario nome="João" idade="32"></CardUsuario>
      <CardUsuario nome="Maria" idade="30"></CardUsuario>
    </div>
```

### Depois

``` HTML
    <div>

    </div>
```

Então, vamos criar um laço de repetição dentro de nossa div, onde, para cada usuário na lista de usuários, vamos criar um componente para esse usuário.

Vamos utilizar o laço de repetição ```map```, talvez ele seja novo para você, mas não se preocupe, seu uso é simples e direto.

Com o laço de repetição ```map()```, podemos mapear cada item da nossa lista para um componente JSX, passando as propriedades necessárias. Isso nos permite renderizar dinamicamente uma lista de componentes com base nos dados fornecidos, facilitando a criação de listas ou grids de elementos em um aplicativo React.

Sua sintaxe será a seguinte:

```JSX
{
    usuarios.map(usuario => (
        <CardUsuario nome={usuario.nome} email={usuario.email}></CardUsuario>
     ))
}
```

Ou seja, para cada ```usuario``` em nossa lista chamada ```usuarios```, crie um componente ```CardUsuario``` e passe os dados desse ```usuario``` via props para o componente.

## UseEffect

Se você fez todas as mudanças anteriores, vai notar que a tela da aplicação está vazia, mas por quê?

A renderização de nossos componentes agora depende do nosso state, o state por sua vez depende da requisição HTTP para o backend, certo?

Pois bem, criamos a requisição, mas ainda **não executamos** nossa função ```BuscarUsuarios()```.

Precisamos executar essa função assim que carregarmos nossa página, para automaticamente realizar a requisição HTTP e exibir os dados em tela.

Para isso, vamos utilizar o UseEffect, que como vimos anteriormente, executa um "efeito colateral" em nosso código, ou seja, podemos utiliza-lo para disparar nossa função assim que a tela carregar, gerando um efeito similar ao evento "onLoad" no javascript.

Vamos adicionar o seguinte código ao nosso componente JSX:

``` JSX
  useEffect(() => {
    //Todo o código presente nessas chaves será executado quando a tela carregar
  }, []);
```

Não se esqueça de importar também o useEffect:

```JS
import { useEffect, useState } from "react";
```

Então basta chamar nossa função ```BuscarUsuarios()``` dentro do useEffect que nossa requisição será executada e nossos dados devem aparecer em tela.

``` JSX
  useEffect(() => {
    BuscarUsuarios();
  }, []);
```

Assim, está pronta nossa integração entre front-end e back-end, ao fim desse processo o código do seu componente deve ter a seguinte estrutura:

```JSX
import { useEffect, useState } from "react";
import CardUsuario from "../../Components/CardUsuario/CardUsuario";
import axios from "axios";

function ListaDeUsuarios() {
  const [usuarios, setUsuarios] = useState([]);

  useEffect(() => {
    BuscarUsuarios();
  }, []);

  async function BuscarUsuarios() {
    const response = await axios.get(
      "https://localhost:44397/api/usuarios/listar"
    );

    if (response.status != 200) {
      alert("Erro ao listar usuários");
      return;
    }
    console.log(response);
    setUsuarios(response.data);
  }

  return (
    <div>
      {usuarios.map((usuario) => (
        <CardUsuario nome={usuario.nome}></CardUsuario>
      ))}
    </div>
  );
}

export default ListaDeUsuarios;

```

E o resultado em tela deve ser o seguinte:

<h4 style="color:red">Em caso de erro, verifique se sua API está executando no Visual Studio.</h3>
