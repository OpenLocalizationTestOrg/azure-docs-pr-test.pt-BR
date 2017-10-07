---
title: "aaaCreate e compartilhar painéis de portal do Azure | Microsoft Docs"
description: "Este artigo explica como toocreate e editar painéis no hello portal do Azure."
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
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a><span data-ttu-id="d49a8-103">Criar e compartilhar dashboards no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d49a8-103">Create and share dashboards in hello Azure portal</span></span>
<span data-ttu-id="d49a8-104">Você pode criar vários painéis e compartilhá-los com outras pessoas que tenham acesso tooyour Azure assinaturas.</span><span class="sxs-lookup"><span data-stu-id="d49a8-104">You can create multiple dashboards and share them with others who have access tooyour Azure subscriptions.</span></span>  <span data-ttu-id="d49a8-105">Este artigo mostra Olá Noções básicas sobre criação, edição, publicação e gerenciamento de acesso toodashboards.</span><span class="sxs-lookup"><span data-stu-id="d49a8-105">This article goes through hello basics of creating, editing, publishing, and managing access toodashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="d49a8-106">Criar um painel</span><span class="sxs-lookup"><span data-stu-id="d49a8-106">Create a dashboard</span></span>
<span data-ttu-id="d49a8-107">toocreate um dashboard, selecione Olá **novo painel** botão Avançar toohello atual do nome do painel.</span><span class="sxs-lookup"><span data-stu-id="d49a8-107">toocreate a dashboard, select hello **New dashboard** button next toohello current dashboard's name.</span></span>  

![criar painel](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="d49a8-109">Essa ação cria um painel novo, vazio, privado e coloca você no modo de personalização onde é possível nomear seu painel e adicionar ou reorganizar blocos.</span><span class="sxs-lookup"><span data-stu-id="d49a8-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="d49a8-110">Nesse modo, Olá recolhível bloco Galeria leva para o menu de navegação à esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="d49a8-110">When in this mode, hello collapsible tile gallery takes over hello left navigation menu.</span></span>  <span data-ttu-id="d49a8-111">Olá Galeria lado a lado permite que você localize lado a lado para recursos do Azure de várias maneiras: você pode procurar por [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), por tipo de recurso, por [marca](../azure-resource-manager/resource-group-using-tags.md), ou por meio de pesquisa para o recurso por nome.</span><span class="sxs-lookup"><span data-stu-id="d49a8-111">hello tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![personalizar painel](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="d49a8-113">Adicione blocos arrastando e soltando na superfície do painel Olá onde desejar.</span><span class="sxs-lookup"><span data-stu-id="d49a8-113">Add tiles by dragging and dropping them onto hello dashboard surface wherever you want.</span></span>

<span data-ttu-id="d49a8-114">Há uma nova categoria chamada **Geral** para blocos que não estejam associados a um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="d49a8-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="d49a8-115">Neste exemplo, podemos fixar o bloco de redução de saudação.</span><span class="sxs-lookup"><span data-stu-id="d49a8-115">In this example, we pin hello Markdown tile.</span></span>  <span data-ttu-id="d49a8-116">Use este painel de tooyour conteúdo personalizado tooadd lado a lado.</span><span class="sxs-lookup"><span data-stu-id="d49a8-116">You use this tile tooadd custom content tooyour dashboard.</span></span>  <span data-ttu-id="d49a8-117">Olá bloco dá suporte a texto sem formatação, [sintaxe de Markdown](https://daringfireball.net/projects/markdown/syntax)e um conjunto limitado de HTML.</span><span class="sxs-lookup"><span data-stu-id="d49a8-117">hello tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="d49a8-118">(Para segurança, você não pode fazer coisas como injetar `<script>` marcas ou usar um determinado elemento de estilo de CSS que possam interferir com o portal de saudação.)</span><span class="sxs-lookup"><span data-stu-id="d49a8-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with hello portal.)</span></span> 

