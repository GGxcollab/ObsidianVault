![Triângulo da CIA](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/58a85d2e5942ebf3e78eb01c82f563be.png)

Antes de podermos descrever algo como _seguro_ , precisamos considerar melhor o que constitui a segurança. Quando você deseja avaliar a segurança de um sistema, precisa pensar em termos da tríade da segurança: confidencialidade, integridade e disponibilidade ( CIA ).

- **A confidencialidade** garante que apenas as pessoas ou destinatários pretendidos possam acessar os dados.
- **A integridade** visa garantir que os dados não possam ser alterados; além disso, podemos detectar qualquer alteração caso ela ocorra.
- **A disponibilidade** visa garantir que o sistema ou serviço esteja disponível quando necessário.

![Um vendedor com um recibo, adicionando um zero ao preço de um item depois que um comprador o escolhe, multiplicando assim o preço por dez.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/6b93d35050cea9dc51b700855677edf4.png)

Vamos considerar a tríade de segurança da CIA no caso de fazer um pedido de compras online:

- **Confidencialidade** : Ao fazer compras online, você espera que o número do seu cartão de crédito seja divulgado apenas para a entidade que processa o pagamento. Se você duvidar que as informações do seu cartão de crédito serão divulgadas a terceiros não confiáveis, provavelmente evitará concluir a transação. Além disso, se uma violação de dados resultar na divulgação de informações pessoais, incluindo dados de cartões de crédito, a empresa sofrerá enormes prejuízos em diversos níveis.
- **Integridade** : Após concluir seu pedido, se um intruso conseguir alterar o endereço de entrega fornecido, o pacote será enviado para outra pessoa. Sem a integridade dos dados, você pode ficar bastante relutante em fazer seu pedido com este vendedor.
- **Disponibilidade** : Para fazer seu pedido online, você poderá acessar o site da loja ou usar o aplicativo oficial. Caso o serviço esteja indisponível, você não poderá navegar pelos produtos nem fazer um pedido. Se continuar enfrentando esses problemas técnicos, você poderá desistir e começar a procurar outra loja online.

Vamos analisar a CIA (Acordo de Integridade Corporativa) em relação aos registros de pacientes e sistemas correlatos:

- **Confidencialidade** : De acordo com diversas leis em países modernos, os profissionais de saúde devem garantir e manter a confidencialidade dos registros médicos. Consequentemente, os profissionais de saúde podem ser responsabilizados legalmente caso divulguem ilegalmente os registros médicos de seus pacientes.
- **Integridade** : Se o registro de um paciente for alterado acidentalmente ou maliciosamente, isso pode levar à administração de um tratamento incorreto, o que, por sua vez, pode resultar em uma situação de risco de vida. Portanto, o sistema seria inútil e potencialmente prejudicial sem garantir a integridade dos registros médicos.
- **Disponibilidade** : Quando um paciente visita uma clínica para acompanhamento de sua condição médica, o sistema deve estar disponível. Um sistema indisponível significa que o profissional de saúde não poderá acessar o prontuário do paciente e, consequentemente, não saberá se os sintomas atuais estão relacionados ao histórico médico do paciente. Essa situação pode tornar o diagnóstico médico mais complexo e propenso a erros.

A ênfase não precisa ser a mesma em todas as três funções de segurança. Um exemplo seria um comunicado universitário; embora geralmente não seja confidencial, a integridade do documento é fundamental.

### Além da CIA

![Um entregador com uma quantidade absurda de caixas de pizza e um homem na porta dizendo: "Eu não pedi isso".](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/aaeda28067dbaa5573f640e467be7834.png)

Indo um passo além da tríade de segurança da CIA , podemos pensar em:

- **Autenticidade** : Autêntico significa não fraudulento ou falsificado. Autenticidade significa garantir que o documento/arquivo/dado seja proveniente da fonte declarada.
- **Não repúdio** : Repudiar significa recusar-se a reconhecer a validade de algo. O não repúdio garante que a fonte original não possa negar ser a origem de um determinado documento/arquivo/dado. Essa característica é indispensável em diversas áreas, como compras, diagnóstico de pacientes e serviços bancários.

Esses dois requisitos estão intimamente relacionados. A necessidade de distinguir arquivos ou pedidos autênticos de falsos é indispensável. Além disso, garantir que a outra parte não possa negar ser a fonte é vital para a usabilidade de muitos sistemas.

No comércio eletrônico, dependendo do seu negócio, você pode tolerar tentar entregar uma camiseta com pagamento na entrega e descobrir depois que o destinatário nunca fez tal pedido. No entanto, nenhuma empresa pode tolerar enviar 1000 carros para descobrir que o pedido é falso. No caso de um pedido de compra online, você quer confirmar que o cliente em questão realmente fez o pedido; isso é autenticidade. Além disso, você quer garantir que ele não possa negar ter feito o pedido; isso é não-repúdio.

Como empresa, ao receber um pedido de 1000 carros, é fundamental garantir a autenticidade do pedido; além disso, a fonte não deve poder negar ter feito tal encomenda. Sem autenticidade e garantia de não repúdio, o negócio não pode ser realizado.

### Parkerian Hexad

Em 1998, Donn Parker propôs a Hexade Parkeriana, um conjunto de seis elementos de segurança. São eles:

1. Disponibilidade
2. Utilidade
3. Integridade
4. Autenticidade
5. Confidencialidade
6. Posse

Já abordamos quatro dos seis elementos acima. Vamos discutir os dois elementos restantes:

- **Utilidade** : A utilidade se concentra na aplicabilidade da informação. Por exemplo, um usuário pode ter perdido a chave de descriptografia para acessar um laptop com armazenamento criptografado. Embora o usuário ainda tenha o laptop com seus discos intactos, ele não consegue acessá-los. Em outras palavras, embora ainda disponível, a informação está em um formato que não é útil, ou seja, não tem utilidade prática.
- **Posse** : Este elemento de segurança exige que protejamos as informações contra apropriação, cópia ou controle não autorizados. Por exemplo, um adversário pode se apropriar de um disco rígido de backup, o que significa que perdemos a posse das informações enquanto ele estiver com o disco. Alternativamente, o adversário pode conseguir criptografar nossos dados usando ransomware; isso também leva à perda da posse dos dados.