---
title: "aaaCreate malha do serviço de cluster no hello portal do Azure | Microsoft Docs"
description: "Este artigo descreve como tooset um cluster do Service Fabric segura no Azure usando Olá portal do Azure e o Azure Key Vault."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="1057b-103">Criar um cluster do Service Fabric no Azure usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1057b-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1057b-104">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="1057b-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="1057b-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1057b-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="1057b-106">Este é um guia passo a passo que guiará você pelas etapas de saudação de configuração de um cluster do Service Fabric seguro no Azure usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1057b-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="1057b-107">Este guia aborda Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1057b-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="1057b-108">Configure chaves do Cofre de chaves toomanage para segurança de cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="1057b-109">Crie um cluster protegido no Azure por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1057b-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="1057b-110">Autentique os administradores que usam certificados.</span><span class="sxs-lookup"><span data-stu-id="1057b-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="1057b-111">Para obter opções de segurança mais avançadas, como autenticação de usuário com o Azure Active Directory e configurar certificados para a segurança de aplicativo, [crie o cluster usando o Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="1057b-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="1057b-112">Um cluster seguro é um cluster que impede que as operações de toomanagement de acesso não autorizado, que inclui a implantar, atualizar e excluir dados Olá que eles contêm, serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1057b-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="1057b-113">Um cluster não seguro é um cluster que qualquer pessoa pode se conectar tooat a qualquer momento e executar operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1057b-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="1057b-114">Embora seja possível toocreate um cluster não seguro, é **altamente recomendável toocreate um cluster seguro**.</span><span class="sxs-lookup"><span data-stu-id="1057b-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="1057b-115">Um cluster não seguro **não pode ser protegido posteriormente** - um novo cluster deverá ser criado.</span><span class="sxs-lookup"><span data-stu-id="1057b-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="1057b-116">conceitos de saudação são Olá mesmo para a criação de clusters seguros, clusters de saudação são clusters do Linux ou clusters do Windows.</span><span class="sxs-lookup"><span data-stu-id="1057b-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="1057b-117">Para obter mais informações e scripts auxiliares para criar clusters do Linux seguras, consulte [Criando clusters seguros no Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="1057b-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="1057b-118">Olá parâmetros obtidos pelo script de auxiliar Olá fornecida podem ser inseridos diretamente no portal de saudação conforme descrito na seção de saudação [criar um cluster no portal do Azure de saudação](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="1057b-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="1057b-119">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="1057b-119">Log in tooAzure</span></span>
<span data-ttu-id="1057b-120">Este guia usa o [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="1057b-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="1057b-121">Ao iniciar uma nova sessão do PowerShell, faça logon no tooyour conta do Azure e selecione sua assinatura antes de executar comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1057b-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="1057b-122">Faça logon na conta tooyour do azure:</span><span class="sxs-lookup"><span data-stu-id="1057b-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1057b-123">Selecione sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="1057b-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="1057b-124">Configurar o Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="1057b-124">Set up Key Vault</span></span>
<span data-ttu-id="1057b-125">Esta parte do guia de saudação orienta a criação de um cofre de chaves para um cluster do Service Fabric no Azure e para aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1057b-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="1057b-126">Para obter um guia completo no cofre de chaves, consulte Olá [guia de Introdução ao Cofre de chaves][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="1057b-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="1057b-127">Serviço de malha usa toosecure de certificados x. 509 um cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="1057b-128">Cofre de chaves do Azure é toomanage usados certificados para clusters de malha do serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="1057b-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="1057b-129">Quando um cluster é implantado no Azure, o provedor de recursos do Azure de saudação responsável pela criação de clusters Service Fabric recebe certificados de Cofre de chaves e instala-os em máquinas virtuais do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1057b-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="1057b-130">Olá diagrama a seguir ilustra a relação Olá entre Cofre de chaves, um cluster do Service Fabric e o provedor de recursos do Azure Olá que usa certificados armazenados no cofre de chaves ao criar um cluster:</span><span class="sxs-lookup"><span data-stu-id="1057b-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="1057b-132">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1057b-132">Create a Resource Group</span></span>
<span data-ttu-id="1057b-133">Olá primeira etapa é toocreate um novo grupo de recursos especificamente para o Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="1057b-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="1057b-134">Colocar chave de cofre em seu próprio grupo de recursos é recomendado para que você possa remover grupos de recursos de computação e armazenamento - como o grupo de recursos de saudação que tem o cluster do Service Fabric - sem perder suas chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="1057b-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="1057b-135">grupo de recursos de saudação que tem seu Cofre de chaves deve estar no hello mesma região Olá cluster que está em uso.</span><span class="sxs-lookup"><span data-stu-id="1057b-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="1057b-136">Criar Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="1057b-136">Create Key Vault</span></span>
<span data-ttu-id="1057b-137">Crie um cofre de chaves no novo grupo de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="1057b-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="1057b-138">Olá Cofre de chaves **deve ser habilitado para implantação** tooallow Olá certificados de tooget de provedor de recursos de malha do serviço-lo e instalar em nós de cluster:</span><span class="sxs-lookup"><span data-stu-id="1057b-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
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

<span data-ttu-id="1057b-139">Se você tiver um Cofre de Chaves existente, poderá habilitá-lo para implantação usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="1057b-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="1057b-140">Adicionar certificados tooKey cofre</span><span class="sxs-lookup"><span data-stu-id="1057b-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="1057b-141">Os certificados são usados em Service Fabric tooprovide toosecure de autenticação e criptografia vários aspectos de um cluster e seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1057b-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="1057b-142">Para obter mais informações sobre como os certificados são usados no Service Fabric, consulte [Cenários de segurança do cluster do Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="1057b-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="1057b-143">Certificado de cluster e de servidor (necessário)</span><span class="sxs-lookup"><span data-stu-id="1057b-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="1057b-144">Esse certificado é necessário toosecure um cluster e impedir o acesso não autorizado tooit.</span><span class="sxs-lookup"><span data-stu-id="1057b-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="1057b-145">Ele fornece segurança de cluster de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="1057b-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="1057b-146">**Autenticação do cluster:** autentica a comunicação de nó para nó para a federação de cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="1057b-147">Somente nós que podem provar sua identidade com esse certificado podem ingressar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1057b-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="1057b-148">**Autenticação de servidor:** autentica o cliente de gerenciamento do tooa pontos de extremidade do hello cluster management, para que hello gerenciamento cliente sabe que está se comunicando cluster real toohello.</span><span class="sxs-lookup"><span data-stu-id="1057b-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="1057b-149">Este certificado também fornece SSL para Olá API de gerenciamento de HTTPS e Service Fabric Explorer via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1057b-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="1057b-150">tooserve esses fins, Olá certificado deve atender a saudação requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1057b-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="1057b-151">certificado de saudação deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="1057b-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="1057b-152">certificado de saudação deve ser criado para troca de chaves, exportável tooa arquivo de troca de informações pessoais (. pfx).</span><span class="sxs-lookup"><span data-stu-id="1057b-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="1057b-153">Olá nome da entidade do certificado deve corresponder Olá domínio usado tooaccess Olá malha do serviço cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="1057b-154">Isso é necessário tooprovide SSL para pontos de extremidade de gerenciamento de HTTPS e o Gerenciador do Service Fabric do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1057b-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="1057b-155">Não é possível obter um certificado SSL de uma autoridade de certificação (CA) Olá `.cloudapp.azure.com` domínio.</span><span class="sxs-lookup"><span data-stu-id="1057b-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="1057b-156">Adquira um nome de domínio personalizado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="1057b-157">Quando você solicitar um certificado do nome da entidade do certificado de saudação uma autoridade de certificação deve corresponder a nome de domínio personalizado Olá usado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="1057b-158">Certificados de autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="1057b-158">Client authentication certificates</span></span>
<span data-ttu-id="1057b-159">Os certificados de cliente adicionais autenticam os administradores para tarefas de gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="1057b-160">O Service Fabric tem dois níveis de acesso: **administrador** e **usuário somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="1057b-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="1057b-161">No mínimo, um único certificado para acesso administrativo deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="1057b-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="1057b-162">Para acesso de nível de usuário adicional, deve ser fornecido um certificado diferente.</span><span class="sxs-lookup"><span data-stu-id="1057b-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="1057b-163">Para obter mais informações sobre as funções de acesso, consulte [Controle de acesso baseado em função para clientes do Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="1057b-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="1057b-164">Não é necessário tooupload cliente autenticação certificados tooKey cofre toowork com o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1057b-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="1057b-165">Esses certificados só precisam toobe fornecida toousers autorizados para o gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="1057b-166">Active Directory do Azure é Olá operações de gerenciamento de clientes de tooauthenticate de maneira para cluster recomendada.</span><span class="sxs-lookup"><span data-stu-id="1057b-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="1057b-167">toouse Active Directory do Azure, você deve [criar um cluster usando o Gerenciador de recursos do Azure][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="1057b-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="1057b-168">Certificados de aplicativo (opcionais)</span><span class="sxs-lookup"><span data-stu-id="1057b-168">Application certificates (optional)</span></span>
<span data-ttu-id="1057b-169">Qualquer número de certificados adicionais pode ser instalado em um cluster para fins de segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1057b-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="1057b-170">Antes de criar o cluster, considere os cenários de segurança de aplicativo hello que exigem um toobe certificado instalado em nós hello, como:</span><span class="sxs-lookup"><span data-stu-id="1057b-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="1057b-171">Criptografia e descriptografia de valores de configuração de aplicativo</span><span class="sxs-lookup"><span data-stu-id="1057b-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="1057b-172">Criptografia de dados entre nós durante a replicação</span><span class="sxs-lookup"><span data-stu-id="1057b-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="1057b-173">Certificados de aplicativo não podem ser configurados ao criar um cluster por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1057b-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="1057b-174">certificados de aplicativo tooconfigure no momento da instalação de cluster, você deve [criar um cluster usando o Gerenciador de recursos do Azure][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="1057b-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="1057b-175">Você também pode adicionar o cluster de toohello de certificados do aplicativo após ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="1057b-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="1057b-176">Formatação de certificados para uso do provedor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="1057b-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="1057b-177">Os arquivos de chave privada (.pfx) podem ser adicionados e usados diretamente por meio do Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="1057b-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="1057b-178">No entanto, o provedor de recursos do Azure Olá requer toobe chaves armazenada em um formato JSON especial que inclui o. pfx de saudação como uma base 64 codificados hello e cadeia de caracteres de senha da chave privada.</span><span class="sxs-lookup"><span data-stu-id="1057b-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="1057b-179">tooaccommodate esses requisitos, as chaves devem ser colocados em uma cadeia de caracteres JSON e, em seguida, são armazenados como *segredos* no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="1057b-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="1057b-180">toomake esse processo mais fácil, um módulo do PowerShell é [disponível no GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="1057b-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="1057b-181">Execute o módulo de saudação de toouse essas etapas:</span><span class="sxs-lookup"><span data-stu-id="1057b-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="1057b-182">Baixe todo o conteúdo do repositório de Olá Olá em um diretório local.</span><span class="sxs-lookup"><span data-stu-id="1057b-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="1057b-183">Importe o módulo de saudação na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1057b-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="1057b-184">Olá `Invoke-AddCertToKeyVault` comando neste módulo PowerShell formata uma chave privada do certificado em uma cadeia de caracteres JSON e carrega tooKey cofre automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1057b-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="1057b-185">Use-certificado de cluster Olá tooadd e quaisquer certificados de aplicativo adicionais tooKey cofre.</span><span class="sxs-lookup"><span data-stu-id="1057b-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="1057b-186">Repita essa etapa para todos os certificados adicionais que você deseja tooinstall em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="1057b-187">Esses são todos os pré-requisitos de Cofre de chaves Olá para configurar um modelo do Gerenciador de recursos de cluster do Service Fabric que instala certificados para autenticação de nó, segurança de ponto de extremidade de gerenciamento e autenticação e segurança de todos os aplicativos adicionais recursos que usam certificados x. 509.</span><span class="sxs-lookup"><span data-stu-id="1057b-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="1057b-188">Neste ponto, você deve ter agora Olá após a instalação no Azure:</span><span class="sxs-lookup"><span data-stu-id="1057b-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="1057b-189">Grupo de recursos do Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="1057b-189">Key Vault resource group</span></span>
  * <span data-ttu-id="1057b-190">Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="1057b-190">Key Vault</span></span>
    * <span data-ttu-id="1057b-191">Certificado de autenticação de servidor de cluster</span><span class="sxs-lookup"><span data-stu-id="1057b-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="1057b-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="1057b-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="1057b-193">Criar o cluster no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1057b-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="1057b-194">Pesquisar Olá recurso de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1057b-194">Search for hello Service Fabric cluster resource</span></span>
![Procure o modelo de cluster do Service Fabric em Olá portal do Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="1057b-196">Entrar toohello [portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="1057b-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="1057b-197">Clique em **novo** tooadd um novo modelo de recurso.</span><span class="sxs-lookup"><span data-stu-id="1057b-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="1057b-198">Procure o modelo de Cluster do Service Fabric Olá Olá **Marketplace** em **tudo**.</span><span class="sxs-lookup"><span data-stu-id="1057b-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="1057b-199">Selecione **Cluster do Service Fabric** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1057b-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="1057b-200">Navegue toohello **Cluster do Service Fabric** folha, clique em **criar**,</span><span class="sxs-lookup"><span data-stu-id="1057b-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="1057b-201">Olá **cluster do Service Fabric criar** folha tem Olá quatro etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="1057b-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="1057b-202">1. Noções básicas</span><span class="sxs-lookup"><span data-stu-id="1057b-202">1. Basics</span></span>
![Captura de tela da criação de um novo grupo de recursos.][CreateRG]

<span data-ttu-id="1057b-204">Na folha de Noções básicas de saudação precisar detalhes básicos do tooprovide Olá para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="1057b-205">Insira o nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="1057b-206">Insira um **nome de usuário** e **senha** para a área de trabalho remota para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="1057b-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="1057b-207">Verifique se Olá de tooselect **assinatura** que você deseja que seu toobe cluster implantado, especialmente se você tiver várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="1057b-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="1057b-208">Crie um **novo grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="1057b-208">Create a **new resource group**.</span></span> <span data-ttu-id="1057b-209">É melhor toogive-Olá mesmo nome de cluster hello, pois ela ajuda a localizá-los mais tarde, especialmente quando você está tentando toomake alterações tooyour implantação ou excluir o cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1057b-210">Embora você possa decidir toouse um grupo de recursos existente, é uma boa prática toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1057b-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="1057b-211">Isso torna fácil toodelete clusters que não é necessário.</span><span class="sxs-lookup"><span data-stu-id="1057b-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="1057b-212">Selecione Olá **região** no qual você deseja que o cluster de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="1057b-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="1057b-213">Você deve usar o hello está mesma região que sua chave de cofre em.</span><span class="sxs-lookup"><span data-stu-id="1057b-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="1057b-214">2. Configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="1057b-214">2. Cluster configuration</span></span>
![Criar um tipo de nó][CreateNodeType]

<span data-ttu-id="1057b-216">Configure os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-216">Configure your cluster nodes.</span></span> <span data-ttu-id="1057b-217">Tipos de nós definem tamanhos de VM hello, número de saudação de VMs e suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="1057b-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="1057b-218">O cluster pode ter mais de um tipo de nó, mas o tipo de nó primário hello (Olá a primeira alteração que você definir no portal de saudação) deve ter pelo menos cinco VMs, como esse é o tipo de nó Olá onde os serviços do sistema do Service Fabric são colocados.</span><span class="sxs-lookup"><span data-stu-id="1057b-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="1057b-219">Não configure as **Propriedades de Posicionamento**, pois uma propriedade de posicionamento padrão de "NodeTypeName" é adicionada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1057b-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="1057b-220">Um cenário comum para vários tipos de nó é um aplicativo que contém um serviço front-end e um serviço back-end.</span><span class="sxs-lookup"><span data-stu-id="1057b-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="1057b-221">Você deseja tooput serviço front-end do hello em VMs menores (tamanhos de VM como D2) com portas abertas toohello da Internet, mas deseja tooput serviço de back-end de saudação em VMs maior (com tamanhos de VM como D4, D6, D15 e assim por diante) sem abrir de portas para a Internet.</span><span class="sxs-lookup"><span data-stu-id="1057b-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="1057b-222">Escolha um nome para o tipo de nó (1 too12 caracteres que contém apenas letras e números).</span><span class="sxs-lookup"><span data-stu-id="1057b-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="1057b-223">Olá mínimo **tamanho** de VMs de nó primário Olá tipo é orientado por Olá **durabilidade** camada que você escolher para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1057b-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="1057b-224">saudação padrão da camada de durabilidade de saudação é bronze.</span><span class="sxs-lookup"><span data-stu-id="1057b-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="1057b-225">Para obter mais informações sobre a durabilidade, consulte [como toochoose Olá malha do serviço de cluster confiabilidade e durabilidade][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="1057b-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="1057b-226">Selecione o tamanho da VM hello e preço.</span><span class="sxs-lookup"><span data-stu-id="1057b-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="1057b-227">As VMs da série D têm unidades SSD e são altamente recomendadas para aplicativos com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="1057b-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="1057b-228">Não use nenhuma SKU de VM com núcleos parciais ou que tenham menos de 7 GB de capacidade em disco disponível.</span><span class="sxs-lookup"><span data-stu-id="1057b-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="1057b-229">Olá mínimo **número** de VMs de nó primário Olá tipo é orientado por Olá **confiabilidade** camada que você escolher.</span><span class="sxs-lookup"><span data-stu-id="1057b-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="1057b-230">saudação padrão da camada de confiabilidade de saudação é prata.</span><span class="sxs-lookup"><span data-stu-id="1057b-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="1057b-231">Para obter mais informações sobre a confiabilidade, consulte [como toochoose Olá malha do serviço de cluster confiabilidade e durabilidade][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="1057b-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="1057b-232">Escolha o número de saudação de VMs para o tipo de nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="1057b-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="1057b-233">Você pode expandir ou reduzir o número de saudação de VMs em um tipo de nó mais tarde, mas no tipo de nó primário hello, Olá mínimo é orientada por nível de confiabilidade de saudação que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="1057b-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="1057b-234">Os outros tipos de nó podem ter um mínimo de 1 VM.</span><span class="sxs-lookup"><span data-stu-id="1057b-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="1057b-235">Configure pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="1057b-235">Configure custom endpoints.</span></span> <span data-ttu-id="1057b-236">Este campo permite que você tooenter uma lista separada por vírgulas de portas que você deseja tooexpose por meio de saudação balanceador de carga do Azure toohello Internet pública para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1057b-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="1057b-237">Por exemplo, se você planejar toodeploy um cluster de tooyour de aplicativo da web, digite "80" aqui tooallow tráfego na porta 80 em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="1057b-238">Para obter mais informações sobre pontos de extremidade, consulte [Comunicando-se com aplicativos][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="1057b-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="1057b-239">Configure o **diagnóstico**do cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="1057b-240">Por padrão, os diagnósticos são habilitados no seu tooassist de cluster com a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="1057b-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="1057b-241">Se você desejar alterar de diagnóstico toodisable Olá **Status** alternar muito**Off**.</span><span class="sxs-lookup"><span data-stu-id="1057b-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="1057b-242">**Não** é recomendável desligar o diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="1057b-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="1057b-243">Selecione Olá deseja definir seu cluster o modo de atualização do Fabric.</span><span class="sxs-lookup"><span data-stu-id="1057b-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="1057b-244">Selecione **automáticas**, se você quiser tooautomatically escolha sistema Olá Olá versão mais recente e tente tooupgrade tooit seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="1057b-245">Definir o modo de saudação muito**Manual**, se você quiser toochoose uma versão com suporte.</span><span class="sxs-lookup"><span data-stu-id="1057b-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="1057b-246">Damos suporte somente para clusters que executam versões com suporte do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1057b-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="1057b-247">Selecionando Olá **Manual** modo, você está aproveitando em Olá responsabilidade tooupgrade sua versão de tooa suporte para cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="1057b-248">Para obter mais detalhes sobre o modo de atualização de malha Olá Olá, consulte [documento de serviço-malha-atualização de cluster.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="1057b-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="1057b-249">3. Segurança</span><span class="sxs-lookup"><span data-stu-id="1057b-249">3. Security</span></span>
![Captura de tela das configurações de segurança no Portal do Azure][SecurityConfigs]

<span data-ttu-id="1057b-251">Olá última etapa é cluster tooprovide certificado informações toosecure hello usando hello Cofre de chaves e certificados informações criadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1057b-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="1057b-252">Preencher os campos de certificado principal de saudação à saída de hello obtida Carregando Olá **certificado de cluster** tooKey cofre usando Olá `Invoke-AddCertToKeyVault` comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1057b-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="1057b-253">Verificar Olá **definir configurações avançadas** caixa tooenter certificados de cliente para **cliente administrador** e **cliente somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="1057b-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="1057b-254">Nesses campos, insira a impressão digital de saudação do seu certificado de cliente do administrador e a impressão digital de saudação do seu certificado de cliente do usuário somente leitura, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="1057b-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="1057b-255">Quando os administradores tentam tooconnect toohello cluster, eles recebem acesso somente se tiverem um certificado com uma impressão digital que faz a correspondência de valores de impressão digital Olá inserido aqui.</span><span class="sxs-lookup"><span data-stu-id="1057b-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="1057b-256">4. Resumo</span><span class="sxs-lookup"><span data-stu-id="1057b-256">4. Summary</span></span>
![<span data-ttu-id="1057b-257">Captura de tela de quadro de início Olá exibindo "Implantando Cluster do Service Fabric."</span><span class="sxs-lookup"><span data-stu-id="1057b-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="1057b-258">criação do cluster Olá toocomplete, clique em **resumo** configurações de saudação toosee que você forneceu ou baixa hello Azure Resource Manager modelo que que usada toodeploy seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1057b-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="1057b-259">Depois que você forneceu configurações obrigatórias hello, Olá **Okey** botão ficará verde e você pode iniciar o processo de criação de cluster Olá clicando nele.</span><span class="sxs-lookup"><span data-stu-id="1057b-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="1057b-260">Você pode ver o progresso da criação da saudação em notificações de saudação.</span><span class="sxs-lookup"><span data-stu-id="1057b-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="1057b-261">(Clique ícone de sino"hello" próximo a barra de status de saudação do superior de saudação à direita da tela). Se você clicou **Pin tooStartboard** durante a criação de cluster hello, você verá **implantação de Cluster do Service Fabric** fixado toohello **iniciar** quadro.</span><span class="sxs-lookup"><span data-stu-id="1057b-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="1057b-262">Exibir o status do cluster</span><span class="sxs-lookup"><span data-stu-id="1057b-262">View your cluster status</span></span>
![Captura de tela de detalhes no painel de saudação do cluster.][ClusterDashboard]

<span data-ttu-id="1057b-264">Quando o cluster é criado, você pode inspecionar o cluster no portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="1057b-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="1057b-265">Vá muito**procurar** e clique em **Clusters de malha do serviço**.</span><span class="sxs-lookup"><span data-stu-id="1057b-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="1057b-266">Localize o cluster e clique nele.</span><span class="sxs-lookup"><span data-stu-id="1057b-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="1057b-267">Agora você pode ver detalhes de saudação do cluster no painel hello, incluindo o ponto de extremidade do cluster Olá público e um link de tooService Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="1057b-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="1057b-268">Olá **nó Monitor** seção na folha do painel de controle do cluster Olá indica o número de saudação de máquinas virtuais que estiverem íntegros e não está íntegro.</span><span class="sxs-lookup"><span data-stu-id="1057b-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="1057b-269">Você pode encontrar mais detalhes sobre a integridade do cluster Olá em [introdução de modelo de integridade do Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="1057b-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="1057b-270">Clusters Service Fabric exigem um determinado número de nós toobe sempre toomaintain disponibilidade e preservam o estado - tooas chamado "mantêm o quórum".</span><span class="sxs-lookup"><span data-stu-id="1057b-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="1057b-271">Therfore, geralmente não é seguro tooshut todas as máquinas no cluster hello, a menos que você tiver executado pela primeira vez um [backup completo do estado do seu][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="1057b-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="1057b-272">Conexão remota tooa instância de conjunto de escala de máquina Virtual ou um nó de cluster</span><span class="sxs-lookup"><span data-stu-id="1057b-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="1057b-273">Cada Olá NodeTypes você especificar nos resultados de cluster em um conjunto de escala de máquina Virtual ao obter a configuração.</span><span class="sxs-lookup"><span data-stu-id="1057b-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="1057b-274">Consulte [remoto conecte-se a instância de conjunto de escala de máquinas virtuais de tooa] [ remote-connect-to-a-vm-scale-set] para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="1057b-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1057b-275">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1057b-275">Next steps</span></span>
<span data-ttu-id="1057b-276">Neste ponto, você tem um cluster seguro usando certificados para autenticação de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1057b-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="1057b-277">Em seguida, [conecte cluster tooyour](service-fabric-connect-to-secure-cluster.md) e saiba como muito[gerenciar segredos do aplicativo](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="1057b-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="1057b-278">Além disso, saiba mais sobre as [Azure Service Fabric support options](service-fabric-support.md) (Opções de suporte do Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="1057b-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
