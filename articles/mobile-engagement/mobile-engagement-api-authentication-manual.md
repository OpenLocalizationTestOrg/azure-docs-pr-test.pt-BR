---
title: "aaaAuthenticate com APIs de REST do Mobile Engagement - configuração manual"
description: "Descreve como toomanually configurar autenticação para APIs de REST do Mobile Engagement"
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
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="207db-103">Autenticar com APIs REST do Mobile Engagement - configuração manual</span><span class="sxs-lookup"><span data-stu-id="207db-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="207db-104">Isso é uma documentação de apêndice muito[autenticar com APIs de REST do Mobile Engagement](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="207db-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="207db-105">Verifique se que você ler o contexto de saudação tooget primeiro.</span><span class="sxs-lookup"><span data-stu-id="207db-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="207db-106">Descreve uma maneira alternativa toodo Olá avulsas de instalação para configurar a autenticação para o uso de APIs de REST do Mobile Engagement Olá Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="207db-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="207db-107">instruções de saudação abaixo baseiam-se neste [guia do Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) e personalizado para o que é necessário para autenticação do Mobile Engagement APIs.</span><span class="sxs-lookup"><span data-stu-id="207db-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="207db-108">Então consulte tooit se você quiser toounderstand Olá etapas em detalhes.</span><span class="sxs-lookup"><span data-stu-id="207db-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="207db-109">Logon tooyour conta do Azure por meio de saudação [portal clássico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="207db-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="207db-110">Selecione **do Active Directory** no painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="207db-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![selecionar Active Directory][1]
3. <span data-ttu-id="207db-112">Escolha Olá **do Active Directory padrão** em seu portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="207db-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![escolher o diretório][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="207db-114">Essa abordagem funciona somente quando você estiver trabalhando no padrão de saudação do Active Directory da sua conta e não funcionará se você estiver fazendo isso em um Active Directory que você criou em sua conta.</span><span class="sxs-lookup"><span data-stu-id="207db-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="207db-115">aplicativos de saudação tooview em seu diretório, clique em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="207db-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![exibir aplicativos][3]
5. <span data-ttu-id="207db-117">Clique em **ADICIONAR**.</span><span class="sxs-lookup"><span data-stu-id="207db-117">Click on **ADD**.</span></span> 
   
     ![adicionar aplicativo][4]
6. <span data-ttu-id="207db-119">Clique em **Adicionar um aplicativo que minha organização está desenvolvendo**</span><span class="sxs-lookup"><span data-stu-id="207db-119">Click on **Add an application my organization is developing**</span></span>
   
     ![novo aplicativo][5]
7. <span data-ttu-id="207db-121">Preencha o nome do aplicativo hello e tipo de select saudação do aplicativo como **aplicativo de WEB e/ou API WEB** e clique no botão Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="207db-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![nomear aplicativo][6]
8. <span data-ttu-id="207db-123">É possível fornecer URLs fictícias para **URL DE LOGON** e **URI DA ID DO APLICATIVO**.</span><span class="sxs-lookup"><span data-stu-id="207db-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="207db-124">Não são usados para o nosso cenário e URLs de saudação si não são validados.</span><span class="sxs-lookup"><span data-stu-id="207db-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![propriedades do aplicativo][7]
9. <span data-ttu-id="207db-126">Final de saudação de isso, você terá um aplicativo AAD com nome hello fornecidas anteriormente como Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="207db-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="207db-127">Este é o seu **NOME\_APLICATIVO\_AD**. Anote-o.</span><span class="sxs-lookup"><span data-stu-id="207db-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![nome do aplicativo][8]
10. <span data-ttu-id="207db-129">Clique no nome do aplicativo hello e clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="207db-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![configurar aplicativo][9]
11. <span data-ttu-id="207db-131">Anote Olá ID do cliente que será usado como **cliente\_ID** para sua API chama.</span><span class="sxs-lookup"><span data-stu-id="207db-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![configurar aplicativo][10]
12. <span data-ttu-id="207db-133">Role para baixo toohello **chaves** seção e adicione uma chave com preferência duração de 2 anos (expiração) e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="207db-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![configurar aplicativo][11]
13. <span data-ttu-id="207db-135">Copie imediatamente o valor de saudação que é mostrado para a chave de saudação conforme ele só é exibido agora e não está armazenado, portanto não será exibido novamente cada vez.</span><span class="sxs-lookup"><span data-stu-id="207db-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="207db-136">Se você perder a ele, em seguida, você terá toogenerate uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="207db-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="207db-137">Isso será Olá **CLIENT_SECRET** para sua API chama.</span><span class="sxs-lookup"><span data-stu-id="207db-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![configurar aplicativo][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="207db-139">Essa chave expirará no final de saudação da duração de saudação especificado caso toorenew de Certifique-se de que, quando chegar a hora da saudação caso contrário, a autenticação de API não funcionará mais.</span><span class="sxs-lookup"><span data-stu-id="207db-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="207db-140">Você também pode excluir e recriar essa chave se achar que ela foi comprometida.</span><span class="sxs-lookup"><span data-stu-id="207db-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="207db-141">Clique em **exibir pontos de EXTREMIDADE** botão agora que será aberta, Olá **pontos de extremidade do aplicativo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="207db-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="207db-142">Na caixa de diálogo de pontos de extremidade do aplicativo hello, copie Olá **ponto de EXTREMIDADE TOKEN OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="207db-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="207db-143">Esse ponto de extremidade será em Olá após o formulário onde Olá GUID na URL de saudação é seu **TENANT_ID** então anote-lo:</span><span class="sxs-lookup"><span data-stu-id="207db-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="207db-144">Agora podemos continuar tooconfigure permissões Olá este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="207db-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="207db-145">Para isso, você terá tooopen backup Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="207db-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="207db-146">Clique em **grupos de recursos** e localize Olá **Mobile Engagement** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="207db-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="207db-147">Clique em Olá **Mobile Engagement** recursos de grupo e navegue toohello **configurações** folha aqui.</span><span class="sxs-lookup"><span data-stu-id="207db-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="207db-148">Clique em **usuários** em Olá folha de configurações e, em seguida, clique em **adicionar** tooadd um usuário.</span><span class="sxs-lookup"><span data-stu-id="207db-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="207db-149">Clique em **Selecionar uma função**</span><span class="sxs-lookup"><span data-stu-id="207db-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="207db-150">Clique em **Proprietário**</span><span class="sxs-lookup"><span data-stu-id="207db-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="207db-151">Pesquisa de nome de saudação do seu aplicativo **AD\_aplicativo\_nome** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="207db-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="207db-152">Você não verá ele por padrão aqui.</span><span class="sxs-lookup"><span data-stu-id="207db-152">You will not see this by default here.</span></span> <span data-ttu-id="207db-153">Depois de encontrar, selecione-o e clique em **selecione** na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="207db-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="207db-154">Em Olá **adicionar acesso** folha, ele será exibido como **1 usuário, 0 grupos**.</span><span class="sxs-lookup"><span data-stu-id="207db-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="207db-155">Clique em **Okey** sobre essa alteração de saudação tooconfirm folha.</span><span class="sxs-lookup"><span data-stu-id="207db-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="207db-156">Agora você concluiu Olá necessária configuração de AAD e são Olá toocall de todos os conjunto de APIs.</span><span class="sxs-lookup"><span data-stu-id="207db-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

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



