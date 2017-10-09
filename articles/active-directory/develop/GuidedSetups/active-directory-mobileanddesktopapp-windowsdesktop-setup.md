---
title: "aaaAzure AD v2 Windows Desktop Introdução - instalação | Microsoft Docs"
description: "Como os aplicativos .NET da Área de Trabalho do Windows (XAML) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurar o seu projeto

Esta seção fornece instruções passo a passo sobre como toocreate um novo toodemonstrate de projeto como toointegrate .NET de área de trabalho do Windows (XAML) do aplicativo com *entrar com a Microsoft* para que ele possa consultar APIs da Web que requer um token.

aplicativo Hello criado por este guia apresenta resultados de toograph e mostrar um botão na tela e um botão de saída.

> Preferir toodownload este projeto do Visual Studio em vez disso? [Baixar um projeto](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) e ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes de executar.


### <a name="create-your-application"></a>Criar o aplicativo
1. No Visual Studio: `File` > `New` > `Project`<br/>
2. Em *Modelos*, selecione `Visual C#`
3. Selecione `WPF App` (ou *aplicativo WPF* dependendo da versão de saudação do Visual Studio)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Adicionar projeto de tooyour Olá biblioteca de autenticação da Microsoft (MSAL)
1. No Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Copiar/colar seguinte Olá na janela do Console do Gerenciador de pacotes de saudação:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> pacote de saudação acima instala Olá biblioteca de autenticação da Microsoft (MSAL). MSAL lida com a aquisição, cache e atualizar usuário toskens usado tooaccess APIs protegido pelo Active Directory do Azure v2.

## <a name="add-hello-code-tooinitialize-msal"></a>Adicionar código de saudação tooinitialize MSAL
Esta etapa ajudará você a criar uma interação de toohandle classe MSAL Library, como a manipulação de tokens.

1. Olá abrir `App.xaml.cs` de arquivos e adicionar referência de saudação para classe de toohello MSAL biblioteca:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Atualize a seguir Olá aplicativo classe toohello:
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a>Criar a interface do usuário do aplicativo
seção de saudação abaixo mostra como um aplicativo pode consultar um servidor de back-end protegido como o Microsoft Graph. Um arquivo MainWindow.xaml deve ser criado automaticamente como parte do modelo de projeto. Abra o arquivo esse arquivo e, em seguida, siga as instruções de saudação abaixo:

Substitua o seu aplicativo `<Grid>` com ser seguinte hello:

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
