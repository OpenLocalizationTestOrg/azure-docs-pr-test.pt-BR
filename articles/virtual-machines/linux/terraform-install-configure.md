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
ms.openlocfilehash: b6706f53b21347442def05a592c30a2d22718984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="a3f03-103">Instalar e configurar Terraform tooprovision VMs e outra infraestrutura para o Azure</span><span class="sxs-lookup"><span data-stu-id="a3f03-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="a3f03-104">Este artigo descreve Olá etapas necessárias tooinstall e configurar recursos de tooprovision Terraform como máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f03-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="a3f03-105">Você aprenderá como toocreate e o uso do Azure credenciais recursos de nuvem tooenable Terraform tooprovision de forma segura.</span><span class="sxs-lookup"><span data-stu-id="a3f03-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="a3f03-106">HashiCorp Terraform fornece uma maneira fácil de toodefine e implantar a infraestrutura de nuvem usando uma linguagem de modelagem personalizado chamada HashiCorp language de configuração (HCL).</span><span class="sxs-lookup"><span data-stu-id="a3f03-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="a3f03-107">Esse idioma personalizado é [toowrite simples e fácil toounderstand](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a3f03-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="a3f03-108">Além disso, usando Olá `terraform plan` de comando, você pode visualizar a infraestrutura de tooyour Olá alterações antes de confirmá-las.</span><span class="sxs-lookup"><span data-stu-id="a3f03-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="a3f03-109">Siga essas toostart etapas usando Terraform com o Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f03-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="a3f03-110">Instalar o Terraform</span><span class="sxs-lookup"><span data-stu-id="a3f03-110">Install Terraform</span></span>
<span data-ttu-id="a3f03-111">tooinstall Terraform, [baixar](https://www.terraform.io/downloads.html) pacote de saudação apropriado para seu sistema operacional em um diretório de instalação separado.</span><span class="sxs-lookup"><span data-stu-id="a3f03-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="a3f03-112">download de saudação contém um único arquivo executável, para que você também deve definir um caminho de global.</span><span class="sxs-lookup"><span data-stu-id="a3f03-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="a3f03-113">Para obter instruções sobre como tooset Olá caminho no Linux e Mac, vá muito[esta página da Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="a3f03-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="a3f03-114">Para obter instruções sobre como tooset Olá caminho no Windows, vá muito[esta página da Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="a3f03-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="a3f03-115">tooverify a instalação, execute Olá `terraform` comando.</span><span class="sxs-lookup"><span data-stu-id="a3f03-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="a3f03-116">Você deve ver uma lista das opções do Terraform disponíveis como saída.</span><span class="sxs-lookup"><span data-stu-id="a3f03-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="a3f03-117">Em seguida, você precisa tooallow Terraform acesso tooyour assinatura do Azure tooperform provisionamento da infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="a3f03-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="a3f03-118">Configurar Terraform tooAzure de acesso</span><span class="sxs-lookup"><span data-stu-id="a3f03-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="a3f03-119">tooenable Terraform tooprovision recursos no Azure, você precisa de duas entidades toocreate no Azure Active Directory (AD do Azure): um aplicativo do AD do Azure e uma entidade de serviço do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f03-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="a3f03-120">Em seguida, use os identificadores dessas entidades nos scripts do Terraform.</span><span class="sxs-lookup"><span data-stu-id="a3f03-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="a3f03-121">A entidade de serviço é uma instância local de um aplicativo Azure AD global.</span><span class="sxs-lookup"><span data-stu-id="a3f03-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="a3f03-122">Uma entidade de serviço permite que os recursos de tooglobal de controle de acesso granular de local.</span><span class="sxs-lookup"><span data-stu-id="a3f03-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="a3f03-123">Há toocreate de várias maneiras de um aplicativo do AD do Azure e uma entidade de serviço do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f03-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="a3f03-124">Olá mais fácil e rápida maneira hoje é toouse 2.0 do CLI do Azure, que [você pode baixar e instalar em um Mac, Linux ou Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a3f03-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="a3f03-125">Você também pode usar infraestrutura de segurança necessárias de saudação toocreate PowerShell ou 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f03-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="a3f03-126">instruções Olá a seguir mostram como tooconfigure Terraform para o Azure usando todas essas abordagens.</span><span class="sxs-lookup"><span data-stu-id="a3f03-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="a3f03-127">Usar a CLI 2.0 do Azure (para usuários do Windows, Linux ou Mac)</span><span class="sxs-lookup"><span data-stu-id="a3f03-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="a3f03-128">Depois de baixar e instalar Olá [2.0 do CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), entrar tooadminister sua assinatura do Azure emitindo Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3f03-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="a3f03-129">Se você usar Olá China, Azure Alemanha ou nuvens de governo do Azure, você precisa toofirst configurar Olá CLI do Azure toowork com a nuvem.</span><span class="sxs-lookup"><span data-stu-id="a3f03-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="a3f03-130">Você pode fazer isso executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="a3f03-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="a3f03-131">Se você tiver várias assinaturas do Azure, seus detalhes serão retornados pelo Olá `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="a3f03-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="a3f03-132">Olá conjunto `SUBSCRIPTION_ID` ambiente variável toohold Olá valor Olá retornado `id` campo da assinatura Olá deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="a3f03-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="a3f03-133">Definir a assinatura de saudação que você deseja toouse para esta sessão.</span><span class="sxs-lookup"><span data-stu-id="a3f03-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="a3f03-134">ID da assinatura Olá Olá conta tooget de consulta e valores de ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="a3f03-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="a3f03-135">Em seguida, crie credenciais separadas para o Terraform.</span><span class="sxs-lookup"><span data-stu-id="a3f03-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="a3f03-136">A appId, a senha, o sp_name e o locatário são retornados.</span><span class="sxs-lookup"><span data-stu-id="a3f03-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="a3f03-137">Anote Olá appId e a senha.</span><span class="sxs-lookup"><span data-stu-id="a3f03-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="a3f03-138">tooconfirm suas credenciais (entidade de serviço), abra um novo shell e execute Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a3f03-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="a3f03-139">Olá substituir valores para sp_name, senha e locatário retornado:</span><span class="sxs-lookup"><span data-stu-id="a3f03-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="a3f03-140">Use o PowerShell (para usuários do Windows)</span><span class="sxs-lookup"><span data-stu-id="a3f03-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="a3f03-141">toouse um Windows toowrite do computador e execute seu Terraform scripts e toouse do PowerShell para tarefas de configuração, configurar seu computador com ferramentas do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a3f03-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="a3f03-142">Instalar as ferramentas do PowerShell, seguindo as etapas de saudação em [instalar e configurar o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a3f03-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="a3f03-143">Baixar e executar Olá [setup.ps1 azure script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) no console do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a3f03-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="a3f03-144">azure setup.ps1 script toorun Olá baixá-lo e executar Olá `./azure-setup.ps1 setup` comando no console do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a3f03-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="a3f03-145">Em seguida, entre tooyour assinatura do Azure com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="a3f03-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="a3f03-146">Forneça um nome de aplicativo (cadeia de caracteres arbitrária, obrigatória) quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="a3f03-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="a3f03-147">Opcionalmente, forneça uma senha forte quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="a3f03-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="a3f03-148">Caso você não forneça a senha, uma senha forte será gerada para você usando as bibliotecas de segurança do .NET.</span><span class="sxs-lookup"><span data-stu-id="a3f03-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="a3f03-149">Usar a CLI 1.0 do Azure (para usuários do Linux ou do Mac)</span><span class="sxs-lookup"><span data-stu-id="a3f03-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="a3f03-150">tooget iniciado com Terraform em máquinas Linux ou Macs com 1.0 da CLI do Azure, instalar Olá adequada bibliotecas em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a3f03-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="a3f03-151">Instalar ferramentas CLI do Azure xPlat, seguindo as etapas de saudação em [instalar o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a3f03-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="a3f03-152">Baixar e instalar um processador JSON, seguindo as instruções de saudação do [baixar jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="a3f03-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="a3f03-153">Baixar e executar Olá [setup.sh azure script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3f03-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="a3f03-154">azure setup.sh script toorun Olá baixá-lo e executar Olá `./azure-setup setup` comando do console de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3f03-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="a3f03-155">Em seguida, entre tooyour assinatura do Azure com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="a3f03-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="a3f03-156">Forneça um nome de aplicativo (cadeia de caracteres arbitrária, obrigatória) quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="a3f03-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="a3f03-157">Opcionalmente, forneça uma senha forte quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="a3f03-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="a3f03-158">Caso você não forneça a senha, uma senha forte será gerada para você usando as bibliotecas de segurança do .NET.</span><span class="sxs-lookup"><span data-stu-id="a3f03-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="a3f03-159">Todos os scripts anteriores de saudação criam um aplicativo do AD do Azure e o serviço principal.</span><span class="sxs-lookup"><span data-stu-id="a3f03-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="a3f03-160">entidade de serviço Olá obtém um colaborador ou o acesso no nível do proprietário da assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="a3f03-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="a3f03-161">Devido ao alto nível de acesso concedido hello, você sempre deve proteger informações de segurança Olá geradas por esses scripts.</span><span class="sxs-lookup"><span data-stu-id="a3f03-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="a3f03-162">Anote as quatro partes das informações de segurança fornecidas por estes scripts: appId, senha, subscription_id e tenant_id.</span><span class="sxs-lookup"><span data-stu-id="a3f03-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="a3f03-163">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="a3f03-163">Set environment variables</span></span>
<span data-ttu-id="a3f03-164">Depois de criar e configurar uma entidade de serviço do AD do Azure, você precisa toolet Terraform saber Olá locatário ID, ID de assinatura, ID do cliente e toouse secreta do cliente.</span><span class="sxs-lookup"><span data-stu-id="a3f03-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="a3f03-165">Você pode fazer isso inserindo os valores em seus scripts do Terraform, conforme descrito em [Criar infraestrutura básica usando o Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a3f03-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="a3f03-166">Como alternativa, você pode definir Olá variáveis de ambiente a seguir (e, assim, evite fazer check-in ou as credenciais de compartilhamento acidentalmente):</span><span class="sxs-lookup"><span data-stu-id="a3f03-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="a3f03-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="a3f03-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="a3f03-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="a3f03-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="a3f03-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="a3f03-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="a3f03-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="a3f03-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="a3f03-171">Você pode usar essas variáveis de tooset de script de shell neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="a3f03-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="a3f03-172">Além disso, se você usar Terraform com o Azure na China ou o Azure Government ou Azure Alemanha, será necessário variável de ambiente tooset Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="a3f03-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello ENVIRONMENT variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3f03-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3f03-173">Next steps</span></span>
<span data-ttu-id="a3f03-174">Agora você instalou o Terraform e configurou as credenciais do Azure, de modo que pode iniciar a implantação da infraestrutura em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f03-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="a3f03-175">Em seguida, Aprenda como muito[criar infra-estrutura de Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a3f03-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
