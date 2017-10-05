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
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="6d0d4-102">Azure Active Directory B2C: Gerenciar a personalização de SSO e de tokens com políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="6d0d4-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="6d0d4-103">Usar políticas personalizadas fornece algum controle sobre seu token, sessão e configurações de logon único (SSO) por meio de políticas internas.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="6d0d4-104">Para saber o que faz cada configuração, veja a documentação [aqui](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="6d0d4-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="6d0d4-105">Configuração de declarações e de tempos de vida de token</span><span class="sxs-lookup"><span data-stu-id="6d0d4-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="6d0d4-106">Para alterar as configurações em seus tempos de vida de token, você precisa adicionar um elemento `<ClaimsProviders>` ao arquivo de terceira parte confiável da política que você deseja afetar.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="6d0d4-107">O elemento `<ClaimsProviders>` é filho do `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="6d0d4-108">Lá, você precisará colocar as informações que afetam os tempos de vida de token.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="6d0d4-109">O XML tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="6d0d4-109">The XML looks like this:</span></span>

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

<span data-ttu-id="6d0d4-110">**Tempos de vida de token de acesso** O tempo de vida de token de acesso pode ser alterado modificando o valor dentro do `<Item>` com Key="token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="6d0d4-111">O valor padrão interno é de 3600 segundos (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="6d0d4-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="6d0d4-112">**Tempo de vida do token de ID** O tempo de vida do token de ID pode ser alterado por meio da modificação do valor de `<Item>` comKey="id_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="6d0d4-113">O valor padrão interno é de 3600 segundos (60 minutos).</span><span class="sxs-lookup"><span data-stu-id="6d0d4-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="6d0d4-114">**Tempo de vida do token de atualização** O tempo de vida do token de atualização pode ser alterado por meio da modificação do valor de `<Item>` com Key="refresh_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="6d0d4-115">O valor padrão interno é 1209600 segundos (14 dias).</span><span class="sxs-lookup"><span data-stu-id="6d0d4-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="6d0d4-116">**Atualizar o tempo de vida de janela deslizante token** Se você deseja definir um tempo de vida de janela deslizante para o token de atualização, modifique o valor de `<Item>` com Key="rolling_refresh_token_lifetime_secs" em segundos.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="6d0d4-117">O valor padrão interno é 7776000 (90 dias).</span><span class="sxs-lookup"><span data-stu-id="6d0d4-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="6d0d4-118">Se você não quiser impor um tempo de vida de janela deslizante, substitua essa linha por:</span><span class="sxs-lookup"><span data-stu-id="6d0d4-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="6d0d4-119">**Declaração do emissor (iss)** Se você quiser alterar a declaração do emissor (iss), modifique o valor no `<Item>` com Key="IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="6d0d4-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="6d0d4-120">Os valores aplicáveis são `AuthorityAndTenantGuid` e `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="6d0d4-121">**Configuração de declaração que representa a ID de política** As opções para definir esse valor são TFP (política de confiança da estrutura) e ACR (referência do contexto de autenticação).</span><span class="sxs-lookup"><span data-stu-id="6d0d4-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="6d0d4-122">É recomendável definir isso como TFP; para fazer isso, verifique se o `<Item>` com Key="AuthenticationContextReferenceClaimPattern" existe e se o valor é `None`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="6d0d4-123">No seu item do `<OutputClaims>`, adicione este elemento:</span><span class="sxs-lookup"><span data-stu-id="6d0d4-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="6d0d4-124">Para o ACR, remova o `<Item>` com Key="AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="6d0d4-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="6d0d4-125">**Declaração de assunto (sub)** Essa opção é padronizada para a ObjectID, se você quiser trocar para `Not Supported`, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6d0d4-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="6d0d4-126">Substituir esta linha</span><span class="sxs-lookup"><span data-stu-id="6d0d4-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="6d0d4-127">com esta linha:</span><span class="sxs-lookup"><span data-stu-id="6d0d4-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="6d0d4-128">Comportamento da sessão e SSO</span><span class="sxs-lookup"><span data-stu-id="6d0d4-128">Session behavior and SSO</span></span>
<span data-ttu-id="6d0d4-129">Para alterar o comportamento da sessão e as configurações de SSO, será necessário adicionar um elemento `<UserJourneyBehaviors>` ao elemento `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="6d0d4-130">O elemento `<UserJourneyBehaviors>` deve seguir imediatamente o `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="6d0d4-131">O interior do seu elemento `<UserJourneyBehavors>` deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="6d0d4-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="6d0d4-132">**Configuração de logon único (SSO)** Para alterar a configuração de logon único, você precisa modificar o valor de `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="6d0d4-133">Os valores aplicáveis são `Tenant`, `Application`, `Policy` e `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="6d0d4-134">**Tempo de vida de sessão do aplicativo Web (minutos)** Para alterar o tempo de vida de sessão do aplicativo Web, você precisa modificar o valor do elemento `<SessionExpiryInSeconds>`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="6d0d4-135">O valor padrão em políticas internas é de 86400 segundos (1440 minutos).</span><span class="sxs-lookup"><span data-stu-id="6d0d4-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="6d0d4-136">**Tempo limite de sessão de aplicativo Web** Para alterar o tempo limite de sessão do aplicativo Web, será necessário modificar o valor de `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="6d0d4-137">Os valores aplicáveis são `Absolute` e `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-137">The applicable values are `Absolute` and `Rolling`.</span></span>
