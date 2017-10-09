---
title: "configurações de imagens do Azure Marketplace aaaConfigure no Azure DevTest Labs | Microsoft Docs"
description: Configure quais imagens do Azure Marketplace podem ser usadas ao criar uma VM no Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="e8b13-103">Definir configurações de imagem do Azure Marketplace no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e8b13-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="e8b13-104">DevTest Labs dá suporte ao criar máquinas virtuais baseadas em imagens do Azure Marketplace dependendo de como você configurou o Azure Marketplace imagens toobe usado no laboratório.</span><span class="sxs-lookup"><span data-stu-id="e8b13-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="e8b13-105">Este artigo mostra como toospecify que, se houver, imagens do Azure Marketplace podem ser usado ao criar máquinas virtuais em um laboratório.</span><span class="sxs-lookup"><span data-stu-id="e8b13-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="e8b13-106">Isso garante que sua equipe tem apenas acesso toohello Marketplace imagens.</span><span class="sxs-lookup"><span data-stu-id="e8b13-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="e8b13-107">Selecionar quais imagens do Azure Marketplace são permitidas durante a criação de uma VM</span><span class="sxs-lookup"><span data-stu-id="e8b13-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="e8b13-108">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e8b13-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="e8b13-109">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8b13-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="e8b13-110">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="e8b13-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="e8b13-111">Na folha do laboratório hello, selecione **políticas e configurações**.</span><span class="sxs-lookup"><span data-stu-id="e8b13-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="e8b13-112">Na folha **Configurações e políticas** do laboratório, em **Bases da Máquina Virtual**, selecione **Imagens do Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="e8b13-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="e8b13-113">Especifique se deseja que todos os Olá qualificado toobe de imagens do Azure Marketplace disponível para uso como uma base de uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="e8b13-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="e8b13-114">Se você selecionar **Sim**, em seguida, todas as imagens do Azure Marketplace Olá que atendem a Olá a todos os critérios a seguir são permitidos em laboratório hello:</span><span class="sxs-lookup"><span data-stu-id="e8b13-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="e8b13-115">imagem de saudação cria uma única VM, **e**</span><span class="sxs-lookup"><span data-stu-id="e8b13-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="e8b13-116">imagem de saudação usa o Azure Resource Manager tooprovision VMs, **e**</span><span class="sxs-lookup"><span data-stu-id="e8b13-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="e8b13-117">imagem Olá não exige a compra um plano de licenciamento adicionais</span><span class="sxs-lookup"><span data-stu-id="e8b13-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="e8b13-118">Se você não quiser que nenhum toobe imagens permitido, ou você deseja toospecify quais imagens podem ser usados, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="e8b13-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Opção tooallow todos os toobe de imagens do Marketplace usado como base imagens para máquinas virtuais](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="e8b13-120">Se você selecionar **não** toohello anterior etapa, hello **permitidos imagens/selecionar todos os** caixa de seleção está habilitada.</span><span class="sxs-lookup"><span data-stu-id="e8b13-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="e8b13-121">Você pode usar essa opção junto com hello pesquisa caixa tooquickly selecionar ou desmarcar todos os itens de saudação exibidos na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8b13-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="e8b13-122">Selecione imagens do Azure Marketplace Olá tooallow você deseja para a criação de VM individualmente, marcando a caixa de seleção de cada imagem correspondente.</span><span class="sxs-lookup"><span data-stu-id="e8b13-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="e8b13-123">Não selecione nada na lista de saudação se você não quiser tooallow qualquer toobe de imagens do Azure Marketplace usado no laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8b13-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![Você pode especificar quais imagens do Marketplace podem ser usadas como imagens base para VMs](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="e8b13-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8b13-125">Next steps</span></span>
<span data-ttu-id="e8b13-126">Depois de ter configurado como imagens do Azure Marketplace são permitidas durante a criação de uma máquina virtual, o hello próxima etapa é muito[adicionar um laboratório de tooyour VM](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="e8b13-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

