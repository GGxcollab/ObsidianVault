# 🔐 Autenticação Azure - Guia Completo

  

## 📊 Cenários de Autenticação

  

### 🎯 O que Você Está Usando AGORA

  

```yaml

# Suas credenciais no .env:

AZURE_TENANT_ID=...

AZURE_CLIENT_ID=...

AZURE_CLIENT_SECRET=...

```

  

**Tipo:** **Service Principal (App Registration)**

  

**O que é:**

- É um "usuário robô" no Azure

- Criado via **Azure App Registration**

- Tem permissões específicas (como ler incidentes do Sentinel)

- Usado para aplicações **server-to-server** (máquina pra máquina)

  

---

  

## 🔑 3 Tipos de Autenticação Azure

  

### 1️⃣ **Service Principal** (O que você USA)

  

```

┌─────────────────────────────────────────────────┐

│  Sua Aplicação (API)                            │

│  ├── CLIENT_ID + CLIENT_SECRET                  │

│  └── Autentica automaticamente                  │

└───────────────────┬─────────────────────────────┘

                    │

                    ▼

┌─────────────────────────────────────────────────┐

│  Azure AD                                       │

│  └─> Gera token de acesso                      │

└───────────────────┬─────────────────────────────┘

                    │

                    ▼

┌─────────────────────────────────────────────────┐

│  Microsoft Sentinel                             │

│  └─> Retorna dados dos incidentes              │

└─────────────────────────────────────────────────┘

```

  

**Quando Usar:**

- ✅ **APIs backend** que rodam sozinhas

- ✅ **Scheduled tasks** (seu caso!)

- ✅ **Scripts automatizados**

- ✅ **Integrações server-to-server**

  

**Vantagens:**

- ✅ Não precisa de usuário logado

- ✅ Funciona 24/7 automaticamente

- ✅ Ideal para sincronização automática

- ✅ Mais simples de implementar

  

**Desvantagens:**

- ❌ Credenciais fixas (se vazarem, problema!)

- ❌ Sem contexto de usuário

- ❌ Todas operações em nome do app

  

**Seu Caso:**

```python

# app/services/sentinel_service.py

def gera_token(self) -> str:

    """Gera token com CLIENT_ID e CLIENT_SECRET"""

    url = f"https://login.microsoftonline.com/{self.tenant_id}/oauth2/v2.0/token"

    data = {

        "client_id": self.app_id,

        "client_secret": self.app_secret,  # ← Service Principal

        "grant_type": "client_credentials"

    }

    # Token gerado automaticamente!

```

  

---

  

### 2️⃣ **User Authentication** (OAuth2 / OpenID Connect)

  

```

┌─────────────────────────────────────────────────┐

│  Usuário no Navegador                           │

│  └─> Clica em "Login com Microsoft"            │

└───────────────────┬─────────────────────────────┘

                    │

                    ▼

┌─────────────────────────────────────────────────┐

│  Azure AD Login Page                            │

│  ├─> Usuário digita email/senha                │

│  └─> Azure valida credenciais                  │

└───────────────────┬─────────────────────────────┘

                    │

                    ▼

┌─────────────────────────────────────────────────┐

│  Azure AD                                       │

│  └─> Redireciona com token                     │

└───────────────────┬─────────────────────────────┘

                    │

                    ▼

┌─────────────────────────────────────────────────┐

│  Sua Aplicação                                  │

│  └─> Recebe token do usuário                   │

│  └─> Acessa recursos em NOME do usuário        │

└─────────────────────────────────────────────────┘

```

  

**Quando Usar:**

- ✅ **Frontend web** (React, Angular, Vue)

- ✅ **Apps mobile** que usuários acessam

- ✅ **Dashboards** com login

- ✅ Quando precisa saber **QUEM** está acessando

  

**Vantagens:**

- ✅ Contexto do usuário (sabe quem fez o quê)

- ✅ Permissões por usuário

- ✅ Mais seguro (sem credenciais no código)

- ✅ SSO (Single Sign-On)

  

**Desvantagens:**

- ❌ Mais complexo de implementar

- ❌ Precisa de usuário interagir

- ❌ Token expira (precisa renovar)

  

**Exemplo de Código:**

```python

from fastapi_azure_auth import SingleTenantAzureAuthorizationCodeBearer

  

# Configuração

azure_scheme = SingleTenantAzureAuthorizationCodeBearer(

    app_client_id="seu-app-id",

    tenant_id="seu-tenant-id",

    scopes=["User.Read"]

)

  

# Proteção de rota

@app.get("/dashboard")

async def dashboard(user = Depends(azure_scheme)):

    # user contém info do usuário logado!

    return {

        "message": f"Bem-vindo, {user.name}!",

        "email": user.email

    }

```

  

---

  

### 3️⃣ **Managed Identity** (Melhor Opção em Produção Azure)

  

