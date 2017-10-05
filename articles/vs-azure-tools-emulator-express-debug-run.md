---
title: "Uso do Emulator Express para executar e depurar um serviço de nuvem do Azure em um computador local | Microsoft Docs"
description: "Usando o Emulator Express para executar e depurar um serviço de nuvem em um computador local"
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
ms.openlocfilehash: d7d87045569fdc473333deae05f95d1df343b68c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="c16bd-103">Uso do Emulator Express para executar e depurar um serviço de nuvem do Azure em um computador local</span><span class="sxs-lookup"><span data-stu-id="c16bd-103">Using Emulator Express to run and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="c16bd-104">Ao usar o Emulator Express, você poderá testar e depurar um serviço de nuvem sem executar o Visual Studio como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c16bd-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="c16bd-105">É possível definir as configurações do projeto para usar o Emulator Express ou o emulador completo, dependendo dos requisitos do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c16bd-105">You can set your project settings to use either Emulator Express or the full emulator, depending on the requirements of your cloud service.</span></span> <span data-ttu-id="c16bd-106">Para saber mais sobre o emulador completo, consulte [Executar um aplicativo Azure no emulador de computação](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="c16bd-106">For more information about the full emulator, see [Run an Azure Application in the Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="c16bd-107">Uso do Emulator Express no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c16bd-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="c16bd-108">Quando você cria um projeto n SDK 2.3 ou posterior do Azure, o Emulator Express é usado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c16bd-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="c16bd-109">No caso de projetos existentes que foram criados com uma versão anterior do SDK do Azure, use as seguintes etapas para selecionar o Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="c16bd-109">For existing projects that were created with an earlier version of the Azure SDK, use the following steps to select Emulator Express:</span></span>

1. <span data-ttu-id="c16bd-110">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c16bd-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="c16bd-111">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e, no menu de contexto, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="c16bd-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>

1. <span data-ttu-id="c16bd-112">Nas páginas de propriedades dos projetos, selecione a guia **Web**.</span><span class="sxs-lookup"><span data-stu-id="c16bd-112">In the projects properties pages, select the **Web** tab.</span></span>

    ![Propriedades de um projeto de serviço de nuvem do Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="c16bd-114">Em **Development Server Local**, escolha a opção **Usar o IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="c16bd-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="c16bd-115">Em **Emulador**, selecione **Usar Emulator Express**.</span><span class="sxs-lookup"><span data-stu-id="c16bd-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="c16bd-116">Para iniciar o Emulator Express, execute o seguinte comando em um prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="c16bd-116">To launch the Emulator Express, run the following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="c16bd-117">Limitações do Emulator Express</span><span class="sxs-lookup"><span data-stu-id="c16bd-117">Emulator Express limitations</span></span>
<span data-ttu-id="c16bd-118">Os seguintes problemas são limitações conhecidas do Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="c16bd-118">The following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="c16bd-119">O Emulator Express não é compatível com o Servidor Web do IIS.</span><span class="sxs-lookup"><span data-stu-id="c16bd-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="c16bd-120">O serviço de nuvem pode conter várias funções, mas cada função é limitada a uma instância.</span><span class="sxs-lookup"><span data-stu-id="c16bd-120">Your cloud service can contain multiple roles, but each role is limited to one instance.</span></span>
- <span data-ttu-id="c16bd-121">Você não pode acessar números de porta abaixo de 1000.</span><span class="sxs-lookup"><span data-stu-id="c16bd-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="c16bd-122">Se você usar um provedor de autenticação que normalmente usa uma porta abaixo de 1000, talvez seja necessário alterar esse valor para um número de porta acima de 1000.</span><span class="sxs-lookup"><span data-stu-id="c16bd-122">If you use an authentication provider that normally uses a port below 1000, you might need to change this value to a port number that's above 1000.</span></span>
- <span data-ttu-id="c16bd-123">As limitações que se aplicam ao Emulador de Computação do Azure também se aplicam ao Emulator Express.</span><span class="sxs-lookup"><span data-stu-id="c16bd-123">Any limitations that apply to the Azure Compute Emulator also apply to Emulator Express.</span></span> <span data-ttu-id="c16bd-124">Por exemplo, você não pode ter mais de 50 instâncias de função por implantação.</span><span class="sxs-lookup"><span data-stu-id="c16bd-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="c16bd-125">Para saber mais sobre o Emulador de Computação do Azure, confira [Executar um aplicativo do Azure no Emulador de Computação](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="c16bd-125">For more information about the Azure Compute Emulator, see [Run an Azure Application in the Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c16bd-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c16bd-126">Next steps</span></span>
[<span data-ttu-id="c16bd-127">Depuração de serviços de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="c16bd-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
