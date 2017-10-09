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
## <a name="set-up-your-project"></a><span data-ttu-id="89af5-103">Configurar o seu projeto</span><span class="sxs-lookup"><span data-stu-id="89af5-103">Set up your project</span></span>

<span data-ttu-id="89af5-104">Esta seção fornece instruções passo a passo sobre como toocreate um novo toodemonstrate de projeto como toointegrate .NET de área de trabalho do Windows (XAML) do aplicativo com *entrar com a Microsoft* para que ele possa consultar APIs da Web que requer um token.</span><span class="sxs-lookup"><span data-stu-id="89af5-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="89af5-105">aplicativo Hello criado por este guia apresenta resultados de toograph e mostrar um botão na tela e um botão de saída.</span><span class="sxs-lookup"><span data-stu-id="89af5-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="89af5-106">Preferir toodownload este projeto do Visual Studio em vez disso?</span><span class="sxs-lookup"><span data-stu-id="89af5-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="89af5-107">[Baixar um projeto](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) e ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes de executar.</span><span class="sxs-lookup"><span data-stu-id="89af5-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="89af5-108">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="89af5-108">Create your application</span></span>
1. <span data-ttu-id="89af5-109">No Visual Studio: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="89af5-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="89af5-110">Em *Modelos*, selecione `Visual C#`</span><span class="sxs-lookup"><span data-stu-id="89af5-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="89af5-111">Selecione `WPF App` (ou *aplicativo WPF* dependendo da versão de saudação do Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="89af5-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="89af5-112">Adicionar projeto de tooyour Olá biblioteca de autenticação da Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="89af5-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="89af5-113">No Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="89af5-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="89af5-114">Copiar/colar seguinte Olá na janela do Console do Gerenciador de pacotes de saudação:</span><span class="sxs-lookup"><span data-stu-id="89af5-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="89af5-115">pacote de saudação acima instala Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="89af5-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="89af5-116">MSAL lida com a aquisição, cache e atualizar usuário toskens usado tooaccess APIs protegido pelo Active Directory do Azure v2.</span><span class="sxs-lookup"><span data-stu-id="89af5-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="89af5-117">Adicionar código de saudação tooinitialize MSAL</span><span class="sxs-lookup"><span data-stu-id="89af5-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="89af5-118">Esta etapa ajudará você a criar uma interação de toohandle classe MSAL Library, como a manipulação de tokens.</span><span class="sxs-lookup"><span data-stu-id="89af5-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="89af5-119">Olá abrir `App.xaml.cs` de arquivos e adicionar referência de saudação para classe de toohello MSAL biblioteca:</span><span class="sxs-lookup"><span data-stu-id="89af5-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="89af5-120">Atualize a seguir Olá aplicativo classe toohello:</span><span class="sxs-lookup"><span data-stu-id="89af5-120">Update hello App class toohello following:</span></span>
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

## <a name="create-your-applications-ui"></a><span data-ttu-id="89af5-121">Criar a interface do usuário do aplicativo</span><span class="sxs-lookup"><span data-stu-id="89af5-121">Create your application’s UI</span></span>
<span data-ttu-id="89af5-122">seção de saudação abaixo mostra como um aplicativo pode consultar um servidor de back-end protegido como o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="89af5-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="89af5-123">Um arquivo MainWindow.xaml deve ser criado automaticamente como parte do modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="89af5-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="89af5-124">Abra o arquivo esse arquivo e, em seguida, siga as instruções de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="89af5-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="89af5-125">Substitua o seu aplicativo `<Grid>` com ser seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="89af5-125">Replace your application’s `<Grid>` with be hello following:</span></span>

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