```

┌─────────────────────────────────────────────────┐

│  Azure App Service / VM / Container             │

│  ├─> Tem identidade automática                 │

│  └─> SEM necessidade de credenciais!           │

└───────────────────┬─────────────────────────────┘

                    │

                    ▼

┌─────────────────────────────────────────────────┐

│  Azure AD                                       │

│  └─> Valida identidade automaticamente         │

└───────────────────┬─────────────────────────────┘

                    │

                    ▼

┌─────────────────────────────────────────────────┐

│  Microsoft Sentinel                             │

│  └─> Acesso concedido automaticamente          │

└─────────────────────────────────────────────────┘

```

  

**Quando Usar:**

- ✅ **App rodando NO Azure** (App Service, VM, AKS)

- ✅ **Produção** (mais seguro!)

- ✅ Quando não quer expor credenciais

  

**Vantagens:**

- ✅ **ZERO credenciais no código!** 🔥

- ✅ Azure gerencia tudo automaticamente

- ✅ Mais seguro

- ✅ Menos manutenção

  

**Desvantagens:**

- ❌ Só funciona dentro do Azure

- ❌ Não funciona local (dev)

  

**Exemplo de Código:**

```python

from azure.identity import DefaultAzureCredential

  

# Em PRODUÇÃO (Azure):

credential = DefaultAzureCredential()  # ← Automático!

  

# Localmente usa variáveis de ambiente

# No Azure usa Managed Identity

```

  

---

  

## 📊 Comparação Visual

  

| Recurso | Service Principal | User Auth | Managed Identity |

|---------|-------------------|-----------|------------------|

| **Seu Caso Atual** | ✅ SIM | ❌ Não | ❌ Não |

| **Sem usuário** | ✅ | ❌ | ✅ |

| **24/7 automático** | ✅ | ❌ | ✅ |

| **Credenciais no código** | ⚠️ Sim | ❌ | ✅ Não! |

| **Complexidade** | 🟢 Baixa | 🟡 Média | 🟢 Baixa |

| **Segurança** | 🟡 Boa | 🟢 Muito Boa | 🟢 Excelente |

| **Onde funciona** | ✅ Qualquer lugar | ✅ Qualquer lugar | ⚠️ Só no Azure |

  

---

  

## 🎯 Quando Usar Cada Um?

  

### Cenário 1: **API Backend Automática** (SEU CASO)

  

**Situação:**

- Sincronização a cada 6 minutos

- Sem usuários acessando

- Roda em servidor

  

**Recomendação:**

```

Desenvolvimento: Service Principal ✅

Produção (fora Azure): Service Principal ✅

Produção (no Azure): Managed Identity ✅✅✅

```

  

---

  

### Cenário 2: **Dashboard Web com Login**

  

**Situação:**

- Usuários fazem login

- Cada usuário vê seus dados

- Frontend React/Angular

  

**Recomendação:**

```

User Authentication (OAuth2) ✅✅✅

```

  

**Exemplo:**

```typescript

// Frontend React

import { MsalProvider } from "@azure/msal-react";

  

function App() {

  return (

    <MsalProvider instance={msalInstance}>

      <Dashboard />

    </MsalProvider>

  );

}

  

// Usuário clica "Login"

// Redireciona para Microsoft

// Volta com token

// Frontend acessa API

```

  

---

  

### Cenário 3: **API com Frontend + Backend**

  

**Situação:**

- Frontend: Usuários fazem login

- Backend: Precisa acessar Sentinel

  

**Recomendação:**

```

Frontend: User Authentication (OAuth2)

Backend: Managed Identity (se no Azure) ou Service Principal

```

  

**Fluxo:**

```

Usuário login → Token JWT → Frontend

Frontend → Chama Backend (com token)

Backend → Valida token

Backend → Usa Managed Identity para Sentinel

Backend → Retorna dados

```

  

---

  

## 🔐 App Registration - O que é?

  

### O que você JÁ tem (sem saber):

  

```

Azure Portal

  └─> Azure Active Directory

      └─> App Registrations

          └─> "Seu-App-Sentinel" (JÁ EXISTE!)

              ├─> CLIENT_ID ← você usa!

              ├─> TENANT_ID ← você usa!

              └─> Certificates & secrets

                  └─> CLIENT_SECRET ← você usa!

```

  

**App Registration** é onde você:

1. ✅ Cria o "robô" (Service Principal)

2. ✅ Define permissões (ex: ler Sentinel)

3. ✅ Gera CLIENT_SECRET

4. ✅ Configura OAuth (se for usar User Auth)

  

---

  

## 🛠️ Como Criar um App Registration

  

### Passo a Passo (Azure Portal):

  

```bash

1. Azure Portal → Azure Active Directory

2. App registrations → New registration

3. Nome: "Sentinel-Sync-API"

4. Supported account types: Single tenant

5. Register

  

6. Overview → Copie:

   - Application (client) ID

   - Directory (tenant) ID

  

7. Certificates & secrets → New client secret

   - Descrição: "API Secret"

   - Expira em: 24 meses

   - Copie o VALUE (só aparece uma vez!)

  

8. API permissions → Add permission

   - Microsoft Graph ou Azure Service Management

   - Delegated permissions OU Application permissions

   - SecurityEvents.Read.All (exemplo)

   - Grant admin consent

```

  

