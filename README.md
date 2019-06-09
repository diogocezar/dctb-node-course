# Curso de NodeJS

Material baseado no curso da RocketSeat sobre NodeJS.

https://rocketseat.com.br/starter

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
yarn run dev
```

Note que, ao alterar o arquivo, o servidor é reiniciado automaticamente.

# MongoDB

O mongodb é um banco não relacional, que se comporta muito bem com NodeJS.

Neste caso, será a escolha para a demonstração deste pequeno minicurso, mas é importante lembrar que o NodeJS pode se comunicar com a maioria dos bancos de dados relacionais já existentes no mercado.

Para continuar com o tutorial é importante que você instalar o MongoDB em seu sistema operacional, e que entenda como ele funciona.

Alguns tutoriais podem ajudar:

- https://medium.com/@NetoVieiraLeo/instalando-e-configurando-o-mongodb-no-windows-b1d4e1e58911
- https://www.digitalocean.com/community/tutorials/como-instalar-o-mongodb-no-ubuntu-16-04-pt

Além disso, também é bem bacana tentar utilizá-lo com Docker.

Mais alguns links interessantes:

- https://medium.com/dockerbr/mongodb-no-docker-dd3b72c7efb7

Ou ainda utilizar algum serviço **online** que possibilite a criação remota de uma banco de dados MongoDB

- https://www.mongodb.com/cloud/atlas
- https://mlab.com/
- https://codeforgeek.com/mongodb-atlas-node-js/
- https://medium.com/baixada-nerd/criando-um-crud-completo-com-nodejs-express-e-mongodb-parte-3-3-b243d14a403c

## Dica

Uma dica importante para utilizar o MongoDB é que possivelmente você vai entender que ele precisa de um comando para ser inicializado.

Neste comando nós vamos fazer com que se "suba" um serviço que arazenará todos os dados do banco em uma determinada pasta.

Para isso, com o seu ambinete instalado, basta executar o seguinte comando

```bash
mongod –dbpath=/home/user
```

Neste caso, o servidor ficará "montado" na pasta `/home/user`

**IMPORTANTE**: Note que essa foi uma pasta utilizada como exemplo, mas você deverá montar o banco de dados em uma pasta que escolher em seu sistema operacional. Também é importante entender que o MongoDB não tem nenhuma relação direta com o seu projeto da API, e pode ser montado em um pasta completamente diferente. E por fim, este comando deverá ficar "rodando" enquanto quiser que o banco fique "online" caso você pare este serviço, com `CTRL + C` por exemplo, é como se estivesse desligando o banco de dados.

Mas e agora? O banco está online... como vou fazer para ver as nossas coleções?

Uma ferramenta bem interessante para "visualizar" os dados do banco MongoDB é o **Compass**.

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

module.exports = mongoose.model("Product", ProductSchema);
```

Notemos que criamos um objeto com os tipos de cada um dos campos, neste caso: Título, Descrição e URL, e ainda um campo de controle createdAt que irá se preencher automaticamente com a data de criação do elemento.

Ainda temos a utlização e exportação do `mongoose.model` que faz o "registro" deste model Product para toda a nossa aplicação.

Agora para testar nosso model, podemos modificar temporariamente nosso arquivo principal, ficando:

```js
const express = require("express");
const mongoose = require("mongoose");
const app = express();
mongoose.connect("mongodb://localhost:27017/node-api", {
  useNewUrlParser: true
});

const Product = require("./models/Product");

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

Até este momento criamos todo o nosso servidor web em um único arquivo.

E isso, nem de longe é recomendado. Inicialmente até faz sentido para entendermos mais facilmente o funcionamento dos comandos.

Mas agora vamos precisar estruturar um pouco melhor o nosso projeto.

Para isso, vamos organizar as rotas da aplicação, e também toda a parte de CRUD dos nossos produtos, utilizando uma nova camada de Controllers.

Então vamos criar um novo arquivo em _/src/routes.js_ que será o arquivo responsável por definir as nossas rotas.

```js
const express = require("express");
const routes = express.Router();

routes.get("/", (req, res) => {
  return res.send("Hello World");
});

