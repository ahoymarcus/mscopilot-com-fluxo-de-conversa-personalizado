# Criando um Copiloto com Fluxo de Conversa Personalizado | Microsoft Copilot Studio 


 objetivo desse artigo é o de tratar de algumas questões específicas para o Copilot Studio da Microsoft, especificamente questões relacionadas à construção agentes com fluxos de conversas personalizadas, sendo assim, também será tratado de alguns pontos importantes para a tarefa da personalização dos agentes, como por exemplo, o do uso dos "tópicos".


Ademais, esse artigo também pretende falar um pouco sobre a integração e o uso de IA Generativa aos fluxos de conversas criados e nas personalizações feitas.


Este artigo é parte do curso Microsoft AI for Tech - Copilot Studio da plataforma DIO.me.


Recordamos ainda, que de acordo com a documentação do [Microsoft.learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/environments-first-run-experience) e do site [Documentação do Copilot Studio](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/), o Copilot Studio é uma ferramenta gráfica em low-codo para criar agentes de IA:

> "uma ferramenta gráfica, low-code para criar um agente, incluindo a construção de automação com o Power Automate, e estender um Microsoft 365 Copilot com seus próprios dados e cenários corporativos".
>  [Microsoft.Learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)


Assim, além de possuir uma grande integração com a estrutura de aplicações e de nuvem da Microsoft, o Copilot Studio também tem grande flexibilidade no trabalho de alcançar e de se conectar com diversas bases de dados, inclusive em se falando de bases de dados personalizados.


<br>

## Tópicos no Copilot Studio

Segundo o [Microsoft Learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/topics-overview), os tópicos seriam os principais blocos de construção para um agente na ferramente Copilot Studio.


Nesse sentido, os tópicos poderiam ser entendidos de maneira genérica como um encadeamento ou fluxo capaz de limitar e descrever os "caminhos de conversa discretos" para o qual o agente é construído e configura de forma a permitir o fluxo adequado e natural de conversa com o usuário.


De modo geral, haveria duas formas básicas para a criação de um tópico, que poderia ser feita do zero, iniciando um tópico em branco, ou por meio da criação e utilização de uma descriação para ser utilizada pela IA, a qual, então, criaria de forma automatizada um novo tópico aplicando as definições que lhe foram apresentadas pelo usuário. 


Ainda em termos gerais, os tópicos pussuiriam duas estruturas com as quais ele trabalharia para alcançar aquele objetivo de limitar e descriver os fluxos de conversas de um agente:

1. **Frases de Gatilho**: estas estruturas funcionam como elementos condicionantes capazes de modificar o fluxo de desenvolvimento de uma conversa. 
2. **Nós de Conversa**: já estas estruturas seriam justamente os pontos para os quais os gatilhos convergiriam ao modificar o fluxo das conversas de um lado a outro.


Assim, com o intuito de simplificar o processo incial para a construção de um agente, a ferramenta Copilot Studio já possui em sua estrutura básica uma série de tópicos padrões, que servem para ajudar e para guiar o trabalho de desenvolvimento da criação dos agentes.


Temos, portanto, esses tipos de tópicos por padrão:

1. **Tópicos Personalizados**: seriam alguns gatilhos e nós fundamentais capazes de auxiliar na construção dos fluxos das conversas. Esses tópicos são mais flexíveis, na medida que os desenvolvedores podem excluí-los ou substituí-lo, bem como criar novos tópicos personalizados para serem usados. Alguns exemplos desses tópicos que a ferramenta já disponibiliza seria o de tópicos de "Saudações", de "Adeus", de "Obrigado", etc. 
2. **Tópicos do Sistema**: estes tópicos estariam presentes na ferramenta de maneira a ajudar no gerenciamento dos eventos para as conversas, como por exemplo, de início da conversa, de fim ou de erros no decorrer do processo. 


Ademais, observe ainda, que no tocante aos **tópicos de sistema**, que esses tópicos não podem ser excluídos, mas que eles apenas poderiam ser desativados, atentando para o fatode que ao ao serem desativados, o próprio comportamento geral da ferramenta Copilot Studio de gestão das conversas dos agentes pode ser afetado.


Abaixo temos as definição da documentação da Microsoft para os **tópicos de sistemas**:

