---
title: "Azure Active Directory B2C: configuração do token, sessão e logon único | Microsoft Docs"
description: "Token, sessão e configuração de logon único no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C: Configuração de token, de sessão e de logon único
Esse recurso oferece um controle refinado, com base [em cada política](active-directory-b2c-reference-policies.md), de:

1. Vida útil dos tokens de segurança emitidos pelo Azure Active Directory (Azure AD) B2C.
2. Vida útil de sessões dos aplicativos Web gerenciados pelo Azure AD B2C.
3. Formatos de importantes declarações em tokens de segurança Olá emitidos pelo Azure AD B2C.
4. Comportamento do SSO (logon único) em vários aplicativos e políticas em seu locatário B2C.

Você pode usar esse recurso em seu locatário B2C da seguinte maneira:

1. Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
2. Clique em **Políticas de entrada**. *Observação: você pode usar esse recurso em qualquer tipo de política, não apenas em **Políticas de entrada***.
3. Clique em uma política para abri-la. Por exemplo, clique em **B2C_1_SiIn**.
4. Clique em **editar** na parte superior de saudação da folha de saudação.
5. Clique em **Configuração de token, de sessão e de logon único**.
6. Faça as alterações desejadas. Saiba mais sobre as propriedades disponíveis nas seções seguintes.
7. Clique em **OK**.
8. Clique em **salvar** na parte superior de saudação da folha de saudação.

## <a name="token-lifetimes-configuration"></a>Configuração da vida útil de tokens
B2C do Azure AD oferece suporte a saudação [protocolo de autorização do OAuth 2.0](active-directory-b2c-reference-protocols.md) para habilitar o acesso seguro tooprotected recursos. tooimplement esse suporte, o Azure AD B2C emite vários [tokens de segurança](active-directory-b2c-reference-tokens.md). Essas são propriedades de saudação, que você pode usar tempos de vida toomanage dos tokens de segurança emitidos pelo Azure AD B2C:

* **Tempos de vida (minutos) de token de acesso & ID**: recurso protegido de tempo de vida de saudação do hello OAuth 2.0 portador token toogain usado acesso tooa. No momento, o Azure AD B2C só emite tokens de ID. Esse valor seria aplicada tooaccess tokens, quando adicionamos suporte para eles.
  * Padrão = 60 minutos.
  * Mínimo (inclusive) = 5 minutos.
  * Máximo (inclusive) = 1440 minutos.
* **Vida útil do token de atualização (dias)**: Olá período de tempo máximo antes que um token de atualização pode ser usado tooacquire um novo acesso ou o token de ID (e, opcionalmente, um novo token de atualização, se seu aplicativo tiver sido concedido Olá `offline_access` escopo).
  * Padrão = 14 dias.
  * Mínimo (inclusive) = 1 dia.
  * Máximo (inclusive) = 90 dias.
* **Atualizar o tempo de vida de janela deslizante token (dias)**: depois que este usuário de saudação de decorrer período de tempo é forçado toore-autenticar, independentemente do período de validade de saudação do token de atualização mais recente Olá obtido pelo aplicativo hello. Ele só pode ser fornecido se o comutador hello está definido muito**limitada**. Ele precisa toobe maior que ou igual toohello **atualização vida útil do token (dias)** valor. Se o comutador hello está definido muito**Unbounded**, você não pode fornecer um valor específico.
  * Padrão = 90 dias.
  * Mínimo (inclusive) = 1 dia.
  * Máximo (inclusive) = 365 dias.

Estes são alguns casos de uso que você pode habilitar usando essas propriedades:

* Permitir que um toostay usuário entrado em um aplicativo móvel indefinidamente, desde que ele ou ela está sempre ativa no aplicativo hello. Você pode fazer isso definindo Olá **atualização deslizante janela vida útil do token (dias)** alternar muito**Unbounded** em sua política de entrada.
* Atender aos requisitos de segurança e conformidade do setor, definindo tempos de vida token Olá acesso apropriado.

    > [!NOTE]
    > Essas configurações não estão disponíveis para as políticas de redefinição de senha.
    > 
    > 

## <a name="token-compatibility-settings"></a>Configurações de compatibilidade de token
Fizemos formatação declarações de tooimportant alterações em tokens de segurança emitidos pelo Azure AD B2C. Isso foi feito tooimprove nosso suporte de protocolo padrão e para melhor interoperabilidade com bibliotecas de identidade de terceiros. No entanto, tooavoid quebra de aplicativos existentes, criamos Olá propriedades tooallow clientes tooopt-conforme necessário a seguir:

