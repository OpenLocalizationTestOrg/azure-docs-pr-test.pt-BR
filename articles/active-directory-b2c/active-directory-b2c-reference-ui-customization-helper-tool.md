---
title: "Azure Active Directory B2C: ferramenta auxiliar de personalização da IU da página | Microsoft Docs"
description: "Uma ferramenta de auxiliar usado o recurso de personalização de interface do usuário do toodemonstrate Olá página no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>B2C de diretório ativo do Azure: Uma ferramenta de auxiliar usado o recurso personalização de interface de usuário do toodemonstrate Olá página
Este artigo é um complemento toohello [artigo de personalização da interface do usuário principal](active-directory-b2c-reference-ui-customization.md) em B2C do Azure Active Directory (AD do Azure). Olá etapas a seguir descrevem como tooexercise Olá o recurso de personalização da interface do usuário de página usando o conteúdo HTML e CSS de exemplo que fornecemos.

## <a name="get-an-azure-ad-b2c-tenant"></a>Obter um locatário do Azure AD B2C
Antes de você pode personalizar qualquer coisa, você precisará de muito[obter um locatário Azure AD B2C](active-directory-b2c-get-started.md) se você ainda não tiver um.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Criar uma política de inscrição ou credenciais
Hello fornecemos de conteúdo de exemplo pode ser usado toocustomze duas páginas em um [política inscrever-se ou entrar](active-directory-b2c-reference-policies.md): Olá [página de entrada unificada](active-directory-b2c-reference-ui-customization.md) e hello [atributos auto-declaradas página](active-directory-b2c-reference-ui-customization.md). Ao [criar a política de inscrição ou de entrada](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), adicione Conta Local (endereço de email), o Facebook, o Google+ e a Microsoft como **Provedores de identidade**. Esses são Olá somente IDPs que nosso conteúdo HTML de exemplo serão aceitas.  Você também pode adicionar um subconjunto desses IDPs, se desejar.

## <a name="register-an-application"></a>Registrar um aplicativo
Você precisará de muito[registrar um aplicativo](active-directory-b2c-app-registration.md) no seu B2C locatário que pode ser usado tooexecute sua política. Depois de registrar seu aplicativo, você tem algumas opções que você pode usar tooactually executar sua política de inscrição:

