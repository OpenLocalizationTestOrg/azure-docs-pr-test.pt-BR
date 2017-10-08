---
title: aaaAuthenticate com APIs de REST do Mobile Engagement
description: Descreve como tooauthenticate com APIs de REST do Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Autenticar com APIs REST do Mobile Engagement
## <a name="overview"></a>Visão geral
Este documento descreve como tooget um Oauth válida do AAD token tooauthenticate com hello APIs de REST do Mobile Engagement. 

Supõe-se que você tenha uma assinatura válida do Azure e criou um aplicativo do Mobile Engagement usando um dos nossos [Tutoriais de Desenvolvedor](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="authentication"></a>Autenticação
Um token OAuth baseado no Microsoft Azure Active Directory é usado para autenticação. 

Tooauthentication uma API de pedido, um cabeçalho de autorização deve ser adicionado solicitação tooevery que é de saudação formulário a seguir:

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Tokens de Azure Active Directory expiram em 1 hora.
> 
> 

Há tooget de várias maneiras de um token. Já que Olá que APIs geralmente são chamados de um serviço de nuvem, você deseja toouse uma chave de API. Uma chave de API na terminologia do Azure é chamada de senha de uma entidade de serviço. Olá, procedimento a seguir descreve uma maneira toosetting-up manualmente.

### <a name="one-time-setup-using-script"></a>Configuração única (usando script)
Você deve seguir o conjunto de instruções abaixo da configuração de saudação tooperform usando um script do PowerShell que demora Olá mínimo para a instalação, mas usa padrões mais permitidos Olá de saudação. Opcionalmente, você também pode seguir as instruções de Olá Olá [configuração manual](mobile-engagement-api-authentication-manual.md) para fazer isso da saudação diretamente o portal do Azure e configuração mais refinada. 

1. Obter versão mais recente de saudação do Azure PowerShell de [aqui](http://aka.ms/webpi-azps). Para obter mais informações sobre as instruções de download do hello, você poderá ver isso [link](/powershell/azure/overview).  
2. Depois de instalar o Azure PowerShell, use a seguir Olá comandos tooensure que você tenha Olá **do módulo Azure** instalado:
   
    a. Verifique se o módulo do PowerShell do Azure hello está disponível na lista de saudação de módulos disponíveis. 
   
        Get-Module –ListAvailable 
   
    ![Módulos do Azure disponíveis][1]
   
    b. Se você não encontrar módulo do PowerShell do Azure Olá Olá acima da lista, em seguida, é necessário a seguir Olá toorun:
   
        Import-Module Azure 
3. Toohello de logon do Azure Resource Manager do PowerShell executando Olá o comando a seguir e fornecendo seu nome de usuário e senha para sua conta do Azure: 
   
        Login-AzureRmAccount
4. Se você tiver várias assinaturas, em seguida, você deve executar o seguinte hello:
   
    a. Obter uma lista de todas as suas assinaturas e Olá cópia SubscriptionId de assinatura Olá que deseja toouse. Verifique se esta assinatura está Olá mesmo um que possua Olá aplicativo móvel do contrato que você toointeract com usando Olá APIs. 
   
        Get-AzureRmSubscription
   
    b. Comando a seguir de execução Olá os toobe de assinatura de saudação da tooconfigure do SubscriptionId Olá fornecendo usado.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Copiar texto de saudação de saudação [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) máquina local tooyour de script e salve-o como um cmdlet do PowerShell (por exemplo, `APIAuth.ps1`) e execute-o `.\APIAuth.ps1`. 
6. Olá script solicitará que você tooprovide uma entrada para **principalName**. Forneça um nome adequado aqui que você deseja toouse toocreate seu aplicativo do Active Directory (por exemplo, APIAuth). 
7. Após a conclusão do script hello, ele exibirá Olá seguintes quatro valores que você precisará tooauthenticate programaticamente com o AD, portanto, certifique-se de que toocopy-los. 
   
    **TenantId**, **SubscriptionId**, **ApplicationId** e **Secret**.
   
    Use o TenantId como `{TENANT_ID}`, o ApplicationId como `{CLIENT_ID}` e o Secret como `{CLIENT_SECRET}`.
   
   > [!NOTE]
   > A política de segurança padrão pode impedir a execução de scripts do PowerShell. Nesse caso, configure temporariamente a execução do script execução política tooallow usando Olá comando a seguir:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. Aqui está como conjunto de saudação de cmdlets do PS seria semelhante. 
   
    ![][3]
9. Verifique no portal de gerenciamento do Azure de saudação que um novo aplicativo do AD foi criado com o nome da saudação você fornecido toohello script chamado **principalName** em **Mostrar aplicativos que minha empresa possui**.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>Etapas tooget um token válido
1. Chamar a API de saudação com hello parâmetros a seguir e certifique-se de que tooreplace Olá LOCATÁRIO\_ID, o cliente\_ID e o cliente\_segredo:
   
   * **URL da solicitação** como *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*
   * **Cabeçalho HTTP Content-Type** : *application/x-www-form-urlencoded*
   * **Corpo da Solicitação HTTP** como *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     a seguir Olá é um exemplo de solicitação:
     
       POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     Aqui está um exemplo de resposta:
     
       HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234
     
       {"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}
     
     Este exemplo incluído a codificação de URL de parâmetros de POSTAGEM Olá, `resource` valor é realmente `https://management.core.windows.net/`. Tenha cuidado de codificação de URL tooalso `{CLIENT_SECRET}` pois ele pode conter caracteres especiais.
     
     > [!NOTE]
     > Para testar, é possível usar uma ferramenta de cliente HTTP como o [Fiddler](http://www.telerik.com/fiddler) ou a [extensão Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) 
     > 
     > 
2. Agora em cada chamada de API, cabeçalho de solicitação de autorização Olá incluem:
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    Se você receber um código de 401 status retornado, verificação de corpo de resposta hello, ele pode informar Olá token tiver expirado. Nesse caso, obtenha um novo token.

## <a name="using-hello-apis"></a>Usando APIs de saudação
Agora que você tem um token válido, você está pronto toomake Olá API chamadas.

1. Cada solicitação de API, você precisará toopass um token válido, ainda que você obteve na seção anterior hello.
2. Você precisará tooplug em alguns parâmetros na solicitação Olá URI que identifica seu aplicativo. URI de solicitação Olá semelhante ao seguinte Olá
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    parâmetros de saudação tooget, clique no nome do seu aplicativo e clique em Painel de controle e você verá uma página como a seguir Olá com todos os Olá 3 parâmetros.
   
   * **1** `{subscription-id}`
   * **2** `{app-collection}`
   * **3** `{app-resource-name}`
   * **4** nome de seu grupo de recursos será toobe **MobileEngagement** , a menos que você criou um novo. 
     
     ![Parâmetros de URI da API do Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. Ignorar Olá API raiz endereço como era para Olá APIs anteriores.<br/>
> 2. Se você criou o aplicativo hello usando o portal clássico do Azure, em seguida, você precisa de nome de recurso de aplicativo de Olá toouse que é diferente do nome de aplicativo hello em si. Se você criou o aplicativo hello no hello Portal do Azure, em seguida, você deve usar Olá nome do aplicativo em si (não há nenhuma diferenciação entre o nome de recurso do aplicativo e o nome do aplicativo para aplicativos criados no novo portal de saudação).  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



