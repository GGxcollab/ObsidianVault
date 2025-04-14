# Ciclo de Desenvolvimento de Software Seguro (SSDLC)
- ![[Pasted image 20250409122212.png]]
- ![[Pasted image 20250409122758.png]]
- OWASP Top 10
# O que é DevOps?
- o DevOps, junto com a metodologia ágil, que é você ter o conceito ali de Sprint e quebrar ali suas funcionalidades em tarefas menores, colocando ali datas específicas, você começou a ter a ideia do DevOps, que é uma ideia de você trazer automação e agilidade ali para o seu modelo ágil.
- Então, dentro dessas automações, a gente começou a ter testes integrados. Durante aquela sprint.
- Então, se você tá desenvolvendo, você tem um programador um, dois e três. Se vocês estão fazendo essas funcionalidades, por exemplo. Como eu comentei sobre você criar o login, o outro fazer uma alteração de cadastro, por exemplo, um produto.
- Durante aquela sprint, naquele tempo de duas semanas mais ou menos, vocês todos testaram essa e essas funcionalidades através de uma esteira que é a Pipeline, onde passariam por alguns testes.
- Um desses testes poderia ser, por exemplo, o teste do teste unitário para ver se não quebrou ali a sua aplicação. Pode ser teste de comportamento para o BDD, que é através da interface da aplicação ou até mesmo teste com Keeway ou testes de segurança, mas você quebra isso em Sprint em partes menores e você descobre de forma muito mais rápida e ao mesmo tempo que você consegue validar se aquela sua integra está de acordo que é esperado com o seu cliente ou com PO (Product Owner).
- E é por isso que é importante quebrar sprints pequenas para você ter tempo de desenvolver bem aquela funcionalidade estar na aplicação e depois passar ele pelo ambiente de teste, depois homologação, até mesmo levarem produção. Isso pode ser feito de forma automatizada ou não.
- ![[Pasted image 20250414141138.png]]
- Então, quando a gente pensa em DevOps, pensa muito em automação, em ferramentas. Como já comentei na fase de planejamento gira.
- Quando a gente pensa em Pipeline, quer você ter uma esteira onde você vai realizar esses testes para você trazer a maior qualidade, pensando gente no GitHub action.
- Quando a gente pensa em encapsular uma aplicação, fazer o build dessa aplicação, a gente pensa no Docker, pode pensar no meio. Você pode utilizar para aplicações Java.
- Se a gente vai fazer deploy, a gente pensa em ferramentas voltadas para nuvem e que através dessas automações a gente tem ali os conceitos para trazer maior qualidade.
- Então DevOps está muito ligado a você trazer qualidade para a aplicação para o seu software em um tempo menor. Através dessas sprites a gente tem ideia do que é esse dia.
- Então, o que seria então a integração contínua (CI)?
	- Então, se a gente está passando de um ambiente de build para teste, a gente vai realizar testes integrados numa pipeline.
	- A gente pode usar isso através de testes unitários, pode usar isso através de Selenium.
	- Por exemplo, um teste de comportamento de vdd.

Então com a gente pensa em testes de integração.

São testes que a gente utiliza ali do build para o teste, para fase de teste e já na fase de seed