# Banco de Dados para Web

## hospedagem de sites

https://infinityfree.net/
https://br.000webhost.com/

## Criação da primeira página em HTML

### index.html
``` HTML
 <!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>This is a Heading</h1>
<p>This is a paragraph.</p>

</body>
</html> 
```
## Criação do SGDB

Um Sistema de Gerenciamento de Banco de Dados (SGBD) – do inglês Data Base Management System (DBMS) – é o conjunto de programas de computador (softwares) responsáveis pelo gerenciamento de uma base de dados. Seu principal objetivo é retirar da aplicação cliente a responsabilidade de gerenciar o acesso, a manipulação e a organização dos dados. O SGBD disponibiliza uma interface para que seus clientes possam incluir, alterar ou consultar dados previamente armazenados. Em bancos de dados relacionais a interface é constituída pelas APIs (Application Programming Interface) ou drivers do SGBD, que executam comandos na linguagem SQL (Structured Query Language).”
https://dicasdeprogramacao.com.br/o-que-e-um-sgbd/

Existem várias marcas de SGDB: Oracle, SQL Serve, PostgreSQL. 

O SGDB que vamos utilizar na disciplina é o MySql.

Nome do BD: id9489171_bd

Usuário BD:id9489171_usuario

## Criando o banco de dados

Utilizando o phpMyAdmin, foi criada uma tabela com 4 colunas.
Uma coluna1 recebeu Nome do usuário(id com incremento) tipo INT, a coluna2 o email tipo VARCHAR, coluna3 a senha tipo VARCHAR e a coluna4 endereço tipo VARCHAR.

## listar.php
``` php
<html>
  
  <head>
    
  </head>
  <body>
    <?php
  $servername = "localhost";
  $username = "id8850089_bd_dsi"; // modificar o usuário
  $password = "id8850089_bd_dsi";//modificar a senha
  $dbname = "id8850089_bd_dsi"; //modificar o banco de dados

// Create connection
$conn = new mysqli($servername, $username, $password,$dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
} 

$sql = "SELECT * FROM usuario";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    // output data of each row
    while($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"]. " - E-mail: " . $row["email"]."<br>";
    }
} else {
    echo "0 results";
}
$conn->close();
?>


    
  </body>
</html>

    
  </body>
</html>
```

## formulario.php
``` php
<!DOCTYPE html>
<html>
<body>

<form action="cadastrar.php">
  Nome:<br>
  <input type="text" name="nome">
  <br>
  e-mail:<br>
  <input type="text" name="email">
  <br><br>
  Endereco:<br>
  <input type="text" name="endereco">
  <br><br>
  senha:<br>
  <input type="password" name="senha">
  <br><br>
  <input type="submit" value="Cadastrar">
</form> 
  
  <a href="listar.php">Listar usuarios</a>


</body>
</html>
```
 
## cadastrar.php
``` php
<html>
<body>

Bem vindo <?php echo $_GET["nome"]; ?><br>
Tome cuidado, agora sei seu e-mail: <?php echo $_GET["email"]; ?>
  <?php
  $servername = "localhost";
  $username = "root";//modificar o usuario
  $password = "";//modificar a senha
  $dbname = "loja";//modificar o banco de dados

// Create connection
$conn = new mysqli($servername, $username, $password,$dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
} 
echo "<br>Sistema conectado ao sgbd";
  $nome = $_GET["nome"];
  $senha = sha1($_GET["senha"]);
  $email = $_GET["email"];
  $endereco = $_GET["endereco"];
  
  $sql = "INSERT INTO usuario (nome, email, senha, endereco)
VALUES ('".$nome."', '".$email."', '".$senha."', '".$endereco."')";

if ($conn->query($sql) === TRUE) {
    echo "Cadastrado com sucesso!";
} else {
    echo "Error: " . $sql . "<br>" . $conn->error;
}

$conn->close();
  
  ?>

</body>
</html>
```

