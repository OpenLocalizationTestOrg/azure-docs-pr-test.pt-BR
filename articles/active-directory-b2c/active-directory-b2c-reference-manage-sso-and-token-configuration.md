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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="fe1f7-102">Azure Active Directory B2C: Gerenciar a personalização de SSO e de tokens com políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="fe1f7-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="fe1f7-103">Usa políticas personalizadas fornece que Olá mesmo controle sobre o token, a sessão e o único configurações sign-on (SSO) por meio de políticas internas.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="fe1f7-104">toolearn que cada configuração faz, consulte a documentação de saudação [aqui](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="fe1f7-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="fe1f7-105">Configuração de declarações e de tempos de vida de token</span><span class="sxs-lookup"><span data-stu-id="fe1f7-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="fe1f7-106">configurações de saudação toochange em seu tempo de vida de token, você precisa tooadd um `<ClaimsProviders>` elemento no arquivo de parte confiável Olá da política de saudação desejado tooimpact.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="fe1f7-107">Olá `<ClaimsProviders>` elemento é um filho de saudação `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="fe1f7-108">Dentro, você precisará de informações de saudação tooput que afeta o tempo de vida de token.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="fe1f7-109">Olá XML tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="fe1f7-109">hello XML looks like this:</span></span>

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

<span data-ttu-id="fe1f7-110">**Tempos de vida de token de acesso** Olá acesso a vida útil do token pode ser alterado modificando o valor hello dentro de saudação `<Item>` com hello Key = "token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="fe1f7-111">valor padrão de saudação em interna é 3600 segundos (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="fe1f7-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="fe1f7-112">**Vida útil do token ID** vida útil do token ID Olá pode ser alterado modificando o valor hello dentro Olá `<Item>` com hello Key = "id_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="fe1f7-113">valor padrão de saudação em interna é 3600 segundos (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="fe1f7-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="fe1f7-114">**Vida útil do token de atualização** vida útil do token atualização Olá pode ser alterado modificando o valor hello dentro Olá `<Item>` com hello Key = "refresh_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="fe1f7-115">valor padrão de saudação em interna é 1209600 segundos (14 dias).</span><span class="sxs-lookup"><span data-stu-id="fe1f7-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="fe1f7-116">**Atualizar o tempo de vida de janela deslizante token** se quiser tooset um token de atualização do tooyour de tempo de vida janela deslizante, modifique o valor de saudação dentro `<Item>` com hello chave = "rolling_refresh_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="fe1f7-117">Olá valor padrão interno é 7776000 (90 dias).</span><span class="sxs-lookup"><span data-stu-id="fe1f7-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="fe1f7-118">Se você não quiser tooenfore um deslizando o tempo de vida de janela, substitua esta linha com:</span><span class="sxs-lookup"><span data-stu-id="fe1f7-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="fe1f7-119">**Declaração do emissor (iss)** se você quiser toochange Olá emissor (iss) declaração, modifique o valor de saudação dentro Olá `<Item>` com hello Key = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="fe1f7-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="fe1f7-120">são valores aplicáveis Olá `AuthorityAndTenantGuid` e `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="fe1f7-121">**Configuração de declaração que representa a ID de política** opções de saudação para definir esse valor são TFP (diretiva de confiança do framework) e ACR (referência do contexto de autenticação).</span><span class="sxs-lookup"><span data-stu-id="fe1f7-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="fe1f7-122">É recomendável definir essa tooTFP, toodo isso, certifique-se Olá `<Item>` com hello Key = "AuthenticationContextReferenceClaimPattern" existe e é o valor de saudação `None`.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="fe1f7-123">No seu item do `<OutputClaims>`, adicione este elemento:</span><span class="sxs-lookup"><span data-stu-id="fe1f7-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="fe1f7-124">Para o ACR, remover Olá `<Item>` com hello Key = "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="fe1f7-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="fe1f7-125">**Declaração de assunto (sub)** essa opção é padronizada tooObjectID, se você quiser tooswitch isso muito`Not Supported`, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe1f7-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="fe1f7-126">Substituir esta linha</span><span class="sxs-lookup"><span data-stu-id="fe1f7-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="fe1f7-127">com esta linha:</span><span class="sxs-lookup"><span data-stu-id="fe1f7-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="fe1f7-128">Comportamento da sessão e SSO</span><span class="sxs-lookup"><span data-stu-id="fe1f7-128">Session behavior and SSO</span></span>
<span data-ttu-id="fe1f7-129">toochange seu comportamento da sessão e as configurações de SSO, você precisa tooadd um `<UserJourneyBehaviors>` elemento dentro Olá `<RelyingParty>` elemento.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="fe1f7-130">Olá `<UserJourneyBehaviors>` elemento deve seguir imediatamente Olá `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="fe1f7-131">Olá dentro de sua `<UserJourneyBehavors>` elemento deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="fe1f7-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="fe1f7-132">**Configuração de logon único (SSO)** toochange Olá única configuração de logon, é necessário que o valor Olá toomodify `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="fe1f7-133">são valores aplicáveis Olá `Tenant`, `Application`, `Policy` e `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="fe1f7-134">**Aplicativo Web do tempo de vida da sessão (minutos)** toochange Olá Olá web app duração da sessão, você precisa que o valor de toomodify de saudação `<SessionExpiryInSeconds>` elemento.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="fe1f7-135">valor padrão de saudação em políticas internas é 86400 segundos (1440 minutos).</span><span class="sxs-lookup"><span data-stu-id="fe1f7-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="fe1f7-136">**Tempo limite de sessão do aplicativo Web** toochange Olá web app tempo limite da sessão, é necessário que o valor Olá toomodify `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="fe1f7-137">são valores aplicáveis Olá `Absolute` e `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="fe1f7-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
