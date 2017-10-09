---
title: aaaService principal para o cluster do Azure Kubernetes | Microsoft Docs
description: "Criar e gerenciar uma entidade de serviço do Azure Active Directory para um cluster Kubernetes no Serviço de Contêiner do Azure"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="9b987-103">Configurar uma entidade de serviço do Azure AD para um cluster Kubernetes no contêiner de serviço</span><span class="sxs-lookup"><span data-stu-id="9b987-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="9b987-104">No serviço de contêiner do Azure, um cluster Kubernetes requer um [entidade de serviço do Active Directory do Azure](../../active-directory/develop/active-directory-application-objects.md) toointeract com APIs do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b987-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="9b987-105">Olá entidade de serviço é necessário toodynamically gerenciar recursos, como [rotas definidas pelo usuário](../../virtual-network/virtual-networks-udr-overview.md) e hello [balanceador de carga do Azure de 4 de camada](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b987-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="9b987-106">Este artigo mostra diferentes opções tooset o serviço principal para o cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9b987-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="9b987-107">Por exemplo, se você instalou e configurar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2), você pode executar Olá [ `az acs create` ](/cli/azure/acs#create) saudação do comando toocreate Kubernetes no principal no hello de serviço de cluster e hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="9b987-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="9b987-108">Requisitos para a entidade de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="9b987-108">Requirements for hello service principal</span></span>

<span data-ttu-id="9b987-109">Você pode usar uma entidade de serviço do AD do Azure existente que atende Olá seguindo os requisitos ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="9b987-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="9b987-110">**Escopo**: grupo de recursos de saudação na assinatura Olá usado cluster do toodeploy Olá Kubernetes ou (menos restrictively) assinatura Olá toodeploy cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b987-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="9b987-111">**Função**: **Colaborador**</span><span class="sxs-lookup"><span data-stu-id="9b987-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="9b987-112">**Segredo do cliente**: deve ser uma senha.</span><span class="sxs-lookup"><span data-stu-id="9b987-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="9b987-113">Atualmente, é possível usar uma entidade de serviço configurada para autenticação de certificado.</span><span class="sxs-lookup"><span data-stu-id="9b987-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="9b987-114">toocreate uma entidade de serviço, você deve ter permissões tooregister um aplicativo com seu locatário do AD do Azure e sua função de tooa tooassign Olá aplicativo em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="9b987-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="9b987-115">toosee se você tiver permissões de saudação necessária [check-in Olá Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="9b987-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="9b987-116">Opção 1: criar uma entidade de serviço no Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b987-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="9b987-117">Se você quiser toocreate uma entidade de serviço do AD do Azure antes de implantar o cluster Kubernetes, o Azure fornece vários métodos.</span><span class="sxs-lookup"><span data-stu-id="9b987-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="9b987-118">Olá comandos de exemplo a seguir mostra como toodo com hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9b987-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="9b987-119">Você também pode criar uma entidade de serviço usando [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), Olá [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), ou outros métodos.</span><span class="sxs-lookup"><span data-stu-id="9b987-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="9b987-120">O resultado é semelhante seguinte toohello (mostrados aqui redigida):</span><span class="sxs-lookup"><span data-stu-id="9b987-120">Output is similar toohello following (shown here redacted):</span></span>

