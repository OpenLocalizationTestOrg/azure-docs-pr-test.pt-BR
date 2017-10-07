---
title: "aaaHow toobuild um aplicativo que possa entrar em qualquer usuário do AD do Azure | Microsoft Docs"
description: "Instruções passo a passo para a criação de um aplicativo que pode conectar um usuário de qualquer locatário do Azure Active Directory, também conhecido como aplicativo multilocatário."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>Como toosign em qualquer usuário do Azure AD (Active Directory) usando Olá padrão de aplicativo multilocatário
Se você oferecer um Software como um toomany do aplicativo de serviço organizações, você pode configurar seu aplicativo tooaccept entradas de qualquer locatário do AD do Azure.  No Azure AD, isso é chamado de tornar seu aplicativo multilocatário.  Os usuários em qualquer locatário do AD do Azure será capaz de toosign no aplicativo tooyour após consentimento toouse sua conta com seu aplicativo.  

Se você tiver um aplicativo que tem seu próprio sistema de contas ou que dá suporte a outros tipos de conexão por meio de outros provedores de nuvem, a adição da conexão do Azure AD em qualquer locatário será simples. Basta registrar o aplicativo, adicionar o código de conexão pelo OAuth2, OpenID Connect ou SAML e colocar um botão “Entrar com a Microsoft” em seu aplicativo. Clique em Olá botão toolearn mais sobre a marcação de seu aplicativo a seguir.

[![Sign in button][AAD-Sign-In]][AAD-App-Branding]

Este artigo pressupõe que você já está familiarizado com a criação de um aplicativo de locatário único do Azure AD.  Se você não tiver, head backup toohello [home page de guia do desenvolvedor] [ AAD-Dev-Guide] e use um dos nossos inícios rápidos!

Há quatro tooconvert de etapas simples de seu aplicativo em um aplicativo de vários locatários do AD do Azure:

1. Atualizar seu aplicativo registro toobe multilocatário
2. Atualizar o /common do código toosend solicitações toohello ponto de extremidade 
3. Atualizar seu código toohandle vários valores de emissor
4. Entender o consentimento do usuário e administrador e fazer as alterações de código apropriadas

Vamos examinar cada etapa detalhadamente. Você também pode ir direto muito[esta lista de exemplos de multilocatários][AAD-Samples-MT].

## <a name="update-registration-toobe-multi-tenant"></a>Atualizar registro toobe vários locatário
Por padrão, os registros de API/aplicativo Web no Azure AD são de locatário único.  Você pode tornar seu registro multilocatário Localizando comutador hello "várias com locatários" na página de propriedades de saudação de seu registro de aplicativo hello [portal do Azure] [ AZURE-portal] e configurá-lo muito "Sim".

Observe também, antes de um aplicativo multilocatário, Azure AD requer Olá URI de ID do aplicativo de saudação aplicativo toobe globalmente exclusivo. Olá URI da ID do aplicativo é uma das maneiras de saudação que um aplicativo é identificado nas mensagens de protocolo.  Para um aplicativo de locatário único, é suficiente para toobe de URI de ID de aplicativo hello exclusivo dentro desse locatário.  Para um aplicativo multilocatário, ele deve ser globalmente exclusivo para que o AD do Azure pode localizar o aplicativo hello em todos os locatários.  A exclusividade global é imposta exigindo Olá URI de ID de aplicativo toohave um nome de host que corresponda a um domínio verificado do locatário do AD do Azure hello.  Por exemplo, se o nome de saudação do seu locatário foi contoso.onmicrosoft.com e válido URI da ID do aplicativo seria `https://contoso.onmicrosoft.com/myapp`.  Se seu locatário tivesse um domínio verificado de `contoso.com`, então um URI da ID do Aplicativo também seria `https://contoso.com/myapp`.  Haverá falha na configuração de um aplicativo como multilocatário se Olá URI da ID do aplicativo não seguir esse padrão.

Registros de cliente nativos são multilocatários por padrão.  Você não precisa tootake toomake qualquer ação um multi-locatário de de registro do aplicativo cliente nativo.

## <a name="update-your-code-toosend-requests-toocommon"></a>Atualizar seu código toosend solicitações muito comum /
Em um aplicativo de locatário único, solicitações de entrada são enviadas entrar no ponto de extremidade do locatário toohello. Por exemplo, para contoso.onmicrosoft.com ponto de extremidade Olá seria:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

