
[![NPM](https://img.shields.io/npm/l/react)](https://github.com/devsuperior/sds1-wmazoni/blob/master/LICENSE) 


## Sobre o projeto

Aplicação desktop desenvolvida utilizando JavaFX durante a realização de um curso de Java, com o objetivo de colocar em prática a criação de interfaces gráficas e a integração com banco de dados através de JDBC.

O sistema permite o gerenciamento de **departamentos** e **vendedores**, possibilitando cadastrar, editar, consultar e remover registros por meio de uma interface gráfica. Além disso, cada vendedor pode ser associado a um departamento, representando o relacionamento entre as entidades.

Durante o desenvolvimento foram aplicados conceitos de orientação a objetos, JavaFX, JDBC e tratamento de exceções. O sistema também possui validações de formulário e tratamento de exceções de integridade, impedindo operações que possam comprometer a consistência dos dados.

A interface foi construída utilizando FXML e CSS, proporcionando uma navegação mais organizada e uma melhor experiência de utilização.

## Modelo conceitual
![Modelo Conceitual](LINK_MODELO_CONCEITUAL)

## Imagens da aplicação

### Lista de vendedores

![Lista de Vendedores](LINK_LISTA_SELLERS)

### Lista de departamentos

![Lista de Departamentos](LINK_LISTA_DEPARTMENTS)

### Cadastro de vendedor

![Cadastro de Vendedor](LINK_CADASTRO_SELLER)

### Edição de vendedor

![Edição de Vendedor](LINK_EDICAO_SELLER)

# Tecnologias utilizadas

## Back end

* Java 26
* JavaFX 26.0.1
* JDBC
* FXML
* CSS

## Banco de dados

* MySQL Server
* MySQL Workbench
* MySQL Connector/J

# Como executar o projeto

## Pré-requisitos

* Java 26 ou superior (recomendado)
* JavaFX SDK 26.0.1 ou compatível com a versão do Java utilizada
* MySQL Server
* MySQL Workbench
* STS, Eclipse ou IntelliJ IDEA

Download do JavaFX:

```text
https://jdk.java.net/javafx26/
```

> Caso utilize outra versão do Java, recomenda-se utilizar uma versão compatível do JavaFX SDK.

## Clonar o repositório

```bash
git clone git@github.com:soleralucas/workshop-javafx-jdbc.git

cd workshop-javafx-jdbc
```

## Importando o projeto

### STS / Eclipse

1. Abra a IDE.
2. Clique em **File → Import**.
3. Selecione **Existing Projects into Workspace**.
4. Clique em **Next**.
5. Selecione a pasta do projeto clonado.
6. Clique em **Finish**.

## Configuração das bibliotecas

Após importar o projeto, acesse:

```text
Project → Properties → Java Build Path → Libraries
```

Caso existam referências quebradas ou bibliotecas não carregadas corretamente, remova-as antes de continuar.

### MySQL Connector/J

O projeto possui o MySQL Connector/J na pasta:

```text
lib
```

Caso necessário:

1. Clique em **Add JARs...** ou **Add External JARs...**
2. Selecione o arquivo do MySQL Connector presente na pasta `lib`.
3. Clique em **Apply and Close**.

### JavaFX SDK

Após baixar e extrair o JavaFX SDK:

1. Clique em **Add External JARs...**
2. Acesse a pasta:

```text
javafx-sdk-26.0.1/lib
```

3. Selecione todos os arquivos `.jar`.
4. Clique em **Open**.
5. Clique em **Apply and Close**.

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

## Configuração dos VM Arguments

Após configurar as bibliotecas e o banco de dados, é necessário adicionar os VM Arguments na IDE utilizada para permitir a execução correta do JavaFX.

No STS/Eclipse:

```text
Run → Run Configurations...
```

Selecione a classe principal da aplicação e acesse:

```text
Arguments
```

No campo **VM Arguments**, adicione:

```text
--module-path "CAMINHO_DO_JAVAFX_SDK\lib" --add-modules javafx.controls,javafx.fxml --enable-native-access=javafx.graphics -Dprism.order=sw
```

Exemplo:

```text
--module-path "D:\java-libs\javafx-sdk-26.0.1\lib" --add-modules javafx.controls,javafx.fxml --enable-native-access=javafx.graphics -Dprism.order=sw
```

> Substitua `CAMINHO_DO_JAVAFX_SDK` pelo diretório onde o JavaFX SDK foi instalado em sua máquina.

> Em algumas máquinas pode ser necessário utilizar o parâmetro `-Dprism.order=sw` para evitar problemas de compatibilidade gráfica durante a inicialização do JavaFX.

## Executando o projeto

Antes de executar a aplicação, verifique se o serviço do MySQL está em execução.

No Windows:

```text
Win + R
services.msc
```

Localize o serviço:

```text
MySQL
```

ou

```text
MySQL80
```

e confirme que ele está iniciado.

Após concluir todas as configurações:

```text
Run As → Java Application
```

A aplicação será iniciada e estará pronta para utilização.

# Autor

Lucas Pereira Solera

https://www.linkedin.com/in/lucas-pereira-solera/
