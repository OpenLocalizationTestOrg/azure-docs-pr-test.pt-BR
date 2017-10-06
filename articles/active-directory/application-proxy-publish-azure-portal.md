---
title: aaaPublish aplicativos com Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Publica a nuvem de toohello de aplicativos local com o Proxy de aplicativo do Azure AD em Olá portal do Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="ccc2f-103">Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ccc2f-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ccc2f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ccc2f-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="ccc2f-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="ccc2f-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="ccc2f-106">Proxy de aplicativo do Azure AD (Active Directory) ajuda você a dar suporte a funcionários remotos publicando local aplicativos toobe acessado por meio de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="ccc2f-107">Você pode publicar esses aplicativos por meio de saudação tooprovide portal do Azure acesso remoto seguro de fora da sua rede.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="ccc2f-108">Este artigo orienta Olá etapas toopublish um aplicativo local com o Proxy de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="ccc2f-109">Depois de concluir este artigo, os usuários serão ser capaz de tooaccess seu aplicativo remotamente.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="ccc2f-110">E você estará pronto tooconfigure recursos adicionais para o aplicativo hello como um único logon informações personalizadas e os requisitos de segurança.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="ccc2f-111">Se você estiver tooApplication novo Proxy, saiba mais sobre esse recurso com o artigo Olá [como tooprovide proteger o acesso remoto aplicativos locais tooon](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ccc2f-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="ccc2f-112">Publicar um aplicativo local para acesso remoto</span><span class="sxs-lookup"><span data-stu-id="ccc2f-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="ccc2f-113">Siga estas etapas toopublish seus aplicativos com Proxy de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="ccc2f-114">Se você já não tiver baixado e configurado um conector para sua organização, vá muito[Introdução ao Proxy de aplicativo e instalar o conector Olá](active-directory-application-proxy-enable.md) primeiro e, em seguida, publicar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="ccc2f-115">Se você estiver testando o Proxy de aplicativo para Olá primeira vez, escolha um aplicativo que está configurado para autenticação baseada em senha.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="ccc2f-116">Proxy de aplicativo oferece suporte a outros tipos de autenticação, mas aplicativos baseados em senha são tooget mais fácil de saudação para cima e em execução rapidamente.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="ccc2f-117">Entrar como um administrador no hello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ccc2f-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ccc2f-118">Selecione **Azure Active Directory** > **Aplicativos empresariais** > **Novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Adicionar um aplicativo empresarial](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="ccc2f-120">Selecione **Todos** e, em seguida, selecione **Aplicativo local**.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Adicionar seu próprio aplicativo](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="ccc2f-122">Fornece Olá informações sobre o aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ccc2f-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="ccc2f-123">**Nome**: nome de saudação do aplicativo de saudação que aparecerá no painel de acesso hello e em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="ccc2f-124">**URL interna**: Olá URL que você usar o aplicativo hello tooaccess na sua rede privada.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="ccc2f-125">Você pode fornecer um caminho específico em Olá toopublish de servidor de back-end, enquanto o restante de saudação do servidor de saudação foi publicada.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="ccc2f-126">Dessa forma, você pode publicar sites diferentes na Olá mesmo servidor que diferentes aplicativos e dê a cada um deles suas próprias regras de acesso e do nome.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="ccc2f-127">Se você publicar um caminho, certifique-se de que ele inclui todas as imagens necessárias hello, scripts e folhas de estilo para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="ccc2f-128">Por exemplo, se seu aplicativo estiver em https://yourapp/app e usa imagens localizadas em https://yourapp/media, você deve publicar https://yourapp/ como caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="ccc2f-129">Essa URL interna não tem página de aterrissagem Olá toobe que os usuários vejam.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="ccc2f-130">Para obter mais informações, consulte [Definir uma página inicial personalizada para aplicativos publicados](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="ccc2f-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="ccc2f-131">**URL externa**: Olá endereço que os usuários irão tooin ordem tooaccess Olá aplicativo de fora da sua rede.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="ccc2f-132">Se você não quiser o domínio de Proxy de aplicativo toouse saudação padrão, leia sobre [domínios personalizados no Proxy de aplicativo do Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="ccc2f-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="ccc2f-133">**Pré-autenticação**: como Proxy de aplicativo verifica os usuários antes de fornecê-los acesso tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="ccc2f-134">Active Directory do Azure: O Proxy de aplicativo redireciona toosign de usuários com o AD do Azure, que autentica suas permissões para o diretório de saudação e o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="ccc2f-135">É recomendável manter essa opção como padrão hello, você pode tirar proveito dos recursos de segurança do AD do Azure como acesso condicional e autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="ccc2f-136">Passagem: Os usuários não têm tooauthenticate no aplicativo do Active Directory do Azure tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="ccc2f-137">Você ainda pode configurar os requisitos de autenticação em Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="ccc2f-138">**Grupo**: conectores processo Olá acesso remoto tooyour aplicativo e ajudam a organizar aplicativos por região, rede ou finalidade e conectores de grupos de conector.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="ccc2f-139">Se você não tiver grupos de conector ainda criados, seu aplicativo recebe muito**padrão**.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![Configurar seu aplicativo](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="ccc2f-141">Se necessário, defina configurações adicionais.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="ccc2f-142">Para a maioria dos aplicativos, você deve manter essas configurações em seus estados padrão.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="ccc2f-143">**Tempo limite do aplicativo de back-end**: Defina esse valor muito**longo** somente se seu aplicativo estiver lenta tooauthenticate e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="ccc2f-144">**Traduzir URLs nos cabeçalhos**: manter esse valor como **Sim** a menos que seu aplicativo exija o cabeçalho de host original Olá na solicitação de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="ccc2f-145">**Traduzir URLs no corpo do aplicativo**: manter esse valor como **não** , a menos que você tiver inserido no código HTML links tooother local aplicativos e não usar domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="ccc2f-146">Para saber mais, consulte [Conversão de link com o Proxy de Aplicativo](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="ccc2f-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Configurar seu aplicativo](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="ccc2f-148">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="ccc2f-149">Adicionar um usuário de teste</span><span class="sxs-lookup"><span data-stu-id="ccc2f-149">Add a test user</span></span> 

<span data-ttu-id="ccc2f-150">tootest que seu aplicativo foi publicado corretamente, adicione uma conta de usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="ccc2f-151">Verifique se essa conta já tem permissões tooaccess Olá aplicativo de dentro da rede corporativa hello.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="ccc2f-152">Volta na folha de início rápido do hello, selecione **atribuir um usuário para teste**.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![Atribuir um usuário para teste](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="ccc2f-154">Usuários de saudação e folha de grupos, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-154">On hello Users and groups blade, select **Add**.</span></span>

  ![Adicionar um usuário ou grupo](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="ccc2f-156">Na folha de atribuição de adicionar hello, selecione **usuários e grupos** , em seguida, escolher conta Olá deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="ccc2f-157">Selecione **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="ccc2f-158">Testar seu aplicativo publicado</span><span class="sxs-lookup"><span data-stu-id="ccc2f-158">Test your published app</span></span>

<span data-ttu-id="ccc2f-159">No seu navegador, navegue toohello URL externa que você configurou durante a saudação publicar etapa.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="ccc2f-160">Você deve ver a tela de início do hello e ser capaz de toosign com conta de teste Olá você configurar.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![Testar seu aplicativo publicado](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="ccc2f-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ccc2f-162">Next steps</span></span>
- <span data-ttu-id="ccc2f-163">[Baixar conectores](active-directory-application-proxy-enable.md) e [criar grupos de conector](active-directory-application-proxy-connectors-azure-portal.md) toopublish aplicativos em redes separadas e locais.</span><span class="sxs-lookup"><span data-stu-id="ccc2f-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="ccc2f-164">[Configurar o logon único](application-proxy-sso-azure-portal.md) para seu aplicativo recém-publicado</span><span class="sxs-lookup"><span data-stu-id="ccc2f-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
