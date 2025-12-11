Aprendemos que a tríade de segurança é representada por Confidencialidade, Integridade e Disponibilidade ( CIA ). Pode-se perguntar: como podemos criar um sistema que garanta uma ou mais funções de segurança? A resposta está no uso de modelos de segurança. Nesta tarefa, apresentaremos três modelos de segurança fundamentais:

- Modelo Bell-LaPadula
- O Modelo de Integridade Biba
- O Modelo Clark-Wilson
### Modelo Bell-LaPadula

O Modelo Bell-LaPadula visa alcançar **a confidencialidade** especificando três regras:

- **Propriedade de segurança simples** : Essa propriedade é conhecida como "sem leitura ascendente"; ela estabelece que um sujeito com um nível de segurança inferior não pode ler um objeto com um nível de segurança superior. Essa regra impede o acesso a informações confidenciais acima do nível autorizado.
- **Propriedade de Segurança Estrela** : Esta propriedade é conhecida como "não escrever"; ela estabelece que um sujeito com um nível de segurança superior não pode escrever em um objeto com um nível de segurança inferior. Esta regra impede a divulgação de informações confidenciais a um sujeito com um nível de segurança inferior.
- **Propriedade de Segurança Discricionária** : Esta propriedade utiliza uma matriz de acesso para permitir operações de leitura e escrita. Um exemplo de matriz de acesso é mostrado na tabela abaixo e utilizado em conjunto com as duas primeiras propriedades.

|Assuntos|Objeto A|Objeto B|
|---|---|---|
|Assunto 1|Escrever|Sem acesso|
|Assunto 2|Ler/Escrever|Ler|

As duas primeiras propriedades podem ser resumidas como "redigir para cima, ler para baixo". Você pode compartilhar informações confidenciais com pessoas com nível de segurança mais alto (redigir para cima) e pode receber informações confidenciais de pessoas com nível de segurança mais baixo (ler para baixo).

O modelo Bell-LaPadula apresenta algumas limitações. Por exemplo, ele não foi projetado para lidar com o compartilhamento de arquivos.

### Modelo Biba

O Modelo Biba visa alcançar **a integridade** especificando duas regras principais:

- **Propriedade de Integridade Simples** : Esta propriedade é conhecida como "sem leitura descendente"; um sujeito de integridade mais alta não deve ler de um objeto de integridade mais baixa.
- **Propriedade de integridade Star** : Esta propriedade é conhecida como "sem escrita"; um sujeito de integridade inferior não deve escrever em um objeto de integridade superior.

Essas duas propriedades podem ser resumidas como "leia, anote". Essa regra contrasta com o Modelo Bell-LaPadula, o que não deve ser surpreendente, já que um se preocupa com a confidencialidade enquanto o outro se preocupa com a integridade.

O modelo Biba apresenta diversas limitações. Um exemplo é que ele não lida com ameaças internas (ameaças internas).

### Modelo de Clark-Wilson

O Modelo Clark-Wilson também visa alcançar a integridade através da utilização dos seguintes conceitos:

- **Item de Dados Restrito (CDI)** : Refere-se ao tipo de dados cuja integridade desejamos preservar.
- **Item de Dados Não Restrito (UDI)** : Refere-se a todos os tipos de dados além do CDI, como entrada do usuário e do sistema.
- **Procedimentos de Transformação (PTs)** : Esses procedimentos são operações programadas, como leitura e gravação, e devem manter a integridade dos CDIs.
- **Procedimentos de Verificação de Integridade (PVI)** : Esses procedimentos verificam e garantem a validade dos CDIs.

Abordamos apenas três modelos de segurança. O leitor pode explorar muitos outros modelos de segurança. Alguns exemplos incluem:

- Modelo Brewer e Nash
- Modelo Goguen-Meseguer
- Modelo de Sutherland
- Modelo de Graham-Denning
- Modelo Harrison-Ruzzo-Ullman