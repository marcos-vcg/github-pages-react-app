# Deploy de App React no GitHub Pages 

\* **OBS:** *Apenas para apps criados com* `create-react-app`

&nbsp;



## Introdução
Criar uma aplicação React e fazer o deploy no GitHub para hospedar e rodar no GitHub Pages.

1. Criar o projeto React usando o [`create-react-app`](https://create-react-app.dev/). 
2. Fazer o deploy no [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages) usando o pacote do npm [`gh-pages`](https://github.com/tschaub/gh-pages).

&nbsp;



## Pré-Requisitos

* [`Node`](https://nodejs.org/en/download/), [`Git`](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

    ```shell 
    $ node --version && git --version
    ```
    > Verificar se tem o node e o git instalados

&nbsp;



## Passo a Passo - Simplificado

> \* **OBS:** *Para apps já existentes criados com* `create-react-app`

### 1. Instalar o pacote do npm [`gh-pages`](https://github.com/tschaub/gh-pages)

```shell
$ npm install gh-pages --save-dev
```

### 2. Adicionar a propriedade `homepage` no `package.json`.
    
```diff
{
    "name": "my-app",
    "version": "0.1.0",
+ "homepage": "https://marcos-vcg.github.io/nome-do-repositorio",
    "private": true,
```

### 3. Adicionar `predeploy` e `deploy` aos `scripts` no `package.json`.

```diff
"scripts": {
+   "predeploy": "npm run build",
+   "deploy": "gh-pages -d build",
    "start": "react-scripts start",
    "build": "react-scripts build",
```

### 4. Fazer o deploy do projeto no GitHub Pages

```shell
$ npm run deploy
```

### 5. Configure GitHub Pages

1. No projeto acesse `"SETTINGS"`, `"Code and Automation"`, `"PAGES"`
3. Configure o "Build and deployment"
    * Source: `Deploy from a branch`
    * Branch: `gh-pages`
    * Folder: `/ (root)`


&nbsp;



## Passo a Passo - Completo e Explicado

### 1. Criar um repositório **VAZIO** no GitHub

- [`Criar novo repositorio`](https://github.com/new).


### 2. Criar o projeto React

* Criar um app React e entrar na pasta do projeto:

    ```shell
    $ npx create-react-app my-app
    $ cd my-app
    ```


### 3. Instalar o pacote do npm `gh-pages`

* Instale o [`gh-pages`](https://github.com/tschaub/gh-pages) :
 
    ```shell
    $ npm install gh-pages --save-dev
    ```


### 4. Adicionar a propriedade `homepage` no `package.json`.

* Adicine a propriedade `homepage` com esse valor: `https://{username}.github.io/{nome-do-repositorio}`
    > Substitua `{username}` com o seu username do GitHub e `{nome-do-repositorio}` com o nome do repositório GitHub que você criou no passo 1.
    
    ```diff
    {
      "name": "my-app",
      "version": "0.1.0",
    + "homepage": "https://marcos-vcg.github.io/nome-do-repositorio",
      "private": true,
    ```



### 5. Adicionar os scripts de `predeploy` e `deploy` no `package.json`.

* Adicione as propriedades `predeploy` e `deploy` nos `scripts`:

    ```diff
    "scripts": {
    +   "predeploy": "npm run build",
    +   "deploy": "gh-pages -d build",
        "start": "react-scripts start",
        "build": "react-scripts build",
    ```


### 6. Apontar o seu repositório LOCAL para o repositório REMOTO criado no Github

* Vincule o repositório local com o "[remote](https://git-scm.com/docs/git-remote)" apontando para o repositório remoto no GitHub.
    
    ```shell
    $ git remote add origin https://github.com/{username}/{repo-name}.git
    ```
    
    > Substitua `{username}` com o seu username do GitHub e `{repo-name}` com o nome do repositório GitHub que você criou no passo 1.
    
    > Esse comando informa ao Git para onde eu quero que ele envie as alterações sempre que for usado o comando `$ git push` por mim, ou pelo npm package `gh-pages` agindo em meu nome.


### 7. Fazer o deploy do projeto em React no GitHub Pages

* Deploy no github pages:

    ```shell
    $ npm run deploy
    ```

    > Esse comando vai rodar os scripts `predeploy` e `deploy` definidos no `package.json`
    >
    > O script `predeploy` vai construir uma versão distribuível da aplicação React e guardá-la na pasta `build`. Em seguida, o script `deploy` vai fazer um novo `COMMIT and PUSH` dessa pasta `build` na branch `gh-pages` que será criada automaticamente caso ainda não exista.
    
    > Por padrão os commits da branch `gh-pages` terão a mensagem de "Updates". você pode especificar a mensagem por meio do comando `-m`, como está abaixo:
    > ```shell
    > $ npm run deploy -- -m "Deploy React app to GitHub Pages"
    > ```
    O GitHub Pages vai detectar automaticamente os commits publicados na branch `gh-pages` do repositorio. Assim que for detectado atualizaçoes nessa branch, o GitHub Pages irá publicar a nova distribuição do projeto na URL `homepage` que foi especificada no passo 4.


### 8. Configure GitHub Pages

1. Acesse o repositório do projeto e selecione a aba de `"SETTINGS"`
2. Na barra lareral na seção de `"Code and Automation"` selecione `"PAGES"`
3. Configure o "Build and deployment"
    * Source: `Deploy from a branch`
    * Branch: `gh-pages`
    * Folder: `/ (root)`
* OBS: Nao esqueça de clicar no botão `"SALVAR"` e aguarde alguns minutos.


### 9. Acesse o seu projeto publicado

* **Prontinho!** O prejeto React foi publicado no GitHub Pages! Agora é só acessar e compartilhar. 

    `https://username.github.io/nome-do-repositorio`
  
&nbsp;



# Referências

1. [ Repositório Original ](https://github.com/gitname/react-gh-pages)
2. [ Guia oficial de Deploy do `create-react-app` ](https://create-react-app.dev/docs/deployment/#github-pages)