---
title: "Azure Active Directory B2C: protocolos de autenticação | Microsoft Docs"
description: "Como aplicativos toobuild diretamente por meio de Olá protocolos com suporte no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Azure AD B2C: protocolos de autenticação
O Azure AD B2C (Azure Active Directory B2C) fornece identidade como um serviço para seus aplicativos, com suporte a dois protocolos padrão de mercado, o OpenID Connect e o OAuth 2.0. serviço de saudação é compatível com os padrões, mas as duas implementações os protocolos podem ter diferenças sutis. 

informações de saudação neste guia serão útil se você escreve seu código enviando diretamente e tratamento de solicitações HTTP, em vez de por meio de uma biblioteca de software livre. É recomendável que você leia esta página antes de mergulhar nos detalhes de saudação de cada protocolo específico. Mas se você já estiver familiarizado com o Azure AD B2C, você pode ir direto muito[Olá guias de referência de protocolo](#protocols).

<!-- TODO: Need link toolibraries above -->

## Noções básicas de saudação
Cada aplicativo que usa o Azure AD B2C precisa toobe registrado em seu diretório do B2C em Olá [portal do Azure](https://portal.azure.com). processo de registro de aplicativo Hello coleta e atribui o aplicativo de tooyour alguns valores:

* Uma **ID de aplicativo** que identifica exclusivamente o aplicativo.
* Um **URI de redirecionamento** ou **identificador de pacote** que pode ser usado toodirect respostas tooyour back aplicativo.
* Alguns outros valores específicos de cenário. Para obter mais informações, saiba [como tooregister seu aplicativo](active-directory-b2c-app-registration.md).

Depois de registrar seu aplicativo, ele se comunica com o Azure Active Directory (AD do Azure), enviando solicitações toohello endpoint:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Em quase todos os fluxos de OpenID Connect e OAuth, quatro partes são envolvidas no exchange hello:

![Funções do OAuth 2.0](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* Olá **servidor de autorização** é o ponto de extremidade de saudação do AD do Azure. Manipule com segurança as informações de qualquer coisa relacionada toouser e acesso. Ele também lida com relações de confiança de saudação entre partes de saudação em um fluxo. Ele é responsável por verificar a identidade do usuário hello, conceder e revogar acesso tooresources e emitir tokens. Ele também é conhecido como provedor de identidade hello.

* Olá **proprietário do recurso** normalmente é o usuário final de saudação. É parte de saudação que possui dados hello e tem Olá power tooallow terceiros tooaccess esses dados ou recursos.

* Olá **cliente OAuth** é seu aplicativo. Ele é identificado pela ID do aplicativo. É normalmente parte de saudação que os usuários finais interagem com. Ela também solicita tokens de saudação do servidor de autorização. proprietário do recurso Olá deve conceder tooaccess de permissão de cliente Olá Olá recursos.

* Olá **servidor recurso** é onde os recursos de saudação ou de dados residem. Ele confia autorização Olá toosecurely servidor autenticar e autorizar o cliente do OAuth hello. Ele também usa o acesso de portador tooensure tokens que acessam recursos tooa pode ser concedida.

## Políticas
Possivelmente, Azure AD B2C políticas são as características mais importantes do serviço Olá Olá. B2C do AD do Azure estende protocolos padrão de OAuth 2.0 e OpenID Connect Olá introduzindo políticas. Isso permite a Azure AD B2C tooperform muito mais do que simples autenticação e autorização. 

As políticas descrevem totalmente as experiências de identidade do consumidor, incluindo inscrição, entrada ou edição de perfil. As políticas podem ser definidas em uma interface do usuário administrativa. Elas podem ser executadas usando um parâmetro de consulta especial nas solicitações de autenticação HTTP. 

As políticas não são recursos padrão do OAuth 2.0 e OpenID Connect, para que você deve tomar Olá tempo toounderstand-los. Para obter mais informações, consulte Olá [guia de referência de política do Azure AD B2C](active-directory-b2c-reference-policies.md).

## Tokens
implementação de saudação do Azure AD B2C do OAuth 2.0 e OpenID Connect faz uso extensivo de tokens de portador, incluindo tokens de portador que são representados como tokens de web JSON (JWTs). Um token de portador é o recurso protegido de um token de segurança leve que concede Olá tooa de acesso de "portador".

portador Olá é qualquer parte que pode apresentar um token de saudação. Primeiro, o Azure AD deve autenticar uma parte para que ela possa receber um token de portador. Mas se Olá necessárias não são as etapas seguidas token de saudação toosecure durante a transmissão e armazenamento, pode ser interceptado e usado por uma parte não pretendida.

Alguns tokens de segurança têm um mecanismo interno que impede que partes não autorizadas os usem, mas os tokens de portador não têm esse mecanismo. Eles devem ser transportados em um canal seguro, como HTTPS (protocolo TLS). 

Se um token de portador for transmitido fora de um canal seguro, um terceiro mal-intencionado pode usar um token de saudação do ataque man-in-the-middle tooacquire e usar o recurso de tooa protegido de acesso toogain não autorizado. Olá mesmos princípios de segurança se aplicam quando os tokens de portador são armazenados ou armazenado em cache para uso posterior. Sempre se certifique de que seu aplicativo transmita e armazene tokens de portador de maneira segura.

Para obter mais considerações de segurança sobre tokens de portador, confira [RFC 6750 seção 5](http://tools.ietf.org/html/rfc6750).

Para obter mais informações sobre tipos diferentes de saudação de tokens que são usados no Azure AD B2C estão disponíveis em [Olá referência de token do AD do Azure](active-directory-b2c-reference-tokens.md).

## Protocolos
Quando você estiver pronto tooreview alguns exemplos de solicitações, você pode começar com uma saudação tutoriais a seguir. Cada corresponde tooa cenário de autenticação específico. Se você precisar ajudar a determinar qual fluxo é ideal para você, confira [Olá tipos de aplicativos, você pode criar usando o Azure AD B2C](active-directory-b2c-apps.md).

* [Compilar aplicativos nativos e móveis com o OAuth 2.0](active-directory-b2c-reference-oauth-code.md)
* [Compilar aplicativos Web usando o OpenID Connect](active-directory-b2c-reference-oidc.md)
* [Compilar aplicativos de única página usando fluxo implícito Olá OAuth 2.0](active-directory-b2c-reference-spa.md)