Solicitações enviadas de ponto de extremidade do locatário tooa pode entrar em usuários (ou convidados) que tooapplications de locatário no locatário.  Com um aplicativo multilocatário, o aplicativo hello não sabe com antecedência que o usuário de saudação do locatário é, portanto não é possível enviar solicitações de ponto de extremidade do locatário tooa.  Em vez disso, solicitações são enviadas de ponto de extremidade de tooan multiplexes entre locatários tudo do Azure AD:

    https://login.microsoftonline.com/common

Quando o AD do Azure recebe uma solicitação de saudação/ponto de extremidade comum, ele entra usuário hello e como uma consequência descobre qual usuário de saudação do locatário é de.  Olá/ponto de extremidade comum funciona com todos os protocolos de autenticação Olá suportados pelo AD do Azure: OAuth 2.0, OpenID Connect, SAML 2.0 e WS-Federation.

Olá resposta de logon toohello aplicativo contém um token que representa o usuário hello.  valor do emissor Olá no token Olá informa um aplicativo que o usuário de saudação do locatário é de.  Quando uma resposta retorna do hello/ponto de extremidade comum, valor de emissor Olá no token Olá corresponderá locatário toohello do usuário.  É importante toonote Olá/ponto de extremidade comum não é um locatário e não é um emissor, é apenas um multiplexador.  Ao usar /common, lógica de saudação nos tokens de toovalidate seu aplicativo precisa tootake toobe atualizado isso em conta. 

Como aplicativos multilocatários mencionados acima também devem fornecer uma experiência de entrada consistente para os usuários, o seguinte Olá diretrizes da marca de aplicativo do AD do Azure. Clique em Olá botão toolearn mais sobre a marcação de seu aplicativo a seguir.

[![Sign in button][AAD-Sign-In]][AAD-App-Branding]

Vamos dar uma olhada no uso de saudação do hello /common ponto de extremidade e a implementação de código mais detalhadamente.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>Atualizar seu código toohandle vários valores de emissor
Os aplicativos Web e as APIs Web recebem e validam os tokens do Azure AD.  

> [!NOTE]
> Enquanto os aplicativos cliente nativos solicitar e recebem tokens do AD do Azure, eles fazem toosend caso eles tooAPIs, onde eles são validados.  Os aplicativos nativos não validam os tokens e devem tratá-los como opacos.
> 
> 

Vamos examinar como um aplicativo valida os tokens que ele recebe do Azure AD.  Um aplicativo de locatário único normalmente terá um valor de ponto de extremidade como:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

e usá-lo tooconstruct como uma URL de metadados (nesse caso, OpenID Connect):

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

toodownload duas informações fundamentais que são tokens toovalidate usada: de assinatura de locatário Olá chaves e o valor de emissor.  Cada locatário do AD do Azure tem um valor exclusivo do emissor do formulário de saudação:

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

onde o valor GUID de Olá é versão de renomeação segura de saudação da ID de locatário de saudação do locatário hello.  Se você clicar em Olá precede o link de metadados para `contoso.onmicrosoft.com`, você pode ver esse valor de emissor documento hello.

Quando um aplicativo de locatário único valida um token, ele verifica a assinatura de saudação do token Olá contra Olá chaves de documento de metadados de saudação de assinatura. Isso permite que ele toomake se que o valor de emissor Olá no hello corresponde ao token Olá um que foi encontrado no documento de metadados de saudação.

Desde Olá/comum o ponto de extremidade não corresponde a tooa locatário e não um emissor, ao examinar o valor de emissor Olá nos metadados de saudação para comum tem uma URL de modelo em vez de um valor real:

    https://sts.windows.net/{tenantid}/

Portanto, um aplicativo multilocatário não é possível validar tokens apenas por correspondência do valor de emissor Olá nos metadados de saudação com hello `issuer` valor no token de saudação.  Um aplicativo multilocatário necessidades lógica toodecide quais valores de emissor são válidas e que são não, com base no locatário Olá parte de identificação do valor de emissor hello.  

Por exemplo, se um aplicativo multilocatário só permite entrar de locatários específicos que se inscreveram para seu serviço, em seguida, ele deve verificar valor do emissor hello ou hello `tid` valor de declaração na toomake de token de saudação se esse locatário está em sua lista de assinantes.  Se um aplicativo multilocatário apenas lida com indivíduos e não faz qualquer decisões de acesso com base em locatários, ele pode ignorar o valor de emissor Olá completamente.

