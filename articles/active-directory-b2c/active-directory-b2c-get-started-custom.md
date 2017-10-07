---
title: "Azure Active Directory B2C: introdução às políticas personalizadas | Microsoft Docs"
description: "Como tooget iniciado com as políticas personalizadas do Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C: introdução às políticas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Depois de concluir as etapas de saudação neste artigo, a política personalizada oferecerá suporte a "conta local" inscrever-se ou entrar por meio de um endereço de email e senha. Você também preparará o ambiente para adicionar provedores de identidade (como Facebook ou Azure Active Directory). Recomendamos que você toocomplete estas etapas antes de ler sobre outros usos de saudação do Framework de experiência de identidade de B2C do Azure Active Directory (AD do Azure).

## <a name="prerequisites"></a>Pré-requisitos

Antes de prosseguir, verifique se você tem um locatário do Azure AD B2C, que é um contêiner para todos os seus usuários, aplicativos, políticas e muito mais. Se você não tiver um já, será necessário muito[criar um locatário Azure AD B2C](active-directory-b2c-get-started.md). É altamente incentivamos Olá toocomplete de todos os desenvolvedores do Azure AD B2C explicações passo a passo de política interna e configurar seus aplicativos com políticas internas antes de continuar. Seus aplicativos funcionará com os dois tipos de políticas quando você fizer uma alteração secundária toohello política nome tooinvoke Olá política personalizada.

>[!NOTE]
>edição de política personalizada tooaccess, é necessário um locatário tooyour vinculado de assinatura do Azure válida. Se você ainda não [vinculado sua tooan de locatário do Azure AD B2C assinatura do Azure](active-directory-b2c-how-to-enable-billing.md) ou sua assinatura do Azure está desabilitada, Olá identidade experiência Framework botão não estará disponível.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>Adicionar assinatura e criptografia locatário tooyour B2C de chaves para uso por políticas personalizadas

1. Olá abrir **identidade experiência Framework** folha em suas configurações de locatário do Azure AD B2C.
2. Selecione **chaves política** tooview chaves de saudação disponíveis em seu locatário.
3. Crie a B2C_1A_TokenSigningKeyContainer, se não existir:<br>
    a. Selecione **Adicionar**. <br>
    b. Selecione **Gerar**.<br>
    c. Para o **Nome**, use `TokenSigningKeyContainer`. <br> 
    prefixo de saudação `B2C_1A_` podem ser adicionadas automaticamente.<br>
    d. Para o **Tipo de chave**, use **RSA**.<br>
    e. Para **datas**, usar padrões de saudação. <br>
    f. Para o **Uso da chave**, use **Assinatura**.<br>
    g. Selecione **Criar**.<br>
4. Crie a B2C_1A_TokenEncryptionKeyContainer, se não existir:<br>
 a. Selecione **Adicionar**.<br>
 b. Selecione **Gerar**.<br>
 c. Para o **Nome**, use `TokenEncryptionKeyContainer`. <br>
   prefixo de saudação `B2C_1A`_ podem ser adicionadas automaticamente.<br>
 d. Para o **Tipo de chave**, use **RSA**.<br>
 e. Para **datas**, usar padrões de saudação.<br>
 f. Para o **Uso da chave**, use **Criptografia**.<br>
 g. Selecione **Criar**.<br>
5. Crie o B2C_1A_FacebookSecret. <br>
Se você já tiver um segredo do aplicativo Facebook, adicioná-lo como um locatário tooyour chave de política. Caso contrário, você deve criar chave Olá com um valor de espaço reservado para que as políticas sejam aprovados.<br>
 a. Selecione **Adicionar**.<br>
 b. Para as **Opções**, use **Manual**.<br>
 c. Para o **Nome**, use `FacebookSecret`. <br>
 prefixo de saudação `B2C_1A_` podem ser adicionadas automaticamente.<br>
 d. Em Olá **segredo** , digite sua FacebookSecret de developers.facebook.com ou `0` como um espaço reservado. *Esse não é a sua ID do aplicativo Facebook.* <br>
 e. Para o **Uso da chave**, use **Assinatura**. <br>
 f. Selecione **Criar** e confirme a criação.

## <a name="register-identity-experience-framework-applications"></a>Registrar aplicativos do Identity Experience Framework

B2C do AD do Azure requer tooregister dois aplicativos adicionais que são usados por Olá mecanismo toosign backup e entre os usuários.

>[!NOTE]
>Você deve criar dois aplicativos que permitem entrar usando contas locais: IdentityExperienceFramework (um aplicativo web) e ProxyIdentityExperienceFramework (um aplicativo nativo) com recebido permissão do aplicativo de IdentityExperienceFramework hello. As contas locais só existem em seu locatário. Os usuários se inscrever com um tooaccess de combinação de endereço e senha de email exclusivo seus aplicativos de locatário registrado.

