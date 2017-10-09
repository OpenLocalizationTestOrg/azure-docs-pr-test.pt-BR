---
title: aaaSet um ambiente de desenvolvimento para microservices do Azure | Microsoft Docs
description: "Instalar o tempo de execução hello, SDK e as ferramentas e criar um cluster de desenvolvimento local. Depois de concluir esta instalação, você será aplicativos toobuild pronto."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>Preparar seu ambiente de desenvolvimento
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild e executar [aplicativos do Azure Service Fabric] [ 1] no computador de desenvolvimento, instalar o tempo de execução hello, SDK e as ferramentas. Você também precisa tooenable a execução de scripts do Windows PowerShell Olá incluídas no SDK do hello.

## <a name="prerequisites"></a>Pré-requisitos
### <a name="supported-operating-system-versions"></a>Versões de sistema operacional com suporte
Olá versões de sistemas operacionais a seguir têm suporte para desenvolvimento:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> O Windows 7 inclui, por padrão, apenas o Windows PowerShell 2.0. Cmdlets de PowerShell do Service Fabric exigem o PowerShell 3.0 ou superior. Você pode [baixar o Windows PowerShell 5.0] [ powershell5-download] de saudação Microsoft Download Center.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Instalar ferramentas e Olá SDK
### <a name="toouse-visual-studio-2017"></a>toouse 2017 do Visual Studio
Ferramentas do Service Fabric fazem parte do hello Azure desenvolvimento e gerenciamento de carga de trabalho no Visual Studio de 2017. Habilite essa carga de trabalho como parte da instalação do Visual Studio.
Além disso, você precisa tooinstall Olá Microsoft Azure SDK do Service Fabric, usando o Web Platform Installer.

* [Instalar Olá SDK do Microsoft Azure Service Fabric][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse Visual Studio 2015 (requer o Visual Studio 2015 atualização 2 ou posterior)
Para Visual Studio 2015, ferramentas de malha do serviço são instaladas junto com o SDK, usando o Web Platform Installer de saudação do hello:

* [Instalar ferramentas e Olá SDK do Microsoft Azure Service Fabric][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Somente instalação do SDK
Se você precisar somente Olá SDK, você pode instalar este pacote:
* [Instalar Olá SDK do Microsoft Azure Service Fabric][core-sdk]

as versões atuais de saudação são:
* SDK do Service Fabric 2.7.198
* Execução do Service Fabric 5.7.198
* Ferramentas do Service Fabric para Visual Studio 2015 1.7.50721
* O Visual Studio 2017 Atualização 2 inclui as Ferramentas do Service Fabric para Visual Studio 1.6.20170504
* O Visual Studio 2017 Atualização 3 Versão Prévia 7 (15.3.0 Versão Prévia 7.0) inclui as Ferramentas do Service Fabric para Visual Studio 1.7.20170721

Para obter uma lista das versões com suporte, consulte [suporte ao Service Fabric](service-fabric-support.md)

## <a name="enable-powershell-script-execution"></a>Habilitar a execução de script do PowerShell
A Malha do Serviço usa scripts do Windows PowerShell para criar um cluster de desenvolvimento local e implantar aplicativos do Visual Studio. Por padrão, o Windows bloqueia a execução desses scripts. tooenable-los, você deve modificar a política de execução do PowerShell. Abra o PowerShell como administrador e digite Olá comando a seguir:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Próximas etapas
Agora que você terminou de configurar seu ambiente de desenvolvimento, comece a compilar e executar aplicativos.

* [Criar seu primeiro aplicativo do Service Fabric no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Saiba como toodeploy e gerenciar aplicativos no seu cluster local](service-fabric-get-started-with-a-local-cluster.md)
* [Saiba mais sobre modelos de programação de saudação: serviços confiáveis e atores confiável](service-fabric-choose-framework.md)
* [Check-out de saudação do Service Fabric exemplos de código no GitHub](https://aka.ms/servicefabricsamples)
* [Visualizar o cluster usando o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
* [Siga Olá aprendizado caminho tooget uma plataforma de toohello introdução abrangente do Service Fabric](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Página da campanha do Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
