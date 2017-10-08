---
title: aaaIntegrating aplicativos com o Active Directory do Azure | Microsoft Docs
description: Obter detalhes sobre como tooadd, atualizar ou remover um aplicativo no Azure Active Directory (AD do Azure).
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Integrando aplicativos com o Active Directory do Azure
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Desenvolvedores de empresas e provedores de software-como um serviço (SaaS) podem desenvolver serviços de nuvem comercial ou de linha de aplicativos de negócios que pode ser integrado ao Active Directory do Azure (AD do Azure) tooprovide segura entrar e autorização para seu serviços. toointegrate um aplicativo ou serviço com o Azure AD, um desenvolvedor deve primeiro registrar detalhes Olá sobre seu aplicativo com o Azure AD por meio de saudação portal clássico do Azure.

Este artigo mostra como tooadd, atualizar ou remover um aplicativo no AD do Azure. Você aprenderá sobre os diferentes tipos de saudação de aplicativos que podem ser integrados ao AD do Azure, como tooconfigure tooaccess seus aplicativos outros recursos, como APIs da web e muito mais.

toolearn mais sobre Olá dois AD do Azure objetos que representam um aplicativo registrado e a relação de saudação entre elas, consulte [objetos Application e entidade de serviço](active-directory-application-objects.md); toolearn mais informações sobre as diretrizes da marca de saudação você deve usar ao desenvolver aplicativos com o Active Directory do Azure, consulte [diretrizes da marca para aplicativos integrados](active-directory-branding-guidelines.md).

## <a name="adding-an-application"></a>Adicionando um aplicativo
Qualquer aplicativo que deseja toouse recursos de saudação do AD do Azure, primeiro deve ser registrado em um locatário do AD do Azure. Esse processo de registro envolve o fornecimento de detalhes do AD do Azure sobre seu aplicativo, como URL Olá onde ele está localizado, Olá URL toosend respostas depois que um usuário é autenticado, Olá URI que identifica o aplicativo hello e assim por diante.

