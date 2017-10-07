---
title: "aaaDeploy tooAzure instâncias de contêiner de saudação do registro de contêiner do Azure | Documentos do Azure"
description: "Implantar instâncias de contêiner de tooAzure de saudação do registro de contêiner do Azure"
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
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="00459-103">Implantar instâncias de contêiner de tooAzure de saudação do registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="00459-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="00459-104">Olá registro de contêiner do Azure é um registro baseado no Azure, em particular, para imagens de contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="00459-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="00459-105">Este artigo aborda como imagens de contêiner toodeploy armazenados em Olá registro de contêiner do Azure tooAzure instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="00459-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="00459-106">Usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="00459-106">Using hello Azure CLI</span></span>

<span data-ttu-id="00459-107">Olá CLI do Azure inclui comandos para criar e gerenciar contêineres em instâncias de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="00459-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="00459-108">Se você especificar uma imagem privada na Olá `create` de comando, você também pode especificar Olá tooauthenticate de senha necessária de registro de imagem com o registro de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="00459-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="00459-109">Olá `create` comando também dá suporte à especificação de saudação `registry-login-server` e `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="00459-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="00459-110">No entanto, o servidor de logon de saudação de saudação do registro de contêiner do Azure é sempre *registryname*. nome de usuário padrão azurecr.io e hello é *registryname*, portanto, esses valores são inferidos do nome da imagem Olá se não é explicitamente fornecido.</span><span class="sxs-lookup"><span data-stu-id="00459-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="00459-111">Usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="00459-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="00459-112">Você pode especificar propriedades de saudação do registro de contêiner do Azure em um modelo do Gerenciador de recursos do Azure, incluindo Olá `imageRegistryCredentials` propriedade na definição de grupo de contêiner hello:</span><span class="sxs-lookup"><span data-stu-id="00459-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="00459-113">tooavoid armazenar sua senha de registro de contêiner diretamente no modelo de hello, recomendamos que você armazená-lo como um segredo no [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) e referenciá-lo no modelo Olá Olá [integração nativa entre Olá Gerenciador de recursos do Azure e o Cofre de chaves](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="00459-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="00459-114">Usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="00459-114">Using hello Azure portal</span></span>

<span data-ttu-id="00459-115">Se você mantiver as imagens de contêiner de saudação do registro de contêiner do Azure, você pode facilmente criar um contêiner em instâncias de contêiner do Azure usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="00459-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="00459-116">No portal do Azure de Olá, navegue tooyour registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="00459-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="00459-117">Escolha Repositórios.</span><span class="sxs-lookup"><span data-stu-id="00459-117">Choose Repositories.</span></span>

    ![menu de registro de contêiner do Azure Olá Olá portal do Azure][acr-menu]

3. <span data-ttu-id="00459-119">Escolha o repositório de saudação que você deseja toodeploy do.</span><span class="sxs-lookup"><span data-stu-id="00459-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="00459-120">Clique com botão direito marca Olá para imagem de contêiner Olá deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="00459-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Menu de contexto para iniciar o contêiner com Instâncias de Contêiner do Azure][acr-runinstance-contextmenu]

5. <span data-ttu-id="00459-122">Insira um nome para o contêiner de saudação e um nome para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="00459-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="00459-123">Você também pode alterar os valores padrão de saudação se desejar.</span><span class="sxs-lookup"><span data-stu-id="00459-123">You can also change hello default values if you wish.</span></span>

    ![Criar menu para Instâncias de Contêiner do Azure][acr-create-deeplink]

6. <span data-ttu-id="00459-125">Após a conclusão da implantação Olá, você pode navegar toohello o grupo de contêiner de saudação notificações painel toofind seu endereço IP e outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="00459-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Exibição de detalhes de grupo de contêineres das Instâncias de Contêiner do Azure][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="00459-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00459-127">Next steps</span></span>

<span data-ttu-id="00459-128">Saiba como contêineres toobuild, enviá-las do registro de contêiner privado tooa e implantá-los em instâncias de contêiner tooAzure por [concluir Olá tutorial](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="00459-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
