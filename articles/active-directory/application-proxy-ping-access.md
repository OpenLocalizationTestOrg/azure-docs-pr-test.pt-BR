---
title: "Autenticação baseada em cabeçalho com o PingAccess para Proxy de Aplicativo do Azure AD | Microsoft Docs"
description: "Publique aplicativos com o PingAccess e o Proxy de Aplicativo a fim de oferecer suporte à autenticação baseada em cabeçalho."
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
ms.openlocfilehash: 58034ab8830cf655199875b448948ea14dc04a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="64fb7-103">Autenticação baseada em cabeçalho para logon único com Proxy de Aplicativo e PingAccess</span><span class="sxs-lookup"><span data-stu-id="64fb7-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="64fb7-104">O Proxy de Aplicativo do Azure Active Directory e o PingAccess fizeram uma parceria para fornecer aos clientes do Azure Active Directory acesso a ainda mais aplicativos.</span><span class="sxs-lookup"><span data-stu-id="64fb7-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="64fb7-105">O PingAccess expande as [ofertas existentes do Proxy de Aplicativo](active-directory-application-proxy-get-started.md) para incluir acesso de logon único a aplicativos que usam cabeçalhos para autenticação.</span><span class="sxs-lookup"><span data-stu-id="64fb7-105">PingAccess expands the [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="64fb7-106">O que é PingAccess para Azure AD?</span><span class="sxs-lookup"><span data-stu-id="64fb7-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="64fb7-107">PingAccess para Azure Active Directory é uma oferta de PingAccess que permite que você conceda acesso de usuários e logon único para aplicativos que usam cabeçalhos de autenticação.</span><span class="sxs-lookup"><span data-stu-id="64fb7-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="64fb7-108">O Proxy de Aplicativo trata esses aplicativos como qualquer outro, usando o Azure AD para autenticar o acesso e, depois, passando o tráfego por meio do serviço de conector.</span><span class="sxs-lookup"><span data-stu-id="64fb7-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="64fb7-109">O PingAccess fica na frente dos aplicativos e converte o token de acesso do Azure AD em um cabeçalho, para que o aplicativo receba a autenticação em um formato que consiga ler.</span><span class="sxs-lookup"><span data-stu-id="64fb7-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="64fb7-110">Os usuários não perceberão algo diferente quando entrarem para usar seus aplicativos corporativos.</span><span class="sxs-lookup"><span data-stu-id="64fb7-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="64fb7-111">Eles ainda podem trabalhar de qualquer lugar e em qualquer dispositivo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="64fb7-112">Como os conectores do Proxy de Aplicativo direcionam o tráfego remoto a todos os aplicativos, independentemente do tipo de autenticação, eles também continuarão a balancear a carga automaticamente.</span><span class="sxs-lookup"><span data-stu-id="64fb7-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="64fb7-113">Como posso obter acesso?</span><span class="sxs-lookup"><span data-stu-id="64fb7-113">How do I get access?</span></span>

<span data-ttu-id="64fb7-114">Como esse cenário é oferecido por meio de uma parceria entre o Azure Active Directory e o PingAccess, você precisa de licenças para os dois serviços.</span><span class="sxs-lookup"><span data-stu-id="64fb7-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="64fb7-115">No entanto, as assinaturas do Azure Active Directory Premium incluem uma licença básica PingAccess que abrange até 20 aplicativos.</span><span class="sxs-lookup"><span data-stu-id="64fb7-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="64fb7-116">Se você precisar publicar mais de 20 aplicativos com base em cabeçalho, poderá adquirir uma licença adicional do PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="64fb7-117">Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="64fb7-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="64fb7-118">Publicar seu aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="64fb7-118">Publish your application in Azure</span></span>

<span data-ttu-id="64fb7-119">Este artigo destina-se a pessoas que estão publicando um aplicativo com esse cenário pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="64fb7-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="64fb7-120">Ele explica como começar com o Aplicativo e o PingAccess, além das etapas de publicação.</span><span class="sxs-lookup"><span data-stu-id="64fb7-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="64fb7-121">Se você já tiver configurado os dois serviços, mas desejar uma atualização sobre as etapas de publicação, poderá ignorar a instalação do conector e ir para [Adicionar seu aplicativo ao Azure AD com o Proxy de Aplicativo](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="64fb7-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="64fb7-122">Como esse cenário é uma parceria entre o Azure AD e o PingAccess, algumas das instruções estão no site do Ping Identity.</span><span class="sxs-lookup"><span data-stu-id="64fb7-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="64fb7-123">Instalar um conector do Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="64fb7-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="64fb7-124">Se você já tiver o Proxy de Aplicativo habilitado, além de um conector instalado, poderá ignorar essa seção e ir para [Adicionar seu aplicativo ao Azure AD com o Proxy de Aplicativo](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="64fb7-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="64fb7-125">O conector do Proxy de Aplicativo é um serviço do Windows Server que direciona o tráfego de seus funcionários remotos para seus aplicativos publicados.</span><span class="sxs-lookup"><span data-stu-id="64fb7-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="64fb7-126">Para obter informações mais detalhadas, confira [Habilitar o Proxy de Aplicativo no Portal do Azure](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="64fb7-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="64fb7-127">Entre no [Portal do Azure](https://portal.azure.com) como administrador global.</span><span class="sxs-lookup"><span data-stu-id="64fb7-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="64fb7-128">Selecione **Azure Active Directory** > **Proxy de aplicativo** .</span><span class="sxs-lookup"><span data-stu-id="64fb7-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="64fb7-129">Selecione **Baixar Conector** para iniciar o download do conector do Proxy de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="64fb7-130">Siga as instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="64fb7-130">Follow the installation instructions.</span></span>

   ![Habilitar o Proxy de Aplicativo e baixar o conector](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="64fb7-132">O download do conector deve habilitar automaticamente o Proxy de Aplicativo para seu diretório, mas se isso não acontecer, selecione **Habilitar Proxy de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="64fb7-133">Adicionar o aplicativo ao Azure AD com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="64fb7-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="64fb7-134">Há duas ações necessárias no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64fb7-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="64fb7-135">Primeiro, você precisa publicar seu aplicativo com o Proxy de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="64fb7-136">Depois, colete algumas informações sobre o aplicativo a ser usado durante as etapas do PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="64fb7-137">Siga estas etapas para publicar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="64fb7-138">Para um passo a passo mais detalhado das etapas 1 a 8, veja [Publicar aplicativos usando o Proxy de Aplicativo do Azure AD](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="64fb7-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="64fb7-139">Se você não fez isso na última seção, entre no [Portal do Azure](https://portal.azure.com) como um administrador global.</span><span class="sxs-lookup"><span data-stu-id="64fb7-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="64fb7-140">Selecione **Azure Active Directory** > **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="64fb7-141">Selecione **Adicionar** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="64fb7-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="64fb7-142">Selecione **Aplicativo local**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="64fb7-143">Preencha os campos obrigatórios com informações sobre seu novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="64fb7-144">Use as diretrizes a seguir para as configurações:</span><span class="sxs-lookup"><span data-stu-id="64fb7-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="64fb7-145">**URL interna**: normalmente, você fornece a URL que levará você até a página de entrada do aplicativo quando você estiver na rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="64fb7-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="64fb7-146">Para esse cenário, o conector precisa tratar o proxy do PingAccess como a página inicial do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="64fb7-147">Use este formato: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="64fb7-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="64fb7-148">A porta é a 3000 por padrão, mas você pode configurá-la no PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="64fb7-149">**Método de Pré-autenticação**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64fb7-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="64fb7-150">**Converter URL em cabeçalhos**: não</span><span class="sxs-lookup"><span data-stu-id="64fb7-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="64fb7-151">Se este for seu primeiro aplicativo, use a porta 3000 para iniciar e retorne para atualizar essa configuração se alterar a configuração de PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-151">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="64fb7-152">Se esse for o seu segundo aplicativo ou posterior, isso será necessário para combinar o Ouvinte configurado no PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-152">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="64fb7-153">Saiba mais sobre [ouvintes no PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="64fb7-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="64fb7-154">Selecione **Adicionar** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="64fb7-154">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="64fb7-155">Seu aplicativo é adicionado e abre o menu de início rápido.</span><span class="sxs-lookup"><span data-stu-id="64fb7-155">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="64fb7-156">No menu de início rápido, selecione **Atribuir um usuário para teste** e adicione pelo menos um usuário para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-156">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="64fb7-157">Verifique se essa conta de teste tem acesso ao aplicativo local.</span><span class="sxs-lookup"><span data-stu-id="64fb7-157">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="64fb7-158">Selecione **Atribuir** para salvar a atribuição do usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="64fb7-158">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="64fb7-159">Na folha de gerenciamento do aplicativo, selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-159">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="64fb7-160">Escolha **Logon baseado em cabeçalho** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="64fb7-160">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="64fb7-161">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="64fb7-162">Se esta for a primeira vez que você usa o logon único com base em cabeçalhos, será necessário instalar o PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-162">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="64fb7-163">Para certificar-se de que sua assinatura do Azure seja automaticamente associada à sua instalação do PingAccess, use o link nesta página de logon único para baixar o PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-163">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="64fb7-164">Você pode abrir o site de download agora ou voltar a esta página mais tarde.</span><span class="sxs-lookup"><span data-stu-id="64fb7-164">You can open the download site now, or come back to this page later.</span></span> 

   ![Selecione o logon com base no cabeçalho](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="64fb7-166">Feche a folha Aplicativos empresariais ou role a tela totalmente para a esquerda para retornar ao menu do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64fb7-166">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="64fb7-167">Selecione **Registros do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-167">Select **App registrations**.</span></span>

   ![Selecionar Registros de aplicativo](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="64fb7-169">Selecione o aplicativo que você acabou de adicionar e, depois, **URLs de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-169">Select the app you just added, then **Reply URLs**.</span></span>

   ![Selecionar URLs de Resposta](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="64fb7-171">Verifique se a URL externa que você atribuiu ao seu aplicativo na etapa 5 está na lista de URLs de Resposta.</span><span class="sxs-lookup"><span data-stu-id="64fb7-171">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="64fb7-172">Se não estiver, adicione-a agora.</span><span class="sxs-lookup"><span data-stu-id="64fb7-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="64fb7-173">Na folha de configurações do aplicativo, selecione **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-173">On the app settings blade, select **Required permissions**.</span></span>

  ![Selecionar Permissões necessárias](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="64fb7-175">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-175">Select **Add**.</span></span> <span data-ttu-id="64fb7-176">Para a API, escolha **Windows Azure Active Directory**, depois, **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-176">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="64fb7-177">Para as permissões, escolha **Leitura e gravação em todos os aplicativos** e **Entrar e ler o perfil do usuário**, depois **Selecionar** e **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-177">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Selecionar permissões](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="64fb7-179">Coletar informações sobre as etapas do PingAccess</span><span class="sxs-lookup"><span data-stu-id="64fb7-179">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="64fb7-180">Na folha de configurações de seu aplicativo, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-180">On your app settings blade, select **Properties**.</span></span> 

  ![Selecionar Propriedades](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="64fb7-182">Salve o valor **ID do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-182">Save the **Application Id** value.</span></span> <span data-ttu-id="64fb7-183">Isso é usado para a ID do cliente quando você configura o PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-183">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="64fb7-184">Na folha de configurações, selecione **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-184">On the app settings blade, select **Keys**.</span></span>

  ![Selecionar Chaves](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="64fb7-186">Crie uma chave inserindo uma descrição de chave e escolhendo uma data de validade no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="64fb7-186">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="64fb7-187">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-187">Select **Save**.</span></span> <span data-ttu-id="64fb7-188">Um GUID será exibido no campo **Valor**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-188">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="64fb7-189">Salve esse valor agora, pois você não poderá vê-lo novamente depois de fechar esta janela.</span><span class="sxs-lookup"><span data-stu-id="64fb7-189">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![Criar uma nova chave](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="64fb7-191">Feche a folha Registros de aplicativo empresariais ou role a tela totalmente para a esquerda para retornar ao menu do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64fb7-191">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="64fb7-192">Selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-192">Select **Properties**.</span></span>
8. <span data-ttu-id="64fb7-193">Salve o GUID em **ID de Diretório**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-193">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="64fb7-194">Opcional - Atualizar a API do Graph para enviar campos personalizados</span><span class="sxs-lookup"><span data-stu-id="64fb7-194">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="64fb7-195">Para obter uma lista de tokens de segurança que o Azure AD envia para autenticação, confira [Referência de token do Azure AD](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="64fb7-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="64fb7-196">Se precisar de uma declaração personalizada que envie outros tokens, use a API do Graph para definir o campo de aplicativo *acceptMappedClaims* como **True**.</span><span class="sxs-lookup"><span data-stu-id="64fb7-196">If you need a custom claim that sends other tokens, use GraphAPI to set the app field *acceptMappedClaims* to **True**.</span></span> <span data-ttu-id="64fb7-197">Você pode usar o Explorador do Graph do Azure AD ou o MS Graph para efetuar essa configuração.</span><span class="sxs-lookup"><span data-stu-id="64fb7-197">You can use either Azure AD Graph Explorer or MS Graph to make this configuration.</span></span> 

<span data-ttu-id="64fb7-198">Este exemplo usa o Explorador do Graph:</span><span class="sxs-lookup"><span data-stu-id="64fb7-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="64fb7-199">Baixar o PingAccess e configurar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="64fb7-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="64fb7-200">Agora que você concluiu todas as etapas de instalação do Azure Active Directory, será possível prosseguir para a configuração do PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-200">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="64fb7-201">As etapas detalhadas para a parte do PingAccess deste cenário continuam na documentação de Identidade de Ping, [Configurar o PingAccess para o Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="64fb7-201">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="64fb7-202">Essas etapas orientarão você durante o processo de obtenção de uma conta do PingAccess, se você ainda não tiver uma, instalação do servidor do PingAccess e criação de uma conexão do Provedor do Azure AD OIDC com a ID de Diretório que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64fb7-202">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="64fb7-203">Depois, use os valores de ID do Aplicativo e Chave para criar uma Sessão da Web no PingAccess.</span><span class="sxs-lookup"><span data-stu-id="64fb7-203">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="64fb7-204">Em seguida, configure o mapeamento de identidade e crie um host virtual, site e aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="64fb7-205">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="64fb7-205">Test your app</span></span>

<span data-ttu-id="64fb7-206">Depois de concluir todas essas etapas, seu aplicativo estará pronto para execução.</span><span class="sxs-lookup"><span data-stu-id="64fb7-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="64fb7-207">Para testá-lo, abra um navegador e navegue até a URL externa que você criou quando publicou o aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="64fb7-207">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="64fb7-208">Entre com a conta de teste que você atribuiu ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64fb7-208">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64fb7-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="64fb7-209">Next steps</span></span>

- [<span data-ttu-id="64fb7-210">Configurar o PingAccess para Azure AD</span><span class="sxs-lookup"><span data-stu-id="64fb7-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="64fb7-211">Como o Proxy de Aplicativo do Azure AD fornece logon único?</span><span class="sxs-lookup"><span data-stu-id="64fb7-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="64fb7-212">Solucionar problemas de Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="64fb7-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
