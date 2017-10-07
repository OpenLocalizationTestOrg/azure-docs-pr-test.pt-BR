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
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="dd072-103">Usando o Emulator Express toorun e depurar um Azure serviço em um computador local de nuvem</span><span class="sxs-lookup"><span data-stu-id="dd072-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="dd072-104">Ao usar o Emulator Express, você poderá testar e depurar um serviço de nuvem sem executar o Visual Studio como um administrador.</span><span class="sxs-lookup"><span data-stu-id="dd072-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="dd072-105">Você pode definir seu toouse de configurações de projeto o Emulator Express ou Olá emulador completo, dependendo dos requisitos de saudação do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="dd072-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="dd072-106">Para obter mais informações sobre o emulador completo hello, consulte [executar um aplicativo do Azure no emulador de computação do hello](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="dd072-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="dd072-107">Uso do Emulator Express no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd072-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="dd072-108">Quando você cria um projeto n SDK 2.3 ou posterior do Azure, o Emulator Express é usado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dd072-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="dd072-109">Para projetos existentes que foram criados com uma versão anterior de saudação do SDK do Azure, use Olá seguindo as etapas tooselect Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="dd072-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="dd072-110">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd072-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="dd072-111">Em **Solution Explorer**, clique com botão direito Olá e, no menu de contexto hello, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="dd072-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="dd072-112">Nas páginas de propriedades de projetos hello, selecione Olá **Web** guia.</span><span class="sxs-lookup"><span data-stu-id="dd072-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Propriedades de um projeto de serviço de nuvem do Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="dd072-114">Em **Development Server Local**, escolha a opção **Usar o IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="dd072-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="dd072-115">Em **Emulador**, selecione **Usar Emulator Express**.</span><span class="sxs-lookup"><span data-stu-id="dd072-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="dd072-116">saudação de toolaunch Emulator Express, execute Olá comando no prompt de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd072-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="dd072-117">Limitações do Emulator Express</span><span class="sxs-lookup"><span data-stu-id="dd072-117">Emulator Express limitations</span></span>
<span data-ttu-id="dd072-118">Olá problemas a seguir é conhecido limitações do emulador Express:</span><span class="sxs-lookup"><span data-stu-id="dd072-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="dd072-119">O Emulator Express não é compatível com o Servidor Web do IIS.</span><span class="sxs-lookup"><span data-stu-id="dd072-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="dd072-120">O serviço de nuvem pode conter várias funções, mas cada função é limitado tooone instância.</span><span class="sxs-lookup"><span data-stu-id="dd072-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="dd072-121">Você não pode acessar números de porta abaixo de 1000.</span><span class="sxs-lookup"><span data-stu-id="dd072-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="dd072-122">Se você usar um provedor de autenticação que normalmente usa uma porta abaixo de 1000, talvez seja necessário toochange esse número de porta de tooa valor acima de 1000.</span><span class="sxs-lookup"><span data-stu-id="dd072-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="dd072-123">As limitações que se aplicam a toohello o emulador de computação do Azure também se aplicam a tooEmulator Express.</span><span class="sxs-lookup"><span data-stu-id="dd072-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="dd072-124">Por exemplo, você não pode ter mais de 50 instâncias de função por implantação.</span><span class="sxs-lookup"><span data-stu-id="dd072-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="dd072-125">Para obter mais informações sobre Olá emulador de computação do Azure, consulte [executar um aplicativo do Azure no emulador de computação do hello](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="dd072-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd072-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd072-126">Next steps</span></span>
[<span data-ttu-id="dd072-127">Depuração de serviços de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="dd072-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
