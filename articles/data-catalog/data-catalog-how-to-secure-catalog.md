---
title: "aaaHow toosecure acesso tooAzure catálogo de dados | Microsoft Docs"
description: "Este artigo explica como toosecure catálogo de dados e seus ativos de dados."
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
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="aedfd-103">Como toosecure acessar ativos de dados e o catálogo de toodata</span><span class="sxs-lookup"><span data-stu-id="aedfd-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="aedfd-104">Este recurso está disponível somente na edição standard de saudação do catálogo de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="aedfd-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="aedfd-105">Catálogo de dados do Azure permite que você toospecify quem pode acessar o catálogo de dados hello e quais operações (registrar, anotar, apropriar-se) eles podem executar em metadados no catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aedfd-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="aedfd-106">Usuários e permissões do catálogo</span><span class="sxs-lookup"><span data-stu-id="aedfd-106">Catalog users and permissions</span></span>
<span data-ttu-id="aedfd-107">toogive um usuário ou uma saudação grupo acessar o catálogo de dados tooa e definir permissões:</span><span class="sxs-lookup"><span data-stu-id="aedfd-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="aedfd-108">Em Olá [home page do seu catálogo de dados](http://www.azuredatacatalog.com), clique em **configurações** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="aedfd-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![catálogo de dados – configurações](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="aedfd-110">Na página de configurações de Olá, expanda Olá **usuários catálogo** seção.</span><span class="sxs-lookup"><span data-stu-id="aedfd-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="aedfd-111">![Catálogo de Usuários – Adicionar](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="aedfd-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="aedfd-112">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="aedfd-112">Click **Add**.</span></span>
4. <span data-ttu-id="aedfd-113">Digite hello totalmente qualificado **nome de usuário** ou nome de saudação **grupo de segurança** no hello Azure AAD (Active Directory) associado com o catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aedfd-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="aedfd-114">Use vírgula (', ') como um separador se você estiver adicionando mais de um usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="aedfd-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="aedfd-115">![Usuários do Catálogo – usuários ou grupos](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="aedfd-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="aedfd-116">Pressione **ENTER** ou **guia** fora da caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="aedfd-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="aedfd-117">Confirme se todas as permissões (**anotar**, **registrar**, e **Take Ownership**) são atribuídos toothese usuários ou grupos por padrão.</span><span class="sxs-lookup"><span data-stu-id="aedfd-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="aedfd-118">Ou seja, Olá usuário ou grupo pode [registrar ativos de dados]( data-catalog-how-to-register.md), [anotar os ativos de dados]( data-catalog-how-to-annotate.md), e [assumir a propriedade de ativos de dados]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="aedfd-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="aedfd-119">![Usuários do Catálogo – permissões padrão](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="aedfd-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="aedfd-120">toogive um usuário ou grupo apenas Olá leitura acessar toohello catálogo, desmarque Olá **anotar** opção para esse usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="aedfd-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="aedfd-121">Quando você fizer isso, Olá usuário ou grupo não é possível anotar os ativos de dados no catálogo de hello, mas eles podem exibi-los.</span><span class="sxs-lookup"><span data-stu-id="aedfd-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="aedfd-122">toodeny um usuário ou grupo do registro de recursos de dados, desmarque Olá **registrar** opção para esse usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="aedfd-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="aedfd-123">toodeny um usuário de assumir a propriedade de um ativo de dados, desmarque Olá **apropriar** opção para esse usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="aedfd-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="aedfd-124">toodelete um usuário/grupo de usuários do catálogo, clique em **x** para Olá/grupo de usuário final Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="aedfd-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="aedfd-125">![Usuários do Catálogo – excluir usuário](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="aedfd-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="aedfd-126">É recomendável que você adiciona usuários de toocatalog de grupos de segurança em vez de adicionar usuários diretamente e atribuir permissões.</span><span class="sxs-lookup"><span data-stu-id="aedfd-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="aedfd-127">Em seguida, adicione os grupos de segurança de toohello de usuários que correspondem ao seu catálogo de toohello de acesso necessários e suas funções.</span><span class="sxs-lookup"><span data-stu-id="aedfd-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="aedfd-128">Considerações especiais</span><span class="sxs-lookup"><span data-stu-id="aedfd-128">Special considerations</span></span>

- <span data-ttu-id="aedfd-129">permissões de saudação atribuídas a grupos de toosecurity são aditivas.</span><span class="sxs-lookup"><span data-stu-id="aedfd-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="aedfd-130">Digamos que um usuário esteja em dois grupos.</span><span class="sxs-lookup"><span data-stu-id="aedfd-130">Say, a user is in two groups.</span></span> <span data-ttu-id="aedfd-131">Um grupo tem permissões para anotar e outro grupo não tem permissões para anotar.</span><span class="sxs-lookup"><span data-stu-id="aedfd-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="aedfd-132">Nesse caso, o usuário tem permissões para anotar.</span><span class="sxs-lookup"><span data-stu-id="aedfd-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="aedfd-133">permissões de saudação atribuídas explicitamente tooa Olá de substituição de usuário as permissões atribuídas toogroups toowhich Olá usuário pertence.</span><span class="sxs-lookup"><span data-stu-id="aedfd-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="aedfd-134">No exemplo anterior de saudação, digamos que você adicionou o hello usuário toocatalog usuários explicitamente e não atribua permissões de anotar.</span><span class="sxs-lookup"><span data-stu-id="aedfd-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="aedfd-135">usuário Olá não pode anotar os ativos de dados mesmo que o usuário Olá é um membro de um grupo que tenha permissões de anotar.</span><span class="sxs-lookup"><span data-stu-id="aedfd-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aedfd-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aedfd-136">Next steps</span></span>
- [<span data-ttu-id="aedfd-137">Introdução ao Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="aedfd-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

