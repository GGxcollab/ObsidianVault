
---

### 🛡️ O que é CORS?

**CORS** significa **Cross-Origin Resource Sharing**. É um mecanismo de segurança implementado pelos navegadores para controlar quais origens (domínios) podem acessar recursos de uma API.

#### Exemplo de problema:

Imagine que sua API está em `https://api.meuservico.com`, e um frontend em `https://meusite.com` quer consumir essa API. Se o navegador detectar que essas origens são diferentes, ele vai bloquear a requisição **a menos que sua API permita explicitamente essa origem**.

#### Como resolver no FastAPI:

Você pode usar o middleware `CORSMiddleware` para configurar isso:

````
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://meusite.com"],  # ou ["*"] para permitir todas
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
````

---

### ⚙️ O que é um Middleware?

Um **middleware** é uma função que intercepta a requisição **antes** de ela chegar ao endpoint ou **depois** que a resposta é gerada. Ele pode ser usado para:

- Autenticação
- Log de requisições
- Manipulação de headers
- Controle de acesso
- Compressão de resposta
- CORS (como vimos acima)

#### Exemplo de middleware personalizado no FastAPI:

````
from fastapi import Request
from fastapi.responses import JSONResponse

@app.middleware("http")
async def log_requests(request: Request, call_next):
    print(f"Recebendo requisição: {request.method} {request.url}")
    response = await call_next(request)
    print(f"Resposta com status: {response.status_code}")
    return response
````

Esse middleware loga cada requisição e resposta, útil para debug ou auditoria.

---

### Resumo:

| Conceito       | Função                                                             |
| -------------- | ------------------------------------------------------------------ |
| **CORS**       | Permite ou bloqueia requisições de outras origens (domínios)       |
| **Middleware** | Intercepta requisições/respostas para aplicar lógica personalizada |

---