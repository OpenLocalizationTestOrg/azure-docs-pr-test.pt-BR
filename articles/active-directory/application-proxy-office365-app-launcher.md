---
title: "aaaSet uma página inicial personalizada para aplicativos publicados usando o Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Noções básicas de saudação abrange sobre conectores de Proxy de aplicativo do Azure AD"
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
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="71fae-103">Definir uma home page personalizada para aplicativos publicados usando o Proxy de Aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="71fae-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="71fae-104">Este artigo aborda como tooconfigure aplicativos toodirect usuários tooa página inicial personalizada.</span><span class="sxs-lookup"><span data-stu-id="71fae-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="71fae-105">Quando você publica um aplicativo com o Proxy de aplicativo, defina uma URL interna, mas, às vezes, que não é página Olá que seus usuários verá primeiro.</span><span class="sxs-lookup"><span data-stu-id="71fae-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="71fae-106">Defina uma página inicial personalizada para que os usuários forem página direita toohello quando acessam aplicativos Olá Olá painel de acesso do Azure Active Directory ou o iniciador do aplicativo hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="71fae-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="71fae-107">Quando os usuários iniciam um aplicativo hello, eles direcionado por padrão toohello URL de domínio raiz para o aplicativo publicado hello.</span><span class="sxs-lookup"><span data-stu-id="71fae-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="71fae-108">página de aterrissagem Olá normalmente é definida como a URL da home page hello.</span><span class="sxs-lookup"><span data-stu-id="71fae-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="71fae-109">Use hello Azure AD PowerShell módulo toodefine página inicial personalizada URLs quando desejar que o aplicativo tooland de usuários em uma página específica no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="71fae-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="71fae-110">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="71fae-110">For example:</span></span>
- <span data-ttu-id="71fae-111">Dentro da rede corporativa, os usuários estão muito*https://ExpenseApp/login/login.aspx* toosign no e acessar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71fae-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="71fae-112">Como você tem outros ativos como imagens que o Proxy de aplicativo precisa tooaccess no nível superior de saudação da estrutura de pasta hello, publicar aplicativo hello com *https://ExpenseApp* como Olá URL interna.</span><span class="sxs-lookup"><span data-stu-id="71fae-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="71fae-113">Olá URL externa padrão é *https://ExpenseApp-contoso.msappproxy.net*, que não tem sua inscrição de toohello usuários na página.</span><span class="sxs-lookup"><span data-stu-id="71fae-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="71fae-114">Definir *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* como Olá toogive de URL da página inicial, seus usuários uma experiência perfeita.</span><span class="sxs-lookup"><span data-stu-id="71fae-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="71fae-115">Quando você concede aos usuários acesso a aplicativos toopublished, Olá aplicativos são exibidos no hello [painel de acesso do AD do Azure](active-directory-saas-access-panel-introduction.md) e hello [iniciador do aplicativo do Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="71fae-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="71fae-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="71fae-116">Before you start</span></span>

