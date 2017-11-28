---
title: "Autenticar com APIs REST do Mobile Engagement - configuração manual"
description: "Descreve como configurar manualmente a autenticação para APIs REST do Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="29ef1-103">Autenticar com APIs REST do Mobile Engagement - configuração manual</span><span class="sxs-lookup"><span data-stu-id="29ef1-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="29ef1-104">Esta é uma documentação de apêndice de [Autenticar com APIs REST do Mobile Engagement](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="29ef1-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="29ef1-105">Leia esse artigo primeiro para obter o contexto.</span><span class="sxs-lookup"><span data-stu-id="29ef1-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="29ef1-106">Ele descreve uma maneira alternativa de fazer a configuração única da autenticação para APIs REST do Mobile Engagement usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29ef1-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="29ef1-107">As instruções a seguir se baseiam nesse [Guia do Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) e são personalizadas para o que é necessário para a autenticação de APIs do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="29ef1-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="29ef1-108">Portanto, consulte-o para entender as etapas abaixo em detalhes.</span><span class="sxs-lookup"><span data-stu-id="29ef1-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="29ef1-109">Faça logon na sua conta do Azure por meio do [portal clássico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="29ef1-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="29ef1-110">Selecione **Active Directory** no painel à esquerda.</span><span class="sxs-lookup"><span data-stu-id="29ef1-110">Select **Active Directory** from the left pane.</span></span>
   
     ![selecionar Active Directory][1]
3. <span data-ttu-id="29ef1-112">Escolha o **Active Directory Padrão** em seu portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29ef1-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![escolher o diretório][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="29ef1-114">Essa abordagem funciona somente quando você está trabalhando no Active Directory padrão de sua conta, e não funcionará se você estiver fazendo isso em um Active Directory que você criou em sua conta.</span><span class="sxs-lookup"><span data-stu-id="29ef1-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="29ef1-115">Para exibir os aplicativos em seu diretório, clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![exibir aplicativos][3]
5. <span data-ttu-id="29ef1-117">Clique em **ADICIONAR**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-117">Click on **ADD**.</span></span> 
   
     ![adicionar aplicativo][4]
6. <span data-ttu-id="29ef1-119">Clique em **Adicionar um aplicativo que minha organização está desenvolvendo**</span><span class="sxs-lookup"><span data-stu-id="29ef1-119">Click on **Add an application my organization is developing**</span></span>
   
     ![novo aplicativo][5]
7. <span data-ttu-id="29ef1-121">Preencha o nome do aplicativo e selecione o tipo de aplicativo como **APLICATIVO WEB E/OU API WEB** e clique no botão Avançar.</span><span class="sxs-lookup"><span data-stu-id="29ef1-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![nomear aplicativo][6]
8. <span data-ttu-id="29ef1-123">É possível fornecer URLs fictícias para **URL DE LOGON** e **URI DA ID DO APLICATIVO**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="29ef1-124">Elas não são usadas em nosso cenário e as próprias URLs não são validadas.</span><span class="sxs-lookup"><span data-stu-id="29ef1-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![propriedades do aplicativo][7]
9. <span data-ttu-id="29ef1-126">Ao final deste artigo, você terá um aplicativo AAD com o nome fornecido anteriormente, como o seguinte.</span><span class="sxs-lookup"><span data-stu-id="29ef1-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="29ef1-127">Este é o seu **NOME\_APLICATIVO\_AD**. Anote-o.</span><span class="sxs-lookup"><span data-stu-id="29ef1-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![nome do aplicativo][8]
10. <span data-ttu-id="29ef1-129">Clique no nome do aplicativo e clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-129">Click on the app name and click on **Configure**.</span></span>
    
      ![configurar aplicativo][9]
11. <span data-ttu-id="29ef1-131">Anote a ID DO CLIENTE que será usada como **ID\_CLIENTE** para suas chamadas à API.</span><span class="sxs-lookup"><span data-stu-id="29ef1-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![configurar aplicativo][10]
12. <span data-ttu-id="29ef1-133">Role para baixo até a seção **Chaves** e adicione uma chave com duração de dois anos (validade) de preferência e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![configurar aplicativo][11]
13. <span data-ttu-id="29ef1-135">Copie imediatamente o valor mostrado para a chave, pois ele será exibido apenas agora e não será armazenado, portanto, não será exibido novamente.</span><span class="sxs-lookup"><span data-stu-id="29ef1-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="29ef1-136">Se você perdê-lo, terá que gerar uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="29ef1-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="29ef1-137">Esse será o **SEGREDO_DO_CLIENTE** para suas chamadas à API.</span><span class="sxs-lookup"><span data-stu-id="29ef1-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![configurar aplicativo][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="29ef1-139">Essa chave expirará ao final da duração especificada, portanto lembre-se de renová-la quando chegar a hora, caso contrário a autenticação da API não funcionará mais.</span><span class="sxs-lookup"><span data-stu-id="29ef1-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="29ef1-140">Você também pode excluir e recriar essa chave se achar que ela foi comprometida.</span><span class="sxs-lookup"><span data-stu-id="29ef1-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="29ef1-141">Clique no botão **EXIBIR PONTOS DE EXTREMIDADE**, o que abrirá a caixa de diálogo **Pontos de Extremidade do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="29ef1-142">Na caixa de diálogo Pontos de Extremidade do Aplicativo, copie o **PONTO DE EXTREMIDADE DO TOKEN OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="29ef1-143">Esse ponto de extremidade terá o seguinte formato, em que o GUID na URL é seu **TENANT_ID**, então anote-o:</span><span class="sxs-lookup"><span data-stu-id="29ef1-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="29ef1-144">Agora, configuraremos as permissões nesse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29ef1-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="29ef1-145">Para isso, você precisará abrir o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="29ef1-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="29ef1-146">Clique em **Grupos de Recursos** e localize o grupo de recursos **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="29ef1-147">Clique no grupo de recursos **Mobile Engagement** e navegue até a folha **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="29ef1-148">Clique em **Usuários** na folha Configurações e clique em **Adicionar** para adicionar um usuário.</span><span class="sxs-lookup"><span data-stu-id="29ef1-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="29ef1-149">Clique em **Selecionar uma função**</span><span class="sxs-lookup"><span data-stu-id="29ef1-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="29ef1-150">Clique em **Proprietário**</span><span class="sxs-lookup"><span data-stu-id="29ef1-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="29ef1-151">Procure o nome de seu aplicativo **NOME\_APLICATIVO\_AD** na caixa Pesquisar.</span><span class="sxs-lookup"><span data-stu-id="29ef1-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="29ef1-152">Você não verá ele por padrão aqui.</span><span class="sxs-lookup"><span data-stu-id="29ef1-152">You will not see this by default here.</span></span> <span data-ttu-id="29ef1-153">Depois de encontrá-lo, selecione-o e clique em **Selecionar** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="29ef1-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="29ef1-154">Na folha **Adicionar Acesso**, ele será exibido como **1 usuário, 0 grupos**.</span><span class="sxs-lookup"><span data-stu-id="29ef1-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="29ef1-155">Clique em **OK** nessa folha para confirmar a alteração.</span><span class="sxs-lookup"><span data-stu-id="29ef1-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="29ef1-156">Agora você concluiu a configuração necessária do AAD e está pronto para chamar as APIs.</span><span class="sxs-lookup"><span data-stu-id="29ef1-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