* Compile uma saudação do Azure AD B2C aplicativos de início rápido listados na seção hello "Introdução" [inscrever-se e entrar consumidores em seus aplicativos](active-directory-b2c-overview.md#get-started).
* Saudação de uso predefinida [parque do Azure AD B2C](https://aadb2cplayground.azurewebsites.net) aplicativo. Se você escolher o espaço de saudação toouse, você deve registrar um aplicativo em seu locatário B2C usando Olá **URI de redirecionamento** `https://aadb2cplayground.azurewebsites.net/`.
* Saudação de uso **executar agora** botão em sua política de saudação [portal do Azure](https://portal.azure.com/).

## <a name="customize-your-policy"></a>Personalizar a política
toocustomize Olá aparência de sua política, você precisa toofirst criar arquivos HTML e CSS usando convenções específicas de saudação do Azure AD B2C. Em seguida, você pode carregar seu local disponível publicamente tooa conteúdo estático para que o Azure AD B2C pode acessá-lo. Esse local pode ser seu próprio servidor Web dedicado, o Armazenamento de Blobs do Azure, a Rede de Distribuição de Conteúdo do Azure ou qualquer outro recurso estático que esteja hospedando o provedor. Olá únicos requisitos são que o conteúdo está disponível via HTTPS e pode ser acessado por meio de CORS. Depois que tiver exposto seu conteúdo estático na web hello, você pode editar o local da diretiva toopoint toothis e presentes que clientes tooyour de conteúdo. Olá [artigo de personalização da interface do usuário principal](active-directory-b2c-reference-ui-customization.md) descreve detalhadamente como funciona o recurso de personalização de saudação do Azure AD B2C.

Para fins de saudação deste tutorial, nós já criou algum conteúdo de exemplo e hospedado-lo no armazenamento de BLOBs do Azure. conteúdo de exemplo Hello é uma personalização muito básica no tema Olá de nossa empresa fictícia, "Wingtip Toys". tootry-lo em sua própria política, siga estas etapas:

1. Entrar no locatário tooyour em Olá [portal do Azure](https://portal.azure.com/) e navegue toohello B2C folha de recursos.
2. Clique em **Políticas de inscrição ou de entrada** e clique em sua política (por exemplo, "b2c1signupsignin\_1\_sign\_up\_sign\_in").
3. Clique na **Personalização da interface do usuário da Página** e na **Página de inscrição ou de entrada unificada**.
4. Saudação de alternância **página personalizada de uso** alternar muito**Sim**. Em Olá **página personalizada URI** , digite `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. Clique em **OK**.
5. Clique em **Página de inscrição da conta local**. Saudação de alternância **usar o modelo personalizado** alternar muito**Sim**. Em Olá **página personalizada URI** , digite `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
6. Olá repetição mesma etapa para Olá **página de inscrição de conta Social**.
   Clique em **Okey** duas vezes tooclose Olá UI personalização folhas.
7. Clique em **Salvar**.

Agora, você pode testar a política personalizada. Você pode usar seu próprio espaço de aplicativo ou hello B2C do Azure AD, se desejar, mas você pode simplesmente clicar Olá **executar agora** comando na folha de política de saudação. Selecione seu aplicativo na caixa de lista suspensa de saudação e escolha o URI de redirecionamento apropriado hello. Clique em Olá **executar agora** botão. Uma nova guia do navegador será aberta e você pode executar através da experiência do usuário Olá de inscrição em seu aplicativo com novo conteúdo Olá no lugar!

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Carregar tooAzure armazenamento de Blob do conteúdo de exemplo de hello
Se você quiser toouse armazenamento de BLOBs do Azure toohost sua página de conteúdo, você pode criar sua própria conta de armazenamento e usar nossos tooupload de ferramenta de auxiliar B2C seus arquivos.

### <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **+ Novo** > **Dados + armazenamento** > **Conta de armazenamento**. Você precisará de uma assinatura do Azure de toocreate uma conta de armazenamento de BLOBs do Azure. Você pode inscrever uma avaliação gratuita em Olá [site do Azure](https://azure.microsoft.com/pricing/free-trial/).
3. Forneça um **nome** para a conta de armazenamento da saudação (por exemplo, "contoso") e escolha Olá seleções apropriadas **preço**, **grupo de recursos** e  **Assinatura**. Certifique-se de que você tenha Olá **tooStartboard Pin** opção marcada. Clique em **Criar**.
4. Voltar toohello quadro inicial e clique na conta de armazenamento Olá que você acabou de criar.
5. Em Olá **resumo** seção, clique em **contêineres**e, em seguida, clique em **+ adicionar**.
6. Forneça um **nome** para o contêiner de saudação (por exemplo, "b2c") e selecione **Blob** como Olá **acessar o tipo**. Clique em **OK**.
7. contêiner de saudação que você criou aparecerá na lista de saudação em Olá **Blobs** folha. Anote a saudação URL do contêiner de saudação; Por exemplo, ela deve parecer muito`https://contoso.blob.core.windows.net/b2c`. Olá fechar **Blobs** folha.
8. Na folha de conta de armazenamento hello, clique em **chaves** e anote os valores hello Olá **nome da conta de armazenamento** e **chave de acesso primária** campos.

> [!NOTE]
> **Chave de Acesso Primária** é uma credencial de segurança importante.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Baixar arquivos de exemplo e a ferramenta de auxiliar Olá
Você pode baixar Olá [arquivos de exemplo e a ferramenta de auxiliar de armazenamento de BLOBs do Azure como um arquivo. zip](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) ou cloná-lo do GitHub:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Esse repositório contém um diretório `sample_templates\wingtip` , que inclui o exemplo HTML, CSS e as imagens. Para esses modelos tooreference sua própria conta de armazenamento de BLOBs do Azure, você precisará tooedit arquivos de saudação HTML. Abra `unified.html` e `selfasserted.html` e substitua todas as instâncias de `https://localhost` com URL de saudação do seu próprio contêiner que você anotou nas etapas anteriores hello. Você deve usar um caminho absoluto de saudação do Olá arquivos HTML, porque, nesse caso, Olá HTML será servido pelo AD do Azure, no domínio Olá `https://login.microsoftonline.com`.

### <a name="upload-hello-sample-files"></a>Carregar arquivos de exemplo hello
No mesmo repositório de hello, descompacte `B2CAzureStorageClient.zip` e execução hello `B2CAzureStorageClient.exe` dentro do arquivo. Esse programa simplesmente carregará todos os arquivos Olá Olá diretório que você especifica a conta de armazenamento tooyour e habilita o acesso CORS para os arquivos. Se você seguiu as etapas de saudação acima, hello HTML e arquivos CSS serão agora estar apontando tooyour conta de armazenamento. Observe que Olá nome da sua conta de armazenamento faz parte de saudação que precede `blob.core.windows.net`; por exemplo, `contoso`. Você pode verificar que o conteúdo de saudação foi carregado corretamente experimentando tooaccess `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` em um navegador. Também use [http://test-cors.org/](http://test-cors.org/) toomake-se de que o conteúdo de saudação agora CORS habilitado. (Procure "status XHR: 200" no resultado hello.)

### <a name="customize-your-policy-again"></a>Personalizar a política, novamente
Agora que você carregou a conta de armazenamento do próprio hello exemplo tooyour conteúdo, você deve editar sua política de inscrição tooreference-lo. Repita as etapas de saudação do hello ["Personalizar a política"](#customize-your-policy) seção acima, desta vez usando URLs de sua própria conta de armazenamento. Olá, por exemplo, o local do seu `unified.html` arquivo seria `<url-of-your-container>/wingtip/unified.html`.

Agora você pode usar o hello **executar agora** botão ou seu próprio aplicativo tooexecute a política novamente. Olá resultado deve pesquisar quase hello mesmo – você usou Olá mesmo em ambos os casos de exemplo HTML e CSS. No entanto, suas políticas agora fazem referência a sua própria instância do armazenamento de BLOBs do Azure, e você é tooedit livre e carregar arquivos de saudação novamente que você entre. Para obter mais informações sobre como personalizar hello HTML e CSS, consulte toohello [artigo principal de personalização da interface do usuário](active-directory-b2c-reference-ui-customization.md).

