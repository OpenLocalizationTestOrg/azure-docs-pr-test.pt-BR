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
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a>Usar o aplicativo de serviços de nuvem toodebug Emulator Express em VS 2017
Este artigo explica como aplicativos de serviços de nuvem emulador Express do toodebug do toouse em 2017 VS.

## <a name="background-context"></a>Contexto
O Emulator Express é usado por padrão para depuração de funções da Web e de Trabalho dos Serviços de Nuvem no Visual Studio. Essa configuração estiver especificada na página de propriedades de projeto de serviços de nuvem hello.

![Abrir propriedades do projeto][0]

![O Emulator Express está selecionado como padrão][1]

Olá [Visual C++ redistribuível] [ Visual C++ Redistributable] para Visual Studio é exigido pelo emulador express. Atualmente não está instalado com hello carga de trabalho do Azure. Após F5 gestos toodebug um aplicativo de serviços de nuvem, o Visual Studio seria solicitar tooinstall esse componente e continue com a depuração.

![Prompt para instalar o C++ Redistribuível][2]

Clique em Sim tooinstall C++ redistribuível.

![Instalar o C++ Redistribuível][3]

Pressione F5 novamente toolaunch sessões de depuração.

![Iniciar a depuração][4]

![Depuração bem-sucedida][5]

> Observação: a instalação do Visual C++ Redistribuível é um esforço único. Se você atualizou de uma versão anterior do SDK do Azure e se tiver instalado o Emulator Express, não encontrará esse problema.
> 
> 

## <a name="manual-workaround"></a>Solução alternativa manual
Você também pode instalar Olá [Visual C++ redistribuível] [ Visual C++ Redistributable] manualmente e o mesmo efeito será aplicado como como Visual Studio instalado em seu sistema.

[vcredist_x86.exe][vcredist_x86.exe]

[VCRedist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como usar o emulador de computação do Azure toodebug seus aplicativos de serviços de nuvem no Visual Studio: [toorun usando o Emulator Express e depurar um serviço de nuvem em um computador local][Using Emulator Express toorun and debug a cloud service on a local machine]

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
