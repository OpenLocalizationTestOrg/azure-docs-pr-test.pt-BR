---
title: "Azure Active Directory B2C: as trocas de declarações da API REST como uma etapa de orquestração | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C que se integram com uma API"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="88b22-103">Passo a passo: integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração</span><span class="sxs-lookup"><span data-stu-id="88b22-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="88b22-104">saudação do Framework de experiência de identidade (IEF) que serve como base para o Azure Active Directory B2C (Azure AD B2C) habilita Olá identidade desenvolvedor toointegrate uma interação com uma API RESTful em uma viagem de usuário.</span><span class="sxs-lookup"><span data-stu-id="88b22-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="88b22-105">Final Olá deste passo a passo, você será capaz de toocreate uma jornada de usuário do Azure AD B2C interage com os serviços RESTful.</span><span class="sxs-lookup"><span data-stu-id="88b22-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="88b22-106">Olá IEF envia dados em declarações e recebe dados de volta em declarações.</span><span class="sxs-lookup"><span data-stu-id="88b22-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="88b22-107">Olá exchange de declarações de API REST:</span><span class="sxs-lookup"><span data-stu-id="88b22-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="88b22-108">Pode ser projetada como uma etapa de orquestração.</span><span class="sxs-lookup"><span data-stu-id="88b22-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="88b22-109">Pode disparar uma ação externa.</span><span class="sxs-lookup"><span data-stu-id="88b22-109">Can trigger an external action.</span></span> <span data-ttu-id="88b22-110">Por exemplo, ela pode registrar um evento em um banco de dados externo.</span><span class="sxs-lookup"><span data-stu-id="88b22-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="88b22-111">Pode ser usado toofetch um valor e, em seguida, armazená-lo no banco de dados de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="88b22-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="88b22-112">Você pode usar as declarações recebida de saudação fluxo de saudação toochange posterior de execução.</span><span class="sxs-lookup"><span data-stu-id="88b22-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="88b22-113">Você também pode criar interação hello como um perfil de validação.</span><span class="sxs-lookup"><span data-stu-id="88b22-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="88b22-114">Para obter mais informações, veja [Passo a passo: integrar as trocas de declarações da API REST no seu percurso do usuário do Azure AD B2C como validação sobre a entrada do usuário](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="88b22-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="88b22-115">cenário de saudação é que quando um usuário executa uma edição de perfil, desejamos:</span><span class="sxs-lookup"><span data-stu-id="88b22-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="88b22-116">Pesquise Olá usuário em um sistema externo.</span><span class="sxs-lookup"><span data-stu-id="88b22-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="88b22-117">Obter cidade Olá onde o usuário está registrado.</span><span class="sxs-lookup"><span data-stu-id="88b22-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="88b22-118">Retorne o aplicativo toohello atributo como uma declaração.</span><span class="sxs-lookup"><span data-stu-id="88b22-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88b22-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="88b22-119">Prerequisites</span></span>

- <span data-ttu-id="88b22-120">Um toocomplete de locatário do Azure AD B2C uma conta local de entrada-o/entrada, conforme descrito em [Introdução](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="88b22-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="88b22-121">Um ponto de extremidade do REST API toointeract com.</span><span class="sxs-lookup"><span data-stu-id="88b22-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="88b22-122">Este passo a passo usa um webhook de aplicativo de funções simples do Azure como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="88b22-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="88b22-123">*Recomendado*: Olá completa [exchange passo a passo como uma etapa de validação de solicitações de API REST](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="88b22-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="88b22-124">Etapa 1: Preparar a função de API REST hello</span><span class="sxs-lookup"><span data-stu-id="88b22-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="88b22-125">A instalação das funções de API REST está fora do escopo deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="88b22-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="88b22-126">[As funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece um excelente toolkit toocreate os serviços RESTful na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="88b22-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="88b22-127">Configuramos a uma função do Azure que recebe uma declaração chamada `email`, e, em seguida, retorna Olá declaração `city` com valor de saudação atribuída de `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="88b22-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="88b22-128">exemplo Hello função do Azure está em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="88b22-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="88b22-129">Olá `userMessage` declaração que Olá retorna a função do Azure é opcional neste contexto, e Olá IEF irá ignorar essa configuração.</span><span class="sxs-lookup"><span data-stu-id="88b22-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="88b22-130">Você pode potencialmente usá-lo como uma mensagem passada aplicativo toohello e apresentados toohello usuário mais tarde.</span><span class="sxs-lookup"><span data-stu-id="88b22-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

<span data-ttu-id="88b22-131">Um aplicativo de função do Azure torna fácil tooget Olá função URL, que inclui o identificador de saudação de função específica de saudação.</span><span class="sxs-lookup"><span data-stu-id="88b22-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="88b22-132">Nesse caso, é a URL de saudação: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="88b22-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="88b22-133">Você pode usá-la para teste.</span><span class="sxs-lookup"><span data-stu-id="88b22-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="88b22-134">Etapa 2: Configurar Olá API RESTful declarações exchange como um perfil técnico em seu arquivo TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="88b22-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="88b22-135">Um perfil técnico é a configuração completa de saudação do exchange Olá desejado com hello serviço RESTful.</span><span class="sxs-lookup"><span data-stu-id="88b22-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="88b22-136">Abrir o arquivo de TrustFrameworkExtensions.xml hello e adicione Olá seguindo o trecho XML dentro de saudação `<ClaimsProvider>` elemento.</span><span class="sxs-lookup"><span data-stu-id="88b22-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="88b22-137">Em Olá RESTful provedor XML a seguir `Version=1.0.0.0` é descrito como protocolo de saudação.</span><span class="sxs-lookup"><span data-stu-id="88b22-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="88b22-138">Considere-a como a função hello irá interagir com o serviço externo hello.</span><span class="sxs-lookup"><span data-stu-id="88b22-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="88b22-139">Olá `<InputClaims>` elemento define declarações Olá Olá serviço REST toohello IEF serão enviadas.</span><span class="sxs-lookup"><span data-stu-id="88b22-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="88b22-140">Neste exemplo, Olá conteúdo da declaração Olá `givenName` será enviado serviço REST de toohello como Olá declaração `email`.</span><span class="sxs-lookup"><span data-stu-id="88b22-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="88b22-141">Olá `<OutputClaims>` elemento define Olá declarações que Olá IEF espera do serviço REST de saudação do.</span><span class="sxs-lookup"><span data-stu-id="88b22-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="88b22-142">Independentemente do número de saudação de declarações que são recebidos, Olá IEF usará somente os identificado aqui.</span><span class="sxs-lookup"><span data-stu-id="88b22-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="88b22-143">Neste exemplo, uma declaração recebida como `city` será chamada tooan mapeada IEF declaração `city`.</span><span class="sxs-lookup"><span data-stu-id="88b22-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="88b22-144">Etapa 3: Adicionar nova declaração de saudação `city` toohello esquema do arquivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="88b22-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="88b22-145">Olá declaração `city` ainda não está definido em qualquer lugar no nosso esquema.</span><span class="sxs-lookup"><span data-stu-id="88b22-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="88b22-146">Portanto, adicione uma definição de dentro do elemento de saudação `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="88b22-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="88b22-147">Você pode encontrar esse elemento no início de saudação do arquivo de TrustFrameworkExtensions.xml hello.</span><span class="sxs-lookup"><span data-stu-id="88b22-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="88b22-148">Etapa 4: Incluir Olá REST serviço declarações exchange como uma etapa de orquestração em sua jornada de usuário de edição de perfil em TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="88b22-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="88b22-149">Adicionar uma etapa toohello perfil Editar usuário jornada depois Olá usuário foi autenticado (orquestração etapas 1 a 4 Olá XML a seguir) e Olá usuário forneceu informações de perfil Olá atualizado (etapa 5).</span><span class="sxs-lookup"><span data-stu-id="88b22-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="88b22-150">Há muitos casos de uso onde Olá chamada à API REST pode ser usada como uma etapa de orquestração.</span><span class="sxs-lookup"><span data-stu-id="88b22-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="88b22-151">Como uma etapa de orquestração, que pode ser usado como um sistema externo de tooan atualização depois que um usuário for concluída com êxito uma tarefa, como o registro pela primeira vez, ou como um perfil de atualização tookeep informações sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="88b22-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="88b22-152">Nesse caso, é usado tooaugment Olá informações toohello aplicativo depois de editar o perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="88b22-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="88b22-153">Copiar Olá perfil Editar código XML do usuário jornada de saudação TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml arquivo dentro de saudação `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="88b22-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="88b22-154">Em seguida, fazer a modificação de saudação na etapa 6.</span><span class="sxs-lookup"><span data-stu-id="88b22-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="88b22-155">Se a ordem de saudação não coincide com a versão, certifique-se de que você inserir o código de saudação como etapa Olá antes de saudação `ClaimsExchange` tipo `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="88b22-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="88b22-156">Olá XML final jornada de usuário Olá deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="88b22-156">hello final XML for hello user journey should look like this:</span></span>

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="88b22-157">Etapa 5: Adicionar Olá declaração `city` tooyour terceira política de parte do arquivo para declaração de saudação é enviada tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="88b22-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="88b22-158">Edite o arquivo do ProfileEdit.xml terceira parte confiável (RP) e modificar Olá `<TechnicalProfile Id="PolicyProfile">` seguinte de saudação do elemento tooadd: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="88b22-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="88b22-159">Depois de adicionar nova declaração de hello, perfil técnico Olá terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="88b22-159">After you add hello new claim, hello technical profile looks like this:</span></span>

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="88b22-160">Etapa 6: carregar suas alterações e testar</span><span class="sxs-lookup"><span data-stu-id="88b22-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="88b22-161">Substitua as versões existentes da política de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="88b22-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="88b22-162">(Opcional:) Salve versão existente da saudação (Baixando) do seu arquivo de extensões antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="88b22-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="88b22-163">tookeep saudação inicial complexidade baixa, é recomendável que você não carregar várias versões do arquivo de extensões de saudação.</span><span class="sxs-lookup"><span data-stu-id="88b22-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="88b22-164">(Opcional:) Renomeie a nova versão Olá Olá ID da política de arquivo de edição de política de saudação alterando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="88b22-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="88b22-165">Carregar arquivo de extensões de saudação.</span><span class="sxs-lookup"><span data-stu-id="88b22-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="88b22-166">Carregar arquivo do hello política Editar RP.</span><span class="sxs-lookup"><span data-stu-id="88b22-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="88b22-167">Use **executar agora** tootest política de saudação.</span><span class="sxs-lookup"><span data-stu-id="88b22-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="88b22-168">Token de saudação de revisão que Olá IEF retorna toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88b22-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="88b22-169">Se tudo está configurado corretamente, o token Olá incluirá a nova declaração de saudação `city`, com valor de saudação `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="88b22-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="88b22-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88b22-170">Next steps</span></span>

[<span data-ttu-id="88b22-171">Usar uma API REST como uma etapa de validação</span><span class="sxs-lookup"><span data-stu-id="88b22-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="88b22-172">Modificar Olá perfil Editar toogather informações adicionais de seus usuários</span><span class="sxs-lookup"><span data-stu-id="88b22-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
