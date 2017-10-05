---
title: "Criar e compartilhar painéis do Portal do Azure | Microsoft Docs"
description: "Este artigo explica como criar e editar painéis no portal do Azure."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 5429e68723448ff5db6ef0ed8da1b927e97e6dd9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-share-dashboards-in-the-azure-portal"></a><span data-ttu-id="f873a-103">Criar e compartilhar painéis no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f873a-103">Create and share dashboards in the Azure portal</span></span>
<span data-ttu-id="f873a-104">Você pode criar vários painéis e compartilhá-los com outras pessoas que tenham acesso às suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f873a-104">You can create multiple dashboards and share them with others who have access to your Azure subscriptions.</span></span>  <span data-ttu-id="f873a-105">Este artigo percorre as noções básicas da criação/edição, publicação e gerenciamento de acesso aos painéis.</span><span class="sxs-lookup"><span data-stu-id="f873a-105">This article goes through the basics of creating, editing, publishing, and managing access to dashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="f873a-106">Criar um painel</span><span class="sxs-lookup"><span data-stu-id="f873a-106">Create a dashboard</span></span>
<span data-ttu-id="f873a-107">Para criar um painel, selecione o botão **Novo painel** ao lado do nome do painel atual.</span><span class="sxs-lookup"><span data-stu-id="f873a-107">To create a dashboard, select the **New dashboard** button next to the current dashboard's name.</span></span>  

