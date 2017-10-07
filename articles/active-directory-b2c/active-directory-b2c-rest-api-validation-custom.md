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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>Passo a passo: Integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como validação na entrada do usuário

saudação do Framework de experiência de identidade (IEF) que serve como base para o Azure Active Directory B2C (Azure AD B2C) habilita Olá identidade desenvolvedor toointegrate uma interação com uma API RESTful em uma viagem de usuário.  

Final Olá deste passo a passo, você será capaz de toocreate uma jornada de usuário do Azure AD B2C interage com os serviços RESTful.

Olá IEF envia dados em declarações e recebe dados de volta em declarações. interação de saudação com hello API:

- Pode ser criada como uma troca de declarações da API REST ou como um perfil de validação, que ocorre em uma etapa de orquestração.
- Geralmente valida a entrada do usuário de saudação. Se o valor de saudação do usuário Olá for rejeitada, o usuário Olá pode tentar novamente tooenter um valor válido com hello oportunidade tooreturn uma mensagem de erro.

Você também pode criar interação hello como uma etapa de orquestração. Para obter mais informações, consulte [Passo a passo: Integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração](active-directory-b2c-rest-api-step-custom.md).

Para exemplo de perfil de validação de hello, usaremos jornada de usuário de edição de perfil Olá no arquivo de pacote de inicializador Olá ProfileEdit.xml.

Podemos verificar esse nome hello fornecido pelo usuário Olá no perfil Olá edição não é parte de uma lista de exclusão.

## <a name="prerequisites"></a>Pré-requisitos

- Um toocomplete de locatário do Azure AD B2C uma conta local de entrada-o/entrada, conforme descrito em [Introdução](active-directory-b2c-get-started-custom.md).
- Um ponto de extremidade do REST API toointeract com. Para este passo a passo, criamos um site de demonstração chamado [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) com um serviço de API REST.

## <a name="step-1-prepare-hello-rest-api-function"></a>Etapa 1: Preparar a função de API REST hello

> [!NOTE]
> A instalação das funções de API REST está fora do escopo deste artigo hello. [As funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) fornece um excelente toolkit toocreate os serviços RESTful na nuvem hello.

Criamos uma função do Azure que recebe uma declaração esperada como `playerTag`. função Hello valida se existe essa declaração. Você pode acessar o código de função do Azure concluída Olá em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

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

Olá IEF espera Olá `userMessage` declaração que Olá função do Azure retorna. Esta declaração será apresentada como um usuário de toohello de cadeia de caracteres se a validação de Olá falhar, como quando um status de 409 conflito é retornado no hello anterior de exemplo.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>Etapa 2: Configurar Olá API RESTful declarações exchange como um perfil técnico em seu arquivo TrustFrameworkExtensions.xml

Um perfil técnico é a configuração completa de saudação do exchange Olá desejado com hello serviço RESTful. Abrir o arquivo de TrustFrameworkExtensions.xml hello e adicione Olá seguindo o trecho XML dentro de saudação `<ClaimsProviders>` elemento.

> [!NOTE]
> Em Olá RESTful provedor XML a seguir `Version=1.0.0.0` é descrito como protocolo de saudação. Considere-a como a função hello irá interagir com o serviço externo hello. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

Olá `InputClaims` elemento define declarações Olá Olá serviço REST toohello IEF serão enviadas. Neste exemplo, Olá conteúdo da declaração Olá `givenName` receberá o serviço REST toohello como `playerTag`. Neste exemplo, Olá que IEF não espera declarações novamente. Em vez disso, ele aguarda uma resposta do serviço REST hello e funciona com base em códigos de status de saudação que recebe.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>Etapa 3: Incluir Olá serviço RESTful declarações exchange auto-declaradas perfil técnica em que você deseja toovalidate entrada do usuário de saudação

uso mais comum de saudação de etapa de validação de saudação é na interação Olá com um usuário. Todas as interações onde o usuário Olá é esperado tooprovide de entrada são *automático declarada perfis técnicos*. Neste exemplo, vamos adicionar perfil de autoatendimento Asserted ProfileUpdate de toohello validação de saudação técnica. Isso é o perfil de técnicas de Olá Olá arquivo de política de terceira parte confiável (RP) `Profile Edit` usa.

tooadd Olá declarações exchange toohello automático declarada perfil técnico:

1. Abrir arquivo de TrustFrameworkBase.xml hello e procure `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Examinar a configuração de saudação do perfil técnico. Observe como exchange Olá com usuário Olá é definido como declarações que serão solicitadas do usuário da saudação (declarações de entrada) e que será esperado do provedor de auto-declaradas hello (declarações de saída).
3. Pesquise `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate` e observe que esse perfil é invocado como a etapa de orquestração 6 do `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>Etapa 4: Carregar e testar o arquivo de política do hello perfil Editar RP

1. Carregar Olá nova versão do arquivo de TrustFrameworkExtensions.xml hello.
2. Use **executar agora** perfil de saudação tootest editar o arquivo de política do RP.
3. Testar a validação de hello, fornecendo um dos nomes de saudação existente (por exemplo, mcvinny) em Olá **nome** campo. Se tudo está configurado corretamente, você deve receber uma mensagem que notifica o usuário Olá que marca de player Olá já está em uso.

## <a name="next-steps"></a>Próximas etapas

[Modificar Olá perfil usuário e editar registro toogather informações adicionais de seus usuários](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[Passo a passo: integrar as trocas de declarações da API REST no percurso do usuário do Azure AD B2C como uma etapa de orquestração](active-directory-b2c-rest-api-step-custom.md)
