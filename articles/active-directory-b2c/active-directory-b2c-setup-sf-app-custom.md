---
title: "Azure Active Directory B2C: adicionando um provedor SAML do Salesforce usando políticas personalizadas | Microsoft Docs"
description: "Saiba mais sobre como toocreate e gerenciar políticas personalizadas do Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C: entrar usando contas do Salesforce via SAML

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artigo mostra como toouse [políticas personalizadas](active-directory-b2c-overview-custom.md) tooset a entrada de usuários de uma organização de vendas específica.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="azure-ad-b2c-setup"></a>Configuração do Azure AD B2C

Certifique-se de que você concluiu todas as etapas de saudação que mostram como muito[Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md) no Azure Active Directory B2C (Azure AD B2C).

Estão incluídos:

* Criar um locatário do Azure AD B2C.
* Criar um aplicativo Azure AD B2C.
* Registrar dois aplicativos de mecanismo de políticas.
* Configurar chaves.
* Configure o pacote de inicializador de saudação.

### <a name="salesforce-setup"></a>Configuração do Salesforce

Neste artigo, vamos supor que você já tenha feito o seguinte hello:

* Inscreveu-se em uma conta do Salesforce. Você pode se inscrever em uma [conta gratuita do Developer Edition](https://developer.salesforce.com/signup).
* [Configurou Meu Domínio](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) para sua organização do Salesforce.

## <a name="set-up-salesforce-so-users-can-federate"></a>Configurar o Salesforce para que os usuários possam estabelecer a federação

toohelp do Azure AD B2C se comunicar com a equipe de vendas, é necessário o URL de metadados de Salesforce tooget hello.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Configurar o Salesforce como um provedor de identidade

> [!NOTE]
> Neste artigo, presumimos que você esteja usando o [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).

1. [Entrar tooSalesforce](https://login.salesforce.com/). 
2. Na saudação esquerda menu em **configurações**, expanda **identidade**e, em seguida, clique em **provedor de identidade**.
3. Clique em **Habilitar Provedor de Identidade**.
4. Em **certificado Olá selecione**, selecione Olá certificado Salesforce toouse toocommunicate com o Azure AD B2C. (Você pode usar o certificado padrão de hello.) Clique em **Salvar**. 

### <a name="create-a-connected-app-in-salesforce"></a>Criar um aplicativo conectado no Salesforce

1. Em Olá **provedor de identidade** página, ir muito**provedores de serviço**.
2. Clique em **Os Provedores de Serviço agora são criados por meio de Aplicativos Conectados. Clique aqui.**
3. Em **informações básicas**, insira valores hello necessários para seu aplicativo conectado.
4. Em **configurações do aplicativo Web**, selecione Olá **habilitar SAML** caixa de seleção.
5. Em Olá **ID da entidade** digite Olá URL a seguir. Certifique-se de que você substitua o valor de saudação para `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. Em Olá **URL do ACS** digite Olá URL a seguir. Certifique-se de que você substitua o valor de saudação para `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. Deixe valores padrão de saudação para todas as outras configurações.
8. Role toohello inferior da lista de saudação e, em seguida, clique em **salvar**.

### <a name="get-hello-metadata-url"></a>Obter URL de metadados de saudação

1. Na página de visão geral de saudação do seu aplicativo conectado, clique em **gerenciar**.
2. Copiar valor Olá **ponto de extremidade de descoberta de metadados**e, em seguida, salvá-lo. Você o usará posteriormente neste artigo.

### <a name="set-up-salesforce-users-toofederate"></a>Configurar toofederate de usuários do Salesforce

1. Em Olá **gerenciar** página do aplicativo conectado, vá muito**perfis**.
2. Clique em **Gerenciar Perfis**.
3. Selecione perfis hello (ou grupos de usuários) que você deseja toofederate com o Azure AD B2C. Como um administrador do sistema, selecione Olá **administrador do sistema** caixa de seleção para que você pode federar usando sua conta do Salesforce.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Gerar um certificado de autenticação para o Azure AD B2C

Solicitações enviadas tooSalesforce necessidade toobe assinado pelo Azure AD B2C. toogenerate um certificado de assinatura, abra o Azure PowerShell e execute Olá comandos a seguir.

> [!NOTE]
> Certifique-se de que você atualize o nome do locatário hello e a senha em duas linhas de saudação superior.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Adicionar certificado tooAzure assinatura Olá SAML AD B2C

Carregar Olá locatário de tooyour do Azure AD B2C do certificado de assinatura: 

1. Vá locatário tooyour B2C do Azure AD. Clique em **Configurações** > **Estrutura de Experiência de Identidade** > **Chaves da Política**.
2. Clique em **+Adicionar** e, em seguida:
    1. Clique em **Opções** > **Carregar**.
    2. Insira um **Nome** (por exemplo, SAMLSigningCert). prefixo de saudação *B2C_1A_* é adicionado automaticamente toohello nome da chave.
    3. tooselect seu certificado, selecione **carregar o controle de arquivo**. 
    4. Insira a senha do certificado Olá definida no script do PowerShell hello.
3. Clique em **Criar**.
4. Verifique se você criou uma chave (por exemplo, B2C_1A_SAMLSigningCert). Anote o nome completo da saudação (incluindo *B2C_1A_*). Você fará referência chave toothis posteriormente na política de saudação.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>Criar hello Salesforce SAML provedor de declarações em sua política de base

É necessário toodefine Salesforce como um provedor de declarações para que os usuários possam se conectar usando a equipe de vendas. Em outras palavras, você precisa toospecify Olá ponto de extremidade do Azure AD B2C se comunicará. ponto de extremidade Olá será *fornecer* um conjunto de *declarações* B2C do Azure AD usa tooverify que um usuário específico autenticado. toodo isso, adicione um `<ClaimsProvider>` para a equipe de vendas no arquivo de extensão de saudação da política:

1. No diretório de trabalho, abra o arquivo de extensão da saudação (TrustFrameworkExtensions.xml).
2. Localize Olá `<ClaimsProviders>` seção. Se não existir, criá-lo sob o nó raiz de saudação.
3. Adicione um novo `<ClaimsProvider>`:

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

Em Olá `<ClaimsProvider>` nó:

1. Alterar valor Olá `<Domain>` tooa valor exclusivo que diferencia `<ClaimsProvider>` de outros provedores de identidade.
2. Atualizar valor Olá `<DisplayName>` tooa nome para exibição para Olá provedor de declarações. Atualmente, esse valor não é usado.

### <a name="update-hello-technical-profile"></a>Atualizar perfil técnica Olá

tooget um token SAML do Salesforce, definir protocolos de saudação do Azure AD B2C usará toocommunicate com o Azure Active Directory (AD do Azure). Fazer isso no hello `<TechnicalProfile>` elemento `<ClaimsProvider>`:

1. Atualizar a ID de saudação do hello `<TechnicalProfile>` nó. Essa ID é usada toorefer toothis perfil técnico de outras partes da política de saudação.
2. Atualizar o valor Olá para `<DisplayName>`. Esse valor é exibido no botão logon Olá na página de entrada.
3. Atualizar o valor Olá para `<Description>`.
4. A equipe de vendas usa o protocolo de saudação SAML 2.0. Verifique se esse valor Olá para `<Protocol>` é **SAML2**.

Saudação de atualização `<Metadata>` seção Olá anterior configurações de saudação do XML tooreflect para sua conta do Salesforce específica. Olá XML, atualize os valores de metadados hello:

1. Atualizar o valor de saudação do `<Item Key="PartnerEntity">` com URL de metadados de Salesforce Olá copiados anteriormente. Ele tem Olá formato a seguir: 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. Em Olá `<CryptographicKeys>` seção atualização Olá valor para ambas as instâncias de `StorageReferenceId` toohello nome da chave de saudação do seu certificado de autenticação (por exemplo, B2C_1A_SAMLSigningCert).

### <a name="upload-hello-extension-file-for-verification"></a>Carregue o arquivo de extensão de saudação para verificação

A política agora está configurada para que o Azure AD B2C sabe como toocommunicate com a equipe de vendas. Tente carregar o arquivo de extensão de saudação de sua política, tooverify que não existem problemas até o momento. arquivo de extensão tooupload Olá da política:

1. No seu locatário do Azure AD B2C, acesse toohello **todas as políticas** folha.
2. Selecione Olá **substituir a política de saudação se ela existe** caixa de seleção.
3. Carregar arquivo de extensão da saudação (TrustFrameworkExtensions.xml). Certifique-se de que ele não falhe na validação.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Registrar Olá jornada de usuário do Salesforce SAML declarações provedor tooa

Em seguida, adicione Olá tooone de provedor de identidade Salesforce SAML de seu Jornadas de usuário. Neste ponto, o provedor de identidade Olá foi configurado, mas não está disponível em qualquer uma das páginas de inscrição ou entrada de usuário hello. tooadd Olá identidade provedor tooa página de entrada, primeiro, crie uma duplicata de uma jornada de usuário do modelo existente. Em seguida, modificar o modelo de saudação para que ele também tem o provedor de identidade do AD do Azure hello.

1. Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).
2. Localize Olá `<UserJourneys>` elemento e, em seguida, hello de cópia inteira `<UserJourney>` valor, incluindo a Id = "SignUpOrSignIn".
3. Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml). Localize Olá `<UserJourneys>` elemento. Se o elemento de saudação não existir, crie um.
4. Saudação de colar todo copiada `<UserJourney>` como um filho do hello `<UserJourneys>` elemento.
5. Renomear a ID de saudação do hello novo `<UserJourney>` (por exemplo, SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>Botão de provedor de identidade de saudação de exibição

Olá `<ClaimsProviderSelection>` elemento é análogo tooan botão de provedor de identidade em uma página de inscrição ou entrar. Adicionando um `<ClaimsProviderSelection>` elemento para a equipe de vendas, um novo botão aparece quando um usuário sai toothis página. botão de provedor de identidade de saudação toodisplay:

1. Em Olá `<UserJourney>` que você criou, localize Olá `<OrchestrationStep>` com `Order="1"`.
2. Adicione Olá XML a seguir:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. Definir `TargetClaimsExchangeId` valor lógico tooa. É recomendável seguir Olá a mesma convenção de outros usuários (por exemplo,  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>Provedor de identidade do link Olá botão tooan ação

Agora que você tem um botão de provedor de identidade em vigor, vincule-tooan ação. Nesse caso, a ação de saudação é para o Azure AD B2C toocommunicate com a equipe de vendas tooreceive um token SAML. Você pode fazer isso por meio da vinculação perfil técnico Olá para o Salesforce SAML provedor de declarações:

1. Em Olá `<UserJourney>` nó, localizar Olá `<OrchestrationStep>` com `Order="2"`.
2. Adicione Olá XML a seguir:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. Atualização `Id` toohello mesmo valor que você usou anteriormente para `TargetClaimsExchangeId`.
4. Atualização `TechnicalProfileReferenceId` toohello `Id` de saudação técnica perfil você criou anteriormente (por exemplo, ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Carregar arquivo de extensão atualizada Olá

Você concluiu a modificar arquivo de extensão de saudação. Salve e carregue esse arquivo. Certifique-se de que todas as validações tenham êxito.

### <a name="update-hello-relying-party-file"></a>Atualizar o arquivo de parte confiável Olá

Em seguida, atualize Olá terceira parte confiável (RP) arquivo inicia jornada saudação do usuário que você criou:

1. Faça uma cópia de SignUpOrSignIn.xml em seu diretório de trabalho. Em seguida, renomeie-a (por exemplo, SignUpOrSignInWithAAD.xml).
2. Olá novo Olá abrir arquivo e atualização `PolicyId` atributo `<TrustFrameworkPolicy>` com um valor exclusivo. Este é o nome de saudação da política (por exemplo, SignUpOrSignInWithAAD).
3. Modificar Olá `ReferenceId` atributo `<DefaultUserJourney>` toomatch Olá `Id` de jornada usuário novo Olá que você criou (por exemplo, SignUpOrSignUsingContoso).
4. Salve suas alterações e, em seguida, carregue o arquivo hello.

## <a name="test-and-troubleshoot"></a>Testar e solucionar problemas

tootest Olá política personalizada que você acaba de carregar, em Olá portal do Azure, vá toohello folha de política e, em seguida, clique em **executar agora**. Se ela falhar, consulte [Solucionar problemas com políticas personalizadas](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Próximas etapas

Fornecer comentários muito[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
