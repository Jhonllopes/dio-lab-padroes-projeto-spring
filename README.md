# Lab Padrões de Projeto com Spring Boot

## Descrição

Este projeto foi desenvolvido como parte do desafio da Digital Innovation One (DIO), com o objetivo de demonstrar a aplicação prática dos padrões de projeto (Design Patterns) utilizando Java, Spring Boot e integração com APIs externas.

A aplicação disponibiliza uma API REST para gerenciamento de clientes, realizando integração automática com a API ViaCEP para obtenção de dados de endereço a partir do CEP informado.

---

## Tecnologias Utilizadas

* Java 21
* Spring Boot
* Spring Data JPA
* Spring Cloud OpenFeign
* Banco de Dados H2
* Maven
* API ViaCEP
* Git e GitHub

---

## Padrões de Projeto Utilizados

### Singleton

O padrão Singleton é utilizado através do gerenciamento de beans realizado pelo Spring Framework.

Exemplos:

```java
@Service
public class ClienteServiceImpl
```

```java
@Autowired
private ClienteRepository clienteRepository;
```

O Spring cria uma única instância dos componentes anotados com `@Service`, `@Repository` e os disponibiliza através da injeção de dependência.

---

### Strategy

O padrão Strategy é aplicado por meio da interface `ClienteService` e sua implementação `ClienteServiceImpl`.

Interface:

```java
public interface ClienteService
```

Implementação:

```java
public class ClienteServiceImpl implements ClienteService
```

Essa abordagem permite criar novas implementações da estratégia sem alterar o restante do sistema.

---

### Facade

O padrão Facade está representado pela classe:

```java
ClienteRestController
```

Essa classe oferece uma interface simplificada para o consumo dos serviços da aplicação, abstraindo toda a complexidade de integração com banco de dados e API externa.

---

## Integração com ViaCEP

A aplicação utiliza o Spring Cloud OpenFeign para consumir a API ViaCEP.

Exemplo:

```java
@FeignClient(name = "viacep", url = "https://viacep.com.br/ws")
public interface ViaCepService
```

Ao cadastrar um cliente informando apenas o CEP, o sistema consulta automaticamente a API ViaCEP e obtém os dados completos do endereço.

---

## Estrutura do Projeto

```text
src/main/java
│
├── controller
│   └── ClienteRestController
│
├── model
│   ├── Cliente
│   ├── Endereco
│   ├── ClienteRepository
│   └── EnderecoRepository
│
├── service
│   ├── ClienteService
│   ├── ViaCepService
│   └── impl
│       └── ClienteServiceImpl
│
└── Application
```

---

## Endpoints Disponíveis

### Buscar todos os clientes

```http
GET /clientes
```

### Buscar cliente por ID

```http
GET /clientes/{id}
```

### Cadastrar cliente

```http
POST /clientes
```

Exemplo:

```json
{
  "nome": "Jhonatan",
  "endereco": {
    "cep": "01001000"
  }
}
```

### Atualizar cliente

```http
PUT /clientes/{id}
```

### Remover cliente

```http
DELETE /clientes/{id}
```

---

## Como Executar o Projeto

### Clonar o Repositório

```bash
git clone <URL_DO_REPOSITORIO>
```

### Acessar a Pasta

```bash
cd lab-padroes-projeto-spring
```

### Executar a Aplicação

```bash
./mvnw spring-boot:run
```

No Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

---

## Banco de Dados H2

A aplicação utiliza o banco H2 em memória para armazenamento dos dados.

Após iniciar a aplicação, os dados podem ser consultados através dos endpoints REST.

---

## Autor

Jhonatan Lopes Caldas

Projeto desenvolvido para fins na plataforma Digital Innovation One (DIO), demonstrando a aplicação dos padrões de projeto Singleton, Strategy e Facade utilizando Spring Boot.