---

  

## 🚀 Seu Caso: O que Fazer?

  

### Atualmente (Desenvolvimento):

```yaml

✅ Service Principal (App Registration)

✅ Funciona perfeitamente!

✅ Simples e direto

```

  

### Recomendação para Produção:

  

#### Opção A: Produção no Azure (RECOMENDADO)

  

```python

# Mude apenas 1 linha!

# app/services/sentinel_service.py

  

# ANTES (local):

credential = ClientSecretCredential(

    tenant_id=settings.azure_tenant_id,

    client_id=settings.azure_client_id,

    client_secret=settings.azure_client_secret

)

  

# DEPOIS (produção Azure):

from azure.identity import DefaultAzureCredential

credential = DefaultAzureCredential()  # ← Automático!

```

  

**Vantagens:**

- 🔥 ZERO credenciais no código

- 🔥 Azure gerencia tudo

- 🔥 Mais seguro

  

**Configuração no Azure:**

```bash

# 1. Habilite Managed Identity no App Service

az webapp identity assign --name seu-app --resource-group seu-rg

  

# 2. Dê permissões ao Managed Identity

az role assignment create \

  --assignee <managed-identity-id> \

  --role "Azure Sentinel Reader" \

  --scope /subscriptions/.../sentinel

  

# 3. Deploy sem credenciais no .env!

```

  

#### Opção B: Produção Fora do Azure

  

```yaml

✅ Continue com Service Principal

⚠️ Guarde CLIENT_SECRET em:

   - Azure Key Vault

   - AWS Secrets Manager

   - HashiCorp Vault

❌ NUNCA no código ou .env commitado!

```

  

---

  

## 💡 Quando Adicionar User Authentication?

  

### Adicione SE:

  

1. **Dashboard Web**

   - Usuários fazem login

   - Cada um vê seus dados

2. **Auditoria por Usuário**

   - Precisa saber quem fez o quê

3. **Permissões Granulares**

   - Admin vê tudo

   - Analista vê só seu setor

  

### NÃO Adicione SE:

  

1. **Apenas sincronização automática** ← SEU CASO

2. **Sem interface para usuários**

3. **Tudo é backend**

  

---

  

## 📝 Exemplo Prático: Adicionar User Auth

  

Se no futuro você quiser um **dashboard**:

  

```python

# 1. Instale

pip install fastapi-azure-auth

  

# 2. Configure (app/core/azure_auth.py)

from fastapi_azure_auth import SingleTenantAzureAuthorizationCodeBearer

  

azure_scheme = SingleTenantAzureAuthorizationCodeBearer(

    app_client_id=settings.azure_client_id,

    tenant_id=settings.azure_tenant_id,

    scopes={

        "api://sentinel-api/access_as_user": "Access API as user"

    }

)

  

# 3. Proteja rotas

@app.get("/dashboard")

async def dashboard(user = Depends(azure_scheme)):

    return {

        "user": user.name,

        "email": user.email,

        "roles": user.roles

    }

  

# 4. Configure no Azure App Registration:

#    - Redirect URIs: https://seu-app.com/oauth/callback

#    - Enable ID tokens

#    - Add API scope

```

  

---

  

## ✅ Checklist de Decisão

  

### Use **Service Principal** SE:

- [ ] É uma API backend

- [ ] Não tem usuários fazendo login

- [ ] Sincronização automática

- [ ] Scheduled tasks

- [ ] **SEU CASO ATUAL** ✅

  

### Use **User Authentication** SE:

- [ ] Frontend com login

- [ ] Precisa saber QUEM acessa

- [ ] Dashboard/Portal

- [ ] Permissões por usuário

  

### Use **Managed Identity** SE:

- [ ] Rodando no Azure (App Service, VM, AKS)

- [ ] Ambiente de produção

- [ ] Quer máxima segurança

- [ ] **UPGRADE FUTURO RECOMENDADO** ✅

  

---

  

## 🎯 Resumo Final

  

### Hoje:

```

✅ Service Principal (App Registration)

✅ Perfeito para seu caso!

✅ Simples e funcional

```

  

### Futuro (Produção no Azure):

```

🔥 Migre para Managed Identity

🔥 ZERO credenciais expostas

🔥 Azure gerencia tudo

```

  

### Se criar Dashboard:

```

💡 Adicione User Authentication

💡 Usuários fazem login

💡 Cada um vê seus dados

```

  

---

  

**🎉 Conclusão:**

  

Você **JÁ está usando** Azure App Registration! É o Service Principal que gera seus `CLIENT_ID` e `CLIENT_SECRET`.

  

Para sua aplicação atual (sincronização automática), está **perfeito**!

  

Só considere mudar para:

- **Managed Identity** quando subir para produção no Azure

- **User Authentication** se criar um frontend com login

  

🚀 Está usando a melhor prática para seu caso!