* **Declaração do emissor (iss)**: Isso identifica o locatário de saudação do Azure AD B2C que emitiu o token de saudação.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: Esse é o valor de padrão de saudação.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: Esse valor inclui IDs para locatário Olá B2C e política Olá usado na solicitação de token hello. Se seu aplicativo ou a biblioteca precisa do Azure AD B2C toobe compatível com hello [OpenID Connect 1.0 de descoberta especificação](http://openid.net/specs/openid-connect-discovery-1_0.html), use esse valor.
* **Declaração de assunto (sub)**: Isso identifica a entidade hello, ou seja, usuário hello, para qual Olá token dá informações.
  * **ObjectID**: Este é o valor padrão de saudação. Ela popula Olá ID de objeto do usuário Olá no diretório de saudação em Olá `sub` declaração no token de saudação.
  * **Não tem suporte**: isso é fornecido somente para compatibilidade com versões anteriores, e é recomendável que você alterne muito**ObjectID** assim que for possível.
* **Que representa a ID da política de declaração**: Isso identifica o tipo de declaração de saudação em qual Olá usado na solicitação de token de saudação do ID de política é preenchido.
  * **TFP**: Este é o valor padrão de saudação.
  * **Acr**: isso é fornecido somente para compatibilidade com versões anteriores, e é recomendável que você alterne muito`tfp` assim que for possível.

## <a name="session-behavior"></a>Comportamento da sessão
B2C do Azure AD oferece suporte a saudação [protocolo de autenticação OpenID Connect](active-directory-b2c-reference-oidc.md) para habilitar aplicativos tooweb entrada segura. Essas são propriedades de hello, que você pode usar sessões dos aplicativos web toomanage:

* **Aplicativo Web do tempo de vida da sessão (minutos)**: tempo de vida de saudação do cookie de sessão do Azure AD B2C armazenado no navegador do usuário Olá após a autenticação bem-sucedida.
  * Padrão = 1440 minutos.
  * Mínimo (inclusive) = 15 minutos.
  * Máximo (inclusive) = 1440 minutos.
* **Tempo limite de sessão do aplicativo Web**: se essa opção for definida muito**absoluto**, usuário Olá é forçado toore-autenticar após Olá período de tempo especificado por **aplicativo Web do tempo de vida da sessão (minutos)** expirar. Se essa opção for definida muito**sem interrupção** (hello a configuração padrão), usuário Olá permanece conectado como usuário Olá é continuamente ativo no seu aplicativo web.

Estes são alguns casos de uso que você pode habilitar usando essas propriedades:

* Atender aos requisitos de segurança e conformidade do setor, definindo a sessão do aplicativo web apropriado Olá tempos de vida.
* Force uma nova autenticação após um período de tempo definido durante a interação do usuário com uma parte do alto nível de segurança de seu aplicativo Web. 

    > [!NOTE]
    > Essas configurações não estão disponíveis para as políticas de redefinição de senha.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>Configuração de SSO (Logon Único)
Se você tiver vários aplicativos e políticas em seu locatário B2C, você pode gerenciar interações do usuário entre eles usando Olá **configuração de logon único** propriedade. Você pode definir Olá propriedade tooone de saudação configurações a seguir:

* **Locatário**: esta é a configuração de padrão de saudação. Usar essa configuração permite que vários aplicativos e políticas em seu locatário B2C tooshare Olá mesma sessão de usuário. Por exemplo, quando um usuário entra em um aplicativo, Contoso Shopping, ele também pode entrar sem problemas em outro aplicativo, Contoso Pharmacy, ao acessá-lo.
* **Aplicativo**: Isso permite toomaintain uma sessão de usuário exclusivamente para um aplicativo, independentemente de outros aplicativos. Por exemplo, se você quiser Olá usuário toosign em tooContoso farmácia (com hello mesmas credenciais), mesmo se ele já está conectado a Contoso compras, outro aplicativo no hello mesmo locatário B2C. 
* **Diretiva**: Isso permite toomaintain uma sessão de usuário exclusivamente para uma política, independente de aplicativos Olá usá-lo. Por exemplo, se o usuário Olá já conectado e concluir uma etapa MFA (autenticação) vários fatores, ele ou ela pode receber partes de toohigher segurança de acesso de vários aplicativos como Olá sessão vinculada toohello política não expira.
* **Desabilitado**: Isso força Olá toorun de usuário por meio de jornada de usuário inteiro Olá em cada execução da política de saudação. Por exemplo, isso permitirá que vários toosign usuários tooyour aplicativo (em um desktop cenário compartilhada), até mesmo enquanto um único usuário permanece conectado durante o tempo todo hello.

    > [!NOTE]
    > Essas configurações não estão disponíveis para as políticas de redefinição de senha.
    > 
    > 

