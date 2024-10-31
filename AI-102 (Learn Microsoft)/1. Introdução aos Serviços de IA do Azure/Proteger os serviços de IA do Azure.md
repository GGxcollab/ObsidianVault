# Introdução
- Os serviços de IA do Azure fornecem várias camadas de segurança que você deve considerar ao implementar uma solução.
- Ao concluir esse módulo, você saberá como:
	- Considerar a autenticação para os serviços de IA do Azure.
	- Gerenciar a segurança de rede para os serviços de IA do Azure.
# Considerar a autenticação
- Por padrão, o acesso aos recursos de Serviços de IA do Azure é restrito usando chaves de assinatura. O gerenciamento de acesso a essas chaves é uma consideração principal para a segurança.
#### Regenerar chaves
- Você deve regenerar as chaves regularmente para proteger contra o risco de que elas sejam compartilhadas ou acessadas por usuários não autorizados. Você pode regenerar chaves usando o portal do Azure ou usando o comando da CLI (interface de linha de comando) do Azure `az cognitiveservices account keys regenerate`.
- Cada serviço de IA é fornecido com duas chaves, permitindo que você gere novamente chaves sem interrupção do serviço. Para realizar isso:
	1. Se você estiver usando as duas chaves em produção, altere o código para que apenas uma chave esteja em uso. Por exemplo, configure todos os aplicativos de produção para usar a chave 1.
	2. Regenerar a chave 2.
	3. Alterne todos os aplicativos de produção para usar a chave 2 regenerada recentemente.
	4. Regenerar a chave 1
	5. Por fim, atualize o código de produção para usar a nova chave 1.
- Por exemplo, para regenerar chaves no portal do Azure, você pode fazer o seguinte:
	1. No portal do Azure, vá para o painel Chaves e Ponto de Extremidade do recurso.
	2. Em seguida, selecione **Regenerar Chave1** ou selecione **Regenerar Chave2**, dependendo de qual você deseja regenerar no momento.
#### Proteger chaves com o Azure Key Vault
- O Azure Key Vault é um serviço do Azure no qual você pode armazenar segredos com segurança (como senhas e chaves). O acesso ao cofre de chaves é concedido a _entidades de segurança_, as quais você pode considerar identidades de usuário autenticadas usando o Microsoft Entra ID. Os administradores podem atribuir uma entidade de segurança a um aplicativo (nesse caso, ele é conhecido como uma _entidade de serviço_) a fim de definir uma _identidade gerenciada_ para o aplicativo. O aplicativo pode usar essa identidade para acessar o cofre de chaves e recuperar um segredo ao qual ele tem acesso. Controlar o acesso ao segredo dessa forma minimiza o risco de que ele seja comprometido por ser embutido em código em um aplicativo ou salvo em um arquivo de configuração.
- Você pode armazenar as chaves de assinatura para um recurso dos serviços de IA do no Azure Key Vault e atribuir uma identidade gerenciada aos aplicativos cliente que precisam usar o serviço. Os aplicativos podem então recuperar a chave conforme necessário no cofre de chaves, sem o risco de expô-la a usuários não autorizados.
- ![[Pasted image 20241031110014.png]]
#### Autenticação baseada em token
- Ao usar a interface REST, alguns serviços de IA dao suporte (ou até mesmo exigem) a autenticação baseada em token. Nesses casos, a chave de assinatura é apresentada em uma solicitação inicial para obter um tojen de autenctincação, que tem um período válido de dez minutos. As solicitações subsequentes devem apresentar um otken para validar que o chamador foi autenticado.

> [!Dica] Dica
> Ao usar um SDK, as chamadas para obter e apresentar um token são tratadas para você pelo SDK.
> 

#### Autenticação do Microsoft Entra ID
- Os serviços de IA do Azure dão suporte à autenticação do Microsoft Entra ID, permitindo que você conceda acesso a entidades de serviço específicas ou identidades gerenciadas para aplicativos e serviços em execução no Azure.

