## Adotando a cultura DevOps - Aula 01
- Nesta aula, abordamos o framework CALMS, uma ferramenta para medir e acompanhar a implementação da cultura DevOps em uma organização. Através de um diagnóstico cultural, o CALMS avalia se a empresa já está no modo DevOps ou se ainda está distante. O diagnóstico considera aspectos como a resolução de problemas, a busca por culpados versus a resolução em equipe, e a existência de um processo de pós-mortem para aprender com os erros. O objetivo é identificar falhas nos processos e implementar medidas para mitigá-las, evitando que se repitam no futuro. Nas próximas aulas, exploraremos o CALMS em mais detalhes.
- A ideia é aprender com o erro, buscar entender qual foi o erro que deu e quais ações podem ser tomadas dado cenário
- Não poder ter uma cultura que prove sempre uma pessoa culpada e que nunca olhe para tras para o passado, mas sempre pensando em buscar medidas para mitigar as falhas

## Automatizando tudo - Aula 02
- Nesta aula, exploramos o pilar de Automação (A) dentro do framework COMS. O foco está em dois aspectos: entrega contínua e GitOps/IAC. A entrega contínua deve ser automatizada para reduzir o tempo gasto em tarefas repetitivas e garantir agilidade na implantação. Já o GitOps/IAC visa estabelecer uma única fonte de verdade para recursos em nuvem, centralizando o gerenciamento no Git e garantindo maior segurança, economia e manutenabilidade. Abordaremos esses tópicos em detalhes em módulos específicos.
- No que tange entrega contínua é todo o fluxo é todo o fluxo de publicação da sua aplicação. Então, instalação de dependências, teste, os tipos de testes que vão ser executados, a parte de buildar a sua aplicação e a parte de fazer, de fato, a implantação ali com o CD. Inclusive, a gente vai ter um módulo somente sobre CA e CD para falar sobre isso.
- o segundo ponto, que é ali a parte IAC e GitOps, nós também vamos ter um módulo sobre isso, um módulo exclusivo sobre isso, mas, explicando rapidamente, você precisa ter fontes únicas de verdade. Então, por exemplo, eu trabalho hoje com a AWS e eu tenho lá um SQS criado, um sistema de fila criado lá na AWS. Legal, bacana. Eu poderia entrar na

04:11.240000000000009

console da AWS e criar? Poderia? Poderia. Não posso falar que não, poderia, mas

04:17.879999999999995

dentro da cultura DevOps, se eu fizer isso, eu estou, digamos que, quebrando um

04:23.399999999999977

pouco a regra, porque eu não tenho uma fonte de verdade. O que eu tenho é, eu entrei no

04:29.720000000000027

console da AWS e criei esse recurso. Alguém da minha equipe também pode ir lá e

04:35.160000000000025

alterar esse recurso ou criar um recurso duplicado, porque não tem visibilidade do

04:39.60000000000002

que já existe lá. Até aí, era muito comum que isso de acontecer, digamos assim.

04:47.24000000000001

Só que é justamente esse o problema, porque a gente não tem a fonte única da

04:51.31999999999999

verdade, que é ali o GitOps. Então, você consegue unir a parte operacional com o

04:57.079999999999984

Git. Então, os recursos que você tem em nuvem, eles ficam mapeados no seu

05:2.8799999999999955

mecanismo ali de SPM, lá no seu Git, no seu GitHub, no seu Bitbucket e assim por

05:8.160000000000025

diante.