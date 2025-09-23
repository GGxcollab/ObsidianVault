# Perguntas e Respostas para Entrevista de Analista Júnior em Python

---

## 📌 Conceitos Básicos de Python

### 1. O que é uma variável?

**Resposta:** É um espaço na memória que recebe um nome e serve para armazenar valores que podem ser usados e alterados durante o programa.

Exemplo:

```python
idade = 25
nome = "Ana"
altura = 1.70
```

---

### 2. O que é uma variável de ambiente?

**Resposta:** É uma configuração do sistema (par chave=valor) que pode ser acessada por programas. São usadas para armazenar dados sensíveis (como senhas e chaves de API) e para configurar diferentes ambientes (dev, teste, produção).

Exemplo em Python:

```python
import os
api_key = os.getenv("API_KEY")
```

---

### 3. Qual a diferença entre uma lista e uma tupla em Python?

**Resposta:**

- **Lista:** mutável, pode ter elementos alterados, adicionados ou removidos.
    
- **Tupla:** imutável, não pode ser alterada depois de criada.
    

---

### 4. O que é uma classe e um objeto em Python?

**Resposta:**

- **Classe:** é um modelo que define atributos e métodos.
    
- **Objeto:** é uma instância de uma classe.
    

Exemplo:

```python
class Pessoa:
    def __init__(self, nome):
        self.nome = nome

p1 = Pessoa("Ana")  # p1 é um objeto da classe Pessoa
```

---

### 5. O que é um container?

**Resposta:**

- Em **Python**: é uma estrutura de dados que guarda outros objetos, como `list`, `tuple`, `dict` e `set`.
    
- Em **infraestrutura**: é uma forma de empacotar aplicações e dependências em um ambiente isolado (ex.: Docker).
    

---

### 6. O que é um ambiente virtual e qual a importância dele?

**Resposta:**  
Um **ambiente virtual** é um espaço isolado dentro do sistema onde você instala pacotes e dependências do Python sem afetar a instalação global da máquina.

**Importância:**

- Isolamento de dependências entre projetos.
    
- Reprodutibilidade de ambientes (ex.: `requirements.txt`).
    
- Segurança, mantendo pacotes restritos ao projeto.
    
- É considerado boa prática em qualquer projeto Python.
    

Exemplo:

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
deactivate                # sair
```

---

## 📌 Perguntas sobre Boas Práticas e Segurança

### 7. Se você precisa receber a senha de um usuário em Python, o que faria para garantir que essa senha não fique exposta?

**Resposta:** Usar `getpass.getpass()` para não exibir no terminal e evitar deixar credenciais no código (usar variáveis de ambiente).

---

### 8. Se você tem uma função que recebe entrada de usuário, como trataria para evitar problemas de segurança?

**Resposta:**

- Validar e sanitizar a entrada (ex.: `strip()`, checar tipo com `isalpha`, `isdigit`).
    
- Evitar executar diretamente entradas do usuário (`eval`, `exec`).
    

---

## 📌 Perguntas sobre Pandas

### 9. O que é o pandas e para que serve?

**Resposta:** É uma biblioteca Python usada para manipulação e análise de dados, especialmente dados tabulares.

---

### 10. Qual a diferença entre um Series e um DataFrame no pandas?

**Resposta:**

- **Series:** é uma estrutura unidimensional (como uma coluna).
    
- **DataFrame:** é uma estrutura bidimensional (como uma tabela).
    

---

### 11. Como você lê um arquivo CSV usando pandas?

**Resposta:**

```python
import pandas as pd
df = pd.read_csv("arquivo.csv")
```

---

### 12. Como exibir apenas as 5 primeiras linhas de um DataFrame?

**Resposta:**

```python
df.head()
```

---

### 13. Como selecionar uma coluna específica de um DataFrame?

**Resposta:**

```python
df["coluna"]
```

---

### 14. Como filtrar linhas onde a coluna `idade` seja maior que 18?

**Resposta:**

```python
df[df["idade"] > 18]
```

---

### 15. Como descobrir valores nulos em um DataFrame?

**Resposta:**

```python
df.isnull().sum()
```

---

### 16. Como calcular a média de valores de uma coluna?

**Resposta:**

```python
df["salario"].mean()
```

---

### 17. Como ordenar um DataFrame pela coluna `nome`?

**Resposta:**

```python
df.sort_values("nome", ascending=True)
```

---

### 18. Qual a diferença entre `df.loc` e `df.iloc`?

**Resposta:**

- `loc`: seleciona por rótulo (nome da linha/coluna).
    
- `iloc`: seleciona por índice numérico.
    

---

## 📌 Perguntas sobre Selenium

### 19. O que é o Selenium e para que serve?

**Resposta:** É uma ferramenta usada para automação de navegadores, muito utilizada em testes automatizados e scraping de páginas dinâmicas.

---

### 20. Como iniciar um navegador com Selenium no Python?

**Resposta:**

```python
from selenium import webdriver

