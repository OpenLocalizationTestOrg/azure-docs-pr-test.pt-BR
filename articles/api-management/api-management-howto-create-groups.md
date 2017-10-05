---
title: Gerenciar contas de desenvolvedor usando grupos no Gerenciamento de API do Azure | Microsoft Docs
description: Aprenda a gerenciar contas de desenvolvedores usando grupos em Gerenciamento de API do Azure
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
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="a5cd7-103">Como criar e usar grupos para gerenciar contas de desenvolvedor no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="a5cd7-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="a5cd7-104">No Gerenciamento de API, os grupos são usados para gerenciar a visibilidade dos produtos para desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="a5cd7-105">Os produtos ficam visíveis primeiro para os grupos, e depois os desenvolvedores nesses grupos podem ver e assinar os produtos associados aos grupos.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="a5cd7-106">O Gerenciamento de API tem os grupos de sistema imutáveis a seguir.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="a5cd7-107">**Administradores** - os administradores de assinatura do Azure são membros desse grupo.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="a5cd7-108">Os administradores gerenciam instâncias de serviço de Gerenciamento de API, criando as APIs, operações e produtos que são usados pelos desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="a5cd7-109">**Desenvolvedores** - usuários autenticados do portal do desenvolvedor se enquadram nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="a5cd7-110">Os desenvolvedores são clientes que compilam aplicativos usando suas APIs.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="a5cd7-111">Os desenvolvedores têm acesso ao portal do desenvolvedor e criam aplicativos que chamam as operações de uma API.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="a5cd7-112">**Convidados** - os usuários não autenticados no portal do desenvolvedor, tais como potenciais clientes visitando o portal do desenvolvedor de uma instância de Gerenciamento de API, pertencem a esse grupo.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="a5cd7-113">Eles podem receber certos acessos somente leitura, como a capacidade de exibir APIs, mas não de chamá-las.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="a5cd7-114">Além desses grupos de sistema, os administradores podem criar grupos personalizados ou [aproveitar grupos externos em locatários do Azure Active Directory][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="a5cd7-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="a5cd7-115">Grupos personalizados e externos podem ser usados juntamente com grupos de sistema oferecendo visibilidade aos desenvolvedores e acesso a produtos de API.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="a5cd7-116">Por exemplo, você poderia criar um grupo personalizado para os desenvolvedores associados a uma organização parceira específica e conceder acesso às APIs de um produto que contém apenas as APIs relevantes.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="a5cd7-117">Um usuário pode ser um membro de mais de um grupo.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="a5cd7-118">Este guia mostra como administradores de uma instância do Gerenciamento de API podem adicionar novos grupos e associá-los a produtos e desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="a5cd7-119">Além de criar e gerenciar grupos no portal do editor, você pode criar e gerenciar seus grupos usando a entidade [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) da API REST do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="a5cd7-120"><a name="create-group"> </a>Criar um grupo</span><span class="sxs-lookup"><span data-stu-id="a5cd7-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="a5cd7-121">Para criar um novo grupo, clique no **portal do Editor** no Portal do Azure para seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="a5cd7-122">Isso levará você ao portal do editor de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-122">This takes you to the API Management publisher portal.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="a5cd7-124">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a5cd7-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a5cd7-125">Clique em **Grupos** no menu **Gerenciamento de API** à esquerda e depois clique em **Adicionar grupo**.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Adicione o novo grupo][api-management-add-group]

<span data-ttu-id="a5cd7-127">Insira um nome exclusivo e uma descrição opcional para o grupo e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Adicione o novo grupo][api-management-add-group-window]

<span data-ttu-id="a5cd7-129">O novo grupo é exibido na guia de grupos.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="a5cd7-130">Para editar o **Nome** ou a **Descrição** do grupo, clique no nome do grupo na lista.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="a5cd7-131">Para excluir o grupo, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-131">To delete the group, click **Delete**.</span></span>

![Grupo adicionado][api-management-new-group]

<span data-ttu-id="a5cd7-133">Agora que foi criado, o grupo pode ser associado a produtos e desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="a5cd7-134"><a name="associate-group-product"> </a>Associar um grupo a um produto</span><span class="sxs-lookup"><span data-stu-id="a5cd7-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="a5cd7-135">Para associar um grupo a um produto, clique em **Produtos** no menu **Gerenciamento de API** à esquerda e depois clique no nome do produto desejado.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Configurar visibilidade][api-management-add-group-to-product]

<span data-ttu-id="a5cd7-137">Selecione a guia **Visibilidade** para adicionar e remover grupos e para ver os grupos atuais do produto.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="a5cd7-138">Para adicionar ou remover grupos, marque ou desmarque as caixas de seleção correspondentes aos grupos desejados e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Configurar visibilidade][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="a5cd7-140">Para adicionar grupos do Active Directory do Azure, consulte [Como autorizar contas de desenvolvedor usando o Active Directory do Azure no Gerenciamento de API do Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="a5cd7-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="a5cd7-141">Para configurar grupos a partir da guia **Visibilidade** de um produto, clique em **Gerenciar Grupos**.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="a5cd7-142">Após um produto ser associado a um grupo, os desenvolvedores nesse grupo poderão ver e assinar o produto.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="a5cd7-143"><a name="associate-group-developer"> </a>Associar grupos a desenvolvedores</span><span class="sxs-lookup"><span data-stu-id="a5cd7-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="a5cd7-144">Para associar grupos a desenvolvedores, clique em **Usuários** no menu **Gerenciamento de API** à esquerda e marque a caixa de seleção ao lado do desenvolvedor que desejar associar a um grupo.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Adicione o desenvolvedor a um grupo][api-management-add-group-to-developer]

<span data-ttu-id="a5cd7-146">Após os desenvolvedores desejados serem selecionados, clique no grupo desejado no menu suspenso **Adicionar ao grupo** .</span><span class="sxs-lookup"><span data-stu-id="a5cd7-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="a5cd7-147">Os desenvolvedores podem ser removidos dos grupos usando o menu suspenso **Remover do grupo** .</span><span class="sxs-lookup"><span data-stu-id="a5cd7-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Desenvolvedores][api-management-add-group-to-developer-saved]

<span data-ttu-id="a5cd7-149">Após fazer a associação entre o desenvolvedor e o grupo, você poderá vê-la na guia **Usuários** .</span><span class="sxs-lookup"><span data-stu-id="a5cd7-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="a5cd7-150"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5cd7-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="a5cd7-151">Após um desenvolvedor ser associado a um grupo, ele poderá ver e assinar produtos associados ao grupo em questão.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="a5cd7-152">Para obter mais informações, consulte [Como criar e publicar um produto no Gerenciamento de API do Azure][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="a5cd7-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="a5cd7-153">Além de criar e gerenciar grupos no portal do editor, você pode criar e gerenciar seus grupos usando a entidade [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) da API REST do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a5cd7-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
