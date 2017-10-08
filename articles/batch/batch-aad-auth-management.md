---
title: "soluções de gerenciamento de lote de tooauthenticate aaaUse Active Directory do Azure | Microsoft Docs"
description: "Aplicativos criados com o Gerenciador de recursos do Azure e o provedor de recursos de lote Olá autenticar com o AD do Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Autenticar soluções de gerenciamento do lote com o Active Directory

Aplicativos que chamam o serviço de gerenciamento do Azure em lote Olá autenticam com [Active Directory do Azure] [ aad_about] (AD do Azure). O Azure AD é o serviço de gerenciamento de identidade e diretório multilocatário com base em nuvem da Microsoft. Azure próprio usa o Azure AD para autenticação de saudação de seus clientes, os administradores de serviços e usuários organizacionais.

biblioteca de Batch Management .NET Olá expõe tipos para trabalhar com contas em lotes, as chaves de conta, aplicativos e pacotes de aplicativos. biblioteca do Hello Batch Management .NET é um cliente do provedor de recursos do Azure e é usada junto com [do Azure Resource Manager] [ resman_overview] toomanage esses recursos por meio de programação. AD do Azure é necessário tooauthenticate solicitações feitas por meio de qualquer cliente de provedor de recursos do Azure, incluindo a biblioteca de Batch Management .NET Olá e [do Azure Resource Manager][resman_overview].

Neste artigo, vamos explorar usando tooauthenticate do AD do Azure de aplicativos que usam a biblioteca de Batch Management .NET hello. Vamos mostrar como toouse AD do Azure tooauthenticate um administrador de assinatura ou coadministrador, usando autenticação integrada. Usamos Olá [AccountManagment] [ acct_mgmt_sample] projeto de exemplo, disponível no GitHub, toowalk por meio do usando o AD do Azure com biblioteca de Batch Management .NET hello.

toolearn mais sobre como usar a biblioteca de Batch Management .NET hello e exemplo de AccountManagement hello, consulte [cotas com biblioteca de cliente de gerenciamento em lote Olá para .NET e contas em lotes gerenciar](batch-management-dotnet.md).

## <a name="register-your-application-with-azure-ad"></a>Registrar seu aplicativo no Azure AD

