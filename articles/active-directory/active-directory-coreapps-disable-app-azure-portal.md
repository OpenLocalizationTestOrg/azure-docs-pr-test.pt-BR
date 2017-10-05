---
title: "Desabilitar entradas de usuário em um aplicativo empresarial no Azure Active Directory | Microsoft Docs"
description: "Como desabilitar um aplicativo empresarial para que nenhum usuário possa entrar nele no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="98712-103">Desabilitar entradas de usuário em um aplicativo empresarial no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98712-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="98712-104">É fácil desabilitar um aplicativo empresarial para que nenhum usuário possa entrar nele no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="98712-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="98712-105">Você deve ter as permissões apropriadas para gerenciar o aplicativo empresarial, além de ser um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="98712-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="98712-106">Como desabilitar entradas de usuário?</span><span class="sxs-lookup"><span data-stu-id="98712-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="98712-107">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="98712-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="98712-108">Escolha **Mais serviços**, insira **Azure Active Directory** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="98712-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="98712-109">Na folha **Azure Active Directory –**  -  ***nomedodiretório*** (ou seja, a folha do Azure AD para o diretório que você está gerenciando), escolha **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="98712-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="98712-111">Na folha **Aplicativos empresariais**, escolha **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="98712-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="98712-112">Você verá uma lista dos aplicativos que pode gerenciar.</span><span class="sxs-lookup"><span data-stu-id="98712-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="98712-113">Na folha **Aplicativos empresariais – Todos os aplicativos** , escolha um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="98712-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="98712-114">Na folha ***nomedoaplicativo*** (ou seja, a folha com o nome do aplicativo escolhido no título), escolha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="98712-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Seleção do comando todos os aplicativos](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="98712-116">Na folha ***nomedoaplicativo*** -  **Propriedades**, escolha **Não** para **Habilitado para usuários entrarem?**.</span><span class="sxs-lookup"><span data-stu-id="98712-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="98712-117">Escolha o comando **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="98712-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98712-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98712-118">Next steps</span></span>
* [<span data-ttu-id="98712-119">Ver todos os meus grupos</span><span class="sxs-lookup"><span data-stu-id="98712-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="98712-120">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="98712-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="98712-121">Remover uma atribuição de usuário ou de grupo de um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="98712-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="98712-122">Alterar o nome ou logotipo de um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="98712-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
