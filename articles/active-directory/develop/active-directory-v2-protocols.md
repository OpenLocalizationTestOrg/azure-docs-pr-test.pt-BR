---
title: "aaaLearn sobre Olá autorização protocolos suportados pelo AD do Azure v 2.0 | Microsoft Docs"
description: Um tooprotocols guia com suporte pelo ponto de extremidade do hello AD do Azure v 2.0.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Protocolos v2.0 - OAuth 2.0 e OpenID Connect
o ponto de extremidade do Hello v 2.0 pode usar o AD do Azure para identidade-como um serviço com protocolos padrão da indústria, OpenID Connect e OAuth 2.0.  Enquanto o serviço de saudação é compatível com os padrões, pode haver diferenças sutis entre quaisquer duas implementações desses protocolos.  informações de saudação aqui será útil se você escolher seu código toowrite enviando diretamente a & tratamento de solicitações HTTP ou use um 3ª parte abra a biblioteca de software, em vez de usar uma das nossas bibliotecas de código-fonte aberto.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
>
>

## Olá Noções básicas
Em quase todos os fluxos de OAuth & OpenID Connect, há quatro partes envolvidas no exchange hello:

![Funções do OAuth 2.0](../../media/active-directory-v2-flows/protocols_roles.png)

* Olá **servidor de autorização** é o ponto de extremidade do hello v 2.0.  Ele é responsável por garantindo Olá a identidade de usuário, conceder e revogar acesso tooresources e emissão de tokens.  Ele também é conhecido como provedor de identidade Olá - com segurança trata qualquer coisa toodo com informações do usuário hello, seu acesso e relações de confiança de saudação entre partes em um fluxo.
* Olá **proprietário do recurso** normalmente é o usuário final de saudação.  É parte Olá possui dados Olá, e tem Olá power tooallow terceiros tooaccess esses dados ou recursos.
* Olá **cliente OAuth** é seu aplicativo, identificado por sua ID de aplicativo.  É normalmente parte de saudação que usuários finais de saudação interage com e solicitações tokens de saudação do servidor de autorização.  cliente Olá deve ser concedida permissão tooaccess Olá recurso pelo proprietário do recurso de saudação.
* Olá **servidor recurso** é onde os recursos de saudação ou de dados residem.  Ele confia Olá servidor de autorização toosecurely autenticar e autorizar Olá cliente OAuth e usa portador tooensure access_tokens que acessam recursos tooa pode ser concedida.

## Registro do Aplicativo
Cada aplicativo que usa o ponto de extremidade do hello v 2.0 precisará toobe registrado no [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) antes que ele pode interagir usando OAuth ou OpenID Connect.  processo de registro de aplicativo Hello coletar & atribuir alguns aplicativos de tooyour de valores:

* Uma **Id de Aplicativo** que identifica exclusivamente o aplicativo
* Um **URI de redirecionamento** ou **identificador de pacote** que pode ser usado toodirect respostas tooyour back aplicativo
* Alguns outros valores específicos de cenário.

Para obter mais detalhes, saiba como muito[registrar um aplicativo](active-directory-v2-app-registration.md).

## Pontos de extremidade
Depois de registrado, Olá aplicativo se comunica com o Azure AD enviando solicitações toohello v 2.0 ponto de extremidade:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Olá onde `{tenant}` pode assumir um dos quatro valores diferentes:

| Valor | Descrição |
| --- | --- |
| `common` |Permite que os usuários com contas pessoais da Microsoft e contas de trabalho/escola do Active Directory do Azure toosign no aplicativo hello. |
| `organizations` |Permite que somente usuários com contas de trabalho/escola de toosign do Active Directory do Azure para o aplicativo hello. |
| `consumers` |Permite que somente usuários com pessoal toosign de contas (MSA) do Microsoft para o aplicativo hello. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` |Permite que somente usuários com contas de trabalho/escola de um determinado toosign de locatário do Active Directory do Azure para o aplicativo hello.  O nome de domínio amigável de Olá Olá locatário do Azure AD ou identificador de guid do locatário Olá pode ser usado. |

Para obter mais informações sobre como toointeract com esses pontos de extremidade, escolha um tipo de determinado aplicativo abaixo.

## Tokens
implementação de v 2.0 de saudação do OAuth 2.0 e OpenID Connect fazem uso extensivo de tokens de portador, incluindo tokens de portador representados como JWTs. Um token de portador é o recurso protegido de um token de segurança leve que concede Olá tooa de acesso de "portador". Nesse sentido, Olá "portador" é qualquer parte que pode apresentar um token de saudação. Embora uma parte deve primeiro autenticar com o token de portador de saudação do AD do Azure tooreceive, se Olá necessárias não são as etapas seguidas token de saudação toosecure durante a transmissão e armazenamento, pode ser interceptado e usado por uma parte não pretendida. Embora alguns tokens de segurança tenham um mecanismo interno para impedir que partes não autorizadas os utilizem, tokens de portador não possuem esse mecanismo e devem ser transportados em um canal seguro, como segurança da camada de transporte (HTTPS). Se um token de portador for transmitido no hello criptografado, um ataque intermediária Olá man-in pode ser usado por um token de saudação do terceiro mal-intencionado tooacquire e usá-lo para um recurso de tooa protegido do acesso não autorizado. Olá mesmos princípios de segurança se aplicam ao armazenar ou armazenamento em cache os tokens de portador para uso posterior. Verifique sempre se seu aplicativo transmite e armazena tokens de portador de maneira segura. Para obter mais considerações de segurança sobre tokens de portador, consulte [RFC 6750 seção 5](http://tools.ietf.org/html/rfc6750).

Mais detalhes de diferentes tipos de tokens usados no ponto de extremidade do hello v 2.0 está disponível em [Olá referência de token de ponto de extremidade v 2.0](active-directory-v2-tokens.md).

## Protocolos
Se você estiver pronto toosee alguns exemplos de solicitações, começar com uma saudação abaixo tutoriais.  Cada um corresponde tooa cenário de autenticação específico.  Se precisar de ajuda para determinar qual é o fluxo de saudação certa para você, confira [Olá tipos de aplicativos, você pode criar com a v 2.0 do hello](active-directory-v2-flows.md).

* [Criar aplicativos nativos e móveis com o OAuth 2.0](active-directory-v2-protocols-oauth-code.md)
* [Criar aplicativos Web com o Open ID Connect](active-directory-v2-protocols-oidc.md)
* [Compilar aplicativos de página única com hello fluxo implícito do OAuth 2.0](active-directory-v2-protocols-implicit.md)
* [Criar Daemons ou processos do servidor com hello fluxo de credenciais do cliente OAuth 2.0](active-directory-v2-protocols-oauth-client-creds.md)
* [Obter tokens em uma API da Web com hello OAuth 2.0 em nome de fluxo](active-directory-v2-protocols-oauth-on-behalf-of.md)
