---
title: contas de desenvolvedor aaaManage usando grupos no gerenciamento de API do Azure | Microsoft Docs
description: Saiba como desenvolvedor toomanage contas usando grupos no gerenciamento de API do Azure
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="ae487-103">Como desenvolvedor de toomanage grupos toocreate e usar contas no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="ae487-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="ae487-104">No gerenciamento de API, os grupos são usados toomanage Olá visibilidade de produtos toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="ae487-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="ae487-105">Os produtos são primeiro toogroups visíveis feitas e, em seguida, os desenvolvedores desses grupos podem exibir e assinar toohello produtos que estão associados a grupos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae487-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="ae487-106">Gerenciamento de API tem Olá seguintes grupos de sistema imutável.</span><span class="sxs-lookup"><span data-stu-id="ae487-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="ae487-107">**Administradores** - os administradores de assinatura do Azure são membros desse grupo.</span><span class="sxs-lookup"><span data-stu-id="ae487-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="ae487-108">Os administradores gerenciar instâncias do serviço de gerenciamento de API, criando Olá APIs, operações e produtos que são usados pelos desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="ae487-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="ae487-109">**Desenvolvedores** - usuários autenticados do portal do desenvolvedor se enquadram nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="ae487-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="ae487-110">Os desenvolvedores são clientes Olá que desenvolvem aplicativos utilizando suas APIs.</span><span class="sxs-lookup"><span data-stu-id="ae487-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="ae487-111">Os desenvolvedores recebem o portal do desenvolvedor do access toohello e criarem aplicativos que chamar operações de saudação de uma API.</span><span class="sxs-lookup"><span data-stu-id="ae487-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="ae487-112">**Convidados** -usuários portal do desenvolvedor, como clientes potenciais visitando o portal do desenvolvedor de saudação de uma queda de instância de gerenciamento de API para este grupo não autenticados.</span><span class="sxs-lookup"><span data-stu-id="ae487-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="ae487-113">Eles podem ser concedidos determinado acesso somente leitura, como Olá capacidade tooview APIs, mas não chamá-los.</span><span class="sxs-lookup"><span data-stu-id="ae487-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="ae487-114">Em grupos de sistema de toothese de adição, os administradores podem criar grupos personalizados ou [aproveitar grupos externos nos locatários do Active Directory do Azure associados][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="ae487-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="ae487-115">Grupos externos e personalizados podem ser usados juntamente com grupos de sistema ao dar visibilidade a desenvolvedores e acessar tooAPI produtos.</span><span class="sxs-lookup"><span data-stu-id="ae487-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="ae487-116">Por exemplo, você pode criar um grupo personalizado para desenvolvedores associados a uma determinada organização do parceiro e permitem acesso toohello APIs de um produto que contém apenas as APIs relevantes.</span><span class="sxs-lookup"><span data-stu-id="ae487-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="ae487-117">Um usuário pode ser um membro de mais de um grupo.</span><span class="sxs-lookup"><span data-stu-id="ae487-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="ae487-118">Este guia mostra como administradores de uma instância do Gerenciamento de API podem adicionar novos grupos e associá-los a produtos e desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="ae487-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="ae487-119">Além disso toocreating e gerenciar grupos no portal do publicador hello, você pode criar e gerenciar seus grupos usando Olá API de REST de gerenciamento de API [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entidade.</span><span class="sxs-lookup"><span data-stu-id="ae487-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="ae487-120"><a name="create-group"> </a>Criar um grupo</span><span class="sxs-lookup"><span data-stu-id="ae487-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="ae487-121">toocreate um novo grupo, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="ae487-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="ae487-122">Isso leva toohello portal do publicador de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="ae487-122">This takes you toohello API Management publisher portal.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="ae487-124">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ae487-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="ae487-125">Clique em **grupos** de saudação **gerenciamento de API** menu saudação à esquerda e clique **adicionar grupo**.</span><span class="sxs-lookup"><span data-stu-id="ae487-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![Adicione o novo grupo][api-management-add-group]

<span data-ttu-id="ae487-127">Insira um nome exclusivo para o grupo de saudação e uma descrição opcional e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="ae487-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![Adicione o novo grupo][api-management-add-group-window]

<span data-ttu-id="ae487-129">Olá novo grupo é exibido na saudação do hello grupos na guia tooedit **nome** ou **descrição** do grupo Olá, clique o nome de saudação do grupo de saudação na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae487-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="ae487-130">grupo de saudação toodelete, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="ae487-130">toodelete hello group, click **Delete**.</span></span>

![Grupo adicionado][api-management-new-group]

<span data-ttu-id="ae487-132">Agora que hello grupo é criado, ele pode ser associado com produtos e desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="ae487-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="ae487-133"><a name="associate-group-product"> </a>Associar um grupo a um produto</span><span class="sxs-lookup"><span data-stu-id="ae487-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="ae487-134">tooassociate um grupo com um produto, clique em **produtos** de saudação **gerenciamento de API** menu saudação à esquerda e clique em nome de saudação do produto desejado hello.</span><span class="sxs-lookup"><span data-stu-id="ae487-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![Configurar visibilidade][api-management-add-group-to-product]

<span data-ttu-id="ae487-136">Selecione Olá **visibilidade** guia tooadd e remover grupos e tooview Olá atual de grupos de produto hello.</span><span class="sxs-lookup"><span data-stu-id="ae487-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="ae487-137">tooadd ou remover grupos, marque ou desmarque as caixas de seleção de saudação para Olá desejado grupos e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="ae487-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![Configurar visibilidade][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="ae487-139">tooadd grupos do Active Directory do Azure, consulte [como desenvolvedor tooauthorize contas usando Active Directory do Azure no gerenciamento de API do Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="ae487-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="ae487-140">grupos de tooconfigure de saudação **visibilidade** para um produto, clique em **gerenciar grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae487-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="ae487-141">Quando um produto está associado um grupo, os desenvolvedores nesse grupo podem exibir e assinar toohello produto.</span><span class="sxs-lookup"><span data-stu-id="ae487-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="ae487-142"><a name="associate-group-developer"> </a>Associar grupos a desenvolvedores</span><span class="sxs-lookup"><span data-stu-id="ae487-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="ae487-143">grupos de tooassociate com os desenvolvedores, clique em **usuários** de saudação **gerenciamento de API** menu saudação à esquerda e, em seguida, caixa Olá de seleção ao lado de desenvolvedores Olá desejar tooassociate com um grupo.</span><span class="sxs-lookup"><span data-stu-id="ae487-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![Adicionar toogroup de desenvolvedor][api-management-add-group-to-developer]

<span data-ttu-id="ae487-145">Depois de saudação desejado desenvolvedores são verificados, clique em grupo desejado de saudação em hello **adicionar tooGroup** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="ae487-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="ae487-146">Os desenvolvedores podem ser removidos dos grupos usando Olá **remover do grupo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="ae487-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![Desenvolvedores][api-management-add-group-to-developer-saved]

<span data-ttu-id="ae487-148">Depois que a associação Olá é adicionada entre desenvolvedor hello e grupo hello, você pode exibi-lo no hello **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="ae487-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="ae487-149"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae487-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="ae487-150">Depois que um desenvolvedor é adicionado tooa grupo, eles podem exibir e assinar toohello produtos associados ao grupo.</span><span class="sxs-lookup"><span data-stu-id="ae487-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="ae487-151">Para obter mais informações, consulte [Como criar e publicar um produto no Gerenciamento de API do Azure][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="ae487-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="ae487-152">Além disso toocreating e gerenciar grupos no portal do publicador hello, você pode criar e gerenciar seus grupos usando Olá API de REST de gerenciamento de API [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entidade.</span><span class="sxs-lookup"><span data-stu-id="ae487-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
