---
title: Gerenciar administradores de servidor no Azure Analysis Services | Microsoft Docs
description: Saiba como gerenciar administradores de servidor para um servidor do Analysis Services no Azure.
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
ms.openlocfilehash: a1b58125dafdf73f245b6a8cd0f4917513b22ea9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="a775d-103">Gerenciar administradores de servidor</span><span class="sxs-lookup"><span data-stu-id="a775d-103">Manage server administrators</span></span>
<span data-ttu-id="a775d-104">Os administradores do servidor devem ser um usuário ou grupo válido no Azure AD (Azure Active Directory) para o locatário no qual o servidor reside.</span><span class="sxs-lookup"><span data-stu-id="a775d-104">Server administrators must be a valid user or group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="a775d-105">Você pode usar os **Administradores do Analysis Services** na folha de controle de seu servidor no portal do Azure ou nas Propriedades do Servidor no SSMS para gerenciar os administradores de servidor.</span><span class="sxs-lookup"><span data-stu-id="a775d-105">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="a775d-106">Para adicionar administradores do servidor usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a775d-106">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="a775d-107">Na folha de controle do seu servidor, clique em **os administradores de serviços de análise de**.</span><span class="sxs-lookup"><span data-stu-id="a775d-107">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="a775d-108">Na folha  **\<nomedoservidor >- Administradores de Serviços de Análise**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a775d-108">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="a775d-109">Na folha **Adicionar Administradores de Servidor**, selecione as contas de usuário do Azure AD ou convide usuários externos por meio de endereço de email.</span><span class="sxs-lookup"><span data-stu-id="a775d-109">In the **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administradores de servidor no portal do Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="a775d-111">Para adicionar administradores do servidor usando o SSMS</span><span class="sxs-lookup"><span data-stu-id="a775d-111">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="a775d-112">Clique com botão direito do mouse em servidor > **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="a775d-112">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="a775d-113">Em **Propriedades do Analysis Server**, clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="a775d-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="a775d-114">Clique em **Adicionar** e, em seguida, insira o endereço de email de um usuário ou grupo em seu Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a775d-114">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![Adicionar administradores do servidor no SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="a775d-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a775d-116">Next steps</span></span> 
[<span data-ttu-id="a775d-117">Autenticação e permissões de usuário</span><span class="sxs-lookup"><span data-stu-id="a775d-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="a775d-118">Gerenciar usuários e funções de banco de dados</span><span class="sxs-lookup"><span data-stu-id="a775d-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="a775d-119">Controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="a775d-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

