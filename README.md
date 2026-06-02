
[![NPM](https://img.shields.io/npm/l/react)](https://github.com/devsuperior/sds1-wmazoni/blob/master/LICENSE) 

# Demo DAO JDBC

## Sobre o projeto

Demo DAO JDBC é uma aplicação Java desenvolvida com o objetivo de praticar o acesso a banco de dados utilizando JDBC e padrões de projeto.

O sistema possui duas entidades principais: **Seller** e **Department**, onde um departamento pode possuir vários vendedores.

Durante o desenvolvimento foram implementadas operações de consulta, inserção, atualização e remoção de dados utilizando JDBC, aplicando o padrão **DAO (Data Access Object)** para separar a lógica de acesso aos dados das demais regras da aplicação.

Além disso, foi utilizado o padrão **Factory** para centralizar a criação e gerenciamento das conexões com o banco de dados, reduzindo o acoplamento entre as classes.

O projeto também implementa tratamento de exceções de integridade referencial do banco de dados. Dessa forma, não é possível excluir um departamento que possua vendedores associados, garantindo a consistência dos dados e respeitando os relacionamentos existentes entre as entidades.

## Modelo conceitual

### Estrutura das entidades

![Modelo Conceitual](https://raw.githubusercontent.com/soleralucas/assets/main/demo-dao-jdbc/Captura%20de%20tela%202026-06-01%20174535.png)

![Modelo Conceitual](https://raw.githubusercontent.com/soleralucas/assets/main/demo-dao-jdbc/Captura%20de%20tela%202026-06-01%20174555.png)

# Tecnologias utilizadas

## Back end

* Java 21
* JDBC
* Maven
* DAO Pattern
* Factory Pattern

## Banco de dados

* MySQL Server
* MySQL Workbench
* MySQL Connector/J

# Como executar o projeto

## Pré-requisitos

* Java 21 ou superior
* Maven
* MySQL Server
* MySQL Workbench
* STS, Eclipse ou IntelliJ IDEA

## Clonar o repositório

```bash
git clone git@github.com:soleralucas/demo-dao-jdbc.git

cd demo-dao-jdbc
```

## Importando o projeto

### STS / Eclipse

1. Abra a IDE.
2. Clique em **File → Import**.
3. Expanda **Maven**.
4. Selecione **Existing Maven Projects**.
5. Clique em **Next**.
6. Em **Root Directory**, clique em **Browse**.
7. Selecione a pasta do projeto clonado.
8. Clique em **Finish**.

O Maven realizará automaticamente o download das dependências necessárias, incluindo o MySQL Connector/J.

## Configuração do banco de dados

Crie um banco de dados MySQL com o nome:

```sql
CREATE DATABASE coursejdbc;
```

Após criar o banco, execute o script abaixo para criar as tabelas:

```sql
CREATE TABLE department (
  Id int(11) NOT NULL AUTO_INCREMENT,
  Name varchar(60) DEFAULT NULL,
  PRIMARY KEY (Id)
);

CREATE TABLE seller (
  Id int(11) NOT NULL AUTO_INCREMENT,
  Name varchar(60) NOT NULL,
  Email varchar(100) NOT NULL,
  BirthDate datetime NOT NULL,
  BaseSalary double NOT NULL,
  DepartmentId int(11) NOT NULL,
  PRIMARY KEY (Id),
  FOREIGN KEY (DepartmentId) REFERENCES department (Id)
);
```

Em seguida, execute o script para popular o banco de dados:

```sql
INSERT INTO department (Name) VALUES
('Computers'),
('Electronics'),
('Fashion'),
('Books');

INSERT INTO seller (Name, Email, BirthDate, BaseSalary, DepartmentId) VALUES
('Bob Brown','bob@gmail.com','1998-04-21 00:00:00',1000,1),
('Maria Green','maria@gmail.com','1979-12-31 00:00:00',3500,2),
('Alex Grey','alex@gmail.com','1988-01-15 00:00:00',2200,1),
('Martha Red','martha@gmail.com','1993-11-30 00:00:00',3000,4),
('Donald Blue','donald@gmail.com','2000-01-09 00:00:00',4000,3),
('Alex Pink','bob@gmail.com','1997-03-04 00:00:00',3000,2);
```

## Configuração do arquivo db.properties

Configure o arquivo `db.properties` com as credenciais do seu ambiente MySQL:

```properties
user=SEU_USUARIO
password=SUA_SENHA
dburl=jdbc:mysql://localhost:3306/coursejdbc
useSSL=false
```

> É necessário informar um usuário e senha válidos do MySQL instalado em sua máquina.

## Executando o projeto

Localize os programas de teste na pasta:

```text
src/application
```

Execute os programas através da IDE utilizando:

```text
Run As → Java Application
```

## Funcionalidades implementadas

### SellerDAO

* findById
* findByDepartment
* findAll
* insert
* update
* deleteById

### DepartmentDAO

* findById
* findAll
* insert
* update
* deleteById

# Autor

Lucas Pereira Solera

https://www.linkedin.com/in/lucas-pereira-solera/
