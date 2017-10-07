---
title: "aaaConfigure um projeto de serviço de nuvem do Azure com o Visual Studio | Microsoft Docs"
description: "Saiba como o projeto de serviço no Visual Studio, dependendo dos requisitos para o projeto de nuvem tooconfigure do Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Configurar um projeto de serviço de nuvem do Azure com o Visual Studio
Você pode configurar um projeto de serviço de nuvem do Azure, dependendo dos requisitos para o projeto. Você pode definir propriedades de projeto Olá para Olá categorias a seguir:

- **Publicar um tooAzure de serviço de nuvem** -você pode definir um toomake propriedade-se de que um tooAzure de serviço implantado de nuvem existente não é excluído acidentalmente.
- **Executar ou depurar um serviço de nuvem no computador local Olá** -você pode selecionar um toouse de configuração de serviço e indique se deseja que o emulador de armazenamento do Azure Olá toostart.
- **Validar um pacote de serviço de nuvem quando ela é criada** -você pode decidir tootreat todos os avisos como erros, para que você possa garantir que esse pacote de serviço de nuvem Olá implanta sem problemas. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>Etapas tooconfigure um projeto de serviço de nuvem do Azure
1. Abra ou crie um projeto de serviço de nuvem do Azure no Visual Studio

1. Em **Solution Explorer**, clique com botão direito Olá e, no menu de contexto hello, selecione **propriedades**.
   
1. Na página de propriedades do projeto hello, selecione Olá **desenvolvimento** guia.

    ![Menu Propriedades do projeto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Definir **perguntar antes de excluir uma implantação existente** muito**True**. Essa configuração ajuda a tooensure não excluir acidentalmente uma implantação existente no Azure

1. Selecione Olá desejado **configuração do serviço** tooindicate qual configuração de serviço você deseja toouse quando você executar ou depurar seu serviço de nuvem localmente. Para obter mais informações sobre como toomodify uma configuração de serviço para uma função, consulte [como tooconfigure Olá funções para um Azure de nuvem do serviço com o Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Definir **emulador de armazenamento do Azure iniciar** muito**True** toostart emulador de armazenamento do Azure hello quando você executar ou depurar seu serviço de nuvem localmente.

1. Definir **tratar avisos como erros** muito**True** toomake-se de que não é possível publicar se houver erros de validação de pacote.

1. Definir **usar portas de projeto web** muito**True** toomake-se de que sua função web usa Olá mesmo cada porta sempre que ele é iniciado localmente no IIS Express.

1. Na barra de ferramentas do Visual Studio hello, selecione **salvar**.

## <a name="next-steps"></a>Próximas etapas
- [Configurando um projeto do Azure usando várias configurações de serviço](vs-azure-tools-multiple-services-project-configurations.md)

