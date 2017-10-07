---
title: "aaaCreating um projeto de serviço de nuvem do Azure com o Visual Studio | Microsoft Docs"
description: "Aprenda Agora toocreate um projeto de serviço de nuvem do Azure com o Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Criando um projeto de serviço de nuvem do Azure com o Visual Studio
Olá ferramentas do Azure para Visual Studio fornece um modelo de projeto que permite que você crie um serviço de nuvem do Azure. Quando o projeto de saudação tiver sido criado, o Visual Studio permite tooconfigure, depurar e implantar Olá tooAzure de serviço de nuvem.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>Etapas toocreate um projeto de serviço de nuvem do Azure no Visual Studio
Esta seção explica como criar um projeto de serviço de nuvem do Azure no Visual Studio com uma ou mais funções web.  

1. Inicie o Visual Studio como administrador.

1. No menu principal do hello, selecione **arquivo** > **novo** > **projeto**.

1. Selecione **nuvem** de saudação Visual c# ou Visual Basic nós modelo de projeto e selecione **serviço de nuvem do Azure** na lista de saudação de modelos.

    ![Novo serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Especifica qual versão de saudação que deseja toouse toodevelop o projeto do .NET Framework.

1. Insira um nome e local para seu projeto e um nome para a solução de saudação. 

1. Selecione **OK**.

1. Em Olá **novo serviço de nuvem do Microsoft Azure** caixa de diálogo, as funções hello selecione que você deseja tooadd e escolha Olá tooadd de botão de seta para a direita-los tooyour solução.

    ![Selecionar novas funções do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. toorename uma função que você adicionou, passe o mouse na função hello em hello **novo serviço de nuvem do Microsoft Azure** caixa de diálogo e, no menu de contexto hello, selecione **Renomear**. Você também pode renomear uma função em sua solução (em Olá **Solution Explorer**) depois que ele foi adicionado.

    ![Renomear uma função do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

projeto do Azure do Visual Studio Olá tem projetos de função toohello associações na solução de saudação. projeto Olá também inclui Olá *arquivo de definição de serviço* e *arquivo de configuração do serviço*:

- **Arquivo de definição de serviço** -define as configurações de tempo de execução de saudação para seu aplicativo, incluindo as funções que são necessárias, os pontos de extremidade e tamanho da máquina virtual. 
- **Arquivo de configuração de serviço** -configura quantas instâncias de uma função são executadas e Olá valores hello configurações definidas para uma função. 

Para obter mais informações sobre esses arquivos, consulte [configurar funções de saudação para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Próximas etapas
- [Gerenciando funções em projetos de serviço de nuvem do Azure com o Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
