# 🚀 ThreadFlow - API REST de Blog

[![Java](https://img.shields.io/badge/Java-17+-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2+-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15+-blue.svg)](https://www.postgresql.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

API REST completa para gerenciamento de blog com sistema de autenticação JWT, autorização por roles e documentação
interativa com Swagger.

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Tecnologias](#tecnologias)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Configuração](#configuração)
- [Executando a Aplicação](#executando-a-aplicação)
- [Documentação da API](#documentação-da-api)
- [Testes](#testes)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Endpoints](#endpoints)
- [Contribuindo](#contribuindo)
- [Licença](#licença)

## 🎯 Sobre o Projeto

ThreadFlow é uma API REST moderna desenvolvida com Spring Boot que oferece todas as funcionalidades necessárias para um
blog completo, incluindo autenticação segura, sistema de permissões e recursos avançados de busca e paginação.

### ✨ Destaques

- 🔐 **Autenticação JWT** - Sistema seguro de autenticação baseado em tokens
- 👥 **Sistema de Roles** - Controle granular de permissões (USER, ADMIN, MODERATOR)
- 📝 **CRUD Completo** - Posts e comentários com todas as operações
- 🔍 **Busca Avançada** - Pesquisa em títulos e conteúdos com paginação
- 📄 **Paginação** - Resultados paginados para melhor performance
- ✅ **Validações** - Validação robusta de dados com Bean Validation
- 🧪 **Testes Completos** - Cobertura de testes unitários e de integração
- 📚 **Documentação Interativa** - Swagger UI para testar a API em tempo real

## 🚀 Funcionalidades

### Autenticação e Autorização

- [x] Registro de novos usuários
- [x] Login com geração de token JWT
- [x] Autenticação via Bearer Token
- [x] Sistema de roles (USER, ADMIN, MODERATOR)
- [x] Controle de acesso baseado em permissões

### Gerenciamento de Posts

- [x] Criar posts (usuários autenticados)
- [x] Listar posts com paginação
- [x] Buscar posts por título/conteúdo
- [x] Visualizar post individual
- [x] Editar próprios posts
- [x] Deletar próprios posts
- [x] Admins podem gerenciar todos os posts

### Sistema de Comentários

- [x] Adicionar comentários em posts
- [x] Listar comentários de um post
- [x] Editar próprios comentários
- [x] Deletar próprios comentários
- [x] Moderadores podem deletar qualquer comentário

### Gerenciamento de Usuários

- [x] Visualizar perfil próprio
- [x] Listar usuários (apenas admins)
- [x] Buscar usuário por ID
- [x] Atualizar dados do perfil

## 🛠️ Tecnologias

### Backend

- **Java 17** - Linguagem de programação
- **Spring Boot 3.2+** - Framework principal
- **Spring Security** - Segurança e autenticação
- **Spring Data JPA** - Persistência de dados
- **Hibernate** - ORM
- **PostgreSQL** - Banco de dados principal
- **H2** - Banco de dados para testes
- **JWT (jjwt)** - Geração e validação de tokens
- **Bean Validation** - Validação de dados
- **Lombok** - Redução de boilerplate

### Documentação

- **SpringDoc OpenAPI 3** - Geração automática de documentação
- **Swagger UI** - Interface interativa da API

### Testes

- **JUnit 5** - Framework de testes
- **Mockito** - Mocks para testes unitários
- **Spring Boot Test** - Testes de integração
- **MockMvc** - Testes de controllers

### Build & Deploy

- **Maven** - Gerenciamento de dependências
- **Docker** - Containerização 

## 📦 Pré-requisitos

Antes de começar, você precisa ter instalado:

- [Java JDK 17+](https://www.oracle.com/java/technologies/downloads/)
- [Maven 3.8+](https://maven.apache.org/download.cgi)
- [PostgreSQL 15+](https://www.postgresql.org/download/)
- [Git](https://git-scm.com/)

## 🔧 Instalação

1. **Clone o repositório**

```bash
git clone https://github.com/Felipe-SMZ/threadflow-api
cd threadflow-api
```

2. **Crie o banco de dados PostgreSQL**

```sql
CREATE
DATABASE threadflow;
CREATE
USER threadflow_user WITH PASSWORD 'sua_senha';
GRANT ALL PRIVILEGES ON DATABASE
threadflow TO threadflow_user;
```

3. **Configure as variáveis de ambiente** (ou edite `application.properties`)

```bash
export DB_HOST=localhost
export DB_PORT=5432
export DB_NAME=threadflow
export DB_USERNAME=threadflow_user
export DB_PASSWORD=sua_senha
export JWT_SECRET=seu_secret_key_256_bits
```

4. **Instale as dependências**

```bash
./mvnw clean install
```

## ⚙️ Configuração

### application.properties

```properties
# Database
spring.datasource.url=jdbc:postgresql://localhost:5432/threadflow
spring.datasource.username=threadflow_user
spring.datasource.password=sua_senha
# JPA/Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=false
spring.jpa.properties.hibernate.format_sql=true
# JWT
jwt.secret=404E635266556A586E3272357538782F413F4428472B4B6250645367566B5970
jwt.expiration=86400000
# Server
server.port=8080
# Swagger
springdoc.swagger-ui.path=/swagger-ui.html
springdoc.api-docs.path=/v3/api-docs
```

## 🚀 Executando a Aplicação

### Desenvolvimento

```bash
./mvnw spring-boot:run
```

### Produção

```bash
./mvnw clean package
java -jar target/threadflow-0.0.1-SNAPSHOT.jar
```

### Com Docker (opcional)

```bash
docker-compose up -d
```

A aplicação estará disponível em: `http://localhost:8080`

## 📚 Documentação da API

### Swagger UI (Recomendado)

Acesse a documentação interativa em:

```
http://localhost:8080/swagger-ui.html
```

### OpenAPI JSON

Documentação em formato JSON:

```
http://localhost:8080/v3/api-docs
```

### Como usar o Swagger

1. Acesse `http://localhost:8080/swagger-ui.html`
2. Registre um usuário em `POST /api/auth/register`
3. Faça login em `POST /api/auth/login` e copie o token
4. Clique no botão **"Authorize"** 🔒 no topo
5. Cole o token (sem o prefixo "Bearer")
6. Agora você pode testar todos os endpoints protegidos!

## 🧪 Testes

### Executar todos os testes

```bash
./mvnw test
```

### Executar apenas testes unitários

```bash
./mvnw test -Dtest=*Test
```

### Executar apenas testes de integração

```bash
./mvnw test -Dtest=*IntegrationTest
```

### Ver cobertura de testes

```bash
./mvnw jacoco:report
```

Relatório disponível em: `target/site/jacoco/index.html`

### Estatísticas de Testes

- ✅ 20+ testes unitários
- ✅ 15+ testes de integração
- ✅ Cobertura de ~80% do código
- ✅ Testes de permissões e autorização
- ✅ Testes de validação de dados

## 📁 Estrutura do Projeto

```
threadflow/
├── src/
│   ├── main/
│   │   ├── java/com/blog/
│   │   │   ├── config/          # Configurações (Security, JWT, Swagger)
│   │   │   ├── controller/      # Controllers REST
│   │   │   ├── dto/             # Data Transfer Objects
│   │   │   ├── exception/       # Exceções customizadas
│   │   │   ├── model/           # Entidades JPA
│   │   │   ├── repository/      # Repositórios Spring Data
│   │   │   ├── security/        # Classes de segurança
│   │   │   └── service/         # Lógica de negócio
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       ├── java/com/blog/
│       │   ├── controller/      # Testes de integração
│       │   └── service/         # Testes unitários
│       └── resources/
│           └── application-test.properties
├── pom.xml
├── README.md
└── docker-compose.yml
```

## 🔗 Endpoints

### Autenticação

| Método | Endpoint             | Descrição              | Autenticação |
|--------|----------------------|------------------------|--------------|
| POST   | `/api/auth/register` | Registrar novo usuário | ❌ Não        |
| POST   | `/api/auth/login`    | Fazer login            | ❌ Não        |

### Posts

| Método | Endpoint            | Descrição               | Autenticação  |
|--------|---------------------|-------------------------|---------------|
| GET    | `/api/posts`        | Listar posts (paginado) | ❌ Não         |
| GET    | `/api/posts/{id}`   | Buscar post por ID      | ❌ Não         |
| GET    | `/api/posts/search` | Buscar posts por termo  | ❌ Não         |
| POST   | `/api/posts`        | Criar novo post         | ✅ USER        |
| PUT    | `/api/posts/{id}`   | Atualizar post          | ✅ OWNER       |
| DELETE | `/api/posts/{id}`   | Deletar post            | ✅ OWNER/ADMIN |

### Comentários

| Método | Endpoint                          | Descrição            | Autenticação      |
|--------|-----------------------------------|----------------------|-------------------|
| GET    | `/api/posts/{postId}/comentarios` | Listar comentários   | ❌ Não             |
| POST   | `/api/posts/{postId}/comentarios` | Criar comentário     | ✅ USER            |
| PUT    | `/api/comentarios/{id}`           | Atualizar comentário | ✅ OWNER           |
| DELETE | `/api/comentarios/{id}`           | Deletar comentário   | ✅ OWNER/MODERATOR |

### Usuários

| Método | Endpoint             | Descrição          | Autenticação |
|--------|----------------------|--------------------|--------------|
| GET    | `/api/usuarios/me`   | Ver perfil próprio | ✅ USER       |
| GET    | `/api/usuarios`      | Listar usuários    | ✅ ADMIN      |
| GET    | `/api/usuarios/{id}` | Buscar usuário     | ✅ USER       |

## 📝 Exemplos de Uso

### 1. Registrar Usuário

```bash
curl -X POST http://localhost:8080/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "email": "john@example.com",
    "password": "senha123",
    "nome": "John Doe"
  }'
```

### 2. Fazer Login

```bash
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "password": "senha123"
  }'
```

Resposta:

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "type": "Bearer",
  "username": "johndoe",
  "email": "john@example.com",
  "roles": [
    "USER"
  ]
}
```

### 3. Criar Post

```bash
curl -X POST http://localhost:8080/api/posts \
  -H "Authorization: Bearer SEU_TOKEN_AQUI" \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Meu Primeiro Post",
    "conteudo": "Este é o conteúdo do meu post!"
  }'
```

### 4. Listar Posts

```bash
curl http://localhost:8080/api/posts?page=0&size=10
```

### 5. Buscar Posts

```bash
curl http://localhost:8080/api/posts/search?termo=java&page=0&size=10
```

## 🔐 Sistema de Roles

### USER (Padrão)

- Criar, editar e deletar próprios posts
- Criar, editar e deletar próprios comentários
- Visualizar todos os posts e comentários públicos

### MODERATOR

- Todas as permissões de USER
- Deletar comentários de qualquer usuário
- Moderar conteúdo inadequado

### ADMIN

- Todas as permissões de MODERATOR
- Deletar posts de qualquer usuário
- Gerenciar usuários
- Acesso total ao sistema

## 🐛 Tratamento de Erros

A API retorna respostas consistentes para erros:

```json
{
  "timestamp": "2024-01-20T10:30:00",
  "status": 400,
  "error": "Bad Request",
  "message": "Email já está em uso",
  "path": "/api/auth/register"
}
```

### Códigos de Status HTTP

- `200 OK` - Requisição bem-sucedida
- `201 Created` - Recurso criado com sucesso
- `204 No Content` - Operação bem-sucedida sem conteúdo
- `400 Bad Request` - Dados inválidos
- `401 Unauthorized` - Não autenticado
- `403 Forbidden` - Sem permissão
- `404 Not Found` - Recurso não encontrado
- `500 Internal Server Error` - Erro no servidor


## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👨‍💻 Autor

**Felipe Shimizu**

- GitHub: [Felipe-SMZ](https://github.com/Felipe-SMZ)
- LinkedIn: [https://www.linkedin.com/in/felipesshimizu]


---

⭐ Se este projeto te ajudou, considere dar uma estrela!

**Desenvolvido com ❤️ usando Spring Boot**