![Criar uma entidade de serviço](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="9b987-122">Estão realçados Olá **ID do cliente** (`appId`) e hello **segredo do cliente** (`password`) que são usados como parâmetros de serviço principal para a implantação de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b987-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="9b987-123">Especifique a entidade de serviço durante a criação de cluster de Kubernetes Olá</span><span class="sxs-lookup"><span data-stu-id="9b987-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="9b987-124">Fornecer Olá **ID do cliente** (também chamado de hello `appId`, para a ID de aplicativo) e **segredo do cliente** (`password`) de um serviço existente principal como parâmetros quando você cria Olá Cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9b987-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="9b987-125">Certifique-se de entidade de serviço Olá atende aos requisitos de saudação em hello a partir deste artigo.</span><span class="sxs-lookup"><span data-stu-id="9b987-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="9b987-126">Você pode especificar esses parâmetros durante a implantação de cluster de Kubernetes hello usando Olá [Azure Interface de linha de comando (CLI) 2.0](container-service-kubernetes-walkthrough.md), [portal do Azure](../dcos-swarm/container-service-deployment.md), ou outros métodos.</span><span class="sxs-lookup"><span data-stu-id="9b987-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="9b987-127">Ao especificar Olá **ID do cliente**, ser Olá de toouse se `appId`, Olá não `ObjectId`, da entidade de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="9b987-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="9b987-128">Hello exemplo a seguir mostra uma maneira toopass parâmetros Olá Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b987-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="9b987-129">Este exemplo usa Olá [Kubernetes quickstart modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="9b987-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="9b987-130">[Baixar](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) arquivo de parâmetros de modelo Olá `azuredeploy.parameters.json` do GitHub.</span><span class="sxs-lookup"><span data-stu-id="9b987-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="9b987-131">serviço de saudação toospecify principal, digite os valores para `servicePrincipalClientId` e `servicePrincipalClientSecret` no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="9b987-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="9b987-132">(Você também precisa tooprovide seus próprios valores para `dnsNamePrefix` e `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="9b987-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="9b987-133">Olá último é cluster de Olá Olá SSH tooaccess de chave pública). Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="9b987-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![Passar parâmetros de entidade de serviço](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="9b987-135">Olá executar comando a seguir, o uso de `--parameters` tooset Olá caminho toohello azuredeploy.parameters.json arquivo de.</span><span class="sxs-lookup"><span data-stu-id="9b987-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="9b987-136">Esse comando implanta Olá em um grupo de recursos que você criar chamado `myResourceGroup` na região Oeste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b987-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="9b987-137">Opção 2: Gerar uma entidade de serviço durante a criação de cluster Olá com`az acs create`</span><span class="sxs-lookup"><span data-stu-id="9b987-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="9b987-138">Se você executar Olá [ `az acs create` ](/cli/azure/acs#create) toocreate comando Olá Kubernetes cluster, você terá Olá opção toogenerate uma entidade de serviço automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9b987-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="9b987-139">Como ocorre com outras opções de criação do cluster Kubernetes, você pode especificar parâmetros para uma entidade de serviço existente quando executa `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="9b987-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="9b987-140">No entanto, quando você omite esses parâmetros, Olá CLI do Azure cria um automaticamente para uso com o serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="9b987-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="9b987-141">Isso ocorre transparente durante a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b987-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="9b987-142">Olá comando a seguir cria um cluster Kubernetes e gera as chaves de SSH e credenciais de serviço principal:</span><span class="sxs-lookup"><span data-stu-id="9b987-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="9b987-143">Se sua conta não tiver hello Azure AD e assinatura permissões toocreate uma entidade de serviço, o comando hello gera um erro semelhante muito`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="9b987-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="9b987-144">Considerações adicionais</span><span class="sxs-lookup"><span data-stu-id="9b987-144">Additional considerations</span></span>

* <span data-ttu-id="9b987-145">Se você não tiver permissões toocreate uma entidade de serviço em sua assinatura, talvez seja necessário tooask AD do Azure ou assinatura administrador tooassign Olá permissões necessárias ou peça para um toouse principal do serviço com o serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b987-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="9b987-146">entidade de serviço Olá para Kubernetes é uma parte da configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b987-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="9b987-147">No entanto, não use o cluster de Olá Olá identidade toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9b987-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="9b987-148">Cada entidade de serviço é associada a um aplicativo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b987-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="9b987-149">Olá entidade de serviço para um cluster Kubernetes pode ser associada a qualquer válida do Azure nome do aplicativo do AD (por exemplo: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="9b987-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="9b987-150">Olá URL para o aplicativo hello não tem um ponto de extremidade real do toobe.</span><span class="sxs-lookup"><span data-stu-id="9b987-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="9b987-151">Ao especificar a entidade de serviço Olá **ID do cliente**, você pode usar o valor Olá Olá `appId` (conforme mostrado neste artigo) ou da entidade de serviço correspondente Olá `name` (por exemplo,`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="9b987-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="9b987-152">Em mestre hello e agente de VMs no cluster de Kubernetes hello, credenciais de entidade de serviço Olá são armazenadas em Olá arquivo /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="9b987-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="9b987-153">Quando você usa Olá `az acs create` comando entidade de serviço toogenerate Olá automaticamente, credenciais de entidade de serviço Olá são gravadas toohello arquivo ~/.azure/acsServicePrincipal.json na máquina de saudação usada toorun comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b987-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="9b987-154">Quando você usa Olá `az acs create` command entidade de serviço toogenerate Olá automaticamente, a entidade de serviço Olá também pode se autenticar com um [registro de contêiner do Azure](../../container-registry/container-registry-intro.md) criado no hello mesmo assinatura.</span><span class="sxs-lookup"><span data-stu-id="9b987-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="9b987-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b987-155">Next steps</span></span>

* <span data-ttu-id="9b987-156">[Introdução ao Kubernetes](container-service-kubernetes-walkthrough.md) em seu cluster de serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="9b987-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="9b987-157">tootroubleshoot Olá entidade de serviço para Kubernetes, consulte Olá [documentação do mecanismo de ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="9b987-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


