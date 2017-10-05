---
title: Definir uma home page personalizada para aplicativos publicados usando o Proxy de Aplicativo Azure AD | Microsoft Docs
description: "Abora as noções básicas sobre os conectores do Proxy de Aplicativo Azure AD"
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
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="83511-103">Definir uma home page personalizada para aplicativos publicados usando o Proxy de Aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="83511-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="83511-104">Este artigo descreve como configurar aplicativos para direcionar os usuários para uma página inicial personalizada.</span><span class="sxs-lookup"><span data-stu-id="83511-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="83511-105">Ao publicar um aplicativo com o Proxy do aplicativo, você define uma URL interna, mas, às vezes, essa não é a página que os usuários devem ver primeiro.</span><span class="sxs-lookup"><span data-stu-id="83511-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="83511-106">Defina uma página inicial personalizada para que os usuários acessem a página correta quando acessarem os aplicativos do Painel de acesso do Azure Active Directory ou do iniciador de aplicativos do Office 365.</span><span class="sxs-lookup"><span data-stu-id="83511-106">Set a custom home page so that your users go to the right page when they access the apps from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="83511-107">Quando os usuários iniciam o aplicativo, são direcionados por padrão para a URL de domínio raiz do aplicativo publicado.</span><span class="sxs-lookup"><span data-stu-id="83511-107">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="83511-108">A página de aterrissagem é normalmente definida como a URL da home page.</span><span class="sxs-lookup"><span data-stu-id="83511-108">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="83511-109">Use o módulo do PowerShell do Azure AD para definir URLs de página inicial personalizada quando desejar que os usuários do aplicativo acessem uma página específica no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83511-109">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="83511-110">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="83511-110">For example:</span></span>
- <span data-ttu-id="83511-111">Dentro da rede corporativa, os usuários usam a URL *https://ExpenseApp/login/login.aspx* para entrar e acessar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83511-111">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="83511-112">Como você tem outros ativos como imagens que o Proxy do aplicativo precisa acessar no nível superior da estrutura de pasta, você publica o aplicativo com *https://ExpenseApp* como a URL interna.</span><span class="sxs-lookup"><span data-stu-id="83511-112">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="83511-113">A URL externa padrão é *https://ExpenseApp-contoso.msappproxy.net*, que não leva os usuários até a página de entrada.</span><span class="sxs-lookup"><span data-stu-id="83511-113">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign in page.</span></span>  
- <span data-ttu-id="83511-114">Defina *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* como a URL da página inicial para dar aos usuários uma experiência contínua.</span><span class="sxs-lookup"><span data-stu-id="83511-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL to give your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="83511-115">Quando você conceder aos usuários acesso a aplicativos publicados, os aplicativos são exibidos no [painel de acesso do Azure AD](active-directory-saas-access-panel-introduction.md) e [lançador de aplicativo do Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="83511-115">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="83511-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="83511-116">Before you start</span></span>

