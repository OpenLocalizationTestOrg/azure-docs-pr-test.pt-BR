---
title: "aaaHow tooconfigure a autenticação do Active Directory do Azure para seu aplicativo de serviços de aplicativos"
description: "Saiba como autenticação do Active Directory do Azure tooconfigure para seu aplicativo de serviços de aplicativos."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>Como tooconfigure seu logon do serviço de aplicativo aplicativo toouse Active Directory do Azure
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Este tópico mostra como tooconfigure toouse de serviços de aplicativo do Azure Active Directory do Azure como um provedor de autenticação.

## <a name="express"> </a>Configurar o Active Directory do Azure usando configurações expressas
1. Em Olá [portal do Azure], navegar tooyour aplicativo. Clique em **Configurações** e depois em **Autenticação/Autorização**.
2. Se Olá autenticação / autorização de recurso não está ativada, ative o comutador hello muito**em**.
3. Clique em **Azure Active Directory** e clique em **Expresso** em **Modo de Gerenciamento**.
4. Clique em **Okey** tooregister aplicativo de hello no Active Directory do Azure. Isso criará um novo registro. Se você quiser toochoose um registro existente em vez disso, clique em **selecionar um aplicativo existente** e procure por nome de saudação de um registro criado anteriormente no seu locatário.
   Clique em Olá registro tooselect-lo e clique em **Okey**. Em seguida, clique em **Okey** na folha de configurações do Active Directory do Azure hello.
   
   ![][0]
   
   Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs. Você deve autorizar os usuários no código do aplicativo.
5. (Opcional) toorestrict acesso tooyour site tooonly usuários autenticados pelo Active Directory do Azure, definir **tootake de ação quando a solicitação não está autenticada** muito**fazer logon com Active Directory do Azure**. Isso requer que todas as solicitações autenticadas, e todas as solicitações não autenticadas são redirecionada tooAzure do Active Directory para autenticação.
6. Clique em **Salvar**.

Agora você está pronto toouse Active Directory do Azure para autenticação em seu aplicativo.

## <a name="advanced"> </a>(Método alternativo) Configurar manualmente o Active Directory do Azure com configurações avançadas
Você também pode escolher tooprovide definições de configuração manualmente. Isso é solução Olá preferido se locatário do AAD Olá desejar toouse for diferente do locatário Olá com a qual você entrar no Azure. configuração de saudação toocomplete, você deve primeiro criar um registro no Active Directory do Azure e, em seguida, você deve fornecer algumas Olá registro detalhes tooApp serviço.

### <a name="register"> </a>Registrar seu aplicativo com o Active Directory do Azure
1. Faça logon no toohello [portal do Azure]e navegue tooyour aplicativo. Copie a **URL**. Você usará esse tooconfigure seu aplicativo do Active Directory do Azure.
2. Entrar toohello [portal clássico do Azure] e navegue muito**do Active Directory**.
   
    ![][2]
3. Selecione seu diretório e selecione Olá **aplicativos** guia na parte superior da saudação. Clique em **adicionar** em Olá inferior toocreate um novo registro de aplicativo.
4. Clique em **Adicionar um aplicativo que a minha organização está desenvolvendo**.
5. No hello Adicionar Assistente de aplicativo, insira um **nome** para seu aplicativo e clique em hello **aplicativo de Web e/ou API Web** tipo. Em seguida, clique em toocontinue.
6. Em Olá **URL de logon** caixa, cole a URL do aplicativo hello copiados anteriormente. Digite essa mesma URL no hello **URI da ID do aplicativo** caixa. Em seguida, clique em toocontinue.
7. Depois que o aplicativo hello tiver sido adicionado, clique em Olá **configurar** guia. Editar saudação **URL de resposta** em **Single Sign-on** toobe Olá URL do seu aplicativo anexado ao caminho hello, */.auth/login/aad/callback*. Por exemplo: `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Certifique-se de que você está usando o esquema do hello HTTPS.
   
    ![][3]
8. Clique em **Salvar**. Então Olá cópia **ID do cliente** para o aplicativo hello. Você irá configurar seu aplicativo toouse isso mais tarde.
9. Na barra de comandos do hello inferior, clique em **exibir pontos de extremidade**e, em seguida, copie hello **documento de metadados de Federação** URL e o download de documentos ou navegue tooit em um navegador.
10. Na raiz da saudação **EntityDescriptor** elemento, deve haver uma **entityID** atributo do formulário Olá `https://sts.windows.net/` seguido de um locatário específico tooyour do GUID (chamado de "ID de locatário"). Copie esse valor - ele servirá como sua **URL do Emissor**. Você irá configurar seu aplicativo toouse isso mais tarde.

