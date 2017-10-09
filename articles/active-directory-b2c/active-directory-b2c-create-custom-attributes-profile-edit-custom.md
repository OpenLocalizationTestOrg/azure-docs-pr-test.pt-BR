---
title: "B2C de diretório ativo do Azure: Adicionar suas próprias políticas de toocustom de atributos e usar no perfil Editar | Microsoft Docs"
description: "Um passo a passo sobre como usar propriedades de extensão, os atributos personalizados e incluí-los na interface do usuário Olá"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C: Como criar e usar atributos personalizados em uma política e edição de perfil personalizado

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Neste artigo, você cria um atributo personalizado em seu diretório do Azure AD B2C e usar esse novo atributo como uma declaração personalizada em jornada de usuário de edição de perfil de saudação.

## <a name="prerequisites"></a>Pré-requisitos

Olá concluído as etapas no artigo de saudação [guia de Introdução com as políticas personalizadas](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Use os atributos personalizados toocollect informações sobre os clientes no Azure Active Directory B2C usa políticas personalizadas
O diretório do Azure Active Directory (Azure AD) B2C é fornecido com um conjunto interno de atributos: Nome, Sobrenome, Cidade e CEP, entre outros atributos.  Muitas vezes é preciso toocreate seus próprios atributos.  Por exemplo:
* Um aplicativo voltado para o cliente precisa toopersist um atributo como "LoyaltyNumber".
* Um provedor de identidade tem um identificador exclusivo do usuário que deve ser salvo como "uniqueUserGUID".
* Jornada de um usuário personalizado precisa toopersist estado de saudação do usuário, como "migrationStatus".

Com o Azure AD B2C, você pode estender o conjunto de saudação de atributos armazenados em cada conta de usuário. Você também pode ler e gravar esses atributos usando Olá [do Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).

Propriedades de extensão estendem o esquema de Olá Olá de objetos de usuário no diretório de saudação.  propriedade de extensão de termos Hello, atributo personalizado e declarações personalizadas, consulte toohello mesmo significado no contexto de saudação desse nome de artigo e hello varia dependendo de contexto de saudação (aplicativo, objeto, política).

As propriedades de extensão só podem ser registradas em um objeto do aplicativo, ainda que contenham dados de um usuário. propriedade Olá é aplicativo toohello anexado. objeto de aplicativo Hello deve ser concedido acesso de gravação tooregister uma propriedade de extensão. Propriedades de extensão 100 (entre todos os tipos e todos os aplicativos) podem ser gravadas tooany único objeto. Propriedades de extensão são adicionadas toohello tipo de diretório de destino e se torna acessíveis imediatamente no locatário de diretório de saudação do Azure AD B2C.
Se o aplicativo hello é excluído, as propriedades de extensão juntamente com todos os dados contidos neles para todos os usuários também serão removidas. Se uma propriedade de extensão for excluída pelo Olá aplicativo, ele será removido em Olá objetos de diretório de destino e Olá valores excluídos.

Propriedades de extensão existem apenas em um contexto de um aplicativo registrado no locatário Olá Olá. id do objeto de saudação do aplicativo deve ser incluído no hello TechnicalProfile que usá-lo.

>[!NOTE]
>diretório de saudação do Azure AD B2C geralmente inclui um aplicativo Web chamado `b2c-extensions-app`.  Este aplicativo é usado principalmente por políticas internas do hello b2c para declarações personalizadas de saudação criadas por meio de saudação portal do Azure.  Usando extensões de tooregister esse aplicativo para políticas personalizadas b2c é recomendada somente para usuários avançados.  Instruções para isso são incluídas no hello seção próximas etapas neste artigo.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Criando um novo toostore de aplicativo propriedades de extensão Olá

1. Abra uma sessão de navegação e navegue toohello [portal do Azure](https://portal.azure.com) e entrar com credenciais administrativas de saudação Directory B2C desejar tooconfigure.
1. Clique em **Active Directory do Azure** no menu de navegação à esquerda de saudação. Talvez seja necessário toofind-lo selecionando mais services >.
1. Selecione **Registros de aplicativo** e clique em **Novo registro de aplicativo**
1. Forneça a seguinte Olá recomendado entradas:
  * Especifique um nome para o aplicativo da web hello: **WebApp-GraphAPI-DirectoryExtensions**
  * Tipo de aplicativo: API/Aplicativo Web
  * Logon URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. Selecione **Criar. Conclusão bem-sucedida é exibida no hello **notificações**
1. Selecionar aplicativo web de saudação recém-criado: **WebApp-GraphAPI-DirectoryExtensions**
1. Selecione as configurações: **Permissões necessárias**
1. Selecione a API **Active Directory do Windows**
1. Coloque uma marca de seleção em Permissões de Aplicativo: **Ler e gravar dados do diretório** e **Salvar**
1. Escolha **Conceder permissões** e confirme **Sim**.
1. Copiar na área de transferência tooyour e salvar Olá seguir identificadores de WebApp-GraphAPI-DirectoryExtensions > Configurações > Propriedades >
*  **ID do aplicativo**. Exemplo: `103ee0e6-f92d-4183-b576-8c3739027780`
* **ID de objeto**. Exemplo: `80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Modificando a saudação de tooadd de política personalizada ApplicationObjectId

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
>Olá <TechnicalProfile Id="AAD-Common"> é chamado tooas "comum" porque seus elementos estão incluídos no e reutilizados em todos os Olá TechnicalProfiles do Azure Active Directory usando o elemento de saudação:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Quando hello TechnicalProfile grava para propriedade de extensão para Olá primeiro tempo toohello recentemente criado, você pode enfrentar um erro de uso único.  propriedade de extensão de saudação é criada Olá primeira vez que ele é usado.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>Usando a nova propriedade de extensão Olá / atributo personalizado em uma viagem de usuário


1. Olá abrir arquivo terceira Party(RP) que descreve a política Editar jornada de usuário.  Se você estiver começando, talvez seja aconselhável toodownload sua versão já configurado do hello RP PolicyEdit arquivo diretamente da saudação seção política do Azure B2C personalizada Olá portal do Azure.  Como alternativa, abra o arquivo XML da pasta de armazenamento.
2. Adicione uma declaração personalizada `loyaltyId`.  Incluindo Olá personalizado de declaração em Olá `<RelyingParty>` elemento, ele é passado como um parâmetro toohello UserJourney TechnicalProfiles e incluído no token Olá para o aplicativo hello.
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. Adicionar um arquivo de política da extensão declaração definição toohello `TrustFrameworkExtensions.xml` dentro Olá `<ClaimsSchema>` elemento conforme mostrado.
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. Adicionar Olá mesma declaração de arquivo de definição de política Base toohello `TrustFrameworkBase.xml`.  
>Adicionando um `ClaimType` definição na base de saudação e o arquivo de extensões de saudação normalmente não é necessária, no entanto, desde que as próximas etapas Olá adicionará Olá extension_loyaltyId tooTechnicalProfiles no arquivo de Base Olá, validação de política de saudação rejeitará carregamento Olá do arquivo básico de saudação sem ele.
>Talvez seja útil tootrace execução Olá Olá jornada de usuário chamada "ProfileEdit" no arquivo de TrustFrameworkBase.xml hello.  Pesquise a jornada de usuário de saudação de saudação de mesmo nome em seu editor e observe a etapa 5 da orquestração invoca Olá TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".  Pesquisar e inspecionar esse toofamiliarize TechnicalProfile com fluxo hello.
5. Adicionar loyaltyId como declarações de entrada e saída no hello TechnicalProfile "SelfAsserted ProfileUpdate"
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. Adicione a declaração no valor de saudação toopersist TechnicalProfile "UserWriteProfileUsingObjectId AAD" da declaração de saudação na propriedade de extensão hello, para o usuário atual do hello no diretório de saudação.
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. Adicione declaração no valor de saudação tooread TechnicalProfile "UserReadUsingObjectId AAD" do atributo de extensão Olá toda vez que um usuário fizer logon. Até o momento Olá TechnicalProfiles foram alteradas no fluxo de saudação do somente para contas locais.  Se desejar fazer novo atributo de saudação no fluxo de saudação de uma conta social/federado, um conjunto diferente de TechnicalProfiles precisa toobe alterado. Confira as Próximas etapas.

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
>elemento de IncludeTechnicalProfile Olá adiciona todos os elementos de saudação do AAD comuns toothis TechnicalProfile.

## <a name="test-hello-custom-policy-using-run-now"></a>Testar a política personalizada do hello usando "Executar agora"
1. Olá abrir **folha do Azure AD B2C** e navegue muito**identidade experiência Framework > políticas personalizadas**.
1. Selecione Olá política personalizada que você carregou e, em seguida, clique em Olá **executar agora** botão.
1. Você deve ser capaz de toosign usando um endereço de email.

token de id de saudação enviada de volta tooyour aplicativo inclui a nova propriedade de extensão hello como uma declaração personalizada precedida por extension_loyaltyId. Confira o exemplo.

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Próximas etapas

Adicione Olá novos declaração toohello fluxos para logons de conta social alterando Olá TechnicalProfiles listados. Esses dois TechnicalProfiles são usados pelo toowrite de logons de conta social/federado e ler dados do usuário hello usando alternativeSecurityId Olá Olá localizador de saudação do objeto de usuário.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

Usando Olá os mesmos atributos de extensão entre políticas internas e personalizadas.
Quando você adiciona atributos de extensão (também conhecido como atributos personalizados) por meio de experiência do portal hello, esses atributos são registrados usando hello * * b2c extensões-aplicativo que existe em cada locatário b2c.  toouse esses atributos de extensão em sua política personalizada:
1. Em seu locatário b2c em portal.azure.com, navegue muito**Active Directory do Azure** e selecione **registros do aplicativo**
2. Localize seu **b2c-extensions-app** e selecione-o
3. Sob saudação do registro 'Essentials' **ID do aplicativo** e hello **ID de objeto**
4. Inclua-os em seus metadados de perfil técnico comuns do AAD da seguinte maneira:

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

tookeep consistência com a experiência do portal hello, crie esses atributos usando a interface de usuário do portal Olá *antes de* usá-los em suas políticas personalizadas.  Quando você criar um atributo "ActivationStatus" no portal de saudação, você deve se referir tooit da seguinte maneira:

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>Referência

* Um **perfil técnica (TP)** é um tipo de elemento que pode ser pensado como um *função* que define o nome de um ponto de extremidade, seus metadados, seu protocolo e detalhes Olá troca de declarações que Olá identidade Experiência Framework deve ser executadas.  Quando isso *função* é chamado em uma etapa de orquestração ou de outro TechnicalProfile, Olá InputClaims e OutputClaims são fornecidos como parâmetros pelo chamador hello.


* Tratamento completo nas propriedades de extensão, consulte o artigo Olá [extensões de esquema de diretório | CONCEITOS DA API DO GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Atributos de extensão na Graph API são nomeados usando a convenção de saudação `extension_ApplicationObjectID_attributename`. Políticas personalizadas consulte tooextensions atributos como extension_attributename, omitindo assim Olá ApplicationObjectId em Olá XML
