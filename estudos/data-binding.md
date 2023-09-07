# Data Binding

- Forma de exibir dados que venham de um componente ou de um backend que se consumiu via REST.
- One-way binding: valor vem do componente até a property mas não faz o caminho inverso.
- Tipos:
    - Interpolation 
    - Property Binding
    - Event Binding
    - Two-way Binding

#### Interpolation

- É a forma mais fácil de exibir um dado na tela.
- É um One-way binding

~~~html
<label>Nome: {{meuDado}}</label>
~~~

#### Property Binding

- Para levar uma informação do componente para o template (tags).
- O angular ficará responsável pela propriedade entre colchetes de uma tag HTML.
- É um One-way binding

~~~html
<img [src]="minhaUrl"> 
    <!-- minhaUrl é a variável 
            O Angular fica responsável por "cuidar" da propriedade src do elemento img
            é equivalente ao interpolation usado desta forma
            <img src={{minhaUrl}}>
    -->
~~~

#### Event Binding

- Realiza a chamada de um método com base em um evento de um elemento HTML.
- Para levar a informação do template para o componente.
- Não faz o caminho contrário.
- Ex. de uso: validar ou submeter formulários
- É um One-way binding

~~~html
<button (click)='clickContador()'>clique aqui</button>
~~~

#### Two-way Binding

- Exibe e atualiza um dado nas duas direções (template, componente).
- É a união do property-binding com o event-binding.

~~~html
<input class="form-control" type="text" [(ngModel)] = "evento.nome" /> 
    <!-- ngModel = diretiva, [()] = notação "banana numa caixa" -->
<label>Nome do evento: {{evento.nome}}</label>
~~~
