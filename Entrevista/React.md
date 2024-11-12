# O que é?
- O React é uma biblioteca para criação de interface de usuário.
- Presentes em grandes projetos, como: Facebook, Whatsapp, Twitter, Yahoo e Netflix.
- É uma das principais ferramentas para desenvolvimento Front-end
- Ele permite compor UIs completas a partir de pequenos e isolados códigos, que é mais conhecido como **componentes**
- É flexivel, ou sejja, é possível usar o react em uma pequena parte de um site com alguma linhas de código e nenhuma ferramenta de **Build** ou em projetos mais completos como uma single-page-app, que nesse caso sim, utiliza outras ferramentas que facilitam e agilizam o trabalho dos desenvolvedores
# Setup Básico
- é necessario a importação de duas libs: React DOM (faz a ligação do react com os elementos da página) e o React
	- ![[Pasted image 20241112151809.png]]
- **Babel** é um compilador em JavaScript, ele basicamente permite que use funcionalidades modernas da linguagem que podem ainda nao serem suportados por todos os navegadores 
	- Em resumo, o Babel transforma o Js em Js, mais precisamente um Js que possa ser interpretado pela maioria dos navegadores
- **Virtual DOM** é uma representação dos elementos do DOM que ficam salvos na memória
	- ![[Pasted image 20241112152357.png]]
- Exemplo:
	- ![[Pasted image 20241112152613.png]]
- **JSX** (JavaScriptXML) permiti a utilização de sintaxe similar a do HTML no momento da criação de elementos para o React, deixando esse processo muito mais amigavel na hora da criação.
- O **Babel** vai por trás das cortinas transformar a sintaxe do **JSX** em funções JavaScript, assim como no exemplo dado acima.
- Exemplo usando **JSX**:
	- ![[Pasted image 20241112153217.png]]
- O JSX é o caminho mais comum usado pelos desenvolvedores, porem não é obrigatorio a adoção dele
# Compone