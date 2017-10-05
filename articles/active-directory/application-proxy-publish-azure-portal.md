---
title: Publicar aplicativos com o Proxy de Aplicativo do Azure AD | Microsoft Docs
description: Publique aplicativos locais na nuvem com o Proxy de Aplicativo do Azure AD no Portal do Azure.
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
ms.openlocfilehash: e00a939f2b20ab8e0a2ddf0ff91e59db440213ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="90f80-103">Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90f80-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="90f80-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="90f80-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="90f80-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="90f80-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="90f80-106">O Proxy de Aplicativo do Active Directory (AD) do Azure o ajuda a dar suporte a funcionários remotos publicando aplicativos locais para serem acessados via Internet.</span><span class="sxs-lookup"><span data-stu-id="90f80-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="90f80-107">É possível publicar esses aplicativos por meio do portal do Azure para fornecer acesso remoto seguro de fora de sua rede.</span><span class="sxs-lookup"><span data-stu-id="90f80-107">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span></span>

<span data-ttu-id="90f80-108">Este artigo explica as etapas para publicar um aplicativo local com o Proxy de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f80-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="90f80-109">Depois de concluir este artigo, os usuários poderão acessar remotamente o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f80-109">After you complete this article, your users will be able to access your app remotely.</span></span> <span data-ttu-id="90f80-110">E você estará pronto para configurar recursos adicionais para o aplicativo como logon único, informações personalizadas e requisitos de segurança.</span><span class="sxs-lookup"><span data-stu-id="90f80-110">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="90f80-111">Se você for iniciante com o Proxy de Aplicativo, aprenda mais sobre este recurso com o artigo [Como fornecer acesso remoto seguro a aplicativos locais](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="90f80-111">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="90f80-112">Publicar um aplicativo local para acesso remoto</span><span class="sxs-lookup"><span data-stu-id="90f80-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="90f80-113">Siga estas etapas para publicar seus aplicativos com Proxy de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f80-113">Follow these steps to publish your apps with Application Proxy.</span></span> <span data-ttu-id="90f80-114">Se você já não tiver baixado e configurado um conector para sua organização, vá para [Introdução ao Proxy de Aplicativo e instale o conector](active-directory-application-proxy-enable.md) primeiro e, em seguida, publique seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f80-114">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="90f80-115">Se você estiver testando pela primeira vez o Proxy de Aplicativo, escolha um aplicativo que esteja configurado para autenticação baseada em senha.</span><span class="sxs-lookup"><span data-stu-id="90f80-115">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="90f80-116">O Proxy de Aplicativo oferece suporte a outros tipos de autenticação, mas os aplicativos baseados em senha são mais fáceis e rápidos de executar.</span><span class="sxs-lookup"><span data-stu-id="90f80-116">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span></span> 

