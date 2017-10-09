---
title: "Autenticação de serviço a serviço: Data Lake Store com o Azure Active Directory | Microsoft Docs"
description: "Saiba como autenticação de serviço a serviço tooachieve com repositório Data Lake usando o Active Directory do Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Autenticação de serviço a serviço com o Data Lake Store usando o Azure Active Directory
> [!div class="op_single_selector"]
> * [Autenticação serviço a serviço](data-lake-store-authenticate-using-active-directory.md)
> * [Autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

O Azure Data Lake Store usa o Azure Active Directory para autenticação. Antes de criar um aplicativo que funciona com repositório Azure Data Lake ou análise Azure Data Lake, primeiro você deve decidir como você gostaria que tooauthenticate seu aplicativo com o Azure Active Directory (AD do Azure). Olá duas opções principais disponíveis são:

* Autenticação do usuário final 
* Autenticação serviço a serviço (este artigo) 

Ambas as opções resultam em seu aplicativo que está sendo fornecido com um token de OAuth 2.0, que obtém tooeach anexado solicitação feita tooAzure repositório Data Lake ou análise Azure Data Lake.

Este artigo explica como criar um **aplicativo Web do Azure AD para autenticação serviço a serviço**. Para obter instruções sobre a configuração de aplicativo do Azure AD para autenticação de usuário final, consulte [Autenticação de usuário final com o Data Lake Store usando o Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Pré-requisitos
* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Etapa 1: Criar um aplicativo Web do Active Directory

Crie e configure um aplicativo Web do Azure AD para autenticação serviço a serviço com o Azure Data Lake Store usando o Azure Active Directory. Para obter instruções, consulte [Criar um aplicativo do Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Ao seguir as instruções Olá Olá acima link, certifique-se de selecionar **aplicativo Web / API** para tipo de aplicativo, conforme mostrado na captura de tela de saudação abaixo.

![Criar aplicativo Web](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Criar aplicativo Web")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Etapa 2: Obter a id do aplicativo, a chave de autenticação e a id de locatário
Ao fazer logon por meio de programação, é necessário id Olá para seu aplicativo. Se o aplicativo hello compatível com suas próprias credenciais, você também precisará uma chave de autenticação.

* Para obter instruções sobre como ID do aplicativo hello tooretrieve e autenticação de chave (também segredo de cliente chamado hello) para seu aplicativo, consulte [chave de autenticação e a ID do aplicativo Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Para obter instruções sobre como tooretrieve Olá ID de locatário, consulte [obter ID de locatário](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Etapa 3: Atribuir pasta (apenas para autenticação de serviços) ou o arquivo da conta do repositório Azure Data Lake aplicativo toohello Olá AD do Azure
1. Logon toohello novo [portal do Azure](https://portal.azure.com) e abra a conta do repositório Azure Data Lake Olá que você deseja tooassociate com hello aplicativo do Active Directory do Azure criado anteriormente.
2. Na folha de sua conta do Repositório Data Lake, clique em **Gerenciador de Dados**.
   
    ![Crie diretórios na conta do Data Lake Store](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "criar diretórios na conta Data Lake")
3. Em Olá **Data Explorer** folha, clique em arquivo hello ou pasta para o qual você deseja tooprovide acesso toohello AD do Azure aplicativo e, em seguida, clique em **acesso**. arquivo de tooa de acesso tooconfigure, você deve clicar em **acesso** de saudação **a visualização de arquivo** folha.
   
    ![Configurar ACLs no sistema de arquivos do Data Lake](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "definir ACLs no sistema de arquivos do Data Lake")
4. Olá **acesso** folha lista padrão de acesso a saudação e acesso personalizado já atribuído toohello raiz. Clique em Olá **adicionar** nível personalizado de ícone tooadd ACLs.
   
    ![Lista de acesso padrão e personalizado](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "lista de acesso padrão e personalizado")
5. Clique em Olá **adicionar** saudação do ícone tooopen **adicionar personalizado acesso** folha. Nessa folha, clique em **Selecionar usuário ou grupo**e, em seguida, em **Selecionar usuário ou grupo** folha, procure o aplicativo do Active Directory do Azure hello criado anteriormente. Se você tiver muitos grupos toosearch do, use a caixa de texto de saudação em toofilter superior de Olá Olá pelo nome de grupo. Clique em Olá grupo você deseja tooadd e, em seguida, clique em **selecione**.
   
    ![Adicionar um grupo](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Adicionar um grupo")
6. Clique em **selecionar permissões**, selecione permissões hello e se você deseja que as permissões de saudação tooassign como uma ACL padrão, para acessar a ACL, ou ambos. Clique em **OK**.
   
    ![Atribuir permissões toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "atribuir permissões toogroup")
   
    Para obter mais informações sobre permissões no Data Lake Store e ACLs de acesso/padrão, consulte [Controle de acesso no Data Lake Store](data-lake-store-access-control.md).
7. Em Olá **adicionar personalizado acesso** folha, clique em **Okey**. Olá recém-adicionado grupo com permissões de saudação associada, agora será listado no hello **acesso** folha.
   
    ![Atribuir permissões toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "atribuir permissões toogroup")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>Etapa 4: Obter ponto de extremidade token do OAuth 2.0 hello (somente para aplicativos baseados em Java)

1. Logon toohello novo [portal do Azure](https://portal.azure.com) e clique em Active Directory no painel esquerdo da saudação.

2. No painel esquerdo do hello, clique em **registros do aplicativo**.

3. Da parte superior de saudação da folha de registros do aplicativo hello, clique em **pontos de extremidade**.

    ![Ponto de extremidade de token OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "Ponto de extremidade de token OAuth")

4. Na lista de saudação de pontos de extremidade, copie o ponto de extremidade token Olá OAuth 2.0.

    ![Ponto de extremidade de token OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "Ponto de extremidade de token OAuth")   

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você criou um aplicativo da web do AD do Azure e coletadas informações Olá necessárias em seus aplicativos cliente que você cria usando o SDK do .NET, Java SDK, etc. Você pode continuar toohello artigos que falar sobre como autenticar toouse Olá AD do Azure web aplicativo toofirst repositório Data Lake e executam outras operações no repositório de saudação a seguir.

* [Introdução ao Repositório Azure Data Lake usando o SDK do .NET](data-lake-store-get-started-net-sdk.md)
* [Introdução ao Azure Data Lake Store usando o SDK do Java](data-lake-store-get-started-java-sdk.md)

Este artigo percorrido você Olá etapas básicas necessárias tooget um usuário principal para cima e em execução para o seu aplicativo. Você pode examinar Olá informações adicionais de tooget artigos a seguir:
* [Usar a entidade de serviço do PowerShell toocreate](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Usar autenticação de certificado para autenticação de entidade de serviço](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [TooAzure de tooauthenticate outros métodos AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


