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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="2ae4e-103">Passo a passo: Integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como validação na entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="2ae4e-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="2ae4e-104">saudação do Framework de experiência de identidade (IEF) que serve como base para o Azure Active Directory B2C (Azure AD B2C) habilita Olá identidade desenvolvedor toointegrate uma interação com uma API RESTful em uma viagem de usuário.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="2ae4e-105">Final Olá deste passo a passo, você será capaz de toocreate uma jornada de usuário do Azure AD B2C interage com os serviços RESTful.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="2ae4e-106">Olá IEF envia dados em declarações e recebe dados de volta em declarações.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="2ae4e-107">interação de saudação com hello API:</span><span class="sxs-lookup"><span data-stu-id="2ae4e-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="2ae4e-108">Pode ser criada como uma troca de declarações da API REST ou como um perfil de validação, que ocorre em uma etapa de orquestração.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="2ae4e-109">Geralmente valida a entrada do usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-109">Typically validates input from hello user.</span></span> <span data-ttu-id="2ae4e-110">Se o valor de saudação do usuário Olá for rejeitada, o usuário Olá pode tentar novamente tooenter um valor válido com hello oportunidade tooreturn uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="2ae4e-111">Você também pode criar interação hello como uma etapa de orquestração.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="2ae4e-112">Para obter mais informações, consulte [Passo a passo: Integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2ae4e-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="2ae4e-113">Para exemplo de perfil de validação de hello, usaremos jornada de usuário de edição de perfil Olá no arquivo de pacote de inicializador Olá ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="2ae4e-114">Podemos verificar esse nome hello fornecido pelo usuário Olá no perfil Olá edição não é parte de uma lista de exclusão.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ae4e-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2ae4e-115">Prerequisites</span></span>

- <span data-ttu-id="2ae4e-116">Um toocomplete de locatário do Azure AD B2C uma conta local de entrada-o/entrada, conforme descrito em [Introdução](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2ae4e-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="2ae4e-117">Um ponto de extremidade do REST API toointeract com.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="2ae4e-118">Para este passo a passo, criamos um site de demonstração chamado [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) com um serviço de API REST.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="2ae4e-119">Etapa 1: Preparar a função de API REST hello</span><span class="sxs-lookup"><span data-stu-id="2ae4e-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="2ae4e-120">A instalação das funções de API REST está fora do escopo deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="2ae4e-121">[As funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece um excelente toolkit toocreate os serviços RESTful na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="2ae4e-122">Criamos uma função do Azure que recebe uma declaração esperada como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="2ae4e-123">função Hello valida se existe essa declaração.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="2ae4e-124">Você pode acessar o código de função do Azure concluída Olá em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="2ae4e-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="2ae4e-125">Olá IEF espera Olá `userMessage` declaração que Olá função do Azure retorna.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="2ae4e-126">Esta declaração será apresentada como um usuário de toohello de cadeia de caracteres se a validação de Olá falhar, como quando um status de 409 conflito é retornado no hello anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="2ae4e-127">Etapa 2: Configurar Olá API RESTful declarações exchange como um perfil técnico em seu arquivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="2ae4e-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="2ae4e-128">Um perfil técnico é a configuração completa de saudação do exchange Olá desejado com hello serviço RESTful.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="2ae4e-129">Abrir o arquivo de TrustFrameworkExtensions.xml hello e adicione Olá seguindo o trecho XML dentro de saudação `<ClaimsProviders>` elemento.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="2ae4e-130">Em Olá RESTful provedor XML a seguir `Version=1.0.0.0` é descrito como protocolo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="2ae4e-131">Considere-a como a função hello irá interagir com o serviço externo hello.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="2ae4e-132">Olá `InputClaims` elemento define declarações Olá Olá serviço REST toohello IEF serão enviadas.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="2ae4e-133">Neste exemplo, Olá conteúdo da declaração Olá `givenName` receberá o serviço REST toohello como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="2ae4e-134">Neste exemplo, Olá que IEF não espera declarações novamente.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="2ae4e-135">Em vez disso, ele aguarda uma resposta do serviço REST hello e funciona com base em códigos de status de saudação que recebe.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="2ae4e-136">Etapa 3: Incluir Olá serviço RESTful declarações exchange auto-declaradas perfil técnica em que você deseja toovalidate entrada do usuário de saudação</span><span class="sxs-lookup"><span data-stu-id="2ae4e-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="2ae4e-137">uso mais comum de saudação de etapa de validação de saudação é na interação Olá com um usuário.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="2ae4e-138">Todas as interações onde o usuário Olá é esperado tooprovide de entrada são *automático declarada perfis técnicos*.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="2ae4e-139">Neste exemplo, vamos adicionar perfil de autoatendimento Asserted ProfileUpdate de toohello validação de saudação técnica.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="2ae4e-140">Isso é o perfil de técnicas de Olá Olá arquivo de política de terceira parte confiável (RP) `Profile Edit` usa.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="2ae4e-141">tooadd Olá declarações exchange toohello automático declarada perfil técnico:</span><span class="sxs-lookup"><span data-stu-id="2ae4e-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="2ae4e-142">Abrir arquivo de TrustFrameworkBase.xml hello e procure `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="2ae4e-143">Examinar a configuração de saudação do perfil técnico.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="2ae4e-144">Observe como exchange Olá com usuário Olá é definido como declarações que serão solicitadas do usuário da saudação (declarações de entrada) e que será esperado do provedor de auto-declaradas hello (declarações de saída).</span><span class="sxs-lookup"><span data-stu-id="2ae4e-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="2ae4e-145">Pesquise `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate` e observe que esse perfil é invocado como a etapa de orquestração 6 do `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="2ae4e-146">Etapa 4: Carregar e testar o arquivo de política do hello perfil Editar RP</span><span class="sxs-lookup"><span data-stu-id="2ae4e-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="2ae4e-147">Carregar Olá nova versão do arquivo de TrustFrameworkExtensions.xml hello.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="2ae4e-148">Use **executar agora** perfil de saudação tootest editar o arquivo de política do RP.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="2ae4e-149">Testar a validação de hello, fornecendo um dos nomes de saudação existente (por exemplo, mcvinny) em Olá **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="2ae4e-150">Se tudo está configurado corretamente, você deve receber uma mensagem que notifica o usuário Olá que marca de player Olá já está em uso.</span><span class="sxs-lookup"><span data-stu-id="2ae4e-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ae4e-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ae4e-151">Next steps</span></span>

[<span data-ttu-id="2ae4e-152">Modificar Olá perfil usuário e editar registro toogather informações adicionais de seus usuários</span><span class="sxs-lookup"><span data-stu-id="2ae4e-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="2ae4e-153">Passo a passo: integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração</span><span class="sxs-lookup"><span data-stu-id="2ae4e-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
