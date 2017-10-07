---
title: "aaaCreate um grupo de usuários no Active Directory do Azure | Microsoft Docs"
description: Como toocreate um grupo no Active Directory do Azure e adicionar membros toohello grupo
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
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="e014d-103">Criar um grupo e adicionar membros no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e014d-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e014d-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e014d-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="e014d-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="e014d-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="e014d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e014d-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="e014d-107">Este artigo explica como toocreate e popular um novo grupo no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="e014d-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="e014d-108">Use as tarefas de gerenciamento de tooperform um grupo como a atribuição de permissões ou licenças tooa o número de usuários ou dispositivos de uma vez.</span><span class="sxs-lookup"><span data-stu-id="e014d-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="e014d-109">Como faço para criar um grupo?</span><span class="sxs-lookup"><span data-stu-id="e014d-109">How do I create a group?</span></span>
1. <span data-ttu-id="e014d-110">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e014d-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e014d-111">Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e014d-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="e014d-113">Em Olá **usuários e grupos** folha, selecione **todos os grupos de**.</span><span class="sxs-lookup"><span data-stu-id="e014d-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Folha de grupos de saudação de abertura](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="e014d-115">Em Olá **usuários e grupos - todos os grupos de** folha, selecione Olá **adicionar** comando.</span><span class="sxs-lookup"><span data-stu-id="e014d-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![Selecionando o comando Add a saudação](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="e014d-117">Em Olá **grupo** folha, adicionar um nome e uma descrição para o grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e014d-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="e014d-118">tooselect membros tooadd toohello grupo, selecione **atribuído** em Olá **tipo de associação** caixa e, em seguida, selecione **membros**.</span><span class="sxs-lookup"><span data-stu-id="e014d-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="e014d-119">Para obter mais informações sobre como toomanage Olá associação de um grupo dinamicamente, consulte [usar atributos toocreate avançado regras de associação de grupo](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e014d-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Selecionando membros tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="e014d-121">Em Olá **membros** folha, selecione um ou mais usuários ou dispositivos de grupo de toohello de tooadd e selecione Olá **selecione** botão na parte inferior de saudação do hello folha tooadd-los toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="e014d-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="e014d-122">Olá **usuário** caixa filtra Olá com base na correspondência de sua parte de tooany de entrada de um nome de usuário ou dispositivo de exibição.</span><span class="sxs-lookup"><span data-stu-id="e014d-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="e014d-123">Caracteres curinga não são aceitos nessa caixa.</span><span class="sxs-lookup"><span data-stu-id="e014d-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="e014d-124">Quando terminar de adicionar o grupo de membros do toohello, selecione **criar** em Olá **grupo** folha.</span><span class="sxs-lookup"><span data-stu-id="e014d-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Criar a confirmação do grupo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="e014d-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e014d-126">Next steps</span></span>
<span data-ttu-id="e014d-127">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="e014d-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e014d-128">Consultar grupos existentes</span><span class="sxs-lookup"><span data-stu-id="e014d-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e014d-129">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="e014d-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="e014d-130">Gerenciar membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="e014d-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="e014d-131">Gerenciar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="e014d-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="e014d-132">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="e014d-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
