---
title: "autenticação baseada em aaaHeader com PingAccess para Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Publica aplicativos com PingAccess e Proxy de aplicativo toosupport com base no cabeçalho de autenticação."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="dd4dd-103">Autenticação baseada em cabeçalho para logon único com Proxy de Aplicativo e PingAccess</span><span class="sxs-lookup"><span data-stu-id="dd4dd-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="dd4dd-104">Azure Active Directory Application Proxy e PingAccess têm uma parceria junto aos clientes do Active Directory do Azure tooprovide tooeven acesso mais aplicativos.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-104">Azure Active Directory Application Proxy and PingAccess have partnered together tooprovide Azure Active Directory customers with access tooeven more applications.</span></span> <span data-ttu-id="dd4dd-105">PingAccess expande Olá [ofertas de Proxy de aplicativo existentes](active-directory-application-proxy-get-started.md) tooinclude tooapplications de acesso de logon único que usam cabeçalhos para autenticação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-105">PingAccess expands hello [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) tooinclude single sign-on access tooapplications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="dd4dd-106">O que é PingAccess para Azure AD?</span><span class="sxs-lookup"><span data-stu-id="dd4dd-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="dd4dd-107">PingAccess para Active Directory do Azure é uma oferta de PingAccess que permite o acesso aos usuários toogive e único logon tooapplications que usam cabeçalhos para autenticação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you toogive users access and single sign-on tooapplications that use headers for authentication.</span></span> <span data-ttu-id="dd4dd-108">Proxy de aplicativo trata esses aplicativos como qualquer outro, usando o acesso do AD do Azure tooauthenticate e, em seguida, passar o tráfego por meio do serviço de conector hello.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-108">Application Proxy treats these apps like any other, using Azure AD tooauthenticate access and then passing traffic through hello connector service.</span></span> <span data-ttu-id="dd4dd-109">PingAccess se encontra na frente de aplicativos hello e converte o token de acesso de saudação do AD do Azure em um cabeçalho para que o aplicativo hello recebe autenticação Olá no formato de saudação pode ler.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-109">PingAccess sits in front of hello apps and translates hello access token from Azure AD into a header so that hello application receives hello authentication in hello format it can read.</span></span>

<span data-ttu-id="dd4dd-110">Os usuários não irá notar algo diferente quando eles entrarem toouse seus aplicativos corporativos.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-110">Your users won’t notice anything different when they sign in toouse your corporate apps.</span></span> <span data-ttu-id="dd4dd-111">Eles ainda podem trabalhar de qualquer lugar e em qualquer dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="dd4dd-112">Desde que os conectores de Proxy de aplicativo hello direcionam tráfego remoto tooall aplicativos independentemente do tipo de autenticação, eles continuará saldo tooload automaticamente, e também.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-112">Since hello Application Proxy connectors direct remote traffic tooall apps regardless of their authentication type, they’ll continue tooload balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="dd4dd-113">Como posso obter acesso?</span><span class="sxs-lookup"><span data-stu-id="dd4dd-113">How do I get access?</span></span>

<span data-ttu-id="dd4dd-114">Como esse cenário é oferecido por meio de uma parceria entre o Azure Active Directory e o PingAccess, você precisa de licenças para os dois serviços.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="dd4dd-115">No entanto, as assinaturas do Azure Active Directory Premium incluem uma licença básica PingAccess que abrange too20 aplicativos.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up too20 applications.</span></span> <span data-ttu-id="dd4dd-116">Se você precisar de mais de 20 aplicativos baseados em cabeçalho toopublish, você pode adquirir uma licença adicional de PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-116">If you need toopublish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="dd4dd-117">Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="dd4dd-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="dd4dd-118">Publicar seu aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="dd4dd-118">Publish your application in Azure</span></span>

