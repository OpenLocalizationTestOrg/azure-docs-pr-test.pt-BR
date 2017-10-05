---
title: "Azure Active Directory B2C: Trocas de declarações da API REST como validação | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C"
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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="42632-103">Passo a passo: Integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como validação na entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="42632-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="42632-104">A IEF (Estrutura de Experiência de Identidade) subjacente ao Azure AD B2C (Azure Active Directory B2C) permite que o desenvolvedor de identidade integre uma interação com uma API RESTful em um percurso do usuário.</span><span class="sxs-lookup"><span data-stu-id="42632-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="42632-105">Ao final deste passo a passo, você estará apto a criar um percurso do usuário do Azure AD B2C que interage com serviços RESTful.</span><span class="sxs-lookup"><span data-stu-id="42632-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="42632-106">A IEF envia dados em declarações e recebe dados de volta em declarações.</span><span class="sxs-lookup"><span data-stu-id="42632-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="42632-107">A interação com a API:</span><span class="sxs-lookup"><span data-stu-id="42632-107">The interaction with the API:</span></span>

- <span data-ttu-id="42632-108">Pode ser criada como uma troca de declarações da API REST ou como um perfil de validação, que ocorre em uma etapa de orquestração.</span><span class="sxs-lookup"><span data-stu-id="42632-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="42632-109">Normalmente valida a entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="42632-109">Typically validates input from the user.</span></span> <span data-ttu-id="42632-110">Se o valor do usuário for rejeitado, o usuário poderá tentar inserir um valor válido novamente com a oportunidade de retornar uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="42632-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="42632-111">Você também pode criar a interação como uma etapa de orquestração.</span><span class="sxs-lookup"><span data-stu-id="42632-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="42632-112">Para obter mais informações, consulte [Passo a passo: Integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="42632-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="42632-113">No exemplo de perfil de validação, usaremos o percurso do usuário de edição de perfil no arquivo de starter pack ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="42632-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="42632-114">Podemos verificar que o nome fornecido pelo usuário na edição de perfil não faz parte de uma lista de exclusões.</span><span class="sxs-lookup"><span data-stu-id="42632-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42632-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42632-115">Prerequisites</span></span>