<span data-ttu-id="83511-117">Antes de definir a URL da página inicial, tenha em mente os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="83511-117">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="83511-118">Garanta que o caminho especificado seja um caminho de subdomínio da URL raiz do domínio.</span><span class="sxs-lookup"><span data-stu-id="83511-118">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="83511-119">Se a URL do domínio raiz for, por exemplo, https://apps.contoso.com/app1/, a URL da página inicial que você configura deverá começar com https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="83511-119">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="83511-120">Se você fizer uma alteração no aplicativo publicado, essa alteração poderá redefinir o valor da URL da home page.</span><span class="sxs-lookup"><span data-stu-id="83511-120">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="83511-121">Quando você decidir atualizar o aplicativo no futuro, você deverá verificar novamente e, se necessário, atualizar a URL da home page.</span><span class="sxs-lookup"><span data-stu-id="83511-121">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="83511-122">Altere a home page no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="83511-122">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="83511-123">Entre no [Portal do Azure](https://portal.azure.com) como administrador.</span><span class="sxs-lookup"><span data-stu-id="83511-123">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="83511-124">Navegue até **Azure Active Directory** > **Registros do aplicativo** e escolha o seu aplicativo na lista.</span><span class="sxs-lookup"><span data-stu-id="83511-124">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="83511-125">Selecione **Propriedades** entre as configurações.</span><span class="sxs-lookup"><span data-stu-id="83511-125">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="83511-126">Atualize o campo **URL da Home page** com o novo caminho.</span><span class="sxs-lookup"><span data-stu-id="83511-126">Update the **Home page URL** field with your new path.</span></span> 

   ![Forneça a nova URL da página inicial](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="83511-128">Selecione **Salvar**</span><span class="sxs-lookup"><span data-stu-id="83511-128">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="83511-129">Alterar a home page com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="83511-129">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="83511-130">Instalar o módulo do Powershell do Azure AD</span><span class="sxs-lookup"><span data-stu-id="83511-130">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="83511-131">Antes de definir uma URL personalizada de página inicial usando o PowerShell, instale o módulo PowerShell do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83511-131">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="83511-132">Baixe esse pacote da [Galeria do PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), que usa o ponto de extremidade de API do Graph.</span><span class="sxs-lookup"><span data-stu-id="83511-132">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="83511-133">Para instalar o pacote, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="83511-133">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="83511-134">Abra uma janela padrão do PowerShell e, em seguida, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="83511-134">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="83511-135">Se você estiver executando o comando como um não administrador, use a opção `-scope currentuser`.</span><span class="sxs-lookup"><span data-stu-id="83511-135">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="83511-136">Durante a instalação, selecione **Y** para instalar dois pacotes do Nuget.org. Ambos os pacotes são necessários.</span><span class="sxs-lookup"><span data-stu-id="83511-136">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="83511-137">Localizar a ObjectID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="83511-137">Find the ObjectID of the app</span></span>

<span data-ttu-id="83511-138">Obtenha o ID do objeto do aplicativo e, em seguida, procure o aplicativo por sua home page.</span><span class="sxs-lookup"><span data-stu-id="83511-138">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="83511-139">Abra o PowerShell e importe o módulo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83511-139">Open PowerShell and import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="83511-140">Entre no módulo Azure AD como o administrador de locatários.</span><span class="sxs-lookup"><span data-stu-id="83511-140">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="83511-141">Localize o aplicativo com base na respectiva URL da home page.</span><span class="sxs-lookup"><span data-stu-id="83511-141">Find the app based on its home page URL.</span></span> <span data-ttu-id="83511-142">Você pode localizar a URL no portal indo para **Azure Active Directory** > **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="83511-142">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="83511-143">Este exemplo usa *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="83511-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="83511-144">Você deve obter um resultado semelhante ao mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="83511-144">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="83511-145">Copie o GUID do ObjectID para usar na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="83511-145">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="83511-146">Atualizar a URL da home page</span><span class="sxs-lookup"><span data-stu-id="83511-146">Update the home page URL</span></span>

<span data-ttu-id="83511-147">No mesmo módulo do PowerShell que você usou para a etapa 1, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="83511-147">In the same PowerShell module that you used for step 1, perform the following steps:</span></span>

1. <span data-ttu-id="83511-148">Confirme se você tem o aplicativo correto e substitua *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* pelo ObjectID que você copiou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="83511-148">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="83511-149">Agora que você confirmou o aplicativo, está pronto para atualizar a home page da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="83511-149">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="83511-150">Crie um objeto de aplicativo em branco para armazenar as alterações que você deseja fazer.</span><span class="sxs-lookup"><span data-stu-id="83511-150">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="83511-151">Essa variável contém os valores que você deseja atualizar.</span><span class="sxs-lookup"><span data-stu-id="83511-151">This variable holds the values that you want to update.</span></span> <span data-ttu-id="83511-152">Nada é criado nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="83511-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="83511-153">Defina a URL da home page como o valor desejado.</span><span class="sxs-lookup"><span data-stu-id="83511-153">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="83511-154">O valor deve ser um caminho de subdomínio do aplicativo publicado.</span><span class="sxs-lookup"><span data-stu-id="83511-154">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="83511-155">Por exemplo, se você alterar a URL da página inicial de *https://sharepoint-iddemo.msappproxy.net/* para *https://sharepoint-iddemo.msappproxy.net/hybrid/*, os usuários do aplicativo serão levados diretamente para a página inicial personalizada.</span><span class="sxs-lookup"><span data-stu-id="83511-155">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="83511-156">Faça a atualização usando o GUID (ObjectID) que você copiou na "etapa 1: localizar o ID do objeto do aplicativo."</span><span class="sxs-lookup"><span data-stu-id="83511-156">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="83511-157">Para confirmar que a alteração foi bem-sucedida, reinicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="83511-157">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="83511-158">Todas as alterações que você fizer no aplicativo poderão redefinir a URL da home page.</span><span class="sxs-lookup"><span data-stu-id="83511-158">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="83511-159">Se a URL da página inicial for redefinida, repita a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="83511-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83511-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83511-160">Next steps</span></span>

- [<span data-ttu-id="83511-161">Habilitar acesso remoto ao SharePoint com o Proxy de Aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="83511-161">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="83511-162">Habilitar o Proxy de Aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="83511-162">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
