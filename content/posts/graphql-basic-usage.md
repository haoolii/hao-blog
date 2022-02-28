---
title: "GraphQL 基本安裝與使用"
date: 2022-02-28T22:16:21+08:00
draft: false
summary: "筆記 GraphQL 基本安裝與使用"
tags: ["graphql", "nodejs"]
categories: ["graphql"]
---

## 概述
建構基本 `GraphQL` 專案，單純筆記初始化流程與大致使用流程。

## 安裝

初始化 `npm` 專案
```bash
npm init -y
```

安裝相依套件

- `apollo-server` Apollo 伺服器的核心
- `graphql` 用於建構 `GraphQL Schema` 和 執行 `Query`

```bash
npm install apollo-server graphql
```

```bash
touch index.js
```

## 定義 `GraphQL Schema`

定義 `Query`與 `Mutation`，驚嘆號為不為 `null`

```javascript
const typeDefs = gql`
  type Book {
    title: String
    author: String
  }

  type Query {
    books: [Book]!
  }

  input newBookInput {
      title: String!
      author: String!
  }

  type Mutation {
    newBook(input: newBookInput!): Book!
  }
`;
```

## 定義資料

此處定義假資料，一般為 `DB` 連結，或是其他連線。
```javascript
const books = [
  {
    title: "The Awakening",
    author: "Kate Chopin",
  },
  {
    title: "City of Glass",
    author: "Paul Auster",
  },
];
```

## 定義 `Resolver`

- 第一個參數是父層的 `Type`，如果是在根上的 `Query`、`Mutation`，此處會是空。
- 第二個參數會是 `Query`、`Mutation` 的參數。
- 第三個參數會是 `Context`。
- 第四個參數會是更細部的 `Query` 參數。

```javascript
const resolvers = {
    Query: {
        books: (_, __, ctx) => {
            return ctx.books;
        }
    },
    Mutation: {
        newBook(_, { input }, ctx) {
            ctx.books.push(input);
            return input;
        }
    }
}
```

## 建立 `ApolloServer` 實體

透過 `context` 可以傳遞 Model 或是 DB 連線等等..，此處也可針對 `Header` 進行身分驗證，並拋出錯誤。

```javascript
const server = new ApolloServer({
    typeDefs,
    resolvers,
    context() {
        return { books }
    }
})

server.listen(4000).then(({ url }) => {
    console.log(`Server ready at ${url}`)
})
```

## 執行

```bash
node index.js
```

## 參考
[Apollographql Docs](https://www.apollographql.com/docs/apollo-server/data/resolvers/)