![adicionar markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="d49a8-120">Editar um painel</span><span class="sxs-lookup"><span data-stu-id="d49a8-120">Edit a dashboard</span></span>
<span data-ttu-id="d49a8-121">Depois de criar seu painel, você pode fixar blocos da Galeria de bloco de saudação ou representação de bloco de saudação de folhas.</span><span class="sxs-lookup"><span data-stu-id="d49a8-121">After creating your dashboard, you can pin tiles from hello tile gallery or hello tile representation of blades.</span></span> <span data-ttu-id="d49a8-122">Vamos fixar a representação de saudação do nosso grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d49a8-122">Let's pin hello representation of our resource group.</span></span> <span data-ttu-id="d49a8-123">Você pode fixar ou durante a navegação Olá item ou na folha de grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d49a8-123">You can either pin when browsing hello item, or from hello resource group blade.</span></span> <span data-ttu-id="d49a8-124">Ambas as abordagens resultam em fixação de representação de bloco Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d49a8-124">Both approaches result in pinning hello tile representation of hello resource group.</span></span>

![PIN toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="d49a8-126">Depois de fixar item hello, ele aparece no painel.</span><span class="sxs-lookup"><span data-stu-id="d49a8-126">After pinning hello item, it appears on your dashboard.</span></span>

![exibir painel](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="d49a8-128">Agora que temos um bloco de Markdown e um painel de toohello fixado do grupo de recursos, podemos redimensionar e reorganizar blocos Olá em um layout adequado.</span><span class="sxs-lookup"><span data-stu-id="d49a8-128">Now that we have a Markdown tile and a resource group pinned toohello dashboard, we can resize and rearrange hello tiles into a suitable layout.</span></span>

<span data-ttu-id="d49a8-129">Ao passar o mouse e selecionando "..." ou clicando duas vezes em um bloco, você pode ver todos os comandos de saudação contextuais para esse bloco.</span><span class="sxs-lookup"><span data-stu-id="d49a8-129">By hovering and selecting "…" or right-clicking on a tile you can see all hello contextual commands for that tile.</span></span> <span data-ttu-id="d49a8-130">Por padrão, há dois itens:</span><span class="sxs-lookup"><span data-stu-id="d49a8-130">By default, there are two items:</span></span>

1. <span data-ttu-id="d49a8-131">**Desafixar do painel** – remove Olá bloco do painel Olá</span><span class="sxs-lookup"><span data-stu-id="d49a8-131">**Unpin from dashboard** – removes hello tile from hello dashboard</span></span>
2. <span data-ttu-id="d49a8-132">**Personalizar** – entra no modo de personalização</span><span class="sxs-lookup"><span data-stu-id="d49a8-132">**Customize** – enters customize mode</span></span>

![personalizar bloco](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="d49a8-134">Selecionando Personalizar, você pode redimensionar e reorganizar blocos.</span><span class="sxs-lookup"><span data-stu-id="d49a8-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="d49a8-135">tooresize um bloco, selecione Olá novo tamanho no menu contextual do hello, conforme mostrado no Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="d49a8-135">tooresize a tile, select hello new size from hello contextual menu, as shown in hello following image.</span></span>

![redimensionar bloco](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="d49a8-137">Ou, se o bloco de saudação dá suporte a qualquer tamanho, você pode arrastar o tamanho do hello inferior direito toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="d49a8-137">Or, if hello tile supports any size, you can drag hello bottom right-hand corner toohello desired size.</span></span>

![redimensionar bloco](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="d49a8-139">Depois de redimensionar blocos, exiba o painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="d49a8-139">After resizing tiles, view hello dashboard.</span></span>

![bloco de exibição](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="d49a8-141">Quando terminar de personalizar um painel, basta selecionar Olá **feito personalizando** tooexit Personalizar modo ou com o botão direito e selecione **feito personalizando** Olá no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="d49a8-141">Once you are finished customizing a dashboard, simply select hello **Done customizing** tooexit customize mode or right-click and select **Done customizing** from hello context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="d49a8-142">Publicar um painel e gerenciar o controle de acesso</span><span class="sxs-lookup"><span data-stu-id="d49a8-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="d49a8-143">Quando você cria um painel, é privado por padrão, o que significa que são Olá única pessoa pode vê-lo.</span><span class="sxs-lookup"><span data-stu-id="d49a8-143">When you create a dashboard, it is private by default, which means you are hello only person who can see it.</span></span>  <span data-ttu-id="d49a8-144">toomake-tooothers visíveis, use Olá **compartilhamento** Olá de botão aparece ao lado de outros comandos do painel.</span><span class="sxs-lookup"><span data-stu-id="d49a8-144">toomake it visible tooothers, use hello **Share** button that appears alongside hello other dashboard commands.</span></span>

![compartilhar painel](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="d49a8-146">Você será solicitado toochoose que um assinatura e grupo de recursos para seu painel toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="d49a8-146">You are asked toochoose a subscription and resource group for your dashboard toobe published to.</span></span> <span data-ttu-id="d49a8-147">tooseamlessly integrar painéis em ecossistema hello, implementamos painéis compartilhados como recursos do Azure (de modo que você não pode compartilhar digitando um endereço de email).</span><span class="sxs-lookup"><span data-stu-id="d49a8-147">tooseamlessly integrate dashboards into hello ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="d49a8-148">Acessar toohello informações exibidas pela maioria dos blocos de saudação no portal de saudação são administradas por [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d49a8-148">Access toohello information displayed by most of hello tiles in hello portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="d49a8-149">Do ponto de vista do controle de acesso, os painéis compartilhados não são diferentes de uma máquina virtual ou de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d49a8-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="d49a8-150">Digamos que você tem uma assinatura do Azure e membros da equipe tiverem sido atribuídos a funções de saudação do **proprietário**, **Colaborador**, ou **leitor** de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="d49a8-150">Let's say you have an Azure subscription and members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** of hello subscription.</span></span>  <span data-ttu-id="d49a8-151">Os usuários que são proprietários ou colaboradores são capaz de toolist, exibir, criar, modificar ou excluir painéis em assinatura.</span><span class="sxs-lookup"><span data-stu-id="d49a8-151">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="d49a8-152">Os usuários que são leitores são capaz de toolist e exibir os painéis, mas não podem modificar ou excluí-los.</span><span class="sxs-lookup"><span data-stu-id="d49a8-152">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="d49a8-153">Usuários com acesso de leitor são painel compartilhado do tooa toomake capaz de edições locais, mas são não é possível toopublish server de back toohello essas alterações.</span><span class="sxs-lookup"><span data-stu-id="d49a8-153">Users with reader access are able toomake local edits tooa shared dashboard, but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="d49a8-154">No entanto, eles podem fazer uma cópia privada de dashboard, Olá para seu próprio uso.</span><span class="sxs-lookup"><span data-stu-id="d49a8-154">However, they can make a private copy of hello dashboard for their own use.</span></span>  <span data-ttu-id="d49a8-155">Como sempre, blocos individuais no painel de saudação impõem suas próprias regras de controle de acesso com base nos recursos de saudação corresponder a.</span><span class="sxs-lookup"><span data-stu-id="d49a8-155">As always, individual tiles on hello dashboard enforce their own access control rules based on hello resources they correspond to.</span></span>  

<span data-ttu-id="d49a8-156">Para sua conveniência, portal de saudação da publicação guias experiência em direção a um padrão de onde você coloca painéis em um grupo de recursos chamado **painéis**.</span><span class="sxs-lookup"><span data-stu-id="d49a8-156">For convenience, hello portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![painel de publicação](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="d49a8-158">Você também pode escolher um grupo de recursos específico do painel tooa toopublish.</span><span class="sxs-lookup"><span data-stu-id="d49a8-158">You can also choose toopublish a dashboard tooa particular resource group.</span></span>  <span data-ttu-id="d49a8-159">controle de acesso de saudação para esse painel faz a correspondência de controle de acesso de Olá Olá para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d49a8-159">hello access control for that dashboard matches hello access control for hello resource group.</span></span>  <span data-ttu-id="d49a8-160">Os usuários que podem gerenciar recursos Olá desse grupo de recursos também têm acesso toohello painéis.</span><span class="sxs-lookup"><span data-stu-id="d49a8-160">Users that can manage hello resources in that resource group also have access toohello dashboards.</span></span>

![publicar um grupo do painel tooresource](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="d49a8-162">Depois que o painel é publicado, Olá **compartilhamento + acesso** painel de controle será atualizar e mostram informações sobre o painel publicado hello, incluindo um link toomanage usuário acesso toohello painel de controle.</span><span class="sxs-lookup"><span data-stu-id="d49a8-162">After your dashboard is published, hello **Sharing + access** control pane will refresh and show you information about hello published dashboard, including a link toomanage user access toohello dashboard.</span></span>  <span data-ttu-id="d49a8-163">Isso inicia saudação padrão de controle de acesso baseado em função folha usada toomanage acesso para qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="d49a8-163">This link launches hello standard Role Based Access Control blade used toomanage access for any Azure resource.</span></span>  <span data-ttu-id="d49a8-164">Você pode sempre voltar toothis exibição selecionando **compartilhamento**.</span><span class="sxs-lookup"><span data-stu-id="d49a8-164">You can always get back toothis view by selecting **Share**.</span></span>

![gerenciar o controle de acesso](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="d49a8-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d49a8-166">Next steps</span></span>
* <span data-ttu-id="d49a8-167">toomanage recursos, consulte [recursos de gerenciamento Azure por meio do portal](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d49a8-167">toomanage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="d49a8-168">toodeploy recursos, consulte [implantar recursos com modelos do Gerenciador de recursos e o portal do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d49a8-168">toodeploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

