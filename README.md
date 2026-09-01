# Central Inteligente de Consulta Empresarial

**Aluno:** Emmanoel Shiroshi Tanaka
**RA:** 237221
**Disciplina:** Integração de APIs

## Objetivo

Aplicação web que consulta dados de uma empresa a partir do CNPJ, integrando
duas APIs públicas, consolidando as informações e armazenando o resultado em
um banco de dados no-code (Airtable), com uma interface simples para consulta.

## Arquitetura

```
Usuário
  ↓
Interface HTML (public/index.html)
  ↓
Node.js / Express (src/server.ts)
  ↓
BrasilAPI  →  ViaCEP  →  Normalização  →  Airtable
  ↓
Resultado apresentado ao usuário
```

## APIs utilizadas

### BrasilAPI
Fornece dados cadastrais empresariais públicos (razão social, nome fantasia,
situação cadastral e CEP) a partir do CNPJ informado.

### ViaCEP
Complementa e padroniza o endereço (logradouro, bairro, cidade, UF e
complemento) a partir do CEP retornado pela BrasilAPI.

## Airtable

Utilizado como banco de dados no-code para persistir cada consulta realizada,
permitindo consultar e organizar os registros sem necessidade de um banco de
dados tradicional.

## Fluxo

```
CNPJ → BrasilAPI → CEP → ViaCEP → normalização → Airtable → interface
```

## Tecnologias

- Node.js + TypeScript
- Express
- Axios
- dotenv
- cors
- HTML / CSS / JavaScript puro no frontend

## Instalação

```bash
npm install
```

## Configuração

Crie um arquivo `.env` na raiz do projeto baseado no `.env.example`:

```bash
cp .env.example .env
```

Preencha o `AIRTABLE_TOKEN` com um Personal Access Token válido do Airtable
(escopos `data.records:read` e `data.records:write`, restrito à base do
projeto). **Nunca coloque o token real no README, no frontend ou em prints.**

## Execução

```bash
npm run dev
```

A aplicação estará disponível em `http://localhost:3000`.

## Segurança

- O token do Airtable é lido apenas via `process.env` no backend.
- O arquivo `.env` está listado no `.gitignore` e nunca é versionado.
- O frontend não recebe nem manipula nenhuma credencial.
- Somente o backend (`src/server.ts`) se comunica diretamente com a API do
  Airtable.

## LGPD e governança

A aplicação utiliza exclusivamente dados cadastrais empresariais de natureza
pública (CNPJ, razão social, situação cadastral e endereço), sem tratar dados
pessoais sensíveis. Apenas os campos necessários à finalidade da consulta são
armazenados no Airtable. As credenciais de acesso são protegidas por variáveis
de ambiente e não são expostas em código, prints ou repositórios. Recomenda-se
manter controle de acesso à base do Airtable e definir uma política de
retenção para os registros de consulta armazenados.
<img width="919" height="506" alt="vs" src="https://github.com/user-attachments/assets/66d76149-c5c3-4c10-8739-86071c5347f7" />
<img width="960" height="504" alt="db" src="https://github.com/user-attachments/assets/43d398b8-a5f2-4714-9cd5-d2b87c8184d1" />
<img width="960" height="504" alt="cice" src="https://github.com/user-attachments/assets/329af02b-845e-4b04-8afc-9c3244dd21a2" />
