---
title: Atribuir grupos aos aplicativos do Azure AD | Microsoft Docs
description: "Como implementar a atribuição de grupos para aplicativos do Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="e347f-103">Atribuir grupos do Azure Active Directory a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="e347f-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="e347f-104">Antes de atribuir usuários e grupos a um aplicativo, você precisa exigir a atribuição de usuários.</span><span class="sxs-lookup"><span data-stu-id="e347f-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="e347f-105">Para saber como exigir a atribuição de usuário, consulte o artigo [Exigindo Atribuição de Usuário](active-directory-applications-guiding-developers-requiring-user-assignment.md) .</span><span class="sxs-lookup"><span data-stu-id="e347f-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="e347f-106">Este artigo pressupõe que você já tenha criado grupos no Active Directory que está usando para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e347f-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="e347f-107">Atribuindo grupos a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="e347f-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="e347f-108">Faça logon no Portal do Azure com uma conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="e347f-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="e347f-109">Clique no item **Todos os Itens** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="e347f-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="e347f-110">Escolha o diretório que você está usando para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e347f-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="e347f-111">Clique na guia **APLICATIVOS** .</span><span class="sxs-lookup"><span data-stu-id="e347f-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="e347f-112">Selecione o aplicativo na lista de aplicativos associada ao diretório.</span><span class="sxs-lookup"><span data-stu-id="e347f-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="e347f-113">Clique na guia **USUÁRIOS E GRUPOS** .</span><span class="sxs-lookup"><span data-stu-id="e347f-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="e347f-114">Filtre a lista de grupos no Active Directory usando a lista suspensa **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="e347f-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="e347f-115">Selecione o grupo.</span><span class="sxs-lookup"><span data-stu-id="e347f-115">Select the group.</span></span>
9. <span data-ttu-id="e347f-116">Clique em **ATRIBUIR**.</span><span class="sxs-lookup"><span data-stu-id="e347f-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="e347f-117">Clique em **sim** quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="e347f-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e347f-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e347f-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