| **Tópico do sistema** |	**Description** |   
| Início da conversa |	Dependendo do cliente do agente, este tópico é iniciado proativamente para iniciar a conversa com o usuário. O agente pode cumprimentar os usuários com mensagens, mesmo antes que os usuários comecem a inserir qualquer entrada. |    
| Fim da conversa    |	Este tópico deve ser posicionado no final da conversa com um agente, para que o usuário possa confirmar se sua consulta foi abordada ou não, e preencher uma pesquisa de satisfação. Este tópico é importante para medir o desempenho de um agente e atuar nele. Quando esse tópico é alcançado, presume-se que o resultado da sessão foi resolvido, a menos que o usuário não confirme explicitamente a resolução. |     
| Escalonar          |	O tópico Escalonar é usado para transferir a conversa para um sistema externo, geralmente para um agente ativo (quando configurado, por exemplo, para o Omnicanal para Customer Service do Dynamics 365). Quando esse tópico é alcançado, o resultado da sessão é escalonado. |     
| Fallback           | Este tópico é disparado quando o agente não consegue entender a consulta do usuário e a consulta não pode ser associada à confiança com nenhum tópico existente. É útil ter uma estratégia para capturar essas exceções e tratá-las de maneira elegante (com mais fontes de dados ou por meio de um caminho de escalonamento). |     
| Vários Tópicos Correspondentes (também conhecido como "você quis dizer") | Esse tópico é disparado quando vários tópicos podem abordar a entrada do usuário e o agente não tem confiança suficiente para disparar um sobre os outros. Quando esse tipo de tópico é acionado, o usuário recebe uma lista de possíveis tópicos correspondentes e pode escolher o mais adequado. |      
| Se Houver Erro     |	O tópico Se Houver Erro informa ao usuário que ocorreu um erro. A mensagem inclui um código de erro, o ID da conversa e o carimbo de data/hora do erro, que pode ser usado posteriormente para depuração. Você pode personalizar este tópico para alterar a forma como ele apresenta erros aos usuários e o que deve acontecer quando ocorrer um erro. |      
| Redefinir conversa |	Este tópico redefine a conversa limpando todos os valores de variável e forçando o agente a usar o conteúdo publicado mais recente. Ele só é acionado quando redirecionado, que é o comportamento padrão com o tópico Recomeçar. |      
| Entre              |	Este tópico solicita aos usuários que entrem quando a autenticação do usuário estiver habilitada. Ele é acionado no início da conversa quando os usuários são obrigados a entrar ou quando a conversa chega a um nó que usa variáveis de autenticação. |      


<br>

###  Gestão de Tópicos em uma Conversa

Veja que, segundo a documentação do [Microsoft Learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/triggering-topics), a seleção dos tópicos e o seu encadeamento em uma conversa partiria da relação da interação dos agentes com os usuários, bem como, ao seguir de perto alugmas daquelas padronizações existentes na própria ferramenta do Copilot Studio, como, por exemplo, com relação a algumas padronizações estabelecidas pelo uso dos tópicos de sistema e de como eles administrariam os eventos das conversas. 


Assim, inicialmente, um "gatilho" básico para a definição de um tópico poderia ser o de se fazer uma consulta ao usuário a partir do prompt esperando ou perguntando explicitamente sobre possíveis tópicos que poderiam ser servidos ao usuário por meio do agente. 


Ademais, uma outra forma corrente de intercalação entre os tópicos poderia ser por meio de redirecinamentos, sejam redirecionamentos criados pelo próprio desenvolvedor, seja por meio de redirecionamentos definidos pelo próprio Copilot. Para o primeiro caso, poderíamos da como exemplo aqueles tópicos personalizados, pois eles são capazes de disparar gatilhos para trazer novos tópicos (de "Saudações", de "Adeus", de "Obrigado", etcde "Saudações", de "Adeus", de "Obrigado", etc.). Já para o segundo caso, poderíamos falar dos tópicos de sistema, que também poderiam criar redirecionamento à medida que um conversa acionasse alguns daqueles eventos presentes na tabela acima ("Início de Conversa", "Fim de Conversa", "Erro", etc.).



<br>

### Como Estruturar os Tópicos de uma Conversa 

Também segundo a documentação do [Microsoft Learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/defining-chatbot-topics), a forma como se deve encadear os fluxos de conversa de um agente estariam intimamente ligados ao modelo de negócio e à forma como se pretende desenvolver o processo de automação de um serviço que é disponibilizado para o usuário. 


Nesse sentido:

> "Definir os melhores tópicos para seu agente requer uma compreensão das perguntas que os usuários podem fazer ou das tarefas que eles tentam realizar, e o tipo de informação e automação que você precisa fornecer. Por exemplo, um agente de varejo pode começar pedindo ao usuário que escolha entre quatro coisas que deseja fazer: encontrar uma loja, fazer um pedido, verificar o status de um pedido ou devolver um produto comprado. A resposta pode levá-los a um dos quatro tópicos, cada um com seu próprio diálogo de tópico."
> [Definir tópicos do agente](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/defining-chatbot-topics)
 

Todavia, a documentação propõem três categorias básicas às quais os serviços prestados poderiam ser encaixar:

1. **Serviço de Informação**
2. **Serviço de Realização ou Conclusão de Rarefas**
3. **Serviço de Solução de Problemas**


<br>

#### Processo de Design do Tópico

