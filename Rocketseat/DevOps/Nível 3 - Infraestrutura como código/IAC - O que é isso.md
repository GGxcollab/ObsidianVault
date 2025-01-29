# Infra As Code
- Declaração de todos os recursos via código
- Facilita a manutenibilidade de toda a infraestrutura
- Automatiza todo o fluxo de criação, edição e remoção de um recurso
- Traz visibilidade do que ta sendo usado
# GitOps
- Incorporar fluxos SCM no contexto operacional
	- basicamente a ideia aqui é incorporar fluxos FCM, fluxos Git, então o commit, por exemplo, um push, políticas de pull request, branch policy, por exemplo, em um repositório que vai cuidar da nossa infraestrutura. Então basicamente a gente tem esses fluxos no contexto operacional.
	- Lembrando que operacional aqui seria de fato a criação de recursos ali na nossa infraestrutura.
- Evita o famoso "Só vou alterar no console"
- Proporciona uma fonte única da verdade
- 