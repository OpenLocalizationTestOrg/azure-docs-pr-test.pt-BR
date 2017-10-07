---
title: "Autenticação do usuário final: Data Lake Store com o Azure Active Directory | Microsoft Docs"
description: "Saiba como autenticação de usuário final tooachieve com repositório Data Lake usando o Active Directory do Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Autenticação do usuário final com o Data Lake Store usando o Azure Active Directory
> [!div class="op_single_selector"]
> * [Autenticação serviço a serviço](data-lake-store-authenticate-using-active-directory.md)
> * [Autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

O Azure Data Lake Store usa o Azure Active Directory para autenticação. Antes de criar um aplicativo que funciona com repositório Azure Data Lake ou análise Azure Data Lake, primeiro você deve decidir como você gostaria que tooauthenticate seu aplicativo com o Azure Active Directory (AD do Azure). Olá duas opções principais disponíveis são:

* Autenticação do usuário final (este artigo)
* Autenticação serviço a serviço

Ambas as opções resultam em seu aplicativo que está sendo fornecido com um token de OAuth 2.0, que obtém tooeach anexado solicitação feita tooAzure repositório Data Lake ou análise Azure Data Lake.

Este artigo descreve como criar um **aplicativo nativo do Azure AD para autenticação do usuário final**. Para obter instruções sobre a configuração de aplicativo do Azure AD para autenticação serviço a serviço, consulte [Autenticação serviço a serviço com o Data Lake Store usando o Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Pré-requisitos
* Uma assinatura do Azure. Consulte [Obter a avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* A ID de sua assinatura. Você pode recuperá-lo da saudação Portal do Azure. Por exemplo, está disponível na folha de conta do repositório Data Lake hello.
  
    ![Obter ID da assinatura](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* O nome de domínio do Azure AD. Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá Portal do Azure. De saudação captura de tela abaixo, o nome de domínio de saudação é **contoso.onmicrosoft.com**, e Olá GUID entre colchetes é a ID de locatário hello. 
  
    ![Obter domínio do AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Autenticação do usuário final
Isso é hello abordagem recomendada se você quiser um toolog do usuário final no aplicativo tooyour por meio do AD do Azure. Seu aplicativo será capaz de tooaccess recursos do Azure com hello mesmo nível de acesso do usuário final Olá que fez logon. O usuário final precisará tooprovide suas credenciais periodicamente para seu aplicativo toomaintain o acesso.

resultantes de saudação do login do usuário final de saudação é que o aplicativo recebe um token de acesso e um token de atualização. token de acesso de saudação obtém tooeach anexado solicitação feita tooData Lake repositório ou análise Data Lake e é válido para uma hora, por padrão. o token de atualização Olá pode ser usado tooobtain um novo token de acesso e é válido para o semanas tootwo por padrão, se usado regularmente. Você pode usar duas abordagens diferentes para o logon do usuário final.

### <a name="using-hello-oauth-20-pop-up"></a>Usando a janela pop-up de saudação OAuth 2.0
Seu aplicativo pode disparar um OAuth 2.0 autorização pop-up, no qual Olá pelos usuários finais podem digitar suas credenciais. Essa janela pop-up também funciona com o processo de autenticação do Azure AD de dois fatores (2FA) hello, se necessário. 

> [!NOTE]
> Este método ainda não é suportado em saudação do Azure AD Authentication Library (ADAL) para Python ou Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Transmitindo credenciais do usuário diretamente
Seu aplicativo diretamente pode fornecer credenciais de usuário tooAzure AD. Esse método só funciona com contas de usuário de IDs organizacionais. Ele não é compatível com contas de usuário "live ID"/pessoais, incluindo as terminadas em @outlook.com ou @live.com. Além disso, esse método não é compatível com contas de usuário que requerem autenticação do Azure AD de dois fatores (2FA).

### <a name="what-do-i-need-toouse-this-approach"></a>O que eu preciso toouse essa abordagem?
* Nome de domínio do Azure AD. Isso já está listado no pré-requisito Olá deste artigo.
* **Aplicativo nativo** do Azure AD
* ID do aplicativo para o aplicativo nativo de saudação do AD do Azure
* URI de redirecionamento para Olá aplicativo nativo do AD do Azure
* Definir permissões delegadas


## <a name="step-1-create-an-active-directory-native-application"></a>Etapa 1: Criar um aplicativo nativo do Active Directory

Crie e configure um aplicativo nativo do Azure AD para autenticação do usuário final com o Azure Data Lake Store usando o Azure Active Directory. Para obter instruções, consulte [Criar um aplicativo do Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Ao seguir as instruções Olá Olá acima link, certifique-se de selecionar **nativo** para tipo de aplicativo, conforme mostrado na captura de tela de saudação abaixo.

![Criar aplicativo Web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Criar aplicativo nativo")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Etapa 2: Obter a ID do aplicativo e URI de redirecionamento

Consulte [obter ID do aplicativo hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve Olá id de aplicativo (também chamado de ID de saudação do cliente no portal clássico do Azure de saudação) do aplicativo nativo de saudação do AD do Azure.

Olá tooretrieve URI de redirecionamento, execute as etapas de saudação abaixo.

1. Olá Portal do Azure, selecione **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, localize e clique em aplicativo nativo de saudação do AD do Azure que você acabou de criar.

2. De saudação **configurações** folha para o aplicativo hello, clique em **URIs de redirecionamento**.

    ![Obter URI de redirecionamento](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Copie o valor de saudação exibida.


## <a name="step-3-set-permissions"></a>Etapa 3: Definir permissões

1. Olá Portal do Azure, selecione **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, localize e clique em aplicativo nativo de saudação do AD do Azure que você acabou de criar.

2. De saudação **configurações** folha para o aplicativo hello, clique em **as permissões necessárias**e, em seguida, clique em **adicionar**.

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. Em Olá **adicionar o acesso à API** folha, clique em **selecionar uma API**, clique em **Azure Data Lake**e, em seguida, clique em **selecione**.

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  Em Olá **adicionar o acesso à API** folha, clique em **selecionar permissões**, selecione Olá toogive da caixa de seleção **completo acessar o repositório de Lake tooData**e, em seguida, clique em **selecionar **.

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Clique em **Concluído**.

5. Olá repetir último duas etapas permissões toogrant para **API de gerenciamento de serviço do Windows Azure** também.
   
## <a name="next-steps"></a>Próximas etapas
Neste artigo, você criou um aplicativo nativo do AD do Azure e coletadas informações Olá que necessárias em seus aplicativos cliente que você cria usando o SDK do .NET, Java SDK, API REST, etc. Você pode continuar toohello artigos que falar sobre como autenticar toouse Olá AD do Azure web aplicativo toofirst repositório Data Lake e executam outras operações no repositório de saudação a seguir.

* [Introdução ao Repositório Azure Data Lake usando o SDK do .NET](data-lake-store-get-started-net-sdk.md)
* [Introdução ao Azure Data Lake Store usando o SDK do Java](data-lake-store-get-started-java-sdk.md)
* [Introdução ao Azure Data Lake Store usando o REST API](data-lake-store-get-started-rest-api.md)

