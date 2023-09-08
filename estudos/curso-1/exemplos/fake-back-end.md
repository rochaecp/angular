# Fake back-end

## Criar um fake back-end com JSON Server

#### Instalar o pacote JSON Server

~~~bash
npm install -g json-server # instala globalmente
~~~

#### Criar o arquivo *produtos.json* na raíz do projeto para simular o back-end

~~~json
{
    "produtos": [
        {
            "id": 1,
            "nome": "notebook topzeira",
            "valor": 1532,
            "promocao": false,
            "valorPromo": 0,
            "imagem": "note.jpg"
        },
        {
            "id": 2,
            "nome": "Impressora Baratona",
            "valor": 499,
            "promocao": true,
            "valorPromo": 200,
            "imagem": "impressora.jpg"
        },
        {
            "id": 3,
            "nome": "Teclado Gamer",
            "valor": 130,
            "promocao": false,
            "valorPromo": 0,
            "imagem": "teclado.jpg"
        },
        {
            "id": 4,
            "nome": "Monitor Ultrawide",
            "valor": 1530,
            "promocao": false,
            "valorPromo": 0,
            "imagem": "monitor.jpg"
        }
    ],
    "servicos" : [
        {
            "id": 1,
            "nome": "Manutenção de celular", 
            "valor": 200
        }
    ]
}
~~~

#### Em um terminal digite no diretório raís do projeto

~~~bash
json-server --watch produtos.json
~~~

- Será criado um endpoint para produtos e outro para serviços:
    - http://localhost:3000/produtos
    - http://localhost:3000/servicos

## Criar um serviço HttpClient

#### No projeto anterior na pasta *app* 

- Criar uma pasta chamada *produtos*.

#### Na pasta *produtos*

- Criar o arquivo *produtos.service.ts*.
- Criar o arquivo *produto.ts*.

#### No arquivo *produto.ts*

- Definir o tipo produto.
- Configurar o "strictPropertyInitialization": false, no compilerOptions

~~~typescript
export class Produto {
    id: string;
    nome: string;
    valor: string;
    promocao: boolean;
    valorPromo: string;
    imagem: string;
}
~~~

#### No arquivo *produtos.service.ts*

~~~typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Produto } from './produto';
import { Observable } from './rxjs';

@Injectable() // indica que é um serviço
export class ProdutoService {

constructor(private http: HttpClient) {} // injeção de dependência no construtor

    protected urlServiceV1: string = "http://localhost:3000/"; // endreço do endpoint

    // retorna uma lista de produtos, observable é um callback
    obterProdutos() : Observable<Produto[]> {  
        return this.http
            .get<Produto[]>(this.UrlServiceV1 + "produtos");
    }
}
~~~

#### No arquivo *app.module.ts*

- Registrar nos providers o módulo do serviço criado.

~~~typescript
// (...)
import { ProdutoService } from './produtos/produtos.service';
// (...)
providers: [
    ProdutoService,
]
~~~

#### Criar um componente para listar os produtos

~~~bash
ng g c produtos/ListaProduto
~~~

#### Na pasta *produtos/lista-produto*

- Criar o *lista-produto.component.html*

#### No arquivo *lista-produto.component.ts*

~~~typescript
import { Component, OnInit } from '@angular/core';
import { Produto } from '../produto';
import { ProdutoService } from '../produtos.service';

@Component({
  selector: 'app-lista-produto',
  templateUrl: './lista-produto.component.html'
})
export class ListaProdutoComponent implements OnInit {

    constructor(private produtoService: ProdutoService) { }

    public produtos: Produto[];

    ngOnInit() { // método chamado assim que o componente é instanciado
        this.produtoService.obterProdutos()
        .subscribe( 
            produtos => { // situação caso não dê erro
                this.produtos = produtos; // passamos o resultado para a coleção de produtos
                console.log(produtos);
            },
            error => console.log(error) // situação caso de erro
        );
    }
}
~~~

#### No arquivo *app.routes.ts*

- Adicionar a rota para o componente ListaProduto.

~~~typescript
// (...)
import { ListaProdutoComponent } from './produtos/lista-produto/lista-produto.component';

export const rootRouterConfig: Routes = [
    // (...)
    { path: 'produtos', component: ListaProdutoComponent }
    { path: 'produto-detalhe/:id', component: ListaProdutoComponent } // adicional
]
~~~

#### No arquivo *app.module.ts*

- Adicionar suporte ao HttpClientModule

~~~typescript
// (...)
import { HttpClientModule } from '@angular/common/http';
import { registerLocaleData } from '@angular/common'; // para o pipe da moeda R$
import localePt from '@angular/common/locales/pt'; // local
registerLocaleData(localePt); // registra o local

// (...)
imports: [
    // (...)
    HttpClientModule,
]
~~~

#### No arquivo *lista-produto.component.html*

~~~html
<div class="row text-center mt-5 ms-5 me-5">
    <div *ngFor="let produto of produtos" class="col-md-4 mb-5">
        <div class="card h-100">
            <div class="card-body">
                <h4 class="card-title">{{produto.nome | titlecase }}</h4>
                <p>Preço: {{produto.valor | currency:'BRL':'symbol':'1.2-2':'pt' }}</p>
                <a [routerLink]="['/produto-detalhe', produto.id]">Ver detalhes do produto</a>
                <div *ngIf="produto.promocao" class="card-body">
                    O Produto está em promoção!
                </div>
                <div [ngSwitch]="produto.promocao">
                    <p *ngSwitchCase="true">Promoção!</p>
                    <p *ngSwitchCase="false">Preço Normal</p>
                </div>                    
            </div>
        </div>        
    </div>
</div>
~~~

#### No arquivo *navegacao/menu/menu.component.html*, adicionar

~~~html
<li class="nav-item">
    <a class="nav-link" [routerLink]="['/produtos']">Produtos</a>
</li>    
~~~
