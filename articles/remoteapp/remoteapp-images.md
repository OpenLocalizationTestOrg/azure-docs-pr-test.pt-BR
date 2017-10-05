---
title: "O que são as imagens de modelo do RemoteApp do Azure? | Microsoft Docs"
description: "Saiba mais sobre as imagens de modelo incluídas no RemoteApp do Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cd4e1a16a7c42bd00d9e543d7b62b72e9de3fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-in-the-azure-remoteapp-template-images"></a><span data-ttu-id="f9d37-104">O que são as imagens de modelo do RemoteApp do Azure?</span><span class="sxs-lookup"><span data-stu-id="f9d37-104">What is in the Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f9d37-105">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="f9d37-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f9d37-106">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f9d37-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f9d37-107">Sua assinatura do RemoteApp do Azure inclui três imagens de modelo:</span><span class="sxs-lookup"><span data-stu-id="f9d37-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="f9d37-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f9d37-108">Windows Server 2012</span></span>
* <span data-ttu-id="f9d37-109">Microsoft Office 365 ProPlus (assinatura do Office 365 necessária)</span><span class="sxs-lookup"><span data-stu-id="f9d37-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="f9d37-110">Microsoft Office 2013 Professional Plus (somente avaliação)</span><span class="sxs-lookup"><span data-stu-id="f9d37-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9d37-111">Sua assinatura do RemoteApp do Azure concede o acesso ao software nas imagens, com exceção do Office 365 ProPlus, que requer uma assinatura separada, e do Office 2013, que não pode ser usado na produção.</span><span class="sxs-lookup"><span data-stu-id="f9d37-111">Your Azure RemoteApp subscription grants you access to the software in the images, with the exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="f9d37-112">Isso significa que você pode compartilhar os programas ou aplicativos nas imagens de modelo com seus usuários.</span><span class="sxs-lookup"><span data-stu-id="f9d37-112">This means that you can share the programs or apps on the template images with your users.</span></span> <span data-ttu-id="f9d37-113">Por exemplo, se você criar uma coleção que usa a imagem do Windows Server 2012 R2, poderá publicar o System Center Endpoint Protection para que os usuários acessem por meio do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f9d37-113">For example, if you create a collection that uses the Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users to access through RemoteApp.</span></span>
> 
> <span data-ttu-id="f9d37-114">Confira os [Detalhes de licenciamento do RemoteApp](remoteapp-licensing.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f9d37-114">Check out the [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="f9d37-115">Consulte também [Usando o Office com o RemoteApp do Azure](remoteapp-o365.md) para obter informações de licenciamento do Office.</span><span class="sxs-lookup"><span data-stu-id="f9d37-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for the Office licensing info.</span></span>
> 
> 

<span data-ttu-id="f9d37-116">Leia mais para obter detalhes sobre o que cada imagem contém.</span><span class="sxs-lookup"><span data-stu-id="f9d37-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--the-vanilla-image"></a><span data-ttu-id="f9d37-117">Windows Server 2012 R2 ("a imagem baunilha")</span><span class="sxs-lookup"><span data-stu-id="f9d37-117">Windows Server 2012 R2  ("the vanilla image")</span></span>
<span data-ttu-id="f9d37-118">Essa imagem é baseada no sistema operacional para Data Center Microsoft Windows Server 2012 R2 e tem as seguintes funções e recursos instalados para atender aos requisitos de imagens de modelo RemoteApp do Azure:</span><span class="sxs-lookup"><span data-stu-id="f9d37-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has the following roles and features installed to meet the requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="f9d37-119">.NET framework 4.5, 3.5.1 e 3.5</span><span class="sxs-lookup"><span data-stu-id="f9d37-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="f9d37-120">Experiência Desktop</span><span class="sxs-lookup"><span data-stu-id="f9d37-120">Desktop Experience</span></span>
* <span data-ttu-id="f9d37-121">Serviços de tinta e manuscrito</span><span class="sxs-lookup"><span data-stu-id="f9d37-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="f9d37-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="f9d37-122">Media Foundation</span></span>
* <span data-ttu-id="f9d37-123">Host de sessão de área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="f9d37-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="f9d37-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="f9d37-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="f9d37-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="f9d37-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="f9d37-126">Suporte a WoW64</span><span class="sxs-lookup"><span data-stu-id="f9d37-126">WoW64 Support</span></span>

<span data-ttu-id="f9d37-127">Esta imagem também tem os seguintes aplicativos instalados:</span><span class="sxs-lookup"><span data-stu-id="f9d37-127">This image also has the following applications installed:</span></span>

* <span data-ttu-id="f9d37-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="f9d37-128">Adobe Flash Player</span></span>
* <span data-ttu-id="f9d37-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="f9d37-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="f9d37-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="f9d37-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="f9d37-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="f9d37-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="f9d37-132">Microsoft Office 365 ProPlus (assinatura necessária)</span><span class="sxs-lookup"><span data-stu-id="f9d37-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="f9d37-133">O Office 365 é o aplicativo mais solicitado, criamos uma imagem "personalizada" para trabalhar com ele.</span><span class="sxs-lookup"><span data-stu-id="f9d37-133">Office 365 is the most requested application, so we created a "custom" image for you to work with.</span></span>

<span data-ttu-id="f9d37-134">Essa imagem é uma extensão da imagem baunilha e tem os seguintes componentes do Microsoft Office 365 ProPlus instalados juntamente com os componentes descritos na imagem do Windows Server 2012 R2:</span><span class="sxs-lookup"><span data-stu-id="f9d37-134">This image is an extension of the vanilla image and has the following components of Microsoft Office 365 ProPlus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="f9d37-135">Access</span><span class="sxs-lookup"><span data-stu-id="f9d37-135">Access</span></span>
* <span data-ttu-id="f9d37-136">Excel</span><span class="sxs-lookup"><span data-stu-id="f9d37-136">Excel</span></span>
* <span data-ttu-id="f9d37-137">Lync</span><span class="sxs-lookup"><span data-stu-id="f9d37-137">Lync</span></span>
* <span data-ttu-id="f9d37-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="f9d37-138">OneNote</span></span>
* <span data-ttu-id="f9d37-139">OneDrive for Business (Observe que o agente de sincronização não é suportado para o uso com o Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="f9d37-139">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="f9d37-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="f9d37-140">Outlook</span></span>
* <span data-ttu-id="f9d37-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f9d37-141">PowerPoint</span></span>
* <span data-ttu-id="f9d37-142">Word</span><span class="sxs-lookup"><span data-stu-id="f9d37-142">Word</span></span>
* <span data-ttu-id="f9d37-143">Revisores de texto do Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="f9d37-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="f9d37-144">A imagem também inclui Visio Pro e Project Pro.</span><span class="sxs-lookup"><span data-stu-id="f9d37-144">The image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="f9d37-145">E os seguintes aplicativos, assim:</span><span class="sxs-lookup"><span data-stu-id="f9d37-145">And the following applications, as well:</span></span>

* <span data-ttu-id="f9d37-146">SQL Native client</span><span class="sxs-lookup"><span data-stu-id="f9d37-146">SQL Native client</span></span>
* <span data-ttu-id="f9d37-147">Driver ODBC</span><span class="sxs-lookup"><span data-stu-id="f9d37-147">ODBC Driver</span></span>
* <span data-ttu-id="f9d37-148">Cliente SQL Server Data Mining</span><span class="sxs-lookup"><span data-stu-id="f9d37-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="f9d37-149">Cliente MasterDataServices</span><span class="sxs-lookup"><span data-stu-id="f9d37-149">MasterDataServices client</span></span>
* <span data-ttu-id="f9d37-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="f9d37-150">Microsoft Publisher</span></span>
* <span data-ttu-id="f9d37-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="f9d37-151">PowerQuery</span></span>
* <span data-ttu-id="f9d37-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="f9d37-152">PowerMap</span></span>

<span data-ttu-id="f9d37-153">Toda a funcionalidade dos aplicativos do Office 365 ProPlus está disponível apenas para os usuários que têm um plano do Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="f9d37-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="f9d37-154">Para obter mais detalhes sobre os planos de assinatura do Office 365, consulte [Planos de serviço do Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9d37-154">For more details on the Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="f9d37-155">Ainda tem dúvidas?</span><span class="sxs-lookup"><span data-stu-id="f9d37-155">Still have questions?</span></span> <span data-ttu-id="f9d37-156">Confira as informações do [Office 365 + RemoteApp](remoteapp-o365.md) .</span><span class="sxs-lookup"><span data-stu-id="f9d37-156">Check out the [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="f9d37-157">Verifique também o novo artigo, [Como usar sua assinatura do Office 365 com o RemoteApp do Azure](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="f9d37-157">Also check out the new article, [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="f9d37-158">Observe que você precisa licenciar o Office 365 ProPlus, o Visio Pro e o Project Pro separadamente - cada um deles tem sua própria licença.</span><span class="sxs-lookup"><span data-stu-id="f9d37-158">Note that you need to license Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="f9d37-159">Microsoft Office 2013 Professional Plus (somente avaliação)</span><span class="sxs-lookup"><span data-stu-id="f9d37-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="f9d37-160">Durante o período de avaliação gratuito, você pode testar o serviço com a imagem do Office 2013.</span><span class="sxs-lookup"><span data-stu-id="f9d37-160">During the free trial period, you can test the service with the Office 2013 image.</span></span>

<span data-ttu-id="f9d37-161">Essa imagem é uma extensão da imagem baunilha e tem os seguintes componentes do Microsoft Office 2013 ProPlus instalados juntamente com os componentes descritos na imagem do Windows Server 2012 R2:</span><span class="sxs-lookup"><span data-stu-id="f9d37-161">This image is an extension of the vanilla image and has the following components of Microsoft Office 2013 Professional Plus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="f9d37-162">Access</span><span class="sxs-lookup"><span data-stu-id="f9d37-162">Access</span></span>
* <span data-ttu-id="f9d37-163">Excel</span><span class="sxs-lookup"><span data-stu-id="f9d37-163">Excel</span></span>
* <span data-ttu-id="f9d37-164">Lync</span><span class="sxs-lookup"><span data-stu-id="f9d37-164">Lync</span></span>
* <span data-ttu-id="f9d37-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="f9d37-165">OneNote</span></span>
* <span data-ttu-id="f9d37-166">OneDrive for Business (Observe que o agente de sincronização não é suportado para o uso com o Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="f9d37-166">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="f9d37-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="f9d37-167">Outlook</span></span>
* <span data-ttu-id="f9d37-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f9d37-168">PowerPoint</span></span>
* <span data-ttu-id="f9d37-169">Project</span><span class="sxs-lookup"><span data-stu-id="f9d37-169">Project</span></span>
* <span data-ttu-id="f9d37-170">Visio</span><span class="sxs-lookup"><span data-stu-id="f9d37-170">Visio</span></span>
* <span data-ttu-id="f9d37-171">Word</span><span class="sxs-lookup"><span data-stu-id="f9d37-171">Word</span></span>
* <span data-ttu-id="f9d37-172">Revisores de texto do Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="f9d37-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9d37-173">**Informações legais:** esta imagem não inclui uma licença do Microsoft Office e *não pode ser usada para a produção*.</span><span class="sxs-lookup"><span data-stu-id="f9d37-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="f9d37-174">A imagem do Office 2013 Professional Plus é destinada apenas ao uso para avaliação.</span><span class="sxs-lookup"><span data-stu-id="f9d37-174">The Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="f9d37-175">Se quiser usar os aplicativos do Office no RemoteApp do Azure para produção, você precisará usar a imagem do Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="f9d37-175">If you want to use Office apps in Azure RemoteApp for production, you need to use the Office 365 ProPlus image.</span></span> <span data-ttu-id="f9d37-176">Para obter mais detalhes sobre licenciamento do Office, consulte [Usar o Office 365 com o RemoteApp do Azure](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="f9d37-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

