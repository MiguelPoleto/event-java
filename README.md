# Event Java

## Sobre o Projeto

O **Event Java** é um sistema de gerenciamento de eventos desenvolvido em Java, utilizando MySQL como banco de dados. O sistema permite a criação de eventos, o cadastro de usuários e a realização de inscrições, incluindo indicações de outros participantes.

## Principais Funcionalidades
- Cadastro e gerenciamento de eventos
- Registro de usuários
- Inscrição em eventos, incluindo indicações
- Persistência de dados em um banco MySQL

## Tecnologias Utilizadas
- **Java**
- **MySQL**
- **JPA/Hibernate** (caso utilize)
- **Maven/Gradle** (caso utilize para dependências)
- **Postman** - Para testar as requisições da API

## Como Clonar e Configurar o Projeto

### 1. Clonar o Repositório
```bash
git clone https://github.com/MiguelPoleto/event-java.git
cd event-java
```

### 2. Configurar o Banco de Dados MySQL
1. Certifique-se de ter o MySQL instalado e rodando.
2. Acesse o MySQL e execute o seguinte script SQL para criar o banco de dados e tabelas:

```sql
-- Criar o schema\CREATE SCHEMA IF NOT EXISTS `db_events` DEFAULT CHARACTER SET utf8mb3;
USE `db_events`;

-- Criar a tabela de eventos
CREATE TABLE IF NOT EXISTS `db_events`.`tbl_event` (
  `event_id` INT NOT NULL AUTO_INCREMENT,
  `title` VARCHAR(255) NOT NULL,
  `pretty_name` VARCHAR(50) NOT NULL UNIQUE,
  `location` VARCHAR(255) NOT NULL,
  `price` DOUBLE NOT NULL,
  `start_date` DATE NULL DEFAULT NULL,
  `end_date` DATE NULL DEFAULT NULL,
  `start_time` TIME NULL DEFAULT NULL,
  `end_time` TIME NULL DEFAULT NULL,
  PRIMARY KEY (`event_id`)
) ENGINE = InnoDB;

-- Criar a tabela de usuários
CREATE TABLE IF NOT EXISTS `db_events`.`tbl_user` (
  `user_id` INT UNSIGNED NOT NULL AUTO_INCREMENT,
  `user_name` VARCHAR(255) NULL DEFAULT NULL,
  `user_email` VARCHAR(255) NULL DEFAULT NULL,
  PRIMARY KEY (`user_id`)
) ENGINE = InnoDB;

-- Criar a tabela de inscrições
CREATE TABLE IF NOT EXISTS `db_events`.`tbl_subscription` (
  `subscription_number` INT UNSIGNED NOT NULL AUTO_INCREMENT,
  `subscribed_user_id` INT UNSIGNED NOT NULL,
  `indication_user_id` INT UNSIGNED NULL DEFAULT NULL,
  `event_id` INT NOT NULL,
  PRIMARY KEY (`subscription_number`),
  FOREIGN KEY (`event_id`) REFERENCES `db_events`.`tbl_event` (`event_id`),
  FOREIGN KEY (`subscribed_user_id`) REFERENCES `db_events`.`tbl_user` (`user_id`),
  FOREIGN KEY (`indication_user_id`) REFERENCES `db_events`.`tbl_user` (`user_id`)
) ENGINE = InnoDB;
```

### 3. Configurar o Arquivo de Conexão
Edite o arquivo de configuração para definir as credenciais do banco de dados:

**Exemplo (application.properties ou persistence.xml, dependendo do framework usado):**
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/db_events
spring.datasource.username=SEU_USUARIO
spring.datasource.password=SUA_SENHA
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
```

### 4. Rodar o Projeto
- Se for um projeto **Maven**, utilize:
  ```bash
  mvn spring-boot:run
  ```
- Se for um projeto **Gradle**, utilize:
  ```bash
  gradle bootRun
  ```

Caso seja uma aplicação Java standalone, execute a classe principal do projeto.

### 5. Testando a API
Para testar as requisições da API (GET, POST, PUT, DELETE), utilize uma ferramenta como o Postman ou cURL.

## Contribuição
Contribuições são bem-vindas! Para contribuir:
1. Fork o repositório
2. Crie uma branch para suas modificações (`git checkout -b minha-feature`)
3. Commit suas alterações (`git commit -m 'Adicionando nova funcionalidade'`)
4. Envie para o repositório remoto (`git push origin minha-feature`)
5. Abra um Pull Request

## Contato

Caso tenha dúvidas ou sugestões, entre em contato:
- GitHub: [MiguelPoleto](https://github.com/MiguelPoleto)
- LinkedIn: [miguelpoleto](https://www.linkedin.com/in/miguelpoleto/)
- E-mail: *miguelpoleto5@gmail.com*
- Instagram: [@miguelsantuchi](https://www.instagram.com/miguelsantuchi/)

