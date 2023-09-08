# Data Bindings

## Criar o componente

~~~bash
ng g c exemplos/DataBinding
~~~

## Adicionar o path para o componente criado

#### No arquivo *app.routes.ts*    

~~~javascript
import { DataBindingComponent } from './exemplos/data-binding/data-binding.component';
{ path: 'exemplo-data-binding', component: DataBindingComponent}
~~~

## Adicionar o item de menu Exemplos

#### No arquivo *menu.component.html*    

~~~html
<li class="nav-item">
    <a class="nav-link" [routerLink]="['/exemplo-data-binding']">Exemplos</a>
</li>  
~~~

#### No arquivo *data-binding.component.ts*

~~~javascript
export class DataBindingComponent {
    public contadorClique: number = 0;
    public urlImagem: string = "https://aventurasnahistoria.uol.com.br/media/uploads/personagem/chico5.jpg";
    public nome: string = "";

    adicionarClique() {
        this.contadorClique++;
    }

    // soltaTecla(evento: any) { // any: argumento pode ser de qualquer tipo
    //     this.nome = evento.target.value; // target == objeto da caixa de texto
    // }
}
~~~

## Criar as páginas html 

#### No arquivo *app.module.ts*

- Adicionar o import do FormsModule

~~~javascript
import { FormsModule } from '@angular/forms';

// (...)

imports : [
    // (...)
    FormsModule,
]
~~~

#### No arquivo *data-binding.component.html*

~~~html
<h4>Interpolation</h4>
<p>O número de cliques é {{contadorClique}}</p>
<p [ngClass]="{
    'text-danger': contadorClique < 3,
    'text-success': contadorClique >= 3 }">
    A classe do parágrafo será alterada dependendo do valor do contador de Clique
</p>
<br>

<h4>Propery Binding</h4>
<button class="btn btn-info" [disabled]="contadorClique >= 10">Posso ficar Disabled</button><br><br>
<img [src]="urlImagem" width="400px">
<br>

<h4>Event Binding</h4>
<button class="btn btn-warning" (click)='adicionarClique()'>Incrementar contador</button><br><br>
<br>

<!-- <h4>Sem Two-way Binding</h4>
<input type="text" (keyup)='soltaTecla($event)' placeholder="Digite o seu nome"><br>
<label>Ola: {{ nome }}</label>
<br> -->

<h4>Two-way Binding - forma menos elegante</h4>
<input type="text" [ngModel]="nome" (ngModelChange)='nome = $event' placeholder="Digite o seu nome">
    <!-- a variável nome é a model e ao alterar o campo o nome recebe
    o valor de retorno do evento -->
<br>
<label>Ola: {{ nome }}</label> 

<h4>Two-way Binding - forma elegante</h4>
<input type="text" [(ngModel)]="nome" placeholder="Digite o seu nome">
    <!-- [(ngModel)]="nome" é o mesmo que 
        [ngModel]="nome" (ngModelChange)='nome = $event' -->
<br>
<label>Ola: {{nome}}</label> 
~~~