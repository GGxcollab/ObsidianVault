O objetivo desta sala é apresentar aos usuários conceitos básicos de criptografia, tais como:

- Criptografia simétrica, como AES
- Criptografia assimétrica, como RSA
- Troca de chaves Diffie-Hellman
- Hashing
- PKI

Imagine que você queira enviar uma mensagem que ninguém, exceto o destinatário pretendido, consiga entender. Como você faria isso?

![Documento ultrassecreto com as palavras WUB KDFN PH](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/a31ad9ee6b4e321453508e8662fc4679.png)  

Uma das cifras mais simples é a cifra de César, usada há mais de 2000 anos. A cifra de César desloca a letra um número fixo de posições para a esquerda ou para a direita. Considere o caso de um deslocamento de 3 posições para a direita para criptografar, como mostrado na figura abaixo.

![Ilustração da criptografia da cifra de César](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/b4f1cbf444e5f19f855dadb7f272ab50.png)  

O destinatário precisa saber que o texto foi deslocado 3 posições para a direita para recuperar a mensagem original.

![Ilustração da decifração da cifra de César](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/45b482f79ebcc2f202813a5d7de4df87.png)  

Usando a mesma chave para criptografar “TRY HACK ME”, obtemos “WUB KDFN PH”.

A Cifra de César que descrevemos acima pode usar uma chave entre 1 e 25. Com uma chave de 1, cada letra é deslocada uma posição, onde A se torna B e Z se torna A. Com uma chave de 25, cada letra é deslocada 25 posições, onde A se torna Z e B se torna A. Uma chave de 0 significa nenhuma alteração; além disso, uma chave de 26 também não resultará em nenhuma alteração, pois levaria a uma rotação completa. Consequentemente, concluímos que a Cifra de César tem um espaço de chaves de 25; existem 25 chaves diferentes que o usuário pode escolher.

Considere o caso em que você interceptou uma mensagem criptografada usando a Cifra de César: “YMNX NX FQUMF GWFAT HTSYFHYNSL YFSLT MTYJQ RNPJ”. É solicitado que a decifremos sem conhecer a chave. Podemos tentar isso usando força bruta, ou seja, podemos testar todas as chaves possíveis e ver qual faz mais sentido. Na figura a seguir, notamos que a chave 5 faz mais sentido: “THIS IS ALPHA BRAVO CONTACTING TANGO HOTEL MIKE”.

![Decifrar um texto cifrado tentando todas as chaves possíveis, ou seja, por força bruta.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/83c79636b07babb43ffe5402e2697772.png)  

A cifra de César é considerada uma **cifra de substituição** porque cada letra do alfabeto é substituída por outra.

Outro tipo de cifra é a **cifra de transposição** , que criptografa a mensagem alterando a ordem das letras. Consideremos uma cifra de transposição simples na figura abaixo. Começamos com a mensagem “THIS IS ALPHA BRAVO CONTACTING TANGO HOTEL MIKE” e a chave `42351`. Depois de escrevermos as letras da nossa mensagem preenchendo uma coluna após a outra, reorganizamos as colunas com base na chave e, em seguida, lemos as linhas. Em outras palavras, escrevemos por colunas e lemos por linhas. Observe também que ignoramos todos os espaços no texto original neste exemplo. O texto cifrado resultante “NPCOTGHOTH…” é lido linha após linha. Ou seja, uma cifra de transposição simplesmente reorganiza a ordem das letras, diferentemente da cifra de substituição, que substitui as letras sem alterar sua ordem.

![Ilustração de uma cifra de transposição](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/d1c99f9bf3e305eb4b50cb8c30be430d.png)  

Esta tarefa introduziu cifras simples de substituição e transposição e as aplicou a mensagens compostas por caracteres alfabéticos. Para que um algoritmo de criptografia seja considerado **seguro** , deve ser inviável recuperar a mensagem original, ou seja, o texto plano. (Em termos matemáticos, precisamos de um problema **difícil** , isto é, um problema que não pode ser resolvido em tempo polinomial. Um problema que podemos resolver em tempo polinomial é um problema viável mesmo para entradas grandes, embora possa levar bastante tempo para o computador concluir.)

Se a mensagem criptografada puder ser quebrada em uma semana, a criptografia utilizada será considerada insegura. No entanto, se a mensagem criptografada puder ser quebrada em 1 milhão de anos, a criptografia será considerada praticamente segura.

Considere a cifra de substituição monoalfabética, onde cada letra é associada a uma nova letra. Por exemplo, em inglês, você associaria "a" a uma das 26 letras do alfabeto, depois associaria "b" a uma das 25 letras restantes, e então associaria "c" a uma das 24 letras restantes, e assim por diante.

Por exemplo, podemos escolher as letras do alfabeto “abcdefghijklmnopqrstuvwxyz” para serem mapeadas para “xpatvrzyjhecsdikbfwunqgmol”, respectivamente. Em outras palavras, “a” se torna “x”, “b” se torna “p” e assim por diante. O destinatário precisa saber a chave, “xpatvrzyjhecsdikbfwunqgmol”, para descriptografar as mensagens criptografadas com sucesso.

Este algoritmo pode parecer muito seguro, especialmente porque testar todas as chaves possíveis não é viável. No entanto, diferentes técnicas podem ser usadas para quebrar um texto cifrado usando um algoritmo de criptografia como esse. Uma das fraquezas desse algoritmo é a frequência das letras. Em textos em inglês, as letras mais comuns são 'e', ​​'t' e 'a', aparecendo com uma frequência de 13%, 9,1% e 8,2%, respectivamente. Além disso, em textos em inglês, as letras iniciais mais comuns são 't', 'a' e 'o', aparecendo em 16%, 11,7% e 7,6% das vezes, respectivamente. Some-se a isso o fato de que a maioria das palavras da mensagem são palavras do dicionário, e será possível quebrar um texto criptografado com a cifra de substituição alfabética em pouco tempo.

Na verdade, não precisamos usar a chave de criptografia para decifrar o texto cifrado recebido, “Uyv sxd gyi siqvw x sinduxjd pvzjdw po axffojdz xgxo wsxcc wuidvw”. Como mostrado na figura abaixo, usando um site como [o quipqiup](https://www.quipqiup.com/) , leva apenas um instante para descobrir que o texto original era “The man who moves a mountain starts by carrying away small stones” (O homem que move uma montanha começa carregando pequenas pedras). Este exemplo indica claramente que este algoritmo está comprometido e não deve ser usado para comunicação confidencial.

![Captura de tela do site quipquip](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/0b4ac26e6f49c1156b6dc5c283b413a7.png)

