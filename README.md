# API Raízes do Nordeste

Projeto desenvolvido para a disciplina de Desenvolvimento Back-End.

Sistema para gerenciamento da rede de lanchonetes Raízes do Nordeste, contemplando autenticação JWT, gerenciamento de produtos, estoque, pedidos, pagamento mock e programa de fidelidade.

---

# Tecnologias Utilizadas

- Node.js
- Express
- PostgreSQL
- JWT (JSON Web Token)
- Bcrypt
- Swagger
- Postman

---

# Requisitos

Antes de executar o projeto é necessário possuir:

- Node.js instalado
- PostgreSQL instalado
- Git instalado
- Postman (opcional para testes)

---

# Instalação

Clone o repositório:

```bash
git clone https://github.com/gabrielferrazByte/projeto-backend-raizes-do-nordeste.git
```

Entre na pasta do projeto:

```bash
cd projeto-raizes-nordeste
```

Instale as dependências:

```bash
npm install
```

---

# Configuração do Banco de Dados

Abra o PostgreSQL ou pgAdmin.

Crie o banco:

```sql
CREATE DATABASE raizes_nordeste;
```

Execute o arquivo:

```text
database/schema.sql
```

Esse arquivo irá criar:

- Tabelas
- Relacionamentos
- Enums
- Estrutura completa do banco

---

# Configuração da Conexão

Abra o arquivo:

```text
src/config/database.js
```

Configure as credenciais do PostgreSQL:

```javascript
const pool = new Pool({
  user: 'postgres',
  host: 'localhost',
  database: 'raizes_nordeste',
  password: '3124',
  port: 5432
});
```

```text
3124 foi a senha utilizada na instalação do PostgreSQL.
```

---

# Executar a Aplicação

Inicie o servidor:

```bash
npm run dev
```

Se tudo estiver correto aparecerá:

```text
Servidor rodando na porta 3000
```

---

# Testando a API

URL base:

```text
http://localhost:3000
```

Teste inicial:

```text
GET /
```

Resposta esperada:

```json
{
  "mensagem": "API Raízes do Nordeste funcionando"
}
```

---

# Ordem de Testes no Postman

## 1. Cadastro

```http
POST /auth/register
```

Exemplo:

```json
{
  "nome": "Gabriel",
  "email": "gabriel@email.com",
  "senha": "123456",
  "perfil": "CLIENTE"
}
```

---

## 2. Login

```http
POST /auth/login
```

Exemplo:

```json
{
  "email": "gabriel@email.com",
  "senha": "123456"
}
```

A resposta retornará um JWT.

---

## 3. Acesso à Rota Protegida

```http
GET /perfil
```

Adicionar:

```text
Authorization: Bearer TOKEN
```

---

## 4. Produtos

Criar Produto:

```http
POST /produtos
```

Listar Produtos:

```http
GET /produtos
```

---

## 5. Estoque

Entrada:

```http
POST /estoque/entrada
```

Saída:

```http
POST /estoque/saida
```

---

## 6. Pedidos

Criar Pedido:

```http
POST /pedidos
```

Exemplo:

```json
{
  "usuario_id": 1,
  "unidade_id": 1,
  "canal_pedido": "APP",
  "valor_total": 59.90
}
```

---

## 7. Pagamento Mock

```http
POST /pagamentos
```

Exemplo:

```json
{
  "pedido_id": 1,
  "metodo": "PIX",
  "status": "APROVADO"
}
```

---

## 8. Fidelidade

Consultar:

```http
GET /fidelidade/1
```

Acumular:

```http
POST /fidelidade/acumular
```

Resgatar:

```http
POST /fidelidade/resgatar
```

---

# Swagger

A documentação pode ser acessada em:

```text
http://localhost:3000/api-docs
```

---

# Principais Endpoints

## Autenticação

```http
POST /auth/register
POST /auth/login
GET /perfil
```

## Produtos

```http
GET /produtos
POST /produtos
PUT /produtos/:id
DELETE /produtos/:id
```

## Estoque

```http
GET /estoque
POST /estoque/entrada
POST /estoque/saida
```

## Pedidos

```http
GET /pedidos
GET /pedidos/:id
POST /pedidos
PATCH /pedidos/:id/status
```

## Pagamentos

```http
POST /pagamentos
```

## Fidelidade

```http
GET /fidelidade/:usuario_id
POST /fidelidade/acumular
POST /fidelidade/resgatar
```

---

# Testes

Os testes foram realizados utilizando Postman.

Os cenários contemplam:

- Login
- Autenticação JWT
- Produtos
- Estoque
- Pedidos
- Pagamento Mock
- Fidelidade
- Validações de erro

---

# Observações

- O sistema utiliza autenticação JWT.
- As senhas são armazenadas utilizando bcrypt.
- O pagamento é simulado (mock), não realizando transações reais.
- A tabela `log_auditoria` foi modelada no banco, porém os registros automáticos não foram implementados nesta versão.

---

# Autor

Gabriel Ferraz Lima Freitas