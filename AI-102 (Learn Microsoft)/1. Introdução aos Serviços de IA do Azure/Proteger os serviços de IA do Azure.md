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
'''
'''
