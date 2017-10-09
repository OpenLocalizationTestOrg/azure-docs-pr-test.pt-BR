---
title: aaaManaging Azure recursos com o Gerenciador de nuvem | Microsoft Docs
description: Saiba como toouse Cloud Explorer toobrowse e gerenciar recursos do Azure no Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="651d4-103">Gerenciar recursos de saudação associados às suas contas do Azure no Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="651d4-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="651d4-104">Cloud Explorer permite que você tooview os recursos do Azure e grupos de recursos, inspecionar suas propriedades e executar ações de diagnóstico do desenvolvedor de chave de dentro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="651d4-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="651d4-105">Como Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer baseia-se na pilha do hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="651d4-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="651d4-106">Sendo assim, o Cloud Explorer compreende recursos tais como os grupos de recursos do Azure e serviços do Azure como Aplicativos Lógicos e Aplicativos de API; além disso, ele dá suporte a RBAC [(controle de acesso baseado em função)](active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="651d4-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="651d4-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="651d4-107">Prerequisites</span></span>
- <span data-ttu-id="651d4-108">[2017 do Visual Studio](https://www.visualstudio.com/downloads/) com hello **a carga de trabalho do Azure** selecionado, ou uma versão anterior do Visual Studio com hello [SDK do Microsoft Azure para .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="651d4-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="651d4-109">Conta do Microsoft Azure – se não tiver uma conta do Azure, você poderá [inscrever-se para uma avaliação gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) ou [ativar seus benefícios de assinante do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="651d4-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="651d4-110">tooview Cloud Explorer, selecione **exibição** > **Cloud Explorer** na barra de menus do hello.</span><span class="sxs-lookup"><span data-stu-id="651d4-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="651d4-111">Adicionar um Gerenciador de tooCloud de conta do Azure</span><span class="sxs-lookup"><span data-stu-id="651d4-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="651d4-112">recursos de Olá tooview associados a uma conta do Azure, primeiro você deve adicionar Olá conta tooCloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="651d4-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="651d4-113">No **Cloud Explorer**, selecione **Configurações de conta do Azure**.</span><span class="sxs-lookup"><span data-stu-id="651d4-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Ícone de configurações de conta do Azure do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="651d4-115">Selecione **Adicionar nova conta**.</span><span class="sxs-lookup"><span data-stu-id="651d4-115">Select **Add new account**.</span></span> 

    ![Link de adicionar a conta do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="651d4-117">Faça logon no toohello conta do Azure cujos recursos você deseja toobrowse.</span><span class="sxs-lookup"><span data-stu-id="651d4-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="651d4-118">Depois de conectado tooan conta do Azure, exibem assinaturas Olá associadas a essa conta.</span><span class="sxs-lookup"><span data-stu-id="651d4-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="651d4-119">Selecione Olá caixas de seleção para assinaturas de conta Olá você deseja toobrowse e, em seguida, selecione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="651d4-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Soluções de nuvem: selecione toodisplay assinaturas do Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="651d4-121">Depois de selecionar assinaturas Olá cujos recursos você deseja toobrowse, as assinaturas e os recursos exibem em Olá Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="651d4-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Listagem de recursos do Cloud Explorer para uma conta do Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="651d4-123">Remover uma conta do Azure do Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="651d4-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="651d4-124">No **Cloud Explorer**, selecione **Configurações de conta do Azure**.</span><span class="sxs-lookup"><span data-stu-id="651d4-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Ícone de configurações de conta do Azure do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="651d4-126">Selecione Avançar toohello conta a ser tooremove, **remover**.</span><span class="sxs-lookup"><span data-stu-id="651d4-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Ícone de configurações de conta do Azure do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="651d4-128">Exibir grupos de recursos ou tipos de recursos</span><span class="sxs-lookup"><span data-stu-id="651d4-128">View resource types or resource groups</span></span>
<span data-ttu-id="651d4-129">tooview os recursos do Azure, você pode escolher a **tipos de recurso** ou **grupos de recursos** exibição.</span><span class="sxs-lookup"><span data-stu-id="651d4-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="651d4-130">Em **Cloud Explorer**, selecione Olá suspenso de exibição de recursos.</span><span class="sxs-lookup"><span data-stu-id="651d4-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Exibição do Explorer suspensa lista tooselect Olá desejado recursos de nuvem](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="651d4-132">No menu de contexto hello, selecione o modo de exibição de saudação desejado:</span><span class="sxs-lookup"><span data-stu-id="651d4-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="651d4-133">**Tipos de recurso** exibição - Olá comum usado em Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), mostra os recursos do Azure, categorizados por seu tipo, como aplicativos web, contas de armazenamento e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="651d4-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="651d4-134">**Grupos de recursos** exibir - recursos do Azure categoriza por grupo de recursos do Azure Olá com a qual está associados.</span><span class="sxs-lookup"><span data-stu-id="651d4-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="651d4-135">Um grupo de recursos é um pacote de recursos do Azure, normalmente usados por um aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="651d4-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="651d4-136">toolearn mais sobre grupos de recursos do Azure, consulte [visão geral do Gerenciador de recursos do Azure](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="651d4-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="651d4-137">Olá imagem a seguir mostra uma comparação de saudação dois modos de exibição de recursos:</span><span class="sxs-lookup"><span data-stu-id="651d4-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Comparação de modos de exibição de recurso do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="651d4-139">Exibir e navegar por recursos no Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="651d4-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="651d4-140">toonavigate tooan recursos do Azure e exibir suas informações no Gerenciador de nuvem, expanda tipo hello item ou grupo de recursos associados e, em seguida, selecione o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="651d4-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="651d4-141">Quando você seleciona um recurso, informações são exibidas nas guias Olá dois - **ações** e **propriedades** - na parte inferior de saudação do Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="651d4-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="651d4-142">**Ações** guia - listas Olá ações no Gerenciador de nuvem para o recurso de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="651d4-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="651d4-143">Você também pode exibir essas opções clicando Olá recurso tooview seu menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="651d4-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="651d4-144">**Propriedades** guia - mostra propriedades de saudação de recurso hello, como o seu grupo de tipo, a localidade e o recurso ao qual está associado.</span><span class="sxs-lookup"><span data-stu-id="651d4-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="651d4-145">Olá imagem a seguir mostra uma comparação de exemplo do que você vê em cada guia para um aplicativo de serviço:</span><span class="sxs-lookup"><span data-stu-id="651d4-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="651d4-146">Cada recurso tem a ação de saudação **abrir no portal de**.</span><span class="sxs-lookup"><span data-stu-id="651d4-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="651d4-147">Quando você escolhe essa ação, Cloud Explorer exibe recursos Olá selecionado em Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="651d4-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="651d4-148">Olá **abrir no portal de** recurso é útil para navegar pelos recursos toodeeply aninhado.</span><span class="sxs-lookup"><span data-stu-id="651d4-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="651d4-149">Ações adicionais e valores de propriedade também podem aparecer com base em Olá recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="651d4-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="651d4-150">Por exemplo, aplicativos web e aplicativos lógicos também têm ações Olá **abrir no navegador** e **Anexar depurador** além muito**abrir no portal de**.</span><span class="sxs-lookup"><span data-stu-id="651d4-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="651d4-151">Editores de tooopen ações aparecem quando você escolhe um blob da conta de armazenamento, fila ou tabela.</span><span class="sxs-lookup"><span data-stu-id="651d4-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="651d4-152">Os aplicativos do Azure têm as propriedades **URL** e **Status**, enquanto os recursos de armazenamento têm as propriedades de cadeia de conexão e chave.</span><span class="sxs-lookup"><span data-stu-id="651d4-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="651d4-153">Localizar recursos no Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="651d4-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="651d4-154">recursos toolocate com um nome específico em suas assinaturas de conta do Azure, insira o nome de Olá Olá **pesquisa** caixa Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="651d4-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Localizando recursos no Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="651d4-156">Como inserir caracteres em Olá **pesquisa** caixa, somente os recursos que correspondem a esses caracteres aparecem na árvore de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="651d4-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
