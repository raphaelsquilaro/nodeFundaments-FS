# Node.js — Módulo File System (`fs`)

Projeto desenvolvido em **Node.js** para demonstrar o uso do módulo nativo `fs` (**File System**).

A aplicação realiza operações básicas com arquivos e diretórios, incluindo:

- Criação de uma pasta;
- Criação de um arquivo;
- Escrita de conteúdo;
- Adição de conteúdo a um arquivo;
- Leitura de um arquivo;
- Tratamento de erros.

## 📋 Sobre o projeto

O módulo `fs` faz parte da API nativa do Node.js e permite trabalhar com o sistema de arquivos do computador.

Neste projeto, o programa cria uma pasta chamada `test`, dentro dela cria o arquivo `test.txt`, adiciona conteúdo ao arquivo e, por fim, lê seu conteúdo.

O fluxo da aplicação é:

```text
Criar pasta
    ↓
Criar arquivo
    ↓
Adicionar conteúdo
    ↓
Ler arquivo
    ↓
Exibir conteúdo no terminal
```

## 📁 Estrutura do projeto

Depois da execução, a estrutura esperada será:

```text
projeto/
├── index.js
├── README.md
└── test/
    └── test.txt
```

## 🛠️ Pré-requisitos

Para executar o projeto, é necessário ter o **Node.js** instalado.

Verifique a instalação com:

```bash
node --version
```

Também é possível verificar o npm:

```bash
npm --version
```

## ▶️ Como executar

Dentro da pasta do projeto, execute:

```bash
node index.js
```

Não é necessário executar `npm install`, pois o projeto utiliza apenas módulos nativos do Node.js.

---

# 📦 Módulo `fs`

O módulo `fs` significa **File System** e fornece métodos para trabalhar com arquivos e diretórios.

A importação é feita através de:

```js
const fs = require("fs");
```

Como o projeto utiliza **CommonJS**, usamos `require()` para importar o módulo.

---

# 📦 Módulo `path`

O projeto também utiliza o módulo `path` para construir os caminhos dos arquivos e diretórios.

```js
const path = require("path");
```

Em conjunto com `__dirname`, ele permite criar caminhos de forma mais segura e compatível entre diferentes sistemas operacionais.

Exemplo:

```js
path.join(__dirname, "test", "test.txt")
```

---

# 📁 Criando uma pasta

A pasta `test` é criada utilizando:

```js
fs.mkdir(
  path.join(__dirname, "test"),
  (error) => {
    if (error) {
      return console.log("Erro: ", error);
    }

    console.log("Pasta criada com sucesso!");
  }
);
```

O método `fs.mkdir()` é utilizado para criar diretórios.

Se ocorrer algum problema, o objeto `error` será preenchido e a mensagem será exibida no terminal.

---

# 📄 Criando um arquivo

Depois que a pasta é criada, o programa cria o arquivo `test.txt` utilizando `fs.writeFile()`:

```js
fs.writeFile(
  path.join(__dirname, "test", "test.txt"),
  "hello node!",
  (error) => {
    if (error) {
      return console.log("Erro: ", error);
    }

    console.log("Arquivo criado com sucesso!");
  }
);
```

Nesse exemplo:

- `path.join()` define o caminho do arquivo;
- `"hello node!"` é o conteúdo inicial;
- `fs.writeFile()` cria o arquivo e escreve o conteúdo;
- O callback informa se ocorreu algum erro.

---

# ✏️ Adicionando conteúdo ao arquivo

Depois de criar o arquivo, o projeto adiciona mais conteúdo utilizando `fs.appendFile()`:

```js
fs.appendFile(
  path.join(__dirname, "test", "test.txt"),
  " hello world!",
  (error) => {
    if (error) {
      return console.log("Erro: ", error);
    }

    console.log("Arquivo modificado com sucesso!");
  }
);
```

O método `appendFile()` adiciona conteúdo ao final do arquivo existente.

Depois dessa operação, o conteúdo do arquivo será:

```text
hello node! hello world!
```

---

# 📖 Lendo o arquivo

Por fim, o programa utiliza `fs.readFile()` para ler o conteúdo:

```js
fs.readFile(
  path.join(__dirname, "test", "test.txt"),
  "utf8",
  (error, data) => {
    if (error) {
      return console.log("Erro: ", error);
    }

    console.log(data);
  }
);
```

