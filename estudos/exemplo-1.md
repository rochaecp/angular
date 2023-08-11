# Exemplo de criação de aplicação

1. Criar a aplicação
    ~~~bash
    ng new --help
        # informacoes gerais sobre o comando
    ng new --minimal -g MeuProjeto 
        # minima (--minimal) e sem git (-g)
        # não adicionar roteamento (para treinar)
        # usar o css
    ng serve 
        # testar
        # Parar a aplicação: Ctrl + C
    ~~~
1. Inserir o css do Bootstrap e o font-awesome no arquivo *index.html*
    - Outra opção de framework front-end seria o Angular Material.
    - Existe também o componente ngx-bootstrap.
    - Não misturar JQuery com Angular.
    ~~~html
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" crossorigin="anonymous">
    ~~~

- - -

1. No arquivo *app.component.ts*
    - Criar o arquivo *app.component.html*
    - Substituir o trecho inline "template: ..." por "templateUrl: app.component.html"
1. No arquivo *app.component.html*
    - Inserir os códigos html/bootstrap do menu, corpo e footer
1. No arquivo *style.css*    
    - Adicionar estilos globais, ex.: uma classe .footer
1. Criar os componentes:
    - São registrados automaticamente no *app.module.ts*
    ~~~bash
    ng g c navegacao/menu 
        # g = generate, c = component
    ~~~
    - Remover os arquivos spec.ts e css
    - Criar manualmente o arquivo menu.component.html
1. No arquivo *menu.component.ts*
    - Remover a referência ao css: "styleUrls:"
    - Adicionar a referência: templateUrl: 'menu.component.html'
1. Criar os demais componentes (e repetir os passos acima):
    - navegacao/home
    - navegacao/footer
    - institucional/sobre
    - institucional/contato
1. No arquivo *app.component.html* 
    - Extrair a parte de navegação para o arquivo *menu.component.html*.
    - Extrair a parte do corpo para o arquivo *home.component.html*.
    - Extrair a parte do rodape para o arquivo *rodape.component.html*.
    - Inserir os seletores dos componentes acima no arquivo *app.component.html*:
        ~~~html
        <app-menu></app-menu>
        <app-home></app-home>
        <app-rodape></app-rodape>
        ~~~

- - - 

1. Na pasta app: criar o arquivo *app.routes.ts* 
    - É um arquivo de configuração.
    ~~~javascript
    import { Routes } from '@angular/router'; // para configuração de rotas
    import { HomeComponent } from './navegacao/home/home.component';
    import { ContatoComponent } from './institucional/contato/contato.component';
    import { SobreComponent } from './institucional/sobre/sobre.component';

    // constante criada para adicionar as rotas
    export const rootRouterConfig: Routes = [
        { path: '', redirectTo: '/home', pathMatch: 'full' }, // path de redirecionamento
        { path: 'home', component: HomeComponent },
        { path: 'contato', component: ContatoComponent },
        { path: 'sobre', component: SobreComponent },
    ];
    ~~~

1. No arquivo *app.module.ts*:
    - Adicionar os imports: 
        ~~~javascript
        import { RouterModule } from '@angular/router';
        import { rootRouterConfig } from './app.routes';
        import { APP_BASE_HREF } from '@angular/common';
        ~~~
    - No @NgModule incluir:
        ~~~javascript
        imports: [
            BrowserModule,
            [RouterModule.forRoot(rootRouterConfig, { useHash: false })] // rootRouterConfig é a constante criada no arquivo app.routes.ts       
        ],
        providers: [
            { provide: APP_BASE_HREF, useValue: '/' } 
                // prefixo de rota
                // poderia ser /nomePrefixo/
        ]
        ~~~    
1. No arquivo *app.component.html*:
    - Substituir a tag app-home pela tag 
        ~~~html
        <router-outlet></router-outlet>
            <!-- Indica que a navegação ocorrerá aqui
                 É o trecho que será modificado -->
        ~~~
1. Preencher os arquivos component.html de:
    - institucional/sobre
    - institucional/contato        
1. No arquivo *menu.component.html*:
    - Substituir os href="#" dos links do menu pelas diretivas:
    - Deve utilizar os paths configurados no arquivo *app.routes.ts*
        ~~~html
        <li class="nav-item">
            <a class="nav-link active" [routerLink]="['/home']">Página Inicial</a>
        </li>        
        <!-- os outros: 
                [routerLink]="['/sobre']"
                [routerLink]="['/contato'] -->
        ~~~

- - - 

#### Data Bindings - exemplo

1. Crie o componente:
    ~~~bash
    ng g c exemplos/DataBinding
    ~~~
1. No arquivo *app.routes.ts*    
    - Adicionar o path para o componente data-binding criado
        ~~~javascript
        import { DataBindingComponent } from './exemplos/data-binding/data-binding.component';
        { path: 'exemplo-data-binding', component: DataBindingComponent}
        ~~~
1. No arquivo *menu.component.html*    
    - Adicionar o item de menu Exemplos:
        ~~~html
        <li class="nav-item">
            <a class="nav-link" [routerLink]="['/exemplo-data-binding']">Exemplos</a>
        </li>  
        ~~~
1. No arquivo *data-binding.component.ts*
    - Adicionar
        ~~~javascript
        export class DataBindingComponent {
            public contadorClique: number = 0;
            public urlImagem: string = "https://aventurasnahistoria.uol.com.br/media/uploads/personagem/chico5.jpg";
            public nome: string = "";

            adicionarClique() {
                this.contadorClique++;
            }

            soltaTecla(evento: any) { // any: argumento pode ser de qualquer tipo
                this.nome = evento.target.value;
            }
        }
        ~~~
1. No arquivo *data-binding.component.html*
    - Adicionar
        ~~~html
        <h4>Interpolation</h4>
        <p>O número de cliques é {{contadorClique}}</p>

        <h4>Propery Binding</h4>
        <button class="btn btn-info" [disabled]="contadorClique >= 10">Posso ficar Disabled</button><br><br>
        <img [src]="urlImagem" width="400px">

        <h4>Event Binding</h4>
        <button class="btn btn-warning" (click)='adicionarClique()'>Incrementar contador</button><br><br>
            <!-- Buscar correspondencia entre eventos HTML e interpretação deles no Angular -->

        <h4>Sem Two-way Binding</h4>
        <input type="text" (keyup)='soltaTecla($event)' placeholder="Digite o seu nome"><br>
        <label>Ola: {{ nome }}</label>
        ~~~

