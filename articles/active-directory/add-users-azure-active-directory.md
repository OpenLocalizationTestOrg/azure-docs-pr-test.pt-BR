---
title: "aaaAdd novo tooAzure de usuários do Active Directory | Microsoft Docs"
description: "Explica como tooadd novos usuários no Active Directory do Azure."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="e0f1f-103">Início rápido: Adicionar novo tooAzure de usuários do Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0f1f-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="e0f1f-104">Este artigo explica como tooadd novos usuários em sua organização em hello Azure Active Directory (AD do Azure) uma por vez usando Olá portal do Azure ou sincronizando seu usuário do Windows Server AD local dados da conta.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="e0f1f-105">Adicionar usuários baseados em nuvem</span><span class="sxs-lookup"><span data-stu-id="e0f1f-105">Add cloud-based users</span></span>
1. <span data-ttu-id="e0f1f-106">Entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e0f1f-107">Selecione **Azure Active Directory** e, em seguida, **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="e0f1f-108">Em Olá **usuários e grupos** folha, selecione **todos os usuários**e, em seguida, selecione **novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="e0f1f-109">![Selecionando o comando Add a saudação](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="e0f1f-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="e0f1f-110">Insira detalhes para usuário hello, como **nome** e **nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="e0f1f-111">Olá parte do nome de domínio do nome de usuário Olá deve estar saudação inicial padrão domínio nome "[nome de domínio].onmicrosoft.com" ou verificado, não federado [nome de domínio personalizado](add-custom-domain.md) como "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="e0f1f-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="e0f1f-112">Cópia ou caso contrário hello de Observação senha gerada pelo usuário para que você possa fornecê-lo toohello usuário depois que o processo seja concluído.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="e0f1f-113">Opcionalmente, você pode abrir e preencha as informações de Olá Olá **perfil** folha, Olá **grupos** folha ou hello **função de diretório** folha para usuário hello.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="e0f1f-114">Para obter mais informações sobre funções de usuário e administrador, consulte [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e0f1f-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="e0f1f-115">Em Olá **usuário** folha, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="e0f1f-116">Com segurança distribua Olá gerado senha toohello novo usuário de forma que hello usuário possa acessar.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="e0f1f-117">Você também pode sincronizar dados de conta de usuário do Windows Server AD local.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="e0f1f-118">Soluções de identidade da Microsoft abrangem locais e recursos baseados em nuvem, criando uma identidade de usuário único para autenticação e autorização tooall recursos, independentemente do local.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="e0f1f-119">Chamamos isso de Identidade Híbrida.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="e0f1f-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) pode ser usado toointegrate seus diretórios locais com o Active Directory do Azure para cenários de identidade híbrida.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="e0f1f-121">Isso permite que você tooprovide uma identidade comum para os usuários para aplicativos do Office 365, Azure e SaaS integrada ao AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="e0f1f-122">Excluir usuários do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0f1f-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="e0f1f-123">Entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e0f1f-124">Selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="e0f1f-125">Em Olá **usuários e grupos** folha, selecione Olá toodelete de usuário na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="e0f1f-126">Na folha de saudação do usuário selecionado hello, selecione **visão geral**e, em seguida, na barra de comandos hello, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="e0f1f-127">![Selecionando o comando Add a saudação](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="e0f1f-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="e0f1f-128">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="e0f1f-128">Learn more</span></span> 
* [<span data-ttu-id="e0f1f-129">Adicionar um usuário externo</span><span class="sxs-lookup"><span data-stu-id="e0f1f-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="e0f1f-130">Atribuir uma função de usuário tooa no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0f1f-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="e0f1f-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0f1f-131">Next steps</span></span>
<span data-ttu-id="e0f1f-132">Este guia de início rápido, você aprendeu como tooadd de novos usuários tooAzure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="e0f1f-133">Você pode usar o hello para seguir link toocreate um novo usuário no AD do Azure de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f1f-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e0f1f-134">Adicionar usuários tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="e0f1f-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
