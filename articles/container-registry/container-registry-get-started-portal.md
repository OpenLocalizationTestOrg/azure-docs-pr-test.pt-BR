---
title: registro de Docker privado aaaCreate - portal do Azure | Microsoft Docs
description: "Começar a criar e gerenciar registros privados de contêiner do Docker com hello portal do Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="bee8f-103">Criar um registro de contêiner do Docker privado usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bee8f-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="bee8f-104">Use Olá toocreate portal do Azure um registro de contêiner e gerenciar suas configurações.</span><span class="sxs-lookup"><span data-stu-id="bee8f-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="bee8f-105">Você também pode criar e gerenciar registros de contêiner usando Olá [comandos 2.0 do CLI do Azure](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) ou programaticamente com hello registro de contêiner [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="bee8f-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="bee8f-106">Para o plano de fundo e conceitos, consulte [Olá visão geral](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="bee8f-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="bee8f-107">Criar um registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="bee8f-107">Create a container registry</span></span>
1. <span data-ttu-id="bee8f-108">Em Olá [portal do Azure](https://portal.azure.com), clique em **+ novo**.</span><span class="sxs-lookup"><span data-stu-id="bee8f-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="bee8f-109">Marketplace de saudação de pesquisa para **registro de contêiner do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bee8f-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="bee8f-110">Selecione **Registro de Contêiner do Azure** com o editor **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="bee8f-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="bee8f-111">![Serviço de registro de contêiner no Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="bee8f-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="bee8f-112">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bee8f-112">Click **Create**.</span></span> <span data-ttu-id="bee8f-113">Olá **registro de contêiner do Azure** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="bee8f-113">hello **Azure Container Registry** blade appears.</span></span>

    ![Configurações de registro de contêiner](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="bee8f-115">Em Olá **registro de contêiner do Azure** folha, digite Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="bee8f-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="bee8f-116">Clique em **Criar** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="bee8f-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="bee8f-117">a.</span><span class="sxs-lookup"><span data-stu-id="bee8f-117">a.</span></span> <span data-ttu-id="bee8f-118">**Nome do registro**: um nome de domínio de nível superior exclusivo para o registro específico.</span><span class="sxs-lookup"><span data-stu-id="bee8f-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="bee8f-119">Neste exemplo, o nome de registro de saudação é *myRegistry01*, mas substitua um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="bee8f-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="bee8f-120">nome de saudação pode conter apenas letras e números.</span><span class="sxs-lookup"><span data-stu-id="bee8f-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="bee8f-121">b.</span><span class="sxs-lookup"><span data-stu-id="bee8f-121">b.</span></span> <span data-ttu-id="bee8f-122">**Grupo de recursos**: selecione uma existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de saudação do tipo para um novo.</span><span class="sxs-lookup"><span data-stu-id="bee8f-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="bee8f-123">c.</span><span class="sxs-lookup"><span data-stu-id="bee8f-123">c.</span></span> <span data-ttu-id="bee8f-124">**Local**: selecione um local de data center do Azure onde está o serviço Olá [disponível](https://azure.microsoft.com/regions/services/), como **Centro Sul dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="bee8f-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="bee8f-125">d.</span><span class="sxs-lookup"><span data-stu-id="bee8f-125">d.</span></span> <span data-ttu-id="bee8f-126">**O usuário administrador**: se desejar, habilite um registro de saudação de tooaccess de usuário admin.</span><span class="sxs-lookup"><span data-stu-id="bee8f-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="bee8f-127">Você pode alterar essa configuração após a criação do registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="bee8f-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="bee8f-128">Além disso tooproviding acesso por meio de uma conta de usuário administrador, registros de contêiner oferecem suporte à autenticação com o apoio de entidades de serviço do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="bee8f-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="bee8f-129">Para obter mais informações e considerações, confira [Autenticar em um registro de contêiner](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bee8f-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="bee8f-130">e.</span><span class="sxs-lookup"><span data-stu-id="bee8f-130">e.</span></span> <span data-ttu-id="bee8f-131">**Conta de armazenamento**: usar saudação padrão configuração toocreate uma [conta de armazenamento](../storage/common/storage-introduction.md), ou selecione uma conta de armazenamento existente na Olá mesmo local.</span><span class="sxs-lookup"><span data-stu-id="bee8f-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="bee8f-132">Atualmente, não há suporte para o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="bee8f-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="bee8f-133">Gerenciar configurações do registro</span><span class="sxs-lookup"><span data-stu-id="bee8f-133">Manage registry settings</span></span>
<span data-ttu-id="bee8f-134">Depois de criar o registro de hello, localize Olá as configurações do registro iniciando em hello **registros de contêiner** folha no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="bee8f-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="bee8f-135">Por exemplo, talvez seja necessário Olá toolog de configurações no registro tooyour ou pode ser desejável tooenable ou desabilitar o usuário de administrador hello.</span><span class="sxs-lookup"><span data-stu-id="bee8f-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="bee8f-136">Em Olá **registros de contêiner** folha, clique em nome de saudação do registro.</span><span class="sxs-lookup"><span data-stu-id="bee8f-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![Folha de registro de contêiner](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="bee8f-138">Clique em configurações de acesso toomanage **chave de acesso**.</span><span class="sxs-lookup"><span data-stu-id="bee8f-138">toomanage access settings, click **Access key**.</span></span>

    ![Acesso ao registro de contêiner](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="bee8f-140">Observe Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="bee8f-140">Note hello following settings:</span></span>

   * <span data-ttu-id="bee8f-141">**Servidor de logon** -nome totalmente qualificado do hello usar toolog no registro toohello.</span><span class="sxs-lookup"><span data-stu-id="bee8f-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="bee8f-142">Neste exemplo, é `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="bee8f-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="bee8f-143">**O usuário administrador** - alternar tooenable ou desabilitar a conta de usuário admin do registro hello.</span><span class="sxs-lookup"><span data-stu-id="bee8f-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="bee8f-144">**Nome de usuário** e **senha** -Olá credenciais da conta de usuário de administrador hello (se habilitado) você pode usar toolog no registro toohello.</span><span class="sxs-lookup"><span data-stu-id="bee8f-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="bee8f-145">Opcionalmente, você pode regenerar senhas hello.</span><span class="sxs-lookup"><span data-stu-id="bee8f-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="bee8f-146">As duas senhas são criadas para que você pode manter registro de toohello conexões usando uma senha enquanto você regenera Olá outra senha.</span><span class="sxs-lookup"><span data-stu-id="bee8f-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="bee8f-147">em vez disso, consulte tooauthenticate com uma entidade de serviço [autenticar com um registro de contêiner do Docker particular](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bee8f-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bee8f-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bee8f-148">Next steps</span></span>
* [<span data-ttu-id="bee8f-149">Enviar por push sua primeira imagem usando Olá CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="bee8f-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
