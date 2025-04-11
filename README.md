# Criando um Copiloto com Fluxo de Conversa Personalizado no Microsoft Copilot Studio | Microsoft AI for Tech - Copilot Studio

O objetivo desse artigo é o de tratar de algumas questões específicas para o Copilot Studio da Microsoft, especificamente questões relacionadas à construção agentes com fluxos de conversas personalizadas, sendo assim, também será tratado de alguns pontos importantes para a tarefa da personalização dos agentes, como por exemplo, o do uso dos "tópicos".


Ademais, esse artigo também pretende falar um pouco sobre a integração e o uso de IA Generativa aos fluxos de conversas criados e nas personalizações feitas.


Recordamos que, de acordo com a documentação do [Microsoft.learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/environments-first-run-experience) e do site [Documentação do Copilot Studio](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/), o Copilot Studio é uma ferramenta gráfica em low-codo para criar agentes de IA:

> "uma ferramenta gráfica, low-code para criar um agente, incluindo a construção de automação com o Power Automate, e estender um Microsoft 365 Copilot com seus próprios dados e cenários corporativos".
>  [Microsoft.Learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)


Assim, além de possuir uma grande integração com a estrutura de aplicações e de nuvem da Microsoft, o Copilot Studio também tem grande flexibilidade no trabalho de alcançar e de se conectar com diversas bases de dados, inclusive em se falando de bases de dados personalizados.


## Tópicos no Copilot Studio

