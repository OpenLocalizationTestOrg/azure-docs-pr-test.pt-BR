---
title: "Configurar um projeto de serviço de nuvem do Azure com o Visual Studio | Microsoft Docs"
description: "Saiba como configurar um projeto de serviço de nuvem do Azure no Visual Studio, dependendo dos requisitos para o projeto."
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
ms.openlocfilehash: 799715093bd1a8c8e77e6cdb7168670dc263dfa5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="16e1a-103">Configurar um projeto de serviço de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16e1a-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="16e1a-104">Você pode configurar um projeto de serviço de nuvem do Azure, dependendo dos requisitos para o projeto.</span><span class="sxs-lookup"><span data-stu-id="16e1a-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="16e1a-105">Você pode definir propriedades do projeto para as seguintes categorias:</span><span class="sxs-lookup"><span data-stu-id="16e1a-105">You can set properties for the project for the following categories:</span></span>

- <span data-ttu-id="16e1a-106">**Publicar um serviço de nuvem no Azure**: você pode definir uma propriedade para ter certeza de que um serviço de nuvem existente implantado no Azure não seja excluído acidentalmente.</span><span class="sxs-lookup"><span data-stu-id="16e1a-106">**Publish a cloud service to Azure** - You can set a property to make sure that an existing cloud service deployed to Azure is not accidentally deleted.</span></span>
- <span data-ttu-id="16e1a-107">**Executar ou depurar um serviço de nuvem no computador local**: você pode selecionar uma configuração de serviço para usar e indicar se deseja iniciar o emulador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="16e1a-107">**Run or debug a cloud service on the local computer** - You can select a service configuration to use and indicate whether you want to start the Azure storage emulator.</span></span>
- <span data-ttu-id="16e1a-108">**Validar um pacote de serviço de nuvem quando ele é criado**: você pode optar por tratar todos os avisos como erros para que seja possível garantir que o pacote de serviço de nuvem seja implantado sem problemas.</span><span class="sxs-lookup"><span data-stu-id="16e1a-108">**Validate a cloud service package when it is created** - You can decide to treat any warnings as errors so that you can ensure that the cloud service package deploys without any issues.</span></span> 

## <a name="steps-to-configure-an-azure-cloud-service-project"></a><span data-ttu-id="16e1a-109">Etapas para configurar um projeto de serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="16e1a-109">Steps to configure an Azure cloud service project</span></span>
1. <span data-ttu-id="16e1a-110">Abra ou crie um projeto de serviço de nuvem do Azure no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16e1a-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="16e1a-111">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e, no menu de contexto, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="16e1a-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="16e1a-112">Na página de propriedades do projeto, selecione a guia **Desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="16e1a-112">In the project's properties page, select the **Development** tab.</span></span>

    ![Menu Propriedades do projeto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="16e1a-114">Defina **Avisar antes de excluir uma implantação existente** como **Verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="16e1a-114">Set **Prompt before deleting an existing deployment** to **True**.</span></span> <span data-ttu-id="16e1a-115">Essa configuração ajuda a garantir que você não exclua acidentalmente uma implantação existente no Azure</span><span class="sxs-lookup"><span data-stu-id="16e1a-115">This setting helps to ensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="16e1a-116">Selecione a **Configuração de serviço** desejada para indicar qual configuração de serviço deseja usar quando executar ou depurar o serviço de nuvem localmente.</span><span class="sxs-lookup"><span data-stu-id="16e1a-116">Select the desired **Service configuration** to indicate which service configuration you want to use when you run or debug your cloud service locally.</span></span> <span data-ttu-id="16e1a-117">Para saber mais sobre como modificar uma configuração de serviço para uma função, confira [Configurar funções de serviço de nuvem do Azure com o Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="16e1a-117">For more information on how to modify a service configuration for a role, see [How to configure the roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="16e1a-118">Defina **Iniciar emulador de armazenamento do Azure** como **Verdadeiro** para iniciar o emulador de armazenamento do Azure ao executar ou depurar o serviço de nuvem localmente.</span><span class="sxs-lookup"><span data-stu-id="16e1a-118">Set **Start Azure storage emulator** to **True** to start the Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="16e1a-119">Defina **Tratar avisos como erros** como **Verdadeiro** para garantir que não seja possível publicar se houver erros de validação de pacote.</span><span class="sxs-lookup"><span data-stu-id="16e1a-119">Set **Treat warnings as errors** to **True** to make sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="16e1a-120">Defina **Usar portas de projeto Web** como **Verdadeiro** para garantir que sua função web use a mesma porta toda vez que ela iniciar localmente no IIS Express.</span><span class="sxs-lookup"><span data-stu-id="16e1a-120">Set **Use web project ports** to **True** to make sure that your web role uses the same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="16e1a-121">Na barra de ferramentas do Visual Studio, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="16e1a-121">From the Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16e1a-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16e1a-122">Next steps</span></span>
- [<span data-ttu-id="16e1a-123">Configurando um projeto do Azure usando várias configurações de serviço</span><span class="sxs-lookup"><span data-stu-id="16e1a-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

