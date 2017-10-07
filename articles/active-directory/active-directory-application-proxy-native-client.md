---
title: aplicativos cliente nativos de aaaPublish - AD do Azure | Microsoft Docs
description: Aborda como tooenable toocommunicate de aplicativos cliente nativo com o conector de Proxy de aplicativo do AD do Azure tooprovide acesso remoto seguro tooyour local aplicativos.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>Como tooenable toointeract de aplicativos cliente nativo com o proxy de aplicativos

Em aplicativos de tooweb de adição, Proxy de aplicativo do Azure Active Directory também podem ser usados toopublish aplicativos de cliente nativo. Os aplicativos cliente nativos diferem dos aplicativos Web porque eles são instalados em um dispositivo, enquanto os aplicativos Web são acessados por meio de um navegador. 

O Proxy de Aplicativo dá suporte a aplicativos cliente nativos aceitando os tokens emitidos pelo Azure AD que são enviados nos cabeçalhos padrão Autorizar HTTP.

![Relação entre os usuários finais, o Active Directory do Azure e os aplicativos publicados](./media/active-directory-application-proxy-native-client/richclientflow.png)

Use Olá biblioteca de autenticação do AD do Azure, que cuida da autenticação e dá suporte a muitos ambientes de cliente, aplicativos nativos toopublish. Proxy de aplicativo se encaixa Olá [cenário do aplicativo nativo tooWeb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). Este artigo orienta Olá quatro etapas toopublish um aplicativo nativo com o Proxy de aplicativo e hello biblioteca de autenticação do AD do Azure. 

## <a name="step-1-publish-your-application"></a>Etapa 1: publicar seu aplicativo
Publicar seu aplicativo proxy como faria com qualquer outro aplicativo e atribuir usuários tooaccess seu aplicativo. Para saber mais, consulte [Publicar aplicativos com o Proxy de Aplicativo](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>Etapa 2: configurar seu aplicativo
Configure seu aplicativo nativo da seguinte maneira:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Navegue muito**Active Directory do Azure** > **registros do aplicativo**.
3. Selecione **Novo registro de aplicativo**.
4. Especifique um nome para seu aplicativo, selecione **nativo** como tipo de aplicativo hello e fornecem Olá URI de redirecionamento para seu aplicativo. 

   ![Criar um novo registro de aplicativo](./media/active-directory-application-proxy-native-client/create.png)
5. Selecione **Criar**.

Para obter informações mais detalhadas sobre como criar um novo registro de aplicativo, confira [Integrando aplicativos ao Azure Active Directory](.//develop/active-directory-integrating-applications.md).


## <a name="step-3-grant-access-tooother-applications"></a>Etapa 3: Acesso tooother candidaturas
Habilite Olá aplicativo nativo toobe exposto tooother aplicativos em seu diretório:

1. Ainda no **registros do aplicativo**, selecione Olá novo aplicativo nativo que você acabou de criar.
2. Selecione **Permissões necessárias**.
3. Selecione **Adicionar**.
4. Olá abrir a primeira etapa **selecionar uma API**.
5. Use Olá barra toofind Olá Proxy de aplicativo aplicativo de pesquisa que você publicou na primeira seção do hello. Escolha esse aplicativo e clique em **Selecionar**. 

   ![Procure Olá proxy aplicativo](./media/active-directory-application-proxy-native-client/select_api.png)
6. Segunda etapa de saudação aberto, **selecionar permissões**.
7. Olá caixa de seleção toogrant seu aplicativo de proxy do aplicativo nativo acesso tooyour e clique em **selecione**.

   ![Conceder acesso tooproxy aplicativo](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Selecione **Concluído**.


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>Etapa 4: Editar Olá biblioteca de autenticação do Active Directory
Edite o código do aplicativo nativo Olá no contexto de autenticação de saudação do Olá biblioteca de autenticação do Active Directory (ADAL) tooinclude Olá texto a seguir:

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

variáveis de saudação no código de exemplo hello devem ser substituídos da seguinte maneira:

* **ID do locatário** pode ser encontrado na Olá portal do Azure. Navegue muito**Active Directory do Azure** > **propriedades** e cópia hello ID de diretório. 
* **URL externa** é Olá URL de front-end inserida no hello Proxy de aplicativo. toofind este valor, navegar toohello **proxy de aplicativo** seção do aplicativo de proxy de saudação.
* **ID do aplicativo** de saudação aplicativo nativo pode ser encontrado no hello **propriedades** página do aplicativo nativo hello.
* **Redirecionar URI do aplicativo nativo Olá** podem ser encontradas no hello **URIs de redirecionamento** página do aplicativo nativo hello.


## <a name="see-also"></a>Consulte também

Para obter mais informações sobre o fluxo do aplicativo nativo hello, consulte [tooweb aplicativo nativo API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

Para Olá últimas notícias e atualizações, confira Olá [blog de Proxy de aplicativo](http://blogs.technet.com/b/applicationproxyblog/)
