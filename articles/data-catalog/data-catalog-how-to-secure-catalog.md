---
title: "Como proteger o acesso ao Catálogo de Dados do Azure | Microsoft Docs"
description: "Este artigo explica como proteger o catálogo de dados e seus ativos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: 9664a7bc8493b08c8e0797ac6f1b212079829833
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-secure-access-to-data-catalog-and-data-assets"></a><span data-ttu-id="3450a-103">Como proteger o acesso ao catálogo de dados e ativos de dados</span><span class="sxs-lookup"><span data-stu-id="3450a-103">How to secure access to data catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3450a-104">Esse recurso está disponível somente na Standard Edition do Catálogo de Dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="3450a-104">This feature is available only in the standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="3450a-105">O Catálogo de Dados do Azure permite que você especifique quem pode acessar o catálogo de dados e quais operações (registrar, anotar, apropriar-se) eles podem executar em metadados no catálogo.</span><span class="sxs-lookup"><span data-stu-id="3450a-105">Azure Data Catalog allows you to specify who can access the data catalog and what operations (register, annotate, take ownership) they can perform on metadata in the catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="3450a-106">Usuários e permissões do catálogo</span><span class="sxs-lookup"><span data-stu-id="3450a-106">Catalog users and permissions</span></span>
<span data-ttu-id="3450a-107">Para dar a um usuário ou grupo o acesso a um catálogo de dados e definir permissões:</span><span class="sxs-lookup"><span data-stu-id="3450a-107">To give a user or a group the access to a data catalog and set permissions:</span></span>

1. <span data-ttu-id="3450a-108">Na [home page do seu catálogo de dados](http://www.azuredatacatalog.com), clique em **Configurações** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="3450a-108">On the [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on the toolbar.</span></span>

    ![catálogo de dados – configurações](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="3450a-110">Na página configurações, expanda a seção **Usuários do Catálogo**.</span><span class="sxs-lookup"><span data-stu-id="3450a-110">In the settings page, expand the **Catalog Users** section.</span></span>
    <span data-ttu-id="3450a-111">![Catálogo de Usuários – Adicionar](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="3450a-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="3450a-112">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3450a-112">Click **Add**.</span></span>
4. <span data-ttu-id="3450a-113">Insira o **nome de usuário** totalmente qualificado ou nome do **grupo de segurança** no AAD (Azure Active Directory) associado ao catálogo.</span><span class="sxs-lookup"><span data-stu-id="3450a-113">Enter the fully qualified **user name** or name of the **security group** in the Azure Active Directory (AAD) associated with the catalog.</span></span> <span data-ttu-id="3450a-114">Use vírgula (', ') como um separador se você estiver adicionando mais de um usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="3450a-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="3450a-115">![Usuários do Catálogo – usuários ou grupos](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="3450a-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="3450a-116">Pressione **ENTER** ou **TAB** fora da caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3450a-116">Press **ENTER** or **TAB** out of the text box.</span></span> 
6.  <span data-ttu-id="3450a-117">Confirme que todas as permissões (**Anotar**, **Registrar** e **Apropriar-se**) sejam atribuídos a esses usuários ou grupos por padrão.</span><span class="sxs-lookup"><span data-stu-id="3450a-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned to these users or groups by default.</span></span> <span data-ttu-id="3450a-118">Ou seja, o usuário ou grupo pode [registrar ativos de dados]( data-catalog-how-to-register.md), [anotar os ativos de dados]( data-catalog-how-to-annotate.md) e [assumir a propriedade de ativos de dados]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="3450a-118">That is, the user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="3450a-119">![Usuários do Catálogo – permissões padrão](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="3450a-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="3450a-120">Para conceder a um usuário ou grupo apenas o acesso de leitura para o catálogo, desmarque a opção **anotar** para esse usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="3450a-120">To give a user or group only the read access to the catalog, clear the **annotate** option for that user or group.</span></span> <span data-ttu-id="3450a-121">Quando você fizer isso, o usuário ou grupo não poderá anotar os ativos de dados no catálogo, mas poderá exibi-los.</span><span class="sxs-lookup"><span data-stu-id="3450a-121">When you do so, the user or group cannot annotate data assets in the catalog but they can view them.</span></span> 
8.  <span data-ttu-id="3450a-122">Para negar a um usuário ou grupo o registro de recursos de dados, desmarque a opção **registrar** para esse usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="3450a-122">To deny a user or group from registering data assets, clear the **register** option for that user or group.</span></span>
9.  <span data-ttu-id="3450a-123">Para negar que um usuário assuma a propriedade de um ativo de dados, desmarque a opção **apropriar-se** para esse usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="3450a-123">To deny a user from taking ownership of a data asset, clear the **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="3450a-124">Para excluir um usuário/grupo de usuários do catálogo, clique em **x** para o usuário/grupo na parte inferior da lista.</span><span class="sxs-lookup"><span data-stu-id="3450a-124">To delete a user/group from catalog users, click **x** for the user/group at the bottom of the list.</span></span> 
    <span data-ttu-id="3450a-125">![Usuários do Catálogo – excluir usuário](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="3450a-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3450a-126">É recomendável que você adicione grupos de segurança para usuários do catálogo em vez de adicionar usuários diretamente e atribuir permissões.</span><span class="sxs-lookup"><span data-stu-id="3450a-126">We recommend that you add security groups to catalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="3450a-127">Em seguida, adicione usuários a grupos de segurança que correspondam às funções e ao acesso necessário ao catálogo desses usuários.</span><span class="sxs-lookup"><span data-stu-id="3450a-127">Then, add users to the security groups that match their roles and their required access to the catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="3450a-128">Considerações especiais</span><span class="sxs-lookup"><span data-stu-id="3450a-128">Special considerations</span></span>

- <span data-ttu-id="3450a-129">As permissões atribuídas a grupos de segurança são aditivas.</span><span class="sxs-lookup"><span data-stu-id="3450a-129">The permissions assigned to security groups are additive.</span></span> <span data-ttu-id="3450a-130">Digamos que um usuário esteja em dois grupos.</span><span class="sxs-lookup"><span data-stu-id="3450a-130">Say, a user is in two groups.</span></span> <span data-ttu-id="3450a-131">Um grupo tem permissões para anotar e outro grupo não tem permissões para anotar.</span><span class="sxs-lookup"><span data-stu-id="3450a-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="3450a-132">Nesse caso, o usuário tem permissões para anotar.</span><span class="sxs-lookup"><span data-stu-id="3450a-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="3450a-133">As permissões atribuídas explicitamente a um usuário substituem as permissões atribuídas a grupos aos quais o usuário pertence.</span><span class="sxs-lookup"><span data-stu-id="3450a-133">The permissions assigned explicitly to a user override the permissions assigned to groups to which the user belongs.</span></span> <span data-ttu-id="3450a-134">No exemplo anterior, digamos, você adicionou explicitamente o usuário a usuários do catálogo e não atribuiu permissões para anotar.</span><span class="sxs-lookup"><span data-stu-id="3450a-134">In the previous example, say, you explicitly added the user to catalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="3450a-135">O usuário não pode anotar os ativos de dados mesmo que o usuário seja um membro de um grupo que tenha permissões para anotar.</span><span class="sxs-lookup"><span data-stu-id="3450a-135">The user cannot annotate data assets even though the user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3450a-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3450a-136">Next steps</span></span>
- [<span data-ttu-id="3450a-137">Introdução ao Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="3450a-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

