# Programação WEB II

## Integração com APIs

A integração com APIs externas é uma parte importante da maioria das aplicações modernas, pois permite que os componentes sejam alimentados com dados a partir de fontes externas. O React fornece várias maneiras de integrar-se com APIs externas, incluindo a utilização de bibliotecas como fetch ou axios. 

// 

Neste exemplo, o componente ExampleComponent integra-se a uma API externa usando o método fetch quando o componente é montado. Ele armazena os dados retornados da API no estado do componente e atualiza o componente com base nos dados. Além disso, ele também gerencia o estado de carregamento e erro para mostrar informações apropriadas ao usuário. 

## Fundamentos do HTTP

### O que é HTTP

HTTP (Hypertext Transfer Protocol) é o protocolo da web utilizado para transmitir dados entre um cliente (navegador) e um servidor. Ele é amplamente utilizado para transferência de páginas da web, imagens e outros tipos de arquivos. 

O HTTP é baseado em requisições e respostas. Quando um usuário acessa uma página da web, o navegador envia uma requisição HTTP ao servidor solicitando o arquivo desejado. O servidor então responde enviando o arquivo para o navegador, que o exibe para o usuário. 

Existem dois tipos principais de requisições HTTP: GET e POST. A requisição GET é utilizada para recuperar dados do servidor, enquanto a requisição POST é utilizada para enviar dados ao servidor. 

O HTTP também utiliza códigos de status para indicar o resultado da requisição. Alguns dos códigos de status mais comuns incluem 200 (OK), 404 (Arquivo não encontrado) e 500 (Erro interno do servidor). 

Ao compreender os conceitos básicos de HTTP, os desenvolvedores web estarão mais bem equipados para construir aplicações que fazem requisições HTTP e processam as respostas, como é o caso em muitas aplicações web modernas que utilizam APIs para acessar dados de outros sistemas.

### HTTP no Front-End e Back-End

O HTTP é usado para fazer requisições do front-end ao back-end e recuperar dados como HTML, JSON, imagens e outros tipos de arquivos. Por exemplo, quando um usuário acessa uma página da web, o navegador envia uma requisição HTTP ao servidor solicitando o HTML da página. O servidor responde enviando o HTML para o navegador, que o exibe para o usuário. 

O HTTP é uma parte fundamental da comunicação entre o front-end e o back-end em aplicações web, permitindo a transferência de dados e a criação de aplicações dinâmicas e interativas, mas vale ressaltar que as responsabilidades de criar requisições HTTP não é exclusiva do front-end, podemos também criar chamadas HTTP entre dois back-ends para integrar diferentes sistemas e compartilhar dados entre eles. 

Por exemplo, um sistema de gerenciamento de pedidos pode fazer uma requisição HTTP a um sistema de gerenciamento de estoque para verificar a disponibilidade de um produto antes de processar um pedido. Ou um sistema de pagamentos pode fazer uma requisição HTTP a um sistema de autenticação para verificar as informações de um cartão de crédito antes de processar uma transação. 

As chamadas HTTP entre back-ends podem ser feitas de várias maneiras, como o uso de APIs REST ou o uso de bibliotecas de comunicação HTTP em diferentes linguagens de programação. É importante considerar questões de segurança, como autenticação e criptografia, ao realizar chamadas HTTP entre back-ends. 

### HTTP na arquitetura cliente servidor  

A arquitetura cliente-servidor é uma arquitetura de software comum na qual os dados são compartilhados entre dois sistemas: o cliente e o servidor. O HTTP é amplamente utilizado na comunicação entre o cliente e o servidor em aplicações web. 

No modelo cliente-servidor, o cliente envia uma requisição HTTP ao servidor, solicitando informações ou dados. O servidor responde enviando os dados solicitados ao cliente. O cliente pode ser um navegador web, um aplicativo móvel ou qualquer outro tipo de software que precisa se comunicar com o servidor. O servidor pode ser um servidor web, um banco de dados ou qualquer outro tipo de software que armazena e processa dados. 

