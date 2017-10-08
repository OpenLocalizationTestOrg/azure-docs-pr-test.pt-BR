---
title: os administradores de servidor aaaManage no Azure Analysis Services | Microsoft Docs
description: Saiba como administradores de servidor toomanage para um servidor do Analysis Services no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="96110-103">Gerenciar administradores de servidor</span><span class="sxs-lookup"><span data-stu-id="96110-103">Manage server administrators</span></span>
<span data-ttu-id="96110-104">Os administradores de servidor devem ser um usuário ou grupo válido no hello Azure Active Directory (AD do Azure) para o locatário Olá em qual Olá servidor reside.</span><span class="sxs-lookup"><span data-stu-id="96110-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="96110-105">Você pode usar **administradores do Analysis Services** na folha de controle Olá para o servidor no portal do Azure ou os administradores de servidor do SSMS toomanage propriedades de servidor.</span><span class="sxs-lookup"><span data-stu-id="96110-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="96110-106">administradores de servidor tooadd usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="96110-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="96110-107">Na folha de controle de saudação do servidor, clique em **administradores do Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="96110-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="96110-108">Em Olá  **\<servername >-os administradores de serviços de análise** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="96110-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="96110-109">Em Olá **adicionar administradores de servidor** folha, selecione as contas de usuário do AD do Azure ou convidar usuários externos por endereço de email.</span><span class="sxs-lookup"><span data-stu-id="96110-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administradores de servidor no portal do Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="96110-111">administradores de servidor tooadd usando o SSMS</span><span class="sxs-lookup"><span data-stu-id="96110-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="96110-112">Servidor de saudação atalho > **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="96110-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="96110-113">Em **Propriedades do Analysis Server**, clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="96110-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="96110-114">Clique em **adicionar**e, em seguida, insira o endereço de email de saudação para um usuário ou grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="96110-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Adicionar administradores do servidor no SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="96110-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96110-116">Next steps</span></span> 
[<span data-ttu-id="96110-117">Autenticação e permissões de usuário</span><span class="sxs-lookup"><span data-stu-id="96110-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="96110-118">Gerenciar usuários e funções de banco de dados</span><span class="sxs-lookup"><span data-stu-id="96110-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="96110-119">Controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="96110-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

