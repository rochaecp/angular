# Exemplo de criação de aplicação

#### Criar a aplicação

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

#### Inserir o css do Bootstrap e do font-awesome no arquivo *index.html*

- Outra opção de framework front-end seria o Angular Material.
- Existe também o componente ngx-bootstrap.
- Não misturar JQuery com Angular.

~~~html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" crossorigin="anonymous">
~~~

#### Criar os componentes

- No arquivo *app.component.ts*
    - Criar o arquivo *app.component.html*
    - Substituir o trecho inline "template: ..." por "templateUrl: app.component.html"
- No arquivo *app.component.html*
    - Inserir os códigos html/bootstrap do menu, corpo e footer
- No arquivo *style.css*    
    - Adicionar estilos globais, ex.: uma classe .footer
- Criar os componentes:
    - São registrados automaticamente no *app.module.ts*
    - Remover os arquivos spec.ts e css
    - Criar manualmente o arquivo menu.component.html

~~~bash
ng g c navegacao/menu 
    # g = generate, c = component
~~~

- No arquivo *menu.component.ts*
    - Remover a referência ao css: "styleUrls:"
    - Adicionar a referência: templateUrl: 'menu.component.html'
- Criar os demais componentes (e repetir os passos acima):
    - navegacao/home
    - navegacao/footer
    - institucional/sobre
    - institucional/contato
- No arquivo *app.component.html* 
    - Extrair a parte de navegação para o arquivo *menu.component.html*.
    - Extrair a parte do corpo para o arquivo *home.component.html*.
    - Extrair a parte do rodape para o arquivo *rodape.component.html*.
    - Inserir os seletores dos componentes acima no arquivo *app.component.html*:

~~~html
<app-menu></app-menu>
<app-home></app-home>
<app-rodape></app-rodape>
~~~

#### Criar rotas

- Na pasta app: criar o arquivo *app.routes.ts* (arquivo de configuração) 

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

- Adicionar os imports No arquivo *app.module.ts*:

~~~javascript
import { RouterModule } from '@angular/router';
import { rootRouterConfig } from './app.routes';
import { APP_BASE_HREF } from '@angular/common';
~~~

- Incluir no @NgModule:

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

- Substituir a tag app-home no arquivo *app.component.html*:

~~~html
<router-outlet></router-outlet>
    <!-- Indica que a navegação ocorrerá aqui
            É o trecho que será modificado -->
~~~

- Preencher os arquivos *component.html* de:
    - institucional/sobre
    - institucional/contato        
- No arquivo *menu.component.html*:
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

## Data Bindings - exemplo

#### Criar o componente

~~~bash
ng g c exemplos/DataBinding
~~~

#### Adicionar o path para o componente data-binding criado

- No arquivo *app.routes.ts*    

~~~javascript
import { DataBindingComponent } from './exemplos/data-binding/data-binding.component';
{ path: 'exemplo-data-binding', component: DataBindingComponent}
~~~

#### Adicionar o item de menu Exemplos

- No arquivo *menu.component.html*    

~~~html
<li class="nav-item">
    <a class="nav-link" [routerLink]="['/exemplo-data-binding']">Exemplos</a>
</li>  
~~~

- No arquivo *data-binding.component.ts*

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

- No arquivo *data-binding.component.html*

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
