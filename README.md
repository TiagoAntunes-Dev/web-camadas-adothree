# ADO 3 - Stack Completa no Ar

## Projeto

Este README documenta minha aplicação web em produção. A stack é formada por front-end Angular, API Node.js/Express, banco MongoDB Atlas e deploy conectado ao GitHub.

### Links do Projeto

- **Front-end:** https://TiagoAntunes-Dev.github.io/crud-products-frontend/
- **API:** https://crud-api-products.onrender.com/
- **Repositório Front-end:** https://github.com/TiagoAntunes-Dev/crud-products-frontend
- **Repositório Back-end:** https://github.com/TiagoAntunes-Dev/crud-api-products
- **Banco de Dados:** MongoDB Atlas (`Cluster0`)

---

## 1. Diagrama da Stack em Produção

![Diagrama da Stack](./assets/diagrama-stack.png)

No meu projeto, o usuário acessa o front-end Angular pelo navegador. O Angular faz requisições HTTP para a API hospedada no Render usando JSON. A API recebe essas requisições, valida os dados, executa as regras de negócio e consulta o MongoDB Atlas.

O banco retorna os documentos para a API, e a API devolve a resposta em JSON para o front-end.

O GitHub entra como repositório central do código. O front-end e o back-end ficam separados, e cada plataforma de hospedagem acompanha seu respectivo repositório para publicar novas versões quando acontece um `git push`.

---

## 2. Front-end Consumindo a API em Produção

O front-end foi desenvolvido com Angular e Angular Material. Ele está hospedado no GitHub Pages.

A URL pública da API está configurada no arquivo:

```ts
src/environments/environment.ts
```

```ts
export const environment = {
  production: false,
  apiUrl: 'https://crud-api-products.onrender.com/api'
};
```

Isso faz com que o front-end não use `localhost`, mas sim a API publicada no Render.

### Print do Front-end em Produção

> Inserir imagem do front-end funcionando em produção.

### Print do Network no DevTools

> Inserir captura da aba Network mostrando as requisições para a API.

No DevTools, aparece a requisição para a API pública. A resposta vem em JSON e retorna status de sucesso, mostrando que o front-end e o back-end estão se comunicando corretamente em produção.

---

## 3. Back-end e Banco em Produção

A API foi desenvolvida com Node.js, Express e MongoDB/Mongoose. Ela está hospedada no Render.

### Rotas da API

#### Autenticação

```http
POST /api/auth/register
POST /api/auth/login
```

#### Produtos

```http
GET    /api/products
POST   /api/products
PUT    /api/products/:id
DELETE /api/products/:id
```

#### Categorias

```http
GET    /api/categories
POST   /api/categories
DELETE /api/categories/:id
```

O banco utilizado é o MongoDB Atlas. A API se conecta ao banco usando uma variável de ambiente, sem expor a string de conexão diretamente no código.

### Print do MongoDB Atlas

> Inserir captura do cluster e das collections.

### Print da API no Render
<br><br>
<p align="center>
<img width="733" height="311" alt="Screenshot 2026-06-02 180404" src="https://github.com/user-attachments/assets/652c6d80-834d-46b7-a7e8-eb7e6ea8c5aa" />
</p>

---

## 4. Como o GitHub Conecta Tudo

Eu mantive front-end e back-end em repositórios separados porque eles possuem responsabilidades diferentes.

- O **front-end** cuida da interface acessada pelo usuário.
- O **back-end** cuida das rotas, autenticação, regras de negócio e conexão com o banco de dados.

Essa separação facilita o deploy, pois cada parte pode ser publicada na plataforma mais adequada.

- Front-end → GitHub Pages
- Back-end → Render

Quando faço um `git push`, a plataforma de hospedagem detecta a nova versão do repositório.

### Fluxo de Publicação

```text
Desenvolvedor
      │
      ▼
   GitHub
      │
 ┌────┴────┐
 ▼         ▼
Render   GitHub Pages
(API)    (Front-end)
```

No caso do Render, um novo deploy da API é iniciado automaticamente.

No GitHub Pages, os arquivos estáticos gerados pelo build do Angular são publicados.

---

## 5. O que é CI/CD

### CI (Continuous Integration)

CI significa **Integração Contínua**.

A ideia é integrar alterações frequentemente e executar validações automáticas para evitar que mudanças quebrem o projeto.

Em equipes de desenvolvimento, isso permite que vários desenvolvedores trabalhem simultaneamente com mais segurança.

### CD (Continuous Delivery / Continuous Deployment)

CD pode significar:

- **Continuous Delivery (Entrega Contínua)**
- **Continuous Deployment (Implantação Contínua)**

Na Entrega Contínua, o sistema prepara automaticamente uma nova versão para publicação.

Na Implantação Contínua, a nova versão pode ser enviada diretamente para produção após a aprovação dos testes.

### Aplicação no Projeto

Durante as ADOs, várias etapas foram realizadas manualmente:

- Configuração do MongoDB Atlas
- Publicação da API
- Ajuste da URL do front-end
- Publicação do Angular no GitHub Pages

Uma pipeline de CI/CD poderia automatizar essas tarefas executando:

1. Testes automatizados
2. Build do projeto
3. Deploy da API
4. Deploy do front-end

### Exemplo de Problema Sem CI/CD

Imagine uma equipe com cinco desenvolvedores.

Se alguém alterar uma rota da API sem perceber o impacto no front-end, a aplicação pode parar de funcionar.

Com CI/CD, os testes e o processo de build identificariam o problema antes da publicação em produção.

---

## 6. Evidências

As seguintes evidências acompanham o projeto:

- Diagrama da stack
- Front-end em produção
- Requisição no DevTools (Network)
- API hospedada no Render
- Banco MongoDB Atlas
- Painel de deploy
- Repositórios no GitHub

---

## Conclusão

Com essa stack, a aplicação funciona de forma completa em produção.

O fluxo acontece da seguinte maneira:

1. O usuário acessa o front-end.
2. O front-end envia requisições para a API.
3. A API processa os dados e consulta o MongoDB Atlas.
4. O banco retorna as informações.
5. A API devolve a resposta em JSON para o front-end.
6. O GitHub integra o código aos serviços de hospedagem, permitindo atualizações contínuas.

Essa arquitetura demonstra uma aplicação full stack funcionando em ambiente de produção, utilizando tecnologias modernas e boas práticas de separação de responsabilidades.
