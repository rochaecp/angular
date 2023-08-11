# Exemplo de criação de aplicação

1. Criar a aplicação
    ~~~bash
    ng new --minimal -g MeuProjeto # minima e sem git (-g)
        # não adicionar roteamento (para treinar)
        # usar o css
    ~~~
1. Inserir o css do Bootstrap no arquivo index.html
1. Criar os componentes
    ~~~bash
    ng g c navegacao/menu 
    ng g c navegacao/home
    ng g c navegacao/footer
    ng g c institucional/sobre
    ng g c institucional/contato
    ~~~
1. Para os componentes criados:
    - Excluir arquivo spec e css 
    - Remover a interface e o css do \<NomeComponente\>.component.ts    
1. Na pasta app: criar o arquivo app.routes.ts    
    ~~~javascript
    import { Routes } from '@angular/router';
    import { HomeComponent } from './navegacao/home/home.component';
    import { ContatoComponent } from './institucional/contato/contato.component';
    import { SobreComponent } from './institucional/sobre/sobre.component';

    export const rootRouterConfig: Routes = [
        { path: '', redirectTo: '/home', pathMatch: 'full' },
        { path: 'home', component: HomeComponent },
        { path: 'contato', component: ContatoComponent },
        { path: 'sobre', component: SobreComponent },
    ];
    ~~~
1. Adicione referências ao app.route.ts no app.module.ts
1. Inserir a tag ```<router-outlet></router-outlet>``` no arquivo app.component.html
1. Adicionar diretivas de navegação no menu.component.html