- <span data-ttu-id="42632-116">Um locatário do Azure AD B2C configurado para concluir uma inscrição/entrada de conta local, conforme descrito em [Introdução](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="42632-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="42632-117">Um ponto de extremidade de API REST com o qual se irá interagir.</span><span class="sxs-lookup"><span data-stu-id="42632-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="42632-118">Para este passo a passo, criamos um site de demonstração chamado [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) com um serviço de API REST.</span><span class="sxs-lookup"><span data-stu-id="42632-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="42632-119">Etapa 1: preparar a função da API REST</span><span class="sxs-lookup"><span data-stu-id="42632-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="42632-120">A configuração das funções da API REST está fora do escopo deste artigo.</span><span class="sxs-lookup"><span data-stu-id="42632-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="42632-121">O [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece um kit de ferramentas excelente para criar serviços RESTful na nuvem.</span><span class="sxs-lookup"><span data-stu-id="42632-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="42632-122">Criamos uma função do Azure que recebe uma declaração esperada como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="42632-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="42632-123">A função valida se essa declaração existe.</span><span class="sxs-lookup"><span data-stu-id="42632-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="42632-124">Você pode acessar o código completo de função do Azure no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="42632-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="42632-125">O IEF espera a declaração `userMessage` retornada pela função do Azure.</span><span class="sxs-lookup"><span data-stu-id="42632-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="42632-126">Essa declaração será apresentada como uma cadeia de caracteres para o usuário se a validação falhar, como quando um status de conflito 409 é retornado no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="42632-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="42632-127">Etapa 2: Configurar a troca de declarações da API RESTful como um perfil técnico no arquivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="42632-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="42632-128">Um perfil técnico é a configuração completa da troca desejada com o serviço RESTful.</span><span class="sxs-lookup"><span data-stu-id="42632-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="42632-129">Abra o arquivo TrustFrameworkExtensions.xml e adicione o seguinte trecho de código XML dentro do elemento `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="42632-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="42632-130">No XML a seguir, o provedor RESTful `Version=1.0.0.0` é descrito como o protocolo.</span><span class="sxs-lookup"><span data-stu-id="42632-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="42632-131">Considere-o como a função que interagirá com o serviço externo.</span><span class="sxs-lookup"><span data-stu-id="42632-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="42632-132">O elemento `InputClaims` define as declarações que serão enviadas pela IEF para o serviço REST.</span><span class="sxs-lookup"><span data-stu-id="42632-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="42632-133">Neste exemplo, o conteúdo da declaração `givenName` será enviado para o serviço REST como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="42632-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="42632-134">Neste exemplo, o IEF não espera declarações novamente.</span><span class="sxs-lookup"><span data-stu-id="42632-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="42632-135">Em vez disso, ele aguarda uma resposta do serviço REST e age de acordo com os códigos de status recebidos.</span><span class="sxs-lookup"><span data-stu-id="42632-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="42632-136">Etapa 3: Incluir a troca de declarações do serviço RESTful no perfil técnico autodeclarado no qual você deseja validar a entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="42632-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="42632-137">O uso mais comum da etapa de validação é na interação com um usuário.</span><span class="sxs-lookup"><span data-stu-id="42632-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="42632-138">Todas as interações nas quais o usuário deve fornecer uma entrada são *perfis técnicos autodeclarados*.</span><span class="sxs-lookup"><span data-stu-id="42632-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="42632-139">Para este exemplo, adicionaremos essa validação ao perfil técnico Self-Asserted-ProfileUpdate.</span><span class="sxs-lookup"><span data-stu-id="42632-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="42632-140">Esse é o perfil técnico utilizado pelo arquivo de política de RP (terceira parte confiável) `Profile Edit`.</span><span class="sxs-lookup"><span data-stu-id="42632-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="42632-141">Para adicionar a troca de declarações ao perfil técnico autodeclarado:</span><span class="sxs-lookup"><span data-stu-id="42632-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="42632-142">Abra o arquivo TrustFrameworkBase.xml e pesquise `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="42632-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="42632-143">Examine a configuração desse perfil técnico.</span><span class="sxs-lookup"><span data-stu-id="42632-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="42632-144">Observe como a troca com o usuário é definida como declarações que serão solicitadas ao usuário (declarações de entrada) e declarações esperadas novamente do provedor autodeclarado (declarações de saída).</span><span class="sxs-lookup"><span data-stu-id="42632-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="42632-145">Pesquise `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate` e observe que esse perfil é invocado como a etapa de orquestração 6 do `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="42632-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="42632-146">Etapa 4: Carregar e testar o arquivo de política de RP de edição de perfil</span><span class="sxs-lookup"><span data-stu-id="42632-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="42632-147">Carregue a nova versão do arquivo TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="42632-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="42632-148">Use **Executar agora** para testar o arquivo de política de edição do perfil RP.</span><span class="sxs-lookup"><span data-stu-id="42632-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="42632-149">Teste a validação fornecendo um dos nomes existentes (por exemplo, mcvinny) no campo **Nome Fornecido**.</span><span class="sxs-lookup"><span data-stu-id="42632-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="42632-150">Se tudo estiver configurado corretamente, você deverá receber uma mensagem que notifica o usuário de que a marcação de player já está sendo usada.</span><span class="sxs-lookup"><span data-stu-id="42632-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42632-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42632-151">Next steps</span></span>

[<span data-ttu-id="42632-152">Modificar a edição de perfil e o registro de usuário para coletar informações adicionais dos usuários</span><span class="sxs-lookup"><span data-stu-id="42632-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="42632-153">Passo a passo: integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração</span><span class="sxs-lookup"><span data-stu-id="42632-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
