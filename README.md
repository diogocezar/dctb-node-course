# Curso de NodeJS

Material baseado no curso da RocketSeat Start sobre NodeJS.

# O que é API NodeJS

## O que é o NodeJS

Permite que utilizemos JavaScript (normalmente utilizada no front-end) em uma aplicação Back-End.

É uma plataforma que utiliza a V8 (a engine que "entende" o JavaScript dentro do Google Chrome) no lado do Back-End.

Ou seja, é uma ferramenta que conseguirá tratar requisições e respostas.

Desta forma é possível conseguir acessar recursos que não são nativamente disponíveis para o Front-End. Como por exemplo, o acesso a bancos de dados.

## O que é uma API Rest?

Atualmente temos 2 tipos principais de aplicações:

1. **FULL MVC**: é quando cria-se a parte visual (HTML + CSS + JavaScript) no próprio servidor (no Back-End);
   Por exemplo: Wordpress;
   Servidor e Front-End estão unidos!
2. Com **REST API**: Separa o Front-End do Back-End; Utiliza uma forma de comunicação entre o Front-End e o Back-End;

## Quais os benefícios de uma API Rest?

- Oferece mais flexibilidade ao Front-End (Conseguimos tratar os dados de uma forma mais elaborada).
- Fica fácil fazer a portabilidade do Front-End, pois não há qualquer tipo de dependência.
- Conseguimos trabalhar ainda, com uma única API para diferentes plataformas (Web + Mobile)

# Um hello world em NodeJS

Obviamente, poderíamos criar uma API de forma nativa com a linguagem NodeJS, mas isso, seria um pouco verboso demais de controlar.

A seguir um exemplo de um servidor simples em NodeJS que faz um Hello World

```js
const http = require("http");
const port = 3000;
const ip = "localhost";

const server = http.createServer((req, res) => {
  console.log("Recebendo uma request!");
  res.end("<h1>Olá Mundo</h1>");
});

server.listen(port, ip, () => {
  console.log(`Servidor rodando em http://${ip}:${port}`);
  console.log("Para derrubar o servidor: ctrl + c");
});
```

Vamos então nos atentar a criar uma aplicação utilizando algumas dependências que irão melhorar o gerenciamento de nossa aplicação.

# Estrutura da Aplicação

Vamos então criar uma pasta para iniciar o projeto da API:

```bash
mkdir node-api
cd node-api
yarn init -y
```

Agora podemos notar que já criamos um package.json. Ele será o arquivo que deverá conter as intruções de como o nosso aplicativo deverá se comportar. Também é o responsável por guardar as dependências do nosso projeto.

Agora precisamos instalar nesse projeto o express. Este é um micro-framework irá nos ajudar principalmente com as rotas, requisições e respostas da aplicação, entre outras coisas.

Para isso:

```bash
yarn add express
```

Notemos que agora dentro do package.json nós temos uma dependência do express.

Agora podemos criar o arquivo principal da aplicação. Para isso, vamos criar um arquivo app.js dentro de /src.

```js
const express = require("express");
const app = express();
app.listen(9999);
```

Agora, já temos um servidor em NodeJS criado com express! E podemos então rodá-lo em nosso navegador:

```bash
node /src/app.js
```

Claro que neste momento, nada será exibido na tela ainda.

# Criando a Primeira Rota

Queremos agora retornar uma mensagem, quando uma rota for acessada, para isso, podemos alterar o arquivo para a seguinte estrutura:

```js
const express = require("express");
const app = express();
app.get("/", (req, res) => {
  res.send("Olá Mundo!");
});
app.listen(9999);
```

Notemos que:

- get: é o protocolo utilizado pela requisição HTTP;
- req: é o objeto que representa a requisição HTTP;
- res: é o objeto que representa a resposta HTTP;
- res.send: foi a função utilizada para retornar alguma informação.

Podemos então rodar a aplicação e abrir o navegador para verificar o resultado.

```
node src/app.js
```

E em seguida, abrir http://localhost:9999

# Conhecendo o Nodemoon

Até este momento, todas as vezes em que nós precisamos alterar alguma informação no nosso código, temos que parar o servidor que estava sendo executado, e startá-lo novamente. O que pode se tornar bem inconveninente ao longo do desenvolvimento.

Por isso, podemos adicionar uma nova dependência que irá cuidar disso automaticamente em nosso ambiente de desenvolvimento. Depois de instalado e configurado, o Nodemon conseguirá ficar observando nossos arquivos, e sempre que houver alguma modificação reiniciará o serviço de forma automática.

Para instalá-lo:

```bash
yarn add -D nodemon
```

Agora, podemos notar que dentro do package.json temos uma nova devDependencies, que representam dependências que serão utilizadas apenas enquanto estivermos desenvolvendo a aplicação. Ou seja, quando esta aplicação for ser colocada em produção, essas dependências serão ignoradas.

Agora vamos criar um script dentro do package.json que irá permitir a utilização de um comando que irá ativar o nodemon, para isso, vamos alterar o package.json:

```json
    ...
    "script":
        "dev" : "nodemon src/app.js"
    ...
