---
title: "Introdução ao acesso condicional no Azure Active Directory | Microsoft Docs"
description: "Teste o acesso condicional usando uma condição de local."
services: active-directory
keywords: "acesso condicional para aplicativos, acesso condicional com o Azure AD, acesso seguro aos recursos da empresa, políticas de acesso condicional"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="5c5a0-104">Introdução ao acesso condicional no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c5a0-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="5c5a0-105">O acesso condicional é um recurso do Azure Active Directory que permite que você defina as condições sob as quais os usuários autorizados possam acessar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="5c5a0-106">Este tópico fornece instruções para testar um acesso condicional com base em uma condição de local em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="5c5a0-107">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5c5a0-107">Scenario description</span></span>

<span data-ttu-id="5c5a0-108">É um requisito comum em muitas organizações só exigir autenticação multifator para acesso a aplicativos que não é executado desde a intranet corporativa.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="5c5a0-109">Com o Azure Active Directory, você pode facilmente atingir essa meta, configurando uma política de acesso condicional com base no local.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="5c5a0-110">Este tópico fornece instruções detalhadas sobre como configurar uma política relacionada.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="5c5a0-111">A política aproveita os [IPs confiáveis](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) para distinguir entre tentativas de acesso de rede da intranet e todos os outros locais.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5c5a0-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c5a0-112">Prerequisites</span></span>

