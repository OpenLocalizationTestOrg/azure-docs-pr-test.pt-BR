---
title: "Personalizar uma interface do usuário usando políticas personalizadas – Azure AD B2C | Microsoft Docs"
description: "Saiba mais sobre como personalizar uma interface do usuário (UI) ao usar políticas personalizadas no Azure AD B2C."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Azure Active Directory B2C: Configurar a personalização da interface do usuário em uma política personalizada

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Depois de concluir este artigo, você terá uma política personalizada de inscrição e entrada com sua marca e aparência. Com o Azure Active Directory B2C (B2C do AD do Azure), você obtém controle quase total do conteúdo HTML e CSS Olá que apresentou toousers. Quando você usar uma política personalizada, configure personalização da interface do usuário em XML em vez de usar controles em Olá portal do Azure. 

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, conclua as etapas em [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md). Você deve ter uma política personalizada funcional para inscrição e conexão com contas locais.

## <a name="page-ui-customization"></a>Personalização da interface do usuário da página

Usando o recurso de personalização de interface do usuário de página hello, você pode personalizar Olá aparência de qualquer política personalizada. Também pode manter a consistência visual e da marca entre seu aplicativo e o Azure AD B2C.

É assim que ela funciona: o Azure AD B2C executa o código no navegador do cliente e usa uma abordagem moderna chamada [CORS (Compartilhamento de Recursos entre Origens)](http://www.w3.org/TR/cors/). Primeiro, você deve especificar uma URL em política personalizada do hello com conteúdo HTML personalizado. B2C do Azure AD mescla os elementos de interface do usuário com hello conteúdo HTML que é carregado de sua URL e, em seguida, exibe o cliente do hello página toohello.

## <a name="create-your-html5-content"></a>Crie seu conteúdo em HTML5

Crie HTML conteúdo com o nome de marca do produto no título de saudação.

1. Saudação de copiar o trecho HTML a seguir. Ela está bem formada HTML5 com um elemento vazio chamado  *\<div id = "api"\>\</div\>*  localizado dentro de saudação  *\<corpo\>*  marcas. Esse elemento indica onde o conteúdo do Azure AD B2C é toobe inserido.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >Por motivos de segurança, uso de saudação do JavaScript está bloqueado no momento para personalização.

2. Colar o trecho de saudação copiado em um editor de texto e, em seguida, salve o arquivo de saudação como *ui.html personalizar*.

## <a name="create-an-azure-blob-storage-account"></a>Criar uma conta de Armazenamento de Blobs do Azure

>[!NOTE]
> Neste artigo, usamos toohost de armazenamento de BLOBs do Azure nosso conteúdo. Você pode escolher toohost seu conteúdo em um servidor web, mas você deve [habilitar CORS em seu servidor web](https://enable-cors.org/server.html).

toohost este conteúdo HTML no armazenamento de Blob, Olá a seguir:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Em Olá **Hub** menu, selecione **novo** > **armazenamento** > **conta de armazenamento**.
3. Insira um **Nome** exclusivo para sua conta de armazenamento.
4. O **Modelo de implantação** pode permanecer **Gerenciador de Recursos**.
5. Alterar **o tipo de conta** muito**armazenamento de Blob**.
6. O **Desempenho** pode permanecer **Padrão**.
7. A **Replicação** pode permanecer **RA-GRS**.
8. A **Camada de acesso** pode permanecer **Dinâmica**.
9. A **Criptografia do serviço de armazenamento** pode permanecer **Desabilitada**.
10. Selecione uma **Assinatura** para a conta de armazenamento.
11. Crie um **Grupo de recursos** ou selecione um existente.
12. Selecione Olá **geográfica** para sua conta de armazenamento.
13. Clique em **criar** toocreate conta de armazenamento de saudação.  
    Após a implantação de hello, Olá **conta de armazenamento** folha será aberta automaticamente.

## <a name="create-a-container"></a>Criar um contêiner

toocreate um contêiner público no armazenamento de Blob, Olá a seguir:

1. Clique em Olá **visão geral** guia.
2. Clique em **Contêiner**.
3. Em **Nome**, digite **$root**.
4. Definir **tipo de acesso** muito**Blob**.
5. Clique em **$root** novo contêiner do tooopen hello.
6. Clique em **Carregar**.
7. Clique o ícone da pasta Olá Avançar muito**selecionar um arquivo**.
8. Vá muito**ui.html personalizar**, que você criou anteriormente no hello [Page UI customization](#the-page-ui-customization-feature) seção.
9. Clique em **Carregar**.
10. Selecione o blob ui.html personalizar Olá carregado.
11. Avançar muito**URL**, clique em **cópia**.
12. Em um navegador, cole a URL de saudação copiada e vá toohello site. Se o site Olá estiver inacessível, certifique-se de tipo de acesso do contêiner hello está definido muito**blob**.

## <a name="configure-cors"></a>Configurar o CORS

Configure o armazenamento de Blob para compartilhamento de recursos entre origens fazendo Olá seguinte:

>[!NOTE]
>Deseja tootry recurso de personalização da interface do usuário hello usando nosso conteúdo HTML e CSS do exemplo? Fornecemos [uma ferramenta auxiliar simples](active-directory-b2c-reference-ui-customization-helper-tool.md) que carrega e configura nosso conteúdo de exemplo em sua conta de armazenamento de Blobs. Se você usar a ferramenta de hello, pular muito[modificar a política personalizada de inscrever-se ou entrar](#modify-your-sign-up-or-sign-in-custom-policy).

1. Em Olá **armazenamento** folha, em **configurações**, abra **CORS**.
2. Clique em **Adicionar**.
3. Para **Origens permitidas**, digite um asterisco (\*).
4. Em Olá **verbos permitidos** lista suspensa, selecione **obter** e **opções**.
5. Para **Cabeçalhos permitidos**, digite um asterisco (\*).
6. Para **Cabeçalhos expostos**, digite um asterisco (\*).
7. Para **Idade máxima (segundos)**, digite **200**.
8. Clique em **Adicionar**.

## <a name="test-cors"></a>Testar o CORS

Valide que você está pronto fazendo Olá seguinte:

1. Vá toohello [teste cors.org](http://test-cors.org/) site e, em seguida, cole URL Olá Olá **URL remota** caixa.
2. Clique em **Enviar Solicitação**.  
    Se você receber um erro, verifique se as [Configurações do CORS](#configure-cors) estão corretas. Talvez você também precise tooclear o cache do navegador ou abrir uma sessão de navegação em particular, pressionando Ctrl + Shift + P.

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>Modificar a política personalizada de inscrição ou conexão

No nível superior de saudação  *\<TrustFrameworkPolicy\>*  de marca, você deve encontrar  *\<BuildingBlocks\>*  marca. Dentro de saudação  *\<BuildingBlocks\>*  marcas, adicione um  *\<ContentDefinitions\>*  marca copiando Olá exemplo a seguir. Substituir *your_storage_account* com nome de saudação da sua conta de armazenamento.

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>Carregar a política personalizada atualizada

1. Em Olá [portal do Azure](https://portal.azure.com), [alternar no contexto de saudação do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e, em seguida, abra Olá **do Azure AD B2C** folha.
2. Clique em **Todas as Políticas**.
3. Clique em **Carregar Política**.
4. Carregar `SignUpOrSignin.xml` com hello  *\<ContentDefinitions\>*  marca que você adicionou anteriormente.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testar a política personalizada do hello usando **executar agora**

1. Em Olá **do Azure AD B2C** folha, ir muito**todas as políticas**.
2. Selecione Olá política personalizada que você carregou e, em seguida, clique em Olá **executar agora** botão.
3. Você deve ser capaz de toosign backup usando um endereço de email.

## <a name="reference"></a>Referência

Encontre modelos de exemplo para personalização da interface do usuário aqui:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

pasta de sample_templates/wingtip Olá contém Olá arquivos HTML a seguir:

| Modelo do HTML5 | Descrição |
|----------------|-------------|
| *phonefactor.html* | Use esse arquivo como modelo para uma página de autenticação multifator. |
| *resetpassword.html* | Use esse arquivo como modelo para uma página de esquecimento de senha. |
| *selfasserted.html* | Use esse arquivo como modelo para uma página de inscrição de conta social ou uma página de inscrição de conta local. |
| *unified.html* | Use esse arquivo como modelo para uma página de inscrição ou entrada unificada. |
| *updateprofile.html* | Use esse arquivo como modelo para uma página de atualização de perfil. |

Em Olá [modificar a seção política personalizada de inscrever-se ou entrar](#modify-your-sign-up-or-sign-in-custom-policy), você configurou a definição de conteúdo Olá para `api.idpselections`. conjunto completo de saudação de definição de conteúdo IDs são reconhecidos pelo framework de experiência de identidade de saudação do Azure AD B2C e suas descrições são em Olá a tabela a seguir:

| ID de definição de conteúdo | Descrição | 
|-----------------------|-------------|
| *api.error* | **Página de erro**. Essa página é exibida quando uma exceção ou um erro é encontrado. |
| *api.idpselections* | **Página de seleção de provedor de identidade**. Esta página contém uma lista de provedores que Olá o usuário podem escolher durante o logon de identidade. Essas opções são os provedores de identidade empresarial, provedores de identidade social, como Facebook e Google+, ou contas locais. |
| *api.idpselections.signup* | **Seleção de provedor de identidade para inscrição**. Esta página contém uma lista de provedores que Olá o usuário podem escolher durante a inscrição de identidade. Essas opções são os provedores de identidade empresarial, provedores de identidade social, como Facebook e Google+, ou contas locais. |
| *api.localaccountpasswordreset* | **Página de esquecimento de senha**. Esta página contém um formulário que o usuário Olá deve concluir tooinitiate uma redefinição de senha.  |
| *api.localaccountsignin* | **Página de entrada da conta local**. Esta página contém um formulário de entrada para entradas com uma conta local baseada em endereço de email ou nome de usuário. formulário de saudação pode conter uma caixa de entrada de texto e a caixa de entrada de senha. |
| *api.localaccountsignup* | **Página de inscrição da conta local**. Esta página contém um formulário de inscrição para inscrições com uma conta local baseada em endereço de email ou nome de usuário. formulário de saudação pode conter vários controles de entrada, como uma caixa de entrada de texto, uma caixa de entrada de senha, um botão de opção, caixas de lista suspensa de seleção única e selecionar várias caixas de seleção. |
| *api.phonefactor* | **Página de autenticação multifator**. Nesta página, os usuários podem verificar seus números de telefone (usando mensagem de texto ou por voz) durante a inscrição ou entrada. |
| *api.selfasserted* | **Página de inscrição de conta social**. Esta página contém um formulário de inscrição que deve ser preenchido pelos usuários ao se inscreverem usando uma conta existente de um provedor de identidade social, como o Facebook ou Google+. Esta página é semelhante toohello anterior página de inscrição de conta sociais, exceto para campos de entrada de senha hello. |
| *api.selfasserted.profileupdate* | **Página de atualização de perfil**. Esta página contém um formulário que os usuários podem usar tooupdate seu perfil. Esta página é semelhante toohello social página conta de inscrição, exceto para campos de entrada de senha hello. |
| *api.signuporsignin* | **Página de inscrição ou entrada unificada**. Esta página lida com ambos os Olá inscrição e entrada de usuários, que podem usar provedores de identidade corporativa, provedores de identidade de redes sociais, como o Facebook ou Google + ou contas locais.  |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre quais elementos de interface do usuário podem ser personalizados, confira [Guia de referência para personalização da interface do usuário para políticas internas](active-directory-b2c-reference-ui-customization.md) .
