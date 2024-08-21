# Objectives:
1. **Planejar e implementar padrões de segurança**
2. **Planeje políticas de acesso condicional**
3. **Implemente controles e atribuições de política de acesso condicional (direcionamento, aplicativos e condicionais)**
4. **Acesso condicional baseado em modelo**
5. **Testar e solucionar problemas de políticas de acesso condicional** 
6. **Implemente controles de aplicativos e gerenciamento de sessão**
7. **Avaliação Contínua de Acesso**
8. **Contexto de autenticação**
# Explore Security Defaults
- ## **Security Defaults**
	- ![[Pasted image 20240820134847.png]]
	- **Who's it for?**
		- **Who should use security defaults?**
			- Organizarions that want to increase their security posture but don't know how oe where to start
			- Organizations utilizing the free tier of Microsoft Entra IDirectory
		- **Who shouldn't use security defaults?**
			- Oranizations currently using Condicional Access policies to bring signals together, make decisions, and enforce organizational policies
			- Organizations with Microsoft Entra ID Premium licenses
			- Organizations with complex security requirements that warrant using Condicional Access
# Plan Condicional Access policies
- ## **About condicional Access policies**
	- ![[Pasted image 20240820142917.png]]
- ## **Benefits of Condicional Access**
	- Increase productivity.
	- Manage risk.
	- Address compliance and governance.
	- Manage cost.
	- Zero Trust.
- ## **Understanding Condicional Access policy components**
	- ![[Pasted image 20240820144059.png]]
- ## Access token inssuance
	- ![[Pasted image 20240820161656.png]]
# Implement Condicional Access policies and assignments
- ## **Setting up Condicional Access**
	- Uma boa prática, sempre antes de criar uma política de condicional access, na parte do "Estado da política", primeiramente crie como "Somente relatório"
	- ![[Pasted image 20240820162223.png]]
	- ### Grant/Block Access controls
		- **Block Access**
			- Cuidado para não bloquear a si mesmo como admin.
			- Use carefully or your could block your system.
			- Always test with What-if and Report-Only mode.
		- **Grant Access**
			- Enforce several different controls befor allowing access.
		- **NOTE - Require All/Require One**
		- ![[Pasted image 20240820164813.png]]
	- ### Session Access control
		- Limit the experience of the user/application within specific cloud application.
		- Base the experience of specific condicions the user has met or failed to meet.
		- ![[Pasted image 20240820165108.png]]
	- ### Types of Condicional Access policies
		- Sign-in risk-based Condicional Access
		- User risk-based Condicional Access

