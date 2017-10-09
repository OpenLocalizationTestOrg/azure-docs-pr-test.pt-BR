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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>Passo a passo: integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração

saudação do Framework de experiência de identidade (IEF) que serve como base para o Azure Active Directory B2C (Azure AD B2C) habilita Olá identidade desenvolvedor toointegrate uma interação com uma API RESTful em uma viagem de usuário.  

Final Olá deste passo a passo, você será capaz de toocreate uma jornada de usuário do Azure AD B2C interage com os serviços RESTful.

Olá IEF envia dados em declarações e recebe dados de volta em declarações. Olá exchange de declarações de API REST:

- Pode ser projetada como uma etapa de orquestração.
- Pode disparar uma ação externa. Por exemplo, ela pode registrar um evento em um banco de dados externo.
- Pode ser usado toofetch um valor e, em seguida, armazená-lo no banco de dados de usuário de saudação.

Você pode usar as declarações recebida de saudação fluxo de saudação toochange posterior de execução.

Você também pode criar interação hello como um perfil de validação. Para obter mais informações, veja [Passo a passo: integrar as trocas de declarações da API REST no seu percurso do usuário do Azure AD B2C como validação sobre a entrada do usuário](active-directory-b2c-rest-api-validation-custom.md).

cenário de saudação é que quando um usuário executa uma edição de perfil, desejamos:

1. Pesquise Olá usuário em um sistema externo.
2. Obter cidade Olá onde o usuário está registrado.
3. Retorne o aplicativo toohello atributo como uma declaração.

## <a name="prerequisites"></a>Pré-requisitos

- Um toocomplete de locatário do Azure AD B2C uma conta local de entrada-o/entrada, conforme descrito em [Introdução](active-directory-b2c-get-started-custom.md).
- Um ponto de extremidade do REST API toointeract com. Este passo a passo usa um webhook de aplicativo de funções simples do Azure como um exemplo.
- *Recomendado*: Olá completa [exchange passo a passo como uma etapa de validação de solicitações de API REST](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>Etapa 1: Preparar a função de API REST hello

> [!NOTE]
> A instalação das funções de API REST está fora do escopo deste artigo hello. [As funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece um excelente toolkit toocreate os serviços RESTful na nuvem hello.

Configuramos a uma função do Azure que recebe uma declaração chamada `email`, e, em seguida, retorna Olá declaração `city` com valor de saudação atribuída de `Redmond`. exemplo Hello função do Azure está em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Olá `userMessage` declaração que Olá retorna a função do Azure é opcional neste contexto, e Olá IEF irá ignorar essa configuração. Você pode potencialmente usá-lo como uma mensagem passada aplicativo toohello e apresentados toohello usuário mais tarde.

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

Um aplicativo de função do Azure torna fácil tooget Olá função URL, que inclui o identificador de saudação de função específica de saudação. Nesse caso, é a URL de saudação: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. Você pode usá-la para teste.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>Etapa 2: Configurar Olá API RESTful declarações exchange como um perfil técnico em seu arquivo TrustFrameworExtensions.xml

Um perfil técnico é a configuração completa de saudação do exchange Olá desejado com hello serviço RESTful. Abrir o arquivo de TrustFrameworkExtensions.xml hello e adicione Olá seguindo o trecho XML dentro de saudação `<ClaimsProvider>` elemento.

> [!NOTE]
> Em Olá RESTful provedor XML a seguir `Version=1.0.0.0` é descrito como protocolo de saudação. Considere-a como a função hello irá interagir com o serviço externo hello. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

Olá `<InputClaims>` elemento define declarações Olá Olá serviço REST toohello IEF serão enviadas. Neste exemplo, Olá conteúdo da declaração Olá `givenName` será enviado serviço REST de toohello como Olá declaração `email`.  

Olá `<OutputClaims>` elemento define Olá declarações que Olá IEF espera do serviço REST de saudação do. Independentemente do número de saudação de declarações que são recebidos, Olá IEF usará somente os identificado aqui. Neste exemplo, uma declaração recebida como `city` será chamada tooan mapeada IEF declaração `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>Etapa 3: Adicionar nova declaração de saudação `city` toohello esquema do arquivo TrustFrameworkExtensions.xml

Olá declaração `city` ainda não está definido em qualquer lugar no nosso esquema. Portanto, adicione uma definição de dentro do elemento de saudação `<BuildingBlocks>`. Você pode encontrar esse elemento no início de saudação do arquivo de TrustFrameworkExtensions.xml hello.

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>Etapa 4: Incluir Olá REST serviço declarações exchange como uma etapa de orquestração em sua jornada de usuário de edição de perfil em TrustFrameworkExtensions.xml

Adicionar uma etapa toohello perfil Editar usuário jornada depois Olá usuário foi autenticado (orquestração etapas 1 a 4 Olá XML a seguir) e Olá usuário forneceu informações de perfil Olá atualizado (etapa 5).

> [!NOTE]
> Há muitos casos de uso onde Olá chamada à API REST pode ser usada como uma etapa de orquestração. Como uma etapa de orquestração, que pode ser usado como um sistema externo de tooan atualização depois que um usuário for concluída com êxito uma tarefa, como o registro pela primeira vez, ou como um perfil de atualização tookeep informações sincronizadas. Nesse caso, é usado tooaugment Olá informações toohello aplicativo depois de editar o perfil de saudação.

Copiar Olá perfil Editar código XML do usuário jornada de saudação TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml arquivo dentro de saudação `<UserJourneys>` elemento. Em seguida, fazer a modificação de saudação na etapa 6.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Se a ordem de saudação não coincide com a versão, certifique-se de que você inserir o código de saudação como etapa Olá antes de saudação `ClaimsExchange` tipo `SendClaims`.

Olá XML final jornada de usuário Olá deve ser assim:

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>Etapa 5: Adicionar Olá declaração `city` tooyour terceira política de parte do arquivo para declaração de saudação é enviada tooyour aplicativo

Edite o arquivo do ProfileEdit.xml terceira parte confiável (RP) e modificar Olá `<TechnicalProfile Id="PolicyProfile">` seguinte de saudação do elemento tooadd: `<OutputClaim ClaimTypeReferenceId="city" />`.

Depois de adicionar nova declaração de hello, perfil técnico Olá terá esta aparência:

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

## <a name="step-6-upload-your-changes-and-test"></a>Etapa 6: carregar suas alterações e testar

Substitua as versões existentes da política de Olá Olá.

1.  (Opcional:) Salve versão existente da saudação (Baixando) do seu arquivo de extensões antes de continuar. tookeep saudação inicial complexidade baixa, é recomendável que você não carregar várias versões do arquivo de extensões de saudação.
2.  (Opcional:) Renomeie a nova versão Olá Olá ID da política de arquivo de edição de política de saudação alterando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Carregar arquivo de extensões de saudação.
4.  Carregar arquivo do hello política Editar RP.
5.  Use **executar agora** tootest política de saudação. Token de saudação de revisão que Olá IEF retorna toohello aplicativo.

Se tudo está configurado corretamente, o token Olá incluirá a nova declaração de saudação `city`, com valor de saudação `Redmond`.

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

## <a name="next-steps"></a>Próximas etapas

[Usar uma API REST como uma etapa de validação](active-directory-b2c-rest-api-validation-custom.md)

[Modificar Olá perfil Editar toogather informações adicionais de seus usuários](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
