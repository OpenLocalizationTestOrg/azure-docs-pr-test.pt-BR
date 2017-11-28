---
title: "Definir configurações de imagem do Azure Marketplace no Azure DevTest Labs | Microsoft Docs"
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
ms.openlocfilehash: 5f888c9d92a9164cc7d3d1aed66c29a724b365d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="5be0e-103">Definir configurações de imagem do Azure Marketplace no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5be0e-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="5be0e-104">O DevTest Labs dá suporte à criação de VMs com base em imagens do Azure Marketplace, dependendo de como você tiver configurado o uso de imagens do Azure Marketplace em seu laboratório.</span><span class="sxs-lookup"><span data-stu-id="5be0e-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span></span> <span data-ttu-id="5be0e-105">Este artigo mostra como especificar quais imagens (caso haja alguma) do Azure Marketplace podem ser usadas durante a criação de VMs em um laboratório.</span><span class="sxs-lookup"><span data-stu-id="5be0e-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="5be0e-106">Isso garante que sua equipe tenha acesso apenas às imagens do Marketplace de que precisam.</span><span class="sxs-lookup"><span data-stu-id="5be0e-106">This ensures that your team only has access to the Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="5be0e-107">Selecionar quais imagens do Azure Marketplace são permitidas durante a criação de uma VM</span><span class="sxs-lookup"><span data-stu-id="5be0e-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="5be0e-108">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5be0e-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="5be0e-109">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="5be0e-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="5be0e-110">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="5be0e-110">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="5be0e-111">Na folha do laboratório, selecione **Configuração e Políticas**.</span><span class="sxs-lookup"><span data-stu-id="5be0e-111">On the lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="5be0e-112">Na folha **Configurações e políticas** do laboratório, em **Bases da Máquina Virtual**, selecione **Imagens do Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="5be0e-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="5be0e-113">Especifique se você deseja que todas as imagens qualificadas do Azure Marketplace estejam disponíveis para uso como uma base de uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="5be0e-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span></span> <span data-ttu-id="5be0e-114">Se você selecionar **Sim**, todas as imagens do Azure Marketplace que atenderem a todos os critérios a seguir serão permitidas no laboratório:</span><span class="sxs-lookup"><span data-stu-id="5be0e-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span></span>
   
   * <span data-ttu-id="5be0e-115">A imagem cria uma única VM **e**</span><span class="sxs-lookup"><span data-stu-id="5be0e-115">The image creates a single VM, **and**</span></span>
   * <span data-ttu-id="5be0e-116">A imagem usa o Azure Resource Manager para provisionar VMs **e**</span><span class="sxs-lookup"><span data-stu-id="5be0e-116">The image uses Azure Resource Manager to provision VMs, **and**</span></span>
   * <span data-ttu-id="5be0e-117">A imagem não exige a compra de um plano de licenciamento extra</span><span class="sxs-lookup"><span data-stu-id="5be0e-117">The image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="5be0e-118">Se você não quiser permitir qualquer imagem, ou se quiser especificar quais imagens poderão ser usadas, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="5be0e-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span></span>
     
     ![Opção para permitir que todas as imagens do Marketplace sejam usadas como imagens base para VMs](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="5be0e-120">Se você tiver selecionado **Não** na etapa anterior, a caixa de seleção **Imagens permitidas/Selecionar todas** será habilitada.</span><span class="sxs-lookup"><span data-stu-id="5be0e-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="5be0e-121">Você pode usar essa opção junto com a caixa de pesquisa para marcar ou desmarcar rapidamente todos os itens exibidos na lista.</span><span class="sxs-lookup"><span data-stu-id="5be0e-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span></span>
   * <span data-ttu-id="5be0e-122">Selecione as imagens do Azure Marketplace que você deseja permitir para a criação da VM individualmente, marcando a caixa de seleção correspondente de cada imagem.</span><span class="sxs-lookup"><span data-stu-id="5be0e-122">Select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="5be0e-123">Não selecione nada na lista se não quiser permitir que as imagens do Azure Marketplace sejam usadas no laboratório.</span><span class="sxs-lookup"><span data-stu-id="5be0e-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span></span>
   
    ![Você pode especificar quais imagens do Marketplace podem ser usadas como imagens base para VMs](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="5be0e-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5be0e-125">Next steps</span></span>
<span data-ttu-id="5be0e-126">Depois de configurar como as imagens do Azure Marketplace são permitidas durante a criação de uma VM, a próxima etapa será [adicionar uma VM ao seu laboratório](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="5be0e-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

