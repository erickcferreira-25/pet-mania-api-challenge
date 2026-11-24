# 🐾 Pet Mania

API REST para gerenciamento de pets para adoção, desenvolvida com **Spring Boot**. O projeto também serve uma página web ("Pet Mania | Adoção de Pets") na raiz da aplicação.

## Tecnologias

- Java 21
- Spring Boot (Spring Web + Spring Data JPA)
- Maven
- MySQL
- Jakarta Persistence (JPA/Hibernate)

## Estrutura do projeto

```
com.dt2.petmania
├── PetManiaApplication.java        # Classe principal
├── controllers
│   └── PetController.java          # Endpoints REST de /api/pets
├── entities
│   ├── Pet.java                    # Entidade (tabela tb_pet)
│   └── enums
│       ├── Porte.java              # PEQUENO, MEDIO, GRANDE
│       └── Sexo.java               # MACHO, FEMEA
└── repositories
    └── PetRepository.java          # JpaRepository<Pet, Long>
```

## Modelo de dados

Tabela `tb_pet`:

| Campo         | Tipo    | Descrição                                |
|---------------|---------|------------------------------------------|
| id            | Long    | Chave primária (auto incremento)         |
| nome          | String  | Nome do pet                              |
| especie       | String  | Espécie (ex.: Cachorro, Gato)            |
| raca          | String  | Raça (ex.: SRD)                          |
| idade         | int     | Idade                                    |
| sexo          | Enum    | `MACHO` ou `FEMEA`                       |
| porte         | Enum    | `PEQUENO`, `MEDIO` ou `GRANDE`           |
| personalidade | String  | Descrição do temperamento                |
| foto          | String  | URL/caminho da foto                      |
| disponivel    | boolean | Indica se está disponível para adoção    |

## Como executar

### Pré-requisitos

- JDK 21
- Maven
- MySQL em execução

### Configuração do banco

Crie o banco e configure o `src/main/resources/application.properties` com os seus dados:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/<nome_do_banco>
spring.datasource.username=<usuario>
spring.datasource.password=<senha>
spring.jpa.hibernate.ddl-auto=update
```

### Rodando

```bash
mvn spring-boot:run
```

A aplicação sobe em `http://localhost:8080`.

## Endpoints

Base URL: `http://localhost:8080/api/pets`

| Método | Rota        | Descrição                | Status                  |
|--------|-------------|--------------------------|-------------------------|
| GET    | `/api/pets` | Lista todos os pets      | ✅ Implementado         |
| POST   | `/api/pets` | Cadastra um novo pet     | ✅ Implementado         |
| DELETE | `/api/pets/{id}` | Remove um pet       | 🚧 A implementar        |

### Exemplo: cadastrar pet (POST)

```json
{
  "nome": "Teste de cadastro",
  "especie": "Cachorro",
  "raca": "SRD",
  "idade": 2,
  "sexo": "FEMEA",
  "porte": "MEDIO",
  "personalidade": "Docil",
  "foto": "",
  "disponivel": true
}
```

### Exemplo: resposta (GET)

```json
[
  {
    "nome": "Teste de cadastro",
    "especie": "Cachorro",
    "raca": "SRD",
    "idade": 2,
    "sexo": "FEMEA",
    "porte": "MEDIO",
    "personalidade": "Docil",
    "foto": "",
    "disponivel": true,
    "id": 1
  }
]
```

## Testando

Os endpoints podem ser testados com o [Postman](https://www.postman.com/):

1. `POST localhost:8080/api/pets` com o corpo JSON acima (raw → JSON).
2. `GET localhost:8080/api/pets` para listar os pets cadastrados.
3. `GET localhost:8080` para abrir a página inicial.

## Próximos passos

- [ ] Implementar `DELETE /api/pets/{id}`
- [ ] Endpoints de busca por id e atualização (PUT)
- [ ] Filtros por espécie, porte e disponibilidade
- [ ] Validação dos dados de entrada
