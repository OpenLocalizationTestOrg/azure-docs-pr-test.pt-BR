---
title: aaaCreate uma imagem do RemoteApp do Azure | Microsoft Docs
description: "Saber mais sobre opções de saudação disponíveis para a criação de imagens do Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="06bda-103">Criar uma imagem de RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="06bda-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="06bda-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="06bda-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="06bda-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="06bda-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="06bda-106">O Azure RemoteApp usa imagens toohold Olá aplicativos que você compartilha com os usuários.</span><span class="sxs-lookup"><span data-stu-id="06bda-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="06bda-107">(É capturar sua imagem e usá-lo VMs toocreate - do qual os usuários de saudação acessam quando entrarem no Azure RemoteApp.) toocreate uma coleção do RemoteApp do Azure com sua escolha de aplicativos, seja nuvem ou híbrida, comece criando uma imagem com os aplicativos instalados.</span><span class="sxs-lookup"><span data-stu-id="06bda-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="06bda-108">Em seguida, crie uma coleção que usa essa imagem, atribuir usuários a coleção de toohello e publicar os usuários toothose de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="06bda-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="06bda-109">Você tem várias opções para criar ou usar as imagens.</span><span class="sxs-lookup"><span data-stu-id="06bda-109">You have several options for creating or using images.</span></span> <span data-ttu-id="06bda-110">Olá básico [requisito](remoteapp-imagereqs.md) para uma imagem que executam o Windows Server 2012 R2 e função de Host de sessão de área de trabalho remota (RDSH) Olá instalada.</span><span class="sxs-lookup"><span data-stu-id="06bda-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="06bda-111">Como você obtém isso é onde as coisas ficam interessantes.</span><span class="sxs-lookup"><span data-stu-id="06bda-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="06bda-112">Você tem as opções a seguir quando se trata de tooimages de saudação:</span><span class="sxs-lookup"><span data-stu-id="06bda-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="06bda-113">Você pode importar e usar uma [imagem com base em uma máquina virtual do Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="06bda-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="06bda-114">Isso é bom para aplicativos de linha de negócios que requerem configurações personalizadas.</span><span class="sxs-lookup"><span data-stu-id="06bda-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="06bda-115">Você pode personalizar Olá toowork de imagem para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="06bda-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="06bda-116">Você pode [criar e carregar uma imagem personalizada](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="06bda-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="06bda-117">Isso é bom se você já tiver uma imagem que use para sua implantação de Serviços de Área de Trabalho Remota local.</span><span class="sxs-lookup"><span data-stu-id="06bda-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="06bda-118">Você pode usar uma saudação [imagens de modelo](remoteapp-images.md) incluído na sua assinatura do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="06bda-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="06bda-119">Essas imagens são criadas e mantido pela equipe do RemoteApp hello e contêm alguns aplicativos padrão (como Olá Office suite) que você pode criar usuários tooyour disponíveis.</span><span class="sxs-lookup"><span data-stu-id="06bda-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="06bda-120">Observe que Olá Office 365 Pro Plus a imagem somente pode ser usada em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="06bda-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="06bda-121">Independentemente de onde obter sua imagem ou como criá-lo, você desejará toomake-se de que entendeu Olá [requisitos do aplicativo](remoteapp-appreqs.md) tooensure que o aplicativo funciona bem no RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="06bda-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="06bda-122">Em seguida, a próxima etapa de saudação é toocreate uma [nuvem](remoteapp-create-cloud-deployment.md) ou [híbrida](remoteapp-create-hybrid-deployment.md) coleção.</span><span class="sxs-lookup"><span data-stu-id="06bda-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

