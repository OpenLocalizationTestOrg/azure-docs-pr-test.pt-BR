---
title: "Azure Active Directory B2C: Como adicionar seus próprios atributos a políticas personalizadas e usar na edição de perfil | Microsoft Docs"
description: "Um passo a passo sobre como usar propriedades de extensão, atributos personalizados e incluí-los na interface de usuário"
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
ms.openlocfilehash: 67c9f6eca18e2dd77e00b8bc8c7bcc546ea3936e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="90db2-103">Azure Active Directory B2C: Como criar e usar atributos personalizados em uma política e edição de perfil personalizado</span><span class="sxs-lookup"><span data-stu-id="90db2-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="90db2-104">Neste artigo, você criará um atributo personalizado no seu diretório do Azure AD B2C e usará esse novo atributo como uma declaração personalizada de percurso do usuário de edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="90db2-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in the profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90db2-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="90db2-105">Prerequisites</span></span>

<span data-ttu-id="90db2-106">Conclua as etapas no artigo [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="90db2-106">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-to-collect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="90db2-107">Use atributos personalizados para coletar informações sobre seus clientes no Azure Active Directory B2C usando políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="90db2-107">Use custom attributes to collect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="90db2-108">O diretório do Azure Active Directory (Azure AD) B2C é fornecido com um conjunto interno de atributos: Nome, Sobrenome, Cidade e CEP, entre outros atributos.  Geralmente, você precisa criar seus próprios atributos.</span><span class="sxs-lookup"><span data-stu-id="90db2-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need to create your own attributes.</span></span>  <span data-ttu-id="90db2-109">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="90db2-109">For example:</span></span>
* <span data-ttu-id="90db2-110">Um aplicativo voltado para o cliente precisa manter um atributo, como "LoyaltyNumber".</span><span class="sxs-lookup"><span data-stu-id="90db2-110">A customer-facing application needs to persist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="90db2-111">Um provedor de identidade tem um identificador exclusivo do usuário que deve ser salvo como "uniqueUserGUID".</span><span class="sxs-lookup"><span data-stu-id="90db2-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="90db2-112">Um percurso do usuário personalizado precisa manter o estado do usuário, como "migrationStatus".</span><span class="sxs-lookup"><span data-stu-id="90db2-112">A custom user journey needs to persist the state of user such as "migrationStatus."</span></span>

<span data-ttu-id="90db2-113">Com o Azure AD B2C, você pode estender o conjunto de atributos armazenados em cada conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="90db2-113">With Azure AD B2C, you can extend the set of attributes stored on each user account.</span></span> <span data-ttu-id="90db2-114">Você também pode ler e gravar esses atributos usando a [API do Graph do Azure AD](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="90db2-114">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="90db2-115">Propriedades de extensão estendem o esquema dos objetos de usuário no diretório.</span><span class="sxs-lookup"><span data-stu-id="90db2-115">Extension properties extend the schema of the user objects in the directory.</span></span>  <span data-ttu-id="90db2-116">A propriedade de extensão de termos, atributo personalizado e declaração personalizada, se referem à mesma coisa no contexto deste artigo, e o nome varia dependendo do contexto (aplicativo, objeto, política).</span><span class="sxs-lookup"><span data-stu-id="90db2-116">The terms extension property, custom attribute and custom claim refer to the same thing in the context of this article and the name varies depending on the context (application, object, policy).</span></span>

<span data-ttu-id="90db2-117">As propriedades de extensão só podem ser registradas em um objeto do aplicativo, ainda que contenham dados de um usuário.</span><span class="sxs-lookup"><span data-stu-id="90db2-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="90db2-118">A propriedade é anexada ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90db2-118">The property is attached to the application.</span></span> <span data-ttu-id="90db2-119">O objeto do aplicativo precisa obter acesso de gravação para registrar uma propriedade de extensão.</span><span class="sxs-lookup"><span data-stu-id="90db2-119">The Application object must be granted write access to register an extension property.</span></span> <span data-ttu-id="90db2-120">É possível gravar 100 propriedades de extensão (entre TODOS os tipos e TODOS os aplicativos) em um único objeto.</span><span class="sxs-lookup"><span data-stu-id="90db2-120">100 Extension properties (across ALL types and ALL applications) can be written to any single object.</span></span> <span data-ttu-id="90db2-121">As propriedades de extensão são adicionadas para o tipo de diretório de destino e tornam-se imediatamente acessíveis no locatário de diretório do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="90db2-121">Extension properties are added to the target directory type and becomes immediately accessible in the Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="90db2-122">Se o aplicativo for excluído, tanto as propriedades de extensão quanto os dados contidos nelas para todos os usuários serão removidos.</span><span class="sxs-lookup"><span data-stu-id="90db2-122">If the application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="90db2-123">Se uma propriedade de extensão for excluída pelo aplicativo, ela será removida nos objetos do diretório de destino, e os dados valores serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="90db2-123">If an extension property is deleted by the Application, it is removed on the target directory objects, and the values deleted.</span></span>

<span data-ttu-id="90db2-124">As propriedades de extensão existem apenas no contexto de um aplicativo registrado no locatário.</span><span class="sxs-lookup"><span data-stu-id="90db2-124">Extension properties exist only in the context of a registered  Application in the tenant.</span></span> <span data-ttu-id="90db2-125">O id de objeto desse Aplicativo deve ser incluído no TechnicalProfile que o usa.</span><span class="sxs-lookup"><span data-stu-id="90db2-125">The object id of that Application must be included in the TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="90db2-126">O diretório do Azure AD B2C geralmente inclui um aplicativo Web chamado `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="90db2-126">The Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="90db2-127">Este aplicativo é usado principalmente pelas políticas internas b2c para as declarações personalizadas criadas por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="90db2-127">This application is primarily used by the b2c built-in  policies for the custom claims created via the Azure portal.</span></span>  <span data-ttu-id="90db2-128">Recomenda-se que apenas usuários avançados usem este aplicativo para registrar extensões para as políticas personalizadas b2c.</span><span class="sxs-lookup"><span data-stu-id="90db2-128">Using this application to register extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="90db2-129">As instruções para isso são incluídas na seção Próximas etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="90db2-129">Instructions for this are included in the Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-to-store-the-extension-properties"></a><span data-ttu-id="90db2-130">Criação de um aplicativo novo para armazenar as propriedades de extensão</span><span class="sxs-lookup"><span data-stu-id="90db2-130">Creating a new application to store the extension properties</span></span>

1. <span data-ttu-id="90db2-131">Abra uma sessão de navegação e navegue até o [portal do Azure](https://portal.azure.com) e entre com as credenciais administrativas do diretório do B2C que deseja configurar.</span><span class="sxs-lookup"><span data-stu-id="90db2-131">Open a browsing session and navigate to the [Azure porta](https://portal.azure.com) and sign in with administrative credentials of the B2C Directory you wish to configure.</span></span>
1. <span data-ttu-id="90db2-132">Clique em **Azure Active Directory** no menu de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="90db2-132">Click **Azure Active Directory** on the left navigation menu.</span></span> <span data-ttu-id="90db2-133">Talvez seja necessário localizá-lo, para isso, selecione Mais serviços>.</span><span class="sxs-lookup"><span data-stu-id="90db2-133">You may need to find it by selecting More services>.</span></span>
1. <span data-ttu-id="90db2-134">Selecione **Registros de aplicativo** e clique em **Novo registro de aplicativo**</span><span class="sxs-lookup"><span data-stu-id="90db2-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="90db2-135">Forneça as seguintes entradas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="90db2-135">Provide the following recommended entries:</span></span>
  * <span data-ttu-id="90db2-136">Especifique um nome para o aplicativo Web: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="90db2-136">Specify a name for the web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="90db2-137">Tipo de aplicativo: API/Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="90db2-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="90db2-138">Logon URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="90db2-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="90db2-139">Selecione **Criar.</span><span class="sxs-lookup"><span data-stu-id="90db2-139">Select **Create.</span></span> <span data-ttu-id="90db2-140">A conclusão bem-sucedida aparece nas **notificações**</span><span class="sxs-lookup"><span data-stu-id="90db2-140">Successful completion appears in the **notifications**</span></span>
1. <span data-ttu-id="90db2-141">Selecione o aplicativo Web criado recentemente: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="90db2-141">Select the newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="90db2-142">Selecione as configurações: **Permissões necessárias**</span><span class="sxs-lookup"><span data-stu-id="90db2-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="90db2-143">Selecione a API **Active Directory do Windows**</span><span class="sxs-lookup"><span data-stu-id="90db2-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="90db2-144">Coloque uma marca de seleção em Permissões de Aplicativo: **Ler e gravar dados do diretório** e **Salvar**</span><span class="sxs-lookup"><span data-stu-id="90db2-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="90db2-145">Escolha **Conceder permissões** e confirme **Sim**.</span><span class="sxs-lookup"><span data-stu-id="90db2-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="90db2-146">Copie para a área de transferência e salve os seguintes identificadores de WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span><span class="sxs-lookup"><span data-stu-id="90db2-146">Copy to your clipboard and save the following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="90db2-147">**ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="90db2-147">**Application ID** .</span></span> <span data-ttu-id="90db2-148">Exemplo: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="90db2-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="90db2-149">**ID de objeto**.</span><span class="sxs-lookup"><span data-stu-id="90db2-149">**Object ID**.</span></span> <span data-ttu-id="90db2-150">Exemplo: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="90db2-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-to-add-the-applicationobjectid"></a><span data-ttu-id="90db2-151">Modificar a política personalizada para adicionar o ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="90db2-151">Modifying your custom policy to add the ApplicationObjectId</span></span>

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
><span data-ttu-id="90db2-152">O <TechnicalProfile Id="AAD-Common"> é conhecido como "comum", pois seus elementos são incluídos e reutilizados em todos os TechnicalProfiles do Azure Active Directory usando o elemento: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="90db2-152">The <TechnicalProfile Id="AAD-Common"> is referred to as "common" because its elements are included in and reused in all the Azure Active Directory TechnicalProfiles by using the element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="90db2-153">Às vezes, quando o TechnicalProfile grava pela primeira vez para a propriedade de extensão recém-criada, pode ocorrer um erro ocasional.</span><span class="sxs-lookup"><span data-stu-id="90db2-153">When the TechnicalProfile writes for the first time to the newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="90db2-154">A propriedade de extensão é criada na primeira vez que ela é usada.</span><span class="sxs-lookup"><span data-stu-id="90db2-154">The extension property is created the first time it is used.</span></span>  

## <a name="using-the-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="90db2-155">Como usar a nova propriedade de extensão / atributo personalizado em um percurso do usuário</span><span class="sxs-lookup"><span data-stu-id="90db2-155">Using the new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="90db2-156">Abra o arquivo da terceira parte confiável (RP) que descreve o seu percurso do usuário de edição da política.</span><span class="sxs-lookup"><span data-stu-id="90db2-156">Open the Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="90db2-157">Se você estiver começando, pode ser aconselhável baixar a versão já configurada do arquivo RP-PolicyEdit diretamente na seção Política de Personalização do Azure B2C no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="90db2-157">If you are starting out, it may be advisable to download your already configured version of the RP-PolicyEdit file directly from the Azure B2C Custom Policy section in the Azure portal.</span></span>  <span data-ttu-id="90db2-158">Como alternativa, abra o arquivo XML da pasta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="90db2-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="90db2-159">Adicione uma declaração personalizada `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="90db2-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="90db2-160">Ao incluir uma declaração personalizada no elemento `<RelyingParty>`, ela será indicada como parâmetro para o TechnicalProfiles de percurso do usuário, além de ser incluída no token para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90db2-160">By including the custom claim in the `<RelyingParty>` element, it is passed as a parameter to the UserJourney TechnicalProfiles and included in the token for the application.</span></span>
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
3. <span data-ttu-id="90db2-161">Adicione uma definição de declaração ao arquivo de política de extensão `TrustFrameworkExtensions.xml` dentro do elemento `<ClaimsSchema>`, conforme mostrado.</span><span class="sxs-lookup"><span data-stu-id="90db2-161">Add a claim definition to the Extension policy file  `TrustFrameworkExtensions.xml` inside the `<ClaimsSchema>` element as shown.</span></span>
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
4. <span data-ttu-id="90db2-162">Adicione a mesma definição de declaração ao arquivo de política base `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="90db2-162">Add the same claim definition to the Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="90db2-163">Geralmente, não é necessário adicionar uma definição `ClaimType` nos arquivos de extensões e de base, no entanto, como as próximas etapas adicionarão o extension_loyaltyId ao TechnicalProfiles no Arquivo Base, o validador de política rejeitará o upload do arquivo base sem ela.</span><span class="sxs-lookup"><span data-stu-id="90db2-163">Adding a `ClaimType` definition in both the base and the extensions file is normally not necessary, however since the next steps will add the extension_loyaltyId to TechnicalProfiles in the Base file, the policy validator will reject the upload of the base file without it.</span></span>
><span data-ttu-id="90db2-164">Poderá ser útil rastrear a execução do percurso do usuário chamado "ProfileEdit" no arquivo TrustFrameworkBase.xml.</span><span class="sxs-lookup"><span data-stu-id="90db2-164">It may be useful to trace the execution of the user journey named "ProfileEdit" in the TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="90db2-165">Pesquise o percurso do usuário do mesmo nome no seu editor e observe que a orquestração da etapa 5 invoca o TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="90db2-165">Search for the user journey of the same name in your editor and observe that Orchestration Step 5 invokes the TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="90db2-166">Pesquise e inspecione esse TechnicalProfile para se familiarizar com o fluxo.</span><span class="sxs-lookup"><span data-stu-id="90db2-166">Search and inspect this TechnicalProfile to familiarize yourself with the flow.</span></span>
5. <span data-ttu-id="90db2-167">Adicione o loyaltyId como declaração de entrada e saída no TechnicalProfile "SelfAsserted-ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="90db2-167">Add loyaltyId as input and output claim in the TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
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

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="90db2-168">Adicione a declaração no TechnicalProfile "AAD-UserWriteProfileUsingObjectId" para manter o valor da declaração na propriedade de extensão para o usuário atual no diretório.</span><span class="sxs-lookup"><span data-stu-id="90db2-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" to persist the value of the claim in the extension property, for the current user in the directory.</span></span>
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
7. <span data-ttu-id="90db2-169">Adicione a declaração no TechnicalProfile "AAD-UserReadUsingObjectId" para ler o valor do atributo de extensão sempre que um usuário fizer logon.</span><span class="sxs-lookup"><span data-stu-id="90db2-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" to read the value of the extension attribute every time a user logs in.</span></span> <span data-ttu-id="90db2-170">Até o momento, os TechnicalProfiles só foram alterados no fluxo de contas locais.</span><span class="sxs-lookup"><span data-stu-id="90db2-170">Thus far the TechnicalProfiles have been changed in the flow of local accounts only.</span></span>  <span data-ttu-id="90db2-171">Se quiser o novo atributo no fluxo de uma conta social/federada, será necessário alterar um conjunto diferente de TechnicalProfiles.</span><span class="sxs-lookup"><span data-stu-id="90db2-171">If the new attribute is desired in the flow of a social/federated account, a different set of TechnicalProfiles needs to be changed.</span></span> <span data-ttu-id="90db2-172">Confira as Próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="90db2-172">See Next Steps.</span></span>

```xml
<!-- The following technical profile is used to read data after user authenticates. -->
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
><span data-ttu-id="90db2-173">O elemento IncludeTechnicalProfile adiciona todos os elementos do AAD comum para esse TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="90db2-173">The IncludeTechnicalProfile element adds all the elements of AAD-Common to this TechnicalProfile.</span></span>

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="90db2-174">Teste a política personalizada usando a opção "Executar Agora"</span><span class="sxs-lookup"><span data-stu-id="90db2-174">Test the custom policy using "Run Now"</span></span>
1. <span data-ttu-id="90db2-175">Abra a **Folha B2C do Azure AD** e navegue até **Identity Experience Framework > Políticas personalizadas**.</span><span class="sxs-lookup"><span data-stu-id="90db2-175">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="90db2-176">Selecione a política personalizada carregada e clique no botão **Executar agora**.</span><span class="sxs-lookup"><span data-stu-id="90db2-176">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
1. <span data-ttu-id="90db2-177">Você deverá conseguir se inscrever usando um endereço de email.</span><span class="sxs-lookup"><span data-stu-id="90db2-177">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="90db2-178">O token de id enviado novamente para o seu aplicativo inclui a propriedade de extensão nova como uma declaração personalizada precedida por extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="90db2-178">The  id token sent back to your application includes the new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="90db2-179">Confira o exemplo.</span><span class="sxs-lookup"><span data-stu-id="90db2-179">See example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="90db2-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90db2-180">Next steps</span></span>

<span data-ttu-id="90db2-181">Adicione a nova declaração aos fluxos para logons de conta social alterando os TechnicalProfiles listados.</span><span class="sxs-lookup"><span data-stu-id="90db2-181">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed.</span></span> <span data-ttu-id="90db2-182">Esses dois TechnicalProfiles são usados por logons de conta social/federados para gravar e ler os dados do usuário usando o alternativeSecurityId como o localizador do objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="90db2-182">These two TechnicalProfiles are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator of the user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="90db2-183">Usando os mesmos atributos de extensão entre políticas internas e personalizadas.</span><span class="sxs-lookup"><span data-stu-id="90db2-183">Using the same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="90db2-184">Quando você adiciona atributos de extensão (também conhecido como atributos personalizados) por meio da experiência do portal, esses atributos são registrados usando o **b2c-extensions-app que existe em cada locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="90db2-184">When you add extension attributes (aka custom attributes) via the portal experience, those attributes are registered using the **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="90db2-185">Para usar esses atributos de extensão em sua política personalizada:</span><span class="sxs-lookup"><span data-stu-id="90db2-185">To use these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="90db2-186">Em seu locatário B2C no portal.azure.com, navegue até **Azure Active Directory** e selecione **Registros de aplicativo**</span><span class="sxs-lookup"><span data-stu-id="90db2-186">Within your b2c tenant in portal.azure.com, navigate to **Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="90db2-187">Localize seu **b2c-extensions-app** e selecione-o</span><span class="sxs-lookup"><span data-stu-id="90db2-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="90db2-188">Em "Essentials" registre a **ID do aplicativo** e a **ID do objeto**</span><span class="sxs-lookup"><span data-stu-id="90db2-188">Under 'Essentials' record the **Application ID** and the **Object ID**</span></span>
4. <span data-ttu-id="90db2-189">Inclua-os em seus metadados de perfil técnico comuns do AAD da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="90db2-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is the "Object ID" from the "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is the "Application ID" from the "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="90db2-190">Para manter a consistência com a experiência do portal, crie esses atributos usando a interface do usuário do portal *antes* de usá-los em suas políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="90db2-190">To keep consistency with the portal experience, create these attributes using the portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="90db2-191">Quando você cria um atributo "ActivationStatus" no portal, é necessário fazer referência a ele da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="90db2-191">When you create an attribute "ActivationStatus" in the portal, you must refer to it as follows:</span></span>

```
extension_ActivationStatus in the custom policy
extension_<app-guid>_ActivationStatus via the Graph API.
```


## <a name="reference"></a><span data-ttu-id="90db2-192">Referência</span><span class="sxs-lookup"><span data-stu-id="90db2-192">Reference</span></span>

* <span data-ttu-id="90db2-193">O **Perfil técnico (TP)** é um tipo de elemento que pode ser pensado como uma *função* que define o nome de um ponto de extremidade, seus metadados, seu protocolo e os detalhes da troca de declarações que o Identity Experience Framework deve executar.</span><span class="sxs-lookup"><span data-stu-id="90db2-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details the exchange of claims that the Identity Experience Framework should perform.</span></span>  <span data-ttu-id="90db2-194">Quando essa *função* é chamada em uma etapa de orquestração ou de outro TechnicalProfile, o InputClaims e o OutputClaims são fornecidos como parâmetros pelo chamador.</span><span class="sxs-lookup"><span data-stu-id="90db2-194">When this *function* is called in an orchestration step or from another TechnicalProfile, the InputClaims and OutputClaims are provided as parameters by the caller.</span></span>


* <span data-ttu-id="90db2-195">Para tratamento completo em propriedades de extensão, confira o artigo [EXTENSÕES DE ESQUEMA DE DIRETÓRIO | CONCEITOS DA API DO GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="90db2-195">For full treatment on extension properties, see the article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="90db2-196">Atributos de extensão na API do Graph são nomeados usando a convenção `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="90db2-196">Extension attributes in Graph API are named using the convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="90db2-197">Políticas personalizadas se referem aos atributos de extensões como extension_attributename, omitindo o ApplicationObjectId no XML</span><span class="sxs-lookup"><span data-stu-id="90db2-197">Custom policies refer to extensions attributes as extension_attributename, thus omitting the ApplicationObjectId in the XML</span></span>
