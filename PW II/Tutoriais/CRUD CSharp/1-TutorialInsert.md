# Adicionando um endpoint de cadastro (POST)

Até agora, nossa API possui apenas um endpoint que utiliza o método **HTTP GET** para listar os usuários cadastrados no banco. O método **GET** serve justamente para **consultar** informações, sem alterar os dados.

Agora, vamos dar o próximo passo e criar um endpoint de **cadastro de usuário**. Para isso, usaremos o método **HTTP POST**.

## O que é o HTTP POST?

Enquanto o **GET** busca dados existentes, o **POST** é utilizado quando queremos **enviar informações para o servidor** com o objetivo de **criar um novo registro**. Ou seja, é o verbo ideal quando precisamos cadastrar algo novo em nossa API.

``` C#
[HttpPost]
[Route("cadastrar")]
public IActionResult Cadastrar([FromBody] UsuarioDTO usuario)
{
    // Aqui iremos chamar o DAO para salvar o usuário no banco
    //Por enquanto a função está incompleta
}
```

### O que mudou?

1. **\[HttpPost\]**  
    Diferente do `Listar`, que usa `[HttpGet]`, agora usamos `[HttpPost]`, pois este endpoint será responsável por **inserir dados**.

2. **\[Route("cadastrar")\]**  
    Define o caminho da rota. Assim, nossa API poderá ser acessada pelo endereço:

    ``` bash
    POST /api/usuarios/cadastrar
    ```

3. **Parâmetro `UsuarioDTO usuario`**  
Usamos o atributo `[FromBody]` para indicar que o objeto `usuario` virá **no corpo da requisição (request body)**, em formato JSON.  
Exemplo de corpo que será enviado:

    ```json
    {
        "nome": "Maria Silva",
        "email": "maria@email.com",
        "telefone": "123456"
    }
    ```

No próximo passo, iremos implementar a lógica dentro do método `Cadastrar`, chamando a classe `UsuarioDAO` para inserir os dados no banco de dados e retornando uma resposta apropriada.

## Implementando a lógica de cadastro

No passo anterior, criamos o endpoint `Cadastrar`. Agora, vamos começar a implementar a lógica dentro dele para que nossa API consiga salvar novos usuários no banco.

Abra o arquivo `UsuariosController` e adicione o seguinte código:

```C#
[HttpPost]
[Route("cadastrar")]
public IActionResult Cadastrar(UsuarioDTO usuario)
{
    var dao = new UsuarioDAO();
    dao.CadastrarUsuario(usuario);

    return Ok("Usuário cadastrado com sucesso!");
}
```

### O que fizemos aqui?

1. **Instanciando o `UsuarioDAO`**  
    Criamos a linha:

    ```c#
    var dao = new UsuarioDAO();
    ```

    Isso significa que estamos **criando uma instância** da classe `UsuarioDAO`.  
    Uma instância nada mais é do que um "objeto real" criado a partir de uma classe.  
    Enquanto a classe é apenas o "molde", a instância é o objeto em uso, pronto para chamar métodos e acessar recursos.

    No nosso caso, essa instância (`dao`) é responsável por acessar o banco de dados para cadastrar o usuário.

2. **Chamando o método `CadastrarUsuario`**  
Logo depois, temos:

    ```c#
    dao.CadastrarUsuario(usuario);
    ```

    Aqui estamos chamando uma função chamada `CadastrarUsuario`, que será responsável por salvar o usuário no banco.  
    O `usuario` passado entre parênteses é o **parâmetro da função**.

    2.1 **[Off-Topic] O que é um parâmetro?**

    Um parâmetro é a informação que passamos para dentro de uma função, para que ela consiga trabalhar com esses dados.  
    No nosso caso, passamos um objeto do tipo `UsuarioDTO`, que contém os dados do usuário (nome, email, senha, etc.).

3. **Retornando uma resposta**  
    Por fim, usamos:

    ```c#
    return Ok("Usuário cadastrado com sucesso!");
    ```

    Esse retorno envia uma resposta HTTP **200 OK** para o cliente, junto com a mensagem `"Usuário cadastrado com sucesso!"`.

### Importante ⚠️

O método `CadastrarUsuario` **ainda não existe** na classe `UsuarioDAO`.  
Por isso, neste momento o código **vai dar erro de compilação**.

No próximo passo, iremos implementar esse método dentro da classe `UsuarioDAO` para que ele realmente grave os dados no banco de dados.

## Criando o método `CadastrarUsuario` no DAO

Agora que já configuramos o endpoint no `UsuariosController`, precisamos implementar o método responsável por inserir o usuário no banco de dados.

Para isso, vá até a classe **`UsuarioDAO`**.
Abaixo do método `ListarUsuarios`, crie um novo método chamado `CadastrarUsuario`, como no exemplo:

```C#
public void CadastrarUsuario(UsuarioDTO usuario)
{
    
}
```