O HTTP é uma parte fundamental da arquitetura cliente-servidor, permitindo a transferência de dados entre cliente e servidor e possibilitando a criação de aplicações dinâmicas e interativas. 

## APIs

### O que é API

API significa "Application Programming Interface" em inglês. É uma interface de programação de software que permite que duas aplicações se comuniquem entre si. 

Uma API define a forma como as aplicações devem se comunicar, incluindo o que deve ser enviado e o que deve ser retornado. Ela permite que uma aplicação acesse os recursos ou serviços de outra aplicação sem precisar conhecer a implementação detalhada desta outra aplicação. 

Exemplos de uso de APIs incluem: 

* Integração de aplicações: Uma aplicação pode utilizar a API de outra aplicação para acessar seus recursos ou serviços. Por exemplo, uma aplicação pode utilizar a API do Google Maps para exibir mapas em sua interface. 

* Acesso a dados: Uma aplicação pode utilizar a API de outra aplicação para obter acesso a seus dados. Por exemplo, uma aplicação pode utilizar a API do Twitter para acessar tweets. 

* Automatização de tarefas: Uma aplicação pode utilizar a API de outra aplicação para automatizar tarefas. Por exemplo, uma aplicação pode utilizar a API de um banco para processar pagamentos automaticamente.

## Os pilares do HTTP

Para sintetizar, podemos descrever uma requisição HTTP em 5 grandes pilares: 

### Tipo do Método: 

Verbo que descreve a ação que a requisição vai executar  

* GET -> Pegar: Geralmente utilizado para consultar e buscar dados 

* POST -> Publicar: Utilizado para criar ou escrever um dado ou registo em nossa aplicação 

* PUT -> Colocar: Utilizado para alterar e colocar um novo dado em um registro criado anteriormente 

* DELETE -> Deletar: Utilizado para remover um registro 

Vale ressaltar que esses 4 verbos são os utilizados quando queremos trabalhar com as operações **CRUD** em nossa API.

### Rota:
A rota HTTP é a parte da URL que identifica um recurso específico que pode ser acessado através da API. Ela é composta pela URL base da API, seguida de uma "rota" que identifica o recurso desejado. Por exemplo, considerando a API "https://api.example.com", uma rota para acessar informações sobre usuários pode ser "https://api.example.com/users". 

A rota HTTP é usada para determinar como uma requisição HTTP deve ser processada pelo servidor. O servidor pode ter regras específicas para processar requisições HTTP com base na rota. Por exemplo, uma requisição GET para "https://api.example.com/users" pode retornar uma lista de todos os usuários, enquanto uma requisição GET para "https://api.example.com/users/1" pode retornar informações específicas sobre o usuário com ID 1. 

Além disso, as rotas também podem incluir parâmetros dinâmicos. Por exemplo, a rota "https://api.example.com/users/:id" pode permitir que o cliente especifique o ID do usuário que deseja acessar ao substituir ":id" pelo valor real do ID.

### Cabeçalho (Header)

O cabeçalho HTTP é uma parte importante da requisição e resposta HTTP que fornece informações adicionais sobre a requisição ou resposta. Ele contém vários campos, cada um dos quais é responsável por uma informação específica, como o tipo de conteúdo, a data e hora, o tamanho do conteúdo, o estado da autenticação etc. 

Alguns exemplos de campos comuns do cabeçalho HTTP incluem: 

* Content-Type: Especifica o tipo de conteúdo da resposta, como "application/json". 

* Authorization: Fornece informações de autenticação, como o token de autenticação do usuário. 

* Accept: Especifica os tipos de conteúdo que o cliente aceita na resposta. 

* Content-Length: Indica o tamanho em bytes do conteúdo da resposta. 

O cabeçalho HTTP é importante porque permite que o cliente e o servidor negociem informações adicionais sobre a requisição e a resposta, como o tipo de conteúdo, a autenticação e outras informações relevantes. Isso ajuda a garantir que a requisição e a resposta sejam processadas corretamente pelo cliente e pelo servidor.

