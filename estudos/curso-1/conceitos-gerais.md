# Angular

- É um framework Web, Mobile e Desktop 
- Usado para desenvolver aplicações client-side web, mobile ou desktop de single page application.
- Usa a linguagem TypeScript no lugar de JavaScript.
- Baseado em Webcomponentes
- Orientado a objetos
- Site Oficial: [https://angular.io/](https://angular.io/)
- Documentação: [https://angular.io/docs](https://angular.io/docs)

## Versões do Angular

- Angular 2 (2015)
- Incompatível com AngularJS (versão 1.x)
- Inicia na versão 2 para não confundir com o AngularJS
- Angular 4 (2016)
- Compatível com a versão ^2 (^ == todos minor e patch)
- Google adotou o Semantic Versioning
- Angular 5 (2017)
- Mudanças importantes
- Angular 6 e 7 (2018)
- Angular 8 e 9 (2019)
- Angular 10 e 11 (2020)
- Versões novas a cada 6 meses
- Cada versão é compatível com a sua versão anterior
- A migração de uma versão 4 para uma 5 não gera break changes, porém migrar de uma versão 4 para uma 6 pode gerar break changes

## Versionamento (a partir da versão 4)

- Semantic Versioning (versionamento semântico) - [https://semver.org/](https://semver.org/)
- Versões são baseadas em 3 números, ex.: 3.2.1   
- Númeração: (Major).(Minor).(Patch)
- Major: mudanças grandes e nome principal da versão, causa break change
- Minor: novas features, não causa break change
- Patch: bugfixes, não causa break change
- Google lança uma versão 
- Major a cada 6 meses    
- Minor de 1 a 3 meses
- Toda semana
- Previews (para testes)
- Beta: ex: 10.0.0-beta
- Release Candidate: ex: 10.1.0-rc

## Aplicação Server-side

- Client faz um request (requisição) inicial
- Server processa o request e retorna um html completo (com js e css)
- Client exibe a informação no browser
- Maior tráfego na rede, recarrega a página

## Aplicação SPA (Single Page Application)

- Requisição inicial
- Client faz um request (requisição) inicial
- Server retorna o html (só na primeira vez)
- Requisições seguintes (usando post, por exemplo)
- Se Client realiza um post (ajax por exemplo)
- Server retorna um JSON (é leve, não precisa formar o HTML novamente)
- A aplicação se torna mais rápida nas próximas requisições
- A idéia é conter apenas uma página    
- Aplicação onde navegamos e interagimos com a tela sem a página ser recarregada. Ex.: Gmail

## Anatomia de um App Angular

- Uma aplicação pode ser dividida em um módulo para cada feature
- Um módulo é composto por uma coleção de componentes e por serviços
- Um componente pode consumir uma API Rest de através de serviços
- Um serviço é uma classe no Angular responsável por trabalhar com o mundo externo

## Linguagens Suportadas

- Javascript 
- Compatível com a versão ES 5 (roda em todos browser)
- Compatível com a versão ES 6 (2015, talvez precise transpilar o código para ser compatível com o ES 5 para browsers mais antigos)
- Typescript
- É a favorita para utilizar com o Angular
- Desenvolvida pela Microsoft, pelo pai do C# e do .NET
- Open Source
- É um superset do Javascript
- É fortemente Tipado
- Utiliza Orientação a Objetos
- Tem um ferramental rico na IDE VScode
- Precisa ser transpilado: arquivo.ts vira um .js
- Dart
- Não é JS
- É uma linguagem do Google

## Setup (Requisitos necessários)

- nodeJS
- npm
- Angular CLI

## Instalar o nodeJs

- Acessar o site: <https://nodejs.org>
- Instalar a última versão LTS (caminho mais seguro)
- Descobrir a versão do node

~~~bash
node --version # ou node -v
~~~

## Instalar ou atualizar o npm (Node Package Manager)

- Acessar o site: <https://npmjs.com>
- Descobrir a versão instalada

~~~bash
npm --version
~~~

## Atualizar para a mais nova versão

~~~bash
npm install npm@latest -g # -g == global
~~~

## Instalar o Angular CLI (Command Line Interface)

~~~bash
npm install -g @angular/cli
~~~

## Anatomia de um app angular

- node_modules
- pacotes necessários para rodar a aplicação
- Cada pasta é um pacote
- As vezes é necessário apagar o conteúdo para resolver problemas
- src
- código fonte da aplicação
- src/app
- componentes da aplicação
- src/assets
- arquivos complementares: css, imagens
- src/environments
- gerenciamento dos ambientes da aplicação: desenvolvimento, produção
- src/index.html
- página da SPA
- Aplicação fica no <app-root></app-root>
    - É o componente principal do Angular
    - Renderiza a aplicação
- src/main.ts
- Arquivo principal da aplicação
- Define qual será o módulo principal (classe de módulo)
- src/style.css
- Estilos globais
- src/app/app.module.ts
- Módulo Principal ou classe de módulo
- Carrega todas as referências
- src/app/app.components.ts
- Componente
- Possui uma url de template html (que será exibida dentro do index.html) e um css próprio
- src/app/app-routing.module.ts
- Arquivo de roteamento para o módulo    
- .editorconfig
- configurações do editor (ex.: Visual Studio Code)
- angular.json
- arquivo de configuração da aplicação
- package.json
- define o nome da aplicação, dependências utilizadas
- referência dos pacotes json instalados
- package-lock.json
- "manter a versão com lock"
- tsconfig.app.json, tsconfig.json, tsconfig.spec.json
- configurações sobre o typescript
- environments/environments.prod.ts
- arquivo para ambiente de produção
- environments/environments.ts
- arquivo para ambiente de desenvolvimento

## Algumas extensões

- Angular Console
- forma visual para comandos
- Angular Snippets
- Augury (plugin para navegador)
- mostra módulos da aplicação no inspect do navegador
- Better Comments
- Debugger for Chrome
- GitLens 
- npm for VS Code
- npm intellisense

## API List

- [API List: https://angular.io/api](https://angular.io/api)
- Decorator
- Diz o que a classe é.
- A classe pode ser um componente, uma diretiva, um módulo, um serviço injetável, um pipe

## Atualizar a versão do angular

#### Instalar o pacote npm-check-updates 

~~~bash
npm install -g npm-check-updates # -g para global
~~~

#### Checar se há atualizações

~~~bash
ncu # npm check updates
~~~

- Cor Verde: atualizações de patch
- Cor Azul: atualizações minor
- Cor Vermelha: atualizações major, pode gerar break change

#### Atualizar tudo

~~~bash
ncu -u # upgrade
~~~

## Realizar o debug da aplicação

- Extensão para VsCode: Debugger for Chrome

## Compilação e entrega da aplicação

- Após a compilação os arquivos para subir para o servidor estarão na pasta dist. que estará ao lado de src

#### Compilador Angular Ivy

- A partir da versão 8.1 do Angular