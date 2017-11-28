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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="58c60-103">Passo a passo: integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração</span><span class="sxs-lookup"><span data-stu-id="58c60-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="58c60-104">A IEF (Estrutura de Experiência de Identidade) subjacente ao Azure AD B2C (Azure Active Directory B2C) permite que o desenvolvedor de identidade integre uma interação com uma API RESTful em um percurso do usuário.</span><span class="sxs-lookup"><span data-stu-id="58c60-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="58c60-105">Ao final deste passo a passo, você estará apto a criar um percurso do usuário do Azure AD B2C que interage com serviços RESTful.</span><span class="sxs-lookup"><span data-stu-id="58c60-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="58c60-106">A IEF envia dados em declarações e recebe dados de volta em declarações.</span><span class="sxs-lookup"><span data-stu-id="58c60-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="58c60-107">A troca de declarações da API REST:</span><span class="sxs-lookup"><span data-stu-id="58c60-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="58c60-108">Pode ser projetada como uma etapa de orquestração.</span><span class="sxs-lookup"><span data-stu-id="58c60-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="58c60-109">Pode disparar uma ação externa.</span><span class="sxs-lookup"><span data-stu-id="58c60-109">Can trigger an external action.</span></span> <span data-ttu-id="58c60-110">Por exemplo, ela pode registrar um evento em um banco de dados externo.</span><span class="sxs-lookup"><span data-stu-id="58c60-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="58c60-111">Pode ser usada para buscar um valor e, em seguida, armazená-lo no banco de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="58c60-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="58c60-112">Você pode usar as declarações recebidas posteriormente para alterar o fluxo de execução.</span><span class="sxs-lookup"><span data-stu-id="58c60-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="58c60-113">Você também pode projetar a interação como um perfil de validação.</span><span class="sxs-lookup"><span data-stu-id="58c60-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="58c60-114">Para obter mais informações, veja [Passo a passo: integrar as trocas de declarações da API REST no seu percurso do usuário do Azure AD B2C como validação sobre a entrada do usuário](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="58c60-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="58c60-115">O cenário é aquele em que, quando um usuário realiza uma edição de perfil, desejamos:</span><span class="sxs-lookup"><span data-stu-id="58c60-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="58c60-116">Procurar pelo usuário em um sistema externo.</span><span class="sxs-lookup"><span data-stu-id="58c60-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="58c60-117">Obter a cidade em que o usuário está registrado.</span><span class="sxs-lookup"><span data-stu-id="58c60-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="58c60-118">Retornar o atributo para o aplicativo como uma declaração.</span><span class="sxs-lookup"><span data-stu-id="58c60-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58c60-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="58c60-119">Prerequisites</span></span>

- <span data-ttu-id="58c60-120">Um locatário do Azure AD B2C configurado para concluir uma inscrição/entrada de conta local, conforme descrito em [Introdução](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="58c60-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="58c60-121">Um ponto de extremidade de API REST com o qual se irá interagir.</span><span class="sxs-lookup"><span data-stu-id="58c60-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="58c60-122">Este passo a passo usa um webhook de aplicativo de funções simples do Azure como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="58c60-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="58c60-123">*Recomendado*: conclua o [passo a passo da troca de declarações da API REST como uma etapa de validação](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="58c60-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="58c60-124">Etapa 1: preparar a função da API REST</span><span class="sxs-lookup"><span data-stu-id="58c60-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="58c60-125">A configuração das funções da API REST está fora do escopo deste artigo.</span><span class="sxs-lookup"><span data-stu-id="58c60-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="58c60-126">O [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece um kit de ferramentas excelente para criar serviços RESTful na nuvem.</span><span class="sxs-lookup"><span data-stu-id="58c60-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="58c60-127">Definimos uma função do Azure que recebe uma declaração chamada `email` e, em seguida, retorna a declaração `city` com o valor atribuído de `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="58c60-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="58c60-128">A função do Azure de exemplo está no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="58c60-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="58c60-129">A declaração `userMessage` que a função do Azure retorna é opcional nesse contexto e a IEF vai ignorá-la.</span><span class="sxs-lookup"><span data-stu-id="58c60-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="58c60-130">Você pode usá-la como uma mensagem passada para o aplicativo e apresentada ao usuário mais tarde.</span><span class="sxs-lookup"><span data-stu-id="58c60-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="58c60-131">Um aplicativo de funções do Azure facilita a obtenção da URL da função, a qual inclui o identificador da função específica.</span><span class="sxs-lookup"><span data-stu-id="58c60-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="58c60-132">Nesse caso, a URL é: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="58c60-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="58c60-133">Você pode usá-la para teste.</span><span class="sxs-lookup"><span data-stu-id="58c60-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="58c60-134">Etapa 2: configurar a troca de declarações da API RESTful como um perfil técnico no arquivo TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="58c60-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="58c60-135">Um perfil técnico é a configuração completa da troca desejada com o serviço RESTful.</span><span class="sxs-lookup"><span data-stu-id="58c60-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="58c60-136">Abra o arquivo TrustFrameworkExtensions.xml e adicione o seguinte trecho de código XML dentro do elemento `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="58c60-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="58c60-137">No XML a seguir, o provedor RESTful `Version=1.0.0.0` é descrito como o protocolo.</span><span class="sxs-lookup"><span data-stu-id="58c60-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="58c60-138">Considere-o como a função que interagirá com o serviço externo.</span><span class="sxs-lookup"><span data-stu-id="58c60-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="58c60-139">O elemento `<InputClaims>` define as declarações que serão enviadas pela IEF para o serviço REST.</span><span class="sxs-lookup"><span data-stu-id="58c60-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="58c60-140">Neste exemplo, o conteúdo da declaração `givenName` será enviado para o serviço REST como a declaração `email`.</span><span class="sxs-lookup"><span data-stu-id="58c60-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="58c60-141">O elemento `<OutputClaims>` define as declarações que a IEF espera do serviço REST.</span><span class="sxs-lookup"><span data-stu-id="58c60-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="58c60-142">Independentemente do número de declarações recebidas, a IEF usará apenas aquelas identificadas aqui.</span><span class="sxs-lookup"><span data-stu-id="58c60-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="58c60-143">Neste exemplo, uma declaração recebida como `city` será mapeada para uma declaração da IEF chamada `city`.</span><span class="sxs-lookup"><span data-stu-id="58c60-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="58c60-144">Etapa 3: adicionar a nova declaração `city` ao esquema do arquivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="58c60-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="58c60-145">A declaração `city` não está definida em nenhum outro lugar no nosso esquema.</span><span class="sxs-lookup"><span data-stu-id="58c60-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="58c60-146">Portanto, adicione uma definição dentro do elemento `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="58c60-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="58c60-147">Você encontra esse elemento no início do arquivo TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="58c60-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="58c60-148">Etapa 4: incluir a troca de declarações do serviço REST como uma etapa de orquestração em seu percurso do usuário de edição de perfil no TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="58c60-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="58c60-149">Adicione uma etapa ao percurso do usuário de edição de perfil após a autenticação do usuário (etapas de orquestração 1 a 4 no XML a seguir) e depois que ele tenha fornecido as informações de perfil atualizado (etapa 5).</span><span class="sxs-lookup"><span data-stu-id="58c60-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="58c60-150">Há muitos casos de uso em que a chamada à API REST pode ser usada como uma etapa de orquestração.</span><span class="sxs-lookup"><span data-stu-id="58c60-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="58c60-151">Como uma etapa de orquestração, ela pode ser usada como uma atualização para um sistema externo depois que um usuário tenha concluído uma tarefa com êxito, como o primeiro registro, ou como uma atualização de perfil para manter as informações sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="58c60-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="58c60-152">Nesse caso, ela é usada para aumentar as informações fornecidas para o aplicativo depois da edição do perfil.</span><span class="sxs-lookup"><span data-stu-id="58c60-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="58c60-153">Copie o código XML do percurso do usuário de edição de perfil do arquivo TrustFrameworkBase.xml para o seu arquivo TrustFrameworkExtensions.xml dentro do elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="58c60-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="58c60-154">Em seguida, faça a modificação conforme a etapa 6.</span><span class="sxs-lookup"><span data-stu-id="58c60-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="58c60-155">Se a ordem não corresponde à sua versão, verifique se você inseriu o código como a etapa antes do tipo `ClaimsExchange` `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="58c60-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="58c60-156">O XML final da jornada do usuário deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="58c60-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="58c60-157">Etapa 5: adicionar a declaração `city` ao seu arquivo de política de terceira parte confiável para que a declaração seja enviada ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="58c60-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="58c60-158">Edite o arquivo RP (terceira parte confiável), ProfileEdit.xml e modifique o elemento `<TechnicalProfile Id="PolicyProfile">` para adicionar o seguinte: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="58c60-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="58c60-159">Depois de adicionar a nova declaração, o perfil técnico terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="58c60-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="58c60-160">Etapa 6: carregar suas alterações e testar</span><span class="sxs-lookup"><span data-stu-id="58c60-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="58c60-161">Substitua as versões existentes da política.</span><span class="sxs-lookup"><span data-stu-id="58c60-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="58c60-162">(Opcional:) Salve a versão existente (baixando-a) do seu arquivo de extensões antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="58c60-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="58c60-163">Para reduzir a complexidade inicial, é recomendável que você não carregue várias versões do arquivo de extensões.</span><span class="sxs-lookup"><span data-stu-id="58c60-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="58c60-164">(Opcional:) Renomeie a nova versão da ID de política do arquivo de edição de política alterando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="58c60-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="58c60-165">Carregue o arquivo de extensões.</span><span class="sxs-lookup"><span data-stu-id="58c60-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="58c60-166">Carregue o arquivo RP de edição de política.</span><span class="sxs-lookup"><span data-stu-id="58c60-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="58c60-167">Use **Executar Agora** para testar a política.</span><span class="sxs-lookup"><span data-stu-id="58c60-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="58c60-168">Examine o token que a IEF retorna ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58c60-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="58c60-169">Se tudo estiver configurado corretamente, o token incluirá a nova declaração `city`, com o valor `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="58c60-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="58c60-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58c60-170">Next steps</span></span>

[<span data-ttu-id="58c60-171">Usar uma API REST como uma etapa de validação</span><span class="sxs-lookup"><span data-stu-id="58c60-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="58c60-172">Modificar a edição de perfil para coletar informações adicionais de seus usuários</span><span class="sxs-lookup"><span data-stu-id="58c60-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