Se você estiver criando um aplicativo web que precisa apenas entrar toosupport para os usuários no AD do Azure, você pode simplesmente seguir instruções de saudação abaixo. Se seu aplicativo precisa de credenciais ou permissões tooaccess tooa web API ou precisa tooallow usuários de outros tooaccess de locatários do AD do Azure, consulte [atualizando um aplicativo](#updating-an-application) toocontinue seção configurar seu aplicativo.

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>um novo aplicativo no portal do Azure de saudação do tooregister
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No painel de navegação esquerdo hello, escolha **mais serviços**, clique em **registros do aplicativo**e clique em **adicionar**.
4. Siga os prompts de saudação e criar um novo aplicativo. Se você desejar exemplos específicos para aplicativos da Web ou aplicativos nativos, confira nossos [inícios rápidos](active-directory-developers-guide.md).
  * Para aplicativos Web, fornecer Olá **URL de logon**, que é Olá a URL base do aplicativo, onde os usuários possam entrar ex `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Para aplicativos nativos, forneça um **URI de redirecionamento**, o AD do Azure usa tooreturn respostas de token. Insira um aplicativo de tooyour específico de valor,. por exemplo`http://MyFirstAADApp`
5. Depois de concluir o registro, o Azure AD atribui seu aplicativo um identificador de cliente exclusivo, Olá ID do aplicativo. Seu aplicativo foi adicionado e você será levado a página de início rápido de toohello para seu aplicativo. Dependendo se o seu aplicativo é uma web ou aplicativo nativo, você verá diferentes opções sobre como aplicativo de tooyour tooadd recursos adicionais. Após a adição de seu aplicativo, você pode começar a atualizar seu toosign de usuários do aplicativo tooenable no acesso APIs da web em outros aplicativos ou configurem aplicativos multilocatário (o que permite que outras organizações tooaccess seu aplicativo).

> [!NOTE]
> Por padrão, o registro do aplicativo hello recém-criado é configurado tooallow usuários toosign seu diretório no aplicativo tooyour.
> 
> 

## <a name="updating-an-application"></a>Atualizando um aplicativo
Quando seu aplicativo tiver sido registrado com o AD do Azure, talvez precise toobe atualizado tooprovide acessar tooweb APIs, ser disponibilizados em outras organizações e muito mais. Esta seção descreve várias formas em que talvez seja necessário tooconfigure ainda mais seu aplicativo. Primeiro vamos começar com uma visão geral da saudação estrutura de consentimento, que é importante toounderstand se você estiver criando aplicativos de API/recursos que serão consumidos por aplicativos cliente criados pelos desenvolvedores da sua organização ou outra organização.

Para obter mais informações sobre Olá autenticação de maneira funciona no AD do Azure, consulte [cenários de autenticação do AD do Azure](active-directory-authentication-scenarios.md).

### <a name="overview-of-hello-consent-framework"></a>Visão geral da estrutura de consentimento Olá
Estrutura de consentimento do AD do Azure torna fácil toodevelop web de vários locatários e os aplicativos cliente nativos que precisam de tooaccess web APIs protegidos por um locatário Azure AD, diferente da saudação um onde o aplicativo de cliente hello é registrado. Essas APIs da web incluem hello Microsoft Graph API (tooaccess Active Directory do Azure, Intune e serviços do Office 365) e APIs de outros serviços da Microsoft, além de tooyour possui APIs da web. estrutura Olá baseia-se em um usuário ou administrador dar consentimento tooan aplicativo que solicita toobe registrado no seu diretório, que pode envolver o acesso a dados do diretório.

Por exemplo, se um aplicativo de cliente da web precisa de informações de calendário tooread sobre o usuário de saudação do Office 365, esse usuário será necessário tooconsent toohello cliente aplicativo. Após o consentimento for dado, aplicativo de cliente hello ser capaz de toocall Olá Microsoft Graph API em nome de usuário de saudação e usar informações de calendário Olá conforme necessário. Olá [Microsoft Graph API](https://graph.microsoft.io) fornece toodata de acesso no Office 365 (como mensagens do Exchange, sites e listas do SharePoint, documentos do OneDrive, blocos de anotações do OneNote, Planner, pastas de trabalho de tarefas e os calendários Excel, etc.), bem como usuários e grupos do AD do Azure e outros objetos de dados de mais serviços de nuvem da Microsoft. 

estrutura de consentimento Olá se baseia no OAuth 2.0 e seus diversos fluxos, como o código de autorização credenciais de cliente e conceda conceder, usando clientes públicos ou confidenciais. Usando o OAuth 2.0, o AD do Azure torna possível toobuild muitos tipos diferentes de aplicativos de cliente, tais como em um telefone, tablet, servidor ou um aplicativo web e obter acesso a recursos toohello necessários.

Para obter mais informações sobre a estrutura de consentimento hello, consulte [OAuth 2.0 no AD do Azure](https://msdn.microsoft.com/library/azure/dn645545.aspx), [cenários de autenticação do AD do Azure](active-directory-authentication-scenarios.md)e para obter informações sobre como obter acesso autorizado tooOffice 365 por meio de O Microsoft Graph, consulte [autenticação do aplicativo com o Microsoft Graph](https://graph.microsoft.io/docs/authorization/auth_overview).

#### <a name="example-of-hello-consent-experience"></a>Exemplo de experiência de consentimento Olá
Olá etapas a seguir mostrará como experiência de consentimento Olá funciona para o desenvolvedor do aplicativo hello e usuário.

1. Na página de configuração de cliente do seu aplicativo web no hello portal do Azure, defina permissões de saudação que requer que seu aplicativo usando os menus de saudação no hello seção permissões necessárias.
   
    ![Permissões tooother aplicativos](./media/active-directory-integrating-applications/requiredpermissions.png)
2. Considere a possibilidade de que as permissões do aplicativo foram atualizadas, executando o aplicativo hello e um usuário é sobre toouse para Olá primeira vez. Se o aplicativo hello ainda não tiver adquirido um aplicativo hello de token, acesso ou atualização precisa tooobtain de ponto de extremidade de autorização toogo tooAzure do AD um código de autorização que pode ser usado tooacquire um novo acesso e token de atualização.
3. Se o usuário Olá não ainda estiver autenticado, serão solicitadas toosign em tooAzure AD.
   
    ![Usuário ou administrador entram no tooAzure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Depois Olá usuário faz logon, o AD do Azure determinará se o usuário Olá precisa toobe mostra uma página de consentimento. Essa decisão depende se usuário hello (ou o administrador de sua organização) já concedeu permissão do aplicativo hello. Se consentimento já não tenha sido concedido, o AD do Azure solicitará o consentimento do usuário hello e Olá necessárias permissões necessárias toofunction serão exibidas. conjunto de saudação de permissões que é exibido na caixa de diálogo de consentimento Olá são Olá mesmo que foi selecionado no permissões delegadas de saudação em Olá portal do Azure.
   
    ![Experiência de consentimento do usuário](./media/active-directory-integrating-applications/consent.png)
5. Depois que o usuário Olá concede permissão, um código de autorização é retornado tooyour aplicativo, que pode ser resgatado tooacquire um token de acesso e token de atualização. Para obter mais informações sobre este fluxo, consulte Olá [web seção do aplicativo tooweb API](active-directory-authentication-scenarios.md#web-application-to-web-api) seção [cenários de autenticação do AD do Azure](active-directory-authentication-scenarios.md).

6. Como administrador, você também pode consentimento permissões delegadas do tooan do aplicativo em nome de todos os usuários de saudação em seu locatário. Isso impedirá a caixa de diálogo de consentimento Olá apareçam para cada usuário no locatário Olá. Você pode fazer isso de saudação [portal do Azure](https://portal.azure.com) de sua página de aplicativo. De saudação **configurações** folha para seu aplicativo, clique em **permissões necessárias** e clique em Olá **conceder permissões** botão. 

    ![Conceda permissões para consentimento explícito de admin](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> Concedendo consentimento explícito usando Olá **conceder permissões** botão é necessário no momento para aplicativos de página única (SPA) usando o ADAL.js, como token de acesso de saudação é solicitado sem um prompt de consentimento, o que irá falhar se o consentimento não é já concedida.   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configurando um cliente aplicativo tooaccess APIs da web
Em ordem para um web/confidencial cliente aplicativo toobe capaz de tooparticipate em um fluxo de concessão de autorização que requer autenticação (e obter um token de acesso), ele deve estabelecer credenciais seguras. método de autenticação padrão Olá Olá portal do Azure com suporte é a ID do cliente + chave simétrica. Esta seção abordará a chave de segredo do Olá Olá configuração etapas tooprovide necessárias credenciais do cliente.

Além disso, antes de um cliente pode acesso uma API da web expostas por um aplicativo de recurso (ou seja: Microsoft Graph API), estrutura de consentimento Olá garantirá cliente Olá obtém Olá permissão grant permissões de saudação necessária, com base no solicitado. Por padrão, todos os aplicativos podem escolher permissões do Active Directory do Azure (Graph API) e API de gerenciamento de serviços do Azure, com a permissão "Habilitar logon e ler perfis dos usuários" hello AD do Azure já selecionada por padrão. Se o aplicativo cliente estiver sendo registrado em um locatário do Azure AD do Office 365, as APIs Web e permissões para o SharePoint e Exchange Online também serão disponibilizadas para seleção. Você pode selecionar [dois tipos de permissões](active-directory-dev-glossary.md#permissions) no hello menus suspensos toohello próximo desejado web API:

* Permissões de aplicativo: O aplicativo cliente precisa tooaccess Olá web API diretamente como em si (nenhum contexto de usuário). Esse tipo de permissão requer o consentimento do administrador e também não está disponível para aplicativos cliente nativos.
* Permissões delegadas: Seu aplicativo cliente precisa tooaccess Olá web API como usuário conectado hello, mas com acesso limitado pela permissão de saudação selecionada. Esse tipo de permissão pode ser concedido por um usuário, a menos que a permissão de saudação é configurada para exigir consentimento do administrador. 

> [!NOTE]
> Adicionar um aplicativo de tooan de permissão delegado não concede automaticamente consentimento toohello usuários dentro do locatário Olá, como no hello Portal clássico do Azure. Olá os usuários devem manualmente dar consentimento para Olá adicionado delegar permissões em tempo de execução, a menos que o administrador de saudação clica Olá **conceder permissões** botão da saudação **permissões necessárias** seção da página de aplicativo hello em Olá portal do Azure. 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>tooadd credenciais ou permissões tooaccess APIs da web
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No menu superior do hello, escolha **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, clique em aplicativo hello deseja tooconfigure. Isso irá levá-lo página de início rápido do aplicativo toohello, bem como abra a folha de configurações Olá para o aplicativo hello.
4. tooadd uma chave secreta para as credenciais do seu aplicativo web, clique em seção de "Chaves" hello da folha de configurações de saudação.  
   
   * Adicionar uma descrição para a sua chave e selecionar 1 ou duração de 2 anos. 
   * coluna da extrema direita de saudação conterá o valor de chave hello, depois de salvar as alterações de configuração de saudação. Ser toocome se volta toothis seção e copie-lo depois que você clicar em Salvar, para que ele para usam em seu aplicativo cliente durante a autenticação em tempo de execução.
5. tooadd permissões tooaccess APIs de recurso de seu cliente, clique em seção de "Permissões necessárias" hello da folha de configurações de saudação. 
   
   * Primeiro, clique o botão de "Adicionar" hello.
   * Clique em "Selecionar uma API" tooselect Olá tipo de recursos que você deseja toopick do.
   * Percorra a lista Olá das APIs disponíveis ou use Olá tooselect de caixa de pesquisa de aplicativos de recurso disponível Olá em seu diretório que expõem uma API da web. Clique Olá recurso você está interessado, clique em **selecione**.
   * Quando selecionada, você pode mover toohello **selecionar permissões** menu, onde você pode selecionar hello "permissões de aplicativo" e "Permissões delegadas" para o seu aplicativo.
   
6. Quando terminar, clique em Olá **feito** botão.

> [!NOTE]
> Olá clicando em **feito** botão também define automaticamente as permissões de saudação para seu aplicativo em seu diretório com base nas permissões de saudação tooother aplicativos que você configurou.  Você pode exibir as permissões do aplicativo examinando o aplicativo hello **configurações** folha.
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configurando um recurso aplicativo tooexpose APIs da web
Você pode desenvolver uma API da web e torná-lo disponível tooclient aplicativos expondo acesso [escopos](active-directory-dev-glossary.md#scopes) e [funções](active-directory-dev-glossary.md#roles). Uma API da web configuradas corretamente é disponibilizada como Olá outra APIs, incluindo Olá Graph API do Microsoft web e Olá APIs do Office 365. Os escopos de acesso são expostos por meio do [manifesto do aplicativo](active-directory-dev-glossary.md#application-manifest), que é um arquivo JSON que representa a configuração de identidade do aplicativo.  

Olá seção a seguir mostrará como escopos tooexpose acesso, modificando o manifesto do aplicativo de recurso hello.

#### <a name="adding-access-scopes-tooyour-resource-application"></a>Adicionar o aplicativo de recurso de tooyour de escopos de acesso
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No menu superior do hello, escolha **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, clique em aplicativo hello deseja tooconfigure. Isso irá levá-lo página de início rápido do aplicativo toohello, bem como abra a folha de configurações Olá para o aplicativo hello.
4. Clique em **manifesto** de saudação página tooopen Olá embutido manifesto editor de aplicativo. 
5. Substitua o nó de "oauth2Permissions" hello trecho JSON a seguir. Este trecho de código é um exemplo de como tooexpose um escopo conhecido como "representação de usuário," que permite uma toogive de proprietário do recurso de um aplicativo cliente um tipo de delegado acesso tooa recursos. Certifique-se de que você alterar valores e o texto de saudação para seu aplicativo:
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    valor de id de saudação deve ser um novo GUID gerado que você cria usando um [ferramenta de geração de GUID](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) ou programaticamente. Representa um identificador exclusivo para a permissão de saudação que é exposto pela API da web hello. Depois que o cliente está configurado adequadamente Olá a API da web do tooyour toorequest acesso e chamadas de API da web, ele apresentará um token de OAuth 2.0 JWT que tem Olá escopo (scp) conjunto toohello valor de declaração acima, que nesse caso é user_impersonation.
   
   > [!NOTE]
   > É possível expor escopos adicionais posteriormente conforme a necessidade. Lembre-se de que a API Web pode expor vários escopos associados a uma variedade de funções diferentes. Agora você pode controlar o acesso toohello API da web usando o escopo da saudação (scp) declaração no token de OAuth 2.0 JWT Olá recebida.
   > 
   > 
6. Clique em **salvar** toosave manifesto de saudação. Web que API está agora configurado toobe usada por outros aplicativos em seu diretório.

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>API da web de saudação tooverify é exposto tooother aplicativos em seu diretório
1. No menu superior do hello, clique em **registros do aplicativo**, selecione Olá desejado aplicativo cliente, você deseja tooconfigure acesso toohello web API e navegar toohello folha de configurações.
2. De saudação **permissões necessárias** seção, selecione a API da web hello qual expôs uma permissão. Menu Olá permissões delegadas lista suspensa, selecione nova permissão de saudação.

![Permissões da lista de tarefas são mostradas](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>Mais informações sobre o manifesto do aplicativo hello
manifesto do aplicativo Hello realmente funciona como um mecanismo para atualizar a entidade de aplicativo hello, que define todos os atributos de configuração de identidade de um aplicativo AD do Azure, incluindo escopos de acesso de API Olá discutimos. Para obter mais informações sobre Olá entidade de aplicativo, consulte Olá [documentação do aplicativo de API do Graph entidade](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity). Nela, você encontrará informações de referência completa sobre permissões de toospecify Olá aplicativo entidade membros usados para a sua API:  

* membro de appRoles Hello, que é uma coleção de [AppRole](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) entidades que podem ser usados toodefine Olá **permissões de aplicativo** para uma API da web  
* membro de oauth2Permissions Hello, que é uma coleção de [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) entidades que podem ser usados toodefine Olá **permissões delegadas** para uma API da web

Para obter mais informações sobre o aplicativo conceitos manifestos em geral, consulte muito[o manifesto do aplicativo do Azure Active Directory Noções básicas sobre Olá](active-directory-application-manifest.md).

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>Acessando hello Azure AD Graph e o Office 365 por meio de APIs do Microsoft Graph  
Como mencionado APIs anteriormente, além de tooexposing/acessar em seus próprios aplicativos de recurso, você também pode atualizar seu aplicativo de cliente tooaccess APIs expostas pelos recursos do Microsoft.  Olá Microsoft Graph API, que é chamado "Microsoft Graph" na lista de saudação do permissões tooother aplicativos, está disponível ou todos os aplicativos que são registrados com o AD do Azure. Se você estiver registrando seu aplicativo cliente em um locatário do AD do Azure que foi fornecido pelo Office 365, você também pode acessar todas as permissões de saudação expostas pelo Olá Microsoft Graph API toovarious recursos do Office 365.

Para obter uma discussão completa sobre escopos de acesso exposto pela API do Microsoft Graph, consulte Olá [escopos de permissão | Conceitos da API do Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes) artigo.

> [!NOTE]
> Devido a limitação atual do tooa, aplicativos cliente nativos só podem chamar a saudação do Azure AD Graph API se usarem a permissão de "Acesso a diretório da sua organização" hello.  Essa restrição não se aplica a aplicativos Web.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>Configurando aplicativos multilocatários
Ao adicionar um aplicativo tooAzure AD, talvez você queira seu toobe aplicativo acessado somente por usuários em sua organização. Como alternativa, talvez você queira que seu toobe aplicativo acessado por usuários em organizações externas. Esses dois tipos de aplicativo são chamados de aplicativos de locatário único e multilocatários. Você pode modificar a configuração de saudação de um toomake do aplicativo de locatário único-um aplicativo multilocatário, consulte a seção abaixo.

É importante toonote diferenças de saudação entre um locatário único e um aplicativo multilocatário:  

* Um aplicativo de locatário único é destinado para uso em uma organização. Normalmente, trata-se de um aplicativo LoB (linha de negócios) escrito por um desenvolvedor corporativo. Um aplicativo de locatário único só precisa toobe acessado por usuários em um diretório e como resultado, ele só precisa toobe provisionado em um diretório.
* Um aplicativo multilocatário é destinado para uso em muitas organizações. Geralmente, trata-se de um aplicativo Web SaaS (software como serviço) escrito por um ISV (fornecedor independente de software). Aplicativos de multilocação precisam toobe provisionado em cada diretório em que eles serão usados, o que exige tooregister de consentimento do usuário ou administrador-los, com suporte por meio da estrutura de consentimento de saudação do AD do Azure. Observe que todos os aplicativos cliente nativo são multilocatários por padrão, como eles são instalados no dispositivo do proprietário do recurso de saudação. Consulte Olá visão geral da saudação seção de estrutura de consentimento acima para obter mais detalhes na estrutura de consentimento hello.

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>Permitindo que usuários externos toogrant os recursos de tootheir de acesso do aplicativo
Se você estiver escrevendo um aplicativo que você deseja toomake tooyour disponíveis clientes ou parceiros fora de sua organização, você precisará de definição de aplicativo hello tooupdate em Olá portal do Azure.

> [!NOTE]
> Ao habilitar o multilocatário, você deve garantir que o URI da ID do Aplicativo do seu aplicativo pertença a um domínio verificado. Além disso, a saudação URL de retorno deve começar com https://. Para saber mais, consulte [Objetos de aplicativo e objetos de entidade de serviço](active-directory-application-objects.md).
> 
> 

aplicativo de tooyour tooenable acesso para usuários externos: 

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No menu superior do hello, escolha **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, clique em aplicativo hello deseja tooconfigure. Isso irá levá-lo página de início rápido do aplicativo toohello, bem como abra a folha de configurações Olá para o aplicativo hello.
4. Na folha de configurações de saudação, clique em **propriedades** e hello invertido **com locatário várias** alternar muito**Sim**.

Depois que você fez Olá alterar acima, os usuários e administradores de outras organizações será capaz de toogrant o diretório de tootheir de acesso do aplicativo e outros dados.

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>Estrutura de consentimento de saudação do AD do Azure em tempo de execução de gatilho
estrutura de consentimento do toouse hello, aplicativos multilocatário cliente devem solicitar autorização usando OAuth 2.0. [Exemplos de código](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) são tooshow disponível como um aplicativo web, o aplicativo nativo ou a autorização de solicitações de aplicativo de servidor/daemon códigos e acessar tokens toocall APIs da web.

Seu aplicativo Web também pode proporcionar uma experiência de inscrição para usuários. Se você oferecer uma experiência de inscrição, espera-se que o usuário Olá clique em um botão de inscrição que redirecionamento Olá navegador toohello OAuth 2.0 do AD do Azure autorizará ponto de extremidade ou um ponto de extremidade userinfo do OpenID Connect. Esses pontos de extremidade permitem que informações de tooget de aplicativo de saudação sobre Olá novo usuário inspecionando Olá id_token. Após a fase de inscrição Olá Olá usuário receberá com um consentimento prompt semelhante toohello mostrado acima em Olá visão geral da saudação seção de estrutura de consentimento.

Como alternativa, é possível que seu aplicativo web também oferecem uma experiência que permite que os administradores muito "inscrever-se minha empresa". Esse processo também redireciona Olá toohello de usuário do Azure AD OAuth 2.0 autorizar o ponto de extremidade. Nesse caso, você passar um prompt = admin_consent toohello parâmetro autorizar o ponto de extremidade tooforce Olá administrador experiência de consentimento, onde o administrador Olá concederá consentimento em nome de sua organização. Somente um usuário que se autentica com uma conta que pertence a função de Administrador Global toohello pode fornecer autorização; outros receberá um erro. Consentimento bem-sucedido, a resposta de saudação conterá admin_consent = true. Quando resgatar um token de acesso, você também receberá um id_token que fornecerá informações sobre a organização hello e administrador Olá que se inscreveu para seu aplicativo.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>Habilitando a concessão implícita do OAuth 2.0 para Aplicativos de Uma Página
Aplicativo de página única (SPAs) normalmente é estruturado com um front-end de excesso de JavaScript que é executado no navegador de saudação, que chama tooperform de back-end de API da web do aplicativo hello sua lógica de negócios. Para SPAs hospedadas no AD do Azure, você use o usuário de saudação do tooauthenticate de concessão implícita do OAuth 2.0 com o Azure AD e obter um token que você pode usar chamadas de tooits de cliente JavaScript do aplicativo hello toosecure volta end da web API. Depois que o usuário Olá concedeu consentimento, esse mesmo protocolo de autenticação pode ser usado tooobtain tokens toosecure chamadas entre o cliente de saudação e outros recursos da API da web configurados para o aplicativo hello. toolearn mais informações sobre concessão de autorização implícita hello e ajuda você a decidir se é adequado para seu cenário de aplicativo, consulte [Olá Noções básicas sobre implícita do OAuth2 conceder fluxo no Azure Active Directory ](active-directory-dev-understanding-oauth2-implicit-grant.md).

Por padrão, a Concessão Implícita do OAuth 2.0 está desabilitada para aplicativos. Você pode habilitar a concessão implícita do OAuth 2.0 para o seu aplicativo por configuração Olá `oauth2AllowImplicitFlow` valor em seu [o manifesto do aplicativo](active-directory-application-manifest.md), que é um arquivo JSON que representa a configuração de identidade do aplicativo.

#### <a name="tooenable-oauth-20-implicit-grant"></a>concessão implícita tooenable OAuth 2.0
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No menu superior do hello, escolha **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, clique em aplicativo hello deseja tooconfigure. Isso irá levá-lo página de início rápido do aplicativo toohello, bem como abra a folha de configurações Olá para o aplicativo hello.
4. Na página de aplicativo hello, clique em **manifesto** editor de manifesto tooopen Olá embutido.
   Localize e defina o valor de "oauth2AllowImplicitFlow" hello muito "true". Por padrão, é "false".
   
    `"oauth2AllowImplicitFlow": true,`
5. Salve o manifesto de saudação atualizado. Uma vez salvo, web que API está agora configurado toouse usuários de tooauthenticate de concessão implícita do OAuth 2.0.


## <a name="removing-an-application"></a>Removendo um aplicativo
Esta seção descreve como tooremove de um aplicativo do AD do Azure locatário.

### <a name="removing-an-application-authored-by-your-organization"></a>Removendo um aplicativo autorizado pela sua organização
Estes são aplicativos de saudação que mostram em hello "Aplicativos que minha empresa possui" Filtrar na página principal de "Aplicativos" Olá para seu locatário do AD do Azure. Em termos de técnicos, esses aplicativos registrados manualmente por meio de saudação portal clássico do Azure, ou programaticamente, por meio do PowerShell ou Olá API do Graph. Mais especificamente, eles são representados por um objeto de Aplicativo e Entidade de Serviço em seu locatário. Para saber mais, confira [Objetos de Aplicativo e de Entidade de Serviço](active-directory-application-objects.md) .

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>tooremove um aplicativo de locatário único de seu diretório
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No menu superior do hello, escolha **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, clique em aplicativo hello deseja tooconfigure. Isso irá levá-lo página de início rápido do aplicativo toohello, bem como abra a folha de configurações Olá para o aplicativo hello.
4. Na página de aplicativo hello, clique em **excluir**.
5. Clique em **Sim** na mensagem de confirmação de saudação.

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>tooremove um aplicativo multilocatário de seu diretório
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Escolha seu locatário do AD do Azure, selecionando a sua conta no canto superior direito de saudação da página de saudação.
3. No menu superior do hello, escolha **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, clique em aplicativo hello deseja tooconfigure. Isso irá levá-lo página de início rápido do aplicativo toohello, bem como abra a folha de configurações Olá para o aplicativo hello.
4. Na folha de configurações de saudação, escolha **propriedades** e hello invertido **com locatário várias** alternar muito**não**. Isso converte seu locatário único de toobe do aplicativo, mas o aplicativo hello ainda permanecerá em uma organização que já aceitou tooit.
5. Clique em Olá **excluir** botão da página de aplicativo hello.
6. Clique em **Sim** na mensagem de confirmação de saudação.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>Removendo um aplicativo multilocatário autorizado por outra organização
Essas são um subconjunto dos aplicativos Olá Mostrar em hello "Aplicativos minha empresa usa" filtro na página de aplicativos"principais" Olá para seu locatário do AD do Azure, especificamente Olá aqueles que não são listados na lista de "Aplicativos que minha empresa possui" hello. Em termos técnicos, estes são aplicativos de multilocação registrados durante o processo de consentimento hello. Mais especificamente, eles são representados apenas por um objeto de Entidade de Serviço em seu locatário. Para saber mais, confira [Objetos de Aplicativo e de Entidade de Serviço](active-directory-application-objects.md) .

Em ordem tooremove diretório de tooyour de acesso de um aplicativo multilocatário (após ter sido concedido o consentimento), o administrador de empresa Olá deve ter acesso de tooremove uma assinatura do Azure por meio de saudação portal do Azure. Como alternativa, o administrador de empresa Olá pode usar Olá [Cmdlets do PowerShell do Azure AD](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove acesso.

## <a name="next-steps"></a>Próximas etapas
* Consulte Olá [diretrizes da marca para aplicativos integrados](active-directory-branding-guidelines.md) para obter dicas sobre orientação visual para seu aplicativo.
* Para obter mais detalhes sobre a relação de saudação entre os objetos de aplicativo e entidade de serviço do aplicativo, consulte [objetos Application e entidade de serviço](active-directory-application-objects.md).
* toolearn mais sobre Olá função hello aplicativo manifesto desempenha, consulte [manifesto do aplicativo Compreendendo Olá Active Directory do Azure](active-directory-application-manifest.md)
* Consulte Olá [Glossário de desenvolvedor do AD do Azure](active-directory-dev-glossary.md) definições de alguns dos conceitos de desenvolvedor Olá básicos do Azure AD (Active Directory).
* Visite Olá [guia do desenvolvedor do Active Directory](active-directory-developers-guide.md) para obter uma visão geral de todos os desenvolvedores de conteúdo relacionado.