Exemplos de multilocatário Olá no hello [conteúdo relacionado](#related-content) seção Olá final deste artigo, a validação do emissor é desabilitado tooenable qualquer toosign de locatário do AD do Azure no.

Agora vamos dar uma olhada na experiência do usuário Olá para usuários que estão se conectando aplicativos toomulti locatários.

## <a name="understanding-user-and-admin-consent"></a>Entendendo o consentimento do usuário e do administrador
Para toosign um usuário no aplicativo tooan no AD do Azure, o aplicativo hello deve ser representado no locatário saudação do usuário.  Isso permite a organização Olá toodo coisas como aplicar políticas exclusivas quando os usuários do seu locatário entrar no aplicativo toohello.  Para um aplicativo de locatário único, o registro é simple; ele tem Olá que acontece quando você registrar o aplicativo hello no hello [portal do Azure][AZURE-portal].

Para um aplicativo multilocatário, registro de saudação inicial para o aplicativo hello reside no locatário do AD do Azure Olá usado pelo desenvolvedor de saudação.  Quando um usuário de um locatário diferente entra no aplicativo toohello para Olá a primeira vez, o AD do Azure-los pergunta tooconsent toohello permissões solicitadas pelo aplicativo hello.  Se eles consentimento, chamado de uma representação de um aplicativo hello um *entidade de serviço* é criado no hello locatário do usuário e entrar pode continuar. Uma delegação também é criada no diretório de saudação que registra o aplicativo de toohello de consentimento do usuário hello. Consulte [objetos Application e entidade de serviço] [ AAD-App-SP-Objects] para obter detalhes sobre objetos Application e ServicePrincipal do aplicativo hello e como elas se relacionam tooeach outros.

![Aplicativo de camada toosingle de consentimento][Consent-Single-Tier] 

Essa experiência de consentimento é afetada por permissões de saudação solicitadas pelo aplicativo hello.  O Azure AD dá suporte a dois tipos de permissões, somente do aplicativo e delegadas:

* Uma permissão delegado concede um tooact de capacidade de saudação do aplicativo como um usuário conectado para um subconjunto de usuário de saudação do hello coisas pode fazer.  Por exemplo, você pode conceder a um aplicativo Olá permissão delegado tooread Olá assinado no calendário do usuário.
* Uma permissão somente de aplicativo é concedida diretamente toohello identidade de aplicativo hello.  Por exemplo, você pode conceder a uma lista de saudação do aplicativo hello permissão somente para aplicativo tooread de usuários em um locatário, independentemente de quem está conectada no aplicativo toohello.

Algumas permissões podem ser consentido tooby um usuário normal, enquanto outros exigem o consentimento do administrador de locatários. 

### <a name="admin-consent"></a>Consentimento do administrador
As permissões somente do aplicativo sempre exigem o consentimento do administrador de locatários.  Se seu aplicativo solicita uma permissão somente de aplicativo e um usuário tenta toosign no aplicativo toohello, uma mensagem de erro será exibida informando que o usuário de saudação não for capaz de tooconsent.

Algumas permissões delegadas também exigem o consentimento do administrador de locatários.  Por exemplo, Olá capacidade toowrite back tooAzure AD como Olá usuário conectado requer o consentimento do administrador de locatários.  Como as permissões somente de aplicativo, se um usuário comum tentar toosign no aplicativo tooan que solicita uma permissão delegada que requer o consentimento do administrador, o aplicativo receberá um erro.  Se ou não requer uma permissão de consentimento do administrador é determinado pelo desenvolvedor de saudação que publicou o recurso Olá e pode ser encontrados na documentação de saudação do recurso de saudação.  Links tootopics que descreve as permissões disponíveis Olá hello Azure AD Graph API e do Microsoft Graph API são em Olá [relacionados conteúdo](#related-content) deste artigo.

Se seu aplicativo usa permissões que exigem o consentimento do administrador, você precisa toohave um gesto como um botão ou link onde Olá administrador pode iniciar a ação de saudação.  solicitação Olá seu aplicativo envia para esta ação é uma solicitação de autorização OAuth2/OpenID Connect normal, mas que também inclui Olá `prompt=admin_consent` parâmetro de cadeia de caracteres de consulta.  Uma vez Olá administrador consentiu e entidade de serviço Olá é criada no locatário saudação do cliente, as solicitações de logon subsequentes não necessário Olá `prompt=admin_consent` parâmetro. Como administrador de saudação decidiu Olá solicitadas permissões são aceitáveis, nenhum outro usuário no locatário Olá deverá consentimento desse ponto em diante.

Olá `prompt=admin_consent` parâmetro também pode ser usado por aplicativos que exigem permissões que não exigem o consentimento do administrador. Isso é feito quando um aplicativo hello requer uma experiência em administração de locatário hello "se inscreve" um tempo e não a outros usuários são solicitados a dar consentimento desse ponto em.

Se um aplicativo requer o consentimento do administrador, e um administrador faz logon no, mas hello `prompt=admin_consent` parâmetro não for enviado, Olá administrador será consentimento com êxito aplicativo toohello **somente para sua conta de usuário**.  Usuários regulares ainda não será capaz de toosign no e consentimento toohello aplicativo.  Isso é útil se você quiser toogive Olá locatário administrador Olá capacidade tooexplore seu aplicativo antes de permitir acesso a outros usuários.

Um administrador de locatários pode desabilitar a capacidade de saudação para usuários regulares tooconsent tooapplications.  Se esse recurso estiver desabilitado, consentimento do administrador é sempre necessário para Olá aplicativo toobe configurado no locatário hello.  Se você quiser tootest seu aplicativo com consentimento do usuário regular desabilitado, você pode encontrar opção de configuração de saudação no locatário de saudação do AD do Azure a seção de configuração de saudação [portal do Azure][AZURE-portal].

> [!NOTE]
> Alguns aplicativos querem uma experiência de onde os usuários regulares estão tooconsent capaz inicialmente e aplicativo de hello posterior pode envolver administrador hello e solicitar permissões que exigem o consentimento do administrador.  Não há nenhuma maneira toodo isso com o registro de um único aplicativo no AD do Azure hoje.  ponto de extremidade de v2 Olá futuros do AD do Azure permitirá que aplicativos toorequest permissões em tempo de execução, em vez de em tempo de registro, que permitirão a esse cenário.  Para obter mais informações, consulte Olá [guia do desenvolvedor do modelo de aplicativo do AD do Azure v2][AAD-V2-Dev-Guide].
> 
> 

### <a name="consent-and-multi-tier-applications"></a>Aplicativos de várias camadas e consentimento
Seu aplicativo pode ter várias camadas, cada uma representada por seu próprio registro no Azure AD.  Por exemplo, um aplicativo nativo que chama uma API Web ou um aplicativo Web que chama uma API Web.  Em ambos os casos, o cliente de hello (aplicativo nativo ou aplicativo web) solicita recursos de saudação permissões toocall (API da web).  Para Olá cliente toobe consentido com êxito no locatário do cliente, todos os toowhich de recursos, ele solicita permissões já deve existir no locatário saudação do cliente.  Se essa condição não for atendida, AD do Azure retornará um erro que Olá recurso deve ser adicionado pela primeira vez.

**Várias camadas em um único locatário**

Isso poderá ser um problema se seu aplicativo lógico consistir em dois ou mais registros de aplicativo, por exemplo, um cliente e um recurso separados.  Como obter recursos de saudação em locatário do cliente Olá primeiro?  AD do Azure abrange nesse caso, permitindo que o cliente e recurso toobe consentido em uma única etapa. usuário Olá vê Olá soma total de permissões Olá solicitada pelo cliente hello e recursos na página de consentimento hello.  tooenable esse comportamento, registro de aplicativo do recurso Olá deve incluir a ID do aplicativo do cliente hello como um `knownClientApplications` em seu manifesto de aplicativo.  Por exemplo:

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Essa propriedade pode ser atualizada por meio do recurso de saudação [manifesto do aplicativo][AAD-App-Manifest]. Isso é demonstrado nos clientes nativos multicamados chamando a API da web de exemplo em Olá [relacionados conteúdo](#related-content) seção Olá final deste artigo. Olá diagrama a seguir fornece uma visão geral de consentimento para um aplicativo de várias camado registrado em um único locatário:

![Aplicativo de cliente conhecidos toomulti da camada de consentimento][Consent-Multi-Tier-Known-Client] 

**Várias camadas em vários locatários**

Um caso semelhante acontece se níveis diferentes de saudação de um aplicativo são registrados em diferentes locatários.  Por exemplo, considere o caso de saudação da criação de um aplicativo cliente nativo que chama Olá API do Office 365 Exchange Online.  toodevelop Olá nativo aplicativo e posterior para Olá aplicativo nativo toorun no locatário do cliente, o principal do serviço Exchange Online Olá deve estar presente.  Nesse caso, hello desenvolvedor e o cliente devem adquirir o Exchange Online para toobe principal do serviço Olá criado em seus locatários.  

No caso de saudação de uma API criado por uma organização diferente da Microsoft, o desenvolvedor de saudação do hello API precisa tooprovide uma maneira para seu aplicativo de saudação tooconsent clientes em locatários de seus clientes. Olá recomendado é de design para Olá 3ª parte desenvolvedor toobuild Olá API, de modo que ele também pode funcionar como um tooimplement de cliente web inscrição:

1. Siga Olá Olá de tooensure seções anterior API implementa os requisitos de registro/código de aplicativo multilocatário Olá
2. Além de funções/escopos tooexposing Olá da API, certifique-se de registro de saudação inclui hello "entrar e ler o perfil de usuário" permissão de AD do Azure (fornecido por padrão)
3. Implementar uma página de entrada-em/entrada o no cliente de web hello, seguir Olá [consentimento do administrador](#admin-consent) orientação discutido anteriormente 
4. Depois que o aplicativo toohello de consentimento do usuário de hello, hello links de delegação de principal e o consentimento de serviço são criados em seu locatário e aplicativo nativo hello pode obter tokens para Olá API

Olá diagrama a seguir fornece uma visão geral de consentimento para um aplicativo de várias camado registrado no locatários diferentes:

![Consentimento de aplicativo de várias partes da camada toomulti][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>Revogando o consentimento
Os usuários e administradores podem revogar consentimento tooyour aplicativo a qualquer momento:

* Os usuários revogar acesso tooindividual aplicativos por removê-los do seu [aplicativos de painel de acesso] [ AAD-Access-Panel] lista.
* Os administradores revogar acesso tooapplications removê-los do AD do Azure usando a seção de gerenciamento de saudação do AD do Azure de saudação [portal do Azure][AZURE-portal].

Se um administrador consentir aplicativos tooan para todos os usuários em um locatário, os usuários não é possível revogar o acesso individualmente.  Somente administrador Olá pode revogar o acesso e apenas para Olá aplicativo inteiro.

### <a name="consent-and-protocol-support"></a>Suporte a protocolo e consentimento
Há suporte para o consentimento no AD do Azure por meio de saudação OAuth, OpenID Connect, WS-Federation e SAML protocolos.  Olá protocolos SAML e WS-Federation não oferecem suporte a saudação `prompt=admin_consent` parâmetro, portanto, só é possível por meio de OpenID Connect e OAuth consentimento do administrador.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>Aplicativos multilocatários e caching de tokens de acesso
Aplicativos de multilocação também podem obter tokens de acesso toocall APIs que são protegidos pelo AD do Azure.  Um erro comum ao usar o hello biblioteca de autenticação do Active Directory (ADAL) com um aplicativo multilocatário, é tooinitially solicitação um token para um usuário usando /common, recebeu uma resposta e solicitar um token subsequente para o mesmo usuário também usando /common.  Desde que a resposta de saudação do AD do Azure vêm de um locatário não/comum, ADAL armazena em cache o token hello como sendo de locatário de saudação. Olá subsequente chamar tooget muito comum/um token de acesso para entrada de cache de saudação do hello usuário erros e usuário Olá é toosign solicitada em novamente.  tooavoid cache de saudação ausentes, fazer subsequentes se chamadas para um usuário já conectado são feitas ponto de extremidade do locatário toohello.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toobuild um aplicativo que pode entrar em um usuário de qualquer locatário do Active Directory do Azure. Depois de habilitar o logon único entre o aplicativo e o Active Directory do Azure, você também pode atualizar seu aplicativo tooaccess APIs expostas pelos recursos da Microsoft, como o Office 365. Então você pode oferecer uma experiência personalizada em seu aplicativo, por exemplo mostrando informações contextuais toohello usuários, como a imagem do seu perfil ou seu próximo compromisso no calendário. toolearn mais sobre como tornar API chama tooAzure do Active Directory e serviços do Office 365 como o Exchange, SharePoint, OneDrive, OneNote, Planner, Excel e muito mais, visite: [Microsoft Graph API][MSFT-Graph-overview].


## <a name="related-content"></a>Conteúdo relacionado
* [Exemplos de aplicativos multilocatários][AAD-Samples-MT]
* [Diretrizes de identidade visual para aplicativos][AAD-App-Branding]
* [Guia do Desenvolvedor do Azure AD][AAD-Dev-Guide]
* [Objetos de Aplicativo e de Entidade de Serviço][AAD-App-SP-Objects]
* [Integrando aplicativos com o Azure Active Directory][AAD-Integrating-Apps]
* [Visão geral da estrutura de consentimento de saudação][AAD-Consent-Overview]
* [Escopos de permissão da API do Microsoft Graph][MSFT-Graph-permision-scopes]
* [Escopos de permissão da API do Graph do Azure AD][AAD-Graph-Perm-Scopes]

Use Olá comentários de tooprovide seção comentários a seguir e ajudar a refinar e formatar o nosso conteúdo.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














