---
title: Criar um cluster do Service Fabric no portal do Azure | Microsoft Docs
description: Este artigo descreve como configurar um cluster seguro do Service Fabric no Azure usando o portal do Azure e o Cofre de Chaves do Azure.
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
ms.openlocfilehash: 7dda9520ce3d93bf0e86bd2481ad06c268d087c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="b75e3-103">Criar um cluster do Service Fabric no usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b75e3-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b75e3-104">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="b75e3-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="b75e3-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b75e3-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="b75e3-106">Este é um guia passo a passo que orienta você pelas etapas de configuração de um cluster do Service Fabric seguro no Azure usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b75e3-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="b75e3-107">Este guia apresenta as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b75e3-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="b75e3-108">Configure o Cofre de Chaves para gerenciar chaves para segurança de cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="b75e3-109">Crie um cluster seguro no Azure por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b75e3-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="b75e3-110">Autentique os administradores que usam certificados.</span><span class="sxs-lookup"><span data-stu-id="b75e3-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="b75e3-111">Para obter opções de segurança mais avançadas, como autenticação de usuário com o Azure Active Directory e configurar certificados para a segurança de aplicativo, [crie o cluster usando o Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="b75e3-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="b75e3-112">Um cluster seguro é um cluster que impede o acesso não autorizado às operações de gerenciamento, que inclui implantar, atualizar e excluir aplicativos, serviços e os dados que eles contêm.</span><span class="sxs-lookup"><span data-stu-id="b75e3-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="b75e3-113">Um cluster não seguro é um cluster ao qual qualquer pessoa pode se conectar a qualquer momento e realizar operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="b75e3-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="b75e3-114">Embora seja possível criar um cluster não seguro, é **altamente recomendável criar um cluster seguro**.</span><span class="sxs-lookup"><span data-stu-id="b75e3-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="b75e3-115">Um cluster não seguro **não pode ser protegido posteriormente** - um novo cluster deverá ser criado.</span><span class="sxs-lookup"><span data-stu-id="b75e3-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="b75e3-116">Os conceitos são os mesmos para a criação de clusters seguros, se os clusters são do Linux ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="b75e3-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="b75e3-117">Para obter mais informações e scripts auxiliares para criar clusters do Linux seguras, consulte [Criando clusters seguros no Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="b75e3-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="b75e3-118">Os parâmetros obtidos pelo script auxiliar fornecido podem ser inseridos diretamente no portal, conforme descrito na seção [Criar um cluster no portal do Azure](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="b75e3-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="b75e3-119">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="b75e3-119">Log in to Azure</span></span>
<span data-ttu-id="b75e3-120">Este guia usa o [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="b75e3-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="b75e3-121">Ao iniciar uma nova sessão do PowerShell, faça logon em sua conta do Azure e selecione sua assinatura antes de executar comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b75e3-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="b75e3-122">Faça logon na sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="b75e3-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="b75e3-123">Selecione sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="b75e3-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="b75e3-124">Configurar o Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="b75e3-124">Set up Key Vault</span></span>
<span data-ttu-id="b75e3-125">Esta parte do guia mostra a criação de um Cofre de Chaves para um cluster do Service Fabric no Azure e para aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b75e3-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="b75e3-126">Para obter um guia completo sobre o Key Vault, consulte o [guia de introdução ao Key Vault][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="b75e3-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="b75e3-127">O Service Fabric usa certificados x. 509 para proteger um cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="b75e3-128">O Cofre de Chaves do Azure é usado para gerenciar certificados para clusters do Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="b75e3-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="b75e3-129">Quando um cluster é implantado no Azure, o provedor de recursos do Azure responsável pela criação de clusters do Service Fabric recebe certificados do Cofre de Chaves e os instala nas VMs do cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="b75e3-130">O diagrama a seguir ilustra o relacionamento entre o Cofre de Chaves, um cluster do Service Fabric e o provedor de recursos do Azure que usa certificados armazenados no Cofre de Chaves quando ele cria um cluster:</span><span class="sxs-lookup"><span data-stu-id="b75e3-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="b75e3-132">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b75e3-132">Create a Resource Group</span></span>
<span data-ttu-id="b75e3-133">A primeira etapa é criar um novo grupo de recursos especificamente para o Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="b75e3-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="b75e3-134">Colocar o Cofre de Chaves em seu próprio grupo de recursos é recomendado para que você possa remover grupos de recursos de computação e armazenamento, como o grupo de recursos com o cluster do Service Fabric - sem perder suas chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="b75e3-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="b75e3-135">O grupo de recursos com o Cofre de Chaves deve estar na mesma região que o cluster que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="b75e3-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="b75e3-136">Criar Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="b75e3-136">Create Key Vault</span></span>
<span data-ttu-id="b75e3-137">Crie um Cofre de Chaves no novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b75e3-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="b75e3-138">O Cofre de Chaves **deve estar habilitado para implantação** para permitir que o provedor de recursos do Service Fabric obtenha certificados ele e os instale em nós de cluster:</span><span class="sxs-lookup"><span data-stu-id="b75e3-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

<span data-ttu-id="b75e3-139">Se você tiver um Cofre de Chaves existente, poderá habilitá-lo para implantação usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="b75e3-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="b75e3-140">Adicionar certificados ao Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="b75e3-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="b75e3-141">Os certificados são usados no Service Fabric para fornecer autenticação e criptografia para proteger vários aspectos de um cluster e de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b75e3-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="b75e3-142">Para obter mais informações sobre como os certificados são usados no Service Fabric, consulte [Cenários de segurança do cluster do Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="b75e3-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="b75e3-143">Certificado de cluster e de servidor (necessário)</span><span class="sxs-lookup"><span data-stu-id="b75e3-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="b75e3-144">Esse certificado é necessário para proteger um cluster e impedir o acesso não autorizado a ele.</span><span class="sxs-lookup"><span data-stu-id="b75e3-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="b75e3-145">Ele fornece segurança de cluster de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="b75e3-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="b75e3-146">**Autenticação do cluster:** autentica a comunicação de nó para nó para a federação de cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="b75e3-147">Somente os nós que podem provar sua identidade com esse certificado podem ingressar no cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="b75e3-148">**Autenticação de servidor:** autentica os pontos de extremidade de gerenciamento de cluster para um cliente de gerenciamento, para que o gerenciamento do cliente saiba que está se comunicando com o cluster real.</span><span class="sxs-lookup"><span data-stu-id="b75e3-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="b75e3-149">Esse certificado também fornece SSL para a API de gerenciamento de HTTPS e para o Service Fabric Explorer sobre HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b75e3-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="b75e3-150">Para servir a essas finalidades, o certificado deverá atender a estes requisitos:</span><span class="sxs-lookup"><span data-stu-id="b75e3-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="b75e3-151">O certificado deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="b75e3-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="b75e3-152">O certificado deve ser criado para troca de chaves, exportável para um arquivo Troca de Informações Pessoais (.pfx).</span><span class="sxs-lookup"><span data-stu-id="b75e3-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="b75e3-153">O nome de assunto do certificado deve corresponder ao domínio usado para acessar o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b75e3-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="b75e3-154">Isso é necessário para fornecer SSL para pontos de extremidade de gerenciamento de HTTPS e Service Fabric Explorer do cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="b75e3-155">Você não pode obter um certificado SSL de uma autoridade de certificação (CA) para o domínio `.cloudapp.azure.com` .</span><span class="sxs-lookup"><span data-stu-id="b75e3-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="b75e3-156">Adquira um nome de domínio personalizado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="b75e3-157">Quando você solicitar um certificado de uma autoridade de certificação, o nome de assunto do certificado deve corresponder ao nome de domínio personalizado usado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="b75e3-158">Certificados de autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="b75e3-158">Client authentication certificates</span></span>
<span data-ttu-id="b75e3-159">Os certificados de cliente adicionais autenticam os administradores para tarefas de gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="b75e3-160">O Service Fabric tem dois níveis de acesso: **administrador** e **usuário somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="b75e3-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="b75e3-161">No mínimo, um único certificado para acesso administrativo deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="b75e3-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="b75e3-162">Para acesso de nível de usuário adicional, deve ser fornecido um certificado diferente.</span><span class="sxs-lookup"><span data-stu-id="b75e3-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="b75e3-163">Para obter mais informações sobre as funções de acesso, consulte [Controle de acesso baseado em função para clientes do Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="b75e3-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="b75e3-164">Você não precisa carrear os certificados de autenticação do cliente no Cofre de Chaves para trabalhar com o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b75e3-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="b75e3-165">Esses certificados só precisam ser fornecido para os usuários autorizados para gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="b75e3-166">O Azure Active Directory é a maneira recomendada para autenticar clientes para operações de gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-166">Azure Active Directory is the recommended way to authenticate clients for cluster management operations.</span></span> <span data-ttu-id="b75e3-167">Para usar o Azure Active Directory, é necessário [criar um cluster usando o Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="b75e3-167">To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="b75e3-168">Certificados de aplicativo (opcionais)</span><span class="sxs-lookup"><span data-stu-id="b75e3-168">Application certificates (optional)</span></span>
<span data-ttu-id="b75e3-169">Qualquer número de certificados adicionais pode ser instalado em um cluster para fins de segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b75e3-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="b75e3-170">Antes de criar o cluster, considere os cenários de segurança de aplicativos que exigem um certificado a ser instalado em nós, como:</span><span class="sxs-lookup"><span data-stu-id="b75e3-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="b75e3-171">Criptografia e descriptografia de valores de configuração de aplicativo</span><span class="sxs-lookup"><span data-stu-id="b75e3-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="b75e3-172">Criptografia de dados entre nós durante a replicação</span><span class="sxs-lookup"><span data-stu-id="b75e3-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="b75e3-173">Os certificados do aplicativo não podem ser configurados durante a criação de um cluster por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b75e3-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="b75e3-174">Para configurar certificados de aplicativo durante a instalação do cluster, é necessário [criar um cluster usando o Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="b75e3-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="b75e3-175">Você também pode adicionar certificados do aplicativo ao cluster após ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="b75e3-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="b75e3-176">Formatação de certificados para uso do provedor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="b75e3-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="b75e3-177">Os arquivos de chave privada (.pfx) podem ser adicionados e usados diretamente por meio do Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="b75e3-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="b75e3-178">No entanto, o provedor de recursos do Azure requer chaves para ser armazenado em um formato JSON especial que inclui o .pfx como uma cadeia de caracteres codificada em base 64 e a senha da chave privada.</span><span class="sxs-lookup"><span data-stu-id="b75e3-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="b75e3-179">Para acomodar esses requisitos, as chaves deverão ser colocadas em uma cadeia de caracteres JSON e então armazenadas como *segredos* no Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="b75e3-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="b75e3-180">Para facilitar esse processo, um módulo do PowerShell está [disponível no GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="b75e3-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="b75e3-181">Siga estas etapas para usar o módulo:</span><span class="sxs-lookup"><span data-stu-id="b75e3-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="b75e3-182">Baixe todo o conteúdo do repositório em um diretório local.</span><span class="sxs-lookup"><span data-stu-id="b75e3-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="b75e3-183">Importe o módulo na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b75e3-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="b75e3-184">O comando `Invoke-AddCertToKeyVault` neste módulo do PowerShell formata automaticamente uma chave privada do certificado em uma cadeia de caracteres JSON e a carrega no Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="b75e3-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="b75e3-185">Use-o para adicionar o certificado do cluster e todos os certificados adicionais de aplicativos para o Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="b75e3-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="b75e3-186">Repita esta etapa para todos os certificados adicionais que deseja instalar em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="b75e3-187">Esses são todos os pré-requisitos do Cofre de Chaves para configurar um modelo do Resource Manager de cluster do Service Fabric que instala certificados para autenticação de nó, autenticação e segurança de ponto de extremidade de gerenciamento e recursos de segurança adicionais de aplicativos que usam certificados x.509.</span><span class="sxs-lookup"><span data-stu-id="b75e3-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="b75e3-188">Neste ponto, agora você deve ter a seguinte configuração no Azure:</span><span class="sxs-lookup"><span data-stu-id="b75e3-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="b75e3-189">Grupo de recursos do Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="b75e3-189">Key Vault resource group</span></span>
  * <span data-ttu-id="b75e3-190">Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="b75e3-190">Key Vault</span></span>
    * <span data-ttu-id="b75e3-191">Certificado de autenticação de servidor de cluster</span><span class="sxs-lookup"><span data-stu-id="b75e3-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="b75e3-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="b75e3-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="b75e3-193">Criar um cluster no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b75e3-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="b75e3-194">Pesquise o recurso de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b75e3-194">Search for the Service Fabric cluster resource</span></span>
![pesquisa pelo modelo de cluster do Service Fabric no portal do Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="b75e3-196">Entre no [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b75e3-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="b75e3-197">Clique em **+ Novo** para adicionar um novo modelo de recurso.</span><span class="sxs-lookup"><span data-stu-id="b75e3-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="b75e3-198">Procure o modelo Cluster do Service Fabric no **Marketplace** em **Tudo**.</span><span class="sxs-lookup"><span data-stu-id="b75e3-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="b75e3-199">Selecione **Cluster do Service Fabric** na lista.</span><span class="sxs-lookup"><span data-stu-id="b75e3-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="b75e3-200">Navegue até a folha **Cluster do Service Fabric** e clique em **Criar**,</span><span class="sxs-lookup"><span data-stu-id="b75e3-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="b75e3-201">A folha **Criar cluster do Service Fabric** tem as quatro etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="b75e3-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="b75e3-202">1. Noções básicas</span><span class="sxs-lookup"><span data-stu-id="b75e3-202">1. Basics</span></span>
![Captura de tela da criação de um novo grupo de recursos.][CreateRG]

<span data-ttu-id="b75e3-204">Na folha Básico, você precisa fornecer os detalhes básicos do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="b75e3-205">Insira o nome do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="b75e3-206">Insira um **nome de usuário** e uma **senha** para a Área de Trabalho Remota para as VMs.</span><span class="sxs-lookup"><span data-stu-id="b75e3-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="b75e3-207">Selecione a **Assinatura** desejada para a implantação do cluster, especialmente se você tiver várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="b75e3-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="b75e3-208">Crie um **novo grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="b75e3-208">Create a **new resource group**.</span></span> <span data-ttu-id="b75e3-209">É melhor dar a ele o mesmo nome do cluster, pois ajuda a encontrá-los mais tarde, especialmente quando você estiver tentando fazer alterações em sua implantação ou excluir o cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b75e3-210">Embora você possa optar por usar um grupo de recursos existente, é uma boa prática criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b75e3-210">Although you can decide to use an existing resource group, it is a good practice to create a new resource group.</span></span> <span data-ttu-id="b75e3-211">Isso facilita a exclusão dos clusters que não são necessários.</span><span class="sxs-lookup"><span data-stu-id="b75e3-211">This makes it easy to delete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="b75e3-212">Selecione a **região** ma qual você deseja criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="b75e3-213">Você deve usar a mesma região em que está o Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="b75e3-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="b75e3-214">2. Configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="b75e3-214">2. Cluster configuration</span></span>
![Criar um tipo de nó][CreateNodeType]

<span data-ttu-id="b75e3-216">Configure os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-216">Configure your cluster nodes.</span></span> <span data-ttu-id="b75e3-217">Os tipos de nó definem os tamanhos e o número de VMs e suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="b75e3-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="b75e3-218">O cluster pode ter mais de um tipo de nó, mas o tipo de nó primário (o primeiro que você define no portal) deve ter pelo menos cinco VMs. Esse é o tipo de nó onde os serviços do sistema do Service Fabric são colocados.</span><span class="sxs-lookup"><span data-stu-id="b75e3-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="b75e3-219">Não configure as **Propriedades de Posicionamento**, pois uma propriedade de posicionamento padrão de "NodeTypeName" é adicionada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b75e3-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="b75e3-220">Um cenário comum para vários tipos de nó é um aplicativo que contém um serviço front-end e um serviço back-end.</span><span class="sxs-lookup"><span data-stu-id="b75e3-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="b75e3-221">Você quer colocar o serviço front-end em VMs menores (tamanhos como D2) com portas abertas para a Internet, mas você quer colocar o serviço de back-end em VMs maiores (com tamanhos como D4, D6, D15 e assim por diante) com portas não são voltadas para a Internet abertas.</span><span class="sxs-lookup"><span data-stu-id="b75e3-221">You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="b75e3-222">Escolha um nome para o tipo de nó (um a 12 caracteres contendo somente letras e números).</span><span class="sxs-lookup"><span data-stu-id="b75e3-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="b75e3-223">O **tamanho** mínimo das VMs para o tipo de nó primário é determinado pela camada de **durabilidade** que você escolhe para o cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="b75e3-224">O padrão para a camada de durabilidade é Bronze.</span><span class="sxs-lookup"><span data-stu-id="b75e3-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="b75e3-225">Para obter mais informações sobre durabilidade, consulte [como escolher a durabilidade e confiabilidade do cluster do Service Fabric][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="b75e3-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="b75e3-226">Selecione o tamanho da VM e o tipo de preços.</span><span class="sxs-lookup"><span data-stu-id="b75e3-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="b75e3-227">As VMs da série D têm unidades SSD e são altamente recomendadas para aplicativos com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="b75e3-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="b75e3-228">Não use nenhuma SKU de VM com núcleos parciais ou que tenham menos de 7 GB de capacidade em disco disponível.</span><span class="sxs-lookup"><span data-stu-id="b75e3-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="b75e3-229">O **número** mínimo de VMs para o tipo de nó primário é determinado pela camada de **confiabilidade** que você escolhe.</span><span class="sxs-lookup"><span data-stu-id="b75e3-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="b75e3-230">O padrão para a camada de confiabilidade é Prata.</span><span class="sxs-lookup"><span data-stu-id="b75e3-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="b75e3-231">Para obter mais informações sobre confiabilidade, consulte [como escolher a durabilidade e confiabilidade do cluster do Service Fabric][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="b75e3-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="b75e3-232">Escolha o número de VMs para o tipo de nó.</span><span class="sxs-lookup"><span data-stu-id="b75e3-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="b75e3-233">Você pode escalar ou reduzir verticalmente o número de VMs em um tipo de nó posteriormente, mas no tipo de nó primário, o mínimo é determinado pelo nível de confiabilidade que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="b75e3-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="b75e3-234">Os outros tipos de nó podem ter um mínimo de 1 VM.</span><span class="sxs-lookup"><span data-stu-id="b75e3-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="b75e3-235">Configure pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="b75e3-235">Configure custom endpoints.</span></span> <span data-ttu-id="b75e3-236">Este campo permite que você insira uma lista separada por vírgulas de portas que você deseja expor por meio do Azure Load Balancer para a Internet pública para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b75e3-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="b75e3-237">Por exemplo, se você planeja implantar um aplicativo web para o cluster, insira "80" aqui para permitir o tráfego na porta 80 em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="b75e3-238">Para obter mais informações sobre pontos de extremidade, consulte [Comunicando-se com aplicativos][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="b75e3-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="b75e3-239">Configure o **diagnóstico**do cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="b75e3-240">Por padrão, os diagnósticos são habilitados no cluster para ajudar na solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="b75e3-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="b75e3-241">Se quiser desabilitar o diagnóstico, alterne o **Status** para **Desligado**.</span><span class="sxs-lookup"><span data-stu-id="b75e3-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="b75e3-242">**Não** é recomendável desligar o diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b75e3-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="b75e3-243">Selecione o modo de atualização do Fabric para o qual você deseja definir o cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="b75e3-244">Selecione **Automático**, se você desejar que o sistema automaticamente obtenha a versão mais recente e tente atualizar o cluster para ela.</span><span class="sxs-lookup"><span data-stu-id="b75e3-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="b75e3-245">Defina o modo como **Manual**, se você desejar escolher uma versão com suporte.</span><span class="sxs-lookup"><span data-stu-id="b75e3-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="b75e3-246">Damos suporte somente para clusters que executam versões com suporte do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b75e3-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="b75e3-247">Selecionando o modo **Manual** , você está assumindo a responsabilidade de atualizar seu cluster para uma versão com suporte.</span><span class="sxs-lookup"><span data-stu-id="b75e3-247">By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version.</span></span> <span data-ttu-id="b75e3-248">Para obter mais detalhes sobre o modo de atualização do Fabric, consulte o documento [Atualizar um cluster do Service Fabric.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="b75e3-248">For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="b75e3-249">3. Segurança</span><span class="sxs-lookup"><span data-stu-id="b75e3-249">3. Security</span></span>
![Captura de tela das configurações de segurança no Portal do Azure][SecurityConfigs]

<span data-ttu-id="b75e3-251">A etapa final é fornecer informações de certificado para proteger o cluster usando o Cofre de Chaves e o certificado informações criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b75e3-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="b75e3-252">Preencha os campos de certificado principal com a saída obtida do carregamento do **certificado do cluster** para o Cofre de Chaves usando o comando `Invoke-AddCertToKeyVault` do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b75e3-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="b75e3-253">Marque a caixa **Definir configurações avançadas** para inserir certificados de cliente para **cliente administrativo** e **cliente somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="b75e3-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="b75e3-254">Nesses campos, insira a impressão digital do seu certificado de cliente do administrador e a impressão digital do seu certificado de cliente do usuário somente leitura, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="b75e3-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="b75e3-255">Quando os administradores tentam se conectar ao cluster, eles só receberão acesso se tiverem um certificado com uma impressão digital que corresponda aos valores da impressão digital inseridos aqui.</span><span class="sxs-lookup"><span data-stu-id="b75e3-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="b75e3-256">4. Resumo</span><span class="sxs-lookup"><span data-stu-id="b75e3-256">4. Summary</span></span>
![<span data-ttu-id="b75e3-257">Captura de tela da Tela Inicial exibindo "Implantação do cluster do Service Fabric".</span><span class="sxs-lookup"><span data-stu-id="b75e3-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="b75e3-258">Para concluir a criação do cluster, clique em **Resumo** para ver as configurações que você forneceu ou baixe o modelo do Azure Resource Manager que será usado para implantar o cluster.</span><span class="sxs-lookup"><span data-stu-id="b75e3-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="b75e3-259">Depois de ter fornecido as configurações obrigatórias, o botão **OK** fica verde e você pode começar o processo de criação do cluster clicando nele.</span><span class="sxs-lookup"><span data-stu-id="b75e3-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="b75e3-260">Você pode ver o progresso da criação nas notificações.</span><span class="sxs-lookup"><span data-stu-id="b75e3-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="b75e3-261">(Clique no ícone de "Sino" próximo à barra de status no canto superior direito da tela). Se você clicou em **Fixar no Quadro Inicial** durante a criação do cluster, verá **Implantando o Cluster do Service Fabric** fixado na **Tela Inicial**.</span><span class="sxs-lookup"><span data-stu-id="b75e3-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="b75e3-262">Exibir o status do cluster</span><span class="sxs-lookup"><span data-stu-id="b75e3-262">View your cluster status</span></span>
![Captura de tela dos detalhes do cluster no painel de controle.][ClusterDashboard]

<span data-ttu-id="b75e3-264">Depois que o cluster for criado, você poderá inspecioná-lo no portal:</span><span class="sxs-lookup"><span data-stu-id="b75e3-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="b75e3-265">Vá para **Procurar** e clique em **Clusters do Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="b75e3-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="b75e3-266">Localize o cluster e clique nele.</span><span class="sxs-lookup"><span data-stu-id="b75e3-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="b75e3-267">Agora você pode ver os detalhes do cluster no painel, inclusive o ponto de extremidade público do cluster e um link para o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b75e3-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="b75e3-268">A seção **Monitor do Nó** na folha do painel do cluster indica o número de VMs íntegras e não íntegras.</span><span class="sxs-lookup"><span data-stu-id="b75e3-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="b75e3-269">Encontre mais detalhes sobre a integridade do cluster em [Introdução ao monitoramento da integridade do Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="b75e3-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="b75e3-270">Os clusters de Service Fabric exigem um determinado número de nós esteja sempre ativo para manter a disponibilidade e preservar o estado – conhecido como "manter o quórum".</span><span class="sxs-lookup"><span data-stu-id="b75e3-270">Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum".</span></span> <span data-ttu-id="b75e3-271">Portanto, normalmente não é seguro desligar todos os computadores no cluster, a menos que você tenha primeiro feito um [backup completo do estado][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="b75e3-271">Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="b75e3-272">Conectar remotamente a uma instância do Conjunto de Escala de Máquinas Virtuais ou a um nó de cluster</span><span class="sxs-lookup"><span data-stu-id="b75e3-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="b75e3-273">Cada um dos NodeTypes que você especifica no cluster resulta na configuração de um Conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b75e3-273">Each of the NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="b75e3-274">Consulte [Conectar-se remotamente a uma instância do Conjunto de dimensionamento de máquinas virtuais][remote-connect-to-a-vm-scale-set] para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="b75e3-274">See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b75e3-275">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b75e3-275">Next steps</span></span>
<span data-ttu-id="b75e3-276">Neste ponto, você tem um cluster seguro usando certificados para autenticação de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="b75e3-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="b75e3-277">Em seguida, [conecte-se ao cluster](service-fabric-connect-to-secure-cluster.md) e saiba como [gerenciar segredos do aplicativo](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="b75e3-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="b75e3-278">Além disso, saiba mais sobre as [Azure Service Fabric support options](service-fabric-support.md) (Opções de suporte do Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="b75e3-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

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
