---
title: "Solucionar problemas de coleções na nuvem do RemoteApp – criação | Microsoft Docs"
description: "Saiba como solucionar problemas de falhas de criação de coleção de nuvem do RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="6df90-103">Solucionar problemas na criação de coleções em nuvem do RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6df90-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6df90-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="6df90-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6df90-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="6df90-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6df90-106">Se você estiver tendo problemas ao criar uma coleção de nuvem, confira as informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="6df90-106">If you are having problems creating a cloud collection, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="6df90-107">A imagem é inválida</span><span class="sxs-lookup"><span data-stu-id="6df90-107">Your image is invalid</span></span>
<span data-ttu-id="6df90-108">Se você receber uma mensagem como “GoldImageInvalid” quando estiver aguardando enquanto o Azure provisiona sua coleção, isso significa que a sua imagem de modelo não atende aos [requisitos de imagem definidos](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="6df90-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="6df90-109">Portanto, leia esses [requisitos](remoteapp-imagereqs.md), corrija sua imagem e tente criar novamente sua coleção.</span><span class="sxs-lookup"><span data-stu-id="6df90-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="common-errors-seen-in-the-azure-management-portal"></a><span data-ttu-id="6df90-110">Erros comuns vistos no portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="6df90-110">Common errors seen in the Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="6df90-111">Coleções de nuvem geralmente falham durante a criação por você estar usando imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="6df90-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="6df90-112">Se você receber um dos erros anteriores e estiver usando uma imagem personalizada para criar a coleção, verifique os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6df90-112">If you see one of the above errors and you are using a custom image to create the collection, please check the following things:</span></span>

* <span data-ttu-id="6df90-113">Certifique-se de que a imagem personalizada carregada atende aos requisitos de imagem.</span><span class="sxs-lookup"><span data-stu-id="6df90-113">Ensure that the custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="6df90-114">Geralmente, o problema comum é que a imagem não foi corretamente preparada para o sistema.</span><span class="sxs-lookup"><span data-stu-id="6df90-114">Most often the common problem is that the image was not properly syspreped.</span></span>  
* <span data-ttu-id="6df90-115">Verifique se a imagem pode inicializar no Hyper-V ou tente criar uma VM IAAS diretamente na assinatura do Azure usando a imagem.</span><span class="sxs-lookup"><span data-stu-id="6df90-115">Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image.</span></span> <span data-ttu-id="6df90-116">Se a VM falhar ao inicializar e não iniciar, isso geralmente indica que a imagem personalizada não estava preparada corretamente.</span><span class="sxs-lookup"><span data-stu-id="6df90-116">If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.</span></span>  <span data-ttu-id="6df90-117">Verifique se a imagem personalizada foi criada seguindo as instruções em Como criar uma imagem de modelo personalizado para o RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6df90-117">Verify the custom image was built following the How to create a custom template image for RemoteApp</span></span>

<span data-ttu-id="6df90-118">Se você estiver usando uma das imagens Microsoft incluídas em sua assinatura, tente criar novamente a coleção.</span><span class="sxs-lookup"><span data-stu-id="6df90-118">If you are using one of the Microsoft images included with your subscription, try to create the collection again.</span></span> <span data-ttu-id="6df90-119">Se o problema persistir, contate o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6df90-119">If the issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="6df90-120">Se você receber esse erro, isso geralmente significa que você atualizou para uma conta paga, mas está tentando usar uma imagem fornecido pela Microsoft que é válida somente durante o modo de avaliação do serviço.</span><span class="sxs-lookup"><span data-stu-id="6df90-120">If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service.</span></span> <span data-ttu-id="6df90-121">Nesse caso, tente criar novamente sua coleção de nuvem, mas não se esqueça de especificar a imagem correta.</span><span class="sxs-lookup"><span data-stu-id="6df90-121">In this case, try to create your cloud collection again, but be sure to specify the correct image.</span></span>

