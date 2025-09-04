# Adicionando um endpoint de atualização (PUT)

Até agora, nossa API já consegue **cadastrar** usuários via **POST**.

O próximo passo é permitir **atualizar** os dados de um usuário existente. Para isso, usaremos o método **HTTP PUT**.

## O que é o HTTP PUT?

Enquanto o **POST** é usado para **criar** um novo registro, o **PUT** é utilizado para **atualizar** um recurso **já existente**.

```C#
[HttpPut]
[Route("atualizar/{id}")]
public IActionResult Atualizar([FromRoute] int id, [FromBody] UsuarioDTO usuario)
{
    // Aqui iremos chamar o DAO para atualizar o usuário no banco
    // Por enquanto a função está incompleta
}
```

### O que mudou?

1. **HttpPut**  
    Diferente do `Cadastrar` (que usa `[HttpPost]`), agora usamos `[HttpPut]`, pois este endpoint será responsável por **atualizar dados**.

2. **Route("atualizar/{id}")**  
    Definimos a rota incluindo o **`{id}`** do usuário que será atualizado.

    Assim, nossa API poderá ser acessada pelo endereço:

    ```Bash
    PUT /api/usuarios/atualizar/5
    ```

3. **Parâmetros `id` e `UsuarioDTO usuario`**

    - Usamos `[FromRoute] int id` para capturar o **identificador** do usuário diretamente da URL.

    - Usamos `[FromBody] UsuarioDTO usuario` para receber **o corpo** da requisição com os novos dados.

    Exemplo de corpo que será enviado:

    ```json
    {
        "nome": "Maria Silva",
        "email": "maria.nova@email.com",
        "telefone": "(11) 99999-0000"
    }
    ```

No próximo passo, iremos implementar a lógica dentro do método `Atualizar`, chamando a classe `UsuarioDAO` para executar a atualização no banco de dados e retornar uma resposta apropriada (`200 Ok` ou `404 Not Found` se o usuário não existir).

## Implementando a lógica de atualização no Controller

Abra o arquivo `UsuariosController` e adicione o seguinte código logo abaixo do endpoint de cadastro:

```C#
[HttpPut]
[Route("atualizar/{id}")]
public IActionResult Atualizar([FromRoute] int id, [FromBody] UsuarioDTO usuario)
{
    var dao = new UsuarioDAO();
    var linhasAfetadas = dao.AtualizarUsuario(id, usuario);

    if (linhasAfetadas == 0)
        return NotFound("Usuário não encontrado.");

    return Ok("Usuário atualizado com sucesso!");
}
```

### O que fizemos aqui?

1. **Instanciando o `UsuarioDAO`**  

    ``` C#
        var dao = new UsuarioDAO();
    ```

    Isso significa que estamos **criando uma instância** da classe `UsuarioDAO`.

    Lembrando: a classe é o “molde”; a **instância** é o objeto real em uso, capaz de **chamar métodos** e **acessar recursos**.  

    No nosso caso, essa instância (`dao`) é responsável por **acessar o banco** para atualizar o usuário.

2. **Chamando o método `AtualizarUsuario`**  
    Logo depois, temos:

    ``` C#
    var linhasAfetadas = dao.AtualizarUsuario(id, usuario);
    ```

    Aqui estamos chamando a função `AtualizarUsuario`, que fará o **UPDATE** no banco.

    - `id` e `usuario` são **parâmetros da função**.

   ### (Off-Topic) O que é um parâmetro?

    É a informação que passamos para dentro de uma função, para que ela consiga trabalhar com esses dados.  

    Neste caso, passamos o **identificador** via rota e o **objeto `UsuarioDTO`** com os novos valores.

3. **Retornando uma resposta**

    - Se `linhasAfetadas == 0`, significa que **nenhuma linha foi atualizada** — geralmente porque o `Id` não existe. Retornamos **`404 Not Found`**.

    - Caso contrário, retornamos **`200 OK`** com a mensagem de sucesso.

### Importante ⚠️

O método `AtualizarUsuario` **ainda não existe** na classe `UsuarioDAO`.

Por isso, neste momento o código **vai dar erro de compilação**.

No próximo passo, iremos implementar esse método dentro da classe `UsuarioDAO` para que ele realmente **atualize** os dados no banco de dados.

## Criando o método `AtualizarUsuario` no DAO

Agora que já configuramos o endpoint no `UsuariosController`, precisamos implementar o método responsável por atualizar o usuário no banco.

Vá até a classe **`UsuarioDAO`** e, abaixo do método `ListarUsuarios` (e do `CadastrarUsuario`, se já existir), crie um novo método chamado `AtualizarUsuario`, como no exemplo:

