---
title: "aaaConfigure autenticação e autorização para um aplicativo personalizado que chama hello Azure tempo série Insights API | Microsoft Docs"
description: "Este tutorial explica como tooconfigure autenticação e autorização para um aplicativo personalizado que chama hello Azure tempo série Insights API"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Autenticação e autorização para API do Azure Time Series Insights

Este artigo explica como tooconfigure um aplicativo personalizado que chama hello Azure tempo série Insights API.

## <a name="service-principal"></a>Entidade de serviço

Esta seção explica como tooconfigure tooaccess um aplicativo hello tempo série Insights API em nome do aplicativo hello. aplicativo Hello pode, em seguida, consultar dados ou publicar dados de referência no ambiente de informações da série de tempo Olá com as credenciais do aplicativo e não as credenciais do usuário hello.

Quando você tiver um aplicativo que necessite tooaccess Insights de série de tempo, você deve configurar um aplicativo do Active Directory do Azure e atribuir políticas de acesso de dados Olá no ambiente de informações da série de tempo de saudação. Essa abordagem é preferível toorunning Olá aplicativo com suas próprias credenciais, porque:

* Você pode atribuir permissões de identidade de aplicativo toohello que são diferentes das suas próprias permissões. Normalmente, essas permissões são restrito tooexactly toodo precisa de qual aplicativo hello. Por exemplo, você pode permitir Olá aplicativo tooonly ler dados em um ambiente de informações da série de tempo específico.
* Você não tem credenciais do aplicativo de saudação toochange se alterar suas responsabilidades.
* Quando você estiver executando um script autônomo, você pode usar um certificado ou uma autenticação de chave tooautomate do aplicativo.

Este artigo mostra como tooperform aqueles percorre Olá portal do Azure. Ele se concentra em um aplicativo de único locatário em que o aplicativo hello é pretendido toorun em uma só organização. Você normalmente usa os aplicativos com um único locatário para os aplicativos da linha de negócios executados em sua organização.

fluxo de instalação Olá consiste em três etapas de alto nível:

1. Criar um aplicativo no Azure Active Directory.
2. Autorize este ambiente do aplicativo tooaccess Olá Insights de série de tempo.
3. Usar identificação do aplicativo hello e toohello um token de chave tooacquire `"https://api.timeseries.azure.com/"` audiência ou recurso. token Hello, em seguida, pode ser usado toocall Olá tempo série Insights API.

Aqui estão as etapas detalhadas de hello:

1. No portal do Azure de Olá, selecione **Active Directory do Azure** > **registros do aplicativo** > **novo registro de aplicativo**.

   ![Novo registro do aplicativo no Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Dê o aplicativo hello um toobe de tipo de nome, selecione Olá **aplicativo Web / API**, selecione qualquer URI válido para **URL de logon**e clique em **criar**.

   ![Criar o aplicativo hello no Active Directory do Azure](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Selecione seu aplicativo recém-criado e copie seu editor de texto favorito de tooyour de ID do aplicativo.

   ![Copie a ID do aplicativo hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Selecione **chaves**, insira o nome da chave hello, expiração Olá select e clique em **salvar**.

   ![Selecione as chaves do aplicativo](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Insira o nome de chave de saudação e expiração e clique em Salvar](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Copie o editor de texto favorito Olá tooyour chave.

   ![Copie a chave de aplicativo hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Para o ambiente de tempo série Insights hello, selecione **políticas de acesso de dados** e clique em **adicionar**.

   ![Adicionar novos dados acesso política toohello Insights de série de tempo ambiente](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. Em Olá **Selecionar usuário** caixa de diálogo, o nome do aplicativo hello Colar (da etapa 2) ou o ID do aplicativo (da etapa 3).

   ![Localizar um aplicativo na caixa de diálogo Selecionar usuário Olá](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Função hello Select (**leitor** para consultar dados, **Colaborador** para consultar dados e alterar dados de referência) e clique em **Okey**.

   ![Escolha o leitor ou colaborador na caixa de diálogo Selecionar função hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Salvar política Olá clicando **Okey**.

10. Usar Olá ID do aplicativo (da etapa 3) e o token de saudação do aplicativo tooacquire chave (da etapa 5) em nome do aplicativo hello. Olá token pode ser passado em Olá `Authorization` cabeçalho quando chamadas de aplicativo Olá Olá tempo série Insights API.

    Se você estiver usando c#, você pode usar Olá token de saudação do código tooacquire em nome do aplicativo hello a seguir. Para obter um exemplo completo, consulte [Consultar dados usando o C#](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Próximas etapas

Use o ID de aplicativo hello e a chave em seu aplicativo. Para exemplo de código que chama Olá tempo série Insights API, consulte [consultar dados usando o c#](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>Consulte também

* [API de consulta](/rest/api/time-series-insights/time-series-insights-reference-queryapi) para referência de API de consulta completa Olá
* [Criar um serviço principal no hello portal do Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md)