<span data-ttu-id="dd4dd-119">Este artigo destina-se a pessoas que estiver publicando um aplicativo com este cenário para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-119">This article is intended for people who are publishing an app with this scenario for hello first time.</span></span> <span data-ttu-id="dd4dd-120">Ele explica como tooget iniciada com o aplicativo e PingAccess, além de etapas de publicação toohello.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-120">It walks through how tooget started with both Application and PingAccess, in addition toohello publishing steps.</span></span> <span data-ttu-id="dd4dd-121">Se você já tiver configurado os dois serviços, mas desejar uma atualização em Olá etapas de publicação, você pode ignorar a instalação do conector hello e mover muito[adicionar tooAzure seu aplicativo AD com o Proxy de aplicativo](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="dd4dd-121">If you’ve already configured both services but want a refresher on hello publishing steps, you can skip hello connector installation and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="dd4dd-122">Como este cenário é uma parceria entre o Azure AD e PingAccess, algumas das instruções Olá existirem no hello site identidade de Ping.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-122">Since this scenario is a partnership between Azure AD and PingAccess, some of hello instructions exist on hello Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="dd4dd-123">Instalar um conector do Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="dd4dd-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="dd4dd-124">Se você já tem o Proxy de aplicativo habilitado e tenha um conector, você pode ignorar esta seção e mover muito[adicionar tooAzure seu aplicativo AD com o Proxy de aplicativo](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="dd4dd-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="dd4dd-125">conector de Proxy de aplicativo Hello é um servidor Windows aplicativos publicados do serviço que direciona o tráfego de saudação do tooyour seus funcionários remotos.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-125">hello Application Proxy connector is a Windows Server service that directs hello traffic from your remote employees tooyour published apps.</span></span> <span data-ttu-id="dd4dd-126">Para obter mais instruções de instalação, consulte [habilitar Proxy de aplicativo no portal do Azure de saudação](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="dd4dd-126">For more detailed installation instructions, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="dd4dd-127">Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador global.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-127">Sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="dd4dd-128">Selecione **Azure Active Directory** > **Proxy de aplicativo** .</span><span class="sxs-lookup"><span data-stu-id="dd4dd-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="dd4dd-129">Selecione **baixar conector** download do conector de Proxy de aplicativo toostart hello.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-129">Select **Download Connector** toostart hello Application Proxy connector download.</span></span> <span data-ttu-id="dd4dd-130">Siga as instruções de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-130">Follow hello installation instructions.</span></span>

   ![Habilitar Proxy de aplicativo e baixar conector Olá](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="dd4dd-132">Baixando Olá connector automaticamente deve habilitar o Proxy de aplicativo para seu diretório, mas se não é possível selecionar **habilitar Proxy de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-132">Downloading hello connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a><span data-ttu-id="dd4dd-133">Adicionar tooAzure seu aplicativo AD com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="dd4dd-133">Add your app tooAzure AD with Application Proxy</span></span>

<span data-ttu-id="dd4dd-134">Há duas ações que você precisa tootake em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-134">There are two actions you need tootake in hello Azure portal.</span></span> <span data-ttu-id="dd4dd-135">Primeiro, você precisa toopublish seu aplicativo com o Proxy de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-135">First, you need toopublish your application with Application Proxy.</span></span> <span data-ttu-id="dd4dd-136">Em seguida, você precisa toocollect algumas informações sobre o aplicativo hello que você pode usar durante as etapas de PingAccess hello.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-136">Then, you need toocollect some information about hello app that you can use during hello PingAccess steps.</span></span>

<span data-ttu-id="dd4dd-137">Siga estas etapas toopublish seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-137">Follow these steps toopublish your app.</span></span> <span data-ttu-id="dd4dd-138">Para um passo a passo mais detalhado das etapas 1 a 8, veja [Publicar aplicativos usando o Proxy de Aplicativo do Azure AD](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dd4dd-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="dd4dd-139">Se você não fez isso na última seção do hello, entre no toohello [portal do Azure](https://portal.azure.com) como um administrador global.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-139">If you didn't in hello last section, sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="dd4dd-140">Selecione **Azure Active Directory** > **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="dd4dd-141">Selecione **adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-141">Select **Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="dd4dd-142">Selecione **Aplicativo local**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="dd4dd-143">Preencha os campos de saudação necessárias com informações sobre seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-143">Fill out hello required fields with information about your new app.</span></span> <span data-ttu-id="dd4dd-144">Use Olá diretrizes para configurações de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd4dd-144">Use hello following guidance for hello settings:</span></span>
   - <span data-ttu-id="dd4dd-145">**URL interna**: normalmente você fornecer Olá URL que leva você de inscrição do aplicativo toohello na página quando você estiver na rede corporativa hello.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-145">**Internal URL**: Normally you provide hello URL that takes you toohello app’s sign in page when you’re on hello corporate network.</span></span> <span data-ttu-id="dd4dd-146">Para este cenário conector Olá precisa tootreat Olá PingAccess proxy como página inicial de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-146">For this scenario hello connector needs tootreat hello PingAccess proxy as hello front page of hello app.</span></span> <span data-ttu-id="dd4dd-147">Use este formato: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="dd4dd-148">porta de saudação é 3000 por padrão, mas você pode configurá-lo no PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-148">hello port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="dd4dd-149">**Método de Pré-autenticação**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd4dd-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="dd4dd-150">**Converter URL em cabeçalhos**: não</span><span class="sxs-lookup"><span data-stu-id="dd4dd-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="dd4dd-151">Se esse for o primeiro aplicativo, use a porta 3000 toostart e voltar tooupdate essa configuração se você alterar a configuração de PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-151">If this is your first application, use port 3000 toostart and come back tooupdate this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="dd4dd-152">Se esse for o seu aplicativo de segundo ou posterior, isso será necessário toomatch Olá ouvinte que você configurou no PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-152">If this is your second or later app, this will need toomatch hello Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="dd4dd-153">Saiba mais sobre [ouvintes no PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="dd4dd-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="dd4dd-154">Selecione **adicionar** na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-154">Select **Add** at hello bottom of hello blade.</span></span> <span data-ttu-id="dd4dd-155">Seu aplicativo é adicionado e menu de início rápido de saudação é aberto.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-155">Your application is added, and hello quick start menu opens.</span></span>
7. <span data-ttu-id="dd4dd-156">No menu de início rápido do hello, selecione **atribuir um usuário para teste**e adicione pelo menos um usuário toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-156">In hello quick start menu, select **Assign a user for testing**, and add at least one user toohello application.</span></span> <span data-ttu-id="dd4dd-157">Verifique se que essa conta de teste possui acesso toohello local aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-157">Make sure this test account has access toohello on-premises application.</span></span>
8. <span data-ttu-id="dd4dd-158">Selecione **atribuir** toosave atribuição de usuário de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-158">Select **Assign** toosave hello test user assignment.</span></span>
9. <span data-ttu-id="dd4dd-159">Na folha de gerenciamento de aplicativo hello, selecione **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-159">On hello app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="dd4dd-160">Escolha **com base no cabeçalho de logon** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-160">Choose **Header-based sign-on** from hello drop-down menu.</span></span> <span data-ttu-id="dd4dd-161">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="dd4dd-162">Se for a primeira vez usando com base no cabeçalho de logon único, você precisa tooinstall PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-162">If this is your first time using header-based single sign-on, you need tooinstall PingAccess.</span></span> <span data-ttu-id="dd4dd-163">toomake-se de que sua assinatura do Azure é associada automaticamente a instalação do PingAccess, use link Olá toodownload essa página de logon único PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-163">toomake sure your Azure subscription is automatically associated with your PingAccess installation, use hello link on this single sign-on page toodownload PingAccess.</span></span> <span data-ttu-id="dd4dd-164">Você pode abrir o site de download de saudação agora ou voltar toothis página mais tarde.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-164">You can open hello download site now, or come back toothis page later.</span></span> 

   ![Selecione o logon com base no cabeçalho](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="dd4dd-166">Feche a folha de aplicativos de empresa hello ou role menu de Active Directory do Azure do hello maneira toohello tooreturn esquerdo toohello todos os.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-166">Close hello Enterprise applications blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
12. <span data-ttu-id="dd4dd-167">Selecione **Registros do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-167">Select **App registrations**.</span></span>

   ![Selecionar Registros de aplicativo](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="dd4dd-169">Olá selecione aplicativo você acabou de adicionar, em seguida, **URLs de resposta**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-169">Select hello app you just added, then **Reply URLs**.</span></span>

   ![Selecionar URLs de Resposta](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="dd4dd-171">Verifique toosee se URL externa Olá esse aplicativo de tooyour atribuído você na etapa 5 estiver na lista de URLs de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-171">Check toosee if hello external URL that you assigned tooyour app in step 5 is in hello Reply URLs list.</span></span> <span data-ttu-id="dd4dd-172">Se não estiver, adicione-a agora.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="dd4dd-173">Na folha de configurações do aplicativo hello, selecione **as permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-173">On hello app settings blade, select **Required permissions**.</span></span>

  ![Selecionar Permissões necessárias](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="dd4dd-175">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-175">Select **Add**.</span></span> <span data-ttu-id="dd4dd-176">Para Olá API, escolha **Windows Azure Active Directory**, em seguida, **selecione**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-176">For hello API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="dd4dd-177">Para permissões de saudação, escolha **leitura e gravar todos os aplicativos** e **entrar e ler o perfil de usuário**, em seguida, **selecione** e **feito**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-177">For hello permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Selecionar permissões](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a><span data-ttu-id="dd4dd-179">Coletar informações de etapas de PingAccess Olá</span><span class="sxs-lookup"><span data-stu-id="dd4dd-179">Collect information for hello PingAccess steps</span></span>

1. <span data-ttu-id="dd4dd-180">Na folha de configurações de seu aplicativo, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-180">On your app settings blade, select **Properties**.</span></span> 

  ![Selecionar Propriedades](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="dd4dd-182">Salvar Olá **Id do aplicativo** valor.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-182">Save hello **Application Id** value.</span></span> <span data-ttu-id="dd4dd-183">Isso é usado para a ID de cliente hello quando você configura PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-183">This is used for hello client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="dd4dd-184">Na folha de configurações do aplicativo hello, selecione **chaves**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-184">On hello app settings blade, select **Keys**.</span></span>

  ![Selecionar Chaves](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="dd4dd-186">Crie uma chave de inserir uma descrição de chave e escolhendo uma data de expiração no menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-186">Create a key by entering a key description and choosing an expiration date from hello drop-down menu.</span></span>
5. <span data-ttu-id="dd4dd-187">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-187">Select **Save**.</span></span> <span data-ttu-id="dd4dd-188">Um GUID é exibida no hello **valor** campo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-188">A GUID appears in hello **Value** field.</span></span>

  <span data-ttu-id="dd4dd-189">Salvar esse valor agora, pois não será capaz de toosee-lo novamente depois de fechar esta janela.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-189">Save this value now, as you won’t be able toosee it again after you close this window.</span></span>

  ![Criar uma nova chave](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="dd4dd-191">Feche a folha de registros do aplicativo hello ou role menu de Active Directory do Azure do hello maneira toohello tooreturn esquerdo toohello todos os.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-191">Close hello App registrations blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
7. <span data-ttu-id="dd4dd-192">Selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-192">Select **Properties**.</span></span>
8. <span data-ttu-id="dd4dd-193">Salvar Olá **ID de diretório** GUID.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-193">Save hello **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-toosend-custom-fields"></a><span data-ttu-id="dd4dd-194">Opcional - atualização GraphAPI toosend os campos personalizados</span><span class="sxs-lookup"><span data-stu-id="dd4dd-194">Optional - Update GraphAPI toosend custom fields</span></span>

<span data-ttu-id="dd4dd-195">Para obter uma lista de tokens de segurança que o Azure AD envia para autenticação, confira [Referência de token do Azure AD](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="dd4dd-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="dd4dd-196">Se você precisar de uma declaração personalizada que envia outros tokens, use o campo de aplicativo GraphAPI tooset Olá *acceptMappedClaims* muito**True**.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-196">If you need a custom claim that sends other tokens, use GraphAPI tooset hello app field *acceptMappedClaims* too**True**.</span></span> <span data-ttu-id="dd4dd-197">Você pode usar o Azure AD Graph Explorer ou MS Graph toomake essa configuração.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-197">You can use either Azure AD Graph Explorer or MS Graph toomake this configuration.</span></span> 

<span data-ttu-id="dd4dd-198">Este exemplo usa o Explorador do Graph:</span><span class="sxs-lookup"><span data-stu-id="dd4dd-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="dd4dd-199">Baixar o PingAccess e configurar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="dd4dd-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="dd4dd-200">Agora que você concluiu todas as etapas de instalação do Active Directory do Azure hello, você pode mover em tooconfiguring PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-200">Now that you've completed all hello Azure Active Directory setup steps, you can move on tooconfiguring PingAccess.</span></span> 

<span data-ttu-id="dd4dd-201">Olá etapas detalhadas para Olá PingAccess parte deste cenário continuam Olá documentação de identidade de Ping, [PingAccess configurar o AD do Azure](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="dd4dd-201">hello detailed steps for hello PingAccess part of this scenario continue in hello Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="dd4dd-202">Essas etapas orientam você durante o processo de saudação de obter uma conta de PingAccess se você ainda não tiver um, a instalação Olá PingAccess Server e a criação de uma conexão de provedor do Azure AD OIDC com hello ID de diretório que você copiou da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-202">Those steps walk you through hello process of getting a PingAccess account if you don't already have one, installing hello PingAccess Server, and creating an Azure AD OIDC Provider connection with hello Directory ID that you copied from hello Azure portal.</span></span> <span data-ttu-id="dd4dd-203">Em seguida, use Olá valores de ID do aplicativo e a chave toocreate uma sessão Web PingAccess.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-203">Then, you use hello Application ID and Key values toocreate a Web Session on PingAccess.</span></span> <span data-ttu-id="dd4dd-204">Em seguida, configure o mapeamento de identidade e crie um host virtual, site e aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="dd4dd-205">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="dd4dd-205">Test your app</span></span>

<span data-ttu-id="dd4dd-206">Depois de concluir todas essas etapas, seu aplicativo estará pronto para execução.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="dd4dd-207">tootest-lo, abra um navegador e navegue toohello URL externa que você criou quando você publicou o aplicativo hello no Azure.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-207">tootest it, open a browser and navigate toohello external URL that you created when you published hello app in Azure.</span></span> <span data-ttu-id="dd4dd-208">Entre com a conta de teste de saudação que você toohello atribuído o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd4dd-208">Sign in with hello test account that you assigned toohello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd4dd-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd4dd-209">Next steps</span></span>

- [<span data-ttu-id="dd4dd-210">Configurar o PingAccess para Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4dd-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="dd4dd-211">Como o Proxy de Aplicativo do Azure AD fornece logon único?</span><span class="sxs-lookup"><span data-stu-id="dd4dd-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="dd4dd-212">Solucionar problemas de Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="dd4dd-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
