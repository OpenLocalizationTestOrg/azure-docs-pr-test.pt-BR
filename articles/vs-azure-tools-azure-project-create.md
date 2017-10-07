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
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="53b2d-103">Criando um projeto de serviço de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53b2d-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="53b2d-104">Olá ferramentas do Azure para Visual Studio fornece um modelo de projeto que permite que você crie um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="53b2d-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="53b2d-105">Quando o projeto de saudação tiver sido criado, o Visual Studio permite tooconfigure, depurar e implantar Olá tooAzure de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="53b2d-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="53b2d-106">Etapas toocreate um projeto de serviço de nuvem do Azure no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53b2d-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="53b2d-107">Esta seção explica como criar um projeto de serviço de nuvem do Azure no Visual Studio com uma ou mais funções web.</span><span class="sxs-lookup"><span data-stu-id="53b2d-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="53b2d-108">Inicie o Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="53b2d-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="53b2d-109">No menu principal do hello, selecione **arquivo** > **novo** > **projeto**.</span><span class="sxs-lookup"><span data-stu-id="53b2d-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="53b2d-110">Selecione **nuvem** de saudação Visual c# ou Visual Basic nós modelo de projeto e selecione **serviço de nuvem do Azure** na lista de saudação de modelos.</span><span class="sxs-lookup"><span data-stu-id="53b2d-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![Novo serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="53b2d-112">Especifica qual versão de saudação que deseja toouse toodevelop o projeto do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="53b2d-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="53b2d-113">Insira um nome e local para seu projeto e um nome para a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="53b2d-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="53b2d-114">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="53b2d-114">Select **OK**.</span></span>

1. <span data-ttu-id="53b2d-115">Em Olá **novo serviço de nuvem do Microsoft Azure** caixa de diálogo, as funções hello selecione que você deseja tooadd e escolha Olá tooadd de botão de seta para a direita-los tooyour solução.</span><span class="sxs-lookup"><span data-stu-id="53b2d-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![Selecionar novas funções do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="53b2d-117">toorename uma função que você adicionou, passe o mouse na função hello em hello **novo serviço de nuvem do Microsoft Azure** caixa de diálogo e, no menu de contexto hello, selecione **Renomear**.</span><span class="sxs-lookup"><span data-stu-id="53b2d-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="53b2d-118">Você também pode renomear uma função em sua solução (em Olá **Solution Explorer**) depois que ele foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="53b2d-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Renomear uma função do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="53b2d-120">projeto do Azure do Visual Studio Olá tem projetos de função toohello associações na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="53b2d-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="53b2d-121">projeto Olá também inclui Olá *arquivo de definição de serviço* e *arquivo de configuração do serviço*:</span><span class="sxs-lookup"><span data-stu-id="53b2d-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="53b2d-122">**Arquivo de definição de serviço** -define as configurações de tempo de execução de saudação para seu aplicativo, incluindo as funções que são necessárias, os pontos de extremidade e tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="53b2d-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="53b2d-123">**Arquivo de configuração de serviço** -configura quantas instâncias de uma função são executadas e Olá valores hello configurações definidas para uma função.</span><span class="sxs-lookup"><span data-stu-id="53b2d-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="53b2d-124">Para obter mais informações sobre esses arquivos, consulte [configurar funções de saudação para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="53b2d-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="53b2d-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53b2d-125">Next steps</span></span>
- [<span data-ttu-id="53b2d-126">Gerenciando funções em projetos de serviço de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53b2d-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