> [!NOTE] Observação
> Para obter mais informações sobre opções de autenticação para serviços de IA, confira a [documentação de serviços de IA](https://learn.microsoft.com/pt-br/azure/ai-services/authentication).

- Há diferentes maneiras de se autenticar nos serviços de IA do Azure usando o Microsoft Entra ID, incluindo:
### Autenticação por meio de entidades de serviço
- O processo geral de autenticação em serviços de IA do Azure por meio de entidades de serviço é o seguinte:
#### Criar um subdomínio personalizado
- Você pode criar um subdomínio personalizado de diferentes maneiras, como por meio do portal do Azure, da CLI do Azure ou do PowerShell.
- Por exemplo, você pode criar um subdomínio usando o PowerShell no Azure Cloud Shell. Para fazer isso, selecione sua assinatura usando o seguinte comando:
##### PowerShell
```
Set-AzContext -SubscriptionName <Your-Subscription-Name>
```

- Em seguida, crie o recurso de serviços de IA do Azure especificando um subdomínio personalizado executando o seguinte:
##### PowerShell
```
$account = New-AzCognitiveServicesAccount -ResourceGroupName <your-resource-group-name> -name <your-account-name> -Type <your-account-type> -SkuName <your-sku-type> -Location <your-region> -CustomSubdomainName <your-unique-subdomain-name>
```

- Depois de criado, o nome do subdomínio será retornado na resposta.
#### Atribuir uma função a uma entidade de serviço
- Você criou um recurso de IA do Azure vinculado a um subdomínio personalizado. Em seguida, atribua uma função a uma entidade de serviço.
- Para começar, você precisará registrar um aplicativo. Para isso, execute o comando a seguir:
##### PowerShell
```
$SecureStringPassword = ConvertTo-SecureString -String <your-password> -AsPlainText -Force

$app = New-AzureADApplication -DisplayName <your-app-display-name> -IdentifierUris <your-app-uris> -PasswordCredentials $SecureStringPassword
```

- Isso cria o recurso do aplicativo.
- Em seguida, use o comando **New-AzADServicePrincipal** para criar uma entidade de serviço e fornecer a ID do aplicativo:
##### PowerShell

```
New-AzADServicePrincipal -ApplicationId <app-id>
```

Por fim, atribua a função **Usuários dos Serviços Cognitivos** à entidade de serviço executando:

PowerShellCopiar

```
New-AzRoleAssignment -ObjectId <your-service-principal-object-id> -Scope <account-id> -RoleDefinitionName "Cognitive Services User"
```

### Autenticar usando identidades gerenciadas

As identidades gerenciadas estão disponíveis em dois tipos:

- **Identidade gerenciada atribuída pelo sistema**: Uma identidade gerenciada é criada e vinculada a um recurso específico, como uma máquina virtual que precisa acessar os serviços de IA do Azure. Quando o recurso é excluído, a identidade também é excluída.
- **Identidade gerenciada atribuída pelo usuário**: A identidade gerenciada é criada para ser utilizável por vários recursos em vez de ser vinculada a um. Ela existe independentemente de qualquer recurso único.

Você pode atribuir cada tipo de identidade gerenciada a um recurso durante a criação do recurso ou depois que ele já tiver sido criado.

Por exemplo, suponha que você tenha uma máquina virtual no Azure que pretende usar para acessar diariamente os serviços de IA do Azure. Para habilitar uma identidade atribuída pelo sistema para essa máquina virtual, primeiro verifique se sua conta do Azure tem a [função de Colaborador de Máquina Virtual](https://learn.microsoft.com/pt-br/azure/role-based-access-control/built-in-roles). Em seguida, execute o seguinte comando usando a CLI do Azure no terminal do Azure Cloud Shell:

CLI do AzureCopiar

```
az vm identity assign -g <my-resource-group> -n <my-vm>
```

Em seguida, conceda acesso aos serviços de IA do Azure no portal do Azure usando o seguinte:

1. Acesse o recurso de serviços de IA do Azure que você deseja conceder ao acesso de identidade gerenciada da máquina virtual.
    
2. No painel de visão geral, selecione **Controle de acesso (IAM)**.
    
3. Selecione **Adicionar** e selecione **Adicionar atribuição de função**.
    
4. Na guia Função, selecione **Colaborador dos Serviços Cognitivos**.
    
    [![A screenshot showing the Add role assignment tab.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/secure-ai-services/media/select-contributor-role-small.png)](https://learn.microsoft.com/pt-br/training/wwl-data-ai/secure-ai-services/media/select-contributor-role.png#lightbox)
    
5. Na guia Membros, em Atribuir acesso, selecione **Identidade gerenciada**. Em seguida, escolha **+ Selecionar membros**.
    
    [![A screenshot showing the Select managed identities pane.](https://learn.microsoft.com/pt-br/training/wwl-data-ai/secure-ai-services/media/select-managed-identity-small.png)](https://learn.microsoft.com/pt-br/training/wwl-data-ai/secure-ai-services/media/select-managed-identity.png#lightbox)
    
6. Verifique se sua assinatura está selecionada na lista suspensa Assinatura. E, para a Identidade gerenciada, selecione **Máquina virtual**.
    
7. Selecione sua máquina virtual na lista e escolha **Selecionar**.
    
8. Por fim, selecione **Examinar + atribuir** para revisão e, em seguida, **Examinar + atribuir** novamente para concluir.
    

 Observação

Para obter mais detalhes sobre como configurar identidades gerenciadas, incluindo identidades gerenciadas pelo usuário, confira [Configurar identidades gerenciadas para o recurso do Azure na VM do Azure usando a CLI do Azure](https://learn.microsoft.com/pt-br/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm)
