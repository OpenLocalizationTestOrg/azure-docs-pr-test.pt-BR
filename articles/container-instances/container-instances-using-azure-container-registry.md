---
title: "Implantar do Registro de Contêiner do Azure em Instâncias de Contêiner do Azure | Azure Docs"
description: "Implantar do Registro de Contêiner do Azure em Instâncias de Contêiner do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: aa1c4ea379c10dff246e2f924a345f9fa444aa64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-container-instances-from-the-azure-container-registry"></a><span data-ttu-id="dfaf5-103">Implantar do Registro de Contêiner do Azure em Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="dfaf5-103">Deploy to Azure Container Instances from the Azure Container Registry</span></span>

<span data-ttu-id="dfaf5-104">O Registro de Contêiner do Azure é um registro privado baseado no Azure para imagens de contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-104">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="dfaf5-105">Este artigo aborda como implantar imagens de contêiner armazenadas no Registro de Contêiner do Azure em Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-105">This article covers how to deploy container images stored in the Azure Container Registry to Azure Container Instances.</span></span>

## <a name="using-the-azure-cli"></a><span data-ttu-id="dfaf5-106">Usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="dfaf5-106">Using the Azure CLI</span></span>

<span data-ttu-id="dfaf5-107">A CLI do Azure inclui comandos para criar e gerenciar contêineres nas Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-107">The Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="dfaf5-108">Se você especificar uma imagem privada no comando `create`, também poderá especificar a senha do registro da imagem, necessária para autenticar com o registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-108">If you specify a private image in the `create` command, you can also specify the image registry password required to authenticate with the container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="dfaf5-109">O comando `create` também dá suporte à especificação de `registry-login-server` e `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-109">The `create` command also supports specifying the `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="dfaf5-110">No entanto, o servidor de logon do Registro de Contêiner do Azure é sempre *registryname*.azurecr.io e o nome de usuário é *registryname*, portanto, esses valores são inferidos do nome da imagem, caso não sejam explicitamente fornecidos.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-110">However, the login server for the Azure Container Registry is always *registryname*.azurecr.io and the default username is *registryname*, so these values are inferred from the image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="dfaf5-111">Usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dfaf5-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="dfaf5-112">Você pode especificar as propriedades do Registro de Contêiner do Azure em um modelo do Azure Resource Manager incluindo a propriedade `imageRegistryCredentials` na definição de grupos do contêiner:</span><span class="sxs-lookup"><span data-stu-id="dfaf5-112">You can specify the properties of your Azure Container Registry in an Azure Resource Manager template by including the `imageRegistryCredentials` property in the container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="dfaf5-113">Para evitar o armazenamento da senha do registro de contêiner diretamente no modelo, é recomendável que você armazene-a como um segredo no [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) e referencie-a no modelo, usando a [integração nativa entre o Azure Resource Manager e o Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="dfaf5-113">To avoid storing your container registry password directly in the template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in the template using the [native integration between the Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="dfaf5-114">Usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dfaf5-114">Using the Azure portal</span></span>

<span data-ttu-id="dfaf5-115">Se você mantiver as imagens de contêiner no Registro de Contêiner do Azure, você poderá facilmente criar um contêiner em Instâncias de Contêiner do Azure usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-115">If you maintain container images in the Azure Container Registry, you can easily create a container in Azure Container Instances using the Azure portal.</span></span>

1. <span data-ttu-id="dfaf5-116">No Portal do Azure, navegue até o registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-116">In the Azure portal, navigate to your container registry.</span></span>

2. <span data-ttu-id="dfaf5-117">Escolha Repositórios.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-117">Choose Repositories.</span></span>

    ![O menu Registro de Contêiner do Azure no Portal do Azure][acr-menu]

3. <span data-ttu-id="dfaf5-119">Escolha o repositório do qual você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-119">Choose the repository that you want to deploy from.</span></span>

4. <span data-ttu-id="dfaf5-120">Clique com o botão direito do mouse na marca para a imagem de contêiner que você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-120">Right-click the tag for the container image you want to deploy.</span></span>

    ![Menu de contexto para iniciar o contêiner com Instâncias de Contêiner do Azure][acr-runinstance-contextmenu]

5. <span data-ttu-id="dfaf5-122">Insira um nome para o contêiner e um nome para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-122">Enter a name for the container and a name for the resource group.</span></span> <span data-ttu-id="dfaf5-123">Você também poderá alterar os valores padrão se desejar.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-123">You can also change the default values if you wish.</span></span>

    ![Criar menu para Instâncias de Contêiner do Azure][acr-create-deeplink]

6. <span data-ttu-id="dfaf5-125">Quando a implantação for concluída, você poderá navegar para o grupo de contêineres do painel de notificações para localizar o endereço IP e outras propriedades do contêiner.</span><span class="sxs-lookup"><span data-stu-id="dfaf5-125">Once the deployment completes, you can navigate to the container group from the notifications pane to find its IP address and other properties.</span></span>

    ![Exibição de detalhes de grupo de contêineres das Instâncias de Contêiner do Azure][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="dfaf5-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dfaf5-127">Next steps</span></span>

<span data-ttu-id="dfaf5-128">Saiba como criar contêineres, enviá-los por push a um registro de contêiner privado e implantá-los em Instâncias de Contêiner do Azure ao [concluir o tutorial](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="dfaf5-128">Learn how to build containers, push them to a private container registry, and deploy them to Azure Container Instances by [completing the tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
