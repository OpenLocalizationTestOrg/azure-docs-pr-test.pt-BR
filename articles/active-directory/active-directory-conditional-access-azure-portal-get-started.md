---
title: aaaGet iniciado com acesso condicional no Active Directory do Azure | Microsoft Docs
description: "Teste o acesso condicional usando uma condição de local."
services: active-directory
keywords: "tooapps de acesso condicional, o acesso condicional com o AD do Azure, proteger o acesso toocompany recursos, políticas de acesso condicional"
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
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="35ed2-104">Introdução ao acesso condicional no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35ed2-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="35ed2-105">Acesso condicional é um recurso do Active Directory do Azure que permite que você toodefine condições sob as quais os usuários autorizados podem acessar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="35ed2-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="35ed2-106">Este tópico fornece instruções para testar um acesso condicional com base em uma condição de local em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="35ed2-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="35ed2-107">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="35ed2-107">Scenario description</span></span>

<span data-ttu-id="35ed2-108">Um requisito comum em muitas organizações é tooonly exigir autenticação multifator para acesso tooapps que não é executada da intranet corporativa hello.</span><span class="sxs-lookup"><span data-stu-id="35ed2-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="35ed2-109">Com o Azure Active Directory, você pode facilmente atingir essa meta, configurando uma política de acesso condicional com base no local.</span><span class="sxs-lookup"><span data-stu-id="35ed2-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="35ed2-110">Este tópico fornece instruções detalhadas sobre como configurar uma política relacionada.</span><span class="sxs-lookup"><span data-stu-id="35ed2-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="35ed2-111">Olá aproveita a política [IPs confiáveis](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish entre tentativas de acesso de saudação corporativa da intranet e todos os outros locais.</span><span class="sxs-lookup"><span data-stu-id="35ed2-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="35ed2-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="35ed2-112">Prerequisites</span></span>