module.exports = routes;
```

Note que utlizamos um novo objeto `routes` que é obtido a partir de `express.Router` utilizado para organizar as rotas da nossa aplicação.

Agora temos aqui a mesma estrutura que já estávamos utilizando, neste exemplo simples a rota "/" vai apenas retornar um "Hello World".

E finalmente, temos a exportação deste módulo para que ele possa ser importado em outro arquivo.

Então no nosso arquivo principal app.js, podemos fazer:

```js
const express = require("express");
const mongoose = require("mongoose");
const app = express();
mongoose.connect("mongodb://localhost:27017/node-api", {
  useNewUrlParser: true
});
app.use("/api", require("./src/routes"));
app.listen(9999);
```

Note que estamos agora utilizando `app.use()` para gerenciar as rotas. Esse é um comando "coringa" que vai conseguir interceptar todos os tipos de requests (POST, DELETE, GET, etc...).

Note que agora fazer o seguinte:

`app.use("/api", require("./src/routes"));`

Neste pontos estamos dizendo: todas as rotas que chegarem em nosso serivdor que começarem com `/api` devem apontar para o arquivo de rotas.

Antes nós poderíamos acessar, por exemplo, http://localhost:9999/produtos mas agora, precisaremos acessar: http://localhost:9999/api/produtos.

Mas se fossemos trabalhar com a nossa estrutura desta forma, ainda ficaríamos com algo muito verboso, imagine tratar toda a lógica dentro do próprio arquivo de rotas.

Então o que vamos fazer é transferir essas responsabilidades para os nossos _Controllers_.

Para isso, podemos criar em _/src/controllers/_ um novo Controller para Produto, chamado _ProductController.js_.

```js
const mongoose = require("mongoose");
const Product = require("../models/Product");

class ProductController {
  async index(req, res) {
    const products = await Product.find();
    return res.json(products);
  }
}

module.exports = new ProductController();
```

Note que criamos uma classe para gerenciar os Produtos, e nela um método async (que permite a utilização de promises).

No método index, nós esperamos 2 parâmetos, os já conhecidos, req e res. Então fazemos uma consulta em todos os dados do banco através do método `find` e retornamos um json com os dados obtidos.

Agora, podemos voltar em nossas rotas e fazer a seguinte alteração:

```js
const express = require("express");
const routes = express.Router();
const ProductController = require("./controllers/ProductController");

routes.get("/products", ProductController.index);

module.exports = routes;
```

# Utilizando o Insomnia

Vamos utilizar um software específico que vai nos ajudar bastante a trabalhar com a nossa API.

Neste caso, vamos utilizar o Insomina:

https://insomnia.rest/

O processo de instalação é bem simples e intuitivo.

Por que utilizá-lo? Testar uma api nem sempre é algo muito simples de se fazer, imagine que vc precisaria criar um "Front-End" só para realizar estes testes. Por isso, o que o Insomia faz, é justamente proporcional um ambiente para "testar" as apis, permitindo que nós enviemos diferentes tipos de requisições para api, como por exemplo: GET (para obter um dado), POST (para salvar), PUT (para atualizar) e DELETE (para excluir).

Além disso, fica simples o envio de um JSON para criar ou alterar um recurso.

Agora podemos testar aquela nossa rota já criada, para ver se os dados são carregados com sucesso dentro do programa.

Para isso, cria-se um New Request, com o nome index e do tipo get.

Agora basta alterar a URL da rota, e enviar.

Note que o JSON é retornado.

# Criando um Registro

Agora precisamos criar um novo método para criar um novo registro em nosso banco de dados.

Para isso vamos alterar o ProductController para:

```js
const mongoose = require("mongoose");
const Product = require("../models/Product");

class ProductController {
  async index(req, res) {
    const products = await Product.find();
    return res.json(products);
  }
  async store(req, res) {
    const product = await Product.create(req.body);
    return res.json(product);
  }
}

module.exports = new ProductController();
```

E em nossas rotas, adicionamos a nova rota para criação que aponta para o método do Controller:

```js
const express = require("express");
const routes = express.Router();
const ProductController = require("./controllers/ProductController");