```C#
public int AtualizarUsuario(int id, UsuarioDTO usuario)
{
    
}
```

### Entendendo o código

1. **`public`**  
    O modificador `public` permite que o controller **acesse** esse método no DAO.

2. **Tipo de retorno `int`**  
    Diferente do `CadastrarUsuario` que era `void`, aqui optamos por retornar um **`int`** indicando **quantas linhas** foram afetadas no banco.  
    Isso nos ajuda a saber se o usuário realmente existia e foi atualizado.

   #### O que é um tipo de retorno?

    É o **tipo do valor** que um método devolve para quem o chamou.

    - Quando um método **não retorna nada**, usamos `void`.

    - Quando **retorna algo**, declaramos o tipo correspondente (ex.: `int`, `string`, um DTO, etc.).

3. **Parâmetros `int id, UsuarioDTO usuario`**  
    Recebemos o `id` (do usuário a ser alterado) e o objeto com os **novos dados**.

## Implementando o `UPDATE` no método `AtualizarUsuario`

Agora que criamos a assinatura do método, vamos escrever a lógica SQL.  
Dentro do método `AtualizarUsuario`, adicione o seguinte código:

```C#
public int AtualizarUsuario(int id, UsuarioDTO usuario)
{
    var conexao = ConnectionFactory.Build();
    conexao.Open();

    var query = @"UPDATE Usuarios
                  SET Nome = @nome,
                      Email = @email,
                      Telefone = @telefone
                  WHERE Id = @id";

    using var comando = new MySqlCommand(query, conexao);
    comando.Parameters.AddWithValue("@nome", usuario.Nome);
    comando.Parameters.AddWithValue("@email", usuario.Email);
    comando.Parameters.AddWithValue("@telefone", usuario.Telefone);
    comando.Parameters.AddWithValue("@id", id);

    var linhasAfetadas = comando.ExecuteNonQuery();
    conexao.Close();

    return linhasAfetadas;
}

```

### Explicando o que foi feito

1. **Abrindo a conexão com o banco**

    ``` C#
    var conexao = ConnectionFactory.Build(); 
    conexao.Open();
    ```

    Criamos e **abrimos** a conexão. Sem isso, nenhum comando SQL é executado.

2. **Criando a query de atualização**

    ``` C#
    var query = @"UPDATE Usuarios
                SET Nome = @nome,
                    Email = @email,
                    Telefone = @telefone
                WHERE Id = @id";
    ```

    Essa é a instrução SQL que fará o **UPDATE**.  

    **Atenção ao `WHERE Id = @id`**: sem ele, você **atualizaria todos os usuários** da tabela — um erro comum e perigoso.

3. **Configurando o comando SQL**

    ``` C#
    using var comando = new MySqlCommand(query, conexao);
    ```

    O `MySqlCommand` representa a instrução SQL que será executada.  
    Usamos `using` para garantir que o objeto seja **descartado corretamente** depois da execução.

4. **Passando os parâmetros para a query**

    ``` C#
    comando.Parameters.AddWithValue("@nome", usuario.Nome);
    comando.Parameters.AddWithValue("@email", usuario.Email);
    comando.Parameters.AddWithValue("@telefone", usuario.Telefone);
    comando.Parameters.AddWithValue("@id", id);
    ```

    Substituímos os placeholders pelos **valores reais** vindos do `UsuarioDTO` e do `id` da rota.

5. **Executando e capturando o número de linhas afetadas**

    ```C#
    var linhasAfetadas = comando.ExecuteNonQuery();
    ```

    `ExecuteNonQuery()` retorna um **inteiro** indicando quantas linhas foram modificadas.

    - `0` geralmente significa que **não encontrou** o usuário com aquele `Id`.

    - `>= 1` indica que a atualização ocorreu.

6. **Fechando a conexão**

    ```C#
    conexao.Close();
    ```

    Liberamos os recursos do banco.

## Resumo

Neste passo, implementamos a **atualização** de usuários via **PUT**.  
Agora, quando chamarmos:

``` http
PUT /api/usuarios/atualizar/5
```

Com um corpo como:

``` json
{
  "nome": "Maria Silva",
  "email": "maria.nova@email.com",
  "telefone": "(11) 99999-0000"
}
```

A API vai montar a query de **UPDATE** e alterar o registro na tabela `Usuarios`.

Se o `Id` não existir, retornará **`404 Not Found`**.

Caso contrário, **`200 OK`** com a mensagem de sucesso.
