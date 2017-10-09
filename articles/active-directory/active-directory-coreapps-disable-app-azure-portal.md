---
title: "aaaDisable entradas do usuário para um aplicativo de empresa no Active Directory do Azure | Microsoft Docs"
description: "Como toodisable um aplicativo corporativo para que nenhum usuário pode entrar tooit no Active Directory do Azure"
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
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="ac978-103">Desabilitar entradas de usuário em um aplicativo empresarial no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac978-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="ac978-104">É fácil toodisable um aplicativo corporativo para que nenhum usuário pode entrar tooit no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ac978-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ac978-105">Você deve ter Olá permissões apropriadas toomanage Olá enterprise aplicativo e deve ser o administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac978-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="ac978-106">Como desabilitar entradas de usuário?</span><span class="sxs-lookup"><span data-stu-id="ac978-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="ac978-107">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac978-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="ac978-108">Selecione **mais serviços**, digite **Active Directory do Azure** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac978-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="ac978-109">Em Olá **Active Directory do Azure** -  ***directoryname*** folha (ou seja, Olá AD do Azure folha para diretório de saudação que você está gerenciando), selecione **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ac978-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="ac978-111">Em Olá **aplicativos empresariais** folha, selecione **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ac978-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="ac978-112">Você ver uma lista de aplicativos de saudação, que você pode gerenciar.</span><span class="sxs-lookup"><span data-stu-id="ac978-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="ac978-113">Em Olá **aplicativos corporativos - todos os aplicativos** folha, selecione um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac978-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="ac978-114">Em Olá ***appname*** folha (ou seja, Olá folha com nome Olá Olá o aplicativo selecionado no título de saudação), selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="ac978-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![Selecionando Olá comando de todos os aplicativos](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="ac978-116">Em Olá ***appname*** - **propriedades** folha, selecione **não** para **habilitada para usuários em toosign?**.</span><span class="sxs-lookup"><span data-stu-id="ac978-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="ac978-117">Selecione Olá **salvar** comando.</span><span class="sxs-lookup"><span data-stu-id="ac978-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac978-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac978-118">Next steps</span></span>
* [<span data-ttu-id="ac978-119">Ver todos os meus grupos</span><span class="sxs-lookup"><span data-stu-id="ac978-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="ac978-120">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="ac978-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="ac978-121">Remover uma atribuição de usuário ou de grupo de um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="ac978-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="ac978-122">Alterar nome de saudação ou logotipo de um aplicativo corporativo</span><span class="sxs-lookup"><span data-stu-id="ac978-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
