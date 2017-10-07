---
title: "aaaCreate uma malha do Azure serviço de cluster de um modelo | Microsoft Docs"
description: "Este artigo descreve como tooset a uma malha seguros do serviço de cluster no Azure usando o Gerenciador de recursos do Azure, o Cofre de chaves do Azure e Azure Active Directory (AD do Azure) para autenticação de cliente."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="5eed5-103">Criar um cluster do Service Fabric usando o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5eed5-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5eed5-104">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="5eed5-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="5eed5-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5eed5-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="5eed5-106">Este guia passo a passo orienta você pela configuração de um cluster do Azure Service Fabric seguro no Azure usando o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5eed5-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="5eed5-107">Confirmamos o que artigo Olá é longo.</span><span class="sxs-lookup"><span data-stu-id="5eed5-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="5eed5-108">No entanto, a menos que já esteja completamente familiarizado com conteúdo hello, ser toofollow-se de que cada etapa com cuidado.</span><span class="sxs-lookup"><span data-stu-id="5eed5-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="5eed5-109">Guia de saudação abrange Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eed5-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="5eed5-110">Configurando certificados de tooupload um cofre de chaves do Azure para segurança de aplicativos e de cluster</span><span class="sxs-lookup"><span data-stu-id="5eed5-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="5eed5-111">Como criar um cluster seguro no Azure usando o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5eed5-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="5eed5-112">Como autenticar usuários usando o Azure AD (Azure Active Directory) para gerenciamento de cluster</span><span class="sxs-lookup"><span data-stu-id="5eed5-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="5eed5-113">Um cluster seguro é um cluster que impede que as operações de toomanagement de acesso não autorizado.</span><span class="sxs-lookup"><span data-stu-id="5eed5-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="5eed5-114">Isso inclui implantar, atualizar e excluir aplicativos, serviços e dados de saudação que eles contêm.</span><span class="sxs-lookup"><span data-stu-id="5eed5-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="5eed5-115">Um cluster não seguro é um cluster que qualquer pessoa pode se conectar tooat a qualquer momento e executar operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="5eed5-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="5eed5-116">Embora seja possível toocreate um cluster não seguro, é altamente recomendável que você crie um cluster seguro desde o início de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="5eed5-117">Um cluster não seguro não pode ser protegido posteriormente; um novo cluster deverá ser criado.</span><span class="sxs-lookup"><span data-stu-id="5eed5-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="5eed5-118">conceito de saudação de criação de clusters seguros é Olá mesmo, independentemente de estarem clusters do Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="5eed5-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="5eed5-119">Para obter mais informações e scripts auxiliares para criar clusters do Linux seguras, consulte [Criando clusters seguros no Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="5eed5-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="5eed5-120">Entrar tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="5eed5-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="5eed5-121">Este guia usa o [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="5eed5-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="5eed5-122">Quando você inicia uma nova sessão do PowerShell, entre no tooyour conta do Azure e selecione sua assinatura antes de executar comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5eed5-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="5eed5-123">Entre tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="5eed5-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="5eed5-124">Selecione sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="5eed5-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="5eed5-125">Configurar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="5eed5-125">Set up a key vault</span></span>
<span data-ttu-id="5eed5-126">Esta seção trata da criação de um cofre de chaves para um cluster do Service Fabric no Azure e para aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5eed5-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="5eed5-127">Para obter um guia completo tooAzure Cofre de chaves, consulte toohello [guia de Introdução ao Cofre de chaves][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="5eed5-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="5eed5-128">Service Fabric usa toosecure de certificados x. 509 um cluster e fornecer recursos de segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5eed5-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="5eed5-129">Você pode usar certificados de toomanage de Cofre de chaves para clusters de malha do serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="5eed5-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="5eed5-130">Quando um cluster é implantado no Azure, provedor de recursos do Azure de saudação que é responsável pela criação de clusters Service Fabric recebe certificados de Cofre de chaves e os instala no cluster Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="5eed5-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="5eed5-131">Olá diagrama a seguir ilustra a relação Olá entre o Cofre de chaves do Azure, um cluster do Service Fabric e provedor de recursos do Azure Olá que usa certificados armazenados em um cofre de chaves ao criar um cluster:</span><span class="sxs-lookup"><span data-stu-id="5eed5-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagrama da instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="5eed5-133">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5eed5-133">Create a resource group</span></span>
<span data-ttu-id="5eed5-134">Olá primeira etapa é toocreate um grupo de recursos especificamente para o Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eed5-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="5eed5-135">É recomendável que você coloque o Cofre de chaves de saudação em seu próprio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5eed5-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="5eed5-136">Essa ação permite remover Olá computação e armazenamento de grupos de recursos, incluindo o grupo de recursos de saudação que contém o cluster do Service Fabric, sem perder suas chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="5eed5-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="5eed5-137">grupo de recursos de saudação que contém seu Cofre de chaves _deve estar no hello mesma região_ como cluster Olá que ele está em uso.</span><span class="sxs-lookup"><span data-stu-id="5eed5-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="5eed5-138">Se você planejar toodeploy clusters em várias regiões, sugerimos que você nomear o grupo de recursos de saudação e Olá cofre da chave de forma que indica a região que pertence a.</span><span class="sxs-lookup"><span data-stu-id="5eed5-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="5eed5-139">saída de Hello deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5eed5-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="5eed5-140">Criar um cofre de chaves no novo grupo de recursos Olá</span><span class="sxs-lookup"><span data-stu-id="5eed5-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="5eed5-141">Cofre de chaves Olá _deve ser habilitado para implantação_ tooallow Olá certificados de tooget de provedor de recursos de computação-lo e instalá-lo em instâncias de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="5eed5-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="5eed5-142">saída de Hello deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5eed5-142">hello output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="5eed5-143">Usar um cofre de chave existente</span><span class="sxs-lookup"><span data-stu-id="5eed5-143">Use an existing key vault</span></span>

<span data-ttu-id="5eed5-144">toouse um cofre de chave existente, você _deve habilitá-la para implantação_ tooallow Olá certificados de tooget de provedor de recursos de computação-lo e instalá-lo em nós de cluster:</span><span class="sxs-lookup"><span data-stu-id="5eed5-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="5eed5-145">Adicionar o Cofre de chaves de tooyour de certificados</span><span class="sxs-lookup"><span data-stu-id="5eed5-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="5eed5-146">Os certificados são usados em Service Fabric tooprovide toosecure de autenticação e criptografia vários aspectos de um cluster e seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5eed5-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="5eed5-147">Para obter mais informações sobre como os certificados são usados no Service Fabric, consulte [Cenários de segurança do cluster do Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="5eed5-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="5eed5-148">Certificado de cluster e de servidor (necessário)</span><span class="sxs-lookup"><span data-stu-id="5eed5-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="5eed5-149">Esse certificado é necessário toosecure um cluster e impedir o acesso não autorizado tooit.</span><span class="sxs-lookup"><span data-stu-id="5eed5-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="5eed5-150">Ele fornece segurança de cluster de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="5eed5-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="5eed5-151">Autenticação do cluster: autentica a comunicação de nó para nó para a federação de cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="5eed5-152">Somente nós que podem provar sua identidade com esse certificado podem ingressar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="5eed5-153">Autenticação de servidor: autentica o cliente de gerenciamento do tooa pontos de extremidade do hello cluster management, para que hello gerenciamento cliente sabe que está se comunicando cluster real toohello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="5eed5-154">Este certificado também fornece um SSL para Olá API de gerenciamento de HTTPS e Service Fabric Explorer via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5eed5-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="5eed5-155">tooserve esses fins, Olá certificado deve atender a saudação requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eed5-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="5eed5-156">certificado de saudação deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="5eed5-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="5eed5-157">certificado de saudação deve ser criado para troca de chaves, que é exportável tooa arquivo de troca de informações pessoais (. pfx).</span><span class="sxs-lookup"><span data-stu-id="5eed5-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="5eed5-158">nome da entidade do certificado Olá deve corresponder domínio Olá que você use o cluster do tooaccess saudação do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5eed5-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="5eed5-159">Esse correspondente é necessário tooprovide um SSL para pontos de extremidade do gerenciamento do cluster Olá HTTPS e o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="5eed5-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="5eed5-160">Não é possível obter um certificado SSL de uma autoridade de certificação (CA) hello. cloudapp.azure.com domínio.</span><span class="sxs-lookup"><span data-stu-id="5eed5-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="5eed5-161">Você deve obter um nome de domínio personalizado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="5eed5-162">Quando você solicitar um certificado de uma autoridade de certificação, hello nome da entidade do certificado deve corresponder nome de domínio personalizado de saudação que você pode usar para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="5eed5-163">Certificados de aplicativo (opcionais)</span><span class="sxs-lookup"><span data-stu-id="5eed5-163">Application certificates (optional)</span></span>
<span data-ttu-id="5eed5-164">Qualquer número de certificados adicionais pode ser instalado em um cluster para fins de segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5eed5-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="5eed5-165">Antes de criar o cluster, considere os cenários de segurança de aplicativo hello que exigem um toobe certificado instalado em nós hello, como:</span><span class="sxs-lookup"><span data-stu-id="5eed5-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="5eed5-166">Criptografia e descriptografia de valores de configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5eed5-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="5eed5-167">Criptografia de dados entre nós durante a replicação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="5eed5-168">Formatação de certificados para uso do provedor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="5eed5-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="5eed5-169">Você pode adicionar e usar arquivos de chave privada (.pfx) diretamente pelo cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eed5-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="5eed5-170">No entanto, o provedor de recursos de computação do Azure Olá requer toobe chaves armazenada em um formato de notação JSON (JavaScript Object) especial.</span><span class="sxs-lookup"><span data-stu-id="5eed5-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="5eed5-171">formato de saudação inclui arquivo.pfx hello como uma base cadeia de caracteres codificada de 64 e a senha da chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="5eed5-172">tooaccommodate esses requisitos, Olá chaves devem ser colocadas em uma cadeia de caracteres JSON e, em seguida, são armazenadas como "segredos" na chave Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="5eed5-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="5eed5-173">toomake esse processo mais fácil, uma [módulo PowerShell está disponível no GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="5eed5-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="5eed5-174">módulo de saudação toouse, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eed5-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="5eed5-175">Baixe todo o conteúdo do repositório de Olá Olá em um diretório local.</span><span class="sxs-lookup"><span data-stu-id="5eed5-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="5eed5-176">Vá toohello a pasta local.</span><span class="sxs-lookup"><span data-stu-id="5eed5-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="5eed5-177">Importe o módulo de ServiceFabricRPHelpers de saudação na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5eed5-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="5eed5-178">Olá `Invoke-AddCertToKeyVault` comando neste módulo PowerShell formata uma chave privada do certificado em uma cadeia de caracteres JSON e carrega o Cofre de chaves toohello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5eed5-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="5eed5-179">Usar certificado de cluster Olá comando tooadd hello e cofre da chave toohello qualquer aplicativo adicional certificados.</span><span class="sxs-lookup"><span data-stu-id="5eed5-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="5eed5-180">Repita essa etapa para todos os certificados adicionais que você deseja tooinstall em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="5eed5-181">Carregando um certificado existente</span><span class="sxs-lookup"><span data-stu-id="5eed5-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="5eed5-182">Se você receber um erro, como Olá mostrada aqui, isso normalmente significa que você tem um conflito de URL de recurso.</span><span class="sxs-lookup"><span data-stu-id="5eed5-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="5eed5-183">conflito de saudação tooresolve, alterar nome do Cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="5eed5-184">Depois de saudação conflito seja resolvido, saída de hello deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5eed5-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="5eed5-185">Você precisa Olá três anterior cadeias de caracteres, CertificateThumbprint, SourceVault e CertificateURL, tooset um cluster do Service Fabric seguro e tooobtain quaisquer certificados de aplicativo que você pode usar para segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5eed5-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="5eed5-186">Se você não salvar cadeias de caracteres hello, pode ser difícil tooretrieve-los consultando chave Olá cofre mais tarde.</span><span class="sxs-lookup"><span data-stu-id="5eed5-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="5eed5-187">Criando um certificado autoassinado e carregá-lo toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="5eed5-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="5eed5-188">Se você já carregou seu Cofre de chaves de certificados toohello, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="5eed5-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="5eed5-189">Esta etapa é para gerar um novo certificado autoassinado e carregá-lo tooyour Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eed5-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="5eed5-190">Depois de alterar parâmetros Olá Olá script a seguir e, em seguida, executá-lo, você deve ser solicitado para uma senha do certificado.</span><span class="sxs-lookup"><span data-stu-id="5eed5-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="5eed5-191">Se você receber um erro, como Olá mostrada aqui, isso normalmente significa que você tem um conflito de URL de recurso.</span><span class="sxs-lookup"><span data-stu-id="5eed5-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="5eed5-192">conflito de saudação tooresolve, alterar nome do Cofre de chaves Olá, nome do RG e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="5eed5-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="5eed5-193">Depois de saudação conflito seja resolvido, saída de hello deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5eed5-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="5eed5-194">Você precisa Olá três anterior cadeias de caracteres, CertificateThumbprint, SourceVault e CertificateURL, tooset um cluster do Service Fabric seguro e tooobtain quaisquer certificados de aplicativo que você pode usar para segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5eed5-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="5eed5-195">Se você não salvar cadeias de caracteres hello, pode ser difícil tooretrieve-los consultando chave Olá cofre mais tarde.</span><span class="sxs-lookup"><span data-stu-id="5eed5-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="5eed5-196">Neste ponto, você deve ter Olá elementos no local a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eed5-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="5eed5-197">grupo de recursos do Cofre de chaves Hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-197">hello key vault resource group.</span></span>
* <span data-ttu-id="5eed5-198">Olá Cofre de chaves e a URL (chamado SourceVault em Olá precede a saída do PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5eed5-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="5eed5-199">certificado de autenticação de servidor de cluster Hello e sua URL no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="5eed5-200">certificados de aplicativo Hello e suas URLs no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="5eed5-201">Configurar o Azure Active Directory para autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="5eed5-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="5eed5-202">AD do Azure permite que as organizações (conhecido como locatários) toomanage usuário acesso tooapplications.</span><span class="sxs-lookup"><span data-stu-id="5eed5-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="5eed5-203">Os aplicativos são divididos entre os que têm IU de entrada na Web e os que têm experiência de cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="5eed5-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="5eed5-204">Neste artigo, partimos do pressuposto que você já tenha criado um locatário.</span><span class="sxs-lookup"><span data-stu-id="5eed5-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="5eed5-205">Se você não tiver, comece lendo [como tooget um Active Directory do Azure locatário][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="5eed5-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="5eed5-206">Um cluster do Service Fabric oferece várias tooits de pontos de entrada de funcionalidade de gerenciamento, incluindo Olá baseado na web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] e [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="5eed5-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="5eed5-207">Como resultado, você criar o cluster de toohello de acesso de toocontrol do AD do Azure aplicativos dois, um aplicativo web e um aplicativo nativo.</span><span class="sxs-lookup"><span data-stu-id="5eed5-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="5eed5-208">toosimplify algumas das etapas de saudação envolvidas na configuração do AD do Azure com um cluster do Service Fabric, criamos um conjunto de scripts do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5eed5-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="5eed5-209">Você deve concluir Olá etapas a seguir antes de criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="5eed5-210">Porque os scripts de saudação esperam que os pontos de extremidade e nomes de cluster, os valores de Olá deve ser planejado e não os valores que você já tenha criado.</span><span class="sxs-lookup"><span data-stu-id="5eed5-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="5eed5-211">[Baixe os scripts de saudação] [ sf-aad-ps-script-download] tooyour computador.</span><span class="sxs-lookup"><span data-stu-id="5eed5-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="5eed5-212">Arquivo de zip Olá com o botão direito, selecione **propriedades**, selecione Olá **desbloquear** caixa de seleção e, em seguida, clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="5eed5-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="5eed5-213">Extraia o arquivo zip de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="5eed5-214">Executar `SetupApplications.ps1`e fornecer Olá TenantId, ClusterName e WebApplicationReplyUrl como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5eed5-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="5eed5-215">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5eed5-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="5eed5-216">Você pode encontrar o TenantId executando o comando do PowerShell Olá `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="5eed5-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="5eed5-217">A execução desse comando exibe o saudação TenantId para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="5eed5-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="5eed5-218">ClusterName é tooprefix usados aplicativos de saudação do AD do Azure que são criados pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="5eed5-219">Nome do toomatch Olá real do cluster não é necessário exatamente.</span><span class="sxs-lookup"><span data-stu-id="5eed5-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="5eed5-220">É pretendido toomake somente ele mais fácil toomap AD do Azure artefatos toohello Service Fabric cluster estão sendo usada em.</span><span class="sxs-lookup"><span data-stu-id="5eed5-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="5eed5-221">WebApplicationReplyUrl é saudação padrão ponto de extremidade do AD do Azure retorna tooyour usuários após a conclusão entrar.</span><span class="sxs-lookup"><span data-stu-id="5eed5-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="5eed5-222">Defina esse ponto de extremidade como ponto de extremidade de Service Fabric Explorer Olá para o cluster, que é por padrão:</span><span class="sxs-lookup"><span data-stu-id="5eed5-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="5eed5-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="5eed5-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="5eed5-224">Você é solicitado toosign tooan conta que tenha privilégios administrativos para o locatário de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5eed5-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="5eed5-225">Depois que você entrar, Olá script cria Olá web e aplicativos nativos toorepresent o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5eed5-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="5eed5-226">Se você examinar aplicativos do locatário Olá Olá [portal clássico do Azure][azure-classic-portal], você deve ver duas novas entradas:</span><span class="sxs-lookup"><span data-stu-id="5eed5-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="5eed5-227">*ClusterName*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="5eed5-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="5eed5-228">*ClusterName*\_Cliente</span><span class="sxs-lookup"><span data-stu-id="5eed5-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="5eed5-229">script Hello imprime Olá JSON necessário pelo modelo do Azure Resource Manager hello quando você cria o cluster de saudação na próxima seção, Olá, portanto, é uma janela do PowerShell boa ideia tookeep Olá abrir.</span><span class="sxs-lookup"><span data-stu-id="5eed5-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="5eed5-230">Criar um modelo do Resource Manager do cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5eed5-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="5eed5-231">Nesta seção, Olá saídas de saudação anterior comandos do PowerShell são usados em um modelo do Gerenciador de recursos de cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5eed5-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="5eed5-232">Modelos do Gerenciador de recursos de exemplo estão disponíveis no hello [Galeria de modelos de início rápido do Azure no GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="5eed5-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="5eed5-233">Esses modelos podem ser usados como ponto de partida para o modelo de cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="5eed5-234">Criar o modelo do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="5eed5-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="5eed5-235">Este guia usa Olá [cluster seguro 5 nós] [ service-fabric-secure-cluster-5-node-1-nodetype] modelo de exemplo e parâmetros de modelo.</span><span class="sxs-lookup"><span data-stu-id="5eed5-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="5eed5-236">Baixar `azuredeploy.json` e `azuredeploy.parameters.json` tooyour computador e abra ambos os arquivos em seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="5eed5-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="5eed5-237">Adicionar certificados</span><span class="sxs-lookup"><span data-stu-id="5eed5-237">Add certificates</span></span>
<span data-ttu-id="5eed5-238">Adicionar o modelo de Gerenciador de recursos de cluster certificados tooa referenciando o Cofre de chaves de saudação que contém as chaves de certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="5eed5-239">É recomendável que você coloque os valores hello Cofre de chaves em um arquivo de parâmetros de modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="5eed5-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="5eed5-240">Isso impede que Olá Gerenciador de recursos de arquivo de modelo reutilizáveis e livre de implantação de tooa específico de valores.</span><span class="sxs-lookup"><span data-stu-id="5eed5-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="5eed5-241">Adicionar que conjunto de escala de máquinas virtuais do todos os certificados toohello osProfile</span><span class="sxs-lookup"><span data-stu-id="5eed5-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="5eed5-242">Cada certificado que é instalado no cluster Olá deve ser configurado na seção de osProfile de saudação do recurso de conjunto de escala hello (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="5eed5-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="5eed5-243">Essa ação instrui Olá recurso provedor tooinstall Olá certificado Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="5eed5-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="5eed5-244">Esta instalação inclui o certificado de cluster hello e quaisquer certificados de segurança do aplicativo que você planeje toouse para seus aplicativos:</span><span class="sxs-lookup"><span data-stu-id="5eed5-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="5eed5-245">Configurar o certificado de cluster do Service Fabric Olá</span><span class="sxs-lookup"><span data-stu-id="5eed5-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="5eed5-246">certificado de autenticação de cluster Olá deve ser configurado em ambos os recurso de cluster do Service Fabric hello (Microsoft.ServiceFabric/clusters) e Olá extensão Service Fabric para a escala de máquina virtual define Olá recurso de conjunto de escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5eed5-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="5eed5-247">Essa organização permite Olá Service Fabric recurso provedor tooconfigure-lo para ser usado para autenticação do cluster e autenticação de servidor para pontos de extremidade de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="5eed5-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="5eed5-248">Recurso Conjunto de dimensionamento de máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="5eed5-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="5eed5-249">Recursos do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="5eed5-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="5eed5-250">Inserir configuração do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5eed5-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="5eed5-251">configuração de saudação do AD do Azure que você criou anteriormente pode ser inserida diretamente no seu modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="5eed5-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="5eed5-252">No entanto, é recomendável que você primeiro extrair valores hello em um reutilizável de modelo parâmetros arquivo tookeep Olá Gerenciador de recursos e livre de implantação de tooa específico de valores.</span><span class="sxs-lookup"><span data-stu-id="5eed5-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="5eed5-253"><a "configure-arm" ></a>Configurar os parâmetros do modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5eed5-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="5eed5-254">Por fim, use os valores de saída de saudação do Cofre de chaves de saudação e o arquivo de parâmetros do PowerShell do Azure AD comandos toopopulate hello:</span><span class="sxs-lookup"><span data-stu-id="5eed5-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="5eed5-255">Neste ponto, você deve ter Olá elementos no local a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eed5-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="5eed5-256">Grupo de recursos do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="5eed5-256">Key vault resource group</span></span>
  * <span data-ttu-id="5eed5-257">Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="5eed5-257">Key vault</span></span>
  * <span data-ttu-id="5eed5-258">Certificado de autenticação de servidor de cluster</span><span class="sxs-lookup"><span data-stu-id="5eed5-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="5eed5-259">Certificado de codificação de dados</span><span class="sxs-lookup"><span data-stu-id="5eed5-259">Data encipherment certificate</span></span>
* <span data-ttu-id="5eed5-260">Locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5eed5-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="5eed5-261">Aplicativo Azure AD para gerenciamento baseado na Web e no Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="5eed5-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="5eed5-262">Aplicativo Azure AD para o gerenciamento de clientes nativos</span><span class="sxs-lookup"><span data-stu-id="5eed5-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="5eed5-263">Usuários e suas funções atribuídas</span><span class="sxs-lookup"><span data-stu-id="5eed5-263">Users and their assigned roles</span></span>
* <span data-ttu-id="5eed5-264">Modelo do Resource Manager de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5eed5-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="5eed5-265">Certificados configurados por meio do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="5eed5-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="5eed5-266">Azure Active Directory configurado</span><span class="sxs-lookup"><span data-stu-id="5eed5-266">Azure Active Directory configured</span></span>

<span data-ttu-id="5eed5-267">Olá diagrama a seguir ilustra onde seu Cofre de chaves e a configuração do AD do Azure se encaixam seu modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="5eed5-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Mapa de dependências do Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="5eed5-269">Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="5eed5-269">Create hello cluster</span></span>
<span data-ttu-id="5eed5-270">Agora você está pronto toocreate cluster de saudação usando [implantação de modelo de recurso do Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="5eed5-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="5eed5-271">Testá-lo</span><span class="sxs-lookup"><span data-stu-id="5eed5-271">Test it</span></span>
<span data-ttu-id="5eed5-272">Olá tootest de comando do PowerShell a seguir ao Use o modelo do Gerenciador de recursos com um arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5eed5-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="5eed5-273">Implantá-lo</span><span class="sxs-lookup"><span data-stu-id="5eed5-273">Deploy it</span></span>
<span data-ttu-id="5eed5-274">Se o teste de modelo do Gerenciador de recursos de Olá passa, use Olá toodeploy de comando do PowerShell a seguir o modelo do Gerenciador de recursos com um arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5eed5-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="5eed5-275">Atribuir usuários tooroles</span><span class="sxs-lookup"><span data-stu-id="5eed5-275">Assign users tooroles</span></span>
<span data-ttu-id="5eed5-276">Depois que você criou Olá aplicativos toorepresent seu cluster, atribuir usuários toohello funções com suporte do Service Fabric: somente leitura e administrador. Você pode atribuir funções hello usando Olá [portal clássico do Azure][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="5eed5-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="5eed5-277">No hello portal do Azure, vá tooyour locatário e, em seguida, selecione **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5eed5-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="5eed5-278">Selecionar aplicativo de web hello, que tem um nome como `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="5eed5-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="5eed5-279">Clique em Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="5eed5-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="5eed5-280">Selecione um usuário tooassign e clique em Olá **atribuir** botão Olá final da tela hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Os usuários tooroles botão atribuir][assign-users-to-roles-button]
5. <span data-ttu-id="5eed5-282">Selecione Olá função tooassign toohello usuário.</span><span class="sxs-lookup"><span data-stu-id="5eed5-282">Select hello role tooassign toohello user.</span></span>

    ![Caixa de diálogo "Atribuir Usuários"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="5eed5-284">Para saber mais sobre as funções no Service Fabric, veja [Controle de acesso baseado em função para clientes do Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5eed5-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="5eed5-285">Criar clusters seguros no Linux</span><span class="sxs-lookup"><span data-stu-id="5eed5-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="5eed5-286">processo de saudação toomake mais fácil, fornecemos um [script auxiliar](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="5eed5-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="5eed5-287">Antes de usar esse script auxiliar, verifique se você já tem a CLI (interface de linha de comando) do Azure instalada e se ele está em seu caminho.</span><span class="sxs-lookup"><span data-stu-id="5eed5-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="5eed5-288">Certifique-se de que o script hello tem permissões tooexecute executando `chmod +x cert_helper.py` após fazer o download.</span><span class="sxs-lookup"><span data-stu-id="5eed5-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="5eed5-289">Olá primeira etapa é toosign em tooyour conta do Azure usando a CLI com hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="5eed5-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="5eed5-290">Depois de entrar no tooyour conta do Azure, use Olá auxiliar script com sua CA certificado autoassinado, como Olá comando mostra a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eed5-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="5eed5-291">parâmetro de IArquivo - Olá pode usar um arquivo. pfx ou. PEM como entrada, com o tipo de certificado da saudação (pfx ou pem ou ss se ele for um certificado autoassinado).</span><span class="sxs-lookup"><span data-stu-id="5eed5-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="5eed5-292">Olá parâmetro -h imprime o texto de ajuda hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="5eed5-293">Esse comando retorna Olá três cadeias de caracteres a seguir como a saída de hello:</span><span class="sxs-lookup"><span data-stu-id="5eed5-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="5eed5-294">SourceVaultID, que é a ID Olá Olá novo KeyVault ResourceGroup ele criado para você</span><span class="sxs-lookup"><span data-stu-id="5eed5-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="5eed5-295">CertificateUrl para acessar o certificado de saudação</span><span class="sxs-lookup"><span data-stu-id="5eed5-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="5eed5-296">CertificateThumbprint, que é usado para autenticação</span><span class="sxs-lookup"><span data-stu-id="5eed5-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="5eed5-297">saudação de exemplo a seguir mostra como toouse Olá comando:</span><span class="sxs-lookup"><span data-stu-id="5eed5-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="5eed5-298">Executando Olá anterior oferece comando você Olá três cadeias de caracteres, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5eed5-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="5eed5-299">nome da entidade do certificado Olá deve corresponder domínio Olá que você use o cluster do tooaccess saudação do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5eed5-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="5eed5-300">Esse correspondente é necessário tooprovide um SSL para pontos de extremidade do gerenciamento do cluster Olá HTTPS e o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="5eed5-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="5eed5-301">Não é possível obter um certificado SSL de uma autoridade de certificação para Olá `.cloudapp.azure.com` domínio.</span><span class="sxs-lookup"><span data-stu-id="5eed5-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="5eed5-302">Você deve obter um nome de domínio personalizado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="5eed5-303">Quando você solicitar um certificado de uma autoridade de certificação, hello nome da entidade do certificado deve corresponder nome de domínio personalizado de saudação que você pode usar para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="5eed5-304">Esses nomes de entidade são entradas Olá necessárias toocreate um cluster do Service Fabric seguro (sem AD do Azure), conforme descrito em [parâmetros de modelo de configurar o Gerenciador de recursos](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="5eed5-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="5eed5-305">Você pode se conectar a cluster seguro toohello seguindo as instruções de saudação para [autenticando o cluster de tooa de acesso de cliente](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5eed5-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="5eed5-306">Os clusters de visualização do Linux não dão suporte à autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5eed5-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="5eed5-307">Você pode atribuir funções de administrador e o cliente conforme descrito em Olá [atribuir funções toousers](#assign-roles) seção.</span><span class="sxs-lookup"><span data-stu-id="5eed5-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="5eed5-308">Quando você especificar funções de administrador e o cliente para um cluster de visualização do Linux, você tem tooprovide impressões digitais de certificado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="5eed5-309">(Você não fornecer nome do assunto hello, porque nenhuma validação de cadeia ou a revogação está sendo executada nessa versão de visualização.)</span><span class="sxs-lookup"><span data-stu-id="5eed5-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="5eed5-310">Se você quiser toouse um certificado autoassinado para testes, você pode usar Olá mesmo toogenerate script um.</span><span class="sxs-lookup"><span data-stu-id="5eed5-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="5eed5-311">É possível carregar o Cofre de chaves Olá certificado tooyour fornecendo sinalizador Olá `ss` em vez de fornecer o nome de caminho e o certificado do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="5eed5-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="5eed5-312">Por exemplo, consulte Olá comando para criar e carregar um certificado autoassinado a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eed5-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="5eed5-313">Esse comando retorna Olá mesmo três cadeias de caracteres: SourceVault, CertificateUrl e CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="5eed5-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="5eed5-314">Você pode usar toocreate de cadeias de caracteres de saudação um cluster Linux seguro e um local onde o certificado autoassinado Olá é colocado.</span><span class="sxs-lookup"><span data-stu-id="5eed5-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="5eed5-315">Pode ser necessário Olá certificado autoassinado tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="5eed5-316">Você pode se conectar a cluster seguro toohello seguindo as instruções de saudação para [autenticando o cluster de tooa de acesso de cliente](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5eed5-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="5eed5-317">nome da entidade do certificado Olá deve corresponder domínio Olá que você use o cluster do tooaccess saudação do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5eed5-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="5eed5-318">Esse correspondente é necessário tooprovide um SSL para pontos de extremidade do gerenciamento do cluster Olá HTTPS e o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="5eed5-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="5eed5-319">Não é possível obter um certificado SSL de uma autoridade de certificação para Olá `.cloudapp.azure.com` domínio.</span><span class="sxs-lookup"><span data-stu-id="5eed5-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="5eed5-320">Você deve obter um nome de domínio personalizado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="5eed5-321">Quando você solicitar um certificado de uma autoridade de certificação, hello nome da entidade do certificado deve corresponder nome de domínio personalizado de saudação que você pode usar para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5eed5-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="5eed5-322">Você pode preencher os parâmetros de saudação do script auxiliar Olá Olá portal do Azure, conforme descrito em Olá [criar um cluster no portal do Azure de saudação](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) seção.</span><span class="sxs-lookup"><span data-stu-id="5eed5-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eed5-323">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5eed5-323">Next steps</span></span>
<span data-ttu-id="5eed5-324">Neste ponto, você tem um cluster seguro com o Azure Active Directory fornecendo autenticação de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="5eed5-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="5eed5-325">Em seguida, [conecte cluster tooyour](service-fabric-connect-to-secure-cluster.md) e saiba como muito[gerenciar segredos do aplicativo](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="5eed5-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="5eed5-326">Solucionar problemas na configuração do Azure Active Directory para autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="5eed5-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="5eed5-327">Se você tiver um problema enquanto você estiver configurando o Azure AD para autenticação de cliente, examine as possíveis soluções Olá nesta seção.</span><span class="sxs-lookup"><span data-stu-id="5eed5-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="5eed5-328">Service Fabric Explorer solicita tooselect um certificado</span><span class="sxs-lookup"><span data-stu-id="5eed5-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="5eed5-329">Problema</span><span class="sxs-lookup"><span data-stu-id="5eed5-329">Problem</span></span>
<span data-ttu-id="5eed5-330">Depois que você entrar com êxito tooAzure AD no Gerenciador do Service Fabric, navegador Olá retorna home page do toohello, mas uma mensagem solicitará que você tooselect um certificado.</span><span class="sxs-lookup"><span data-stu-id="5eed5-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![Caixa de diálogo de seleção de certificado SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="5eed5-332">Motivo</span><span class="sxs-lookup"><span data-stu-id="5eed5-332">Reason</span></span>
<span data-ttu-id="5eed5-333">usuário Olá não está atribuído a uma função no hello aplicativo de cluster do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5eed5-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="5eed5-334">Assim, a autenticação do Azure AD falha no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5eed5-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="5eed5-335">Gerenciador do Service Fabric reverterá toocertificate autenticação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="5eed5-336">Solução</span><span class="sxs-lookup"><span data-stu-id="5eed5-336">Solution</span></span>
<span data-ttu-id="5eed5-337">Siga as instruções de saudação para a configuração do AD do Azure e atribuir funções de usuário.</span><span class="sxs-lookup"><span data-stu-id="5eed5-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="5eed5-338">Além disso, é recomendável que você ativar "Aplicativo de tooaccess necessária de atribuição de usuário", como `SetupApplications.ps1` does.</span><span class="sxs-lookup"><span data-stu-id="5eed5-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="5eed5-339">Conexão com o PowerShell falha com erro: "hello especificado credenciais são inválidas"</span><span class="sxs-lookup"><span data-stu-id="5eed5-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="5eed5-340">Problema</span><span class="sxs-lookup"><span data-stu-id="5eed5-340">Problem</span></span>
<span data-ttu-id="5eed5-341">Quando você usar o PowerShell tooconnect toohello cluster usando o modo de segurança "AzureActiveDirectory", depois que você entra com êxito tooAzure AD, conexão Olá falhará com um erro: "hello especificado credenciais são inválidas."</span><span class="sxs-lookup"><span data-stu-id="5eed5-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="5eed5-342">Solução</span><span class="sxs-lookup"><span data-stu-id="5eed5-342">Solution</span></span>
<span data-ttu-id="5eed5-343">Essa solução é hello que igual Olá precedentes.</span><span class="sxs-lookup"><span data-stu-id="5eed5-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="5eed5-344">O Service Fabric Explorer retorna uma falha quando você entra: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="5eed5-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="5eed5-345">Problema</span><span class="sxs-lookup"><span data-stu-id="5eed5-345">Problem</span></span>
<span data-ttu-id="5eed5-346">Quando você tenta toosign em tooAzure AD no Gerenciador do Service Fabric, página Olá retorna uma falha: "AADSTS50011: Olá endereço de resposta &lt;url&gt; não coincide com os endereços de resposta de saudação configurados para o aplicativo hello: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="5eed5-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![O endereço de resposta SFX não corresponde][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="5eed5-348">Motivo</span><span class="sxs-lookup"><span data-stu-id="5eed5-348">Reason</span></span>
<span data-ttu-id="5eed5-349">aplicativo de cluster (web) Hello que representa o Gerenciador do Service Fabric tentativas tooauthenticate no AD do Azure e como parte da solicitação de saudação fornece Olá URL de retorno de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="5eed5-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="5eed5-350">Mas Olá URL não está listado no aplicativo hello AD do Azure **URL de resposta** lista.</span><span class="sxs-lookup"><span data-stu-id="5eed5-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="5eed5-351">Solução</span><span class="sxs-lookup"><span data-stu-id="5eed5-351">Solution</span></span>
<span data-ttu-id="5eed5-352">Em Olá **configurar** guia da saudação aplicativo (web) do cluster, adicione Olá URL do Gerenciador do Service Fabric toohello **URL de resposta** lista ou substituir um Olá itens na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eed5-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="5eed5-353">Quando terminar, salve a alteração.</span><span class="sxs-lookup"><span data-stu-id="5eed5-353">When you have finished, save your change.</span></span>

![URL de resposta do aplicativo Web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="5eed5-355">Conecte-se o cluster hello usando a autenticação do AD do Azure por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="5eed5-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="5eed5-356">Olá tooconnect cluster do Service Fabric, use Olá exemplo de comando do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eed5-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="5eed5-357">toolearn sobre Olá Connect-ServiceFabricCluster cmdlet, consulte [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="5eed5-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="5eed5-358">Posso reutilizar o locatário Olá mesmo Azure AD em vários clusters?</span><span class="sxs-lookup"><span data-stu-id="5eed5-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="5eed5-359">Sim.</span><span class="sxs-lookup"><span data-stu-id="5eed5-359">Yes.</span></span> <span data-ttu-id="5eed5-360">Mas, lembre-se o aplicativo de cluster (web) tooadd hello URL do Gerenciador do Service Fabric tooyour.</span><span class="sxs-lookup"><span data-stu-id="5eed5-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="5eed5-361">Caso contrário, o Service Fabric Explorer não funcionará.</span><span class="sxs-lookup"><span data-stu-id="5eed5-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="5eed5-362">Por que eu ainda preciso de um certificado de servidor quando o Azure AD está habilitado?</span><span class="sxs-lookup"><span data-stu-id="5eed5-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="5eed5-363">FabricClient e FabricGateway realizam autenticação mútua.</span><span class="sxs-lookup"><span data-stu-id="5eed5-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="5eed5-364">Durante a autenticação do AD do Azure, integração do AD do Azure fornece um cliente para servidor toohello de identidade e certificado do servidor de saudação é a identidade do servidor de saudação tooverify usado.</span><span class="sxs-lookup"><span data-stu-id="5eed5-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="5eed5-365">Para saber mais sobre certificados do Service Fabric, confira [Certificados X.509 e Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="5eed5-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

