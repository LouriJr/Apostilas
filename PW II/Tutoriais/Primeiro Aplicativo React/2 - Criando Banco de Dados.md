# Tutorial - Primeiro aplicativo React

Antes de prosseguirmos para a criação de todo o backend, será necessário criar e executar o script de banco de dados a seguir:

``` SQL
CREATE DATABASE Apostila;
USE Apostila;

CREATE TABLE Usuarios(
		ID INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
        Nome VARCHAR(255),
        Email VARCHAR(255),
        Telefone VARCHAR(255)
);

INSERT INTO Usuarios (Nome, Email, Telefone) Values 
('Lourival',  'lourival@gmail.com' , '(11)987654321'),
('João',  'joao@gmail.com' , '(11)123456789'),
('Maria',  'maria@gmail.com' , '(99)987654321');

```

Esse script cria um banco de dados chamado ```Apostila```, com uma tabela com o nome```Usuarios``` e por fim inserimos três usuários nessa tabela.

O intuito final dessa aplicação é exibir os dados inseridos nessa tabela na tela para o usuário.

Ou seja, no final do tutorial, caso queira inserir novos dados na tela, basta inserir novos dados nessa tabela.