Em termos gerais, para o processo de definição do design dos tópicos, a documentação propõe alguns passo, entre eles:

1. **Identificar o Tópico**: aqui então, entra justamente o propósito geral dos serviços para os quais a organização está abrindo espaço para os seus usuários, lembrando apenas que, para a construção dos tópicos deve ser levando em conta também aspectos formas dos próprios usuários, como por exemplo, o ponto de vista do usuário, idade, comunidades a que pertence, nível de conhecimento técnico, etc.
2. **Listar Todos os Cenários Possíveis**: assim, é preciso lembrar-se que juntamente com a descrição dos cenários é preciso pensar em uma experiência completa e útil ao usuário, trazendo as informações necessárias, resoluções de tarefaz, a solução de problemas e tudo mais quanto possa ser considerado importante para construir uma boa experiência para o usuário.
3. **Projetar uma Árvore de Conversa de Alto Nível**: esta etapa, que poderia também ser vista como uma extensão da anterior, visa chamar a atenção para a importância de se construir uum modelo de agente simples e claro, ou seja, de uma modelo capaz de juntar ao serviço que se propõe, gerar satisfação ao oferecer ao usuário um fluxo agradável e capaz de ganhar a apreciação do usurário. Para tanto, o desenvolvedor poderia pensar aqui em uma série de estruturas e limitações capazes de melhorar a forma do fluxo das conversas: limite de perguntas, limites nos redirecionamentos de tópicos, limitar a quatidade de informação e manter limpa a estrutura de conversa com o cliente, criar hierarquia entre os encadeamentos para evitar que o cliente tenha necessariamente de cobrir todas as etapas, todas as vezes que ele recebe um atendimento, etc. 
4. Validação e Melhora Contínua: assim, é preciso testar se o propósito do serviço fora atendido e se ele permanece sempre atualizado com relação às necessidades do modelo de negócio e também do próprio cliente.


Algumas dicas passadas pela documentação na hora de se construir a experiẽncia do usuário:

> [!TIP]
> "Não apenas replique o que seu site ou aplicativo já pode fazer, seus clientes provavelmente estão familiarizados com seu site ou aplicativo e podem realizar tarefas comuns sozinhos sem precisar interagir com um agente."

> [!TIP]
> "Concentre-se em criar tópicos para problemas ou cenários que geram um grande volume de chats ou chamadas primeiro. Trabalhe por um período maior em outros problemas menos críticos."

> [!TIP]
> "Apresente o design mais completo possível e considere todos os possíveis cenários em que os usuários possam solicitar ou precisar de ajuda."

- **Fonte**: [Microsoft Learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/defining-chatbot-topics)


<br>

#### Uso do Tópico de Fallback

Lembramos, aqui, daquilo que fora tratado anteriormente acerca da forma como o Copilot Studio gerencia a estrutura e os fluxos de encadeamento das conversas dos agentes e de como existem alguns eventos que são padronizado dentro da ferramenta para facilitar a tarefa de desenvolvimento dos agentes.


Assim, um exemplo interessante de como trabalhar essa padronização do Copilot Studio poderia ser ao se falar dos **tópicos de sistema**, mais especificamente do tópico de sistema que diz respeito ao **"Fallback"**, uma vez que este tópico além de poder trazer uma certa complexidade natural, deve ser também bastante recorrente durante o desenvovimento das conversas do usuário com o agente.


No que diz respeito à documentação, o envento de **Fallback** seria definido assim:

> "O tópico de Fallback é disparado quando o Copilot Studio não entende um enunciado do usuário e não tem confiança suficiente para disparar um dos tópicos existentes."
> [Usar o tópico Fallback](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/fallback-topic)
 

Nesse sentido, uma importante aspecto para o uso do fallback seria a de estruturar o agente de forma que ele pudesse alcançar a "personalidade" necessária para permanecer como uma boa experiência ao usuário. Ou seja, que tão importante quanto é definir de maneira clara, precisa e agradável o encadeamento da conversa do agente com o usuário, também é importante fazer o mesmo durante esses períodos de "questão" do encadeamento do fluxo de conversa, para evitar que o usuário possa se sentir frustado ou desrespeitado, etc.


Para tanto, a ferramenta do Copilot Studio possuiria duas importantes estrurus capazes de auxiliar o desenvolvedor ao modelar e ao definir a forma dessas interações em eventos de fallback:
1. **Serviço Interno Cognitivo da Azure para Linguagem**: aqui a ferramenta traz importantes elementos capazes de gerenciar os vários "tons" da conversação, como "amigáveis", "inteligêntes", os quais inclusive podem ser também customizados pelo desenvolvedor através daqueles tópicos personalizados.
2. **Integração com Modelos de IA Generativa**: por meio de **engenharia de prompts** também seria possível alimentar o modelo básico do agente com regra e dados para gerar respostas mais específicas, atualizadas e mais abalizadas sobre tópicos variados. 


