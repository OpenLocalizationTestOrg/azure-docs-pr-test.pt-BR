---
title: Instalar e configurar o Terraform para provisionar VMs e outra infraestrutura no Azure | Microsoft Docs
description: Saiba como instalar e configurar o Terraform para criar recursos do Azure
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
ms.openlocfilehash: 1f26bccf279ebb61fbf77767186d0435e4f4ba40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-configure-terraform-to-provision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="535a9-103">Instalar e configurar o Terraform para provisionar VMs e outra infraestrutura no Azure</span><span class="sxs-lookup"><span data-stu-id="535a9-103">Install and configure Terraform to provision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="535a9-104">Este artigo descreve as etapas necessárias para instalar e configurar o Terraform para provisionar recursos como máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="535a9-104">This article describes the necessary steps to install and configure Terraform to provision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="535a9-105">Você aprenderá a criar e usar as credenciais do Azure para permitir que o Terraform provisione recursos da nuvem de forma segura.</span><span class="sxs-lookup"><span data-stu-id="535a9-105">You will learn how to create and use Azure credentials to enable Terraform to provision cloud resources in a secure manner.</span></span>

<span data-ttu-id="535a9-106">O HashiCorp Terraform fornece uma maneira fácil de definir e implantar a infraestrutura de nuvem usando uma linguagem de modelagem personalizada chamada HCL (linguagem de configuração HashiCorp).</span><span class="sxs-lookup"><span data-stu-id="535a9-106">HashiCorp Terraform provides an easy way to define and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="535a9-107">Essa linguagem personalizada é [fácil de escrever e de entender](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="535a9-107">This custom language is [easy to write and easy to understand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="535a9-108">Além disso, usando o comando `terraform plan`, você pode visualizar as alterações à sua infraestrutura antes de confirmá-las.</span><span class="sxs-lookup"><span data-stu-id="535a9-108">Additionally, by using the `terraform plan` command, you can visualize the changes to your infrastructure before you commit them.</span></span> <span data-ttu-id="535a9-109">Siga estas etapas para começar a usar o Terraform com o Azure.</span><span class="sxs-lookup"><span data-stu-id="535a9-109">Follow these steps to start using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="535a9-110">Instalar o Terraform</span><span class="sxs-lookup"><span data-stu-id="535a9-110">Install Terraform</span></span>
<span data-ttu-id="535a9-111">Para instalar o Terraform, [baixe](https://www.terraform.io/downloads.html) o pacote apropriado para seu sistema operacional para um diretório de instalação separado.</span><span class="sxs-lookup"><span data-stu-id="535a9-111">To install Terraform, [download](https://www.terraform.io/downloads.html) the package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="535a9-112">O download contém um único arquivo executável, para o qual também deve definir um caminho global.</span><span class="sxs-lookup"><span data-stu-id="535a9-112">The download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="535a9-113">Para obter instruções sobre como definir o caminho no Linux e no Mac, acesse [esta página da Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="535a9-113">For instructions on how to set the path on Linux and Mac, go to [this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="535a9-114">Para obter instruções sobre como definir o caminho no Windows, acesse [esta página da Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="535a9-114">For instructions on how to set the path on Windows, go to [this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="535a9-115">Para verificar sua instalação, execute o comando `terraform`.</span><span class="sxs-lookup"><span data-stu-id="535a9-115">To verify your installation, run the `terraform` command.</span></span> <span data-ttu-id="535a9-116">Você deve ver uma lista das opções do Terraform disponíveis como saída.</span><span class="sxs-lookup"><span data-stu-id="535a9-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="535a9-117">Em seguida, você precisa permitir o acesso do Terraform à sua assinatura do Azure para executar o provisionamento de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="535a9-117">Next, you need to allow Terraform access to your Azure subscription to perform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-to-azure"></a><span data-ttu-id="535a9-118">Configurar o acesso do Terraform ao Azure</span><span class="sxs-lookup"><span data-stu-id="535a9-118">Set up Terraform access to Azure</span></span>
<span data-ttu-id="535a9-119">Para habilitar o Terraform a provisionar recursos para o Azure, você precisa criar duas entidades no Azure AD (Azure Active Directory): aplicativo Azure AD e entidade de serviço do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="535a9-119">To enable Terraform to provision resources into Azure, you need to create two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="535a9-120">Em seguida, use os identificadores dessas entidades nos scripts do Terraform.</span><span class="sxs-lookup"><span data-stu-id="535a9-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="535a9-121">A entidade de serviço é uma instância local de um aplicativo Azure AD global.</span><span class="sxs-lookup"><span data-stu-id="535a9-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="535a9-122">Uma entidade de serviço permite um controle de acesso local granular aos recursos globais.</span><span class="sxs-lookup"><span data-stu-id="535a9-122">A service principal allows granular local access control to global resources.</span></span>

<span data-ttu-id="535a9-123">Há várias maneiras de criar um aplicativo Azure AD e uma entidade de serviço do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="535a9-123">There are several ways to create an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="535a9-124">A maneira mais fácil e rápida hoje é usar a CLI 2.0 do Azure, que [pode ser baixada e instalada no Windows/Linux/Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="535a9-124">The easiest and fastest way today is to use Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="535a9-125">Você também pode usar o PowerShell ou a CLI 1.0 do Azure para criar a infraestrutura de segurança necessária.</span><span class="sxs-lookup"><span data-stu-id="535a9-125">You also can use PowerShell or Azure CLI 1.0 to create the necessary security infrastructure.</span></span> <span data-ttu-id="535a9-126">As instruções a seguir mostram como configurar o Terraform para Azure usando todas essas abordagens.</span><span class="sxs-lookup"><span data-stu-id="535a9-126">The instructions that follow show you how to configure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="535a9-127">Usar a CLI 2.0 do Azure (para usuários do Windows, Linux ou Mac)</span><span class="sxs-lookup"><span data-stu-id="535a9-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="535a9-128">Depois de baixar e instalar a [CLI 2.0 do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), entre como administrar na sua assinatura do Azure emitindo o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="535a9-128">After you download and install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in to administer your Azure subscription by issuing the following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="535a9-129">Se você usar as nuvens da China, do Azure Alemanha ou do Azure Governamental, precisará primeiro configurar a CLI do Azure para funcionar com essa nuvem.</span><span class="sxs-lookup"><span data-stu-id="535a9-129">If you use the China, Azure Germany, or Azure Government clouds, you need to first configure the Azure CLI to work with that cloud.</span></span> <span data-ttu-id="535a9-130">Você pode fazer isso executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="535a9-130">You can do this by running the following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="535a9-131">Se você tiver várias assinaturas do Azure, seus detalhes serão retornados pelo comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="535a9-131">If you have multiple Azure subscriptions, their details are returned by the `az login` command.</span></span> <span data-ttu-id="535a9-132">Defina a variável de ambiente `SUBSCRIPTION_ID` para manter o valor do campo `id` retornado da assinatura que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="535a9-132">Set the `SUBSCRIPTION_ID` environment variable to hold the value of the returned `id` field from the subscription you want to use.</span></span> 

<span data-ttu-id="535a9-133">Defina a assinatura que você deseja usar para essa sessão.</span><span class="sxs-lookup"><span data-stu-id="535a9-133">Set the subscription that you want to use for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="535a9-134">Consulte a conta para obter os valores de ID da assinatura e ID do locatário.</span><span class="sxs-lookup"><span data-stu-id="535a9-134">Query the account to get the subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="535a9-135">Em seguida, crie credenciais separadas para o Terraform.</span><span class="sxs-lookup"><span data-stu-id="535a9-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="535a9-136">A appId, a senha, o sp_name e o locatário são retornados.</span><span class="sxs-lookup"><span data-stu-id="535a9-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="535a9-137">Anote a appId e a senha.</span><span class="sxs-lookup"><span data-stu-id="535a9-137">Make a note of the appId and password.</span></span>

<span data-ttu-id="535a9-138">Para confirmar suas credenciais (entidade de serviço), abra um novo shell e execute os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="535a9-138">To confirm your credentials (service principal), open a new shell and run the following commands.</span></span> <span data-ttu-id="535a9-139">Substitua os valores retornados para sp_name, senha e locatário:</span><span class="sxs-lookup"><span data-stu-id="535a9-139">Substitute the returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="535a9-140">Use o PowerShell (para usuários do Windows)</span><span class="sxs-lookup"><span data-stu-id="535a9-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="535a9-141">Para usar um computador Windows para escrever e executar seus scripts do Terraform e usar o PowerShell para tarefas de configuração, configure o computador com as ferramentas certas do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="535a9-141">To use a Windows machine to write and execute your Terraform scripts and to use PowerShell for configuration tasks, configure your machine with the right PowerShell tools.</span></span> 

1. <span data-ttu-id="535a9-142">Instale as ferramentas do PowerShell seguindo as etapas em [Instalar e configurar o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="535a9-142">Install PowerShell tools by following the steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="535a9-143">Baixe e execute o [script azure-setup.ps1](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) no console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="535a9-143">Download and execute the [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from the PowerShell console.</span></span>

3. <span data-ttu-id="535a9-144">Para executar o script azure-setup.ps1, baixe-o e execute o comando `./azure-setup.ps1 setup` no console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="535a9-144">To run the azure-setup.ps1 script, download it and execute the `./azure-setup.ps1 setup` command from the PowerShell console.</span></span> <span data-ttu-id="535a9-145">Em seguida, entre na sua assinatura do Azure com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="535a9-145">Then sign in to your Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="535a9-146">Forneça um nome de aplicativo (cadeia de caracteres arbitrária, obrigatória) quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="535a9-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="535a9-147">Opcionalmente, forneça uma senha forte quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="535a9-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="535a9-148">Caso você não forneça a senha, uma senha forte será gerada para você usando as bibliotecas de segurança do .NET.</span><span class="sxs-lookup"><span data-stu-id="535a9-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="535a9-149">Usar a CLI 1.0 do Azure (para usuários do Linux ou do Mac)</span><span class="sxs-lookup"><span data-stu-id="535a9-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="535a9-150">Para começar a usar o Terraform em computadores Linux ou Macs com a CLI 1.0 do Azure, instale as bibliotecas adequadas no seu computador.</span><span class="sxs-lookup"><span data-stu-id="535a9-150">To get started with Terraform on Linux machines or Macs with Azure CLI 1.0, install the proper libraries on your machine.</span></span>  

1. <span data-ttu-id="535a9-151">Instale as ferramentas da CLI xPlat do Azure seguindo as etapas em [Instalar CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="535a9-151">Install Azure xPlat CLI tools by following the steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="535a9-152">Baixe e instale um processador JSON seguindo as instruções em [Baixar jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="535a9-152">Download and install a JSON processor by following the instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="535a9-153">Baixe e execute o script bash [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) do console.</span><span class="sxs-lookup"><span data-stu-id="535a9-153">Download and execute the [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from the console.</span></span>

4. <span data-ttu-id="535a9-154">Para executar o script azure-setup.sh, baixe-o e execute o comando `./azure-setup setup` do console.</span><span class="sxs-lookup"><span data-stu-id="535a9-154">To run the azure-setup.sh script, download it and execute the `./azure-setup setup` command from the console.</span></span> <span data-ttu-id="535a9-155">Em seguida, entre na sua assinatura do Azure com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="535a9-155">Then sign in to your Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="535a9-156">Forneça um nome de aplicativo (cadeia de caracteres arbitrária, obrigatória) quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="535a9-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="535a9-157">Opcionalmente, forneça uma senha forte quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="535a9-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="535a9-158">Caso você não forneça a senha, uma senha forte será gerada para você usando as bibliotecas de segurança do .NET.</span><span class="sxs-lookup"><span data-stu-id="535a9-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="535a9-159">Todos os scripts anteriores criam um aplicativo Azure AD e a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="535a9-159">All the previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="535a9-160">A entidade de serviço obtém um acesso em nível do proprietário ou colaborador na assinatura.</span><span class="sxs-lookup"><span data-stu-id="535a9-160">The service principal gets a contributor or owner-level access on the subscription.</span></span> <span data-ttu-id="535a9-161">Devido ao alto nível de acesso concedido, você sempre deve proteger as informações de segurança geradas por esses scripts.</span><span class="sxs-lookup"><span data-stu-id="535a9-161">Because of the high level of access granted, you should always protect the security information generated by those scripts.</span></span> <span data-ttu-id="535a9-162">Anote as quatro partes das informações de segurança fornecidas por estes scripts: appId, senha, subscription_id e tenant_id.</span><span class="sxs-lookup"><span data-stu-id="535a9-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="535a9-163">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="535a9-163">Set environment variables</span></span>
<span data-ttu-id="535a9-164">Depois de criar e configurar a entidade de serviço do Azure AD, você precisa informar o Terraform sobre a ID do locatário, a ID da assinatura, a ID do cliente e o segredo do cliente a serem usados.</span><span class="sxs-lookup"><span data-stu-id="535a9-164">After you create and configure an Azure AD service principal, you need to let Terraform know the tenant ID, subscription ID, client ID, and client secret to use.</span></span> <span data-ttu-id="535a9-165">Você pode fazer isso inserindo os valores em seus scripts do Terraform, conforme descrito em [Criar infraestrutura básica usando o Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="535a9-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="535a9-166">Como alternativa, você pode definir as seguintes variáveis de ambiente (e, assim, evitar o check-in ou o compartilhamento acidental de suas credenciais):</span><span class="sxs-lookup"><span data-stu-id="535a9-166">Alternately, you can set the following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="535a9-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="535a9-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="535a9-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="535a9-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="535a9-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="535a9-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="535a9-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="535a9-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="535a9-171">Você pode usar esse exemplo de script shell para definir essas variáveis:</span><span class="sxs-lookup"><span data-stu-id="535a9-171">You can use this sample shell script to set those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="535a9-172">Além disso, se estiver usando o Terraform com o Azure na China ou o Azure Governamental ou o Azure Alemanha, você precisará definir a variável de ambiente de modo adequado.</span><span class="sxs-lookup"><span data-stu-id="535a9-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need to set the environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="535a9-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="535a9-173">Next steps</span></span>
<span data-ttu-id="535a9-174">Agora você instalou o Terraform e configurou as credenciais do Azure, de modo que pode iniciar a implantação da infraestrutura em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="535a9-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="535a9-175">Em seguida, saiba como [criar a infraestrutura com o Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="535a9-175">Next, learn how to [create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