### Corpo

O corpo da requisição HTTP é a parte da requisição que contém os dados enviados pelo cliente ao servidor. Ele é opcional e só é incluído na requisição se houver dados a serem enviados. Alguns exemplos de dados que podem ser enviados no corpo da requisição incluem informações de formulário, JSON, XML ou outros tipos de dados estruturados. 

O corpo da requisição é precedido pelo cabeçalho da requisição, que contém informações adicionais sobre a requisição, incluindo o tipo de conteúdo do corpo da requisição. Por exemplo, se o corpo da requisição contiver dados JSON, o cabeçalho da requisição pode incluir um campo "Content-Type" com o valor "application/json". 

Além disso, o corpo da requisição também pode ser codificado antes de ser enviado, dependendo da requisição. Por exemplo, pode ser necessário codificar os dados do corpo da requisição como URL codificado se a requisição for feita usando o método HTTP GET. 

### Status Code
Os códigos de status HTTP são códigos numéricos que indicam o resultado da requisição HTTP feita pelo cliente ao servidor. Eles são enviados pelo servidor como parte da resposta HTTP e permitem que o cliente saiba se a requisição foi bem-sucedida ou se houve algum problema. 

Alguns exemplos de códigos de status HTTP incluem: 

* 200 OK: Indica que a requisição foi bem-sucedida e o servidor retornou o conteúdo solicitado. 

* 201 Created: Indica que a requisição foi bem-sucedida e o servidor criou um registro como resultado. 

* 204 No Content: Indica que a requisição foi bem-sucedida, mas não há conteúdo para retornar. 

* 400 Bad Request: Indica que a requisição não foi compreendida pelo servidor devido a uma sintaxe inválida. 

* 401 Unauthorized: Indica que a requisição não foi autorizada devido a falta de autenticação ou autorização. 

* 403 Forbidden: Indica que a requisição não foi autorizada devido a restrições de autorização. 

* 404 Not Found: Indica que o recurso solicitado não foi encontrado pelo servidor. 

* 500 Internal Server Error: Indica que o servidor encontrou um erro ao processar a requisição. 

Existem muitos outros códigos de status HTTP, mas esses são alguns dos mais comuns. É importante que os desenvolvedores compreendam os códigos de status HTTP e saibam como lidar com eles na construção de aplicações web.

## JSON

### O que é o JSON

JSON (JavaScript Object Notation) é um formato de dados leve e independente de linguagem que é usado para transmitir dados entre sistemas. Ele é baseado na sintaxe de objeto do JavaScript, mas pode ser lido e interpretado por muitas outras linguagens de programação. 

O JSON é um formato de dados estruturado que é composto por pares chave/valor. Cada par chave/valor representa um atributo de um objeto. Os objetos são agrupados em uma série de elementos, que podem ser organizados em matrizes ou em uma hierarquia de objetos aninhados. 

O JSON é amplamente utilizado em aplicativos web e móveis como um formato de troca de dados. Ele é geralmente mais leve do que outros formatos de dados, como XML, o que o torna mais rápido e mais fácil de processar. Além disso, o JSON é fácil de ler e entender para humanos, o que torna a depuração de erros mais fácil. 

Aqui está um exemplo simples de um objeto JSON que contém informações sobre um usuário: 

``` JSON
{ 
  "nome": "João Silva", 
  "idade": 30, 
  "email": "joao.silva@email.com", 
  "endereco": { 
    "rua": "Rua das Flores", 
    "numero": 123, 
    "cidade": "São Paulo", 
    "estado": "SP"
  }, 
  "interesses": [ 
    "leitura", 
    "viagens", 
    "música" 
  ] 
}
```

Durante nossa integração de aplicações utilizaremos o formato de arquivo JSON para transportar dados do back-end para o front-end e vice-versa.

