# CRUD em PHP
### Código 1

## 1. Descrição do problema
Durante a análise, foram encontrados alguns erros no código que poderiam impedir o sistema de funcionar corretamente.

Também foi encontrado um problema de segurança relacionado ao uso de comandos SQL. Para melhorar a segurança, foram utilizados Prepared Statements.

Os problemas encontrados foram:

- falta de ";" em algumas linhas;
- problemas que poderiam acontecer durante a execução das consultas;
- risco de SQL Injection.

---

## 2. Os 3 erros de sintaxe/execução

Erro 1 - Falta de ponto e vírgula no "bind_param()"<br>
Erro 2 - Falta de ponto e vírgula no "query()"<br>
Erro 3 - Falta de tratamento das consultas

## 3. Falha de segurança

A principal falha de segurança encontrada foi o risco de SQL Injection.<br>
SQL Injection acontece quando uma pessoa consegue colocar comandos SQL dentro dos campos do sistema.
### Para evitar isso, foram utilizados Prepared Statements.

## 4. Correção de cada
### 4.1 Cadastro

O cadastro foi feito utilizando Prepared Statement.

<b>Código:</b>

$sql = "INSERT INTO usuarios (nome, email) VALUES (?, ?)";<br>
$stmt = $conn->prepare($sql);<br>
$stmt->bind_param("ss", $nome, $email);<br>
$stmt->execute();

### 4.2 Exclusão

A exclusão também foi corrigida utilizando Prepared Statement.

<b>Código:</b>

$sql = "DELETE FROM usuarios WHERE id = ?";<br>
$stmt = $conn->prepare($sql);<br>
$stmt->bind_param("i", $id);<br>
$stmt->execute();


### 4.3 Edição

A edição utiliza três parâmetros:

$sql = "UPDATE usuarios SET nome = ?, email = ? WHERE id = ?";<br>
$stmt = $conn->prepare($sql);<br>
$stmt->bind_param("ssi", $nome, $email, $id);<br>
$stmt->execute();

Os tipos são:

s = nome, texto;<br>
s = e-mail, texto;<br>
i = ID, número inteiro.

### 4.4 Busca dos usuários

<b>A busca ficou:</b>

$sql = "SELECT id, nome, email FROM usuarios ORDER BY id DESC";<br>
$resultado = $conn->query($sql);

Também foi corrigido o ; que estava faltando.

### 4.5 Correção dos erros de sintaxe

Os dois pontos onde faltavam ; foram corrigidos.

$stmt->bind_param("ssi", $nome, $email, $id);<br>
$resultado = $conn->query($sql);