![criar painel](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="f873a-109">Essa ação cria um painel novo, vazio, privado e coloca você no modo de personalização onde é possível nomear seu painel e adicionar ou reorganizar blocos.</span><span class="sxs-lookup"><span data-stu-id="f873a-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="f873a-110">Nesse modo, a galeria de blocos recolhíveis assume o menu de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f873a-110">When in this mode, the collapsible tile gallery takes over the left navigation menu.</span></span>  <span data-ttu-id="f873a-111">A galeria de blocos permite que você encontre blocos para os recursos do Azure de várias maneiras: você pode procurar por [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), pelo tipo de recurso, por [marca](../azure-resource-manager/resource-group-using-tags.md) ou procurando por seus recursos por nome.</span><span class="sxs-lookup"><span data-stu-id="f873a-111">The tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![personalizar painel](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="f873a-113">Adicione blocos arrastando e soltando-os na superfície do painel onde você desejar.</span><span class="sxs-lookup"><span data-stu-id="f873a-113">Add tiles by dragging and dropping them onto the dashboard surface wherever you want.</span></span>

<span data-ttu-id="f873a-114">Há uma nova categoria chamada **Geral** para blocos que não estejam associados a um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="f873a-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="f873a-115">Neste exemplo, podemos fixar o bloco Markdown.</span><span class="sxs-lookup"><span data-stu-id="f873a-115">In this example, we pin the Markdown tile.</span></span>  <span data-ttu-id="f873a-116">Use este bloco para adicionar conteúdo personalizado ao seu painel.</span><span class="sxs-lookup"><span data-stu-id="f873a-116">You use this tile to add custom content to your dashboard.</span></span>  <span data-ttu-id="f873a-117">O bloco dá suporte a texto sem formatação, [sintaxe de Markdown](https://daringfireball.net/projects/markdown/syntax)e um conjunto limitado de HTML.</span><span class="sxs-lookup"><span data-stu-id="f873a-117">The tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="f873a-118">(Para segurança, você não pode fazer coisas como injetar marcas `<script>` ou usar um determinado elemento de estilo de CSS que podem interferir com o portal).</span><span class="sxs-lookup"><span data-stu-id="f873a-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with the portal.)</span></span> 

![adicionar markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="f873a-120">Editar um painel</span><span class="sxs-lookup"><span data-stu-id="f873a-120">Edit a dashboard</span></span>
<span data-ttu-id="f873a-121">Depois de criar seu painel, você pode fixar blocos da galeria de blocos ou a representação de bloco de folhas.</span><span class="sxs-lookup"><span data-stu-id="f873a-121">After creating your dashboard, you can pin tiles from the tile gallery or the tile representation of blades.</span></span> <span data-ttu-id="f873a-122">Vamos fixar a representação do nosso grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f873a-122">Let's pin the representation of our resource group.</span></span> <span data-ttu-id="f873a-123">Você pode fixar ao procurar o item, ou da folha do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f873a-123">You can either pin when browsing the item, or from the resource group blade.</span></span> <span data-ttu-id="f873a-124">As duas abordagens resultam na fixação da representação do bloco do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f873a-124">Both approaches result in pinning the tile representation of the resource group.</span></span>

![Fixar no painel](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="f873a-126">Depois de fixar o item, ele aparecerá em seu painel.</span><span class="sxs-lookup"><span data-stu-id="f873a-126">After pinning the item, it appears on your dashboard.</span></span>

![exibir painel](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="f873a-128">Agora que temos um bloco Markdown e um grupo de recursos fixado ao painel, podemos redimensionar e reorganizar os blocos em um layout adequado.</span><span class="sxs-lookup"><span data-stu-id="f873a-128">Now that we have a Markdown tile and a resource group pinned to the dashboard, we can resize and rearrange the tiles into a suitable layout.</span></span>

<span data-ttu-id="f873a-129">Ao passar o mouse e selecionar "…" ou clicar com o botão direito do mouse em um bloco, você poderá ver todos os comandos contextuais do bloco.</span><span class="sxs-lookup"><span data-stu-id="f873a-129">By hovering and selecting "…" or right-clicking on a tile you can see all the contextual commands for that tile.</span></span> <span data-ttu-id="f873a-130">Por padrão, há dois itens:</span><span class="sxs-lookup"><span data-stu-id="f873a-130">By default, there are two items:</span></span>

1. <span data-ttu-id="f873a-131">**Desafixar do painel** – remove o bloco do painel</span><span class="sxs-lookup"><span data-stu-id="f873a-131">**Unpin from dashboard** – removes the tile from the dashboard</span></span>
2. <span data-ttu-id="f873a-132">**Personalizar** – entra no modo de personalização</span><span class="sxs-lookup"><span data-stu-id="f873a-132">**Customize** – enters customize mode</span></span>

![personalizar bloco](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="f873a-134">Selecionando Personalizar, você pode redimensionar e reorganizar blocos.</span><span class="sxs-lookup"><span data-stu-id="f873a-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="f873a-135">Para redimensionar uma imagem, selecione o novo tamanho no menu contextual, conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="f873a-135">To resize a tile, select the new size from the contextual menu, as shown in the following image.</span></span>

![redimensionar bloco](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="f873a-137">Ou, se o bloco der suporte a qualquer tamanho, você poderá arrastar o canto inferior direito para o tamanho desejado.</span><span class="sxs-lookup"><span data-stu-id="f873a-137">Or, if the tile supports any size, you can drag the bottom right-hand corner to the desired size.</span></span>

![redimensionar bloco](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="f873a-139">Depois de redimensionar os blocos, exiba o painel.</span><span class="sxs-lookup"><span data-stu-id="f873a-139">After resizing tiles, view the dashboard.</span></span>

![bloco de exibição](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="f873a-141">Quando tiver concluído a personalização de um painel, basta selecionar **Personalização concluída** para sair no modo de personalização ou pressione o botão direito do mouse e selecione **Personalização concluída** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="f873a-141">Once you are finished customizing a dashboard, simply select the **Done customizing** to exit customize mode or right-click and select **Done customizing** from the context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="f873a-142">Publicar um painel e gerenciar o controle de acesso</span><span class="sxs-lookup"><span data-stu-id="f873a-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="f873a-143">Quando você cria um painel, ele será privado por padrão, o que significa que você é a única pessoa que pode vê-lo.</span><span class="sxs-lookup"><span data-stu-id="f873a-143">When you create a dashboard, it is private by default, which means you are the only person who can see it.</span></span>  <span data-ttu-id="f873a-144">Para torná-lo visível para outras pessoas, use o botão **Compartilhar** exibido juntamente com os outros comandos do painel.</span><span class="sxs-lookup"><span data-stu-id="f873a-144">To make it visible to others, use the **Share** button that appears alongside the other dashboard commands.</span></span>

![compartilhar painel](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="f873a-146">Será solicitado que você escolha uma assinatura e o grupo de recursos para que seu painel seja publicado.</span><span class="sxs-lookup"><span data-stu-id="f873a-146">You are asked to choose a subscription and resource group for your dashboard to be published to.</span></span> <span data-ttu-id="f873a-147">Para integrar totalmente os painéis ao ecossistema, implementamos painéis compartilhados como recursos do Azure (e, por isso, não é possível compartilhar ao digitar um endereço de email).</span><span class="sxs-lookup"><span data-stu-id="f873a-147">To seamlessly integrate dashboards into the ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="f873a-148">O acesso às informações exibidas pela maioria dos blocos no portal é controlado pelo [Controle de Acesso Baseado em Função do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f873a-148">Access to the information displayed by most of the tiles in the portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="f873a-149">Do ponto de vista do controle de acesso, os painéis compartilhados não são diferentes de uma máquina virtual ou de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f873a-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="f873a-150">Digamos que você tenha uma assinatura do Azure e membros de sua equipe receberam as funções de **proprietário**, **colaborador** ou **leitor** da assinatura.</span><span class="sxs-lookup"><span data-stu-id="f873a-150">Let's say you have an Azure subscription and members of your team have been assigned the roles of **owner**, **contributor**, or **reader** of the subscription.</span></span>  <span data-ttu-id="f873a-151">Os usuários que são proprietários ou colaboradores podem listar, exibir, criar, modificar ou excluir painéis na assinatura.</span><span class="sxs-lookup"><span data-stu-id="f873a-151">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="f873a-152">Os usuários que são os leitores podem listar e exibir os painéis, mas não podem modificá-los ou excluí-los.</span><span class="sxs-lookup"><span data-stu-id="f873a-152">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="f873a-153">Os usuários com acesso de leitor podem fazer edições locais em um painel compartilhado, mas não podem publicar essas alterações no servidor.</span><span class="sxs-lookup"><span data-stu-id="f873a-153">Users with reader access are able to make local edits to a shared dashboard, but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="f873a-154">No entanto, eles podem fazer uma cópia privada do painel para seu próprio uso.</span><span class="sxs-lookup"><span data-stu-id="f873a-154">However, they can make a private copy of the dashboard for their own use.</span></span>  <span data-ttu-id="f873a-155">Como sempre, os blocos individuais no painel impõem suas próprias regras de controle de acesso com base nos recursos aos quais eles correspondem.</span><span class="sxs-lookup"><span data-stu-id="f873a-155">As always, individual tiles on the dashboard enforce their own access control rules based on the resources they correspond to.</span></span>  

<span data-ttu-id="f873a-156">Para sua conveniência, a experiência de publicação do portal guia você por um padrão onde você coloca painéis em um grupo de recursos chamado **painéis**.</span><span class="sxs-lookup"><span data-stu-id="f873a-156">For convenience, the portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![painel de publicação](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="f873a-158">Você pode optar por publicar um painel em um determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f873a-158">You can also choose to publish a dashboard to a particular resource group.</span></span>  <span data-ttu-id="f873a-159">O controle de acesso para esse painel corresponde ao controle de acesso para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f873a-159">The access control for that dashboard matches the access control for the resource group.</span></span>  <span data-ttu-id="f873a-160">Os usuários que podem gerenciar os recursos desse grupo de recursos também têm acesso aos painéis.</span><span class="sxs-lookup"><span data-stu-id="f873a-160">Users that can manage the resources in that resource group also have access to the dashboards.</span></span>

![painel de publicação para o grupo de recursos](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="f873a-162">Depois que o painel é publicado, o painel de controle **Compartilhamento + acesso** será atualizado e mostrará informações sobre o painel publicado, incluindo um link para gerenciar o acesso de usuário ao painel.</span><span class="sxs-lookup"><span data-stu-id="f873a-162">After your dashboard is published, the **Sharing + access** control pane will refresh and show you information about the published dashboard, including a link to manage user access to the dashboard.</span></span>  <span data-ttu-id="f873a-163">Isso inicia a folha Controle de Acesso Baseado em Função padrão usada para gerenciar o acesso a qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="f873a-163">This link launches the standard Role Based Access Control blade used to manage access for any Azure resource.</span></span>  <span data-ttu-id="f873a-164">Você sempre pode voltar a esta exibição ao selecionar **Compartilhar**.</span><span class="sxs-lookup"><span data-stu-id="f873a-164">You can always get back to this view by selecting **Share**.</span></span>

![gerenciar o controle de acesso](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="f873a-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f873a-166">Next steps</span></span>
* <span data-ttu-id="f873a-167">Para gerenciar recursos, veja [Gerenciar recursos do Azure pelo portal](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f873a-167">To manage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="f873a-168">Para implantar recursos, confira [Implantar recursos com modelos do Resource Manager e o Portal do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f873a-168">To deploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