### <a name="secrets"></a>Aplicativo de tooyour de informações de adicionar o Azure Active Directory
1. Em Olá [portal do Azure], navegar tooyour aplicativo. Clique em **Configurações** e depois em **Autenticação/Autorização**.
2. Se o recurso de autenticação/autorização Olá não estiver habilitado, desative comutador hello muito**em**.
3. Clique em **Azure Active Directory** e clique em **Avançado** em **Modo de Gerenciamento**. Colar em Olá ID do cliente e a URL do emissor de valor que você obtido anteriormente. Em seguida, clique em **OK**.
   
   ![][1]
   
   Por padrão, o serviço de aplicativo fornece autenticação, mas não restringe o conteúdo do site tooyour acesso autorizado e APIs. Você deve autorizar os usuários no código do aplicativo.
4. (Opcional) toorestrict acesso tooyour site tooonly usuários autenticados pelo Active Directory do Azure, definir **tootake de ação quando a solicitação não está autenticada** muito**fazer logon com Active Directory do Azure**. Isso requer que todas as solicitações autenticadas, e todas as solicitações não autenticadas são redirecionada tooAzure do Active Directory para autenticação.
5. Clique em **Salvar**.

Agora você está pronto toouse Active Directory do Azure para autenticação em seu aplicativo.

## <a name="optional-configure-a-native-client-application"></a>(Opcional) Configurar um aplicativo de cliente nativo
Active Directory do Azure também permite que você tooregister de clientes nativos, que proporciona maior controle sobre as permissões de mapeamento. Isso é necessário se desejar tooperform logons usando uma biblioteca como Olá **biblioteca de autenticação do Active Directory**.

1. Navegue muito**do Active Directory** em Olá [portal clássico do Azure].
2. Selecione seu diretório e selecione Olá **aplicativos** guia na parte superior da saudação. Clique em **adicionar** em Olá inferior toocreate um novo registro de aplicativo.
3. Clique em **Adicionar um aplicativo que a minha organização está desenvolvendo**.
4. No hello Adicionar Assistente de aplicativo, insira um **nome** para seu aplicativo e clique em hello **aplicativo cliente nativo** tipo. Em seguida, clique em toocontinue.
5. Em Olá **URI de redirecionamento** , digite o seu site */.auth/login/done* ponto de extremidade, usando o esquema do hello HTTPS. Esse valor deve ser semelhante muito*https://contoso.azurewebsites.net/.auth/login/done*. Se criar um aplicativo do Windows, em vez disso, use Olá [SID do pacote](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) como Olá URI.
6. Após a adição de aplicativo nativo hello, clique em Olá **configurar** guia. Localize Olá **ID do cliente** e anote esse valor.
7. Página de saudação de rolagem para baixo toohello **permissões tooother aplicativos** seção e clique em **Adicionar aplicativo**.
8. Procure o aplicativo web hello que você registrou anteriormente e clique em ícone de adição hello. Clique em caixa de diálogo da saudação tooclose Olá seleção. Se o aplicativo da web hello não pode ser encontrado, navegue registro tooits e adicionar uma nova URL de resposta (por exemplo, Olá versão HTTP da URL atual), clique em Salvar e, em seguida, repita essas etapas - aplicativo hello deve aparecer na lista de saudação.
9. No hello nova entrada adicionada, abra Olá **permissões delegadas** lista suspensa e selecione **acesso (appName)**. Em seguida, clique em **Salvar**.

Você configurou um aplicativo de cliente nativo que pode acessar o aplicativo de Serviço de Aplicativo.

## <a name="related-content"> </a>Conteúdo relacionado
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[portal do Azure]: https://portal.azure.com/
[portal clássico do Azure]: https://manage.windowsazure.com/
[alternative method]:#advanced