navegador = webdriver.Chrome()
navegador.get("https://google.com")
```

---

### 21. Qual a diferença entre `find_element` e `find_elements`?

**Resposta:**

- `find_element`: retorna o **primeiro elemento** encontrado.
    
- `find_elements`: retorna uma **lista de elementos**.
    

---

### 22. Quais as formas de localizar elementos no Selenium?

**Resposta:** ID, Name, Class Name, Tag Name, Link Text, Partial Link Text, CSS Selector, XPath.

---

### 23. Como clicar em um botão com Selenium?

**Resposta:**

```python
driver.find_element("id", "meu_botao").click()
```

---

### 24. Como digitar um texto em um input?

**Resposta:**

```python
driver.find_element("name", "usuario").send_keys("teste123")
```

---

### 25. Como esperar um elemento aparecer antes de interagir?

**Resposta:**

```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

elemento = WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.ID, "meu_id"))
)
```

---

### 26. Como tirar um print da tela com Selenium?

**Resposta:**

```python
driver.save_screenshot("print.png")
```

---

### 27. Qual a diferença entre Selenium e BeautifulSoup?

**Resposta:**

- Selenium: interage com o navegador (executa JavaScript).
    
- BeautifulSoup: apenas analisa HTML estático.
    

---

### 28. Quais cuidados de segurança ao usar Selenium?

**Resposta:**

- Não expor credenciais no código (usar variáveis de ambiente).
    
- Usar perfis temporários.
    
- Limpar cookies e sessões.
    
- Respeitar limites de acesso para evitar bloqueios.
    

---

📑 **Esse documento pode ser usado como guia de perguntas e respostas em entrevistas para avaliar candidatos a analista júnior em Python, cobrindo lógica de programação, boas práticas de segurança, ambientes virtuais, pandas e Selenium.**

###  **Pergunta prática com foco em segurança**

**"Imagine que você precisa receber dados de um usuário via uma API em Flask. Quais cuidados você tomaria para garantir que esses dados não comprometam a segurança da aplicação?"**

**O que observar:**

- Se menciona validação e sanitização de entrada.
- Se conhece práticas como uso de `request.get_json()` com verificação de tipos.
- Se tem noção de riscos como **injeção de código**, **XSS**, ou **CSRF**.
- Se fala sobre uso de bibliotecas como `pydantic` ou `marshmallow` para validação.

---

### **3. Pergunta sobre boas práticas de código seguro**

**"Você já ouviu falar sobre o princípio do menor privilégio? Como ele se aplica ao desenvolvimento de software em Python?"**

**O que observar:**

- Se entende que o princípio do menor privilégio significa conceder apenas as permissões necessárias.
- Se consegue aplicar isso a exemplos como controle de acesso a arquivos, uso de variáveis de ambiente, ou configuração de permissões em APIs.
- Se demonstra preocupação com segurança desde o design do código.