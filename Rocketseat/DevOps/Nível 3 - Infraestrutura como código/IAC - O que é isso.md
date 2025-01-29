# Infra As Code - Aula 1
- Declaração de todos os recursos via código
- Facilita a manutenibilidade de toda a infraestrutura
- Automatiza todo o fluxo de criação, edição e remoção de um recurso
- Traz visibilidade do que ta sendo usado
# GitOps
- Incorporar fluxos SCM no contexto operacional
	- basicamente a ideia aqui é incorporar fluxos SCM, fluxos Git, então o commit, por exemplo, um push, políticas de pull request, branch policy, por exemplo, em um repositório que vai cuidar da nossa infraestrutura. Então basicamente a gente tem esses fluxos no contexto operacional.
	- Lembrando que operacional aqui seria de fato a criação de recursos ali na nossa infraestrutura.
- Evita o famoso "Só vou alterar no console"
- Proporciona uma fonte única da verdade
	- Então qual recurso nós temos hoje na AWS, por exemplo? Bastaria ir lá no nosso repositório que cuida disso, ou nos nossos repositórios, eu posso ter vários repositórios, e checar por ali, por exemplo. Então eu sei que o que está ali, o estado que está no meu repositório reflete o que está na minha nuvem e eu consigo, por exemplo, acompanhar a parte de deploy, a parte ali do push, a parte ali de fazer um merge, um pull request e tudo mais, tudo ali pelo Git
- Controle de versão de todo fluxo
	- Também proporciona versionamento, isso também é muito legal, então a gente consegue versionar a nossa infraestrutura


# Overview - Aula 2

![[Pasted image 20250128214533.png]]


# Declarativo vs. Imperativo
## Modelo Declarativo ("O que precisa fazer?!")
- Define o estado desejado
	- Basicamente, se a gente for pensar em programação, a linguagem resolve. Então a gente tem o estado representado do recurso e a gente quer que esse mesmo estado representado esteja presente na nossa nuvem ou em algum lugar
- Engloba todos os recursos do fluxo
- Mantém estados passados no histórico
- Facilita possíveis deleções futuras
## Modelo Imperativo ("Como fazer")
- Define os comandos para criar o recurso
- Necessário execução em ordem
- Em alguns casos é possível manter o histórico do que foi feito

# Ferramentas
- AWS e CloudFormatio
- 