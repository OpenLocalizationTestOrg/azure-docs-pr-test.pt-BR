---
title: Definir uma home page personalizada para aplicativos publicados usando o Proxy de Aplicativo Azure AD | Microsoft Docs
description: "Abora as noções básicas sobre os conectores do Proxy de Aplicativo Azure AD"
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
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Definir uma home page personalizada para aplicativos publicados usando o Proxy de Aplicativo Azure AD

Este artigo descreve como configurar aplicativos para direcionar os usuários para uma página inicial personalizada. Ao publicar um aplicativo com o Proxy do aplicativo, você define uma URL interna, mas, às vezes, essa não é a página que os usuários devem ver primeiro. Defina uma página inicial personalizada para que os usuários acessem a página correta quando acessarem os aplicativos do Painel de acesso do Azure Active Directory ou do iniciador de aplicativos do Office 365.

Quando os usuários iniciam o aplicativo, são direcionados por padrão para a URL de domínio raiz do aplicativo publicado. A página de aterrissagem é normalmente definida como a URL da home page. Use o módulo do PowerShell do Azure AD para definir URLs de página inicial personalizada quando desejar que os usuários do aplicativo acessem uma página específica no aplicativo. 

Por exemplo:
- Dentro da rede corporativa, os usuários usam a URL *https://ExpenseApp/login/login.aspx* para entrar e acessar seu aplicativo.
- Como você tem outros ativos como imagens que o Proxy do aplicativo precisa acessar no nível superior da estrutura de pasta, você publica o aplicativo com *https://ExpenseApp* como a URL interna.
- A URL externa padrão é *https://ExpenseApp-contoso.msappproxy.net*, que não leva os usuários até a página de entrada.  
- Defina *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* como a URL da página inicial para dar aos usuários uma experiência contínua. 

>[!NOTE]
>Quando você conceder aos usuários acesso a aplicativos publicados, os aplicativos são exibidos no [painel de acesso do Azure AD](active-directory-saas-access-panel-introduction.md) e [lançador de aplicativo do Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Antes de começar

Antes de definir a URL da página inicial, tenha em mente os seguintes requisitos:

* Garanta que o caminho especificado seja um caminho de subdomínio da URL raiz do domínio.

  Se a URL do domínio raiz for, por exemplo, https://apps.contoso.com/app1/, a URL da página inicial que você configura deverá começar com https://apps.contoso.com/app1/.

* Se você fizer uma alteração no aplicativo publicado, essa alteração poderá redefinir o valor da URL da home page. Quando você decidir atualizar o aplicativo no futuro, você deverá verificar novamente e, se necessário, atualizar a URL da home page.

## <a name="change-the-home-page-in-the-azure-portal"></a>Altere a home page no portal do Azure

1. Entre no [Portal do Azure](https://portal.azure.com) como administrador.
2. Navegue até **Azure Active Directory** > **Registros do aplicativo** e escolha o seu aplicativo na lista. 
3. Selecione **Propriedades** entre as configurações.
4. Atualize o campo **URL da Home page** com o novo caminho. 

   ![Forneça a nova URL da página inicial](./media/application-proxy-office365-app-launcher/homepage.png)

5. Selecione **Salvar**

## <a name="change-the-home-page-with-powershell"></a>Alterar a home page com o PowerShell

### <a name="install-the-azure-ad-powershell-module"></a>Instalar o módulo do Powershell do Azure AD

Antes de definir uma URL personalizada de página inicial usando o PowerShell, instale o módulo PowerShell do Azure AD. Baixe esse pacote da [Galeria do PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), que usa o ponto de extremidade de API do Graph. 

Para instalar o pacote, siga estas etapas:

1. Abra uma janela padrão do PowerShell e, em seguida, execute o seguinte comando:

    ```
     Install-Module -Name AzureAD
    ```
    Se você estiver executando o comando como um não administrador, use a opção `-scope currentuser`.
2. Durante a instalação, selecione **Y** para instalar dois pacotes do Nuget.org. Ambos os pacotes são necessários. 

### <a name="find-the-objectid-of-the-app"></a>Localizar a ObjectID do aplicativo

Obtenha o ID do objeto do aplicativo e, em seguida, procure o aplicativo por sua home page.

1. Abra o PowerShell e importe o módulo do Azure AD.

    ```
    Import-Module AzureAD
    ```

2. Entre no módulo Azure AD como o administrador de locatários.

    ```
    Connect-AzureAD
    ```
3. Localize o aplicativo com base na respectiva URL da home page. Você pode localizar a URL no portal indo para **Azure Active Directory** > **Aplicativos empresariais** > **Todos os aplicativos**. Este exemplo usa *sharepoint-iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Você deve obter um resultado semelhante ao mostrado aqui. Copie o GUID do ObjectID para usar na próxima seção.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a>Atualizar a URL da home page

No mesmo módulo do PowerShell que você usou para a etapa 1, realize as seguintes etapas:

1. Confirme se você tem o aplicativo correto e substitua *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* pelo ObjectID que você copiou na etapa anterior.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Agora que você confirmou o aplicativo, está pronto para atualizar a home page da seguinte maneira.

2. Crie um objeto de aplicativo em branco para armazenar as alterações que você deseja fazer. Essa variável contém os valores que você deseja atualizar. Nada é criado nesta etapa.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. Defina a URL da home page como o valor desejado. O valor deve ser um caminho de subdomínio do aplicativo publicado. Por exemplo, se você alterar a URL da página inicial de *https://sharepoint-iddemo.msappproxy.net/* para *https://sharepoint-iddemo.msappproxy.net/hybrid/*, os usuários do aplicativo serão levados diretamente para a página inicial personalizada.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Faça a atualização usando o GUID (ObjectID) que você copiou na "etapa 1: localizar o ID do objeto do aplicativo."

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. Para confirmar que a alteração foi bem-sucedida, reinicie o aplicativo.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Todas as alterações que você fizer no aplicativo poderão redefinir a URL da home page. Se a URL da página inicial for redefinida, repita a etapa 2.

## <a name="next-steps"></a>Próximas etapas

- [Habilitar acesso remoto ao SharePoint com o Proxy de Aplicativo Azure AD](application-proxy-enable-remote-access-sharepoint.md)
- [Habilitar o Proxy de Aplicativo no portal do Azure](active-directory-application-proxy-enable.md)
