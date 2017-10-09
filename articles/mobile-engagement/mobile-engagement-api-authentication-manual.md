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
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Autenticar com APIs REST do Mobile Engagement - configuração manual
Isso é uma documentação de apêndice muito[autenticar com APIs de REST do Mobile Engagement](mobile-engagement-api-authentication.md). Verifique se que você ler o contexto de saudação tooget primeiro. Descreve uma maneira alternativa toodo Olá avulsas de instalação para configurar a autenticação para o uso de APIs de REST do Mobile Engagement Olá Olá Portal do Azure. 

> [!NOTE]
> instruções de saudação abaixo baseiam-se neste [guia do Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) e personalizado para o que é necessário para autenticação do Mobile Engagement APIs. Então consulte tooit se você quiser toounderstand Olá etapas em detalhes. 
> 
> 

1. Logon tooyour conta do Azure por meio de saudação [portal clássico](https://manage.windowsazure.com/).
2. Selecione **do Active Directory** no painel esquerdo do hello.
   
     ![selecionar Active Directory][1]
3. Escolha Olá **do Active Directory padrão** em seu portal do Azure. 
   
     ![escolher o diretório][2]
   
   > [!IMPORTANT]
   > Essa abordagem funciona somente quando você estiver trabalhando no padrão de saudação do Active Directory da sua conta e não funcionará se você estiver fazendo isso em um Active Directory que você criou em sua conta. 
   > 
   > 
4. aplicativos de saudação tooview em seu diretório, clique em **aplicativos**.
   
     ![exibir aplicativos][3]
5. Clique em **ADICIONAR**. 
   
     ![adicionar aplicativo][4]
6. Clique em **Adicionar um aplicativo que minha organização está desenvolvendo**
   
     ![novo aplicativo][5]
7. Preencha o nome do aplicativo hello e tipo de select saudação do aplicativo como **aplicativo de WEB e/ou API WEB** e clique no botão Avançar hello.
   
     ![nomear aplicativo][6]
8. É possível fornecer URLs fictícias para **URL DE LOGON** e **URI DA ID DO APLICATIVO**. Não são usados para o nosso cenário e URLs de saudação si não são validados.  
   
     ![propriedades do aplicativo][7]
9. Final de saudação de isso, você terá um aplicativo AAD com nome hello fornecidas anteriormente como Olá seguinte. Este é o seu **NOME\_APLICATIVO\_AD**. Anote-o.  
   
     ![nome do aplicativo][8]
10. Clique no nome do aplicativo hello e clique em **configurar**.
    
      ![configurar aplicativo][9]
11. Anote Olá ID do cliente que será usado como **cliente\_ID** para sua API chama. 
    
     ![configurar aplicativo][10]
12. Role para baixo toohello **chaves** seção e adicione uma chave com preferência duração de 2 anos (expiração) e clique em **salvar**. 
    
     ![configurar aplicativo][11]
13. Copie imediatamente o valor de saudação que é mostrado para a chave de saudação conforme ele só é exibido agora e não está armazenado, portanto não será exibido novamente cada vez. Se você perder a ele, em seguida, você terá toogenerate uma nova chave. Isso será Olá **CLIENT_SECRET** para sua API chama. 
    
     ![configurar aplicativo][12]
    
    > [!IMPORTANT]
    > Essa chave expirará no final de saudação da duração de saudação especificado caso toorenew de Certifique-se de que, quando chegar a hora da saudação caso contrário, a autenticação de API não funcionará mais. Você também pode excluir e recriar essa chave se achar que ela foi comprometida.
    > 
    > 
14. Clique em **exibir pontos de EXTREMIDADE** botão agora que será aberta, Olá **pontos de extremidade do aplicativo** caixa de diálogo. 
    
    ![][13]
15. Na caixa de diálogo de pontos de extremidade do aplicativo hello, copie Olá **ponto de EXTREMIDADE TOKEN OAUTH 2.0**. 
    
    ![][14]
16. Esse ponto de extremidade será em Olá após o formulário onde Olá GUID na URL de saudação é seu **TENANT_ID** então anote-lo: 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. Agora podemos continuar tooconfigure permissões Olá este aplicativo. Para isso, você terá tooopen backup Olá [portal do Azure](https://portal.azure.com). 
18. Clique em **grupos de recursos** e localize Olá **Mobile Engagement** grupo de recursos.  
    
    ![][15]
19. Clique em Olá **Mobile Engagement** recursos de grupo e navegue toohello **configurações** folha aqui. 
    
    ![][16]
20. Clique em **usuários** em Olá folha de configurações e, em seguida, clique em **adicionar** tooadd um usuário. 
    
    ![][17]
21. Clique em **Selecionar uma função**
    
    ![][18]
22. Clique em **Proprietário**
    
    ![][19]
23. Pesquisa de nome de saudação do seu aplicativo **AD\_aplicativo\_nome** na caixa de pesquisa de saudação. Você não verá ele por padrão aqui. Depois de encontrar, selecione-o e clique em **selecione** na parte inferior da saudação da folha de saudação. 
    
    ![][20]
24. Em Olá **adicionar acesso** folha, ele será exibido como **1 usuário, 0 grupos**. Clique em **Okey** sobre essa alteração de saudação tooconfirm folha. 
    
    ![][21]

Agora você concluiu Olá necessária configuração de AAD e são Olá toocall de todos os conjunto de APIs. 

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



