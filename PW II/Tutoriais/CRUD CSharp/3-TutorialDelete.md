# Adicionando um endpoint de exclusão (DELETE)

Já temos **cadastro (POST)** e **atualização (PUT)**.

Agora vamos permitir **excluir** um usuário existente. Para isso, usaremos o método **HTTP DELETE**.

## O que é o HTTP DELETE?

Enquanto o **POST** cria e o **PUT** atualiza, o **DELETE** é utilizado para **remover** um recurso existente.

```csharp
[HttpDelete]
[Route("deletar/{id}")]
public IActionResult Deletar([FromRoute] int id)
{
    // Aqui iremos chamar o DAO para excluir o usuário do banco
    // Por enquanto a função está incompleta
}
```

### O que mudou?

1. **[HttpDelete]**  
   Diferente do `Cadastrar` (`[HttpPost]`) e do `Atualizar` (`[HttpPut]`), agora usamos **`[HttpDelete]`** porque este endpoint **remove dados**.

2. **[Route("deletar/{id}")]**  
   Incluímos o **`{id}`** do usuário a ser removido na rota:

   ```bash
   DELETE /api/usuarios/deletar/5
   ```

3. **Parâmetro `id`**  
   Usamos `[FromRoute] int id` para capturar o **identificador** diretamente da URL.

---

No próximo passo, iremos implementar a lógica dentro do método `Deletar`, chamando a classe `UsuarioDAO` para executar a exclusão no banco de dados e retornar uma resposta apropriada.

## Implementando a lógica de exclusão no Controller

Abra o arquivo `UsuariosController` e adicione o seguinte código:

```csharp
[HttpDelete]
[Route("deletar/{id}")]
public IActionResult Deletar([FromRoute] int id)
{
    var dao = new UsuarioDAO();
    var linhasAfetadas = dao.DeletarUsuario(id);

    if (linhasAfetadas == 0)
        return NotFound("Usuário não encontrado.");

    return Ok("Usuário excluído com sucesso!");
}
```

### O que fizemos aqui?

1. **Instanciando o `UsuarioDAO`**  

   ```csharp
   var dao = new UsuarioDAO();
   ```

   Criamos uma **instância** (objeto real) de `UsuarioDAO`. A classe é o molde; a instância é o objeto em uso que consegue **chamar métodos** e **acessar recursos**. Ela será responsável por falar com o banco para excluir o usuário.

2. **Chamando o método `DeletarUsuario`**

   ```csharp
   var linhasAfetadas = dao.DeletarUsuario(id);
   ```

   Chamamos a função que fará o **DELETE** no banco. O `id` é o **parâmetro** usado para indicar qual registro excluir.

   **[Off-Topic] O que é um parâmetro?**  
   É a informação que passamos para dentro de uma função para que ela execute sua lógica com base nesses dados. Aqui, é o identificador do usuário.

3. **Retornando uma resposta**  
   - Se `linhasAfetadas == 0`, significa que **nenhuma linha foi excluída** — normalmente porque o `Id` não existe. Retornamos **`404 Not Found`**.  
   - Caso contrário, retornamos **`200 OK`** com mensagem de sucesso (ou **`204 No Content`** se preferir resposta sem corpo).

### Importante ⚠️

O método `DeletarUsuario` **ainda não existe** na classe `UsuarioDAO`.  
Por isso, neste momento o código **vai dar erro de compilação**.

No próximo passo, iremos implementar esse método dentro da classe `UsuarioDAO` para que ele realmente **remova** o usuário no banco de dados.

## Criando o método `DeletarUsuario` no DAO

Vá até a classe **`UsuarioDAO`** e, abaixo dos métodos já criados, adicione a assinatura do novo método:

```csharp
public int DeletarUsuario(int id)
{
    
}
```

### Entendendo o código

1. **`public`**  
   Permite que o controller **acesse** esse método no DAO.

2. **Tipo de retorno `int`**  
   Vamos retornar um **`int`** indicando **quantas linhas** foram afetadas no banco. Isso ajuda a diferenciar entre “não encontrado” (0) e “excluído” (1).

3. **Parâmetro `int id`**  
   É o identificador do usuário que será removido.

## Implementando o `DELETE` no método `DeletarUsuario`

Agora, vamos escrever a lógica SQL. Dentro do método, adicione:

```csharp
public int DeletarUsuario(int id)
{
    var conexao = ConnectionFactory.Build();
    conexao.Open();

    var query = @"DELETE FROM Usuarios
                  WHERE Id = @id";

    using var comando = new MySqlCommand(query, conexao);
    comando.Parameters.AddWithValue("@id", id);

    var linhasAfetadas = comando.ExecuteNonQuery();
    conexao.Close();

    return linhasAfetadas;
}
```

### Explicando o que foi feito

1. **Abrindo a conexão com o banco**

   ```csharp
   var conexao = ConnectionFactory.Build();
   conexao.Open();
   ```

   Criamos e **abrimos** a conexão para poder executar a instrução SQL.

2. **Criando a query de exclusão**

   ```csharp
   var query = @"DELETE FROM Usuarios
                 WHERE Id = @id";
   ```

   Essa é a instrução SQL que **remove** o registro.  
   **Atenção ao `WHERE Id = @id`**: sem esse filtro, você excluiria **todos os usuários** — erro crítico e comum.

3. **Configurando o comando SQL**

   ```csharp
   using var comando = new MySqlCommand(query, conexao);
   ```

   Representa a instrução a ser executada. O `using` garante o **descarte correto** do objeto após o uso.

4. **Passando o parâmetro**

   ```csharp
   comando.Parameters.AddWithValue("@id", id);
   ```

   Substitui `@id` pelo valor recebido do controller.

5. **Executando e capturando o número de linhas afetadas**

   ```csharp
   var linhasAfetadas = comando.ExecuteNonQuery();
   ```

   Retorna um **inteiro** com a quantidade de linhas removidas.  
   - `0` → usuário não encontrado  
   - `1` → exclusão realizada

6. **Fechando a conexão**

   ```csharp
   conexao.Close();
   ```

   Libera os recursos.

## Resumo

Com isso, implementamos a exclusão de usuários via **DELETE**.  
Ao chamar:

```bash
DELETE /api/usuarios/deletar/5
```

a API executa o **DELETE** na tabela `Usuarios`.

Se o `Id` não existir, retornará **`404 Not Found`**.

Se existir, **`200 OK`** com mensagem (ou **`204 No Content`**, se preferir).
