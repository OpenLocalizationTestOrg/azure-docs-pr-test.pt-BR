---
title: "aaaSet uma página inicial personalizada para aplicativos publicados usando o Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Noções básicas de saudação abrange sobre conectores de Proxy de aplicativo do Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Definir uma home page personalizada para aplicativos publicados usando o Proxy de Aplicativo Azure AD

Este artigo aborda como tooconfigure aplicativos toodirect usuários tooa página inicial personalizada. Quando você publica um aplicativo com o Proxy de aplicativo, defina uma URL interna, mas, às vezes, que não é página Olá que seus usuários verá primeiro. Defina uma página inicial personalizada para que os usuários forem página direita toohello quando acessam aplicativos Olá Olá painel de acesso do Azure Active Directory ou o iniciador do aplicativo hello Office 365.

Quando os usuários iniciam um aplicativo hello, eles direcionado por padrão toohello URL de domínio raiz para o aplicativo publicado hello. página de aterrissagem Olá normalmente é definida como a URL da home page hello. Use hello Azure AD PowerShell módulo toodefine página inicial personalizada URLs quando desejar que o aplicativo tooland de usuários em uma página específica no aplicativo hello. 

Por exemplo:
- Dentro da rede corporativa, os usuários estão muito*https://ExpenseApp/login/login.aspx* toosign no e acessar seu aplicativo.
- Como você tem outros ativos como imagens que o Proxy de aplicativo precisa tooaccess no nível superior de saudação da estrutura de pasta hello, publicar aplicativo hello com *https://ExpenseApp* como Olá URL interna.
- Olá URL externa padrão é *https://ExpenseApp-contoso.msappproxy.net*, que não tem sua inscrição de toohello usuários na página.  
- Definir *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* como Olá toogive de URL da página inicial, seus usuários uma experiência perfeita. 

>[!NOTE]
>Quando você concede aos usuários acesso a aplicativos toopublished, Olá aplicativos são exibidos no hello [painel de acesso do AD do Azure](active-directory-saas-access-panel-introduction.md) e hello [iniciador do aplicativo do Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Antes de começar

Antes de configurar a URL da home page hello, lembre-Olá mente requisitos a seguir:

* Certifique-se de que esse caminho de saudação especificado é um caminho de subdomínio da URL de domínio de raiz de saudação.

  Se for a URL do domínio raiz de saudação, por exemplo, https://apps.contoso.com/app1/, Olá URL da página inicial que você configura deve começar com https://apps.contoso.com/app1/.

* Se você fizer uma alteração toohello publicado o aplicativo, alteração Olá pode redefinir o valor de saudação do hello URL da página inicial. Quando você atualiza o aplicativo hello Olá futura, você deve verificar novamente e, se necessário, atualize a URL da home page hello.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Alterar Olá home page no hello portal do Azure

1. Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.
2. Navegue muito**Active Directory do Azure** > **registros do aplicativo** e escolha o aplicativo hello lista. 
3. Selecione **propriedades** das configurações da saudação.
4. Saudação de atualização **URL da Home page** campo com o novo caminho. 

   ![Forneça a nova URL da página inicial](./media/application-proxy-office365-app-launcher/homepage.png)

5. Selecione **Salvar**

## <a name="change-hello-home-page-with-powershell"></a>Alterar Olá home page com o PowerShell

### <a name="install-hello-azure-ad-powershell-module"></a>Instalar o módulo do PowerShell do Azure AD Olá

Antes de definir uma URL de página inicial personalizada usando o PowerShell, instale o módulo do PowerShell do Azure AD hello. Você pode baixar o pacote de saudação do hello [Galeria do PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), que usa Olá ponto de extremidade de API do Graph. 

Olá tooinstall do pacote, siga estas etapas:

1. Abrir uma janela do PowerShell padrão e, em seguida, execute Olá comando a seguir:

    ```
     Install-Module -Name AzureAD
    ```
    Se você estiver executando o comando hello como não administrador, use Olá `-scope currentuser` opção.
2. Durante a instalação do hello, selecione **Y** tooinstall dois pacotes de Nuget.org. Ambos os pacotes são necessários. 

### <a name="find-hello-objectid-of-hello-app"></a>Localize Olá ObjectID do aplicativo hello

Obter Olá ObjectID do aplicativo hello e, em seguida, procure o aplicativo de saudação por sua página inicial.

1. Abra o PowerShell e importe o módulo de saudação do AD do Azure.

    ```
    Import-Module AzureAD
    ```

2. Entre toohello módulo AD do Azure como administrador de locatários hello.

    ```
    Connect-AzureAD
    ```
3. Localize o aplicativo hello com base em sua URL da página inicial. Você pode encontrar hello URL no portal de saudação indo muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos**. Este exemplo usa *sharepoint-iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Você deve obter um resultado semelhante toohello mostrada aqui. Saudação de cópia toouse ObjectID GUID na próxima seção, Olá.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>Atualizar a URL da home page Olá

Olá mesmo módulo do PowerShell que você usou para a etapa 1, executar Olá etapas a seguir:

1. Confirme se você tem Olá corrigir o aplicativo e substitua *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* com hello ObjectID que você copiou na saudação anterior da etapa.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Agora que você confirmou aplicativo hello, você está pronto tooupdate Olá home page da seguinte maneira.

2. Crie um toohold de objeto de aplicativo em branco alterações Olá que você deseja toomake. Essa variável contém valores hello que você deseja tooupdate. Nada é criado nesta etapa.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. Definir valor toohello de URL de página inicial de saudação que você deseja. valor de saudação deve ser um caminho de subdomínio do aplicativo publicado hello. Por exemplo, se você alterar Olá URL da página inicial do *https://sharepoint-iddemo.msappproxy.net/* muito*https://sharepoint-iddemo.msappproxy.net/hybrid/*, os usuários do aplicativo vá diretamente toohello personalizado página inicial.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Verifique Olá update usando Olá GUID (ID de objeto) que você copiou na "etapa 1: localizar Olá ObjectID do aplicativo hello."

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. tooconfirm que a alteração de saudação foi bem-sucedida, reinicie o aplicativo hello.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>As alterações feitas toohello aplicativo poderão redefinir Olá URL da página inicial. Se a URL da página inicial for redefinida, repita a etapa 2.

## <a name="next-steps"></a>Próximas etapas

- [Habilitar acesso remoto tooSharePoint com Proxy de aplicativo do Azure AD](application-proxy-enable-remote-access-sharepoint.md)
- [Habilitar Proxy de aplicativo no portal do Azure de saudação](active-directory-application-proxy-enable.md)
