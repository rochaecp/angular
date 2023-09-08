# Componentes

- Cada componente é formado por: 
    - Um template (é um arquivo HTML, parte visual)
    - Uma classe (com propriedades e métodos, code behind) 
    - Metadata (dados que dizem como a classe se comporta e com quais arquivos está ligada)
- Código de um componente
    - Dependências
    - Metadados
    - Definição da classe
- Um componente é formado por
    - um arquivo .ts - "componente" e "metadado" ou "decorators"
    - um arquivo .html - "template"
    - um arquivo .css - "estilo"
    - um arquivo .spec.ts - "especificação de testes"

## Exemplo

~~~javascript
// Arquivo app.component.ts
import { Component } from '@angular/core'; // import da diretiva que diz que é um componente

@Component({ // @Component indica que classe é um componente
    selector: 'app-root', // nome para invocar o componente no html
    templateUrl: './app.component.html', // caminho do template
    styleUrls: ['./app.component.css'] // caminho do css
})
export class AppComponent { // parte declarativa da classe
    title = 'MeuApp';
}
~~~

## Criar um componente via Angular CLI

- Pode deletar a spec.ts e o .css (remover respectivos caminhos do .ts)
- Os nomes de arquivo terminarão automaticamente com .component.\<extensão\>
- Implementa a interface OnInit logo, implementar método ngOnInit (método que sempre é chamado após o construtor)
- Ao criarmos um componente ele é automaticamente registrado no app.module.ts

~~~bash
ng generate component pasta/NomeComponente 
    # ou ainda ng g c pasta/NomeComponente
~~~