routes.get("/products", ProductController.index);
routes.post("/products", ProductController.store);

module.exports = routes;
```

Note que usamos o método POST para CRIAR um novo recurso no servidor.

Precisamos agora, realizar um ajuste no nosso arquivo principal app.js. Este ajuste irá permite que nós recebamos entradas JSON para os nossos endpoints, então para isso, vamos incluir `app.use(express.json())` logo após a criação do app, ficando:

```js
const express = require("express");
const mongoose = require("mongoose");
const app = express();
app.use(express.json());
mongoose.connect("mongodb://localhost:27017/node-api", {
  useNewUrlParser: true
});
app.use("/api", require("./src/routes"));
app.listen(9999);
```

E então, podemos utilizar o Insomina para criar o teste de um novo endpoint, desta vez do tipo POST.

Mas também vamos utilizá-lo para "enviar" um JSON para o recurso criado, para isso, alteramos a aba Body para JSON, e escrevemos o JSON de entrada:

```json
  "title" : "ReactJS",
  "description": "Biblioteca para criar aplicações interativas com JS",
  "url" : "http://github.com/facebook/react"
```

Agora podemos tentar o envio e conferir com o Compass, se o produto foi criado com sucesso!

# Outras Operações do CRUD

Já criamos a listagem e criação, mas ainda faltam os detalhes de um único produto, a parte de atualização e a parte de exclusão de um produto.

Então vamos criar os outros métodos:

```js
const mongoose = require("mongoose");
const Product = require("../models/Product");

class ProductController {
  async index(req, res) {
    const products = await Product.find();
    return res.json(products);
  }
  async store(req, res) {
    const product = await Product.create(req.body);
    return res.json(product);
  }
  async show(req, res) {
    const produtct = await Product.findById(req.params.id);
    return res.json(product);
  }
  async update(req, res) {
    const product = await Product.findByIdAndUpdate(req.params.id, req.body, {
      new: true
    });
    return res.json(product);
  }
  async destroy(req, res) {
    await Product.findByIdAndRemove(req.params.id);
    return res.send({ deleted: true });
  }
}

module.exports = new ProductController();
```

Notemos que o método de show procura por um produto com id específico e o retorna para o response. Usamos aqui o `req.params.id` que será recuperado da próprioa URL enviada na rota (vista logo a seguir).

O método update, utiliza um método bem interessante do Mongoose, que permite procurar, atualizar e o parametro `{new: true}` também retorna para uma variável o resultado atualizado.

As rotas ficam:

```js
const express = require("express");
const routes = express.Router();
const ProductController = require("./controllers/ProductController");

routes.get("/products", ProductController.index);
routes.post("/products", ProductController.store);
routes.get("/products/:id", ProductController.show);
routes.put("/products/:id", ProductController.update);
routes.delete("/products/:id", ProductController.destroy);

module.exports = routes;
```

# Adicionando CORS

Para fechar a API, temos que permitir que outros endereços tenham o acesso a nossa api. Até o momento, estamos permitindo apenas que o localhost faça o acesso a esta api, mas se ela for para produção, por exemplo, então precisaremos permitir que outras aplicações acessem de outros servidores.

Para isso, precisamos intalar uma dependência chamada cors:

```bash
yarn add cors
```

Agora, em nosso aplicativo principal app.js, alteramos da seguinte forma:

```js
const express = require("express");
const mongoose = require("mongoose");
const app = express();
app.use(express.json());
app.use(cors());
mongoose.connect("mongodb://localhost:27017/node-api", {
  useNewUrlParser: true
});
app.use("/api", require("./src/routes"));
app.listen(9999);
```

É isso, agora nossa api já consegue responder a qualquer domínio fora do domínio em que estiver rodando.

# Conclusão

Caso você queira ver um exemplo completo, temos isso organizado neste repositório: https://github.com/diogocezar/node-course-sample

---

Espero que todos possam ter aproveitado este minicurso de Node, e que possam ter aprendido o básico de como trabalhar de forma PRÁTICA e objetiva com NodeJS e MongoDB.

Qualquer dúvida, é só chamar pelo diogo@diogocezar.com

Boa paz! 🙏🙏🙏
