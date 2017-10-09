---
title: aaaInstall e configurar Terraform tooprovision VMs e outra infraestrutura no Azure | Microsoft Docs
description: Saiba como tooinstall e configurar Terraform toocreate Azure recursos
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>Instalar e configurar Terraform tooprovision VMs e outra infraestrutura para o Azure 
Este artigo descreve Olá etapas necessárias tooinstall e configurar recursos de tooprovision Terraform como máquinas virtuais no Azure. Você aprenderá como toocreate e o uso do Azure credenciais recursos de nuvem tooenable Terraform tooprovision de forma segura.

HashiCorp Terraform fornece uma maneira fácil de toodefine e implantar a infraestrutura de nuvem usando uma linguagem de modelagem personalizado chamada HashiCorp language de configuração (HCL). Esse idioma personalizado é [toowrite simples e fácil toounderstand](terraform-create-complete-vm.md). Além disso, usando Olá `terraform plan` de comando, você pode visualizar a infraestrutura de tooyour Olá alterações antes de confirmá-las. Siga essas toostart etapas usando Terraform com o Azure.

## <a name="install-terraform"></a>Instalar o Terraform
tooinstall Terraform, [baixar](https://www.terraform.io/downloads.html) pacote de saudação apropriado para seu sistema operacional em um diretório de instalação separado. download de saudação contém um único arquivo executável, para que você também deve definir um caminho de global. Para obter instruções sobre como tooset Olá caminho no Linux e Mac, vá muito[esta página da Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux). Para obter instruções sobre como tooset Olá caminho no Windows, vá muito[esta página da Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows). tooverify a instalação, execute Olá `terraform` comando. Você deve ver uma lista das opções do Terraform disponíveis como saída.

Em seguida, você precisa tooallow Terraform acesso tooyour assinatura do Azure tooperform provisionamento da infraestrutura.

## <a name="set-up-terraform-access-tooazure"></a>Configurar Terraform tooAzure de acesso
tooenable Terraform tooprovision recursos no Azure, você precisa de duas entidades toocreate no Azure Active Directory (AD do Azure): um aplicativo do AD do Azure e uma entidade de serviço do AD do Azure. Em seguida, use os identificadores dessas entidades nos scripts do Terraform. A entidade de serviço é uma instância local de um aplicativo Azure AD global. Uma entidade de serviço permite que os recursos de tooglobal de controle de acesso granular de local.

Há toocreate de várias maneiras de um aplicativo do AD do Azure e uma entidade de serviço do AD do Azure. Olá mais fácil e rápida maneira hoje é toouse 2.0 do CLI do Azure, que [você pode baixar e instalar em um Mac, Linux ou Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Você também pode usar infraestrutura de segurança necessárias de saudação toocreate PowerShell ou 1.0 da CLI do Azure. instruções Olá a seguir mostram como tooconfigure Terraform para o Azure usando todas essas abordagens.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Usar a CLI 2.0 do Azure (para usuários do Windows, Linux ou Mac) 
Depois de baixar e instalar Olá [2.0 do CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), entrar tooadminister sua assinatura do Azure emitindo Olá comando a seguir:

```
az login
```

>[!NOTE]
>Se você usar Olá China, Azure Alemanha ou nuvens de governo do Azure, você precisa toofirst configurar Olá CLI do Azure toowork com a nuvem. Você pode fazer isso executando Olá seguinte:

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

Se você tiver várias assinaturas do Azure, seus detalhes serão retornados pelo Olá `az login` comando. Olá conjunto `SUBSCRIPTION_ID` ambiente variável toohold Olá valor Olá retornado `id` campo da assinatura Olá deseja toouse. 

Definir a assinatura de saudação que você deseja toouse para esta sessão.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

ID da assinatura Olá Olá conta tooget de consulta e valores de ID de locatário.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

Em seguida, crie credenciais separadas para o Terraform.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

A appId, a senha, o sp_name e o locatário são retornados. Anote Olá appId e a senha.

tooconfirm suas credenciais (entidade de serviço), abra um novo shell e execute Olá comandos a seguir. Olá substituir valores para sp_name, senha e locatário retornado:

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>Use o PowerShell (para usuários do Windows) 
toouse um Windows toowrite do computador e execute seu Terraform scripts e toouse do PowerShell para tarefas de configuração, configurar seu computador com ferramentas do PowerShell hello. 

1. Instalar as ferramentas do PowerShell, seguindo as etapas de saudação em [instalar e configurar o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). 

2. Baixar e executar Olá [setup.ps1 azure script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) no console do PowerShell hello.

3. azure setup.ps1 script toorun Olá baixá-lo e executar Olá `./azure-setup.ps1 setup` comando no console do PowerShell hello. Em seguida, entre tooyour assinatura do Azure com privilégios administrativos.

4. Forneça um nome de aplicativo (cadeia de caracteres arbitrária, obrigatória) quando solicitado. Opcionalmente, forneça uma senha forte quando solicitado. Caso você não forneça a senha, uma senha forte será gerada para você usando as bibliotecas de segurança do .NET.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Usar a CLI 1.0 do Azure (para usuários do Linux ou do Mac)
tooget iniciado com Terraform em máquinas Linux ou Macs com 1.0 da CLI do Azure, instalar Olá adequada bibliotecas em seu computador.  

1. Instalar ferramentas CLI do Azure xPlat, seguindo as etapas de saudação em [instalar o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). 

2. Baixar e instalar um processador JSON, seguindo as instruções de saudação do [baixar jq](https://stedolan.github.io/jq/download/).

3. Baixar e executar Olá [setup.sh azure script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script no console de saudação.

4. azure setup.sh script toorun Olá baixá-lo e executar Olá `./azure-setup setup` comando do console de saudação. Em seguida, entre tooyour assinatura do Azure com privilégios administrativos.
 
5. Forneça um nome de aplicativo (cadeia de caracteres arbitrária, obrigatória) quando solicitado. Opcionalmente, forneça uma senha forte quando solicitado. Caso você não forneça a senha, uma senha forte será gerada para você usando as bibliotecas de segurança do .NET.

Todos os scripts anteriores de saudação criam um aplicativo do AD do Azure e o serviço principal. entidade de serviço Olá obtém um colaborador ou o acesso no nível do proprietário da assinatura hello. Devido ao alto nível de acesso concedido hello, você sempre deve proteger informações de segurança Olá geradas por esses scripts. Anote as quatro partes das informações de segurança fornecidas por estes scripts: appId, senha, subscription_id e tenant_id.

## <a name="set-environment-variables"></a>Configurar variáveis de ambiente
Depois de criar e configurar uma entidade de serviço do AD do Azure, você precisa toolet Terraform saber Olá locatário ID, ID de assinatura, ID do cliente e toouse secreta do cliente. Você pode fazer isso inserindo os valores em seus scripts do Terraform, conforme descrito em [Criar infraestrutura básica usando o Terraform](terraform-create-complete-vm.md). Como alternativa, você pode definir Olá variáveis de ambiente a seguir (e, assim, evite fazer check-in ou as credenciais de compartilhamento acidentalmente):

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

Você pode usar essas variáveis de tooset de script de shell neste exemplo:

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

Além disso, se você usar Terraform com o Azure na China ou o Azure Government ou Azure Alemanha, será necessário variável de ambiente tooset Olá adequadamente.

## <a name="next-steps"></a>Próximas etapas
Agora você instalou o Terraform e configurou as credenciais do Azure, de modo que pode iniciar a implantação da infraestrutura em sua assinatura do Azure. Em seguida, Aprenda como muito[criar infra-estrutura de Terraform](terraform-create-complete-vm.md).
