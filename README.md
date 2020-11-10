# V4H Client API

[![npm version](https://img.shields.io/npm/v/v4h-client-api)](https://www.npmjs.com/package/v4h-client-api)
[![NPM](https://img.shields.io/npm/l/v4h-client-api)](https://www.npmjs.com/package/v4h-client-api)
[![npm](https://img.shields.io/npm/dm/v4h-client-api)](https://www.npmjs.com/package/v4h-client-api)
[![npm bundle size](https://img.shields.io/bundlephobia/min/v4h-client-api)](https://www.npmjs.com/package/v4h-client-api)

Biblioteca para o serviço de vídeoconferência segura para saúde (V4H - Video for Health), essa aplicação permite colocar em um sistema web já existente vídeo chamadas além de um controle de acesso complexo, onde você é possível delimitar ações dos usuários dependendo do seu papel. Para mais informações clique [aqui](https.v4h.cloud).

## Sumário

  - [Features](#features)
  - [Instalação](#instalação)
  - [Example](#example)
  - [Client API](#client-api)
    - [Organicação](#organização)
    - [Sessões](#Sessões)

## Features

- Controle de organizações e unidades organizacionais
- Controle de usuários
- Funcionalidades dentro da conferências configuráveis
- Customização de interface configurável
- Gravação da vídeo conferência do client-side e server-side
- Storage de vídeos gravados
- Criação de um manifesto de todas as ações ocorridas dentro da conferência
- Manifesto salvo em blockchain
- Integração com serviços de blockchain privadas
- Envio de arquivos referentes a uma videoconferência

## Instalação

Usando npm:

```bash
$ npm install v4h-client-api
```

Usando yarn:

```bash
$ yarn add v4h-client-api
```

Usando jsDelivr CDN:

```html
<script src="https://cdn.jsdelivr.net/gh/leossoaress/v4h-client-api@0.0.1/V4HApi.min.js"></script>
```

## Client API

A client API deve ser definida da seguinte forma para ser utilizada:

```javascript
const v4h = new V4HApi();
v4h.setup(options);
```

Options:
- login: [opcional] string de identificação para login no sistema
- password: [opcional] senha para login no sistema

Após o setup você estará disponível para accessar as classes que serão descritas abaixo.

### Organização

Sessões de conferência são criadas por usuários de uma organização. Esta entidade é a base que permite especialização futura para pessoa física ou pessoa jurídica. 

#### ``create(data)``

Método responsável por criar uma organização

```javascript
const v4h = new V4HApi();
v4h.setup({ login: 'usuario', senha: 'senha' });

const data = {
  shortname: "organização",
  planId: 1,
  fullname: "organizacao LTDA",
  alias: "organizacao de teste",
  admin: 1,
  type: "J",
  reg: "12345678912"
};

cosnt org = v4h.org.create(data).then((response) => {
  console.log(org);
});
```

data: 
- shortname: Nome curto – usado para ocasiões com pouco espaço
- planId: O plano ao qual a organização está vinculada
- fullName: Nome completo ou razão social
- alias: [opcional] Nome de fantasia
- admin: id do usuário administrador da organização
- type: Pessoa física ou jurídica
- reg: Identificador do registro (CNPJ ou CPF)
- logo: [opcional] URL externa para logo

Retorno: 

```javascript
{
  id: 1
}
```

#### ``getAll()``

Método responsável por recuperar todas as organizações criadas

```javascript
const v4h = new V4HApi();
v4h.setup({ login: 'usuario', senha: 'senha' });

v4h.org.getAll().then((org) => {
  console.log(org);
});
```

Retorno:

```javascript
[{
  id: 1,
  shortname: "organização",
  planId: 1,
  fullname: "organizacao LTDA",
  alias: "organizacao de teste",
  admin: 1,
  type: "J",
  reg: "12345678912",
  logo: null
}]
```

#### ``get(orgId)``

Método responsável por recuperar informações de uma única organiação pela identificador único da organização.

```javascript
const v4h = new V4HApi();
v4h.setup({ login: 'usuario', senha: 'senha' });

const orgId = 1;

v4h.org.get(orgId).then((org) => {
  console.log(org);
});
```

Retorno:

```javascript
{
  id: 1,
  shortname: "organização",
  planId: 1,
  fullname: "organizacao LTDA",
  alias: "organizacao de teste",
  admin: 1,
  type: "J",
  reg: "12345678912",
  logo: null
}
```

#### ``update(orgId, data)``

Método responsável por atualizar informações de uma organiação pelo identificador único da organização.

```javascript
const v4h = new V4HApi();
v4h.setup({ login: 'usuario', senha: 'senha' });

const orgId = 1;

const data = {
  alias: "organizacao de teste",
};

v4h.org.update(orgId, data).then((response) => {
  console.log(response);
});
```

data: 
- shortname: [opcional] Nome curto – usado para ocasiões com pouco espaço
- planId: [opcional] O plano ao qual a organização está vinculada
- fullName: [opcional] Nome completo ou razão social
- alias: [opcional] Nome de fantasia
- admin: [opcional] id do usuário administrador da organização
- type: [opcional] Pessoa física ou jurídica
- reg: [opcional] Identificador do registro (CNPJ ou CPF)
- logo: [opcional] URL externa para logo

Retorno: 

```javascript
true or false
```

#### ``delete(orgId)``

Método responsável por deletar uma organização.

```javascript
const v4h = new V4HApi();
v4h.setup({ login: 'usuario', senha: 'senha' });

const orgId = 1;

v4h.org.delete(orgId).then((response) => {
  console.log(response);
});
```

Retorno: 

```javascript
true or false
```

#### ``getAllSessions(orgId)``

Método responsável por recuperar todas as sessões de uma organização

```javascript
const v4h = new V4HApi();
v4h.setup({ login: 'usuario', senha: 'senha' });

v4h.org.getAllSessions().then((sessions) => {
  console.log(sessions);
});
```

retorno: 

```javascript
[{
  id: 1,
  orgId: 1,
  ouId: 1,
  profileId: 1,
  skinId: 1,
  finished: null,
  firstJoin: null,
  started: null,
  status: "READY"
}]
```
