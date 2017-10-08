---
title: "fluxo de concessão de aaaUnderstanding Olá implícita do OAuth2 no AD do Azure | Microsoft Docs"
description: "Saiba mais sobre a implementação do Azure Active Directory do fluxo de concessão implícita de saudação OAuth2, e se é adequado para seu aplicativo."
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 90e42ff9-43b0-4b4f-a222-51df847b2a8d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/15/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3402e6619709e1a5b1e790ffd79dc62139552d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-oauth2-implicit-grant-flow-in-azure-active-directory-ad"></a>Saudação de Noções básicas sobre implícita do OAuth2 conceder fluxo no Azure Active Directory (AD)
concessão implícita do OAuth2 de saudação é famosa por sendo Olá concessão com a lista mais longa Olá das preocupações de segurança na especificação de OAuth2 hello. E ainda, que é a abordagem Olá implementada por ADAL JS e hello recomendada ao escrever aplicativos SPA. O que acontece? É todos os uma questão de compensações: e acontece, concessão implícita Olá é a abordagem recomendada hello, você pode adotar para aplicativos que consomem uma API da Web por meio de JavaScript em um navegador.

## <a name="what-is-hello-oauth2-implicit-grant"></a>O que é a concessão implícita Olá OAuth2?
Olá melhor [concessão de código de autorização OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.1) é Olá concessão de autorização que usa dois pontos de extremidade separados. ponto de extremidade de autorização de saudação é usado para a fase de interação do usuário hello, que resulta em um código de autorização. ponto de extremidade token Olá é usado pelo cliente Olá para trocar o código de saudação para um token de acesso e, geralmente, um token de atualização. Aplicativos Web é necessária toopresent sua próprias credenciais toohello token extremidade do aplicativo, para que hello servidor de autorização pode autenticar o cliente hello.

