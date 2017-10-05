---
title: Criar uma imagem do RemoteApp do Azure | Microsoft Docs
description: "Saiba mais sobre as opções disponíveis para a criação de imagens para o RemoteApp do Azure"
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
ms.openlocfilehash: 4b8ba6f264f982e03930c5ad4ccdb2d80f2c8665
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="3acdc-103">Criar uma imagem de RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="3acdc-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3acdc-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="3acdc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3acdc-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="3acdc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3acdc-106">O Azure RemoteApp usa imagens para manter os aplicativos que você compartilha com seus usuários.</span><span class="sxs-lookup"><span data-stu-id="3acdc-106">Azure RemoteApp uses images to hold the apps that you share with your users.</span></span> <span data-ttu-id="3acdc-107">(Obtemos sua imagem e a usamos para criar VMs – e é isso o que os usuários acessam quando entram no Azure RemoteApp.) Para criar uma coleção do RemoteApp do Azure com sua escolha de aplicativos, seja ela de nuvem ou híbrida, você começa criando uma imagem com os aplicativos instalados.</span><span class="sxs-lookup"><span data-stu-id="3acdc-107">(We take your image and use it to create VMs - that's what the users access when they sign into Azure RemoteApp.) To create an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="3acdc-108">Em seguida, crie uma coleção que usa essa imagem, atribua usuários à coleção e publique aplicativos aos usuários.</span><span class="sxs-lookup"><span data-stu-id="3acdc-108">Then, create a collection that uses that image, assign users to the collection, and publish apps to those users.</span></span>

<span data-ttu-id="3acdc-109">Você tem várias opções para criar ou usar as imagens.</span><span class="sxs-lookup"><span data-stu-id="3acdc-109">You have several options for creating or using images.</span></span> <span data-ttu-id="3acdc-110">O [requisito](remoteapp-imagereqs.md) básico para uma imagem é ela executar o Windows Server 2012 R2 e ter a função de Host da Sessão da Área de Trabalho Remota (RDSH) instalada.</span><span class="sxs-lookup"><span data-stu-id="3acdc-110">The basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have the Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="3acdc-111">Como você obtém isso é onde as coisas ficam interessantes.</span><span class="sxs-lookup"><span data-stu-id="3acdc-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="3acdc-112">Você tem as seguintes opções quando se trata de imagens:</span><span class="sxs-lookup"><span data-stu-id="3acdc-112">You have the following options when it comes to images:</span></span>

* <span data-ttu-id="3acdc-113">Você pode importar e usar uma [imagem com base em uma máquina virtual do Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="3acdc-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="3acdc-114">Isso é bom para aplicativos de linha de negócios que requerem configurações personalizadas.</span><span class="sxs-lookup"><span data-stu-id="3acdc-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="3acdc-115">Você pode personalizar a imagem para trabalhar para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3acdc-115">You can customize the image to work for the app.</span></span>
* <span data-ttu-id="3acdc-116">Você pode [criar e carregar uma imagem personalizada](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="3acdc-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="3acdc-117">Isso é bom se você já tiver uma imagem que use para sua implantação de Serviços de Área de Trabalho Remota local.</span><span class="sxs-lookup"><span data-stu-id="3acdc-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="3acdc-118">Você pode usar uma das [imagens de modelo](remoteapp-images.md) incluídas na sua assinatura do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3acdc-118">You can use one of the [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="3acdc-119">Essas imagens são criadas e mantidas pela equipe do RemoteApp e contêm alguns aplicativos padrão (como o pacote do Office) que você pode disponibilizar para os usuários.</span><span class="sxs-lookup"><span data-stu-id="3acdc-119">These images are created and maintained by the RemoteApp team and contain some standard applications (like the Office suite) that you can make available to your users.</span></span> <span data-ttu-id="3acdc-120">Observe que apenas a imagem do Office 365 Pro Plus pode ser usada em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3acdc-120">Note that only the Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="3acdc-121">Independentemente de onde obter sua imagem ou como criá-la, convém certificar-se de que você entende os [requisitos de aplicativo](remoteapp-appreqs.md) para garantir que seu aplicativo funcione bem no RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3acdc-121">Regardless of where you get your image or how you create it, you'll want to make sure you understand the [app requirements](remoteapp-appreqs.md) to ensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="3acdc-122">Em seguida, a próxima etapa é criar uma coleção de [nuvem](remoteapp-create-cloud-deployment.md) ou [híbrida](remoteapp-create-hybrid-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="3acdc-122">Then, the next step is to create a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

