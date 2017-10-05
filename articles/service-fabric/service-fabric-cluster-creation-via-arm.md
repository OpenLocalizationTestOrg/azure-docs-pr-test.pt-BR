---
title: Atualizar um cluster do Azure Service Fabric de um modelo | Microsoft Docs
description: "Este artigo descreve como configurar um cluster seguro do Service Fabric no Azure usando o Azure Resource Manager, o Azure Key Vault e o Azure Active Directory (Azure AD) para autenticação do cliente."
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
ms.openlocfilehash: 420ea486e626763af65a23e49ce04033ea418fb4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="22180-103">Criar um cluster do Service Fabric usando o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22180-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22180-104">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="22180-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="22180-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="22180-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="22180-106">Este guia passo a passo orienta você pela configuração de um cluster do Azure Service Fabric seguro no Azure usando o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22180-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="22180-107">Sabemos que o artigo é longo.</span><span class="sxs-lookup"><span data-stu-id="22180-107">We acknowledge that the article is long.</span></span> <span data-ttu-id="22180-108">No entanto, a menos que você já esteja totalmente familiarizado com o conteúdo, não deixe de seguir cada etapa com cuidado.</span><span class="sxs-lookup"><span data-stu-id="22180-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span></span>

<span data-ttu-id="22180-109">O guia aborda os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="22180-109">The guide covers the following procedures:</span></span>