O segundo argumento:

```text
utf8
```

define a codificação utilizada para interpretar o conteúdo do arquivo como texto.

A variável `data` recebe o conteúdo lido.

---

# ⚠️ Correção importante no código original

No código enviado, o caminho utilizado no `readFile()` aparece como:

```js
path.join(__dirname, "/test", "test/test.txt")
```

Isso acaba adicionando `test` duas vezes ao caminho.

O ideal é utilizar:

```js
path.join(__dirname, "test", "test.txt")
```

Assim, o caminho será:

```text
projeto/test/test.txt
```

---

# 💻 Código completo corrigido

```js
const fs = require("fs");
const path = require("path");

// Criar uma pasta
fs.mkdir(
  path.join(__dirname, "test"),
  (error) => {
    if (error) {
      return console.log("Erro: ", error);
    }

    console.log("Pasta criada com sucesso!");
  }
);

// Criar um arquivo
fs.writeFile(
  path.join(__dirname, "test", "test.txt"),
  "hello node!",
  (error) => {
    if (error) {
      return console.log("Erro: ", error);
    }

    console.log("Arquivo criado com sucesso!");

    // Adicionar conteúdo ao arquivo
    fs.appendFile(
      path.join(__dirname, "test", "test.txt"),
      " hello world!",
      (error) => {
        if (error) {
          return console.log("Erro: ", error);
        }

        console.log("Arquivo modificado com sucesso!");

        // Ler arquivo
        fs.readFile(
          path.join(__dirname, "test", "test.txt"),
          "utf8",
          (error, data) => {
            if (error) {
              return console.log("Erro: ", error);
            }

            console.log(data);
          }
        );
      }
    );
  }
);
```

> O `const { error } = require("console");` presente no código original não é necessário e pode ser removido. O `error` utilizado nos callbacks já é fornecido pelo próprio Node.js.

---

# 🖥️ Resultado esperado

Ao executar:

```bash
node index.js
```

O terminal deverá apresentar mensagens semelhantes a:

```text
Pasta criada com sucesso!
Arquivo criado com sucesso!
Arquivo modificado com sucesso!
hello node! hello world!
```

E o arquivo:

```text
test/test.txt
```

terá o conteúdo:

```text
hello node! hello world!
```

---

# 🧠 Principais métodos utilizados

| Método | Função |
|---|---|
| `fs.mkdir()` | Cria um diretório |
| `fs.writeFile()` | Cria ou sobrescreve um arquivo |
| `fs.appendFile()` | Adiciona conteúdo ao final de um arquivo |
| `fs.readFile()` | Lê o conteúdo de um arquivo |
| `path.join()` | Combina partes de um caminho |

---

# 🔄 Fluxo assíncrono

Os métodos utilizados neste projeto possuem callbacks:

```js
(error) => {
  // ...
}
```

Isso significa que as operações de arquivo são realizadas de maneira **assíncrona**.

Por exemplo:

```js
fs.writeFile(
  "arquivo.txt",
  "Olá!",
  (error) => {
    // Executado quando a operação terminar
  }
);
```

O Node.js inicia a operação e continua seu funcionamento enquanto aguarda a conclusão dela.

Esse modelo é especialmente importante em aplicações Node.js que precisam lidar com muitas operações de entrada e saída.

---

# 🎯 Objetivos de aprendizado

Com este projeto, é possível praticar:

- Node.js;
- Módulos nativos;
- `require()`;
- Módulo `fs`;
- Módulo `path`;
- `__dirname`;
- Criação de diretórios;
- Criação de arquivos;
- Escrita em arquivos;
- Leitura de arquivos;
- Callbacks;
- Tratamento de erros;
- Operações assíncronas.

---

# 🚀 Próximos passos

Depois de compreender este exemplo, alguns exercícios interessantes são:

1. Criar arquivos JSON utilizando `fs`;
2. Ler e alterar arquivos JSON;
3. Criar vários arquivos automaticamente;
4. Listar arquivos de uma pasta;
5. Excluir arquivos e diretórios;
6. Renomear arquivos;
7. Utilizar `fs.promises`;
8. Reescrever o projeto utilizando `async/await`;
9. Criar um pequeno sistema de cadastro utilizando arquivos JSON.

## 📄 Licença

Projeto desenvolvido para fins educacionais e de aprendizado de **Node.js** e manipulação do sistema de arquivos.
