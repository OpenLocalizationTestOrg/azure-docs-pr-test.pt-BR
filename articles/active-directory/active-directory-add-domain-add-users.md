---
title: "Atribuir usuários a um domínio personalizado no Azure Active Directory | Microsoft Docs"
description: "Como preencher um domínio personalizado no Active Directory do Azure com contas de usuário."
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
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="ad39f-103">Atribuir usuários a um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ad39f-103">Assign users to a custom domain</span></span>
<span data-ttu-id="ad39f-104">Após ter adicionado seu domínio personalizado ao Active Directory do Azure, você deve adicionar as contas de usuário a esse domínio para que possa começar a autenticá-los.</span><span class="sxs-lookup"><span data-stu-id="ad39f-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad39f-105">A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ad39f-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="ad39f-106">Para saber como gerenciar seus nomes de domínio no centro de administração do Azure AD, consulte [Gerenciando nomes de domínio personalizados no Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ad39f-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="ad39f-107">Usuários sincronizados por meio de um diretório local</span><span class="sxs-lookup"><span data-stu-id="ad39f-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="ad39f-108">Se você já configurou uma conexão entre seu Active Directory local e o Active Directory do Azure, a sincronização poderá preencher as contas.</span><span class="sxs-lookup"><span data-stu-id="ad39f-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="ad39f-109">Para obter mais informações sobre como sincronizar o Active Directory do Azure com o Active Directory local, consulte [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ad39f-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="ad39f-110">Usuários adicionados e gerenciados na nuvem</span><span class="sxs-lookup"><span data-stu-id="ad39f-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="ad39f-111">Para alterar o domínio para uma conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="ad39f-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="ad39f-112">Abra o portal clássico do Azure usando uma conta que seja um administrador global ou administrador de usuário.</span><span class="sxs-lookup"><span data-stu-id="ad39f-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="ad39f-113">Abra seu diretório.</span><span class="sxs-lookup"><span data-stu-id="ad39f-113">Open your directory.</span></span>
3. <span data-ttu-id="ad39f-114">Clique a guia **Usuários** .</span><span class="sxs-lookup"><span data-stu-id="ad39f-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="ad39f-115">Selecione o usuário na lista.</span><span class="sxs-lookup"><span data-stu-id="ad39f-115">Select the user from the list.</span></span>
5. <span data-ttu-id="ad39f-116">Altere o domínio para o usuário e selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ad39f-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="ad39f-117">Isso também pode ser feito usando o [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou a [API do Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="ad39f-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="ad39f-118">Selecione um domínio personalizado ao criar um novo usuário</span><span class="sxs-lookup"><span data-stu-id="ad39f-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="ad39f-119">Abra o portal clássico do Azure usando uma conta que seja um administrador global ou administrador de usuário.</span><span class="sxs-lookup"><span data-stu-id="ad39f-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="ad39f-120">Abra seu diretório.</span><span class="sxs-lookup"><span data-stu-id="ad39f-120">Open your directory.</span></span>
3. <span data-ttu-id="ad39f-121">Clique a guia **Usuários** .</span><span class="sxs-lookup"><span data-stu-id="ad39f-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="ad39f-122">Na barra de comandos, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ad39f-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="ad39f-123">Quando adicionar o nome de usuário, escolha o domínio personalizado na lista de domínios.</span><span class="sxs-lookup"><span data-stu-id="ad39f-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="ad39f-124">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ad39f-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad39f-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ad39f-125">Next steps</span></span>
* [<span data-ttu-id="ad39f-126">Como usar nomes de domínio personalizados para simplificar a experiência de conexão para os usuários</span><span class="sxs-lookup"><span data-stu-id="ad39f-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="ad39f-127">Gerenciar nomes de domínio personalizados</span><span class="sxs-lookup"><span data-stu-id="ad39f-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="ad39f-128">Saiba mais sobre os conceitos de gerenciamento de domínio no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ad39f-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