1. <span data-ttu-id="90f80-117">Entre como administrador no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90f80-117">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="90f80-118">Selecione **Azure Active Directory** > **Aplicativos empresariais** > **Novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="90f80-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Adicionar um aplicativo empresarial](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="90f80-120">Selecione **Todos** e, em seguida, selecione **Aplicativo local**.</span><span class="sxs-lookup"><span data-stu-id="90f80-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Adicionar seu próprio aplicativo](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="90f80-122">Forneça as seguintes informações sobre o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="90f80-122">Provide the following information about your application:</span></span>

   - <span data-ttu-id="90f80-123">**Nome**: o nome do aplicativo que será exibido no painel de acesso e no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="90f80-123">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span></span> 

   - <span data-ttu-id="90f80-124">**URL interna**: é a URL para acessar o aplicativo dentro da sua rede privada.</span><span class="sxs-lookup"><span data-stu-id="90f80-124">**Internal URL**: The URL that you use to access the application from inside your private network.</span></span> <span data-ttu-id="90f80-125">Você pode fornecer um caminho específico no servidor back-end para publicar, enquanto o restante do servidor é não publicado.</span><span class="sxs-lookup"><span data-stu-id="90f80-125">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="90f80-126">Assim, você pode publicar sites diferentes no mesmo servidor como diferentes aplicativos, e dar a cada um deles seu próprio nome e suas regras de acesso.</span><span class="sxs-lookup"><span data-stu-id="90f80-126">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="90f80-127">Se você publicar um caminho, verifique se ele inclui todas as imagens, scripts e folhas de estilo necessários para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f80-127">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="90f80-128">Por exemplo, se seu aplicativo está em https://seuaplicativo/app e usa imagens localizadas em https://seuaplicativo/media, você deve publicar https://seuaplicativo/ como o caminho.</span><span class="sxs-lookup"><span data-stu-id="90f80-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span> <span data-ttu-id="90f80-129">Essa URL interna não precisa ser a página de aterrissagem que os usuários veem.</span><span class="sxs-lookup"><span data-stu-id="90f80-129">This internal URL doesn't have to be the landing page your users see.</span></span> <span data-ttu-id="90f80-130">Para obter mais informações, consulte [Definir uma página inicial personalizada para aplicativos publicados](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="90f80-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="90f80-131">**URL externa**: o endereço que seus usuários usam para acessar o aplicativo de fora da sua rede.</span><span class="sxs-lookup"><span data-stu-id="90f80-131">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span> <span data-ttu-id="90f80-132">Se você não quiser usar o domínio padrão de Proxy de Aplicativo, leia sobre [domínios personalizados no Proxy de Aplicativo do Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="90f80-132">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="90f80-133">**Pré-autenticação**: como o Proxy de Aplicativo verifica os usuários antes de lhes dar acesso ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f80-133">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="90f80-134">Azure Active Directory: o Proxy de Aplicativo redireciona os usuários para entrar com o Azure AD, que autentica as permissões para o diretório e o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f80-134">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="90f80-135">É recomendável manter essa opção como padrão, para que você possa tirar proveito dos recursos de segurança do Azure AD como acesso condicional e Autenticação Multifator.</span><span class="sxs-lookup"><span data-stu-id="90f80-135">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="90f80-136">Passagem: os usuários não precisam ser autenticados no Azure Active Directory para acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f80-136">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="90f80-137">Você ainda pode configurar os requisitos de autenticação no back-end.</span><span class="sxs-lookup"><span data-stu-id="90f80-137">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="90f80-138">**Grupo de Conectores**: conectores processam o acesso remoto ao seu aplicativo e o ajudam a organizar conectores e aplicativos por região, rede ou finalidade.</span><span class="sxs-lookup"><span data-stu-id="90f80-138">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="90f80-139">Se você ainda não tiver grupos de conectores criados, seu aplicativo é atribuído a **Padrão**.</span><span class="sxs-lookup"><span data-stu-id="90f80-139">If you don't have any connector groups created yet, your app is assigned to **Default**.</span></span>

   ![Configurar seu aplicativo](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="90f80-141">Se necessário, defina configurações adicionais.</span><span class="sxs-lookup"><span data-stu-id="90f80-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="90f80-142">Para a maioria dos aplicativos, você deve manter essas configurações em seus estados padrão.</span><span class="sxs-lookup"><span data-stu-id="90f80-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="90f80-143">**Tempo limite do aplicativo de back-end**: Defina esse valor como **Longo** somente se seu aplicativo estiver lento para se autenticar e se conectar.</span><span class="sxs-lookup"><span data-stu-id="90f80-143">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span></span> 
   - <span data-ttu-id="90f80-144">**Converter URLs nos cabeçalhos**: Mantenha esse valor como **Sim** a menos que seu aplicativo exija o cabeçalho de host original na solicitação de autenticação.</span><span class="sxs-lookup"><span data-stu-id="90f80-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span></span>
   - <span data-ttu-id="90f80-145">**Converter URLs no corpo do aplicativo**: Mantenha esse valor como **Não** a menos que você tenha inserido no código HTML links para outros aplicativos locais e não use domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="90f80-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="90f80-146">Para saber mais, consulte [Conversão de link com o Proxy de Aplicativo](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="90f80-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Configurar seu aplicativo](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="90f80-148">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="90f80-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="90f80-149">Adicionar um usuário de teste</span><span class="sxs-lookup"><span data-stu-id="90f80-149">Add a test user</span></span> 

<span data-ttu-id="90f80-150">Para testar se o aplicativo foi publicado corretamente, adicione uma conta de usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="90f80-150">To test that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="90f80-151">Verifique se essa conta já tem permissões para acessar o aplicativo dentro da rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="90f80-151">Verify that this account already has permissions to access the app from inside the corporate network.</span></span>

1. <span data-ttu-id="90f80-152">De volta à folha Início Rápido, selecione **Atribuir um usuário para teste**.</span><span class="sxs-lookup"><span data-stu-id="90f80-152">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![Atribuir um usuário para teste](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="90f80-154">Na folha Usuários e grupos, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="90f80-154">On the Users and groups blade, select **Add**.</span></span>

  ![Adicionar um usuário ou grupo](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="90f80-156">Na folha de Adicionar Atribuição, selecione **Usuários e grupos**, em seguida escolha a conta que você deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="90f80-156">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="90f80-157">Selecione **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="90f80-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="90f80-158">Testar seu aplicativo publicado</span><span class="sxs-lookup"><span data-stu-id="90f80-158">Test your published app</span></span>

<span data-ttu-id="90f80-159">No seu navegador, navegue até a URL externa configurada durante a etapa de publicação.</span><span class="sxs-lookup"><span data-stu-id="90f80-159">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="90f80-160">Você deve ver a tela inicial e ser capaz de entrar com a conta de teste que configurou.</span><span class="sxs-lookup"><span data-stu-id="90f80-160">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![Testar seu aplicativo publicado](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="90f80-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90f80-162">Next steps</span></span>
- <span data-ttu-id="90f80-163">[Baixe conectores](active-directory-application-proxy-enable.md) e [crie grupos de conectores](active-directory-application-proxy-connectors-azure-portal.md) para publicar aplicativos em redes e locais separados.</span><span class="sxs-lookup"><span data-stu-id="90f80-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="90f80-164">[Configurar o logon único](application-proxy-sso-azure-portal.md) para seu aplicativo recém-publicado</span><span class="sxs-lookup"><span data-stu-id="90f80-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
