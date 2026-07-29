# API - Exercita365

<p>
  <img alt="JavaScript" src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=000000">
  <img alt="Node.js" src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=FFFFFF">
  <img alt="Express" src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=FFFFFF">
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=FFFFFF">
  <img alt="Sequelize" src="https://img.shields.io/badge/Sequelize-52B0E7?style=for-the-badge&logo=sequelize&logoColor=FFFFFF">
  <img alt="Swagger" src="https://img.shields.io/badge/Swagger-85EA2D?style=for-the-badge&logo=swagger&logoColor=000000">
</p>

> Projeto colaborativo desenvolvido em equipe. Este repositório é um [fork do projeto original](https://github.com/gbetsa/Exercita365) e preserva seu histórico de commits e autoria.

## Descrição
O Exercita365 é uma plataforma que facilita o gerenciamento de exercícios e locais para atividades físicas serem praticadas. Os usuários podem cadastrar novos locais de exercícios, encontrar pontos próximos, visualizar informações sobre os exercícios em cada ponto e registrar suas próprias contribuições para o sistema.

## Requisitos Para Instalação do Projeto

1. **Node.js**: É a plataforma usada para executar o servidor. Certifique-se de instalar a versão recomendada. (18.x ou superior)
2. **npm**: O gerenciador de pacotes para Node.js, necessário para instalar as dependências do projeto. Normalmente é instalado junto com o Node.js. (versão recomendada: 8.x ou superior)
3. **PostgreSQL**: É o sistema de gerenciamento de banco de dados utilizado. Instale a versão compatível com o projeto. (13.x ou superior)

## Instalação

1. Clone o repositório:
  ```bash
  git clone https://github.com/Luizhprovin/Exercita365.git
  cd Exercita365
  ```
2. Instale as dependências:
  ```bash
  npm install
  ```

## Configurações
1. Crie um arquivo .env na raiz do projeto com as seguintes variáveis:
  ```bash
  APP_PORT= // Porta para executar o servidor

  DB_DIALECT=postgres
  DB_HOST= // Host da base de dados
  DB_USER= // Usuário da base de dados
  DB_PASSWORD= // Senha da base de dados
  DB_DATABASE= // Nome da base de dados
  DB_PORT= // Porta da base de dados

  JWT_KEY= // Chave JWT
  ```

## Scripts
   ```bash
   npm run start:prod
   ```
-  Este comando executa várias etapas importantes no ambiente de produção:
  1. **Criação do Banco de Dados**: Executa `npx sequelize-cli db:create` para criar o banco de dados se ele ainda não existir.
  2. **Migrações do Banco de Dados**: Executa `npx sequelize-cli db:migrate` para aplicar as migrações e estruturar o banco de dados conforme definido nos arquivos de migração.
  3. **Inserção de Dados Iniciais**: Executa `npx sequelize-cli db:seed:all` para popular o banco de dados com dados iniciais definidos nos arquivos de seed.
  4. **Geração da Documentação do Swagger**: Executa `node ./autogen.swagger.js` para gerar a documentação da API usando Swagger.
  5. **Início do Servidor**: Executa `node ./src/index.js` para iniciar o servidor da aplicação.

## Swagger
Acesse a rota `/doc` para acessar a interface do Swagger e utilizar as rotas.

## Cadastro e Login
Efetue o cadastro de um novo usuário com os parâmetros descritos abaixo e realize o login para obter um token de acesso. Utilize esse token no cabeçalho para obter acesso as rotas.

## Rotas

### Usuários

- **Cadastrar Usuário**
  - **URL:** `/usuarios`
  - **Método:** `POST`
  - **Descrição:** Cadastra um novo usuário.
  - **Corpo da Requisição:**
  ```json
  {
  "nome": "STRING",
  "email": "STRING",
  "sexo": "ENUN('Masculino', 'Feminino', 'Outro')",
  "cpf": "STRING",
  "endereco": "STRING",
  "data_nascimento": "DATE",
  "password_hash": "STRING"
  }
  ```
- **Login do Usuário**
  - **URL:** `/login`
  - **Método:** `POST`
  - **Descrição:** Realiza o login do usuário.
  - **Corpo da Requisição:**
  ```json
  {
  "email": "STRING",
  "senha": "STRING"
  }
  ```
### Locais de Exercício

- **Cadastrar Local de Exercício**
  - **URL:** `/locais`
  - **Método:** `POST`
  - **Descrição:** Cadastra um novo local de exercício.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
  - **Corpo da Requisição:**
  ```json
  {
  "nome": "STRING",
  "descricao": "STRING",
  "cep": "STRING",
  "numero": "STRING",
  "atividades_id": [ INTERGER, INTERGER ]
  }
  ```
- **Listar Locais de Exercício**
  - **URL:** `/locais`
  - **Método:** `GET`
  - **Descrição:** Lista todos os locais de exercício cadastrados pelo usuário logado.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
- **Listar Local de Exercício Especifico**
  - **URL:** `/locais/{local_id}`
  - **Método:** `GET`
  - **Descrição:** Listar um local cadastrado pelo usuário logado.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
- **Deletar Local de Exercício**
  - **URL:** `/locais/{local_id}`
  - **Método:** `DELETE`
  - **Descrição:** Deleta um local cadastrado pelo usuário logado.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
- **Atualizar Local de Exercício**
  - **URL:** `/locais/{local_id}`
  - **Método:** `PUT`
  - **Descrição:** Deletar um local cadastrado pelo usuário logado.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
  - **Corpo da Requisição:**
  ```json
  {
  "nome": "STRING",
  "descricao": "STRING",
  "cep": "STRING",
  "numero": "STRING",
  "atividades_id": [ INTERGER, INTERGER ]
  }
  ```
- **Listar link do Google Maps de um Local de Exercício Especifico**
  - **URL:** `/locais/{local_id}/maps`
  - **Método:** `GET`
  - **Descrição:** Listar link do google maps de um local de exercício cadastrados pelo usuário logado.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
### Atividades (Somente usuários administradores tem acesso.)
#### Usuário administrador:
Efetue o login com esses dados.
  ```json
  {
  "email": "admin@example.com",
  "password_hash": "password123"
  }
  ```

- **Cadastrar Uma nova Atividade**
  - **URL:** `/atividades`
  - **Método:** `POST`
  - **Descrição:** Cadastrar uma nova categoria de atividade de exercicios.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
  - **Corpo da Requisição:**
  ```json
  {
  "categoria": "STRING"
  }
  ```
- **Deletar Uma Atividade**
  - **URL:** `/atividades/{atividade_id}`
  - **Método:** `DELETE`
  - **Descrição:** Deletar uma categoria de atividade de exercicios.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
### Permissões (Somente usuários administradores tem acesso.)
#### Usuário administrador:
Efetue o login com esses dados.
  ```json
  {
  "email": "admin@example.com",
  "password_hash": "password123"
  }
  ```

- **Cadastrar Uma Nova Permissão**
  - **URL:** `/permissoes`
  - **Método:** `POST`
  - **Descrição:** Cadastrar uma nova permissão de acesso.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
  - **Corpo da Requisição:**
  ```json
  {
  "nome": "STRING"
  }
  ```
- **Atribuir Uma Nova Permissão**
  - **URL:** `/permissoes/atribuir-permissoes`
  - **Método:** `POST`
  - **Descrição:** Atribuir uma nova permissão a um usuário.
  - **Cabeçalho da requisição:**
  ```json
  {
  authorization: Bearer <token>
  }
  ```
  - **Corpo da Requisição:**
  ```json
  {
  "usuario_id": INTERGER,
  "permissao_id": INTERGER
  }
  ```
## Banco de Dados

O banco de dados utiliza os seguintes relacionamentos:

- Usuários e Locais: Um usuário pode estar associado a muitos locais (relacionamento 1 entre Usuários e Locais).
- Usuários e Permissões: Muitos usuários podem ter muitas permissões (relacionamento N entre Usuários e Permissões, mediado pela tabela Usuarios_Permissoes).
- Locais e Atividades: Muitos locais podem estar associados a muitas atividades (relacionamento N entre Locais e Atividades, mediado pela tabela Locais_Atividades).

![image](https://github.com/user-attachments/assets/0f1a2b02-5f62-4e9e-a48c-7e166e0a8906)

## Tecnologias

- JavaScript e Node.js
- Express
- PostgreSQL
- Sequelize e Sequelize CLI
- JSON Web Token
- Swagger

## Autoria e colaboração

Desenvolvido de forma colaborativa. Consulte o [repositório de origem](https://github.com/gbetsa/Exercita365) para conhecer o projeto e seu histórico completo. Este fork integra o portfólio de [Luiz Henrique Provin](https://github.com/Luizhprovin) sem remover os créditos dos demais participantes.