<span data-ttu-id="5c5a0-113">O cenário descrito neste tópico pressupõe que você esteja familiarizado com os conceitos descritos em [Acesso condicional do Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c5a0-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="5c5a0-114">Para testar este cenário, você precisa:</span><span class="sxs-lookup"><span data-stu-id="5c5a0-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="5c5a0-115">Criar um usuário de teste</span><span class="sxs-lookup"><span data-stu-id="5c5a0-115">Create a test user</span></span> 

- <span data-ttu-id="5c5a0-116">Atribuir uma licença do Azure AD Premium ao usuário de teste</span><span class="sxs-lookup"><span data-stu-id="5c5a0-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="5c5a0-117">Configurar um aplicativo gerenciado e atribuir o usuário de teste a ele</span><span class="sxs-lookup"><span data-stu-id="5c5a0-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="5c5a0-118">Configurar IPs confiáveis</span><span class="sxs-lookup"><span data-stu-id="5c5a0-118">Configure trusted IPs</span></span>

<span data-ttu-id="5c5a0-119">Se você precisar de mais detalhes sobre IPs confiáveis, veja [IPs confiáveis](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="5c5a0-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="5c5a0-120">Etapas de configuração de política</span><span class="sxs-lookup"><span data-stu-id="5c5a0-120">Policy configuration steps</span></span>

<span data-ttu-id="5c5a0-121">**Para configurar a política de acesso condicional, execute:**</span><span class="sxs-lookup"><span data-stu-id="5c5a0-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="5c5a0-122">No portal do Azure, na barra de navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="5c5a0-124">Na folha **Azure Active Directory**, na seção **Gerenciar**, clique em **Acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="5c5a0-126">Na folha **Acesso Condicional**, para abrir a folha **Novo**, na barra de ferramentas na parte superior, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="5c5a0-128">Na folha **Novo**, na caixa de texto **Nome**, digite um nome para a política.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="5c5a0-130">Na seção **Atribuição**, clique em **Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="5c5a0-132">Na folha **Usuários e grupos**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c5a0-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="5c5a0-134">a.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-134">a.</span></span> <span data-ttu-id="5c5a0-135">Clique em **Selecionar usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="5c5a0-136">b.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-136">b.</span></span> <span data-ttu-id="5c5a0-137">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-137">Click **Select**.</span></span>

    <span data-ttu-id="5c5a0-138">c.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-138">c.</span></span> <span data-ttu-id="5c5a0-139">Na folha **Selecionar**, selecione seu usuário de teste e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="5c5a0-140">d.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-140">d.</span></span> <span data-ttu-id="5c5a0-141">Na folha **Usuários e grupos**, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="5c5a0-142">Na folha **Novo**, para abrir a folha **Aplicativos de nuvem**, na seção **Atribuição**, clique em **Aplicativos de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="5c5a0-144">Na folha **Aplicativos de nuvem**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c5a0-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="5c5a0-146">a.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-146">a.</span></span> <span data-ttu-id="5c5a0-147">Clique em **Selecionar aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-147">Click **Select apps**.</span></span>

    <span data-ttu-id="5c5a0-148">b.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-148">b.</span></span> <span data-ttu-id="5c5a0-149">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-149">Click **Select**.</span></span>

    <span data-ttu-id="5c5a0-150">c.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-150">c.</span></span> <span data-ttu-id="5c5a0-151">Na folha **Selecionar**, selecione seu aplicativo em nuvem e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="5c5a0-152">d.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-152">d.</span></span> <span data-ttu-id="5c5a0-153">Na folha **Aplicativos de nuvem**, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="5c5a0-154">Na folha **Novo**, para abrir a folha **Condições**, na seção **Atribuição**, clique em **Condições**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="5c5a0-156">Na folha **Condições**, para abrir a folha **Locais**, clique em **Locais**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="5c5a0-158">Na folha **Locais**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c5a0-158">On the **Locations** blade, perform the following steps:</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="5c5a0-160">a.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-160">a.</span></span> <span data-ttu-id="5c5a0-161">Em **Configurar**, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="5c5a0-162">b.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-162">b.</span></span> <span data-ttu-id="5c5a0-163">Em **Incluir**, clique em **Todos os locais**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="5c5a0-164">c.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-164">c.</span></span> <span data-ttu-id="5c5a0-165">Clique em **Excluir** e clique em **Todos os IPs confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="5c5a0-167">d.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-167">d.</span></span> <span data-ttu-id="5c5a0-168">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-168">Click **Done**.</span></span>

12. <span data-ttu-id="5c5a0-169">Na folha **Condições**, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="5c5a0-170">Na folha **Novo**, para abrir a folha **Conceder**, na seção **Controles**, clique em **Conceder**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="5c5a0-172">Na folha **Conceder**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c5a0-172">On the **Grant** blade, perform the following steps:</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="5c5a0-174">a.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-174">a.</span></span> <span data-ttu-id="5c5a0-175">Selecione **Exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="5c5a0-176">b.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-176">b.</span></span> <span data-ttu-id="5c5a0-177">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-177">Click **Select**.</span></span>

15. <span data-ttu-id="5c5a0-178">Na folha **Novo**, em **Habilitar política**, clique em **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="5c5a0-180">Na folha **Novo**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="5c5a0-181">Testar a política</span><span class="sxs-lookup"><span data-stu-id="5c5a0-181">Testing the policy</span></span>

<span data-ttu-id="5c5a0-182">Para testar sua política, você deve acessar o aplicativo de um dispositivo que:</span><span class="sxs-lookup"><span data-stu-id="5c5a0-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="5c5a0-183">Tenha um endereço IP que esteja dentro de seus IPs Confiáveis configurados</span><span class="sxs-lookup"><span data-stu-id="5c5a0-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="5c5a0-184">Tenha um endereço IP que não esteja dentro de seus IPs Confiáveis configurados</span><span class="sxs-lookup"><span data-stu-id="5c5a0-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="5c5a0-185">A autenticação multifator só será necessária durante uma tentativa de conexão feita de um dispositivo que não esteja dentro dos seus IPs Confiáveis configurados.</span><span class="sxs-lookup"><span data-stu-id="5c5a0-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5c5a0-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c5a0-186">Next steps</span></span>

<span data-ttu-id="5c5a0-187">Se você quiser saber mais sobre o acesso condicional, veja [Acesso condicional do Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c5a0-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