<span data-ttu-id="71fae-117">Antes de configurar a URL da home page hello, lembre-Olá mente requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="71fae-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="71fae-118">Certifique-se de que esse caminho de saudação especificado é um caminho de subdomínio da URL de domínio de raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="71fae-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="71fae-119">Se for a URL do domínio raiz de saudação, por exemplo, https://apps.contoso.com/app1/, Olá URL da página inicial que você configura deve começar com https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="71fae-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="71fae-120">Se você fizer uma alteração toohello publicado o aplicativo, alteração Olá pode redefinir o valor de saudação do hello URL da página inicial.</span><span class="sxs-lookup"><span data-stu-id="71fae-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="71fae-121">Quando você atualiza o aplicativo hello Olá futura, você deve verificar novamente e, se necessário, atualize a URL da home page hello.</span><span class="sxs-lookup"><span data-stu-id="71fae-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="71fae-122">Alterar Olá home page no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="71fae-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="71fae-123">Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.</span><span class="sxs-lookup"><span data-stu-id="71fae-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="71fae-124">Navegue muito**Active Directory do Azure** > **registros do aplicativo** e escolha o aplicativo hello lista.</span><span class="sxs-lookup"><span data-stu-id="71fae-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="71fae-125">Selecione **propriedades** das configurações da saudação.</span><span class="sxs-lookup"><span data-stu-id="71fae-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="71fae-126">Saudação de atualização **URL da Home page** campo com o novo caminho.</span><span class="sxs-lookup"><span data-stu-id="71fae-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![Forneça a nova URL da página inicial](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="71fae-128">Selecione **Salvar**</span><span class="sxs-lookup"><span data-stu-id="71fae-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="71fae-129">Alterar Olá home page com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="71fae-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="71fae-130">Instalar o módulo do PowerShell do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="71fae-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="71fae-131">Antes de definir uma URL de página inicial personalizada usando o PowerShell, instale o módulo do PowerShell do Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="71fae-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="71fae-132">Você pode baixar o pacote de saudação do hello [Galeria do PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), que usa Olá ponto de extremidade de API do Graph.</span><span class="sxs-lookup"><span data-stu-id="71fae-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="71fae-133">Olá tooinstall do pacote, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="71fae-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="71fae-134">Abrir uma janela do PowerShell padrão e, em seguida, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="71fae-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="71fae-135">Se você estiver executando o comando hello como não administrador, use Olá `-scope currentuser` opção.</span><span class="sxs-lookup"><span data-stu-id="71fae-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="71fae-136">Durante a instalação do hello, selecione **Y** tooinstall dois pacotes de Nuget.org. Ambos os pacotes são necessários.</span><span class="sxs-lookup"><span data-stu-id="71fae-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="71fae-137">Localize Olá ObjectID do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="71fae-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="71fae-138">Obter Olá ObjectID do aplicativo hello e, em seguida, procure o aplicativo de saudação por sua página inicial.</span><span class="sxs-lookup"><span data-stu-id="71fae-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="71fae-139">Abra o PowerShell e importe o módulo de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="71fae-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="71fae-140">Entre toohello módulo AD do Azure como administrador de locatários hello.</span><span class="sxs-lookup"><span data-stu-id="71fae-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="71fae-141">Localize o aplicativo hello com base em sua URL da página inicial.</span><span class="sxs-lookup"><span data-stu-id="71fae-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="71fae-142">Você pode encontrar hello URL no portal de saudação indo muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="71fae-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="71fae-143">Este exemplo usa *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="71fae-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="71fae-144">Você deve obter um resultado semelhante toohello mostrada aqui.</span><span class="sxs-lookup"><span data-stu-id="71fae-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="71fae-145">Saudação de cópia toouse ObjectID GUID na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="71fae-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="71fae-146">Atualizar a URL da home page Olá</span><span class="sxs-lookup"><span data-stu-id="71fae-146">Update hello home page URL</span></span>

<span data-ttu-id="71fae-147">Olá mesmo módulo do PowerShell que você usou para a etapa 1, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71fae-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="71fae-148">Confirme se você tem Olá corrigir o aplicativo e substitua *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* com hello ObjectID que você copiou na saudação anterior da etapa.</span><span class="sxs-lookup"><span data-stu-id="71fae-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="71fae-149">Agora que você confirmou aplicativo hello, você está pronto tooupdate Olá home page da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="71fae-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="71fae-150">Crie um toohold de objeto de aplicativo em branco alterações Olá que você deseja toomake.</span><span class="sxs-lookup"><span data-stu-id="71fae-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="71fae-151">Essa variável contém valores hello que você deseja tooupdate.</span><span class="sxs-lookup"><span data-stu-id="71fae-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="71fae-152">Nada é criado nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="71fae-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="71fae-153">Definir valor toohello de URL de página inicial de saudação que você deseja.</span><span class="sxs-lookup"><span data-stu-id="71fae-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="71fae-154">valor de saudação deve ser um caminho de subdomínio do aplicativo publicado hello.</span><span class="sxs-lookup"><span data-stu-id="71fae-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="71fae-155">Por exemplo, se você alterar Olá URL da página inicial do *https://sharepoint-iddemo.msappproxy.net/* muito*https://sharepoint-iddemo.msappproxy.net/hybrid/*, os usuários do aplicativo vá diretamente toohello personalizado página inicial.</span><span class="sxs-lookup"><span data-stu-id="71fae-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="71fae-156">Verifique Olá update usando Olá GUID (ID de objeto) que você copiou na "etapa 1: localizar Olá ObjectID do aplicativo hello."</span><span class="sxs-lookup"><span data-stu-id="71fae-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="71fae-157">tooconfirm que a alteração de saudação foi bem-sucedida, reinicie o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="71fae-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="71fae-158">As alterações feitas toohello aplicativo poderão redefinir Olá URL da página inicial.</span><span class="sxs-lookup"><span data-stu-id="71fae-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="71fae-159">Se a URL da página inicial for redefinida, repita a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="71fae-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71fae-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71fae-160">Next steps</span></span>

- [<span data-ttu-id="71fae-161">Habilitar acesso remoto tooSharePoint com Proxy de aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="71fae-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="71fae-162">Habilitar Proxy de aplicativo no portal do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="71fae-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
