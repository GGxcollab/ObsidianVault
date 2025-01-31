# Documentação, Providers e TerraCloud - Aula 01
## Terraform Cloud
- O Terraform Cloud é uma ferramenta de pipeline de infraestrutura
- Uma ferramenta de CI e CD, digamos assim, para fazer um link, que a própria HashCorp oferece, não é open source
- E a ideia aqui é simplesmente facilitar a sua automação, então quando, por exemplo, você tiver um merge, um pull request ali fechado, por exemplo, um commit lá no seu repositório de infra, você já poderia disparar uma pipeline para criar esse recurso, editar ou deletar esse recurso ali no seu provedor de nuvem]

## Providers
- basicamente é a forma de se utilizar o terraform
- ferramentas presentes dentro do terraform registry

## Documentação
- basicamente todos os recursos presentes da ferramenta, por exemplo AWS, estao dentro da documentação

>[!NOTE] Estrutura
>A estrutura basica é: definir o provedor -> coloca o recurso ->  roda o terraform na maquina ou uma pipeline de automação 

## Modules
- é possivel importar um modulo pré pronto de um recurso para usar dentro da sua automação
- funciona como um template com regras ja pré-definidas


# CLI do Terraform - Aula 02