Segundo o [Microsoft Learn](https://learn.microsoft.com/pt-br/microsoft-copilot-studio/guidance/topics-overview), os tópicos seriam os principais blocos de construção para um agente na ferramente Copilot Studio.


Nesse sentido, os tópicos poderiam ser entendidos de maneira genérica como um encadeamento ou fluxo capaz de limitar e descrever os "caminhos de conversa discretos" para o qual o agente é construído e configura de forma a permitir o fluxo adequado e natural de conversa com o usuário.


De modo geral, haveria duas formas básicas para a criação de um tópico, que poderia ser feita do zero, iniciando um tópico em branco, ou por meio da criação e utilização de uma descriação para ser utilizada pela IA, a qual, então, criaria de forma automatizada um novo tópico aplicando as definições que lhe foram apresentadas pelo usuário. 


Ainda em termos gerais, os tópicos pussuiriam duas estruturas com as quais ele trabalharia para alcançar aquele objetivo de limitar e descriver os fluxos de conversas de um agente:

1. Frases de Gatilho: estas estruturas funcionam como elementos condicionantes capazes de modificar o fluxo de desenvolvimento de uma conversa. 
2. Nós de Conversa: já estas estruturas seriam justamente os pontos para os quais os gatilhos convergiriam ao modificar o fluxo das conversas de um lado a outro.


Assim, com o intuito de simplificar o processo incial para a construção de um agente, a ferramenta Copilot Studio já possui em sua estrutura básica uma série de tópicos padrões, que servem para ajudar e para guiar o trabalho de desenvolvimento da criação dos agentes.


Temos, portanto, esses tipos de tópicos por padrão:

1. **Tópicos Personalizados**: seriam alguns gatilhos e nós fundamentais capazes de auxiliar na construção dos fluxos das conversas. Esses tópicos são mais flexíveis, na medida que os desenvolvedores podem excluí-los ou substituí-lo, bem como criar novos tópicos personalizados para serem usados. Alguns exemplos desses tópicos que a ferramenta já disponibiliza seria o de tópicos de "Saudações", de "Adeus", de "Obrigado", etc. 
2. **Tópicos do Sistema**: estes tópicos estariam presentes na ferramenta de maneira a ajudar no gerenciamento dos eventos para as conversas, como por exemplo, de início da conversa, de fim ou de erros no decorrer do processo. 


Ademais, observe ainda, que no tocante aos **tópicos de sistema**, que esses tópicos não podem ser excluídos, mas que eles apenas poderiam ser desativados, atentando para o fatode que ao ao serem desativados, o próprio comportamento geral da ferramenta Copilot Studio de gestão das conversas dos agentes pode ser afetado.


Abaixo temos as definição da documentação da Microsoft para os **tópicos de sistemas**:
|  Tópico do sistema |	Description |
| Início da conversa |	Dependendo do cliente do agente, este tópico é iniciado proativamente para iniciar a conversa com o usuário. O agente pode cumprimentar os usuários com mensagens, mesmo antes que os usuários comecem a inserir qualquer entrada. |
| Fim da conversa    |	Este tópico deve ser posicionado no final da conversa com um agente, para que o usuário possa confirmar se sua consulta foi abordada ou não, e preencher uma pesquisa de satisfação. Este tópico é importante para medir o desempenho de um agente e atuar nele. Quando esse tópico é alcançado, presume-se que o resultado da sessão foi resolvido, a menos que o usuário não confirme explicitamente a resolução. |
| Escalonar          |	O tópico Escalonar é usado para transferir a conversa para um sistema externo, geralmente para um agente ativo (quando configurado, por exemplo, para o Omnicanal para Customer Service do Dynamics 365). Quando esse tópico é alcançado, o resultado da sessão é escalonado. | 
| Fallback           | Este tópico é disparado quando o agente não consegue entender a consulta do usuário e a consulta não pode ser associada à confiança com nenhum tópico existente. É útil ter uma estratégia para capturar essas exceções e tratá-las de maneira elegante (com mais fontes de dados ou por meio de um caminho de escalonamento). |
| Vários Tópicos Correspondentes (também conhecido como "você quis dizer") | Esse tópico é disparado quando vários tópicos podem abordar a entrada do usuário e o agente não tem confiança suficiente para disparar um sobre os outros. Quando esse tipo de tópico é acionado, o usuário recebe uma lista de possíveis tópicos correspondentes e pode escolher o mais adequado. |
| Se Houver Erro     |	O tópico Se Houver Erro informa ao usuário que ocorreu um erro. A mensagem inclui um código de erro, o ID da conversa e o carimbo de data/hora do erro, que pode ser usado posteriormente para depuração. Você pode personalizar este tópico para alterar a forma como ele apresenta erros aos usuários e o que deve acontecer quando ocorrer um erro. |
| Redefinir conversa |	Este tópico redefine a conversa limpando todos os valores de variável e forçando o agente a usar o conteúdo publicado mais recente. Ele só é acionado quando redirecionado, que é o comportamento padrão com o tópico Recomeçar. |
| Entre              |	Este tópico solicita aos usuários que entrem quando a autenticação do usuário estiver habilitada. Ele é acionado no início da conversa quando os usuários são obrigados a entrar ou quando a conversa chega a um nó que usa variáveis de autenticação. |


##  Gestão de Tópicos em uma Conversa

Veja que, segundo a documentação do [Microsoft Learn](), a seleção dos tópicos e o seu encadeamento em uma conversa partiria da relação da interação dos agentes com os usuários, bem como, ao seguir de perto alugmas daquelas padronizações existentes na própria ferramenta do Copilot Studio, como, por exemplo, com relação a algumas padronizações estabelecidas pelo uso dos tópicos de sistema e de como eles administrariam os eventos das conversas. 


Assim, inicialmente, um "gatilho" básico para a definição de um tópico poderia ser o de se fazer uma consulta ao usuário a partir do prompt esperando ou perguntando explicitamente sobre possíveis tópicos que poderiam ser servidos ao usuário por meio do agente. 


Ademais, uma outra forma corrente de intercalação entre os tópicos poderia ser por meio de redirecinamentos, sejam redirecionamentos criados pelo próprio desenvolvedor, seja por meio de redirecionamentos definidos pelo próprio Copilot. Para o primeiro caso, poderíamos da como exemplo aqueles tópicos personalizados, pois eles são capazes de disparar gatilhos para trazer novos tópicos (de "Saudações", de "Adeus", de "Obrigado", etcde "Saudações", de "Adeus", de "Obrigado", etc.). Já para o segundo caso, poderíamos falar dos tópicos de sistema, que também poderiam criar redirecionamento à medida que um conversa acionasse alguns daqueles eventos presentes na tabela acima ("Início de Conversa", "Fim de Conversa", "Erro", etc.).




















 


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