Finalmente, a documentação termina esse ponto sobre o **tópico de fallback** explicando que uma maneira prática para gerenciar de maneira adequadas esses eventos seia de modelar o fluxo de conversas de modo que pudesse haver um acompanhamento não apenas do que tem sido conversado pelo usuário com o agente, mas também de acompanhar a próprias palavras, termos e ideias trazidas pelos usuários durante a conversa, usando essas frases e termos das conversas para ajudar a dirigir e enriquecer os gatilhos a serem disparadosde novos eventos.   
 

<br>

## Algumas Orientações para o Uso de Instruções no Modo Generativo de IA

Primeiramente, é essencial apontar para a necessidade de se modelar todo o fluxo da conversa e a personalização dos tópicos, para que seja feito todo o tratamento sobre as instruções que devem alcançar o módulo de respostas generativas de IA.


<br>

### Estabelecendo Contexto para as Instruções


Assim, uma forma de aprimorar a execução das ações ou das pesquisaspor parte dos agentes seria o de trazer os dados do negócio e tratá-los de modo que possam atender as  especificações asperadas pela gestão do serviço. Nesse sentido a documentação estabelece que uma forma de se definir esse contexto no fluxo das conversas seria a de atualizar as fontes de conhecimento para o agente:

> "Por exemplo, se você der uma instrução para que seu agente pesquise as Perguntas frequentes de um site, o agente não poderá seguir essa instrução, a menos que você adicione as Perguntas frequentes do site como fonte de conhecimento. Certifique-se de que todas as instruções fornecidas ao agente estejam fundamentadas nas ações e no conhecimento que você configurou para o agente."
> [Orientação para o uso de instruções no modo generativo](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/generative-mode-guidance)


<br>

### Instruções Baseadas em Conversações

Ainda segundo a documentação, as **instruções baseadas em conversações** poderiam ser feitas adicionando-se informações específicas junto ao terminal para a chamada do módulo generativo de IA, sendo que a documentação apontaria três tipos de informações nesse sentido:

1. **Restrições**: as restrições seriam instruções para o módulo generativo de IA que definiriam **limites** ou **restrições** para o conteúdo sendo retornado para o usuário.
  - Exemplo: "Responda apenas a requerimentos que peçam informação sobre educação, legislação, bem estar, saúde e benefícios dirigidos a funcionários." 
2. **Formato de Resposta**: já o formato de resposta tem o intuito de prover instruções para o módulo generativo de IA sendo chamado de como formatar para o usuário a resposta sendo entregue ao usuário.
  - Exemplo: "Monte a responda provendo quais são os tipos de benefícios esperados, juntamente com detalhamento. Para requisitos de saúde traga comparações disponíveis aos usuários, apresentando isto em formato tabular. Responda em negrito e sublinhando as fontes." 
3. **Orientação**: finalmente, pelas orientações o desenvolvedor poderia passar insights variados, seja na forma como o módulo generativo deveria tratar os dados sendo utilizados para a resposta, bem como estabelecer condições gerais que também deveriam ser seguidas.
  - Exemplo: "Procurar apenas informações relativas a países relevantes para o empregado que busca as informações. Use o conhecimento do FAQ apenas se a questão não é relevante a consultas realizadas ou a conbranças feitas. Crie apenas tickets para o tópico de criação de tickets, pois para solução de problemas, deve ser usado o tópico específico de soluções. Não responsder questões que digam respeito ao que trata o tópico criando atendimentos manuais."


> [!TIP]
> Pode ser usada a linguagem de marcação Markdown para não apenas melhorar a legibilidade das instruções passadas para o módulo generativo de IA, como também por gerar encadeamente de prioridades, por meio do uso da listas e de listas ordenadas. 


<br>

### Recursos Adicionais

> [!NOTE]
> [Orquestrar o comportamento do agente com a IA generativa](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/advanced-generative-actions)

> [!NOTE]
> [Visão geral das fontes de conhecimento](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/knowledge-copilot-studio)

> [!NOTE]
> [Usar ações com agentes personalizados (versão preliminar)](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/advanced-plugin-actions)



<br>

- Referências:

1. [Tópicos no Copilot Studio](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/topics-overview)
2. [Visão geral do Copilot Studio](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)
3. [Documentação do Microsoft Copilot Studio](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/)
4. [Auditar atividades do Copilot Studio no Microsoft Purview](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/admin-logging-copilot-studio)


<br>

## Links:

 - [linkedin](https://www.linkedin.com/in/marcus-vinicius-richa-183104199/)
 - [Github](https://github.com/ahoymarcus/)
 - [My Old Web Portfolio](https://redux-reactjs-personal-portfolio-webpage-version-2.netlify.app/)



