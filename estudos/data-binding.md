# Data Binding

- Forma de exibir dados que venham de um componente ou de um backend que se consumiu via REST.
- One-way binding: valor vem do componente até a property mas não faz o caminho inverso.

- - - 

- Tipos
    
    - Interpolation
        ~~~html
        <label>Nome: {{meuDado}}</label>
        ~~~

    - Property Binding
        - Para ir do componente para o template.
        ~~~html
        <img [src]="minhaUrl"> <!-- minhaUrl é a variável -->
        ~~~

    - Event Binding
        - Chama método com base em um evento de um elemento HTML.
        - Para ir do template para o componente.
        - Não faz o caminho contrário.
        ~~~html
        <button (click)='clickContador()'>clique aqui</button>
        ~~~

    - Two-way Binding
        - Exibe e atualiza um dado nas duas direções.
        - É a união do property binding com o event binding.
        ~~~html
        <input class="form-control" type="text" [(ngModel)] = "evento.nome" /> <!-- ngModel = diretiva, [()] = notação "banana numa caixa" -->
        <label>Nome do evento: {{evento.nome}}</label>
        ~~~