### <a name="create-hello-identityexperienceframework-application"></a>Criar aplicativo de IdentityExperienceFramework hello

1. Em Olá [portal do Azure](https://portal.azure.com), alternar para Olá [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md).
2. Olá abrir **Active Directory do Azure** folha (Olá não **do Azure AD B2C** folha). Talvez seja necessário tooselect **mais serviços** toofind-lo.
3. Selecione **Registros do Aplicativo**.
4. Selecione **Novo registro de aplicativo**.
   * Para o **Nome**, use `IdentityExperienceFramework`.
   * Para o **Tipo de aplicativo**, use **Aplicativo Web/API**.
   * Para a **URL de Entrada**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, em que `yourtenant` é o nome de domínio do seu locatário do Azure AD B2C.
5. Selecione **Criar**.
6. Quando ele é criado, selecione o aplicativo hello recém-criado **IdentityExperienceFramework**.<br>
   * Selecione **Propriedades**.<br>
   * Copie a ID do aplicativo hello e salvá-lo para mais tarde.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Criar aplicativo de ProxyIdentityExperienceFramework hello

1. Selecione **Registros do Aplicativo**.
1. Selecione **Novo registro de aplicativo**.
   * Para o **Nome**, use `ProxyIdentityExperienceFramework`.
   * Para o **Tipo de aplicativo**, use **Nativo**.
   * Para a **URI de Redirecionamento**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, em que `yourtenant` é o seu locatário do Azure AD B2C.
1. Selecione **Criar**.
1. Depois de ele ter sido criado, selecione o aplicativo hello **ProxyIdentityExperienceFramework**.<br>
   * Selecione **Propriedades**. <br>
   * Copie a ID do aplicativo hello e salvá-lo para mais tarde.
1. Selecione **Permissões necessárias**.
1. Selecione **Adicionar**.
1. Selecione **Selecionar uma API**.
1. Pesquisar por nome hello IdentityExperienceFramework. Selecione **IdentityExperienceFramework** Olá resultados e, em seguida, clique em **selecione**.
1. Selecione caixa de seleção Olá Avançar muito**acesso IdentityExperienceFramework**e, em seguida, clique em **selecione**.
1. Selecione **Concluído**.
1. Selecione **Conceder Permissões** e, em seguida, confirme selecionando **Sim**.

## <a name="download-starter-pack-and-modify-policies"></a>Baixar o pacote de início e modificar políticas

Políticas personalizadas são um conjunto de arquivos XML que precisam de locatário de tooyour do Azure AD B2C toobe carregado. Fornecemos starter pacotes tooget sobre rapidamente. Cada pacote de inicializador Olá lista a seguir contém o menor número Olá perfis técnicos e Jornadas de usuário necessária cenários de saudação tooachieve descritos:
 * LocalAccounts. Permite o uso de saudação do somente para contas locais.
 * SocialAccounts. Permite o uso de saudação somente contas social (ou federado).
 * **SocialAndLocalAccounts**. Usamos este arquivo hello passo a passo.
 * SocialAndLocalAccountsWithMFA. As opções de Autenticação Multifator, local e social estão incluídas aqui.

Cada pacote de início contém:

* Olá [arquivo base](active-directory-b2c-overview-custom.md#policy-files) da política de saudação. Algumas modificações são necessária toohello base.
* Olá [arquivo de extensão](active-directory-b2c-overview-custom.md#policy-files) da política de saudação.  Esse arquivo é o local em que a maioria das alterações de configuração é feita.
* [Arquivos de terceira parte confiável](active-directory-b2c-overview-custom.md#policy-files) são os arquivos específicos de tarefa, chamados pelo aplicativo.

>[!NOTE]
>Se seu editor de XML compatível com a validação, valide os arquivos de saudação com base no esquema de XML TrustFrameworkPolicy_0.3.0.0.xsd Olá que está localizado no diretório raiz de saudação do pacote de inicializador de saudação. A validação de esquema XML identifica erros antes do upload.

 Vamos começar:

1. Baixe o active-directory-b2c-custom-policy-starterpack do GitHub. [Baixe o arquivo. zip de saudação](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) ou execute

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Abra a pasta de SocialAndLocalAccounts hello.  arquivo base Hello (TrustFrameworkBase.xml) nessa pasta contém conteúdo necessário para contas locais e social/corporativa. conteúdo social Olá não interfere nas etapas Olá para colocar as contas locais em execução.
3. Abra o TrustFrameworkBase.xml. Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.
4. Na raiz da saudação `TrustFrameworkPolicy` elemento, Olá atualização `TenantId` e `PublicPolicyUri` atributos, substituindo `yourtenant.onmicrosoft.com` com o nome de domínio de saudação do seu locatário do Azure AD B2C:
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`é o nome hello da política que você vê no portal de saudação e o nome de Olá pelo qual este arquivo de política é referenciado por outros arquivos de política.

5. Salve o arquivo hello.
6. Abra o TrustFrameworkExtensions.xml. Alterar Olá mesmo dois substituindo `yourtenant.onmicrosoft.com` com seu locatário do Azure AD B2C. Verifique Olá mesmo substituição em Olá `<TenantId>` elemento para um total de três alterações. Salve o arquivo hello.
7. Abra o SignUpOrSignIn.xml. Alterar Olá mesmo substituindo `yourtenant.onmicrosoft.com` com seu locatário do Azure AD B2C em três locais. Salve o arquivo hello.
8. Redefinição de senha Olá aberto e perfil Editar arquivos. Alterar Olá mesmo substituindo `yourtenant.onmicrosoft.com` com seu locatário do Azure AD B2C em três locais em cada arquivo. Salve arquivos hello.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Adicionar política personalizada do hello aplicativo IDs tooyour
Adicione o arquivo de extensões do hello aplicativo IDs toohello (`TrustFrameworkExtensions.xml`):

1. No arquivo de extensões de saudação (TrustFrameworkExtensions.xml), localizar o elemento de saudação `<TechnicalProfile Id="login-NonInteractive">`.
2. Substitua as duas instâncias de `IdentityExperienceFrameworkAppId` com ID de aplicativo de saudação do hello application Framework de experiência de identidade que você criou anteriormente. Aqui está um exemplo:

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. Substitua as duas instâncias de `ProxyIdentityExperienceFrameworkAppId` com ID de aplicativo de saudação do hello application Framework de experiência de identidade de Proxy que você criou anteriormente.
4. Salve o arquivo de extensões.

## <a name="upload-hello-policies-tooyour-tenant"></a>Carregar o locatário do hello políticas tooyour

1. Em Olá [portal do Azure](https://portal.azure.com), alternar para Olá [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra hello **do Azure AD B2C** folha.
2. Selecione **Estrutura de Experiência de Identidade**.
3. Selecione **Carregar Política**.

    >[!WARNING]
    >arquivos de política personalizada de saudação devem ser carregados no hello ordem a seguir:

1. Carregue o TrustFrameworkBase.xml.
2. Carregue o TrustFrameworkExtensions.xml.
3. Carregue o SignUpOrSignin.xml.
4. Carregue os outros arquivos de política.

Quando um arquivo é carregado, o nome de saudação do arquivo de política de saudação é anexado com `B2C_1A_`.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testar a política personalizada do hello usando Executar agora

1. Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.

   >[!NOTE]
   >**Executar agora** requer pelo menos um aplicativo toobe pré-registrado no locatário hello. Aplicativos devem ser registrados no locatário Olá B2C usando Olá **aplicativos** seleção de menu no Azure AD B2C ou usando Olá identidade experiência Framework tooinvoke políticas internas e personalizadas. Somente um registro por aplicativo é necessário.<br><br>
   toolearn como tooregister aplicativos, consulte hello Azure AD B2C [começar](active-directory-b2c-get-started.md) artigo ou hello [registro do aplicativo](active-directory-b2c-app-registration.md) artigo.  

2. Abra B2C_1A_signup_signin, Olá política personalizada do terceira parte confiável (RP) que você carregou. Selecione **Executar Agora**.

3. Você deve ser capaz de toosign usando um endereço de email.

4. Entrar com hello mesma conta tooconfirm tiver Olá configuração correta.

>[!NOTE]
>Uma causa comum de falha de entrada é um aplicativo IdentityExperienceFramework configurado incorretamente.


## <a name="next-steps"></a>Próximas etapas

### <a name="add-facebook-as-an-identity-provider"></a>Adicionar o Facebook como um provedor de identidade
tooset o Facebook:
1. [Configurar um aplicativo do Facebook em developers.facebook.com](active-directory-b2c-setup-fb-app.md).
2. [Adicionar Olá Facebook aplicativo tooyour segredo do Azure AD B2C locatário](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).
3. No arquivo de política de TrustFrameworkExtensions hello, substitua o valor de saudação do `client_id` com a ID do aplicativo Facebook hello:

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Carregar o locatário do hello TrustFrameworkExtensions.xml política arquivo tooyour.
5. Teste usando **executar agora** ou invocando política Olá diretamente do seu aplicativo registrado.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Adicionar o Azure Active Directory como um provedor de identidade
o arquivo de base Olá usado neste guia de Introdução ao obter já contém Olá conteúdo que você precisa para adicionar outros provedores de identidade. Para obter informações sobre como configurar logons, consulte Olá [do Azure Active Directory B2C: entrar usando contas do AD do Azure](active-directory-b2c-setup-aad-custom.md) artigo.

Para obter uma visão geral de políticas personalizadas no Azure AD B2C que usam saudação do Framework de experiência de identidade, consulte Olá [do Azure Active Directory B2C: políticas personalizadas](active-directory-b2c-overview-custom.md) artigo. 