<span data-ttu-id="35ed2-113">Olá cenário descrito neste tópico pressupõe que você esteja familiarizado com os conceitos de saudação descritos em [acesso condicional do Active Directory do Azure](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35ed2-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="35ed2-114">tootest neste cenário, você precisa:</span><span class="sxs-lookup"><span data-stu-id="35ed2-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="35ed2-115">Criar um usuário de teste</span><span class="sxs-lookup"><span data-stu-id="35ed2-115">Create a test user</span></span> 

- <span data-ttu-id="35ed2-116">Atribuir um usuário de teste do Azure AD Premium licença toohello</span><span class="sxs-lookup"><span data-stu-id="35ed2-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="35ed2-117">Configurar um aplicativo gerenciado e atribuir seu tooit de usuário de teste</span><span class="sxs-lookup"><span data-stu-id="35ed2-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="35ed2-118">Configurar IPs confiáveis</span><span class="sxs-lookup"><span data-stu-id="35ed2-118">Configure trusted IPs</span></span>

<span data-ttu-id="35ed2-119">Se você precisar de mais detalhes sobre IPs confiáveis, veja [IPs confiáveis](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="35ed2-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="35ed2-120">Etapas de configuração de política</span><span class="sxs-lookup"><span data-stu-id="35ed2-120">Policy configuration steps</span></span>

<span data-ttu-id="35ed2-121">**tooconfigure política de acesso condicional, execute:**</span><span class="sxs-lookup"><span data-stu-id="35ed2-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="35ed2-122">No hello portal do Azure, na barra de navegação esquerda hello, clique em **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="35ed2-124">Em Olá **Active Directory do Azure** folha em Olá **gerenciar** seção, clique em **acesso condicional**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="35ed2-126">Em Olá **acesso condicional** folha, Olá tooopen **novo** folha, na barra de ferramentas Olá superior hello, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="35ed2-128">Em Olá **novo** folha em Olá **nome** caixa de texto, digite um nome para a política.</span><span class="sxs-lookup"><span data-stu-id="35ed2-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="35ed2-130">Em Olá **atribuição** seção, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="35ed2-132">Em Olá **usuários e grupos** folha, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35ed2-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="35ed2-134">a.</span><span class="sxs-lookup"><span data-stu-id="35ed2-134">a.</span></span> <span data-ttu-id="35ed2-135">Clique em **Selecionar usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="35ed2-136">b.</span><span class="sxs-lookup"><span data-stu-id="35ed2-136">b.</span></span> <span data-ttu-id="35ed2-137">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-137">Click **Select**.</span></span>

    <span data-ttu-id="35ed2-138">c.</span><span class="sxs-lookup"><span data-stu-id="35ed2-138">c.</span></span> <span data-ttu-id="35ed2-139">Em Olá **selecione** folha, selecione seu usuário de teste e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="35ed2-140">d.</span><span class="sxs-lookup"><span data-stu-id="35ed2-140">d.</span></span> <span data-ttu-id="35ed2-141">Em Olá **usuários e grupos** folha, clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="35ed2-142">Em Olá **novo** folha, Olá tooopen **aplicativos de nuvem** folha em Olá **atribuição** seção, clique em **aplicativos de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="35ed2-144">Em Olá **aplicativos de nuvem** folha, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35ed2-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="35ed2-146">a.</span><span class="sxs-lookup"><span data-stu-id="35ed2-146">a.</span></span> <span data-ttu-id="35ed2-147">Clique em **Selecionar aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-147">Click **Select apps**.</span></span>

    <span data-ttu-id="35ed2-148">b.</span><span class="sxs-lookup"><span data-stu-id="35ed2-148">b.</span></span> <span data-ttu-id="35ed2-149">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-149">Click **Select**.</span></span>

    <span data-ttu-id="35ed2-150">c.</span><span class="sxs-lookup"><span data-stu-id="35ed2-150">c.</span></span> <span data-ttu-id="35ed2-151">Em Olá **selecione** folha, selecione o aplicativo de nuvem e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="35ed2-152">d.</span><span class="sxs-lookup"><span data-stu-id="35ed2-152">d.</span></span> <span data-ttu-id="35ed2-153">Em Olá **aplicativos de nuvem** folha, clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="35ed2-154">Em Olá **novo** folha, Olá tooopen **condições** folha em Olá **atribuição** seção, clique em **condições**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="35ed2-156">Em Olá **condições** folha, Olá tooopen **locais** folha, clique em **locais**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="35ed2-158">Em Olá **locais** folha, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35ed2-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="35ed2-160">a.</span><span class="sxs-lookup"><span data-stu-id="35ed2-160">a.</span></span> <span data-ttu-id="35ed2-161">Em **Configurar**, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="35ed2-162">b.</span><span class="sxs-lookup"><span data-stu-id="35ed2-162">b.</span></span> <span data-ttu-id="35ed2-163">Em **Incluir**, clique em **Todos os locais**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="35ed2-164">c.</span><span class="sxs-lookup"><span data-stu-id="35ed2-164">c.</span></span> <span data-ttu-id="35ed2-165">Clique em **Excluir** e clique em **Todos os IPs confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="35ed2-167">d.</span><span class="sxs-lookup"><span data-stu-id="35ed2-167">d.</span></span> <span data-ttu-id="35ed2-168">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-168">Click **Done**.</span></span>

12. <span data-ttu-id="35ed2-169">Em Olá **condições** folha, clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="35ed2-170">Em Olá **novo** folha, Olá tooopen **Grant** folha em Olá **controles** seção, clique em **Grant**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="35ed2-172">Em Olá **Grant** folha, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35ed2-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="35ed2-174">a.</span><span class="sxs-lookup"><span data-stu-id="35ed2-174">a.</span></span> <span data-ttu-id="35ed2-175">Selecione **Exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="35ed2-176">b.</span><span class="sxs-lookup"><span data-stu-id="35ed2-176">b.</span></span> <span data-ttu-id="35ed2-177">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-177">Click **Select**.</span></span>

15. <span data-ttu-id="35ed2-178">Em Olá **novo** folha, em **habilitar política**, clique em **em**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Acesso condicional](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="35ed2-180">Em Olá **novo** folha, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="35ed2-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="35ed2-181">Política de teste Olá</span><span class="sxs-lookup"><span data-stu-id="35ed2-181">Testing hello policy</span></span>

<span data-ttu-id="35ed2-182">tootest sua política, você deve acessar o aplicativo de um dispositivo que:</span><span class="sxs-lookup"><span data-stu-id="35ed2-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="35ed2-183">Tenha um endereço IP que esteja dentro de seus IPs Confiáveis configurados</span><span class="sxs-lookup"><span data-stu-id="35ed2-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="35ed2-184">Tenha um endereço IP que não esteja dentro de seus IPs Confiáveis configurados</span><span class="sxs-lookup"><span data-stu-id="35ed2-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="35ed2-185">A autenticação multifator só será necessária durante uma tentativa de conexão feita de um dispositivo que não esteja dentro dos seus IPs Confiáveis configurados.</span><span class="sxs-lookup"><span data-stu-id="35ed2-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="35ed2-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35ed2-186">Next steps</span></span>

<span data-ttu-id="35ed2-187">Se você quiser toolearn mais sobre o acesso condicional, consulte [acesso condicional do Active Directory do Azure](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35ed2-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

