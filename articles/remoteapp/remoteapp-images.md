---
title: "aaaWhat está em imagens de modelo hello Azure RemoteApp? | Microsoft Docs"
description: "Saiba mais sobre imagens de modelo Olá incluídas com o Azure RemoteApp."
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
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a><span data-ttu-id="29518-104">O que há imagens de modelo hello Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="29518-104">What is in hello Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="29518-105">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="29518-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="29518-106">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="29518-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="29518-107">Sua assinatura do RemoteApp do Azure inclui três imagens de modelo:</span><span class="sxs-lookup"><span data-stu-id="29518-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="29518-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="29518-108">Windows Server 2012</span></span>
* <span data-ttu-id="29518-109">Microsoft Office 365 ProPlus (assinatura do Office 365 necessária)</span><span class="sxs-lookup"><span data-stu-id="29518-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="29518-110">Microsoft Office 2013 Professional Plus (somente avaliação)</span><span class="sxs-lookup"><span data-stu-id="29518-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29518-111">Sua assinatura do Azure RemoteApp concede que acesso toohello software nas imagens hello, com exceção de saudação do Office 365 ProPlus, que requer uma assinatura separada, e Office 2013, que não pode ser usado na produção.</span><span class="sxs-lookup"><span data-stu-id="29518-111">Your Azure RemoteApp subscription grants you access toohello software in hello images, with hello exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="29518-112">Isso significa que você pode compartilhar programas hello ou aplicativos em imagens de modelo Olá com seus usuários.</span><span class="sxs-lookup"><span data-stu-id="29518-112">This means that you can share hello programs or apps on hello template images with your users.</span></span> <span data-ttu-id="29518-113">Por exemplo, se você criar uma coleção que usa a imagem do Windows Server 2012 R2 hello, você pode publicar System Center Endpoint Protection para tooaccess de usuários por meio do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="29518-113">For example, if you create a collection that uses hello Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users tooaccess through RemoteApp.</span></span>
> 
> <span data-ttu-id="29518-114">Check-out Olá [RemoteApp licenciamento detalhes](remoteapp-licensing.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="29518-114">Check out hello [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="29518-115">E [usando o Office com o Azure RemoteApp](remoteapp-o365.md) para Olá informações de licenciamento do Office.</span><span class="sxs-lookup"><span data-stu-id="29518-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for hello Office licensing info.</span></span>
> 
> 

<span data-ttu-id="29518-116">Leia mais para obter detalhes sobre o que cada imagem contém.</span><span class="sxs-lookup"><span data-stu-id="29518-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--hello-vanilla-image"></a><span data-ttu-id="29518-117">Windows Server 2012 R2 ("Olá baunilha imagem")</span><span class="sxs-lookup"><span data-stu-id="29518-117">Windows Server 2012 R2  ("hello vanilla image")</span></span>
<span data-ttu-id="29518-118">Esta imagem é baseada no sistema de operacional do Microsoft Windows Server 2012 R2 Datacenter e tem hello seguintes funções e recursos instalados toomeet requisitos de saudação para imagens de modelo do RemoteApp do Azure:</span><span class="sxs-lookup"><span data-stu-id="29518-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has hello following roles and features installed toomeet hello requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="29518-119">.NET framework 4.5, 3.5.1 e 3.5</span><span class="sxs-lookup"><span data-stu-id="29518-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="29518-120">Experiência Desktop</span><span class="sxs-lookup"><span data-stu-id="29518-120">Desktop Experience</span></span>
* <span data-ttu-id="29518-121">Serviços de tinta e manuscrito</span><span class="sxs-lookup"><span data-stu-id="29518-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="29518-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="29518-122">Media Foundation</span></span>
* <span data-ttu-id="29518-123">Host de sessão de área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="29518-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="29518-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="29518-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="29518-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="29518-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="29518-126">Suporte a WoW64</span><span class="sxs-lookup"><span data-stu-id="29518-126">WoW64 Support</span></span>

<span data-ttu-id="29518-127">Esta imagem tem também Olá aplicativos instalados a seguir:</span><span class="sxs-lookup"><span data-stu-id="29518-127">This image also has hello following applications installed:</span></span>

* <span data-ttu-id="29518-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="29518-128">Adobe Flash Player</span></span>
* <span data-ttu-id="29518-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="29518-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="29518-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="29518-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="29518-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="29518-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="29518-132">Microsoft Office 365 ProPlus (assinatura necessária)</span><span class="sxs-lookup"><span data-stu-id="29518-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="29518-133">O Office 365 é hello mais aplicativo solicitado, criamos uma imagem "custom" você toowork com.</span><span class="sxs-lookup"><span data-stu-id="29518-133">Office 365 is hello most requested application, so we created a "custom" image for you toowork with.</span></span>

<span data-ttu-id="29518-134">Esta imagem é uma extensão da imagem de baunilha hello e tem hello seguintes componentes do Microsoft Office 365 ProPlus instalado além toohello componentes descritos na imagem do Windows Server 2012 R2 hello:</span><span class="sxs-lookup"><span data-stu-id="29518-134">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 365 ProPlus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="29518-135">Access</span><span class="sxs-lookup"><span data-stu-id="29518-135">Access</span></span>
* <span data-ttu-id="29518-136">Excel</span><span class="sxs-lookup"><span data-stu-id="29518-136">Excel</span></span>
* <span data-ttu-id="29518-137">Lync</span><span class="sxs-lookup"><span data-stu-id="29518-137">Lync</span></span>
* <span data-ttu-id="29518-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="29518-138">OneNote</span></span>
* <span data-ttu-id="29518-139">OneDrive para empresas (Observe que o agente de sincronização Olá não tem suporte para uso com o Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="29518-139">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="29518-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="29518-140">Outlook</span></span>
* <span data-ttu-id="29518-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="29518-141">PowerPoint</span></span>
* <span data-ttu-id="29518-142">Word</span><span class="sxs-lookup"><span data-stu-id="29518-142">Word</span></span>
* <span data-ttu-id="29518-143">Revisores de texto do Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="29518-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="29518-144">imagem de saudação também inclui Visio Pro e Pro do projeto.</span><span class="sxs-lookup"><span data-stu-id="29518-144">hello image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="29518-145">E Olá aplicativos, bem como a seguir:</span><span class="sxs-lookup"><span data-stu-id="29518-145">And hello following applications, as well:</span></span>

* <span data-ttu-id="29518-146">SQL Native client</span><span class="sxs-lookup"><span data-stu-id="29518-146">SQL Native client</span></span>
* <span data-ttu-id="29518-147">Driver ODBC</span><span class="sxs-lookup"><span data-stu-id="29518-147">ODBC Driver</span></span>
* <span data-ttu-id="29518-148">Cliente SQL Server Data Mining</span><span class="sxs-lookup"><span data-stu-id="29518-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="29518-149">Cliente MasterDataServices</span><span class="sxs-lookup"><span data-stu-id="29518-149">MasterDataServices client</span></span>
* <span data-ttu-id="29518-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="29518-150">Microsoft Publisher</span></span>
* <span data-ttu-id="29518-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="29518-151">PowerQuery</span></span>
* <span data-ttu-id="29518-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="29518-152">PowerMap</span></span>

<span data-ttu-id="29518-153">Toda a funcionalidade dos aplicativos do Office 365 ProPlus está disponível apenas para os usuários que têm um plano do Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="29518-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="29518-154">Para obter mais detalhes sobre a assinatura do Office 365 de saudação planos consulte [planos de serviço do Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="29518-154">For more details on hello Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="29518-155">Ainda tem dúvidas?</span><span class="sxs-lookup"><span data-stu-id="29518-155">Still have questions?</span></span> <span data-ttu-id="29518-156">Check-out Olá [Office 365 + RemoteApp](remoteapp-o365.md) informações.</span><span class="sxs-lookup"><span data-stu-id="29518-156">Check out hello [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="29518-157">Confira também novo artigo de hello, [como toouse sua assinatura do Office 365 com o Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="29518-157">Also check out hello new article, [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="29518-158">Observe que você precisa toolicense Office 365 ProPlus, Visio Pro e projeto Pro separadamente - cada um deles tem sua própria licença.</span><span class="sxs-lookup"><span data-stu-id="29518-158">Note that you need toolicense Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="29518-159">Microsoft Office 2013 Professional Plus (somente avaliação)</span><span class="sxs-lookup"><span data-stu-id="29518-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="29518-160">Durante o período de avaliação gratuita hello, você pode testar o serviço de saudação com imagem Olá Office 2013.</span><span class="sxs-lookup"><span data-stu-id="29518-160">During hello free trial period, you can test hello service with hello Office 2013 image.</span></span>

<span data-ttu-id="29518-161">Esta imagem é uma extensão da imagem de baunilha hello e tem hello seguintes componentes do Microsoft Office 2013 Professional Plus instalado além toohello componentes descritos na imagem do Windows Server 2012 R2 hello:</span><span class="sxs-lookup"><span data-stu-id="29518-161">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 2013 Professional Plus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="29518-162">Access</span><span class="sxs-lookup"><span data-stu-id="29518-162">Access</span></span>
* <span data-ttu-id="29518-163">Excel</span><span class="sxs-lookup"><span data-stu-id="29518-163">Excel</span></span>
* <span data-ttu-id="29518-164">Lync</span><span class="sxs-lookup"><span data-stu-id="29518-164">Lync</span></span>
* <span data-ttu-id="29518-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="29518-165">OneNote</span></span>
* <span data-ttu-id="29518-166">OneDrive para empresas (Observe que o agente de sincronização Olá não tem suporte para uso com o Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="29518-166">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="29518-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="29518-167">Outlook</span></span>
* <span data-ttu-id="29518-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="29518-168">PowerPoint</span></span>
* <span data-ttu-id="29518-169">Project</span><span class="sxs-lookup"><span data-stu-id="29518-169">Project</span></span>
* <span data-ttu-id="29518-170">Visio</span><span class="sxs-lookup"><span data-stu-id="29518-170">Visio</span></span>
* <span data-ttu-id="29518-171">Word</span><span class="sxs-lookup"><span data-stu-id="29518-171">Word</span></span>
* <span data-ttu-id="29518-172">Revisores de texto do Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="29518-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29518-173">**Informações legais:** esta imagem não inclui uma licença do Microsoft Office e *não pode ser usada para a produção*.</span><span class="sxs-lookup"><span data-stu-id="29518-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="29518-174">imagem do Office 2013 Professional Plus Olá destina-se somente para teste.</span><span class="sxs-lookup"><span data-stu-id="29518-174">hello Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="29518-175">Se você quiser toouse aplicativos do Office no Azure RemoteApp para produção, você precisa imagem Office 365 ProPlus do toouse hello.</span><span class="sxs-lookup"><span data-stu-id="29518-175">If you want toouse Office apps in Azure RemoteApp for production, you need toouse hello Office 365 ProPlus image.</span></span> <span data-ttu-id="29518-176">Para obter mais detalhes sobre licenciamento do Office, consulte [Usar o Office 365 com o RemoteApp do Azure](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="29518-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

