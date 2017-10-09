---
title: "aaaSetup emulador express toodebug aplicativos de serviços de nuvem no Visual Studio | Microsoft Docs"
description: "Explica como tooinstall Olá C++ tooenable redistribuível Emulator Express no Visual Studio"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="70084-103">Usar o aplicativo de serviços de nuvem toodebug Emulator Express em VS 2017</span><span class="sxs-lookup"><span data-stu-id="70084-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="70084-104">Este artigo explica como aplicativos de serviços de nuvem emulador Express do toodebug do toouse em 2017 VS.</span><span class="sxs-lookup"><span data-stu-id="70084-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="70084-105">Contexto</span><span class="sxs-lookup"><span data-stu-id="70084-105">Background context</span></span>
<span data-ttu-id="70084-106">O Emulator Express é usado por padrão para depuração de funções da Web e de Trabalho dos Serviços de Nuvem no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70084-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="70084-107">Essa configuração estiver especificada na página de propriedades de projeto de serviços de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="70084-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![Abrir propriedades do projeto][0]

![O Emulator Express está selecionado como padrão][1]

<span data-ttu-id="70084-110">Olá [Visual C++ redistribuível] [ Visual C++ Redistributable] para Visual Studio é exigido pelo emulador express.</span><span class="sxs-lookup"><span data-stu-id="70084-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="70084-111">Atualmente não está instalado com hello carga de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="70084-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="70084-112">Após F5 gestos toodebug um aplicativo de serviços de nuvem, o Visual Studio seria solicitar tooinstall esse componente e continue com a depuração.</span><span class="sxs-lookup"><span data-stu-id="70084-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![Prompt para instalar o C++ Redistribuível][2]

<span data-ttu-id="70084-114">Clique em Sim tooinstall C++ redistribuível.</span><span class="sxs-lookup"><span data-stu-id="70084-114">Click Yes tooinstall C++ Redistributable.</span></span>

![Instalar o C++ Redistribuível][3]

<span data-ttu-id="70084-116">Pressione F5 novamente toolaunch sessões de depuração.</span><span class="sxs-lookup"><span data-stu-id="70084-116">Press F5 again toolaunch debugging sessions.</span></span>

![Iniciar a depuração][4]

![Depuração bem-sucedida][5]

> <span data-ttu-id="70084-119">Observação: a instalação do Visual C++ Redistribuível é um esforço único.</span><span class="sxs-lookup"><span data-stu-id="70084-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="70084-120">Se você atualizou de uma versão anterior do SDK do Azure e se tiver instalado o Emulator Express, não encontrará esse problema.</span><span class="sxs-lookup"><span data-stu-id="70084-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="70084-121">Solução alternativa manual</span><span class="sxs-lookup"><span data-stu-id="70084-121">Manual workaround</span></span>
<span data-ttu-id="70084-122">Você também pode instalar Olá [Visual C++ redistribuível] [ Visual C++ Redistributable] manualmente e o mesmo efeito será aplicado como como Visual Studio instalado em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="70084-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="70084-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="70084-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="70084-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="70084-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="70084-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70084-125">Next Steps</span></span>
<span data-ttu-id="70084-126">Saiba mais sobre como usar o emulador de computação do Azure toodebug seus aplicativos de serviços de nuvem no Visual Studio: [toorun usando o Emulator Express e depurar um serviço de nuvem em um computador local][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="70084-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
