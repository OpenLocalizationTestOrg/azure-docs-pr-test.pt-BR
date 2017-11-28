---
title: falhas de artefato aaaDiagnose na VM do Azure DevTest Labs | Microsoft Docs
description: Saiba como falhas de artefato de tootroubleshoot em DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="6c388-103">Diagnosticar falhas de artefato laboratório Olá</span><span class="sxs-lookup"><span data-stu-id="6c388-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="6c388-104">Depois que você criou um artefato, você pode verificar toosee se ela teve êxito ou falhou.</span><span class="sxs-lookup"><span data-stu-id="6c388-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="6c388-105">Logs de artefato em DevTest Labs fornecem informações que você pode usar toodiagnose uma falha de artefato.</span><span class="sxs-lookup"><span data-stu-id="6c388-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="6c388-106">Há duas maneiras diferentes, você pode exibir informações de log de artefato Olá para uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="6c388-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="6c388-107">tooensure falhas são identificadas e explicadas, é importante que esse artefato Olá corretamente é estruturado corretamente.</span><span class="sxs-lookup"><span data-stu-id="6c388-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="6c388-108">Para obter informações sobre como toocorrectly construir um artefato, consulte [criar artefatos personalizados](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="6c388-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="6c388-109">E toosee um exemplo de um artefato corretamente estruturado, confira esta [tipos de parâmetro de teste](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefato.</span><span class="sxs-lookup"><span data-stu-id="6c388-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="6c388-110">Solucionar problemas de falhas de artefato usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6c388-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="6c388-111">falhas de toodiagnose portal do Azure Olá toouse durante a criação do artefato, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="6c388-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="6c388-112">Na lista de saudação de recursos, selecione seu laboratório.</span><span class="sxs-lookup"><span data-stu-id="6c388-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="6c388-113">Escolha Olá VM do Windows que inclui o artefato Olá deseja tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="6c388-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="6c388-114">No painel esquerdo, Olá em **geral**, escolha **artefatos**.</span><span class="sxs-lookup"><span data-stu-id="6c388-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="6c388-115">Uma lista de artefatos associados a essa VM é exibida, indicando que nome de saudação do artefato hello e seu status.</span><span class="sxs-lookup"><span data-stu-id="6c388-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![Exemplo de repositório git de artefatos](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="6c388-117">Escolha um artefato que mostra um status **de falha**.</span><span class="sxs-lookup"><span data-stu-id="6c388-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="6c388-118">artefato Olá é aberto e mostra uma mensagem de extensão que inclui detalhes sobre a falha de saudação do artefato hello.</span><span class="sxs-lookup"><span data-stu-id="6c388-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![Exemplo de repositório git de artefatos](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="6c388-120">Solucionar problemas de falhas de artefato de dentro de saudação VM</span><span class="sxs-lookup"><span data-stu-id="6c388-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="6c388-121">logs de artefato de Olá tooview de dentro da máquina virtual de hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="6c388-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="6c388-122">Faça logon no toohello VM que contém o artefato Olá toodiagnose desejado.</span><span class="sxs-lookup"><span data-stu-id="6c388-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="6c388-123">Navegue tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status onde "1.9 é Olá CSE número da versão.</span><span class="sxs-lookup"><span data-stu-id="6c388-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![Exemplo de repositório git de artefatos](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="6c388-125">Olá abrir **status** tooview informações que ajuda a diagnosticar falhas de artefato para a VM do arquivo.</span><span class="sxs-lookup"><span data-stu-id="6c388-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="6c388-126">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="6c388-126">Related blog posts</span></span>
* [<span data-ttu-id="6c388-127">Ingressar em um domínio de AD usando um modelo do Gerenciador de recursos no Azure DevTest Labs de tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="6c388-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="6c388-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c388-128">Next steps</span></span>
* <span data-ttu-id="6c388-129">Saiba como muito[adicionar um laboratório de tooa repositório Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="6c388-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

