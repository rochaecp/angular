# Diretivas de Decisão

- ngIf
- ngFor
- ngSwitch

#### ngSwitch

~~~html
<div [ngSwitch]="produto.promocao">
    <p *ngSwitchCase="true">Promoção!</p>
    <p *ngSwitchCase="false">Preço Normal</p>
</div>    
~~~