Olá [concessão implícita do OAuth2](https://tools.ietf.org/html/rfc6749#section-1.3.2) é uma variante de outros concessões de autorização. Ele permite que um cliente tooobtain um token de acesso (e id_token, ao usar [OpenId Connect](http://openid.net/specs/openid-connect-core-1_0.html)) diretamente do hello autorização ponto de extremidade, sem entrar em contato com o ponto de extremidade token Olá nem autenticação cliente hello. Esta variante foi projetada especificamente para aplicativos em execução em um navegador da Web com base do JavaScript: na especificação de OAuth2 original hello, os tokens são retornados em um fragmento URI. Que torna o bits token Olá toohello disponível o código JavaScript no cliente hello, mas ela garante que eles não serão incluídos em redireciona para o servidor de saudação. Retornar tokens via navegador redireciona diretamente do ponto de extremidade de autorização de saudação. Ele também tem a vantagem de saudação de eliminar os requisitos de várias chamadas de origem, que serão necessários se Olá aplicativo JavaScript é necessário toocontact Olá ponto de extremidade.

Uma característica importante de concessão implícita do OAuth2 de saudação é o fato de saudação que tais fluxos retornam nunca atualizar tokens toohello cliente. Como veremos na próxima seção, Olá, que não é realmente necessário e na verdade seria um problema de segurança.

## <a name="suitable-scenarios-for-hello-oauth2-implicit-grant"></a>Conceder cenários adequados para Olá implícita do OAuth2
Como declara Olá OAuth2 especificação, hello concessão implícita foi desenvolvido tooenable agente do usuário aplicativos – que é toosay, JavaScript em execução em um navegador. Olá definindo característica de tais aplicativos é que o código JavaScript é usado para acessar recursos do servidor (normalmente uma API da Web) e para atualizar o aplicativo hello UX adequadamente. Pense em aplicativos como Gmail ou o Outlook Web Access: quando você seleciona uma mensagem da caixa de entrada, a única mensagem de saudação do painel de visualização muda toodisplay Olá nova seleção, enquanto o restante de saudação da página de saudação permanece inalterada. Isso está em contraste com redirecionamento aplicativos tradicionais baseados na Web, onde cada interação do usuário resulta em uma renderização de página inteira Olá novo da resposta do servidor e um postback da página inteira.

Aplicativos que se Olá baseado em JavaScript abordagem tooits extreme são chamados de aplicativos de página única ou SPAs: Olá trata-se que esses aplicativos somente servem uma página inicial de HTML e JavaScript associado, com todas as interações subsequentes conduzidas pelo Chamadas de API da Web executada por meio de JavaScript. No entanto, abordagens híbrido, onde o aplicativo hello principalmente é controlada por postback mas executa ocasionais chamadas JS, não são incomuns – discussão Olá sobre o uso de fluxo implícito é relevante para aqueles também.

Aplicativos baseados em redirecionamento normalmente protegem suas solicitações por meio de cookies. No entanto, essa abordagem não funciona bem para aplicativos JavaScript. Cookies só funcionam em relação ao domínio Olá que tiverem sido gerados, enquanto chamadas de JavaScript podem ser direcionadas para outros domínios. Na verdade, que será frequentemente caso Olá: pense aplicativos invocação Microsoft Graph API, API do Office, API do Azure – todos os residentes fora Olá domínio onde o aplicativo hello é servido. Uma tendência crescente de aplicativos JavaScript não é toohave nenhum back-end, terceira 3º tooimplement APIs da Web de terceiros de 100% de sua função de negócios.

Atualmente, hello método preferencial de proteção tooa chamadas API da Web é toouse a abordagem de token de portador do hello OAuth2, onde cada chamada é acompanhada por um token de acesso OAuth2. Olá Web API examina o token de acesso de entrada de saudação e, se encontrar em ele hello escopos necessários, ele concede acesso toohello a operação solicitada. fluxo implícito Olá fornece um mecanismo prático para aplicativos JavaScript tooobtain tokens de acesso para uma API da Web, oferece que várias vantagens em respeitam toocookies:

* Tokens podem ser obtidos sem a necessidade de várias chamadas de origem confiável – registro obrigatório de toowhich URI de redirecionamento Olá tokens são retornar garante que os tokens não sejam substituídos
* Aplicativos JavaScript podem obter tantos tokens de acesso quantos forem necessários, para todas as APIs Web que direcionam, sem restrição quanto aos domínios
* Recursos do HTML5 como sessão ou armazenamento local conceder controle total sobre o cache de token e o gerenciamento de vida útil, enquanto o gerenciamento de cookies é opaco toohello aplicativo
* Tokens de acesso não são site tooCross suscetível a ataques de falsificação (CSRF)

fluxo de concessão implícita de saudação não emite tokens de atualização, principalmente por razões de segurança. Um token de atualização não tem escopo tão restrito quanto tokens de acesso, concedendo muito mais capacidade e, assim, causando muito mais danos caso seja vazado. No fluxo implícito do hello, tokens são entregues em URL hello, portanto, o risco de saudação de interceptação é maior do que na concessão de código de autorização de saudação.

No entanto, observe que um aplicativo JavaScript tem outro mecanismo à sua disposição para renovação de tokens de acesso sem repetidamente solicitando credenciais do usuário hello. Olá aplicativo pode usar um iframe oculto tooperform novas solicitações de token no ponto de extremidade de autorização de saudação do AD do Azure: como navegador Olá ainda tem uma sessão ativa (leitura: tem um cookie de sessão) em relação ao domínio de saudação do AD do Azure, Olá solicitação de autenticação pode ocorrer com êxito sem a necessidade de interação do usuário.

Esse modelo permite Olá JavaScript aplicativo hello tooindependently renovar os tokens de acesso e até mesmo adquirir novos para uma nova API (desde que hello usuário anteriormente consentimento para eles. Isso evita Olá carga da aquisição, manutenção e protegendo um artefato de alto valor, como um token de atualização. artefato de saudação que torna possível a renovação silenciosa Olá cookie de sessão do AD do Azure Olá, é gerenciado fora do aplicativo hello. Outra vantagem dessa abordagem é que um usuário pode sair do AD do Azure, usando qualquer um dos aplicativos Olá entrados no AD do Azure, em execução em qualquer uma das guias do navegador hello. Isso resulta na exclusão de saudação do cookie de sessão do AD do Azure hello e Olá aplicativo JavaScript automaticamente perderá capacidade Olá toorenew tokens para Olá desconectado do usuário.

## <a name="is-hello-implicit-grant-suitable-for-my-app"></a>Concessão implícita Olá é adequado para meu aplicativo?
concessão implícita Olá apresenta mais riscos que outros concede e áreas de saudação necessário toopay atenção tooare bem documentada. Por exemplo, [tooImpersonate uso indevido do Token de acesso proprietário do recurso no fluxo implícito] [ OAuth2-Spec-Implicit-Misuse] e [modelo de ameaça do OAuth 2.0 e considerações de segurança] [ OAuth2-Threat-Model-And-Security-Implications]). No entanto, o perfil de risco mais alto de saudação é amplamente devido fatos toohello que é destinada tooenable aplicativos que executam código ativo, servido por um navegador de tooa recurso remoto. Se você estiver planejando uma arquitetura SPA, não ter nenhum dos componentes back-end ou pretende tooinvoke uma API da Web por meio de JavaScript, é recomendável usar fluxo implícito Olá para aquisição de token.

Se seu aplicativo for um cliente nativo, o fluxo implícito Olá não é uma excelente opção. ausência de saudação do cookie de sessão de saudação do AD do Azure no contexto de saudação de um cliente nativo deprives seu aplicativo de meios de saudação de manter uma sessão de vida útil longa. Que significa que seu aplicativo solicitará repetidamente usuário Olá ao obter tokens de acesso para os novos recursos.

Se você estiver desenvolvendo um aplicativo da Web que inclui um back-end e consumir uma API em seu código de back-end, fluxo implícito Olá também não é uma boa opção. Outras concessões oferecem capacidade muito maior. Por exemplo, concessão de credenciais de cliente Olá OAuth2 fornece tokens de tooobtain de capacidade de Olá que refletem permissões Olá atribuído toohello próprio aplicativo, como as delegações de toouser contrário. Isso significa que o cliente Olá tem Olá capacidade toomaintain acesso programático tooresources mesmo quando um usuário não está ativamente envolvido em uma sessão e assim por diante. Não apenas isso, mas essas concessões dão garantias de segurança mais alta. Por exemplo, tokens de acesso de trânsito nunca por meio do navegador do usuário hello, não sendo salvo no histórico do navegador de saudação de risco e assim por diante. aplicativo de cliente Hello também pode executar autenticação forte ao solicitar um token.

## <a name="next-steps"></a>Próximas etapas
* Para obter uma lista completa de recursos para desenvolvedores, incluindo informações de referência para protocolos hello e autorização de OAuth2 concedem fluxos suporte pelo AD do Azure, consulte toohello [guia do desenvolvedor do AD do Azure][AAD-Developers-Guide]
* Consulte [como toointegrate um aplicativo com o Azure AD] [ ACOM-How-To-Integrate] profundidade adicionais no processo de integração de aplicativo hello.

<!--Image references-->

<!--Reference style links in use-->
[AAD-Developers-Guide]: active-directory-developers-guide.md
[ACOM-How-And-Why-Apps-Added-To-AAD]: active-directory-how-applications-are-added.md
[ACOM-How-To-Integrate]: active-directory-how-to-integrate.md
[OAuth2-Spec-Implicit-Misuse]: https://tools.ietf.org/html/rfc6749#section-10.16
[OAuth2-Threat-Model-And-Security-Implications]: https://tools.ietf.org/html/rfc6819
