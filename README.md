# 🛒 Workshop Spring Boot + JPA

![Java](https://img.shields.io/badge/Java-17+-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![JPA](https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![H2](https://img.shields.io/badge/H2_Database-004088?style=for-the-badge&logo=h2&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white)

> API REST desenvolvida com Spring Boot e JPA/Hibernate, com foco em boas práticas de arquitetura em camadas, tratamento de exceções personalizado e modelagem de domínio com relacionamentos entre entidades.

---

## 📋 Sobre o projeto

Este projeto foi desenvolvido como parte de um workshop prático de Spring Boot com JPA. O objetivo é construir uma API RESTful completa com domínio de e-commerce, abordando desde a modelagem das entidades até o tratamento adequado de erros HTTP.

---

## 🏗️ Arquitetura

O projeto segue o padrão de **arquitetura em camadas**, separando responsabilidades de forma clara:

```
├── resources/          → Controllers REST (camada de apresentação)
│   └── exceptions/     → Tratamento global de exceções HTTP
├── services/           → Regras de negócio
│   └── exceptions/     → Exceções de domínio
├── repositories/       → Acesso a dados (Spring Data JPA)
├── entities/           → Entidades do domínio / modelos
└── config/             → Configurações e seed de dados
```

---

## 🗂️ Modelo de Domínio

O sistema modela um contexto de e-commerce com as seguintes entidades e relacionamentos:

```
User  ───< Order >─── OrderItem >─── Product
                │
               Payment
                │
             Category
```

- **User** faz múltiplos **Orders**
- **Order** contém múltiplos **Products** via **OrderItem** (tabela associativa com atributo extra: quantidade e preço)
- **Order** possui um **Payment**
- **Product** pertence a uma ou mais **Categories**

---

## ✨ Funcionalidades

- ✅ CRUD completo de usuários, pedidos, produtos e categorias
- ✅ Relacionamentos JPA: `@OneToMany`, `@ManyToMany`, `@OneToOne`, `@ManyToOne`
- ✅ Tratamento de exceções centralizado com `@ControllerAdvice`
- ✅ Respostas de erro padronizadas (timestamp, status, mensagem, path)
- ✅ Banco de dados H2 em memória com dados de teste pré-carregados
- ✅ Console H2 disponível em desenvolvimento

---

## 🛠️ Tecnologias utilizadas

| Tecnologia | Finalidade |
|---|---|
| Java 17+ | Linguagem principal |
| Spring Boot 3.x | Framework base |
| Spring Data JPA | Persistência e acesso a dados |
| Hibernate | Implementação JPA / ORM |
| H2 Database | Banco de dados em memória |
| Maven | Gerenciamento de dependências |
| Jakarta EE | Servlets e anotações |

---

## 🚀 Como executar

### Pré-requisitos

- Java 17 ou superior
- Maven 3.8+

### Passo a passo

```bash
# Clone o repositório
git clone git@github.com:Ketketpli/workshop-springboot-jpa.git

# Acesse a pasta do projeto
cd workshop-springboot-jpa

# Execute o projeto
./mvnw spring-boot:run
```

A aplicação estará disponível em `http://localhost:8080`.

### Console H2 (banco de dados em memória)

Acesse `http://localhost:8080/h2-console` com as credenciais configuradas em `application.properties`.

---

## 🔗 Endpoints principais

### Usuários
| Método | Endpoint | Descrição |
|---|---|---|
| `GET` | `/users` | Lista todos os usuários |
| `GET` | `/users/{id}` | Busca usuário por ID |
| `POST` | `/users` | Cria novo usuário |
| `PUT` | `/users/{id}` | Atualiza usuário |
| `DELETE` | `/users/{id}` | Remove usuário |

### Pedidos
| Método | Endpoint | Descrição |
|---|---|---|
| `GET` | `/orders` | Lista todos os pedidos |
| `GET` | `/orders/{id}` | Busca pedido por ID |

### Produtos
| Método | Endpoint | Descrição |
|---|---|---|
| `GET` | `/products` | Lista todos os produtos |
| `GET` | `/products/{id}` | Busca produto por ID |

### Categorias
| Método | Endpoint | Descrição |
|---|---|---|
| `GET` | `/categories` | Lista todas as categorias |
| `GET` | `/categories/{id}` | Busca categoria por ID |

---

## ⚠️ Tratamento de Exceções

O projeto implementa um mecanismo centralizado de tratamento de erros:

**`ResourceNotFoundException`** → lançada quando um recurso não é encontrado pelo ID informado.

**`ResourceExceptionHandler`** → intercepta as exceções via `@ControllerAdvice` e retorna respostas HTTP padronizadas.

**Exemplo de resposta de erro (404):**
```json
{
  "timestamp": "2024-01-15T10:30:00Z",
  "status": 404,
  "error": "Resource not found",
  "message": "Resource not found. Id 99",
  "path": "/users/99"
}
```

---

## 📚 Conceitos praticados

- Arquitetura em camadas (Resources → Services → Repositories)
- Mapeamento objeto-relacional com JPA/Hibernate
- Relacionamentos entre entidades (`@OneToMany`, `@ManyToMany`, `@ManyToOne`, `@OneToOne`)
- Tabela associativa com atributos extras (`OrderItem`)
- Enumerações com JPA (`@Enumerated`)
- Tratamento de exceções com `@ControllerAdvice` e `@ExceptionHandler`
- Perfis de ambiente com Spring Profiles (`test`, `dev`, `prod`)
- Seed de dados com `CommandLineRunner`

---

## 👨‍💻 Autor

Feito por **Paulo H** — projeto desenvolvido para fins educacionais e de portfólio.

[![GitHub](https://img.shields.io/badge/GitHub-Ketketpli-181717?style=flat&logo=github)](https://github.com/Ketketpli)
