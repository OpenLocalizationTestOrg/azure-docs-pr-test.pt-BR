---
title: "Exigir a atribuição de usuário – Azure AD| Microsoft Docs"
description: "Como exigir a atribuição de usuários para aplicativos do Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a><span data-ttu-id="0742c-103">Azure AD e aplicativos: exigir atribuição de usuário</span><span class="sxs-lookup"><span data-stu-id="0742c-103">Azure AD and applications: Require user assignment</span></span>
## <a name="requiring-user-assignment"></a><span data-ttu-id="0742c-104">Exigindo atribuição do usuário</span><span class="sxs-lookup"><span data-stu-id="0742c-104">Requiring User Assignment</span></span>
1. <span data-ttu-id="0742c-105">Faça logon no Portal do Azure com uma conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="0742c-105">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="0742c-106">Clique no item **Todos os Itens** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="0742c-106">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="0742c-107">Escolha o diretório que você está usando para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0742c-107">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="0742c-108">Clique na guia **APLICATIVOS** .</span><span class="sxs-lookup"><span data-stu-id="0742c-108">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="0742c-109">Selecione o aplicativo na lista de aplicativos associada ao diretório.</span><span class="sxs-lookup"><span data-stu-id="0742c-109">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="0742c-110">Clique na guia **CONFIGURAR** .</span><span class="sxs-lookup"><span data-stu-id="0742c-110">Click the **CONFIGURE** tab.</span></span>
7. <span data-ttu-id="0742c-111">Altere **Atribuição do usuário necessária para acessar o aplicativo** para Sim.</span><span class="sxs-lookup"><span data-stu-id="0742c-111">Change the **User Assignment Required to Access App** toggle to Yes.</span></span>
8. <span data-ttu-id="0742c-112">Clique no botão **Salvar** na parte inferior da tela.</span><span class="sxs-lookup"><span data-stu-id="0742c-112">Click the **Save** button at the bottom of the screen.</span></span>

<span data-ttu-id="0742c-113">Agora, você precisará atribuir usuários e/ou grupos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0742c-113">You will now have to assign users and/or groups to the application.</span></span> <span data-ttu-id="0742c-114">Consulte [Atribuir usuários a um aplicativo](active-directory-applications-guiding-developers-assigning-users.md) e [Atribuir grupos a um aplicativo](active-directory-applications-guiding-developers-assigning-groups.md).</span><span class="sxs-lookup"><span data-stu-id="0742c-114">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0742c-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0742c-115">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