### Entendendo o código

1. **`public`**  
    O modificador `public` significa que esse método pode ser acessado de qualquer parte do projeto.  
    Isso é importante porque o controller precisa "enxergar" esse método para poder utilizá-lo.

2. **`void`**  
    A palavra-chave **`void`** indica que este método **não retorna nada**.  
    Ou seja, ao ser chamado, ele executa sua lógica (no futuro, um `INSERT` no banco), mas não devolve nenhum valor diretamente para quem chamou.

   ### O que é um tipo de retorno?

    Em C#, cada método pode (ou não) devolver um resultado.

    - Quando um método **retorna algo**, ele precisa especificar o tipo desse retorno.  
        Exemplo:

    ```C#
        public int Somar(int a, int b) 
        {
            return a + b; // aqui o retorno é do tipo int 
        }
    ```

    - Quando um método **não retorna nada**, usamos o tipo especial `void`.

    No nosso caso, como o objetivo do método `CadastrarUsuario` é apenas **executar a ação de salvar** no banco de dados, não precisamos que ele devolva nada — por isso usamos `void`.

3. **Parâmetro `UsuarioDTO usuario`**  
    Assim como no controller, o método recebe como parâmetro um objeto `UsuarioDTO`.  
    Esse parâmetro carrega todas as informações do usuário que será cadastrado (nome, email, senha etc.).

## Implementando o `INSERT` no método `CadastrarUsuario`

Agora que criamos a estrutura do método `CadastrarUsuario`, vamos implementar de fato a lógica que insere os dados no banco de dados.

No arquivo **`UsuarioDAO`**, dentro do método `CadastrarUsuario`, adicione o seguinte código:

```C#
public void CadastrarUsuario(UsuarioDTO usuario)
{
    var conexao = ConnectionFactory.Build();
    conexao.Open();

    var query = @"INSERT INTO Usuarios (Nome, Email, Telefone) 
                  VALUES (@nome, @email, @telefone)";

    var comando = new MySqlCommand(query, conexao);
    comando.Parameters.AddWithValue("@nome", usuario.Nome);
    comando.Parameters.AddWithValue("@email", usuario.Email);
    comando.Parameters.AddWithValue("@telefone", usuario.Telefone);

    comando.ExecuteNonQuery();
    conexao.Close();
}
```

### Explicando o que foi feito

1. **Abrindo a conexão com o banco**

    ```C#
    var conexao = ConnectionFactory.Build(); 
    conexao.Open();
    ```

    Aqui usamos a `ConnectionFactory` para criar uma conexão com o banco.  
    Em seguida, chamamos `.Open()` para abrir de fato a comunicação.  
    Sem isso, não conseguiríamos executar nenhum comando SQL.

2. **Criando a query de inserção**

    ```C#
    var query = @"INSERT INTO Usuarios (Nome, Email, Telefone)
    VALUES (@nome, @email, @telefone)";
    ```

    Essa é a instrução SQL que será enviada ao banco.  

    Note que usamos **parâmetros com `@`** (`@nome`, `@email`, `@telefone`) em vez de colocar os valores diretamente.  
    Isso é importante porque:

    - Evita ataques de _SQL Injection_ (Caso queiram saber sobre, perguntem ao professor).

    - Facilita o reaproveitamento da query.

3. **Configurando o comando SQL**

    ```C#
    var comando = new MySqlCommand(query, conexao);
    ```

    Criamos um objeto `MySqlCommand`, que representa a instrução SQL que vamos executar no banco, associada à nossa conexão.

4. **Passando os parâmetros para a query**

    ```C#
    comando.Parameters.AddWithValue("@nome", usuario.Nome);
    comando.Parameters.AddWithValue("@email", usuario.Email);
    comando.Parameters.AddWithValue("@telefone", usuario.Telefone);
    ```

    Aqui substituímos os placeholders (`@nome`, `@email`, `@telefone`) pelos valores reais vindos do objeto `usuario` (do tipo `UsuarioDTO`).

    Esse é o ponto em que os dados recebidos da API são, de fato, preparados para entrar no banco.

5. **Executando o comando**

    ```C#
    comando.ExecuteNonQuery();
    ```

    O método `ExecuteNonQuery()` executa a instrução SQL no banco.  

    O nome _NonQuery_ significa que esse método é usado para comandos que **não retornam dados**, como `INSERT`, `UPDATE` ou `DELETE`.

6. **Fechando a conexão**

    ```C#
    conexao.Close();
    ```

    Após terminar, fechamos a conexão. Isso é uma boa prática para liberar recursos do banco de dados.

## Resumo

Neste passo, implementamos a lógica completa do **INSERT** no banco.

Agora, quando chamarmos o endpoint `POST /api/usuarios/cadastrar`, nossa API vai pegar os dados enviados no corpo da requisição, construir a query de inserção e gravar um novo usuário na tabela `Usuarios`.
