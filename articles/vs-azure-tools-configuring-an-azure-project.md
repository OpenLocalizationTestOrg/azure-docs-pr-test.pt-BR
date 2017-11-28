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
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="86cb7-103">Configurar um projeto de serviço de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86cb7-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="86cb7-104">Você pode configurar um projeto de serviço de nuvem do Azure, dependendo dos requisitos para o projeto.</span><span class="sxs-lookup"><span data-stu-id="86cb7-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="86cb7-105">Você pode definir propriedades de projeto Olá para Olá categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="86cb7-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="86cb7-106">**Publicar um tooAzure de serviço de nuvem** -você pode definir um toomake propriedade-se de que um tooAzure de serviço implantado de nuvem existente não é excluído acidentalmente.</span><span class="sxs-lookup"><span data-stu-id="86cb7-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="86cb7-107">**Executar ou depurar um serviço de nuvem no computador local Olá** -você pode selecionar um toouse de configuração de serviço e indique se deseja que o emulador de armazenamento do Azure Olá toostart.</span><span class="sxs-lookup"><span data-stu-id="86cb7-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="86cb7-108">**Validar um pacote de serviço de nuvem quando ela é criada** -você pode decidir tootreat todos os avisos como erros, para que você possa garantir que esse pacote de serviço de nuvem Olá implanta sem problemas.</span><span class="sxs-lookup"><span data-stu-id="86cb7-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="86cb7-109">Etapas tooconfigure um projeto de serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="86cb7-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="86cb7-110">Abra ou crie um projeto de serviço de nuvem do Azure no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86cb7-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="86cb7-111">Em **Solution Explorer**, clique com botão direito Olá e, no menu de contexto hello, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="86cb7-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="86cb7-112">Na página de propriedades do projeto hello, selecione Olá **desenvolvimento** guia.</span><span class="sxs-lookup"><span data-stu-id="86cb7-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![Menu Propriedades do projeto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="86cb7-114">Definir **perguntar antes de excluir uma implantação existente** muito**True**.</span><span class="sxs-lookup"><span data-stu-id="86cb7-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="86cb7-115">Essa configuração ajuda a tooensure não excluir acidentalmente uma implantação existente no Azure</span><span class="sxs-lookup"><span data-stu-id="86cb7-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="86cb7-116">Selecione Olá desejado **configuração do serviço** tooindicate qual configuração de serviço você deseja toouse quando você executar ou depurar seu serviço de nuvem localmente.</span><span class="sxs-lookup"><span data-stu-id="86cb7-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="86cb7-117">Para obter mais informações sobre como toomodify uma configuração de serviço para uma função, consulte [como tooconfigure Olá funções para um Azure de nuvem do serviço com o Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="86cb7-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="86cb7-118">Definir **emulador de armazenamento do Azure iniciar** muito**True** toostart emulador de armazenamento do Azure hello quando você executar ou depurar seu serviço de nuvem localmente.</span><span class="sxs-lookup"><span data-stu-id="86cb7-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="86cb7-119">Definir **tratar avisos como erros** muito**True** toomake-se de que não é possível publicar se houver erros de validação de pacote.</span><span class="sxs-lookup"><span data-stu-id="86cb7-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="86cb7-120">Definir **usar portas de projeto web** muito**True** toomake-se de que sua função web usa Olá mesmo cada porta sempre que ele é iniciado localmente no IIS Express.</span><span class="sxs-lookup"><span data-stu-id="86cb7-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="86cb7-121">Na barra de ferramentas do Visual Studio hello, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="86cb7-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86cb7-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86cb7-122">Next steps</span></span>
- [<span data-ttu-id="86cb7-123">Configurando um projeto do Azure usando várias configurações de serviço</span><span class="sxs-lookup"><span data-stu-id="86cb7-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

