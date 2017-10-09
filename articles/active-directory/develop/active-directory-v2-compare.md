---
title: "aaaWhat é diferente no ponto de extremidade do hello AD do Azure v 2.0? | Microsoft Docs"
description: "Uma comparação entre hello original do AD do Azure e pontos de extremidade do hello v 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>O que é diferente no ponto de extremidade do hello v 2.0?
Se você estiver familiarizado com o Active Directory do Azure ou tiver integrado a aplicativos com o Azure AD em Olá anterior, pode haver algumas diferenças no hello v 2.0 ponto de extremidade não esperado.  Este documento chama a atenção para essas diferenças para sua compreensão.

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Contas da Microsoft e contas do Azure AD
o ponto de extremidade do Hello v 2.0 permitem aos desenvolvedores de aplicativos toowrite que aceitam entrada de contas Accounts da Microsoft e do AD do Azure, usando um ponto de extremidade de autenticação único.  Isso dá a você Olá capacidade toowrite seu aplicativo completamente independente da conta; pode ser com ignorância de tipo de saudação da conta que Olá usuário se autentica no.  Naturalmente, você *pode* tornar seu aplicativo com reconhecimento de tipo de saudação da conta que está sendo usado em uma sessão específica, mas não é necessário.

Por exemplo, se seu aplicativo chamar hello [Microsoft Graph](https://graph.microsoft.io), algumas funcionalidades adicionais e os dados serão usuários tooenterprise disponíveis, como seus sites do SharePoint ou os dados do diretório.  Mas para várias ações, como [ler email do usuário](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message), código de saudação pode ser escrito exatamente hello mesmo para contas do AD do Azure e Accounts da Microsoft.  

Integrar seu aplicativo com as contas da Microsoft e do AD do Azure agora é um processo simples.  Você pode usar um único conjunto de pontos de extremidade, uma única biblioteca e um único aplicativo registro toogain acesso tooboth Olá consumidor e empresariais mundos.  toolearn mais sobre Olá v 2.0 de ponto de extremidade, o check-out [Olá visão geral](active-directory-appmodel-v2-overview.md).

## <a name="new-app-registration-portal"></a>Novo portal de registro de aplicativos
tooregister um aplicativo que funciona com o ponto de extremidade do hello v 2.0, você deve usar um novo portal de registro de aplicativo: [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Esse é Olá portal onde você pode obter uma ID de aplicativo, personalizar a aparência de saudação da página de entrada do aplicativo e muito mais.  Tudo o que você precisa tooaccess portal de saudação é uma conta da Microsoft com - conta de trabalho/escola ou pessoal.

## <a name="one-app-id-for-all-platforms"></a>Uma ID do aplicativo para todas as plataformas
Se você já usou o Azure Active Directory, provavelmente, você já registrou vários aplicativos diferentes para um único projeto.  Por exemplo, se você compilou um site e um aplicativo iOS, você tinha tooregistê-los separadamente, usando duas Ids de aplicativo diferente. portal de registro de aplicativo Hello AD do Azure forçado você toomake essa distinção durante o registro:

![Interface do usuário do registro de aplicativo antigo](../../media/active-directory-v2-flows/old_app_registration.PNG)

De forma semelhante, se você tiver um site e uma API Web de back-end, poderá ter registrado cada um deles como um aplicativo separado no Azure AD.  Ou se você tiver um aplicativo iOS e um aplicativo Android, também poderá ter registrado dois aplicativos diferentes.  Registro de cada componente de um aplicativo levou toosome comportamentos inesperados para os desenvolvedores e seus clientes:

* Cada componente que aparece como um aplicativo separado no locatário do Active Directory do Azure saudação de cada cliente.
* Quando um administrador de locatários tentada tooapply política para gerenciar o acesso ao ou excluir um aplicativo, eles teriam toodo caso para cada componente do aplicativo hello.
* Quando os clientes consentido tooan aplicativo, cada componente apareça na tela de consentimento hello como um aplicativo distinto.

Com o ponto de extremidade Olá v 2.0, você pode registrar todos os componentes do seu projeto como um registro de um único aplicativo e usar uma Id de aplicativo único para o projeto inteiro.  Você pode adicionar várias tooa de "plataformas" cada projeto e fornecer dados apropriados Olá para cada plataforma que você adicionar.  Obviamente, você pode criar quantos aplicativos você deseja dependendo dos seus requisitos, mas para maioria Olá dos casos apenas uma Id de aplicativo deve ser necessário.

Nosso objetivo é que isso levar o gerenciamento de aplicativos tooa mais simplificada e experiência de desenvolvimento e criará uma exibição consolidada mais de um único projeto, talvez você esteja trabalhando no.

## <a name="scopes-not-resources"></a>Escopos, não recursos
No Azure Active Directory, um aplicativo pode se comportar como um **recurso** ou um contêiner de tokens.  Um recurso pode definir um número de **escopos** ou **oAuth2Permissions** que ele entenda, permitindo que os aplicativos cliente do recurso de toothat toorequest tokens para um determinado conjunto de escopos.  Considere a possibilidade de saudação do Azure AD Graph API como um exemplo de um recurso:

* Identificador de recurso, ou `AppID URI`: `https://graph.windows.net/`
* Escopos, ou `OAuth2Permissions`: `Directory.Read`, `Directory.Write`, etc.  

Tudo isso é válido para o ponto de extremidade Olá Olá v 2.0.  Um aplicativo ainda pode se comportar como recurso, definir escopos e ser identificado por um URI.  Aplicativos cliente ainda podem solicitar acesso toothose escopos.  No entanto, forma Olá no qual um cliente solicita essas permissões foi alterado.  Olá após um OAuth 2.0 autorize tooAzure solicitação que AD pode ter visto como:

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

Olá onde **recurso** parâmetro indicado qual aplicativo de cliente de saudação do recurso está solicitando a autorização para.  O AD do Azure computada permissões Olá exigidas pelo aplicativo hello com base na configuração estática em Olá Portal do Azure e tokens emitidos adequadamente.  Agora, hello mesmo OAuth 2.0 autorizar solicitação parece:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Olá onde **escopo** parâmetro indica qual aplicativo de recurso e permissões hello está solicitando a autorização para. Olá desejado recurso ainda está muito presente na solicitação de saudação - simplesmente contido em cada um dos valores de saudação do parâmetro de escopo de saudação.  Usar o parâmetro de escopo Olá dessa maneira permite toobe de ponto de extremidade v 2.0 hello mais compatível com a especificação de saudação OAuth 2.0 e alinhe com práticas recomendadas do setor comuns.  Ele também permite que aplicativos tooperform [consentimento incremental](#incremental-and-dynamic-consent), que é descrito na próxima seção, Olá.

## <a name="incremental-and-dynamic-consent"></a>Consentimento incremental e dinâmico
Aplicativos registrados no AD do Azure anteriormente necessário toospecify suas permissões de OAuth 2.0 necessários no hello Portal do Azure, no momento de criação do aplicativo:

![Interface do usuário do registro de permissões](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

permissões de saudação um aplicativo necessário foram configuradas **estaticamente**.  Embora configuração de saudação aplicativo tooexist permitidos em Olá Portal do Azure e mantidos código Olá adequado e simples, ele apresenta algumas questões para desenvolvedores:

* Um aplicativo tinha tooknow todas as permissões de saudação nunca seriam necessárias no momento de criação do aplicativo.  Adicionar permissões ao longo do tempo era um processo difícil.
* Um aplicativo tinha tooknow todos os recursos de saudação nunca acessaria antecipadamente.  Era difícil toocreate aplicativos que possam acessar um número arbitrário de recursos.
* Um aplicativo tinha toorequest todas as permissões de saudação nunca seriam necessárias após a entrar pela primeira saudação usuário vez.  Em alguns casos, isso levou tooa muito longa lista de permissões, que não recomendado os usuários finais de aprovação de acesso do aplicativo hello na entrada inicial.

Com o ponto de extremidade Olá v 2.0, você pode especificar permissões de saudação suas necessidades de aplicativo **dinamicamente**, em tempo de execução durante o uso normal do seu aplicativo.  toodo assim, você pode especificar Olá escopos suas necessidades de aplicativo em qualquer ponto no tempo incluindo-os em Olá `scope` parâmetro de uma solicitação de autorização:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Olá acima solicita permissão para Olá aplicativo tooread de um usuário AD do Azure dados do diretório, bem como gravar dados no diretório tootheir.  Se o usuário Olá consentiu toothose permissões em Olá anterior para esse aplicativo específico, eles simplesmente insere suas credenciais e entrar no aplicativo hello.  Se o usuário Olá não consentiu tooany dessas permissões, o ponto de extremidade do hello v 2.0 solicitará Olá usuário consentimento toothose permissões.  toolearn mais, você pode ler sobre [permissões, autorização e escopos](active-directory-v2-scopes.md).

Permitindo que um aplicativo toorequest permissões dinamicamente por meio de saudação `scope` parâmetro lhe dá controle total sobre a experiência do usuário.  Se desejar, você pode escolher toofrontload seu consentimento experiência e peça para todas as permissões em uma solicitação de autorização inicial.  Ou, se seu aplicativo requer um grande número de permissões, você pode escolher toogather essas permissões de usuário Olá incrementalmente, como eles tentem toouse determinados recursos do seu aplicativo ao longo do tempo.

## <a name="well-known-scopes"></a>Escopos conhecidos
#### <a name="offline-access"></a>Acesso offline
Aplicativos que usam o ponto de extremidade do hello v 2.0 podem exigir Olá uso de uma nova permissão conhecida para aplicativos - Olá `offline_access` escopo.  Todos os aplicativos precisará toorequest essa permissão se eles precisarem de recursos de tooaccess em nome de saudação de um usuário por um período prolongado de tempo, mesmo quando o usuário Olá pode não estar ativamente usando aplicativo hello.  Olá `offline_access` escopo aparecerá usuário toohello em consentimento caixas de diálogo como "Acesso a dados offline", qual usuário Olá deve concordar em.  Olá solicitante `offline_access` permissão permite que seu aplicativo de web tooreceive refresh_tokens OAuth 2.0 do ponto de extremidade do hello v 2.0.  Refresh_tokens são duradouros e podem ser trocados por novos access_tokens do OAuth 2.0 por longos períodos de acesso.  

Se seu aplicativo não solicitar Olá `offline_access` escopo, ele não receberá refresh_tokens.  Isso significa que quando você resgatar um authorization_code no fluxo de código de autorização Olá OAuth 2.0, você só receberá novamente um access_token de saudação `/token` ponto de extremidade.  Esse access_token permanecerá válido por um curto período de tempo (normalmente uma hora), mas acabará expirando.  No momento, seu aplicativo precisará tooredirect Olá usuário back toohello `/authorize` tooretrieve de ponto de extremidade authorization_code um novo.  Durante esse redirecionamento Olá usuário pode ou pode não precisar tooenter suas credenciais novamente ou consentimento novamente toopermissions, dependendo do tipo de Olá Olá do aplicativo.

mais sobre o OAuth 2.0, refresh_tokens e access_tokens, check-out de saudação do toolearn [referência de protocolo v 2.0](active-directory-v2-protocols.md).

#### <a name="openid-profile-and-email"></a>OpenID, perfil e email
Historicamente, hello mais básico OpenID Connect fluxo de entrada com o Azure Active Directory podem fornecer uma grande quantidade de informações sobre o usuário Olá no id_token resultante hello.  Olá declarações em um id_token podem incluir Olá nome de usuário nome, preferencial, endereço de email, ID de objeto e muito mais.

Estamos agora restringir informações Olá que Olá `openid` escopo permite ao aplicativo acesso aos.  escopo de 'openid' Hello somente que seu aplicativo toosign Olá usuário e recebe um identificador específico do aplicativo para o usuário hello.  Se você quiser tooobtain informações de identificação pessoal (PII) sobre o usuário Olá no seu aplicativo, seu aplicativo precisará de permissões adicionais de toorequest de usuário de saudação.  Estamos introduzindo dois novos escopos – hello `email` e `profile` escopos – que permitem toodo.

Olá `email` escopo é muito simples – ele permite que o endereço de email principal do usuário seu aplicativo acesso toohello via Olá `email` Olá id_token de declaração.  Olá `profile` escopo dá seu tooall de acesso do aplicativo outras informações básicas sobre o usuário hello – seu nome, o nome do usuário preferencial, a ID de objeto e assim por diante.

Isso permite toocode seu aplicativo de forma mínima divulgação – somente solicite usuário Olá Olá um conjunto de informações que seu aplicativo requer toodo seu trabalho.  Para obter mais informações sobre os escopos, consulte muito[Olá referência de escopo v 2.0](active-directory-v2-scopes.md).

## <a name="token-claims"></a>Declarações de token
Olá declarações em tokens emitidos pelo ponto de extremidade do hello v 2.0 não será idêntico tootokens emitidas pelos pontos de extremidade de saudação do AD do Azure disponível - toohello novo serviço de migração de aplicativos não devem presumir que exista uma declaração específica em id_tokens ou access_tokens. toolearn sobre declarações específicas do hello emitido em tokens v 2.0, consulte Olá [referência de token v 2.0](active-directory-v2-tokens.md).

## <a name="limitations"></a>Limitações
Há alguns toobe de restrições atento ao usar Olá v 2.0 ponto.  Consulte toohello [doc de limitações v 2.0](active-directory-v2-limitations.md) toosee se quaisquer dessas restrições se aplicam tooyour cenário em particular.
