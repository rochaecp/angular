# Modules

- Um módulo pode representar uma funcionalidde
- Existe apenas um módulo principal: app.module.ts
- Criar um módulo
    ~~~bash
    ng g module Funcionalidade
    ~~~
- Um módulo é um arquivo nomeModulo.module.ts
- Todos módulos criados precisam importar o CommonModule
- Cada módulo possui
    - declarações
        - colocamos os componentes
    - imports
        - colocamos os módulos
    - providers
        - colocamos os serviços
    - bootstrap
        - só existe no app.module.ts
        - diz que o AppComponent chamará todo o restante da aplicação  
            - No arquivo main.ts isso é configurado
- app-routing.module.ts
    - Módulo que cuida das rotas
        - "forRoot" = "para o módulo principal"
- Criar um serviço
    ~~~bash
    ng g service Servico
    ~~~       
- Um serviço é um arquivo nomeServico.service.ts
    - Ele será um Injectable
    - Podemos colocar o serviço criado no providers do app.module.ts