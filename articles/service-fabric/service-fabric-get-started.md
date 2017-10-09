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
# <a name="prepare-your-development-environment"></a><span data-ttu-id="1602f-104">Preparar seu ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="1602f-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1602f-105">Windows</span><span class="sxs-lookup"><span data-stu-id="1602f-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="1602f-106">Linux</span><span class="sxs-lookup"><span data-stu-id="1602f-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="1602f-107">OSX</span><span class="sxs-lookup"><span data-stu-id="1602f-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="1602f-108">toobuild e executar [aplicativos do Azure Service Fabric] [ 1] no computador de desenvolvimento, instalar o tempo de execução hello, SDK e as ferramentas.</span><span class="sxs-lookup"><span data-stu-id="1602f-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="1602f-109">Você também precisa tooenable a execução de scripts do Windows PowerShell Olá incluídas no SDK do hello.</span><span class="sxs-lookup"><span data-stu-id="1602f-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1602f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1602f-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="1602f-111">Versões de sistema operacional com suporte</span><span class="sxs-lookup"><span data-stu-id="1602f-111">Supported operating system versions</span></span>
<span data-ttu-id="1602f-112">Olá versões de sistemas operacionais a seguir têm suporte para desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="1602f-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="1602f-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="1602f-113">Windows 7</span></span>
* <span data-ttu-id="1602f-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="1602f-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="1602f-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1602f-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="1602f-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1602f-116">Windows Server 2016</span></span>
* <span data-ttu-id="1602f-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="1602f-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="1602f-118">O Windows 7 inclui, por padrão, apenas o Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="1602f-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="1602f-119">Cmdlets de PowerShell do Service Fabric exigem o PowerShell 3.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="1602f-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="1602f-120">Você pode [baixar o Windows PowerShell 5.0] [ powershell5-download] de saudação Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="1602f-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="1602f-121">Instalar ferramentas e Olá SDK</span><span class="sxs-lookup"><span data-stu-id="1602f-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="1602f-122">toouse 2017 do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1602f-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="1602f-123">Ferramentas do Service Fabric fazem parte do hello Azure desenvolvimento e gerenciamento de carga de trabalho no Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="1602f-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="1602f-124">Habilite essa carga de trabalho como parte da instalação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1602f-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="1602f-125">Além disso, você precisa tooinstall Olá Microsoft Azure SDK do Service Fabric, usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="1602f-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="1602f-126">[Instalar Olá SDK do Microsoft Azure Service Fabric][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="1602f-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="1602f-127">toouse Visual Studio 2015 (requer o Visual Studio 2015 atualização 2 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="1602f-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="1602f-128">Para Visual Studio 2015, ferramentas de malha do serviço são instaladas junto com o SDK, usando o Web Platform Installer de saudação do hello:</span><span class="sxs-lookup"><span data-stu-id="1602f-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="1602f-129">[Instalar ferramentas e Olá SDK do Microsoft Azure Service Fabric][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="1602f-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="1602f-130">Somente instalação do SDK</span><span class="sxs-lookup"><span data-stu-id="1602f-130">SDK installation only</span></span>
<span data-ttu-id="1602f-131">Se você precisar somente Olá SDK, você pode instalar este pacote:</span><span class="sxs-lookup"><span data-stu-id="1602f-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="1602f-132">[Instalar Olá SDK do Microsoft Azure Service Fabric][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="1602f-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="1602f-133">as versões atuais de saudação são:</span><span class="sxs-lookup"><span data-stu-id="1602f-133">hello current versions are:</span></span>
* <span data-ttu-id="1602f-134">SDK do Service Fabric 2.7.198</span><span class="sxs-lookup"><span data-stu-id="1602f-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="1602f-135">Execução do Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="1602f-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="1602f-136">Ferramentas do Service Fabric para Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="1602f-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="1602f-137">O Visual Studio 2017 Atualização 2 inclui as Ferramentas do Service Fabric para Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="1602f-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="1602f-138">O Visual Studio 2017 Atualização 3 Versão Prévia 7 (15.3.0 Versão Prévia 7.0) inclui as Ferramentas do Service Fabric para Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="1602f-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="1602f-139">Para obter uma lista das versões com suporte, consulte [suporte ao Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="1602f-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="1602f-140">Habilitar a execução de script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="1602f-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="1602f-141">A Malha do Serviço usa scripts do Windows PowerShell para criar um cluster de desenvolvimento local e implantar aplicativos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1602f-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="1602f-142">Por padrão, o Windows bloqueia a execução desses scripts.</span><span class="sxs-lookup"><span data-stu-id="1602f-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="1602f-143">tooenable-los, você deve modificar a política de execução do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1602f-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="1602f-144">Abra o PowerShell como administrador e digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1602f-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="1602f-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1602f-145">Next steps</span></span>
<span data-ttu-id="1602f-146">Agora que você terminou de configurar seu ambiente de desenvolvimento, comece a compilar e executar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1602f-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="1602f-147">Criar seu primeiro aplicativo do Service Fabric no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1602f-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="1602f-148">Saiba como toodeploy e gerenciar aplicativos no seu cluster local</span><span class="sxs-lookup"><span data-stu-id="1602f-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="1602f-149">Saiba mais sobre modelos de programação de saudação: serviços confiáveis e atores confiável</span><span class="sxs-lookup"><span data-stu-id="1602f-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="1602f-150">Check-out de saudação do Service Fabric exemplos de código no GitHub</span><span class="sxs-lookup"><span data-stu-id="1602f-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="1602f-151">Visualizar o cluster usando o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="1602f-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="1602f-152">Siga Olá aprendizado caminho tooget uma plataforma de toohello introdução abrangente do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1602f-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="1602f-153">Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="1602f-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Página da campanha do Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