* <span data-ttu-id="22180-110">Como configurar um Azure Key Vault para carregar certificados de segurança de aplicativos e cluster</span><span class="sxs-lookup"><span data-stu-id="22180-110">Setting up an Azure key vault to upload certificates for cluster and application security</span></span>
* <span data-ttu-id="22180-111">Como criar um cluster seguro no Azure usando o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22180-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="22180-112">Como autenticar usuários usando o Azure AD (Azure Active Directory) para gerenciamento de cluster</span><span class="sxs-lookup"><span data-stu-id="22180-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="22180-113">Um cluster seguro é um cluster que impede o acesso não autorizado às operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="22180-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span></span> <span data-ttu-id="22180-114">Isso inclui implantação, atualização e exclusão de aplicativos, serviços e dados neles contidos.</span><span class="sxs-lookup"><span data-stu-id="22180-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="22180-115">Um cluster não seguro é um cluster ao qual qualquer pessoa pode se conectar a qualquer momento e realizar operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="22180-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="22180-116">Embora seja possível criar um cluster não seguro, recomendamos que você crie um cluster seguro desde o início.</span><span class="sxs-lookup"><span data-stu-id="22180-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span></span> <span data-ttu-id="22180-117">Um cluster não seguro não pode ser protegido posteriormente; um novo cluster deverá ser criado.</span><span class="sxs-lookup"><span data-stu-id="22180-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="22180-118">O conceito para criar clusters seguros é o mesmo, sejam clusters do Linux ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="22180-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="22180-119">Para obter mais informações e scripts auxiliares para criar clusters do Linux seguras, consulte [Criando clusters seguros no Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="22180-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="22180-120">Entre na sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="22180-120">Sign in to your Azure account</span></span>
<span data-ttu-id="22180-121">Este guia usa o [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="22180-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="22180-122">Ao iniciar uma nova sessão do PowerShell, entre em sua conta do Azure e selecione sua assinatura antes de executar comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="22180-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="22180-123">Entre na sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="22180-123">Sign in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="22180-124">Selecione sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="22180-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="22180-125">Configurar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="22180-125">Set up a key vault</span></span>
<span data-ttu-id="22180-126">Esta seção trata da criação de um cofre de chaves para um cluster do Service Fabric no Azure e para aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22180-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="22180-127">Para obter um guia completo sobre o Azure Key Vault, veja o [Guia de introdução ao Key Vault][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="22180-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="22180-128">O Service Fabric usa certificados x.509 para proteger um cluster e fornecer recursos de segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22180-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span></span> <span data-ttu-id="22180-129">O Key Vault é usado para gerenciar certificados de clusters do Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="22180-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="22180-130">Quando um cluster é implantado no Azure, o provedor de recursos do Azure responsável pela criação de clusters do Service Fabric recebe certificados do Key Vault e os instala nas VMs do cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="22180-131">O diagrama a seguir ilustra o relacionamento entre o Azure Key Vault, um cluster do Service Fabric e o provedor de recursos do Azure que usa certificados armazenados em um cofre de chaves quando ele cria um cluster:</span><span class="sxs-lookup"><span data-stu-id="22180-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagrama da instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="22180-133">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="22180-133">Create a resource group</span></span>
<span data-ttu-id="22180-134">A primeira etapa é criar um grupo de recursos especificamente para o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-134">The first step is to create a resource group specifically for your key vault.</span></span> <span data-ttu-id="22180-135">Recomendamos que você coloque o cofre de chaves em seu próprio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="22180-135">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="22180-136">Essa ação permite que você remova os grupos de recursos de computação e armazenamento, incluindo o grupo de recursos que contém o cluster do Service Fabric sem perder suas chaves e seus segredos.</span><span class="sxs-lookup"><span data-stu-id="22180-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="22180-137">O grupo de recursos que contém o cofre de chaves _tem que estar na mesma região_ que o cluster que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="22180-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span></span>

<span data-ttu-id="22180-138">Se você planeja implantar clusters em várias regiões, sugerimos que você nomeie o grupo de recursos e o cofre de chaves de forma a indicar a qual região eles pertencem.</span><span class="sxs-lookup"><span data-stu-id="22180-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="22180-139">O resultado deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="22180-139">The output should look like this:</span></span>

```powershell

    WARNING: The output object type of this cmdlet is going to be modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-the-new-resource-group"></a><span data-ttu-id="22180-140">Crie um cofre de chaves no novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="22180-140">Create a key vault in the new resource group</span></span>
<span data-ttu-id="22180-141">O cofre de chaves _tem que estar habilitado para implantação_ para permitir que o provedor de recursos de computação obtenha certificados e os instale em instâncias de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="22180-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="22180-142">O resultado deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="22180-142">The output should look like this:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="22180-143">Usar um cofre de chave existente</span><span class="sxs-lookup"><span data-stu-id="22180-143">Use an existing key vault</span></span>

<span data-ttu-id="22180-144">Para usar um cofre de chaves existente, você _tem habilitá-lo para implantação_ a fim de permitir que o provedor de recursos de computação obtenha certificados e os instale em nós de cluster:</span><span class="sxs-lookup"><span data-stu-id="22180-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-to-your-key-vault"></a><span data-ttu-id="22180-145">Adicionar certificados ao cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="22180-145">Add certificates to your key vault</span></span>

<span data-ttu-id="22180-146">Os certificados são usados no Service Fabric para fornecer autenticação e criptografia para proteger vários aspectos de um cluster e de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="22180-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="22180-147">Para obter mais informações sobre como os certificados são usados no Service Fabric, consulte [Cenários de segurança do cluster do Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="22180-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="22180-148">Certificado de cluster e de servidor (necessário)</span><span class="sxs-lookup"><span data-stu-id="22180-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="22180-149">Esse certificado é necessário para proteger um cluster e impedir o acesso não autorizado a ele.</span><span class="sxs-lookup"><span data-stu-id="22180-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="22180-150">Ele fornece segurança de cluster de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="22180-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="22180-151">Autenticação do cluster: autentica a comunicação de nó para nó para a federação de cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="22180-152">Somente os nós que podem provar sua identidade com esse certificado podem ingressar no cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-152">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="22180-153">Autenticação de servidor: autentica os pontos de extremidade de gerenciamento de cluster para um cliente de gerenciamento, para que o gerenciamento do cliente saiba que está se comunicando com o cluster real.</span><span class="sxs-lookup"><span data-stu-id="22180-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="22180-154">Esse certificado também fornece um SSL para a API de gerenciamento de HTTPS e para o Service Fabric Explorer sobre HTTPS.</span><span class="sxs-lookup"><span data-stu-id="22180-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="22180-155">Para servir a essas finalidades, o certificado deverá atender a estes requisitos:</span><span class="sxs-lookup"><span data-stu-id="22180-155">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="22180-156">O certificado deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="22180-156">The certificate must contain a private key.</span></span>
* <span data-ttu-id="22180-157">O certificado deve ser criado para troca de chaves, que deve ser exportável para um arquivo Troca de Informações Pessoais (.pfx).</span><span class="sxs-lookup"><span data-stu-id="22180-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="22180-158">O nome da referência do certificado deve corresponder ao domínio usado para acessar o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22180-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="22180-159">Essa correspondência é necessária para fornecer um SSL para os pontos de extremidade de gerenciamento de HTTPS e o Service Fabric Explorer do cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="22180-160">Você não pode obter um certificado SSL de uma AC (autoridade de certificação) para o domínio cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="22180-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span></span> <span data-ttu-id="22180-161">Você deve obter um nome de domínio personalizado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="22180-162">Quando você solicitar um certificado de uma autoridade de certificação, o nome de assunto do certificado deve corresponder ao nome de domínio personalizado usado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="22180-163">Certificados de aplicativo (opcionais)</span><span class="sxs-lookup"><span data-stu-id="22180-163">Application certificates (optional)</span></span>
<span data-ttu-id="22180-164">Qualquer número de certificados adicionais pode ser instalado em um cluster para fins de segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22180-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="22180-165">Antes de criar o cluster, considere os cenários de segurança de aplicativos que exigem um certificado a ser instalado em nós, como:</span><span class="sxs-lookup"><span data-stu-id="22180-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="22180-166">Criptografia e descriptografia de valores de configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22180-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="22180-167">Criptografia de dados entre nós durante a replicação.</span><span class="sxs-lookup"><span data-stu-id="22180-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="22180-168">Formatação de certificados para uso do provedor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="22180-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="22180-169">Você pode adicionar e usar arquivos de chave privada (.pfx) diretamente pelo cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="22180-170">No entanto, o provedor de recursos de computação do Azure requer que as chaves sejam armazenadas em um formato especial JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="22180-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="22180-171">O formato inclui o arquivo .pfx como uma cadeia de caracteres em codificação de base 64 e a senha da chave privada.</span><span class="sxs-lookup"><span data-stu-id="22180-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span></span> <span data-ttu-id="22180-172">Para acomodar esses requisitos, as chaves deverão ser colocadas em uma cadeia de caracteres JSON e então armazenadas como “segredos” no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span></span>

<span data-ttu-id="22180-173">Para facilitar esse processo, um [módulo do PowerShell está disponível no GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="22180-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="22180-174">Para usar o módulo, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="22180-174">To use the module, do the following:</span></span>

1. <span data-ttu-id="22180-175">Baixe todo o conteúdo do repositório em um diretório local.</span><span class="sxs-lookup"><span data-stu-id="22180-175">Download the entire contents of the repo into a local directory.</span></span>
2. <span data-ttu-id="22180-176">Vá para o diretório local.</span><span class="sxs-lookup"><span data-stu-id="22180-176">Go to the local directory.</span></span>
2. <span data-ttu-id="22180-177">Importe o módulo ServiceFabricRPHelpers na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="22180-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="22180-178">O comando `Invoke-AddCertToKeyVault` neste módulo do PowerShell formata automaticamente uma chave privada do certificado em uma cadeia de caracteres JSON e a carrega no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span></span> <span data-ttu-id="22180-179">Use o comando para adicionar o certificado do cluster e todos os certificados adicionais de aplicativos ao cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span></span> <span data-ttu-id="22180-180">Repita esta etapa para todos os certificados adicionais que deseja instalar em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-180">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="22180-181">Carregando um certificado existente</span><span class="sxs-lookup"><span data-stu-id="22180-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="22180-182">Se você receber um erro como o mostrado aqui, provavelmente tem um conflito de URL de recurso.</span><span class="sxs-lookup"><span data-stu-id="22180-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="22180-183">Para resolver o conflito, altere o nome do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-183">To resolve the conflict, change the key vault name.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="22180-184">Depois que o conflito for resolvido, o resultado deverá ser assim:</span><span class="sxs-lookup"><span data-stu-id="22180-184">After the conflict is resolved, the output should look like this:</span></span>

```

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: The output object type of this cmdlet is going to be modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to mywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="22180-185">Você precisa das três cadeias de caracteres anteriores, CertificateThumbprint, SourceVault e CertificateURL, para configurar um cluster do Service Fabric seguro e obter os certificados de aplicativo que estejam sendo usados na segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22180-185">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="22180-186">Se você não salvar as cadeias de caracteres, poderá ter dificuldade em recuperá-los consultando o cofre da chave mais tarde.</span><span class="sxs-lookup"><span data-stu-id="22180-186">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-to-the-key-vault"></a><span data-ttu-id="22180-187">Criando um certificado autoassinado e carregando no cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="22180-187">Creating a self-signed certificate and uploading it to the key vault</span></span>

<span data-ttu-id="22180-188">Se você já carregou os certificados para o cofre da chaves, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="22180-188">If you have already uploaded your certificates to the key vault, skip this step.</span></span> <span data-ttu-id="22180-189">Esta etapa é para gerar um novo certificado autoassinado e carregá-lo no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span></span> <span data-ttu-id="22180-190">Depois de alterar os parâmetros no script a seguir e executá-lo, você deverá inserir a senha do certificado.</span><span class="sxs-lookup"><span data-stu-id="22180-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #The certificate's subject name must match the domain used to access the Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want the .PFX to be stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="22180-191">Se você receber um erro como o mostrado aqui, provavelmente tem um conflito de URL de recurso.</span><span class="sxs-lookup"><span data-stu-id="22180-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="22180-192">Para resolver o conflito, altere o nome do cofre de chaves, o nome RG e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="22180-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="22180-193">Depois que o conflito for resolvido, o resultado deverá ser assim:</span><span class="sxs-lookup"><span data-stu-id="22180-193">After the conflict is resolved, the output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context to SubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: The output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret to chackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="22180-194">Você precisa das três cadeias de caracteres anteriores, CertificateThumbprint, SourceVault e CertificateURL, para configurar um cluster do Service Fabric seguro e obter os certificados de aplicativo que estejam sendo usados na segurança do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22180-194">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="22180-195">Se você não salvar as cadeias de caracteres, poderá ter dificuldade em recuperá-los consultando o cofre da chave mais tarde.</span><span class="sxs-lookup"><span data-stu-id="22180-195">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

 <span data-ttu-id="22180-196">Agora você deve ter os seguintes elementos:</span><span class="sxs-lookup"><span data-stu-id="22180-196">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="22180-197">Grupo de recursos do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-197">The key vault resource group.</span></span>
* <span data-ttu-id="22180-198">O cofre de chaves e sua URL (chamada SourceVault na saída do PowerShell acima).</span><span class="sxs-lookup"><span data-stu-id="22180-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span></span>
* <span data-ttu-id="22180-199">O certificado de autenticação de servidor de cluster e sua URL no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-199">The cluster server authentication certificate and its URL in the key vault.</span></span>
* <span data-ttu-id="22180-200">Os certificados de aplicativo e as URLs no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="22180-200">The application certificates and their URLs in the key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="22180-201">Configurar o Azure Active Directory para autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="22180-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="22180-202">O Azure AD permite que as organizações (conhecidas como locatários) gerenciem o acesso dos usuários aos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="22180-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span></span> <span data-ttu-id="22180-203">Os aplicativos são divididos entre os que têm IU de entrada na Web e os que têm experiência de cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="22180-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="22180-204">Neste artigo, partimos do pressuposto que você já tenha criado um locatário.</span><span class="sxs-lookup"><span data-stu-id="22180-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="22180-205">Se não for o caso, comece lendo [Como obter um locatário do Azure Active Directory][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="22180-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="22180-206">Os clusters do Service Fabric oferecem vários pontos de entrada para a funcionalidade de gerenciamento, incluindo o [Service Fabric Explorer][service-fabric-visualizing-your-cluster] online o [Visual Studio][service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="22180-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="22180-207">Como resultado, você criará dois aplicativos do Azure AD para controlar o acesso ao cluster, um aplicativo Web e um aplicativo nativo.</span><span class="sxs-lookup"><span data-stu-id="22180-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span></span>

<span data-ttu-id="22180-208">Para simplificar algumas das etapas envolvidas na configuração do Azure AD com um cluster do Service Fabric, criamos um conjunto de scripts do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22180-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="22180-209">Você deve concluir as etapas a seguir para poder criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-209">You must complete the following steps before you create the cluster.</span></span> <span data-ttu-id="22180-210">Como os scripts esperam pontos de extremidade e nomes de cluster, os valores devem ser planejados, não os valores que você já tinha criado.</span><span class="sxs-lookup"><span data-stu-id="22180-210">Because the scripts expect cluster names and endpoints, the values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="22180-211">[Baixe os scripts][sf-aad-ps-script-download] em seu computador.</span><span class="sxs-lookup"><span data-stu-id="22180-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span></span>
2. <span data-ttu-id="22180-212">Clique com o botão direito do mouse no arquivo zip, selecione **Propriedades**, marque a caixa de seleção **Desbloquear** e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="22180-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="22180-213">Extraia o arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="22180-213">Extract the zip file.</span></span>
4. <span data-ttu-id="22180-214">Execute `SetupApplications.ps1` e forneça TenantId, ClusterName e WebApplicationReplyUrl como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="22180-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="22180-215">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="22180-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="22180-216">Você pode encontrar o TenantId executando o comando `Get-AzureSubscription` do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22180-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="22180-217">A execução desse comando exibe a TenantId para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="22180-217">Executing this command displays the TenantId for every subscription.</span></span>

    <span data-ttu-id="22180-218">O ClusterName é usado para prefixar os aplicativos do Azure AD criados pelo script.</span><span class="sxs-lookup"><span data-stu-id="22180-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span></span> <span data-ttu-id="22180-219">Ele não precisa corresponder exatamente ao nome real do cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-219">It does not need to match the actual cluster name exactly.</span></span> <span data-ttu-id="22180-220">Serve apenas para tornar mais fácil mapear artefatos do Azure AD para o cluster do Service Fabric com que estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="22180-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="22180-221">WebApplicationReplyUrl é o ponto de extremidade padrão que o Azure AD retorna para seus usuários depois que eles concluem o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="22180-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span></span> <span data-ttu-id="22180-222">Defina esse ponto de extremidade como o ponto de extremidade do Service Fabric Explorer para o seu cluster, que por padrão é:</span><span class="sxs-lookup"><span data-stu-id="22180-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="22180-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="22180-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="22180-224">Você precisará entrar em uma conta que tenha privilégios administrativos para o locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22180-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span></span> <span data-ttu-id="22180-225">Depois de entrar, o script criará aplicativos Web e nativos para representar seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22180-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span></span> <span data-ttu-id="22180-226">Se você observar os aplicativos do locatário no [Portal Clássico do Azure][azure-classic-portal], você verá duas novas entradas:</span><span class="sxs-lookup"><span data-stu-id="22180-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="22180-227">*ClusterName*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="22180-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="22180-228">*ClusterName*\_Cliente</span><span class="sxs-lookup"><span data-stu-id="22180-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="22180-229">O script imprimirá o JSON necessário para o modelo do Azure Resource Manager ao criar o cluster na próxima seção. Portanto, convém manter a janela do PowerShell aberta.</span><span class="sxs-lookup"><span data-stu-id="22180-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="22180-230">Criar um modelo do Resource Manager do cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="22180-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="22180-231">Nesta seção, as saídas dos comandos anteriores do PowerShell serão usadas em um modelo do Resource Manager de um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22180-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="22180-232">Os exemplos de modelo do Resource Manager estão disponíveis na [Galeria de modelos de início rápido do Azure no GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="22180-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="22180-233">Esses modelos podem ser usados como ponto de partida para o modelo de cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-the-resource-manager-template"></a><span data-ttu-id="22180-234">Criar o modelo do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="22180-234">Create the Resource Manager template</span></span>
<span data-ttu-id="22180-235">Este guia usa o modelo de exemplo e parâmetros de modelo do [cluster seguro de cinco nós][service-fabric-secure-cluster-5-node-1-nodetype].</span><span class="sxs-lookup"><span data-stu-id="22180-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="22180-236">Baixe `azuredeploy.json` e `azuredeploy.parameters.json` em seu computador e abra ambos os arquivos em seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="22180-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="22180-237">Adicionar certificados</span><span class="sxs-lookup"><span data-stu-id="22180-237">Add certificates</span></span>
<span data-ttu-id="22180-238">Os certificados são adicionados a um modelo do Resource Manager de cluster quando você faz a referência ao Key Vault que contém as chaves de certificado.</span><span class="sxs-lookup"><span data-stu-id="22180-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span></span> <span data-ttu-id="22180-239">Recomendamos que você coloque os valores do cofre de chaves em um arquivo de parâmetros do modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22180-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="22180-240">Isso faz com que o modelo do Resource Manager seja reutilizável e fique livre de valores específicos de uma implantação.</span><span class="sxs-lookup"><span data-stu-id="22180-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span></span>

#### <a name="add-all-certificates-to-the-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="22180-241">Adicionar todos os certificados ao conjunto de dimensionamento de máquinas virtuais osProfile</span><span class="sxs-lookup"><span data-stu-id="22180-241">Add all certificates to the virtual machine scale set osProfile</span></span>
<span data-ttu-id="22180-242">Todos os certificados instalados no cluster devem ser configurados na seção osProfile do recurso de conjunto de dimensionamento (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="22180-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="22180-243">Essa ação instrui o provedor de recursos para instalar o certificado nas VMs.</span><span class="sxs-lookup"><span data-stu-id="22180-243">This action instructs the resource provider to install the certificate on the VMs.</span></span> <span data-ttu-id="22180-244">Essa instalação inclui o certificado do cluster e os certificados de segurança de aplicativo que você planeja usar para seus aplicativos:</span><span class="sxs-lookup"><span data-stu-id="22180-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span></span>

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

#### <a name="configure-the-service-fabric-cluster-certificate"></a><span data-ttu-id="22180-245">Configurar o certificado do cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="22180-245">Configure the Service Fabric cluster certificate</span></span>
<span data-ttu-id="22180-246">O certificado de autenticação do cluster tem que ser configurado tanto no recurso de cluster do Service Fabric (Microsoft.ServiceFabric/clusters) quanto na extensão do Service Fabric para conjuntos de dimensionamento de máquinas virtuais no recurso de conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="22180-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span></span> <span data-ttu-id="22180-247">Essa disposição permite que o provedor de recursos do Service Fabric o configure para autenticação do cluster e autenticação de servidor para pontos de extremidade de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="22180-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="22180-248">Recurso Conjunto de dimensionamento de máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="22180-248">Virtual machine scale set resource:</span></span>
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

##### <a name="service-fabric-resource"></a><span data-ttu-id="22180-249">Recursos do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="22180-249">Service Fabric resource:</span></span>
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

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="22180-250">Inserir configuração do Azure AD</span><span class="sxs-lookup"><span data-stu-id="22180-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="22180-251">A configuração do Azure AD que você criou anteriormente pode ser inserida diretamente no modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22180-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="22180-252">No entanto, recomendamos que você primeiro extraia os valores em um arquivo de parâmetros para fazer com que o modelo do Resource Manager seja reutilizável e fique livre de valores específicos de uma implantação.</span><span class="sxs-lookup"><span data-stu-id="22180-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span></span>

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

### <span data-ttu-id="22180-253"><a "configure-arm" ></a>Configurar os parâmetros do modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22180-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since the link seems not to be redirecting correctly --->
<span data-ttu-id="22180-254">Por fim, use os valores de saída dos comandos do cofre de chaves e do PowerShell do Azure AD para preencher o arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="22180-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span></span>

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
<span data-ttu-id="22180-255">Agora você deve ter os seguintes elementos:</span><span class="sxs-lookup"><span data-stu-id="22180-255">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="22180-256">Grupo de recursos do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="22180-256">Key vault resource group</span></span>
  * <span data-ttu-id="22180-257">Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="22180-257">Key vault</span></span>
  * <span data-ttu-id="22180-258">Certificado de autenticação de servidor de cluster</span><span class="sxs-lookup"><span data-stu-id="22180-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="22180-259">Certificado de codificação de dados</span><span class="sxs-lookup"><span data-stu-id="22180-259">Data encipherment certificate</span></span>
* <span data-ttu-id="22180-260">Locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22180-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="22180-261">Aplicativo Azure AD para gerenciamento baseado na Web e no Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="22180-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="22180-262">Aplicativo Azure AD para o gerenciamento de clientes nativos</span><span class="sxs-lookup"><span data-stu-id="22180-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="22180-263">Usuários e suas funções atribuídas</span><span class="sxs-lookup"><span data-stu-id="22180-263">Users and their assigned roles</span></span>
* <span data-ttu-id="22180-264">Modelo do Resource Manager de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="22180-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="22180-265">Certificados configurados por meio do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="22180-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="22180-266">Azure Active Directory configurado</span><span class="sxs-lookup"><span data-stu-id="22180-266">Azure Active Directory configured</span></span>

<span data-ttu-id="22180-267">O diagrama a seguir ilustra onde a configuração do cofre de chaves e do Azure AD se encaixa em seu modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22180-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Mapa de dependências do Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-the-cluster"></a><span data-ttu-id="22180-269">Criar o cluster</span><span class="sxs-lookup"><span data-stu-id="22180-269">Create the cluster</span></span>
<span data-ttu-id="22180-270">Agora você está pronto para criar o cluster usando a [implantação do modelo do Azure Resource Manager][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="22180-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="22180-271">Testá-lo</span><span class="sxs-lookup"><span data-stu-id="22180-271">Test it</span></span>
<span data-ttu-id="22180-272">Use o seguinte comando do PowerShell para testar o modelo do Resource Manager com um arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="22180-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="22180-273">Implantá-lo</span><span class="sxs-lookup"><span data-stu-id="22180-273">Deploy it</span></span>
<span data-ttu-id="22180-274">Se o modelo do Resource Manager passar no teste, use o comando do PowerShell a seguir para implantar seu modelo do Resource Manager com um arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="22180-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-to-roles"></a><span data-ttu-id="22180-275">Atribuir usuários a funções</span><span class="sxs-lookup"><span data-stu-id="22180-275">Assign users to roles</span></span>
<span data-ttu-id="22180-276">Depois de criar os aplicativos para representar seu cluster, atribua os usuários às funções com suporte no Service Fabric: somente leitura e administrador. Você pode atribuir as funções usando o [portal clássico do Azure][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="22180-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="22180-277">No portal do Azure, vá para seu locatário e selecione **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="22180-277">In the Azure portal, go to your tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="22180-278">Selecione o aplicativo Web, que tem um nome semelhante a `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="22180-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="22180-279">Clique na guia **Usuários** .</span><span class="sxs-lookup"><span data-stu-id="22180-279">Click the **Users** tab.</span></span>
4. <span data-ttu-id="22180-280">Selecione um usuário para atribuir e clique no botão **Atribuir** na parte inferior da tela.</span><span class="sxs-lookup"><span data-stu-id="22180-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span></span>

    ![Botão Atribuir usuários a funções][assign-users-to-roles-button]
5. <span data-ttu-id="22180-282">Selecione a função para atribuir ao usuário.</span><span class="sxs-lookup"><span data-stu-id="22180-282">Select the role to assign to the user.</span></span>

    ![Caixa de diálogo "Atribuir Usuários"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="22180-284">Para saber mais sobre as funções no Service Fabric, veja [Controle de acesso baseado em função para clientes do Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="22180-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused the wrong redirection of the link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="22180-285">Criar clusters seguros no Linux</span><span class="sxs-lookup"><span data-stu-id="22180-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="22180-286">Para facilitar o processo, fornecemos um [script auxiliar](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="22180-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="22180-287">Antes de usar esse script auxiliar, verifique se você já tem a CLI (interface de linha de comando) do Azure instalada e se ele está em seu caminho.</span><span class="sxs-lookup"><span data-stu-id="22180-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="22180-288">Certifique-se de que o script tenha permissões para execução ao executar `chmod +x cert_helper.py` após fazer o download.</span><span class="sxs-lookup"><span data-stu-id="22180-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="22180-289">A primeira etapa é entrar na sua conta do Azure usando a CLI com o comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="22180-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span></span> <span data-ttu-id="22180-290">Depois de entrar na sua conta do Azure, use o script auxiliar com seu certificado da AC assinado, como mostra o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="22180-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="22180-291">O parâmetro -ifile pode usar um arquivo .pfx ou .pem como entrada, com o tipo de certificado (pfx, pem ou ss se for um certificado autoassinado).</span><span class="sxs-lookup"><span data-stu-id="22180-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="22180-292">O parâmetro -h imprime o texto de ajuda.</span><span class="sxs-lookup"><span data-stu-id="22180-292">The parameter -h prints out the help text.</span></span>


<span data-ttu-id="22180-293">Esse comando retorna as três cadeias de caracteres a seguir como a saída:</span><span class="sxs-lookup"><span data-stu-id="22180-293">This command returns the following three strings as the output:</span></span>

* <span data-ttu-id="22180-294">SourceVaultID, que é a ID para o novo KeyVault ResourceGroup criado para você</span><span class="sxs-lookup"><span data-stu-id="22180-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="22180-295">CertificateUrl para acessar o certificado</span><span class="sxs-lookup"><span data-stu-id="22180-295">CertificateUrl for accessing the certificate</span></span>
* <span data-ttu-id="22180-296">CertificateThumbprint, que é usado para autenticação</span><span class="sxs-lookup"><span data-stu-id="22180-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="22180-297">O exemplo a seguir mostra como usar o comando:</span><span class="sxs-lookup"><span data-stu-id="22180-297">The following example shows how to use the command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="22180-298">A execução do comando anterior dá as seguintes três cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="22180-298">Executing the preceding command gives you the three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="22180-299">O nome da referência do certificado deve corresponder ao domínio usado para acessar o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22180-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="22180-300">Essa correspondência é necessária para fornecer um SSL para os pontos de extremidade de gerenciamento de HTTPS e o Service Fabric Explorer do cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="22180-301">Você não pode obter um certificado SSL de uma AC para o domínio `.cloudapp.azure.com` .</span><span class="sxs-lookup"><span data-stu-id="22180-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="22180-302">Você deve obter um nome de domínio personalizado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="22180-303">Quando você solicitar um certificado de uma autoridade de certificação, o nome de assunto do certificado deve corresponder ao nome de domínio personalizado usado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="22180-304">Esses nomes de referência são as entradas necessárias para criar um cluster do Service Fabric seguro (sem o Azure AD), conforme descrito em [Configurar parâmetros de modelo do Resource Manager](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="22180-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="22180-305">Você pode se conectar ao cluster seguro seguindo as instruções para [autenticar o acesso de cliente a um cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="22180-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="22180-306">Os clusters de visualização do Linux não dão suporte à autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22180-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="22180-307">Você pode atribuir funções de administrador e cliente, conforme descrito na seção [Atribuir funções a usuários](#assign-roles).</span><span class="sxs-lookup"><span data-stu-id="22180-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span></span> <span data-ttu-id="22180-308">Quando você especifica funções de administrador e cliente para um cluster de visualização do Linux, precisa fornecer as impressões digitais de certificado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="22180-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span></span> <span data-ttu-id="22180-309">(Você não fornece o nome da entidade porque nenhuma validação ou revogação de cadeia está sendo executada nessa versão de visualização.)</span><span class="sxs-lookup"><span data-stu-id="22180-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="22180-310">Se quiser usar um certificado autoassinado para testes, você poderá usar o mesmo script para gerá-lo.</span><span class="sxs-lookup"><span data-stu-id="22180-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span></span> <span data-ttu-id="22180-311">Em seguida, você pode carregar o certificado no cofre de chaves fornecendo o sinalizador `ss` em vez do caminho e do nome do certificado.</span><span class="sxs-lookup"><span data-stu-id="22180-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span></span> <span data-ttu-id="22180-312">Por exemplo, consulte o seguinte comando para criar e carregar um certificado autoassinado:</span><span class="sxs-lookup"><span data-stu-id="22180-312">For example, see the following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="22180-313">Esse comando retorna as mesmas três cadeias de caracteres: SourceVault, CertificateUrl e CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="22180-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="22180-314">Em seguida, você pode usar as cadeias de caracteres para criar um cluster do Linux seguro e um local onde o certificado autoassinado fica armazenado.</span><span class="sxs-lookup"><span data-stu-id="22180-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span></span> <span data-ttu-id="22180-315">Você precisa do certificado autoassinado para se conectar ao cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-315">You need the self-signed certificate to connect to the cluster.</span></span> <span data-ttu-id="22180-316">Você pode se conectar ao cluster seguro seguindo as instruções para [autenticar o acesso de cliente a um cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="22180-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="22180-317">O nome da referência do certificado deve corresponder ao domínio usado para acessar o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22180-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="22180-318">Essa correspondência é necessária para fornecer um SSL para os pontos de extremidade de gerenciamento de HTTPS e o Service Fabric Explorer do cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="22180-319">Você não pode obter um certificado SSL de uma AC para o domínio `.cloudapp.azure.com` .</span><span class="sxs-lookup"><span data-stu-id="22180-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="22180-320">Você deve obter um nome de domínio personalizado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="22180-321">Quando você solicitar um certificado de uma autoridade de certificação, o nome de assunto do certificado deve corresponder ao nome de domínio personalizado usado para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="22180-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="22180-322">Você pode preencher os parâmetros do script auxiliar no portal do Azure, conforme descrito na seção [criar um cluster no portal do Azure](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="22180-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22180-323">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22180-323">Next steps</span></span>
<span data-ttu-id="22180-324">Neste ponto, você tem um cluster seguro com o Azure Active Directory fornecendo autenticação de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="22180-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="22180-325">Em seguida, [conecte-se ao cluster](service-fabric-connect-to-secure-cluster.md) e saiba como [gerenciar segredos do aplicativo](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="22180-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="22180-326">Solucionar problemas na configuração do Azure Active Directory para autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="22180-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="22180-327">Se você tiver um problema durante a configuração do Azure AD para autenticação de cliente, examine as possíveis soluções nesta seção.</span><span class="sxs-lookup"><span data-stu-id="22180-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-to-select-a-certificate"></a><span data-ttu-id="22180-328">O Service Fabric Explorer solicita que você selecione um certificado</span><span class="sxs-lookup"><span data-stu-id="22180-328">Service Fabric Explorer prompts you to select a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="22180-329">Problema</span><span class="sxs-lookup"><span data-stu-id="22180-329">Problem</span></span>
<span data-ttu-id="22180-330">Depois de entrar no Azure AD no Service Fabric Explorer, o navegador retornará para a home page, mas uma mensagem solicitará que você selecione um certificado.</span><span class="sxs-lookup"><span data-stu-id="22180-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span></span>

![Caixa de diálogo de seleção de certificado SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="22180-332">Motivo</span><span class="sxs-lookup"><span data-stu-id="22180-332">Reason</span></span>
<span data-ttu-id="22180-333">O usuário não recebeu uma função no aplicativo de cluster do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22180-333">The user isn’t assigned a role in the Azure AD cluster application.</span></span> <span data-ttu-id="22180-334">Assim, a autenticação do Azure AD falha no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22180-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="22180-335">O Service Fabric Explorer reverterá para autenticação de certificado.</span><span class="sxs-lookup"><span data-stu-id="22180-335">Service Fabric Explorer falls back to certificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="22180-336">Solução</span><span class="sxs-lookup"><span data-stu-id="22180-336">Solution</span></span>
<span data-ttu-id="22180-337">Siga as instruções para configurar o Azure AD e atribuir funções de usuário.</span><span class="sxs-lookup"><span data-stu-id="22180-337">Follow the instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="22180-338">Além disso, recomendamos que você habilite a "Atribuição de usuário necessária para acessar o aplicativo" da mesma forma feita por `SetupApplications.ps1`.</span><span class="sxs-lookup"><span data-stu-id="22180-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-the-specified-credentials-are-invalid"></a><span data-ttu-id="22180-339">A conexão com o PowerShell falha e exibe o seguinte erro: “as credenciais especificadas são inválidas”</span><span class="sxs-lookup"><span data-stu-id="22180-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="22180-340">Problema</span><span class="sxs-lookup"><span data-stu-id="22180-340">Problem</span></span>
<span data-ttu-id="22180-341">Quando você usa o PowerShell para se conectar ao cluster usando o modo de segurança "AzureActiveDirectory", ao entrar no AD do Azure, a conexão falhará com um erro: "as credenciais especificadas são inválidas."</span><span class="sxs-lookup"><span data-stu-id="22180-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="22180-342">Solução</span><span class="sxs-lookup"><span data-stu-id="22180-342">Solution</span></span>
<span data-ttu-id="22180-343">Essa solução é igual à anterior.</span><span class="sxs-lookup"><span data-stu-id="22180-343">This solution is the same as the preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="22180-344">O Service Fabric Explorer retorna uma falha quando você entra: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="22180-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="22180-345">Problema</span><span class="sxs-lookup"><span data-stu-id="22180-345">Problem</span></span>
<span data-ttu-id="22180-346">Ao tentar entrar no Azure AD no Service Fabric Explorer, a página retorna uma falha: “AADSTS50011: a &lt;URL&gt; do endereço de resposta não coincide com os endereços de resposta configurados para o aplicativo: &lt;GUID&gt;”.</span><span class="sxs-lookup"><span data-stu-id="22180-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span></span>

![O endereço de resposta SFX não corresponde][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="22180-348">Motivo</span><span class="sxs-lookup"><span data-stu-id="22180-348">Reason</span></span>
<span data-ttu-id="22180-349">O aplicativo do cluster (Web) que representa o Service Fabric Explorer tenta se autenticar no Azure AD como parte da solicitação que ele fornece à URL de retorno de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="22180-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span></span> <span data-ttu-id="22180-350">Mas a URL não está listada na lista **URL DE RESPOSTA** do aplicativo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22180-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="22180-351">Solução</span><span class="sxs-lookup"><span data-stu-id="22180-351">Solution</span></span>
<span data-ttu-id="22180-352">Na guia **Configurar** do aplicativo do cluster (Web), adicione a URL do Service Fabric Explorer à lista **URL DE RESPOSTA** ou substitua um dos itens na lista.</span><span class="sxs-lookup"><span data-stu-id="22180-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span></span> <span data-ttu-id="22180-353">Quando terminar, salve a alteração.</span><span class="sxs-lookup"><span data-stu-id="22180-353">When you have finished, save your change.</span></span>

![URL de resposta do aplicativo Web][web-application-reply-url]

### <a name="connect-the-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="22180-355">Conectar o cluster usando a autenticação do Azure AD por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="22180-355">Connect the cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="22180-356">Para se conectar ao cluster do Service Fabric, use o seguinte exemplo de comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="22180-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="22180-357">Para saber mais sobre o cmdlet Connect-ServiceFabricCluster, confira [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="22180-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-the-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="22180-358">Posso reutilizar o mesmo locatário do Azure AD em vários clusters?</span><span class="sxs-lookup"><span data-stu-id="22180-358">Can I reuse the same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="22180-359">Sim.</span><span class="sxs-lookup"><span data-stu-id="22180-359">Yes.</span></span> <span data-ttu-id="22180-360">Mas lembre-se de adicionar a URL do Service Fabric Explorer ao aplicativo do cluster (Web).</span><span class="sxs-lookup"><span data-stu-id="22180-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span></span> <span data-ttu-id="22180-361">Caso contrário, o Service Fabric Explorer não funcionará.</span><span class="sxs-lookup"><span data-stu-id="22180-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="22180-362">Por que eu ainda preciso de um certificado de servidor quando o Azure AD está habilitado?</span><span class="sxs-lookup"><span data-stu-id="22180-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="22180-363">FabricClient e FabricGateway realizam autenticação mútua.</span><span class="sxs-lookup"><span data-stu-id="22180-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="22180-364">Durante a autenticação do Azure AD, a integração dele fornece uma identidade de cliente para o servidor e o certificado do servidor é usado para verificar a identidade do servidor.</span><span class="sxs-lookup"><span data-stu-id="22180-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span></span> <span data-ttu-id="22180-365">Para saber mais sobre certificados do Service Fabric, confira [Certificados X.509 e Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="22180-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

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

