# O que é?
- O React é uma biblioteca para criação de interface de usuário.
- Presentes em grandes projetos, como: Facebook, Whatsapp, Twitter, Yahoo e Netflix.
- É uma das principais ferramentas para desenvolvimento Front-end
- Ele permite compor UIs completas a partir de pequenos e isolados códigos, que é mais conhecido como **componentes**
- É flexivel, ou sejja, é possível usar o react em uma pequena parte de um site com alguma linhas de código e nenhuma ferramenta de **Build** ou em projetos mais completos como uma single-page-app, que nesse caso sim, utiliza outras ferramentas que facilitam e agilizam o trabalho dos desenvolvedores
# Setup Básico
- é necessario a importação de duas libs: React DOM (faz a ligação do react com os elementos da página) e o React
	- ![[Pasted image 20241112151809 1.png]]
- **Babel** é um compilador em JavaScript, ele basicamente permite que use funcionalidades modernas da linguagem que podem ainda nao serem suportados por todos os navegadores 
	- Em resumo, o Babel transforma o Js em Js, mais precisamente um Js que possa ser interpretado pela maioria dos navegadores
- **Virtual DOM** é uma representação dos elementos do DOM que ficam salvos na memória
	- ![[Pasted image 20241112152357 1.png]]
- Exemplo:
	- ![[Pasted image 20241112152613 1.png]]
- **JSX** (JavaScriptXML) permiti a utilização de sintaxe similar a do HTML no momento da criação de elementos para o React, deixando esse processo muito mais amigavel na hora da criação.
- O **Babel** vai por trás das cortinas transformar a sintaxe do **JSX** em funções JavaScript, assim como no exemplo dado acima.
- Exemplo usando **JSX**:
	- ![[Pasted image 20241112153217 1.png]]
- O JSX é o caminho mais comum usado pelos desenvolvedores, porem não é obrigatorio a adoção dele
# Componentização
- é um dos principais pilares na utilização do React para dividir as aplicações em partes independentes, isolados e reutilizáveis
- Um componente pode ser representado por uma simples função JavaScript desde que atenda a dois requisitos:
	- Aceitar um parametro e propriedade (properties)
	- E retornar um React Element que é basicamente o JSX
- Exemplo de criação de um componente:
	- ![[Pasted image 20241112160418 1.png]]
	- Agora a versão de componentes usando classes:
	- ![[Pasted image 20241112160510 1.png]]
- **Diferença entre componentes criados por Funções ou Classes**
	- Antes da Versão 16.8, a criação usando funções possui restrições, como por exemplo sem acesso ao Estado e Hooks, so que a partir dessa versão essas funcionalidades foram adicionados esses componentes 
	- Sendo assim, hoje em dia a criaçãovai muito do gosto do desenvolvedor
# Libs mais usadas para compor o React
- As vezes é necessário a adição de outras libs para adicionar outras funcionalidades extras a nossa aplicação
- **Libs mais utilizadas:**
	- _redux_: lib para o gerenciamento de status
		- uma aplicação com vários componentes trocando informações entre si acaba se tornando dificil de gerencias, com o redux é uam mao na roda para centralizar o gerenciamento de Estado dos componentes
	- _React Router_: é uma lib para lidar com acesso a rota das aplicações
	- _React Intl_: disponibiliza vários componentes para manusear datas e números 
	- _React DevTools_: é uma extensão do Google Chrome com diversas ferramentas de debug para aplicações em React