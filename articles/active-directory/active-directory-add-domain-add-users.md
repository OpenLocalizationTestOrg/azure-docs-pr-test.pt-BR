---
title: "domínio personalizado do aaaAssign usuários tooa no Active Directory do Azure | Microsoft Docs"
description: "Como toopopulate um domínio personalizado no Azure Active Directory com contas de usuário."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="6c86a-103">Atribuir usuários tooa o domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="6c86a-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="6c86a-104">Depois que você adicionou tooAzure seu domínio personalizado do Active Directory, você deve adicionar contas de usuário Olá para esse domínio para que você possa começar a autenticá-los.</span><span class="sxs-lookup"><span data-stu-id="6c86a-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c86a-105">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6c86a-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="6c86a-106">Para como toomanage seu nomes de domínio no Centro de administração de saudação do AD do Azure, consulte [gerenciar nomes de domínio personalizado no Active Directory do Azure](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6c86a-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="6c86a-107">Usuários sincronizados por meio de um diretório local</span><span class="sxs-lookup"><span data-stu-id="6c86a-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="6c86a-108">Se você já configurou uma conexão entre o local do Active Directory e o Active Directory do Azure, a sincronização pode preencher contas hello.</span><span class="sxs-lookup"><span data-stu-id="6c86a-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="6c86a-109">Para obter mais informações sobre como toosynchronize do Active Directory do Azure com seu local no Active Directory, consulte [integrando suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="6c86a-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="6c86a-110">Os usuários adicionados e gerenciados em nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="6c86a-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="6c86a-111">domínio de saudação toochange para uma conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="6c86a-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="6c86a-112">Olá Abrir portal clássico do Azure usando uma conta que seja um administrador global ou um administrador do usuário.</span><span class="sxs-lookup"><span data-stu-id="6c86a-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="6c86a-113">Abra seu diretório.</span><span class="sxs-lookup"><span data-stu-id="6c86a-113">Open your directory.</span></span>
3. <span data-ttu-id="6c86a-114">Selecione Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="6c86a-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="6c86a-115">Selecione usuário Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="6c86a-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="6c86a-116">Alterar domínio Olá para usuário hello e, em seguida, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="6c86a-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="6c86a-117">Isso também pode ser feito usando [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou hello [API do Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="6c86a-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="6c86a-118">Selecione um domínio personalizado ao criar um novo usuário</span><span class="sxs-lookup"><span data-stu-id="6c86a-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="6c86a-119">Olá Abrir portal clássico do Azure usando uma conta que seja um administrador global ou um administrador do usuário.</span><span class="sxs-lookup"><span data-stu-id="6c86a-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="6c86a-120">Abra seu diretório.</span><span class="sxs-lookup"><span data-stu-id="6c86a-120">Open your directory.</span></span>
3. <span data-ttu-id="6c86a-121">Selecione Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="6c86a-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="6c86a-122">Na barra de comandos hello, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6c86a-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="6c86a-123">Quando você adiciona um nome de usuário hello, escolha domínio personalizado Olá Olá lista de domínios.</span><span class="sxs-lookup"><span data-stu-id="6c86a-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="6c86a-124">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6c86a-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c86a-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c86a-125">Next steps</span></span>
* [<span data-ttu-id="6c86a-126">Usando o domínio personalizado nomes toosimplify Olá experiência de logon para os usuários</span><span class="sxs-lookup"><span data-stu-id="6c86a-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="6c86a-127">Gerenciar nomes de domínio personalizados</span><span class="sxs-lookup"><span data-stu-id="6c86a-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="6c86a-128">Saiba mais sobre os conceitos de gerenciamento de domínio no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6c86a-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

