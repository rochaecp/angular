# Angular CLI (Command Line Interface)

## Obter informações sobre comandos

- Documentação oficial: <https://angular.io/cli>

~~~bash
ng --help
ng new --help
ng g --help # Verificar o que podemos criar
ng version # versao do angular, do cli, ...
~~~

## Criar uma nova aplicação

- Por default o prefixo (--prefix) da aplicação é app

~~~bash
ng new NomeApp
~~~

## Criar uma aplicação de tamanho mínimo e sem git

~~~bash
ng new --minimal -g NomeProjeto # minima e sem git (-g)
~~~    

## Criar uma parte de uma aplicação (componente, rota, serviço, etc)

~~~bash
ng generate --help # ou n g --help para ver opções
~~~

## Criar um módulo

~~~bash
ng g module NomeModulo 
~~~    

## Criar um serviço

~~~bash
ng g service NomeServico
~~~            

## Rodar localmente a aplicação

- "Builda" e serve seu aplicativo
- "re-Builda" caso haja alterações de arquivo
- O webpack compacta tudo
- Gera os chunks (pedaços de código da aplicação)

~~~bash
ng serve # ou ng s
~~~

## Rodar localmente de modo semelhante a como seria em produção  

- Apenas para desenvolvimento

~~~bash
ng serve --prod
~~~

## Compilar a aplicação (sem rodar) no diretório dist (distribution)

- No diretório dist gera os arquivos que iriam par ao servidor
- TODO: comando para buildar de modo otimizado para prod

~~~bash
ng build
~~~   

## Compilar para produção

~~~bash
ng build --prod
~~~

## Executar testes de unidade em um determinado projeto

~~~bash
ng test
~~~

## Criar e atender um aplicativo Angular e, em seguida, executa testes de ponta a ponta

~~~bash
ng e2e
~~~

## Diversos

#### Baixar um código fonte (virá sempre sem o node_modules) e rodar localmente

~~~bash
npm i
~~~
