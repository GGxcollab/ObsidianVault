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
