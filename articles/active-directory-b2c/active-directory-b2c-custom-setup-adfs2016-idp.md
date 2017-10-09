---
title: "Azure Active Directory B2C: Adicionar ADFS como um provedor de identidade SAML usando políticas personalizadas"
description: "Um como-tooarticle sobre como configurar o ADFS 2016 usando o protocolo SAML e políticas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Adicionar ADFS como um provedor de identidade SAML usando políticas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Este artigo mostra como tooenable entrar para usuários de conta do AD FS através do uso de saudação do [políticas personalizadas](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Pré-requisitos

Olá concluir as etapas em Olá [guia de Introdução com políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.

As etapas incluem:

1.  Criar um objeto de confiança de terceira parte confiável do ADFS.
2.  Adicionando Olá ADFS terceira parte confiável certificado tooAzure AD B2C.
3.  Adicionar política de tooa do provedor de declarações.
4.  Conta ADFS Olá registrar declarações jornada de usuário do provedor tooa.
5.  Carregando tooan de política de saudação do Azure AD B2C locatário e testá-lo.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate uma terceira parte confiável com reconhecimento de declarações

toouse ADFS como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um ADFS terceira parte confiável e fornecê-lo com os parâmetros de saudação à direita.

tooadd uma terceira parte confiável nova confiança usando o snap-in de gerenciamento de TI de saudação AD e configurar manualmente as definições de hello, executar Olá procedimento a seguir em um servidor de Federação.

Associação **administradores**, ou equivalente, no computador local Olá toocomplete necessária mínima de saudação esse procedimento. Examine os detalhes sobre como usar as contas apropriadas hello e associações dos grupos em [locais e grupos do domínio padrão](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  Em Gerenciador do Servidor, clique em **Ferramentas** e depois selecione **Gerenciamento do ADFS**.

2.  Clique em **Adicionar Objeto de Confiança de Terceira Parte Confiável**.
    ![Adicionar Objeto de Confiança de Terceira Parte Confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  Em Olá **bem-vindo** escolha **reconhecimento de declaração** e clique em **iniciar**.
    ![Na página de boas-vindas hello, escolha o reconhecimento de declaração](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  Em Olá **Selecionar fonte de dados** , clique em **inserir manualmente dados sobre a terceira parte confiável Olá**e, em seguida, clique em **próximo**.
    ![Inserir dados sobre a terceira parte confiável Olá](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  Em Olá **especificar nome para exibição** página, digite um nome na **nome de exibição**, em **notas** digite uma descrição para essa terceira parte confiável e, em seguida, clique em **Avançar** .
    ![Especifique o Nome de Exibição e notas](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  Opcional. Se você tem um certificado de criptografia de token opcional, em seguida, em Olá **configurar certificado** , clique em **procurar** toolocate o arquivo de certificado e clique **próximo** .
    ![Configurar Certificado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  Em Olá **configurar URL** página, selecione Olá **habilitar o suporte para o protocolo WebSSO do SAML 2.0 de saudação** caixa de seleção. Em **URL do serviço de SSO do SAML 2.0 terceira parte confiável**, digite a URL do ponto de extremidade de serviço do hello SAML Security Assertion Markup Language () para essa terceira parte confiável e, em seguida, clique em **próximo**.  Para Olá **URL do serviço de SSO do SAML 2.0 terceira parte confiável**, cole Olá `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. Substitua {Locatário} com o nome do locatário (por exemplo, contosob2c.onmicrosoft.com) e Olá {política} com o nome da política extensões (por exemplo, B2C_1A_TrustFrameworkExtensions).
    > [!IMPORTANT]
    >nome da política Olá é Olá uma política signup_or_signin herda, nesse caso é: `B2C_1A_TrustFrameworkExtensions`.
    >Por exemplo hello URL pode ser: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![URL do serviço de SSO do SAML 2.0 da terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. Em Olá **configurar identificadores** especifique Olá mesma URL da etapa anterior de saudação, clique em **adicionar** tooadd-los toohello lista e, em seguida, clique em **próximo**.
    ![Identificadores de objeto de confiança de terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  Em Olá **escolha política de controle de acesso** selecione uma política e clique em **próximo**.
    ![Escolher a Política de Controle de Acesso](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  Em Olá **pronto tooAdd confiança** página, examine as configurações de saudação e, em seguida, clique em **próximo** toosave informações de confiança de sua terceira parte confiável.
    ![Salvar as informações de seu objeto de confiança de terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  Em Olá **concluir** , clique em **fechar**, essa ação exibe automaticamente Olá **editar regras de declaração** caixa de diálogo.
    ![Editar Regras de Declaração](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Clique em **Adicionar Regra**.  
      ![Adicionar nova regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  Em **Modelo de regra de declaração**, selecione **Enviar atributos do LDAP como declarações**.
    ![Selecione Enviar atributos do LDAP como regra de modelo de declarações](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Forneça o **Nome da regra de declaração**. Para Olá **repositório de atributos** selecione **selecione Active Directory** adicionar Olá declarações a seguir e clique em **concluir** e **Okey**.
    ![Definir propriedades de regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  No Gerenciador do servidor, selecione **terceira parte confiável** , em seguida, selecione Olá terceira parte confiável é criado e clique em **propriedades**.
    ![Editar propriedades da terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Uma terceira parte confiáveis (B2C demonstração) propriedades janela clique de Olá **assinatura** guia e clique em **adicionar**.  
    ![Definir assinatura](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  Adicione o certificado de assinatura (arquivo .cert, sem a chave privada).  
    ![Adicionar seu certificado de assinatura](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  Na janela de propriedades do hello terceira parte confiáveis (B2C demonstração) clique em **avançado** guia e alterar Olá **algoritmo de hash seguro** muito**SHA-1**, clique em **Okey**.  
    ![Definir o algoritmo de hash seguro tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Adicionar tooAzure de chave aplicativo AD B2C de conta ADFS Olá
Federação com contas do AD FS requer um segredo do cliente para ADFS tootrust de conta do Azure AD B2C em nome do aplicativo hello. Você precisa toostore seu certificado do AD FS no seu locatário do Azure AD B2C. 

1.  Vá locatário tooyour B2C do Azure AD e selecione **B2C configurações** > **Framework de experiência de identidade**
2.  Selecione **chaves política** tooview chaves de saudação disponíveis em seu locatário.
3.  Clique em **+Adicionar**.
4.  Para as **Opções**, use **Upload**.
5.  Para o **Nome**, use `ADFSSamlCert`.  
    prefixo de saudação `B2C_1A_` podem ser adicionadas automaticamente.
6.  No carregamento do arquivo hello, * * selecione o arquivo. pfx de certificado com chave privada. Observação: este certificado (com a chave privada de saudação) deve ser Olá aquele mesmo que emitidos e usados para a terceira parte confiável Olá ADFS.
![Carregar chave de política](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  Clique em **Criar**
8.  Confirme que você criou a chave Olá `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Adicionar um provedor de declarações à política de extensão
Se você quiser usuários toosign no usando a conta do AD FS, você precisa de conta ADFS toodefine como um provedor de declarações. Em outras palavras, você precisa toospecify do Azure AD B2C se comunica com um ponto de extremidade. ponto de extremidade Olá fornece um conjunto de declarações que são usados pelo Azure AD B2C tooverify que um usuário específico autenticado.

Defina o ADFS como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:

1. Abra o arquivo de política de extensão de saudação (TrustFrameworkExtensions.xml) do seu diretório de trabalho. Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.
2. Localize Olá `<ClaimsProviders>` seção
3. Adicionar Olá seguindo o trecho XML em Olá `ClaimsProviders` elemento e substituir `identityProvider` com o DNS (valor arbitrário que indica o seu domínio) e salve o arquivo hello. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Registrar tooSign de provedor de declarações do hello ADFS conta se ou entrar a jornada de usuário
Neste ponto, o provedor de identidade Olá configurado.  No entanto, não está disponível em qualquer uma das telas de entrada-o/entrada hello. Agora você precisa tooadd Olá ADFS conta identidade tooyour de usuário do provedor `SignUpOrSignIn` jornada de usuário. toomake-lo, podemos criar uma duplicata de uma jornada de usuário do modelo existente.  Em seguida, podemos modificá-la para que ela inclua o provedor de identidade ADFS hello:
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).
2.  Localize Olá `<UserJourneys>` elemento e cópia Olá todo conteúdo do `<UserJourneys>` nó.
3.  Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml) e localize Olá `<UserJourneys>` elemento. Se o elemento de saudação não existir, adicione um.
4.  Cole a todo o conteúdo de saudação `<UserJournesy>` nó que você copiou como um filho do hello `<UserJourneys>` elemento.

### <a name="display-hello-button"></a>Botão de saudação de exibição
Olá `<ClaimsProviderSelections>` elemento define a lista de saudação das opções de seleção de provedor de declarações e sua ordem.  `<ClaimsProviderSelection>`elemento é análogo tooan botão de provedor de identidade em uma página de entrada-o/entrar. Se você adicionar um `<ClaimsProviderSelection>` elemento para a conta do AD FS, um novo botão aparece quando um usuário chega na página de saudação. tooadd este elemento:

1.  Localize Olá `<UserJourney>` nó inclui `Id="SignUpOrSignIn"` em jornada saudação do usuário que você copiou.
2.  Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`
3.  Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Ação de link de saudação botão tooan

Agora que você tem um botão em vigor, é necessário toolink-tooan ação. ação de Olá, nesse caso, é para o Azure AD B2C toocommunicate com ADFS conta tooreceive um token. Ação de link Olá botão tooan vinculando perfil técnico Olá para o seu provedor de declarações do ADFS conta:

1.  Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.
2.  Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Certifique-se de saudação `Id` tem Olá mesmo valor de `TargetClaimsExchangeId` em Olá anterior seção.
> * Certifique-se de `TechnicalProfileReferenceId` é definido toohello perfil técnico que você criou anteriormente (Contoso-SAML2).

## <a name="upload-hello-policy-tooyour-tenant"></a>Carregar o locatário de tooyour política Olá
1.  Em Olá [portal do Azure](https://portal.azure.com), alternar para Olá [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra hello **do Azure AD B2C** folha.
2.  Selecione **Estrutura de Experiência de Identidade**.
3.  Olá abrir **todas as políticas** folha.
4.  Selecione **Carregar Política**.
5.  Verificar **substituir a política de saudação se ela existe** caixa.
6.  **Carregar** TrustFrameworkExtensions.xml e certifique-se de que ele não falha na validação de saudação

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testar a política personalizada do hello usando Executar agora
1.  Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.
2.  Abra **B2C_1A_signup_signin**, Olá política personalizada do terceira parte confiável (RP) que você carregou. Selecione **Executar Agora**.
3.  Você deve ser capaz de toosign usando a conta do AD FS.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcional] Registrar a jornada do hello ADFS conta declarações provedor tooProfile Editar usuário
Você pode querer provedor de identidade de conta tooadd Olá ADFS também tooyour usuário `ProfileEdit` jornada de usuário. toomake disponível, podemos Repita Olá último duas etapas:

### <a name="display-hello-button"></a>Botão de saudação de exibição
1.  Abra o arquivo de extensão de saudação da política (por exemplo, TrustFrameworkExtensions.xml).
2.  Localize Olá `<UserJourney>` nó inclui `Id="ProfileEdit"` em jornada saudação do usuário que você copiou.
3.  Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`
4.  Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Ação de link de saudação botão tooan
1.  Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.
2.  Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testar a política personalizada de perfil Editar hello usando Executar agora
1.  Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.
2.  Abra **B2C_1A_ProfileEdit**, Olá política personalizada do terceira parte confiável (RP) que você carregou. Selecione **Executar Agora**.
3.  Você deve ser capaz de toosign usando a conta do AD FS.

## <a name="download-hello-complete-policy-files"></a>Baixar arquivos de política completa Olá
Opcional: É recomendável que criar o seu cenário usando seus próprios arquivos de política personalizada após a conclusão Olá guia de Introdução com as políticas personalizadas percorrer. [Arquivos de exemplo de política apenas para referência](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
