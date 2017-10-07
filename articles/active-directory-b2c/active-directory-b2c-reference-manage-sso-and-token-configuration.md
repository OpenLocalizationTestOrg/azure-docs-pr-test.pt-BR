---
title: "Azure Active Directory B2C: Gerenciar a personalização de SSO e de tokens com políticas personalizadas | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C: Gerenciar a personalização de SSO e de tokens com políticas personalizadas
Usa políticas personalizadas fornece que Olá mesmo controle sobre o token, a sessão e o único configurações sign-on (SSO) por meio de políticas internas.  toolearn que cada configuração faz, consulte a documentação de saudação [aqui](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Configuração de declarações e de tempos de vida de token
configurações de saudação toochange em seu tempo de vida de token, você precisa tooadd um `<ClaimsProviders>` elemento no arquivo de parte confiável Olá da política de saudação desejado tooimpact.  Olá `<ClaimsProviders>` elemento é um filho de saudação `<TrustFrameworkPolicy>`.  Dentro, você precisará de informações de saudação tooput que afeta o tempo de vida de token.  Olá XML tem esta aparência:

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

**Tempos de vida de token de acesso** Olá acesso a vida útil do token pode ser alterado modificando o valor hello dentro de saudação `<Item>` com hello Key = "token_lifetime_secs" em segundos.  valor padrão de saudação em interna é 3600 segundos (60 minutos).

**Vida útil do token ID** vida útil do token ID Olá pode ser alterado modificando o valor hello dentro Olá `<Item>` com hello Key = "id_token_lifetime_secs" em segundos.  valor padrão de saudação em interna é 3600 segundos (60 minutos).

**Vida útil do token de atualização** vida útil do token atualização Olá pode ser alterado modificando o valor hello dentro Olá `<Item>` com hello Key = "refresh_token_lifetime_secs" em segundos.  valor padrão de saudação em interna é 1209600 segundos (14 dias).

**Atualizar o tempo de vida de janela deslizante token** se quiser tooset um token de atualização do tooyour de tempo de vida janela deslizante, modifique o valor de saudação dentro `<Item>` com hello chave = "rolling_refresh_token_lifetime_secs" em segundos.  Olá valor padrão interno é 7776000 (90 dias).  Se você não quiser tooenfore um deslizando o tempo de vida de janela, substitua esta linha com:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Declaração do emissor (iss)** se você quiser toochange Olá emissor (iss) declaração, modifique o valor de saudação dentro Olá `<Item>` com hello Key = "IssuanceClaimPattern".  são valores aplicáveis Olá `AuthorityAndTenantGuid` e `AuthorityWithTfp`.

**Configuração de declaração que representa a ID de política** opções de saudação para definir esse valor são TFP (diretiva de confiança do framework) e ACR (referência do contexto de autenticação).  
É recomendável definir essa tooTFP, toodo isso, certifique-se Olá `<Item>` com hello Key = "AuthenticationContextReferenceClaimPattern" existe e é o valor de saudação `None`.
No seu item do `<OutputClaims>`, adicione este elemento:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
Para o ACR, remover Olá `<Item>` com hello Key = "AuthenticationContextReferenceClaimPattern".

**Declaração de assunto (sub)** essa opção é padronizada tooObjectID, se você quiser tooswitch isso muito`Not Supported`, Olá a seguir:

Substituir esta linha 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
com esta linha:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Comportamento da sessão e SSO
toochange seu comportamento da sessão e as configurações de SSO, você precisa tooadd um `<UserJourneyBehaviors>` elemento dentro Olá `<RelyingParty>` elemento.  Olá `<UserJourneyBehaviors>` elemento deve seguir imediatamente Olá `<DefaultUserJourney>`.  Olá dentro de sua `<UserJourneyBehavors>` elemento deve ter esta aparência:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Configuração de logon único (SSO)** toochange Olá única configuração de logon, é necessário que o valor Olá toomodify `<SingleSignOn>`.  são valores aplicáveis Olá `Tenant`, `Application`, `Policy` e `Disabled`. 

**Aplicativo Web do tempo de vida da sessão (minutos)** toochange Olá Olá web app duração da sessão, você precisa que o valor de toomodify de saudação `<SessionExpiryInSeconds>` elemento.  valor padrão de saudação em políticas internas é 86400 segundos (1440 minutos).

**Tempo limite de sessão do aplicativo Web** toochange Olá web app tempo limite da sessão, é necessário que o valor Olá toomodify `<SessionExpiryType>`.  são valores aplicáveis Olá `Absolute` e `Rolling`.
