---
title: "Criar um grupo para usuários no Azure Active Directory | Microsoft Docs"
description: Como criar um grupo no Azure Active Directory e adicionar membros ao grupo
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d3d37761a9fdf9bd9801396d45f2fcd47efb0be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="ea28a-103">Criar um grupo e adicionar membros no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea28a-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea28a-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ea28a-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="ea28a-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="ea28a-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="ea28a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea28a-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="ea28a-107">Este artigo explica como criar e popular um novo grupo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea28a-107">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="ea28a-108">Use um grupo para executar tarefas de gerenciamento, como a atribuição de licenças ou permissões a vários usuários ou dispositivos de uma vez.</span><span class="sxs-lookup"><span data-stu-id="ea28a-108">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="ea28a-109">Como faço para criar um grupo?</span><span class="sxs-lookup"><span data-stu-id="ea28a-109">How do I create a group?</span></span>
1. <span data-ttu-id="ea28a-110">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="ea28a-110">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="ea28a-111">Selecione **Mais serviços**, digite **Usuário e grupos** na caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ea28a-111">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="ea28a-113">Na folha **Usuários e grupos**, escolha **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="ea28a-113">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Abrir a folha de grupos](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="ea28a-115">Na folha **Usuários e grupos – Todos os grupos**, selecione o comando **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ea28a-115">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![Selecionando o comando Adicionar](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="ea28a-117">Na folha **Grupo** , adicione um nome e uma descrição ao grupo.</span><span class="sxs-lookup"><span data-stu-id="ea28a-117">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="ea28a-118">Para selecionar os membros a serem adicionados ao grupo, selecione **Atribuído** na caixa **Tipo de associação** e, em seguida, selecione **Membros**.</span><span class="sxs-lookup"><span data-stu-id="ea28a-118">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="ea28a-119">Para saber mais sobre como gerenciar a associação de um grupo dinamicamente, consulte [Usar atributos para criar regras avançadas para a associação de grupo](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ea28a-119">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Selecionando membros para adicionar](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="ea28a-121">Na folha **Membros**, escolha um ou mais usuários ou dispositivos para adicionar ao grupo e escolha o botão **Selecionar** na parte inferior da folha para adicioná-los ao grupo.</span><span class="sxs-lookup"><span data-stu-id="ea28a-121">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="ea28a-122">A caixa **Usuário** filtra a exibição com base na correspondência de sua entrada com qualquer parte de um nome de usuário ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ea28a-122">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="ea28a-123">Caracteres curinga não são aceitos nessa caixa.</span><span class="sxs-lookup"><span data-stu-id="ea28a-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="ea28a-124">Quando terminar de adicionar membros ao grupo, selecione **Criar** na folha **Grupo**.</span><span class="sxs-lookup"><span data-stu-id="ea28a-124">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![Criar a confirmação do grupo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="ea28a-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea28a-126">Next steps</span></span>
<span data-ttu-id="ea28a-127">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea28a-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="ea28a-128">Consultar grupos existentes</span><span class="sxs-lookup"><span data-stu-id="ea28a-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="ea28a-129">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="ea28a-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="ea28a-130">Gerenciar membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="ea28a-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="ea28a-131">Gerenciar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="ea28a-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="ea28a-132">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="ea28a-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
