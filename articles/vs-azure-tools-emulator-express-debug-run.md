---
title: "serviço em um computador local em nuvem aaaUsing Emulator Express toorun e depuração do Azure | Microsoft Docs"
description: "Usando o Emulator Express toorun e depurar um serviço de nuvem em um computador local"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Usando o Emulator Express toorun e depurar um Azure serviço em um computador local de nuvem
Ao usar o Emulator Express, você poderá testar e depurar um serviço de nuvem sem executar o Visual Studio como um administrador. Você pode definir seu toouse de configurações de projeto o Emulator Express ou Olá emulador completo, dependendo dos requisitos de saudação do seu serviço de nuvem. Para obter mais informações sobre o emulador completo hello, consulte [executar um aplicativo do Azure no emulador de computação do hello](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Uso do Emulator Express no Visual Studio
Quando você cria um projeto n SDK 2.3 ou posterior do Azure, o Emulator Express é usado automaticamente. Para projetos existentes que foram criados com uma versão anterior de saudação do SDK do Azure, use Olá seguindo as etapas tooselect Emulator Express:

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, clique com botão direito Olá e, no menu de contexto hello, selecione **propriedades**.

1. Nas páginas de propriedades de projetos hello, selecione Olá **Web** guia.

    ![Propriedades de um projeto de serviço de nuvem do Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. Em **Development Server Local**, escolha a opção **Usar o IIS Express**.

1. Em **Emulador**, selecione **Usar Emulator Express**.
   
1. saudação de toolaunch Emulator Express, execute Olá comando no prompt de comando a seguir: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Limitações do Emulator Express
Olá problemas a seguir é conhecido limitações do emulador Express: 

- O Emulator Express não é compatível com o Servidor Web do IIS.
- O serviço de nuvem pode conter várias funções, mas cada função é limitado tooone instância.
- Você não pode acessar números de porta abaixo de 1000. Se você usar um provedor de autenticação que normalmente usa uma porta abaixo de 1000, talvez seja necessário toochange esse número de porta de tooa valor acima de 1000.
- As limitações que se aplicam a toohello o emulador de computação do Azure também se aplicam a tooEmulator Express. Por exemplo, você não pode ter mais de 50 instâncias de função por implantação. Para obter mais informações sobre Olá emulador de computação do Azure, consulte [executar um aplicativo do Azure no emulador de computação do hello](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Próximas etapas
[Depuração de serviços de nuvem do Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
