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
- ##  Types of Condicional Access policies
		- Sign-in risk-based Condicional Access
		- User risk-based Condicional Access

# Template based Condicional Access
- ## Condicional Access Templates
	- **14 policy templates**:
		- Azure Portal.
		- Microsoft Entra ID.
		- Security.
		- Condicional Access.
		- Create new policy from template.
- ## Examples of Condicional Access scenarios
	- Require registration from a trusted location.
	- Block access bu location.
	- Require compliant devices.
	- Exclude access from emergency and service accounts.
- ## Condicional Access Terms of Use (TOU)
	- ![[Pasted image 20240821142755.png]]
# Test and troubleshoot condicional access policies
- ## Configure to avoid
	- **For all users, all cloud apps:**
		- Block access;
		- Require device to be marked as compliant;
		- Require Hybrid Microsoft Entra ID domain joined device;
		- Require app protection policy;
	- **For all users, all cloud apps, all platforms:**
		- Block access;
- ## Troubleshooting sign-in interrupts
	- In this error, the message states that the application can only be accessed from devices or client applications that meet the company's mobile device management policy. In this case, the application and device do not meet that policy
	- Exemplo:
	- ![[Pasted image 20240821144751.png]]
# Implement application controls
- ## Condicional Access - App Control
	- Block download, cut, copy and print
	- Enforce document labeling with Azure Information Protection
	- Prevent file uploads
	- Monitor/Logs sessions for compliance
	- Block app access based on risk factors
	- **CA - App Control works with Microsoft Defender for Cloud Apps**
	- ![[Pasted image 20240821150732.png]]
- ## Benefits of using app protection policies (MDM/MAM)
	- MDM - Mobile Device Management / MAM - Mobile App Management
	- Protecting your company data at the app levell
	- End-user productivity isn't affected, and policies don't apply when using the app in a personal context
	- App protection policies ensure that the app-layer protections are in place
	- MDM, in addition to MAM, ensures that the device is protected
- ## Validation
	- Use the What-If tool to simulate a login from the user to the target application and other conditions based on how you configured your policy. 
	- The authentication session management controls show up in the result of the tool
	- ![[Pasted image 20240821154951.png]]
# Continuous Access Evaluation
- ## Benefits
	- There are several key benefits to continuous access evaluation.
	- User termination or password change/restet: User session revocation will be enforced in near real time.
	- Network location change: Condicional Access location policies will be enforced in near real time.
	- Token export to a machine outside of a trusted network can be prevented with Condicional Access location policies.
	- ![[Pasted image 20240821160014.png]]
# Authentication Context
- ## Configure authen