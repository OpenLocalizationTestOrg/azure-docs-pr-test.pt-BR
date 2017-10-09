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
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="217db-103">Azure Active Directory B2C: Como criar e usar atributos personalizados em uma política e edição de perfil personalizado</span><span class="sxs-lookup"><span data-stu-id="217db-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="217db-104">Neste artigo, você cria um atributo personalizado em seu diretório do Azure AD B2C e usar esse novo atributo como uma declaração personalizada em jornada de usuário de edição de perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="217db-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="217db-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="217db-105">Prerequisites</span></span>

<span data-ttu-id="217db-106">Olá concluído as etapas no artigo de saudação [guia de Introdução com as políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="217db-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="217db-107">Use os atributos personalizados toocollect informações sobre os clientes no Azure Active Directory B2C usa políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="217db-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="217db-108">O diretório do Azure Active Directory (Azure AD) B2C é fornecido com um conjunto interno de atributos: Nome, Sobrenome, Cidade e CEP, entre outros atributos.  Muitas vezes é preciso toocreate seus próprios atributos.</span><span class="sxs-lookup"><span data-stu-id="217db-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="217db-109">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="217db-109">For example:</span></span>
* <span data-ttu-id="217db-110">Um aplicativo voltado para o cliente precisa toopersist um atributo como "LoyaltyNumber".</span><span class="sxs-lookup"><span data-stu-id="217db-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="217db-111">Um provedor de identidade tem um identificador exclusivo do usuário que deve ser salvo como "uniqueUserGUID".</span><span class="sxs-lookup"><span data-stu-id="217db-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="217db-112">Jornada de um usuário personalizado precisa toopersist estado de saudação do usuário, como "migrationStatus".</span><span class="sxs-lookup"><span data-stu-id="217db-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="217db-113">Com o Azure AD B2C, você pode estender o conjunto de saudação de atributos armazenados em cada conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="217db-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="217db-114">Você também pode ler e gravar esses atributos usando Olá [do Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="217db-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="217db-115">Propriedades de extensão estendem o esquema de Olá Olá de objetos de usuário no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="217db-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="217db-116">propriedade de extensão de termos Hello, atributo personalizado e declarações personalizadas, consulte toohello mesmo significado no contexto de saudação desse nome de artigo e hello varia dependendo de contexto de saudação (aplicativo, objeto, política).</span><span class="sxs-lookup"><span data-stu-id="217db-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="217db-117">As propriedades de extensão só podem ser registradas em um objeto do aplicativo, ainda que contenham dados de um usuário.</span><span class="sxs-lookup"><span data-stu-id="217db-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="217db-118">propriedade Olá é aplicativo toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="217db-118">hello property is attached toohello application.</span></span> <span data-ttu-id="217db-119">objeto de aplicativo Hello deve ser concedido acesso de gravação tooregister uma propriedade de extensão.</span><span class="sxs-lookup"><span data-stu-id="217db-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="217db-120">Propriedades de extensão 100 (entre todos os tipos e todos os aplicativos) podem ser gravadas tooany único objeto.</span><span class="sxs-lookup"><span data-stu-id="217db-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="217db-121">Propriedades de extensão são adicionadas toohello tipo de diretório de destino e se torna acessíveis imediatamente no locatário de diretório de saudação do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="217db-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="217db-122">Se o aplicativo hello é excluído, as propriedades de extensão juntamente com todos os dados contidos neles para todos os usuários também serão removidas.</span><span class="sxs-lookup"><span data-stu-id="217db-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="217db-123">Se uma propriedade de extensão for excluída pelo Olá aplicativo, ele será removido em Olá objetos de diretório de destino e Olá valores excluídos.</span><span class="sxs-lookup"><span data-stu-id="217db-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="217db-124">Propriedades de extensão existem apenas em um contexto de um aplicativo registrado no locatário Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="217db-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="217db-125">id do objeto de saudação do aplicativo deve ser incluído no hello TechnicalProfile que usá-lo.</span><span class="sxs-lookup"><span data-stu-id="217db-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="217db-126">diretório de saudação do Azure AD B2C geralmente inclui um aplicativo Web chamado `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="217db-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="217db-127">Este aplicativo é usado principalmente por políticas internas do hello b2c para declarações personalizadas de saudação criadas por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="217db-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="217db-128">Usando extensões de tooregister esse aplicativo para políticas personalizadas b2c é recomendada somente para usuários avançados.</span><span class="sxs-lookup"><span data-stu-id="217db-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="217db-129">Instruções para isso são incluídas no hello seção próximas etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="217db-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="217db-130">Criando um novo toostore de aplicativo propriedades de extensão Olá</span><span class="sxs-lookup"><span data-stu-id="217db-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="217db-131">Abra uma sessão de navegação e navegue toohello [portal do Azure](https://portal.azure.com) e entrar com credenciais administrativas de saudação Directory B2C desejar tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="217db-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="217db-132">Clique em **Active Directory do Azure** no menu de navegação à esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="217db-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="217db-133">Talvez seja necessário toofind-lo selecionando mais services >.</span><span class="sxs-lookup"><span data-stu-id="217db-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="217db-134">Selecione **Registros de aplicativo** e clique em **Novo registro de aplicativo**</span><span class="sxs-lookup"><span data-stu-id="217db-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="217db-135">Forneça a seguinte Olá recomendado entradas:</span><span class="sxs-lookup"><span data-stu-id="217db-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="217db-136">Especifique um nome para o aplicativo da web hello: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="217db-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="217db-137">Tipo de aplicativo: API/Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="217db-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="217db-138">Logon URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="217db-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="217db-139">Selecione **Criar.</span><span class="sxs-lookup"><span data-stu-id="217db-139">Select **Create.</span></span> <span data-ttu-id="217db-140">Conclusão bem-sucedida é exibida no hello **notificações**</span><span class="sxs-lookup"><span data-stu-id="217db-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="217db-141">Selecionar aplicativo web de saudação recém-criado: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="217db-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="217db-142">Selecione as configurações: **Permissões necessárias**</span><span class="sxs-lookup"><span data-stu-id="217db-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="217db-143">Selecione a API **Active Directory do Windows**</span><span class="sxs-lookup"><span data-stu-id="217db-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="217db-144">Coloque uma marca de seleção em Permissões de Aplicativo: **Ler e gravar dados do diretório** e **Salvar**</span><span class="sxs-lookup"><span data-stu-id="217db-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="217db-145">Escolha **Conceder permissões** e confirme **Sim**.</span><span class="sxs-lookup"><span data-stu-id="217db-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="217db-146">Copiar na área de transferência tooyour e salvar Olá seguir identificadores de WebApp-GraphAPI-DirectoryExtensions > Configurações > Propriedades ></span><span class="sxs-lookup"><span data-stu-id="217db-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="217db-147">**ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="217db-147">**Application ID** .</span></span> <span data-ttu-id="217db-148">Exemplo: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="217db-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="217db-149">**ID de objeto**.</span><span class="sxs-lookup"><span data-stu-id="217db-149">**Object ID**.</span></span> <span data-ttu-id="217db-150">Exemplo: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="217db-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="217db-151">Modificando a saudação de tooadd de política personalizada ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="217db-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

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
><span data-ttu-id="217db-152">Olá <TechnicalProfile Id="AAD-Common"> é chamado tooas "comum" porque seus elementos estão incluídos no e reutilizados em todos os Olá TechnicalProfiles do Azure Active Directory usando o elemento de saudação:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="217db-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="217db-153">Quando hello TechnicalProfile grava para propriedade de extensão para Olá primeiro tempo toohello recentemente criado, você pode enfrentar um erro de uso único.</span><span class="sxs-lookup"><span data-stu-id="217db-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="217db-154">propriedade de extensão de saudação é criada Olá primeira vez que ele é usado.</span><span class="sxs-lookup"><span data-stu-id="217db-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="217db-155">Usando a nova propriedade de extensão Olá / atributo personalizado em uma viagem de usuário</span><span class="sxs-lookup"><span data-stu-id="217db-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="217db-156">Olá abrir arquivo terceira Party(RP) que descreve a política Editar jornada de usuário.</span><span class="sxs-lookup"><span data-stu-id="217db-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="217db-157">Se você estiver começando, talvez seja aconselhável toodownload sua versão já configurado do hello RP PolicyEdit arquivo diretamente da saudação seção política do Azure B2C personalizada Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="217db-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="217db-158">Como alternativa, abra o arquivo XML da pasta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="217db-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="217db-159">Adicione uma declaração personalizada `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="217db-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="217db-160">Incluindo Olá personalizado de declaração em Olá `<RelyingParty>` elemento, ele é passado como um parâmetro toohello UserJourney TechnicalProfiles e incluído no token Olá para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="217db-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
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
3. <span data-ttu-id="217db-161">Adicionar um arquivo de política da extensão declaração definição toohello `TrustFrameworkExtensions.xml` dentro Olá `<ClaimsSchema>` elemento conforme mostrado.</span><span class="sxs-lookup"><span data-stu-id="217db-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
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
4. <span data-ttu-id="217db-162">Adicionar Olá mesma declaração de arquivo de definição de política Base toohello `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="217db-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="217db-163">Adicionando um `ClaimType` definição na base de saudação e o arquivo de extensões de saudação normalmente não é necessária, no entanto, desde que as próximas etapas Olá adicionará Olá extension_loyaltyId tooTechnicalProfiles no arquivo de Base Olá, validação de política de saudação rejeitará carregamento Olá do arquivo básico de saudação sem ele.</span><span class="sxs-lookup"><span data-stu-id="217db-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="217db-164">Talvez seja útil tootrace execução Olá Olá jornada de usuário chamada "ProfileEdit" no arquivo de TrustFrameworkBase.xml hello.</span><span class="sxs-lookup"><span data-stu-id="217db-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="217db-165">Pesquise a jornada de usuário de saudação de saudação de mesmo nome em seu editor e observe a etapa 5 da orquestração invoca Olá TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="217db-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="217db-166">Pesquisar e inspecionar esse toofamiliarize TechnicalProfile com fluxo hello.</span><span class="sxs-lookup"><span data-stu-id="217db-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="217db-167">Adicionar loyaltyId como declarações de entrada e saída no hello TechnicalProfile "SelfAsserted ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="217db-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
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
6. <span data-ttu-id="217db-168">Adicione a declaração no valor de saudação toopersist TechnicalProfile "UserWriteProfileUsingObjectId AAD" da declaração de saudação na propriedade de extensão hello, para o usuário atual do hello no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="217db-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
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
7. <span data-ttu-id="217db-169">Adicione declaração no valor de saudação tooread TechnicalProfile "UserReadUsingObjectId AAD" do atributo de extensão Olá toda vez que um usuário fizer logon.</span><span class="sxs-lookup"><span data-stu-id="217db-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="217db-170">Até o momento Olá TechnicalProfiles foram alteradas no fluxo de saudação do somente para contas locais.</span><span class="sxs-lookup"><span data-stu-id="217db-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="217db-171">Se desejar fazer novo atributo de saudação no fluxo de saudação de uma conta social/federado, um conjunto diferente de TechnicalProfiles precisa toobe alterado.</span><span class="sxs-lookup"><span data-stu-id="217db-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="217db-172">Confira as Próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="217db-172">See Next Steps.</span></span>

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
><span data-ttu-id="217db-173">elemento de IncludeTechnicalProfile Olá adiciona todos os elementos de saudação do AAD comuns toothis TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="217db-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="217db-174">Testar a política personalizada do hello usando "Executar agora"</span><span class="sxs-lookup"><span data-stu-id="217db-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="217db-175">Olá abrir **folha do Azure AD B2C** e navegue muito**identidade experiência Framework > políticas personalizadas**.</span><span class="sxs-lookup"><span data-stu-id="217db-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="217db-176">Selecione Olá política personalizada que você carregou e, em seguida, clique em Olá **executar agora** botão.</span><span class="sxs-lookup"><span data-stu-id="217db-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="217db-177">Você deve ser capaz de toosign usando um endereço de email.</span><span class="sxs-lookup"><span data-stu-id="217db-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="217db-178">token de id de saudação enviada de volta tooyour aplicativo inclui a nova propriedade de extensão hello como uma declaração personalizada precedida por extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="217db-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="217db-179">Confira o exemplo.</span><span class="sxs-lookup"><span data-stu-id="217db-179">See example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="217db-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="217db-180">Next steps</span></span>

<span data-ttu-id="217db-181">Adicione Olá novos declaração toohello fluxos para logons de conta social alterando Olá TechnicalProfiles listados.</span><span class="sxs-lookup"><span data-stu-id="217db-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="217db-182">Esses dois TechnicalProfiles são usados pelo toowrite de logons de conta social/federado e ler dados do usuário hello usando alternativeSecurityId Olá Olá localizador de saudação do objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="217db-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="217db-183">Usando Olá os mesmos atributos de extensão entre políticas internas e personalizadas.</span><span class="sxs-lookup"><span data-stu-id="217db-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="217db-184">Quando você adiciona atributos de extensão (também conhecido como atributos personalizados) por meio de experiência do portal hello, esses atributos são registrados usando hello * * b2c extensões-aplicativo que existe em cada locatário b2c.</span><span class="sxs-lookup"><span data-stu-id="217db-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="217db-185">toouse esses atributos de extensão em sua política personalizada:</span><span class="sxs-lookup"><span data-stu-id="217db-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="217db-186">Em seu locatário b2c em portal.azure.com, navegue muito**Active Directory do Azure** e selecione **registros do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="217db-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="217db-187">Localize seu **b2c-extensions-app** e selecione-o</span><span class="sxs-lookup"><span data-stu-id="217db-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="217db-188">Sob saudação do registro 'Essentials' **ID do aplicativo** e hello **ID de objeto**</span><span class="sxs-lookup"><span data-stu-id="217db-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="217db-189">Inclua-os em seus metadados de perfil técnico comuns do AAD da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="217db-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

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

<span data-ttu-id="217db-190">tookeep consistência com a experiência do portal hello, crie esses atributos usando a interface de usuário do portal Olá *antes de* usá-los em suas políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="217db-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="217db-191">Quando você criar um atributo "ActivationStatus" no portal de saudação, você deve se referir tooit da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="217db-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="217db-192">Referência</span><span class="sxs-lookup"><span data-stu-id="217db-192">Reference</span></span>

* <span data-ttu-id="217db-193">Um **perfil técnica (TP)** é um tipo de elemento que pode ser pensado como um *função* que define o nome de um ponto de extremidade, seus metadados, seu protocolo e detalhes Olá troca de declarações que Olá identidade Experiência Framework deve ser executadas.</span><span class="sxs-lookup"><span data-stu-id="217db-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="217db-194">Quando isso *função* é chamado em uma etapa de orquestração ou de outro TechnicalProfile, Olá InputClaims e OutputClaims são fornecidos como parâmetros pelo chamador hello.</span><span class="sxs-lookup"><span data-stu-id="217db-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="217db-195">Tratamento completo nas propriedades de extensão, consulte o artigo Olá [extensões de esquema de diretório | CONCEITOS DA API DO GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="217db-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="217db-196">Atributos de extensão na Graph API são nomeados usando a convenção de saudação `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="217db-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="217db-197">Políticas personalizadas consulte tooextensions atributos como extension_attributename, omitindo assim Olá ApplicationObjectId em Olá XML</span><span class="sxs-lookup"><span data-stu-id="217db-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