```

Agora podemos iniciar o nosso servidor da aplicação com o comando

```bash
yarn start dev
```

Note que, ao alterar o arquivo, o servidor é reiniciado automaticamente.

# MongoDB

O mongodb é um banco não relacional, que se comporta muito bem com NodeJS.

Neste caso, será a escolha para a demonstração deste pequeno minicurso, mas é importante lembrar que o NodeJS pode se comunicar com a maioria dos bancos de dados relacionais já existentes no mercado.

Para continuar com o tutorial é importante que você instalar o MongoDB em seu sistema operacional, e que entenda como ele funciona.

Alguns tutoriais podem ajudar:

https://medium.com/@NetoVieiraLeo/instalando-e-configurando-o-mongodb-no-windows-b1d4e1e58911
https://www.digitalocean.com/community/tutorials/como-instalar-o-mongodb-no-ubuntu-16-04-pt

Além disso, também é bem bacana tentar utilizá-lo com Docker.

Mais alguns links interessantes:

https://medium.com/dockerbr/mongodb-no-docker-dd3b72c7efb7

Ou ainda utilizar algum serviço online que possibilite a criação remota de uma banco de dados MongoDB

https://www.mongodb.com/cloud/atlas
https://mlab.com/
https://codeforgeek.com/mongodb-atlas-node-js/
https://medium.com/baixada-nerd/criando-um-crud-completo-com-nodejs-express-e-mongodb-parte-3-3-b243d14a403c

## Dica

Uma dica importante para utilizar o MongoDB é que possivelmente você vai entender que ele precisa de um comando para ser inicializado.

Neste comando nós vamos fazer com que se "suba" um serviço que arazenará todos os dados do banco em uma determinada pasta.

Para isso, com o seu ambinete instalado, basta executar o seguinte comando

```bash
mongod –dbpath=/home/user
```

Neste caso, o servidor ficará "montado" na pasta `/home/user`

Uma ferramenta bem interessante para "visualizar" os dados do banco MongoDB é o Compass.

Com uma instância do MongoDB iniciada, basta abrir o programa e vizualisar as tabelas criadas.

https://docs.mongodb.com/compass/master/install/

A partir da próxima sessão, vamos assumir que de alguma forma, você possui o acesso à um banco em MongoDB.

# Conectando com o Banco de Dados

Para nos ajudar no processo de gerenciamento do banco de dados, vamos instalar o Mongoose

```bash
yarn add mongoose
```

O Mongose pode ser considerado um ORM (Object Relational Mapping) para o MongoDB, basicamente vamos conseguir "representar" os dados armazenados em objetos dentro da nossa aplicação. Também encapusla a lógica das operações do banco de dados. Ou seja, faremos os CRUDS com comandos e não com alguma sintaxe própria, como o SQL.

E agora podemos modificar um pouco o nosso arquivo para que ele se conecte ao MongoDB:

```js
const express = require("express");
const mongoose = require("mongoose");
const app = express();
mongoose.connect("mongodb://localhost:27017/node-api", {
  useNewUrlParser: true
});
app.get("/", (req, res) => {
  res.send("Olá Mundo!");
});
app.listen(9999);
```

Um detalhe importante é que a string de conexão pode se alterar dependendo de como será a utlilização do MongoDB.

E para testar se a conexão foi feita com sucesso, basta executar o comando para subir a aplicação, e se nenhum erro foi apontado, então, tudo estará ok!

```bash
yarn start dev
```

# Criando o Primeiro Model

Agora, vamos criar o nosso primeiro model, que dentro do modelo MVC representa uma entidade do banco de dados.

Neste minicurso, vamos trabalhar com um model de produto.

Então agora, dentro da pasta src, vamos criar uma outra pasta para organizar nossos models. E um model específico para o produto.

**/src/models/Product.js**

Agora, dentro deste Model, prcisaremos definir um Schema. Que são os campos que um produto vai ter e que tipos de dados eles vão salvar.

O arquivo de model ficaria basicamente:

```js
const mongoose = require("mongoose");
const ProductSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  url: {
    type: String,
    required: true
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

mongoose.model("Product", ProductSchema);
```

Notemos que criamos um objeto com os tipos de cada um dos campos, neste caso: Título, Descrição e URL, e ainda um campo de controle createdAt que irá se preencher automaticamente com a data de criação do elemento.

Ainda temos a utlização do `mongoose.model` que faz o "registro" deste model Product para toda a nossa aplicação.

Agora para testar nosso model, podemos modificar temporariamente nosso arquivo principal, ficando:

```js
const express = require("express");
const mongoose = require("mongoose");
const app = express();
mongoose.connect("mongodb://localhost:27017/node-api", {
  useNewUrlParser: true
});

require("./src/models/Product");
const Product = mongoose.model("Product");

app.get("/", (req, res) => {
  Product.create({
    title: "ReactJS",
    description: "Just a sample",
    url: "http://www.google.com"
  });
  return res.send("Olá Mundo!");
});
app.listen(9999);
```

Notemos que agora estamos importando o nosso model, e criando uma variável que "representa" este model no banco de dados.

Apenas para efeito de testes, sempre que houver uma requisição em "/" criaremos um novo produto fake.

Nenhuma modificação será mostrada em tela, mas ao acessar os registros do banco de dados, podemos ver que um novo produto foi criado, para cada requisição realizada.

# Reestruturação dos Arquivos e Fazendo CRUDS