Hello Azure [biblioteca de autenticação do Active Directory] [ aad_adal] (ADAL) fornece uma interface programática de tooAzure AD para uso em seus aplicativos. toocall ADAL do seu aplicativo, você deve registrar seu aplicativo em um locatário do AD do Azure. Quando você registra seu aplicativo, você fornecer AD do Azure com informações sobre seu aplicativo, incluindo um nome para ele no locatário do AD do Azure hello. Em seguida, o AD do Azure fornece uma ID de aplicativo que você use tooassociate seu aplicativo com o AD do Azure em tempo de execução. toolearn mais informações sobre a ID do aplicativo hello, consulte [objetos de aplicativo e serviço principal no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

Olá tooregister AccountManagement aplicativo de exemplo, siga as etapas de Olá Olá [adicionar um aplicativo](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) seção [integrando aplicativos com o Active Directory do Azure] [ aad_integrate]. Especifique **aplicativo cliente nativo** para o tipo de saudação do aplicativo. Olá setor URI de OAuth 2.0 padrão para Olá **URI de redirecionamento** é `urn:ietf:wg:oauth:2.0:oob`. No entanto, você pode especificar qualquer URI válido (como `http://myaccountmanagementsample`) para Olá **URI de redirecionamento**, pois ele não precisa toobe um ponto de extremidade real:

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

Depois de concluir o processo de registro Olá, você ver a ID do aplicativo hello e Olá ID de objeto (entidade de serviço) listado para seu aplicativo.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Conceder ao aplicativo de tooyour de acesso de API do Gerenciador de recursos do Azure Olá

Em seguida, você precisará toodelegate acesso tooyour aplicativo toohello API do Gerenciador de recursos do Azure. Identificador de saudação do AD do Azure para Olá API do Gerenciador de recursos é **API de gerenciamento de serviço do Windows Azure**.

Siga estas etapas no hello portal do Azure:

1. No painel de navegação do lado esquerdo de saudação do Olá portal do Azure, escolha **mais serviços**, clique em **registros do aplicativo**e clique em **adicionar**.
2. Pesquisar por nome de saudação do seu aplicativo na lista de saudação de registros do aplicativo:

    ![Procure o nome do aplicativo](./media/batch-aad-auth-management/search-app-registration.png)

3. Saudação de exibição **configurações** folha. Em Olá **acesso à API** seção, selecione **as permissões necessárias**.
4. Clique em **adicionar** tooadd uma nova permissão necessária. 
5. Na etapa 1, digite **API de gerenciamento de serviço do Windows Azure**, selecione essa API Olá lista de resultados e clique Olá **selecione** botão.
6. Na etapa 2, selecione Olá caixa de seleção próxima muito**modelo de implantação clássico do Azure de acesso como usuários da organização**e clique em Olá **selecione** botão.
7. Clique em Olá **feito** botão.

Olá **permissões necessárias** folha agora mostra que o aplicativo de tooyour permissões são concedidas tooboth Olá ADAL e APIs do Gerenciador de recursos. Permissões são concedidas tooADAL por padrão, quando você primeiro registra seu aplicativo com o Azure AD.

![Delegar permissões toohello API do Gerenciador de recursos do Azure](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Pontos de extremidade do Azure AD

tooauthenticate suas soluções de gerenciamento em lote com o AD do Azure, você precisará de dois pontos de extremidade bem conhecidos.

- Olá **ponto de extremidade comum do AD do Azure** fornece uma credencial genérica coletar interface quando um locatário específico não for fornecido, como no caso de saudação da autenticação integrada do:

    `https://login.microsoftonline.com/common`

- Olá **ponto de extremidade do Azure Resource Manager** é tooacquire usado um token para autenticar o serviço de gerenciamento de lote de toohello solicitações:

    `https://management.core.windows.net/`

Olá AccountManagement aplicativo de exemplo define constantes para esses pontos de extremidade. Deixe essas constantes inalterados:

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>Consultar a ID do aplicativo 

O aplicativo cliente usa Olá aplicativo ID (também chamado tooas Olá ID do cliente) tooaccess AD do Azure em tempo de execução. Depois de registrar seu aplicativo no portal do Azure de saudação, atualize sua ID de aplicativo do código toouse Olá fornecido pelo AD do Azure para seu aplicativo registrado. Em Olá AccountManagement aplicativo de exemplo, copie a ID do aplicativo de constante apropriada do hello toohello portal do Azure:

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
Também copie o URI que você especificou durante o processo de registro de saudação de redirecionamento de saudação. Olá redirecionar URI especificado em seu código deve coincidir com a URI que você forneceu ao registrar o aplicativo hello de redirecionamento de saudação.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Adquirir um token de autenticação do Azure AD

Depois que você registrar o exemplo de AccountManagement hello no locatário do AD do Azure hello e atualize o código-fonte exemplo hello com seus valores, o exemplo hello é pronto tooauthenticate usando o Azure AD. Quando você executar o exemplo hello, Olá ADAL tenta tooacquire um token de autenticação. Nesta etapa, ele solicitará suas credenciais da Microsoft: 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

Depois de fornecer suas credenciais, o aplicativo de exemplo hello poderá tooissue autenticado solicitações toohello serviço de gerenciamento de lote. 

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como executar Olá [aplicativo de exemplo AccountManagement][acct_mgmt_sample], consulte [contas de lote de gerenciar e cotas com biblioteca de cliente de gerenciamento em lote Olá para .NET](batch-management-dotnet.md).

toolearn mais sobre o AD do Azure, consulte Olá [documentação do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/). Os exemplos mais detalhados mostrando como toouse ADAL estão disponíveis no hello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteca.

aplicativos de serviço de lote tooauthenticate usando o AD do Azure, consulte [soluções de serviço de lote autenticar com o Active Directory](batch-aad-auth.md). 


[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
