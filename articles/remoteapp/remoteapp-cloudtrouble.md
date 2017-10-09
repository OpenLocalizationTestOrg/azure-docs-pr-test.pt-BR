---
title: "coleções de nuvem do RemoteApp aaaTroubleshoot - criação | Microsoft Docs"
description: "Saiba como tootroubleshoot RemoteApp nuvem falhas na criação de coleção"
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
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="4763d-103">Solucionar problemas na criação de coleções em nuvem do RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4763d-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4763d-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="4763d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4763d-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="4763d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4763d-106">Se você estiver tendo problemas ao criar uma coleção de nuvem, confira Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="4763d-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="4763d-107">A imagem é inválida</span><span class="sxs-lookup"><span data-stu-id="4763d-107">Your image is invalid</span></span>
<span data-ttu-id="4763d-108">Se você vir uma mensagem como "GoldImageInvalid" quando você está esperando por Azure tooprovision sua coleção, isso significa que a imagem de modelo não atende a saudação [definido requisitos de imagem](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="4763d-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="4763d-109">Assim, vá ler os [requisitos](remoteapp-imagereqs.md), corrija sua imagem e tente toocreate sua coleção novamente.</span><span class="sxs-lookup"><span data-stu-id="4763d-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="4763d-110">Erros comuns vistos no portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="4763d-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="4763d-111">Coleções de nuvem geralmente falham durante a criação por você estar usando imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="4763d-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="4763d-112">Se você vir um Olá acima erros e você estiver usando uma coleção de saudação toocreate imagem personalizada, consulte Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4763d-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="4763d-113">Certifique-se de que essa imagem personalizada Olá carregado atende aos requisitos de imagem.</span><span class="sxs-lookup"><span data-stu-id="4763d-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="4763d-114">Problema comum geralmente Olá é que imagem Olá não foi corretamente submetida a Sysprep.</span><span class="sxs-lookup"><span data-stu-id="4763d-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="4763d-115">Verifique se imagem Olá pode inicializar dentro do Hyper-V ou tente criar uma VM IAAS diretamente na sua assinatura do Azure usando a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="4763d-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="4763d-116">Se Olá VM falhar tooboot e não iniciar, em seguida, isso geralmente indica que essa imagem personalizada Olá não estava preparada corretamente.</span><span class="sxs-lookup"><span data-stu-id="4763d-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="4763d-117">Verifique se a imagem personalizada Olá foi criada seguindo hello como toocreate um modelo personalizado de imagem do RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4763d-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="4763d-118">Se você estiver usando uma das imagens do Microsoft hello incluídas com sua assinatura, tente toocreate a coleção de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="4763d-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="4763d-119">Se Olá problema persistir, entre em contato com o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4763d-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="4763d-120">Se você vir esse erro geral, isso significa que foram atualizados tooa paga conta, mas você está tentando toouse uma imagem fornecido pela Microsoft que é válida somente durante o modo de avaliação de saudação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="4763d-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="4763d-121">Nesse caso, tente toocreate novamente sua coleção de nuvem, mas se toospecify Olá correto imagem.</span><span class="sxs-lookup"><span data-stu-id="4763d-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

