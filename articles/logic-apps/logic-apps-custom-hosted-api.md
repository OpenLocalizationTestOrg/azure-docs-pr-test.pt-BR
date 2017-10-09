---
title: "aaaDeploy, chamar e autenticar as APIs da web e APIs REST para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Implantar, autenticar e chamar APIs Web e APIs REST em fluxos de trabalho para integrações do sistema com o Aplicativo Lógico do Azure"
keywords: "APIs Web, APIs REST, conectores, fluxos de trabalho, integrações do sistema, autenticar"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Implantar, chamar e autenticar as APIs personalizadas como conectores para aplicativos lógicos

Depois que você [criar APIs personalizadas](./logic-apps-create-api-app.md) que fornecem toouse ações ou disparadores na lógica de fluxos de trabalho de aplicativos, você deve implantar suas APIs antes de você pode chamá-los. E embora você possa chamar qualquer API de um aplicativo lógico, para obter melhor experiência hello, adicione [Swagger metadados](http://swagger.io/specification/) que descreve as operações e os parâmetros de sua API. Este arquivo Swagger ajuda sua API a funcionar melhor e se integrar aos aplicativos lógicos mais facilmente.

Você pode implantar suas APIs como [aplicativos web](../app-service-web/app-service-web-overview.md), mas considere a implantação de suas APIs como [aplicativos de API](../app-service-api/app-service-api-apps-why-best-platform.md), que pode facilitar o trabalho quando você criar, hospeda e consumir APIs na nuvem hello e no local. Você não tem qualquer código de toochange em suas APIs - apenas implantar seu aplicativo de API de tooan de código. Você pode hospedar suas APIs em [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md), um plataforma-como-um-serviço (PaaS) que oferece uma das maneiras de saudação melhores, mais fácil e mais escalonáveis para API de hospedagem.

chamadas de tooauthenticate de lógica aplicativos tooyour APIs, você pode definir o Azure Active Directory no hello portal do Azure para que você não tenha tooupdate seu código. Ou você pode exigir e aplicar a autenticação por meio do seu código da API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Implantar sua API como um aplicativo Web ou aplicativo de API

Antes de chamar sua API personalizada de um aplicativo lógico, implante sua API como um aplicativo web ou tooAzure do aplicativo de API do serviço de aplicativo. Além disso, a toomake Swagger documento legível por Olá lógica de aplicativo Designer, defina as propriedades de definição de saudação API e ativar [recursos entre origens (CORS) de compartilhamento](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) para seu aplicativo web ou aplicativo de API.

1. No hello portal do Azure, selecione o aplicativo web ou aplicativo de API.

2. Na folha de saudação que é aberta, em **API**, escolha **de definição de API**. Saudação de conjunto **local da definição de API** toohello URL para o arquivo swagger. JSON.

   Geralmente, Olá URL aparece neste formato:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Arquivo de tooSwagger link para sua API personalizada](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. Em **API**, escolha **CORS**. Definir a diretiva de CORS Olá **permitido origens** muito**'*'** (permitir todos os).

   Essa configuração permite solicitações do Designer de Aplicativo Lógico.

   ![Permitir solicitações de API personalizada do Designer de lógica do aplicativo tooyour](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Para obter mais informações, consulte estes artigos:

* [Adicionar metadados do Swagger para APIs Web do ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Implantar tooAzure APIs da web ASP.NET do serviço de aplicativo](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Chamar sua API personalizada de fluxos de trabalho de aplicativo lógico

Depois de configurar propriedades de definição de saudação API e CORS, gatilhos e ações de sua API personalizada deverá ficar disponíveis para você tooinclude no seu fluxo de trabalho do aplicativo de lógica. 

*  tooview Olá sites que tenham URLs Swagger, você pode procurar seus sites de assinatura em Olá lógica do Designer de aplicativos.

*  ações disponíveis tooview e entradas apontando para um documento de Swagger, use Olá [HTTP + Swagger ação](../connectors/connectors-native-http-swagger.md).

*  toocall qualquer API, incluindo aquelas que não têm ou expor um documento de Swagger, você sempre pode criar uma solicitação com hello [ação HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Autenticar chamadas tooyour personalizado API

Você pode proteger chamadas API personalizada do tooyour das seguintes maneiras:

* [Nenhuma alteração de código](#no-code): proteger sua API com [do Azure Active Directory (AD do Azure)](../active-directory/active-directory-whatis.md) por meio de Olá portal do Azure, portanto não tiver tooupdate seu código ou reimplantar sua API.

  > [!NOTE]
  > Por padrão, a autenticação do AD do Azure Olá que ativar Olá portal do Azure não fornece autorização refinada. Por exemplo, essa autenticação bloqueios toojust sua API um locatário específico, não tooa usuário específico ou aplicativo. 

* [Atualizar o código da API](#update-code): proteja sua API impondo a [autenticação de certificado](#certificate), a [autenticação básica](#basic) ou a [autenticação do Azure AD](#azure-ad-code) por meio de código.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Autenticar chamadas tooyour API sem alterar o código

Eis as etapas gerais para este método hello:

1. Crie duas [identidades de aplicativo do Azure AD (Azure Active Directory)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): uma para seu aplicativo lógico e um para seu aplicativo Web (ou aplicativo de API).

2. tooauthenticate tooyour de chamadas API, use credenciais de saudação (ID do cliente e segredo) para Olá [entidade de serviço](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associado Olá identidade de aplicativo do AD do Azure para seu aplicativo lógico.

3. Inclua o aplicativo hello IDs em sua definição de aplicativo de lógica.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Parte 1: Criar uma identidade do aplicativo do Azure AD para seu aplicativo lógico

Sua lógica de aplicativo usa esse tooauthenticate de identidade de aplicativo do AD do Azure no AD do Azure. Você só tem tooset a essa identidade de uma vez para seu diretório. Por exemplo, você pode escolher toouse Olá identidade mesmo para todos os seus aplicativos lógicos, mesmo que você pode criar identidades exclusivas para cada aplicativo lógico. Você pode configurar essas identidades no hello portal do Azure, [portal clássico do Azure](#app-identity-logic-classic), ou use [PowerShell](#powershell).

**Criar identidade de aplicativo hello para seu aplicativo lógica no hello portal do Azure**

1. Em Olá [portal do Azure](https://portal.azure.com "https://portal.azure.com"), escolha **Active Directory do Azure**. 

2. Confirme que você está no hello mesmo diretório que o aplicativo web ou aplicativo de API.

   > [!TIP]
   > tooswitch diretórios, clique em seu perfil e selecione outro diretório. Ou escolha **Visão Geral** > **Mudar diretório**.

3. No menu de diretório hello, em **gerenciar**, escolha **registros do aplicativo** > **novo registro de aplicativo**.

   > [!TIP]
   > Por padrão, a lista de registros do aplicativo hello mostra todos os registros do aplicativo em seu diretório. tooview somente seus registros do aplicativo, próxima toohello caixa de pesquisa, selecione **meus aplicativos**. 

   ![Criar novo registro de aplicativo](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Dê um nome de sua identidade de aplicativo, deixe **tipo de aplicativo** definido muito**aplicativo Web / API**, fornecer uma única cadeia de caracteres formatada como um domínio para **URL de logon**e escolha  **Criar**.

   ![Forneça o nome e a URL de entrada para a identidade do aplicativo](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   identidade de aplicativo Hello que você criou para seu aplicativo lógico agora aparece na lista de registros do aplicativo hello.

   ![Identidade do aplicativo para seu aplicativo lógico](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Na lista de registros do aplicativo hello, selecione sua nova identidade do aplicativo. Copie e salve Olá **ID do aplicativo** toouse como hello "ID do cliente" para seu aplicativo lógica na parte 3.

   ![Copie e salve a ID do aplicativo para o aplicativo lógico](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Se as configurações de identidade do aplicativo não estiverem visíveis, escolha **Configurações** ou **Todas as configurações**.

7. Em **Acesso à API**, escolha **Chaves**. Em **Descrição**, forneça um nome para sua chave. Em **Expira**, selecione uma duração para a chave.

   chave de saudação que você está criando atua como da identidade do aplicativo hello "segredo" ou a senha para seu aplicativo lógico.

   ![Criar chave para identidade de aplicativo lógico](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Na barra de ferramentas hello, escolha **salvar**. Em **Valor**, agora sua chave aparece. 
**Certifique-se de que toocopy e salvar sua chave** para uso posterior porque está oculta chave hello quando você deixa folha chave hello.

   Quando você configura seu aplicativo lógico na parte 3, você especificar essa chave hello "segredo" ou a senha.

   ![Copiar e salvar a chave para mais tarde](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Criar identidade de aplicativo hello para seu aplicativo lógica no hello portal clássico do Azure**

1. Nas Olá portal clássico do Azure, escolha [ **do Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Selecione Olá mesmo diretório que você pode usar para seu aplicativo web ou aplicativo de API.

3. Em Olá **aplicativos** guia, escolha **adicionar** final Olá Olá página.

4. Dê um nome à identidade do aplicativo e escolha **Avançar** (seta para a direita).

5. Em **Propriedades do aplicativo**, forneça uma única cadeia de caracteres formatada como um domínio para **URL de Entrada** e **URI da ID do Aplicativo** e escolha **Concluir** (marca de seleção).

6. Em Olá **configurar** guia, copiar e salvar Olá **ID do cliente** para toouse de aplicativo sua lógica na parte 3.

7. Em **chaves**, abra Olá **selecionar duração** lista. Selecione uma duração para a chave.

   chave de saudação que você está criando atua como da identidade do aplicativo hello "segredo" ou a senha para seu aplicativo lógico.

8. Final Olá Olá página, escolha **salvar**. Você pode ter toowait alguns segundos.

9. Em **chaves**, certifique-se de que toocopy e salvar chave de saudação agora aparece. 

   Quando você configura seu aplicativo lógico na parte 3, você especificar essa chave hello "segredo" ou a senha.

Para obter mais informações, saiba como muito [configurar seu aplicativo de serviço de aplicativo toouse Active Directory do Azure logon](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Criar identidade de aplicativo de saudação para seu aplicativo lógico no PowerShell**

Você pode executar essa tarefa por meio do Azure Resource Manager com o PowerShell. No PowerShell, execute estes comandos:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Verifique se Olá de toocopy **ID de locatário** hello (GUID para seu locatário do AD do Azure), **ID do aplicativo**e a senha de saudação que você usou.

Para obter mais informações, saiba como muito [criar uma entidade de serviço com recursos do PowerShell tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Parte 2: Criar uma identidade do aplicativo do Azure AD para seu aplicativo Web ou aplicativo de API

Se seu aplicativo de API ou um aplicativo web já estiver implantado, pode ativar a autenticação e criar a identidade do aplicativo hello no hello portal do Azure. Caso contrário, você pode [ativar a autenticação quando implantar com um modelo do Azure Resource Manager](#authen-deploy). 

**Criar identidade de aplicativo hello e ativar a autenticação no portal do Azure para aplicativos implantados de saudação**

1. Em Olá [portal do Azure](https://portal.azure.com "https://portal.azure.com"), localize e selecione o aplicativo web ou aplicativo de API. 

2. Em **Configurações**, escolha **Autenticação/Autorização**. Em **Autenticação do Serviço de Aplicativo**, **Ative** a autenticação. Em **Provedores de Autenticação**, escolha **Azure Active Directory**.

   ![Ativar a autenticação](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Agora crie uma identidade do aplicativo para seu aplicativo Web ou aplicativo de API conforme mostrado aqui. Em Olá **configurações do Active Directory do Azure** folha, defina **modo de gerenciamento** muito**Express**. Escolha **Criar novo aplicativo do AD**. Dê um nome à identidade do aplicativo e escolha **OK**. 

   ![Criar identidade do aplicativo para seu aplicativo Web ou aplicativo de API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. Em Olá **autenticação / folha de autorização**, escolha **salvar**.

Agora você deve localizar a ID do cliente hello e ID de locatário para a identidade de aplicativo hello associada com o aplicativo web ou aplicativo de API. Você usará essas IDs na Parte 3. Para continuar com estas etapas para Olá portal do Azure ou [portal clássico do Azure](#find-id-classic).

**Localizar a ID do cliente da identidade do aplicativo e a ID do locatário para seu aplicativo web ou aplicativo de API no hello portal do Azure**

1. Em **Provedores de Autenticação**, escolha **Azure Active Directory**. 

   ![Escolha "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. Em Olá **configurações do Active Directory do Azure** folha, defina **modo de gerenciamento** muito**avançado**.

3. Saudação de cópia **ID do cliente**e salve o GUID para uso na parte 3.

   > [!TIP] 
   > Se **ID do cliente** e **Url do emissor** não aparecer, tente atualizar Olá portal do Azure e repita a etapa 1.

4. Em **Url do emissor**, copiar e salvar apenas hello GUID para a parte 3. Você também pode usar esse GUID no modelo de implantação do aplicativo Web ou aplicativo de API, se necessário.

   Esse GUID é GUID específico do locatário ("ID de locatário") e deve aparecer nessa URL: `https://sts.windows.net/{GUID}`

5. Sem salvar as alterações, fechar Olá **configurações do Active Directory do Azure** folha.

<a name="find-id-classic"></a>

**Localizar a ID do cliente da identidade do aplicativo e ID de locatário para seu aplicativo web ou aplicativo de API no hello portal clássico do Azure**

1. Nas Olá portal clássico do Azure, escolha [ **do Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Selecione o diretório de saudação que você pode usar para seu aplicativo web ou aplicativo de API.

3. Em Olá **pesquisa** , localize e selecione a identidade de aplicativo hello para seu aplicativo web ou aplicativo de API.

4. Em Olá **configurar** guia, Olá cópia **ID do cliente**e salve o GUID para uso na parte 3.

5. Depois de obter a ID do cliente hello, na parte inferior de saudação do hello **configurar** guia, escolha **exibir pontos de extremidade**.

6. Copiar URL Olá **documento de metadados de Federação**e procurar toothat URL.

7. No documento de metadados de saudação é aberto, localize a raiz de saudação **EntityDescriptor ID** elemento que tem um **entityID** atributo neste formulário:`https://sts.windows.net/{GUID}` 

      Olá GUID nesse atributo é GUID específico do locatário (ID do Locatário).

8. Copie a ID de locatário hello e salve essa ID para uso na parte 3 e também toouse em seu aplicativo web ou o modelo de implantação do aplicativo de API, se necessário.

Para saber mais, consulte esses tópicos:

* [Autenticação de usuário para Aplicativos de API no Serviço de Aplicativo do Azure](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Autenticação e autorização no Serviço de Aplicativo do Azure](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Ativar a autenticação quando implantar com um modelo do Azure Resource Manager**

Você ainda deve criar uma identidade de aplicativo do AD do Azure para seu aplicativo web ou aplicativo de API que é diferente de identidade de aplicativo hello para seu aplicativo lógico. identidade do aplicativo hello toocreate, siga Olá anterior etapas na parte 2 para Olá portal do Azure. Você também pode siga etapas Olá na parte 1, mas verifique toouse-se de que seu aplicativo web ou aplicativo de API real `https://{URL}` para **URL de logon** e **URI da ID do aplicativo**. Essas etapas, você tem toosave ambos os computadores cliente Olá ID e a ID de locatário para uso no modelo de implantação do aplicativo e também para a parte 3.

> [!NOTE]
> Quando você cria a identidade de aplicativo de saudação do AD do Azure para seu aplicativo web ou aplicativo de API, você deve usar o hello portal do Azure ou portal clássico do Azure, em vez de PowerShell. Olá PowerShell commandlet não configurar permissões de saudação necessária toosign usuários em um site.

Depois de obter a ID do cliente hello e ID de locatário, inclua essas IDs como um subresource do seu aplicativo web ou aplicativo de API em seu modelo de implantação:

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically implantar um aplicativo da web em branco e um aplicativo de lógica junto com a autenticação do Active Directory do Azure, [exibição Olá modelo completa aqui](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), ou clique em **implantar tooAzure** aqui:

[![Implantar tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>Parte 3: Preencher a seção de autorização de saudação em seu aplicativo de lógica

modelo anterior Olá já tem essa seção de autorização configurar, mas se estiver criando Olá lógica aplicativo diretamente, você deve incluir a seção de autorização total de saudação.

Abrir sua definição lógica do aplicativo no modo de exibição de código, vá toohello **HTTP** seção de ação, localizar Olá **autorização** seção e inclua esta linha:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Elemento | Descrição |
| ------- | ----------- |
| locatário |Olá GUID para o locatário de saudação do AD do Azure |
| audiência |Obrigatório. Olá GUID do recurso de destino Olá que você deseja tooaccess - Olá ID do cliente de identidade de aplicativo hello para seu aplicativo web ou aplicativo de API |
| clientId |Olá GUID para o cliente Olá solicitando acesso - Olá ID do cliente de identidade de aplicativo hello para seu aplicativo de lógica |
| segredo |Obrigatório. chave de saudação ou a senha de identidade de aplicativo hello para cliente Olá que está solicitando o token de acesso de saudação |
| type |tipo de autenticação de saudação. Para autenticação do ActiveDirectoryOAuth, o valor de saudação é `ActiveDirectoryOAuth`. |

Por exemplo:

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Proteger chamadas à API por meio de código

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Autenticação de certificado

toovalidate Olá solicitações de entrada do seu aplicativo de lógica de tooyour aplicativo web ou aplicativo de API, você pode usar certificados de cliente. Saiba tooset seu código, [como autenticação mútua de TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

Em Olá **autorização** seção, inclua esta linha: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Elemento | Descrição |
| ------- | ----------- |
| type |Obrigatório. tipo de autenticação de saudação. Para certificados de cliente SSL, o valor de saudação deve ser `ClientCertificate`. |
| Senha |Obrigatório. senha de saudação para acessar o certificado de cliente da saudação (arquivo PFX) |
| pfx |Obrigatório. Conteúdo codificado com base64 do certificado de cliente da saudação (arquivo PFX) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Autenticação básica

solicitações de entrada toovalidate do seu aplicativo de lógica de tooyour aplicativo web ou aplicativo de API, você pode usar a autenticação básica, como um nome de usuário e senha. A autenticação básica é um padrão comum, e você pode usar essa autenticação em qualquer idioma usado toobuild seu aplicativo web ou aplicativo de API.

Em Olá **autorização** seção, inclua esta linha:

`{"type": "basic", "username": "username", "password": "password"}`.

| Elemento | Descrição |
| --- | --- |
| type |Obrigatório. tipo de autenticação de saudação. Para a autenticação básica, o valor de saudação deve ser `Basic`. |
| Nome de Usuário |Obrigatório. saudação de nome de usuário para autenticação |
| Senha |Obrigatório. senha de saudação para autenticação |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Autenticação do Azure Active Directory pelo código

Por padrão, a autenticação do AD do Azure Olá que ativar Olá portal do Azure não fornece autorização refinada. Por exemplo, essa autenticação bloqueios toojust sua API um locatário específico, não tooa usuário específico ou aplicativo. 

aplicativo de lógica de tooyour toorestrict API access por meio de código, extrair cabeçalho Olá que tem Olá JSON web token (JWT). Verificar a identidade do chamador hello e rejeitar as solicitações que não correspondem.

Continuar, tooimplement essa autenticação inteiramente em seu próprio código e não use Olá portal do Azure, Aprenda como muito [autenticar com o Active Directory local em seu aplicativo do Azure](../app-service-web/web-sites-authentication-authorization.md).

toocreate uma identidade de aplicativo para seu aplicativo lógico e usar essa identidade toocall sua API, você deve seguir as etapas anteriores hello.

## <a name="next-steps"></a>Próximas etapas

* [Verificar o desempenho do aplicativo lógico com alertas e logs de diagnóstico](logic-apps-monitor-your-logic-apps.md)