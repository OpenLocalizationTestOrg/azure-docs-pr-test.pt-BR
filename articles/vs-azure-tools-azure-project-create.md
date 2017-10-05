---
title: "Criando um projeto de serviço de nuvem do Azure com o Visual Studio | Microsoft Docs"
description: "Saiba como criar um projeto de serviço de nuvem do Azure com o Visual Studio"
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
ms.openlocfilehash: 1f6ded87b551f660853ea4eb0548f3d942e28fa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="01990-103">Criando um projeto de serviço de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01990-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="01990-104">As Ferramentas do Azure para Visual Studio fornecem um modelo de projeto que permite criar um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="01990-104">The Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="01990-105">Após a criação do projeto, o Visual Studio permite configurar, depurar e implantar o serviço de nuvem no Azure.</span><span class="sxs-lookup"><span data-stu-id="01990-105">Once the project has been created, Visual Studio enables you to configure, debug, and deploy the cloud service to Azure.</span></span>

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="01990-106">Etapas para criar um projeto de serviço de nuvem do Azure no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01990-106">Steps to create an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="01990-107">Esta seção explica como criar um projeto de serviço de nuvem do Azure no Visual Studio com uma ou mais funções web.</span><span class="sxs-lookup"><span data-stu-id="01990-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="01990-108">Inicie o Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="01990-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="01990-109">No menu principal, selecione **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="01990-109">On the main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="01990-110">Selecione **Nuvem** nos nós do modelo de projeto do Visual C# ou Visual Basic e selecione **Serviço de Nuvem do Azure** na lista de modelos.</span><span class="sxs-lookup"><span data-stu-id="01990-110">Select **Cloud** from the Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from the list of templates.</span></span>

    ![Novo serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="01990-112">Especifica qual versão do .NET Framework você deseja usar para desenvolver o projeto.</span><span class="sxs-lookup"><span data-stu-id="01990-112">Specify which version of the .NET Framework you want to use to develop your project.</span></span>

1. <span data-ttu-id="01990-113">Insira um nome e local para seu projeto e um nome para a solução.</span><span class="sxs-lookup"><span data-stu-id="01990-113">Enter a name and location for your project and a name for the solution.</span></span> 

1. <span data-ttu-id="01990-114">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="01990-114">Select **OK**.</span></span>

1. <span data-ttu-id="01990-115">Na caixa de diálogo **Novo Serviço de Nuvem do Microsoft Azure**, selecione as funções que você deseja adicionar e escolha o botão de seta para a direita para adicioná-las à solução.</span><span class="sxs-lookup"><span data-stu-id="01990-115">In the **New Microsoft Azure Cloud Service** dialog, select the roles that you want to add, and choose the right arrow button to add them to your solution.</span></span>

    ![Selecionar novas funções do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="01990-117">Para renomear uma função adicionada, focalize a função na caixa de diálogo **Novo Serviço de Nuvem do Microsoft Azure** e, no menu de contexto, selecione **Renomear**.</span><span class="sxs-lookup"><span data-stu-id="01990-117">To rename a role that you've added, hover on the role in the **New Microsoft Azure Cloud Service** dialog, and, from the context menu, select **Rename**.</span></span> <span data-ttu-id="01990-118">Você também pode renomear uma função na solução (no **Gerenciador de Soluções**) depois de adicioná-la.</span><span class="sxs-lookup"><span data-stu-id="01990-118">You can also rename a role within your solution (in the **Solution Explorer**) after it has been added.</span></span>

    ![Renomear uma função do serviço de nuvem do Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="01990-120">O projeto do Azure no Visual Studio tem associações aos projetos de função na solução.</span><span class="sxs-lookup"><span data-stu-id="01990-120">The Visual Studio Azure project has associations to the role projects in the solution.</span></span> <span data-ttu-id="01990-121">Ele também inclui o *arquivo de definição de serviço* e o *arquivo de configuração de serviço*:</span><span class="sxs-lookup"><span data-stu-id="01990-121">The project also includes the *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="01990-122">**Arquivo de definição de serviço** – define as configurações de tempo de execução do aplicativo, incluindo quais funções são necessárias, pontos de extremidade e tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01990-122">**Service definition file** - Defines the runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="01990-123">**Arquivo de configuração de serviço** – configura quantas instâncias de uma função são executadas e os valores das configurações definidas para uma função.</span><span class="sxs-lookup"><span data-stu-id="01990-123">**Service configuration file** - Configures how many instances of a role are run and the values of the settings defined for a role.</span></span> 

<span data-ttu-id="01990-124">Para obter mais informações sobre esses arquivos, consulte [Configurar as funções para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="01990-124">For more information about these files, see [Configure the Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01990-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01990-125">Next steps</span></span>
- [<span data-ttu-id="01990-126">Gerenciando funções em projetos de serviço de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01990-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
