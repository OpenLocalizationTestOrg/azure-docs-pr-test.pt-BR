---
title: "implantação de aaaAutomate do seu aplicativo do Azure com as ferramentas de linha de comando | Microsoft Docs"
description: "Descobrir informações sobre como você pode implantar o aplicativo do Azure de saudação de linha de comando"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Automatizar a implantação do seu aplicativo do Azure com as ferramentas de linha de comando
Você pode automatizar a implantação dos seus aplicativos do Azure com as ferramentas de linha de comando. Este artigo lista as ferramentas disponíveis e links úteis de saudação que mostram como toouse-los em seu fluxo de trabalho de implantação. 

## <a name="msbuild"></a>Automatizar a implantação com o MSBuild
Se você usar o hello [IDE do Visual Studio](#vs) para o desenvolvimento, você pode usar [MSBuild](http://msbuildbook.com/) tooautomate qualquer coisa que você pode fazer em seu IDE. Você pode configurar o MSBuild toouse ou [implantação da Web](#webdeploy) ou [FTP/FTPS](#ftp) toocopy arquivos. A Implantação da Web também pode automatizar várias outras tarefas relacionadas à implantação tarefas, como a implantação de bancos de dados.

Para obter mais informações sobre a implantação de linha de comando usando MSBuild, consulte Olá recursos a seguir:

* [Implantação da Web do ASP.NET usando o Visual Studio: implantação de linha de comando](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). Décimo em uma série de tutoriais sobre tooAzure de implantação usando o Visual Studio. Mostra como toouse Olá toodeploy de linha de comando após a configuração de perfis de publicação no Visual Studio.
* [Olá interna Microsoft Build Engine: usando MSBuild e o Team Foundation Build](http://msbuildbook.com/). Catálogo de cópia impressa que inclui capítulos sobre como toouse MSBuild para implantação.

## <a name="powershell"></a>Automatizar a implantação com o Windows PowerShell
Você pode executar funções de implantação do MSBuild ou de FTP a partir do [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Se você fizer isso, você também pode usar um conjunto de cmdlets do Windows PowerShell que tornam toocall fácil de API para gerenciamento Olá REST do Azure.

Para obter mais informações, consulte Olá recursos a seguir:

* [Implantar um repositório GitHub do web app vinculado tooa](app-service-web-arm-from-github-provision.md)
* [Provisionar um aplicativo Web com um banco de dados SQL](app-service-web-arm-with-sql-database-provision.md)
* [Provisionar e implantar microsserviços previsíveis no Azure](app-service-deploy-complex-application-predictably.md)
* [Compilando aplicativos de nuvem do mundo real com o Azure - automatizar tudo](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything). Capítulo de livro eletrônico que explica como o aplicativo de exemplo hello mostrado no livro eletrônico Olá usa toocreate de scripts do Windows PowerShell do Azure ambiente de teste e implante tooit. Consulte Olá [recursos](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) seção para links tooadditional documentação do PowerShell do Azure.
* [Usando Scripts do Windows PowerShell tooPublish tooDev e ambientes de teste](../vs-azure-tools-publishing-using-powershell-scripts.md). Como os scripts de toouse de implantação do Windows PowerShell que o Visual Studio gera.

## <a name="api"></a>Automatizar a implantação com a API de gerenciamento do .NET
Você pode escrever código c# tooperform funções de MSBuild ou FTP para implantação. Se você fizer isso, você pode acessar as funções de gerenciamento de site Olá gerenciamento do Azure API REST tooperform.

Para obter mais informações, consulte Olá recursos a seguir:

* [Automatizando tudo com bibliotecas de gerenciamento do Azure hello e .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Introdução toohello .NET API e links toomore documentação gerenciamento.

## <a name="cli"></a>Implantar da CLI (Interface de Linha de Comando) do Azure
Você pode usar a linha de comando Olá no Windows, Mac ou Linux toodeploy de máquinas usando FTP. Se você fizer isso, você também pode acessar a API de gerenciamento do Azure REST hello usando Olá CLI do Azure.

Para obter mais informações, consulte Olá recursos a seguir:

* <seg>
  [Ferramentas de linha de comando do Azure](https://azure.microsoft.com/downloads/).</seg> Página de portal em Azure.com que fornece informações da ferramenta de linha de comando.

## <a name="webdeploy"></a>Implantar por meio da linha de comando de Implantação da Web
[Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy) é o software da Microsoft para implantação tooIIS que fornece não só inteligente recursos de sincronização, mas também pode executar ou coordenar muitas outras relacionadas à implantação tarefas que não podem ser automatizadas quando você usar o FTP. Por exemplo, a Implantação da Web pode implantar um novo banco de dados ou atualizações de banco de dados junto com seu aplicativo Web. A implantação da Web também pode minimizar Olá tempo necessário tooupdate um site existente, desde que ele inteligente pode copiar somente os arquivos alterados. Microsoft Visual Studio e o Team Foundation Server têm suporte para implantação interna da Web, mas você também pode usar a implantação da Web diretamente da implantação de tooautomate de linha de comando de saudação. Comandos de implantação da Web são muito poderosos mas Olá curva de aprendizado pode ser acentuada.

## <a name="more-resources"></a>Mais recursos
Outro automação de linha de toocommand de opção de implantação é o serviço de toouse um baseado em nuvem, como [Polvo implantar](http://en.wikipedia.org/wiki/Octopus_Deploy). Para obter mais informações, consulte [tooAzure de aplicativos ASP.NET implantar Sites da Web](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Para obter mais informações sobre ferramentas de linha de comando, consulte Olá recursos a seguir:

* [Aplicativos Web simples: implantação](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Blog de David Ebbo sobre uma ferramenta que ele escreveu toomake-toouse mais fácil implantação da Web.
* [Ferramenta de Implantação de Web](http://technet.microsoft.com/library/dd568996). Documentação oficial no site do Microsoft TechNet hello. Data mas ainda um toostart BOM.
* [Usando a Implantação da Web](http://www.iis.net/learn/publish/using-web-deploy). Documentação oficial no site do Microsoft IIS.NET hello. Também data mas toostart um bom lugar.
* [Implantação da Web do ASP.NET usando o Visual Studio: implantação de linha de comando](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild é Olá compilar mecanismo usado pelo Visual Studio, e também pode ser usado de saudação linha de comando toodeploy web aplicativos tooWeb aplicativos. Este tutorial faz parte de uma série que trata principalmente da implantação do Visual Studio.

