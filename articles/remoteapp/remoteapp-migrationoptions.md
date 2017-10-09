---
title: "aaaOptions para a migração do Azure RemoteApp | Microsoft Docs"
description: "Saiba mais sobre opções de saudação para migrar do Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="28b49-103">Opções de migração fora do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="28b49-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="28b49-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="28b49-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="28b49-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="28b49-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="28b49-106">Se você interrompeu a usar o Azure RemoteApp devido a saudação [anúncio de desativação](https://go.microsoft.com/fwlink/?linkid=821148) ou como terminar sua avaliação, é necessário toomigrate do serviço de aplicativo do Azure RemoteApp tooanother.</span><span class="sxs-lookup"><span data-stu-id="28b49-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="28b49-107">Há duas abordagens diferentes para a migração: uma implantação autogerenciada (geralmente chamada de IaaS [infraestrutura como serviço]) ou uma oferta totalmente gerenciada (geralmente chamada de PaaS/SaaS [plataforma como serviço ou software como serviço]).</span><span class="sxs-lookup"><span data-stu-id="28b49-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="28b49-108">O IaaS de autoatendimento é uma implantação do tipo faça você mesmo que é gerenciada, operada e de sua propriedade, implantada diretamente em VMs (máquinas virtuais) ou sistemas físicos.</span><span class="sxs-lookup"><span data-stu-id="28b49-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="28b49-109">Em outros Olá terminar uma totalmente gerenciado PaaS/oferta de SaaS é mais como o Azure RemoteApp - um parceiro fornece uma camada de serviço sobre uma solução de comunicação remota que manipula operacionais e manutenção, enquanto você, como cliente Olá, fazer alguns gerenciamento de aplicativos e de imagem.</span><span class="sxs-lookup"><span data-stu-id="28b49-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="28b49-110">[Exibir hello Azure RemoteApp webinars nas opções de migração](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), ou continue lendo para obter mais informações (incluindo exemplos de saudação diferente opções de hospedagem).</span><span class="sxs-lookup"><span data-stu-id="28b49-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="28b49-111">Soluções (IaaS) autogerenciadas</span><span class="sxs-lookup"><span data-stu-id="28b49-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="28b49-112">**RDS em IaaS**</span><span class="sxs-lookup"><span data-stu-id="28b49-112">**RDS on IaaS**</span></span>
<span data-ttu-id="28b49-113">Você pode implantar uma implantação de Serviços de Área de Trabalho Remota (no Windows Server) com base em sessão nativa usando o RemoteApp ou áreas de trabalho locais ou em um ambiente hospedado (como em VMs do Azure).</span><span class="sxs-lookup"><span data-stu-id="28b49-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="28b49-114">Os RDS em implantações de IaaS são melhores para os clientes já familiarizados com eles e que já têm experiência técnica com implantações de RDS.</span><span class="sxs-lookup"><span data-stu-id="28b49-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="28b49-115">Você precisa com Software Assurance (SA) de licenciamento por Volume para toouse de licenças de acesso de cliente RDS essa opção de implantação.</span><span class="sxs-lookup"><span data-stu-id="28b49-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="28b49-116">A implantação dos RDS na VMs do Azure é mais fácil do que nunca quando você usa modelos de aplicação de patch e de implantação (leia uma [visão geral](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) e [obtenha-as](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="28b49-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="28b49-117">Você pode obter Olá mesmo recursos de dimensionamento Elásticos com recursos de modelo de implantação clássico do Azure (não recursos de modelo de recurso do Azure) dentro do Azure RemoteApp usando Olá [script de escala automática](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), embora não haja mais configurações e personalizações.</span><span class="sxs-lookup"><span data-stu-id="28b49-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="28b49-118">Quando você implanta RDS em VMs do Azure, o suporte é fornecido por meio de [suporte do Azure](https://azure.microsoft.com/support/plans/), Olá mesmo profissionais de suporte que o suporte para você com o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="28b49-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="28b49-119">Você pode obter estimativas de custo com base no seu uso existente entrando em contato com [suporte do Azure](https://azure.microsoft.com/support/plans/), ou você pode executar cálculos usando um breve toobe liberado Calculadora de preços.</span><span class="sxs-lookup"><span data-stu-id="28b49-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="28b49-120">Além disso, com as VMs da série N (atualmente na visualização privada) você pode adicionar vGPU - saber mais sobre como adicionar vGPU e sobre como muito[utilizem as melhorias de RDS no Windows Server 2016](https://myignite.microsoft.com/videos/2794) em nossa sessão Ignite.</span><span class="sxs-lookup"><span data-stu-id="28b49-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="28b49-121">Temos guias passo a passo de implantação para [Windows Server 2012 R2](http://aka.ms/rdsonazure) e [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist com sua implantação.</span><span class="sxs-lookup"><span data-stu-id="28b49-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="28b49-122">Check-out Olá [blog de área de trabalho remota](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) para notícias mais recentes hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="28b49-123">**Citrix no IaaS**</span><span class="sxs-lookup"><span data-stu-id="28b49-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="28b49-124">Uma implantação de Citrix nativa de XenApp ou XenDesktop com base em sessão pode ser implantada localmente ou em um ambiente hospedado (como em VMs do Azure).</span><span class="sxs-lookup"><span data-stu-id="28b49-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="28b49-125">Check-out de guia de implantação passo a passo do hello [Citrix XA 7.6 no Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="28b49-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="28b49-126">Leia mais sobre [Citrix no Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), incluindo uma calculadora de preços.</span><span class="sxs-lookup"><span data-stu-id="28b49-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="28b49-127">Você também pode encontrar um [Citrix contato](http://citrix.com/English/contact/index.asp) toodiscuss suas opções de com.</span><span class="sxs-lookup"><span data-stu-id="28b49-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="28b49-128">Ofertas (PaaS/SaaS) totalmente gerenciadas</span><span class="sxs-lookup"><span data-stu-id="28b49-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="28b49-129">Citrix XenApp Essentials (lançado em abril de 2017)</span><span class="sxs-lookup"><span data-stu-id="28b49-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="28b49-130">Disponível no hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials é o novo serviço de virtualização de aplicativo hello, combinando power hello e flexibilidade de Olá plataforma de nuvem Citrix com hello simples e prescritivas, e fácil de consumir a visão do Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="28b49-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="28b49-131">Os clientes existentes do Azure RemoteApp podem [registrar-se para uma avaliação gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="28b49-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="28b49-132">Observação: somente o encargo de serviço do usuário do Citrix é gratuito, os custos de computação e armazenamento do Azure ainda se aplicam</span><span class="sxs-lookup"><span data-stu-id="28b49-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="28b49-133">Saiba Mais:</span><span class="sxs-lookup"><span data-stu-id="28b49-133">Learn More:</span></span>
- [<span data-ttu-id="28b49-134">Migrar do Azure RemoteApp tooCitrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="28b49-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="28b49-135">Citrix e Microsoft</span><span class="sxs-lookup"><span data-stu-id="28b49-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="28b49-136">[Apresentação do Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span><span class="sxs-lookup"><span data-stu-id="28b49-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="28b49-137">Citrix Cloud XenApp Service e XenDesktop Service</span><span class="sxs-lookup"><span data-stu-id="28b49-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="28b49-138">[Serviço de nuvem XenApp do Citrix e XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) é a melhor solução Olá para entrega de saudação de aplicativos e desktops, além de gerenciamento avançado e recursos de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="28b49-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="28b49-139">Conexlink (nome da plataforma: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="28b49-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="28b49-140">[MyCloudIT](https://mycloudit.com) é uma plataforma de automação para toosimplify de empresas IT, otimizar e dimensionar migração hello e Olá de entrega de áreas de trabalho remotas, aplicativos remotos e infraestrutura de nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="28b49-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="28b49-141">plataforma de MyCloudIT Olá reduz o tempo de implantação em 95%, o custo em 30% do Azure e move a infra-estrutura de TI do seu cliente para nuvem Olá em questão de alguns pressionamentos de tecla.</span><span class="sxs-lookup"><span data-stu-id="28b49-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="28b49-142">Parceiros agora podem gerenciar os clientes de um painel global, os usuários finais de serviço em torno de Olá, mundo como nunca antes e aumentar as receitas sem adicionar uma sobrecarga adicional ou amplo treinamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="28b49-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="28b49-143">Localização primária: Dallas, Texas, EUA</span><span class="sxs-lookup"><span data-stu-id="28b49-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="28b49-144">Região de operação: em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="28b49-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="28b49-145">Status de parceiro: [ouro](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="28b49-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="28b49-146">Provedor de Serviços Microsoft Cloud: sim</span><span class="sxs-lookup"><span data-stu-id="28b49-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="28b49-147">Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos</span><span class="sxs-lookup"><span data-stu-id="28b49-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="28b49-148">Soluções de migração do Azure RemoteApp: sim, [saiba mais](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="28b49-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="28b49-149">Brian Garoutte, vice-presidente de desenvolvimento de negócios</span><span class="sxs-lookup"><span data-stu-id="28b49-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="28b49-150">Telefone: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="28b49-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="28b49-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="28b49-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="28b49-152">Frame</span><span class="sxs-lookup"><span data-stu-id="28b49-152">Frame</span></span>

<span data-ttu-id="28b49-153">As organizações de TI na empresa e governamentais, provedores de serviços gerenciados e principais fornecedores de software escolha quadro toocreate e gerenciar seus espaços de trabalho seguros, definida pelo software na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="28b49-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="28b49-154">Em organizações de pequeno toolarge quadro torna extremamente fácil toolet usuários acessar aplicativos do Windows em qualquer navegador em qualquer dispositivo.</span><span class="sxs-lookup"><span data-stu-id="28b49-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="28b49-155">Hello plataforma quadro inclui tudo o que um administrador necessidades toodeploy aplicativos da nuvem Olá incluindo hello infraestrutura do Azure e licenças RDS (trazer a sua conta do Azure e licenças é opcional).</span><span class="sxs-lookup"><span data-stu-id="28b49-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="28b49-156">Saiba sobre o [Frame no Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="28b49-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="28b49-157">Localização primária: San Mateo, CA, EUA</span><span class="sxs-lookup"><span data-stu-id="28b49-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="28b49-158">Região de operação: em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="28b49-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="28b49-159">Parceiro da Microsoft: Sim</span><span class="sxs-lookup"><span data-stu-id="28b49-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="28b49-160">Telefone: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="28b49-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="28b49-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="28b49-161">Awingu</span></span>
<span data-ttu-id="28b49-162">O Awingu fornece uma solução de espaço de trabalho online simples que executa aplicativos herdados, SaaS e documentos em um navegador com html5.</span><span class="sxs-lookup"><span data-stu-id="28b49-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="28b49-163">Disponibilizando, dessa forma, os aplicativos com segurança em qualquer tipo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="28b49-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="28b49-164">Para serviços SaaS, há uma ampla variedade de opções de logon único disponível.</span><span class="sxs-lookup"><span data-stu-id="28b49-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="28b49-165">Também é possível integrar profundamente diversos sistemas de arquivos (nuvem) ao seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="28b49-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="28b49-166">Mobilidade toofull Avançar, avançados de trabalho online do Awingu dará a segurança ideal com controles granulares (por exemplo, baixando/carregar), uso completo auditoria, multi-Factor Authentication (por exemplo, o Azure MFA), gravação da sessão e muito mais.</span><span class="sxs-lookup"><span data-stu-id="28b49-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="28b49-167">Desde a configuração inicial, o Awingu habilita o compartilhamento de documentos e aplicativos para colaboração otimizada e segura.</span><span class="sxs-lookup"><span data-stu-id="28b49-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="28b49-168">A solução do Awingu é uma API livre multilocatário e com diversos AD.</span><span class="sxs-lookup"><span data-stu-id="28b49-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="28b49-169">Ele é usado por pequenas e grandes empresas, provedores de serviços de nuvem e [ISVs](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="28b49-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="28b49-170">Esses clientes apreciam especialmente Olá fácil de usar, fácil de instalar e de baixo custo total de propriedade.</span><span class="sxs-lookup"><span data-stu-id="28b49-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="28b49-171">É Awingu tudo em um [disponíveis no hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) com 2 usuários simultâneos internos.</span><span class="sxs-lookup"><span data-stu-id="28b49-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="28b49-172">Licenças adicionais estão disponíveis por meio de uma [ampla gama de distribuidores e revendedores](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="28b49-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="28b49-173">Saiba mais sobre [Awingu em como tooAzure alternativo RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="28b49-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="28b49-174">Localização primária: Bélgica</span><span class="sxs-lookup"><span data-stu-id="28b49-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="28b49-175">Regiões de operação: EMEA, América do Norte e Brasil</span><span class="sxs-lookup"><span data-stu-id="28b49-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="28b49-176">Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos</span><span class="sxs-lookup"><span data-stu-id="28b49-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="28b49-177">**Global**:</span><span class="sxs-lookup"><span data-stu-id="28b49-177">**Global**:</span></span>
> 
> <span data-ttu-id="28b49-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="28b49-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="28b49-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="28b49-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="28b49-180">Telefone: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="28b49-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="28b49-181">**EC da Bélgica**:</span><span class="sxs-lookup"><span data-stu-id="28b49-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="28b49-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="28b49-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="28b49-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="28b49-183">9000 Gent</span></span>
> 
> <span data-ttu-id="28b49-184">Email: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="28b49-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="28b49-185">Telefone: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="28b49-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="28b49-186">**EUA**:</span><span class="sxs-lookup"><span data-stu-id="28b49-186">**USA**:</span></span>
> 
> <span data-ttu-id="28b49-187">7 floor, Ave 1177 de saudação Américas,</span><span class="sxs-lookup"><span data-stu-id="28b49-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="28b49-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="28b49-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="28b49-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="28b49-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="28b49-190">Provedor de serviços hospedados da Microsoft</span><span class="sxs-lookup"><span data-stu-id="28b49-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="28b49-191">Parceiros de hospedagem geralmente oferecem totalmente gerenciado hospedado área de trabalho do Windows hello de serviço de aplicativo, que pode incluir o gerenciamento de recursos do Azure, sistemas operacionais, aplicativos e assistência técnica usando o parceiro de saudação do contratos de licenciamento por com a Microsoft e outros fornecedores de software juntamente com sendo um contrato de licença de provedor de serviços tooallow revenda de licença de acesso de assinante (SAL).</span><span class="sxs-lookup"><span data-stu-id="28b49-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="28b49-192">Olá informações a seguir fornecem detalhes e informações de contato para alguns hosters Olá especializadas em ajudar os clientes com a migração do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="28b49-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="28b49-193">Check-out [lista atual de saudação de provedores de serviços hospedados](http://aka.ms/rdsonazurecertified) que concluiu Olá RDS no caminho e avaliação de aprendizado de IaaS.</span><span class="sxs-lookup"><span data-stu-id="28b49-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="28b49-194">Programa Citrix Service Provider</span><span class="sxs-lookup"><span data-stu-id="28b49-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="28b49-195">Olá Citrix programa do provedor de serviço facilita para serviço provedores toodeliver Olá manter a simplicidade da nuvem virtual computação tooSMBs, oferecendo a eles serviços Olá desejarem em um modelo fácil e flexível.</span><span class="sxs-lookup"><span data-stu-id="28b49-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="28b49-196">Provedores de serviço do Citrix aumentar seus negócios Microsoft SPLA e expandir seus investimentos na plataforma RDS com qualquer dispositivo, acesso em qualquer lugar, hello mais amplo suporte a aplicativos, uma experiência avançada, aumentar a segurança e maior escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="28b49-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="28b49-197">Por sua vez, provedores Citrix atraem mais assinantes, aumentam a satisfação do cliente e reduzem seus custos operacionais.</span><span class="sxs-lookup"><span data-stu-id="28b49-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="28b49-198">[Saiba mais](http://www.citrix.com/products/service-providers.html) ou [encontre um parceiro](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="28b49-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="28b49-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="28b49-199">Acuutech</span></span>
<span data-ttu-id="28b49-200">[Acuutech](http://www.acuutech.com) especializada em fornecer soluções de área de trabalho hospedadas, entrega de área de trabalho inteira e os aplicativos ISV experiências criadas no Microsoft tooa global cliente da tecnologia de base do Azure e seus datacenters.</span><span class="sxs-lookup"><span data-stu-id="28b49-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="28b49-201">Localização primária: Londres, Reino Unido; Cingapura; Houston, Texas</span><span class="sxs-lookup"><span data-stu-id="28b49-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="28b49-202">Região de operação: em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="28b49-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="28b49-203">Status de parceiro: ouro</span><span class="sxs-lookup"><span data-stu-id="28b49-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="28b49-204">Provedor de Serviços Microsoft Cloud: sim</span><span class="sxs-lookup"><span data-stu-id="28b49-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="28b49-205">Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos</span><span class="sxs-lookup"><span data-stu-id="28b49-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="28b49-206">Soluções de migração do Azure RemoteApp: sim, [saiba mais](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="28b49-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="28b49-207">**Reino Unido**:</span><span class="sxs-lookup"><span data-stu-id="28b49-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="28b49-208">5/6 York House, Road Langston,</span><span class="sxs-lookup"><span data-stu-id="28b49-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="28b49-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="28b49-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="28b49-210">Telefone: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="28b49-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="28b49-211">**Cingapura**:</span><span class="sxs-lookup"><span data-stu-id="28b49-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="28b49-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="28b49-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="28b49-213">Olá mundo, Cingapura 069532</span><span class="sxs-lookup"><span data-stu-id="28b49-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="28b49-214">Telefone: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="28b49-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="28b49-215">**América do Norte**:</span><span class="sxs-lookup"><span data-stu-id="28b49-215">**North America**:</span></span>
>   
> <span data-ttu-id="28b49-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="28b49-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="28b49-217">Suite 200, Houston, Texas 77098</span><span class="sxs-lookup"><span data-stu-id="28b49-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="28b49-218">Telefone: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="28b49-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="28b49-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="28b49-219">ASPEX</span></span>
<span data-ttu-id="28b49-220">[ASPEX](http://www.aspex.be/en) especializada em ISVs transição toohello nuvem e ISV' procurando toooptimize suas configurações atuais de nuvem.</span><span class="sxs-lookup"><span data-stu-id="28b49-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="28b49-221">O ASPEX oferece uma ampla variedade de serviços gerenciados, DeVOps e serviços de consultoria.</span><span class="sxs-lookup"><span data-stu-id="28b49-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="28b49-222">Localização primária: Antuérpia, Bélgica</span><span class="sxs-lookup"><span data-stu-id="28b49-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="28b49-223">Região de operação: Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="28b49-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="28b49-224">Status de parceiro: [prata](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="28b49-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="28b49-225">Provedor de Serviços Microsoft Cloud: sim</span><span class="sxs-lookup"><span data-stu-id="28b49-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="28b49-226">Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos</span><span class="sxs-lookup"><span data-stu-id="28b49-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="28b49-227">Soluções de migração do Azure RemoteApp: sim, [saiba mais](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="28b49-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="28b49-228">Telefone: +3232202198</span><span class="sxs-lookup"><span data-stu-id="28b49-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="28b49-229">Email: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="28b49-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="28b49-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="28b49-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="28b49-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="28b49-231">Caase.com</span></span>
<span data-ttu-id="28b49-232">[Caase.com](http://www.caase.com/) ajuda as empresas, governos locais, corpos de não-governamentais e instituições de saúde com sua jornada até uma maneira inteligente de trabalho no hello Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="28b49-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="28b49-233">Ser seguros e produtivos em qualquer lugar, com qualquer dispositivo e com baixo custo de TI.</span><span class="sxs-lookup"><span data-stu-id="28b49-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="28b49-234">Caase.com é uma verdadeira especialista em Microsoft Office365, Azure, Enterprise Mobility and Security e Windows.</span><span class="sxs-lookup"><span data-stu-id="28b49-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="28b49-235">Com nossa consultoria, serviços de migração, programas de adoção, treinamento, gerenciamento e suporte, o Caase.com cria uma plataforma segura e otimizada para colaboração para fornecedores, parceiros e funcionários de clientes.</span><span class="sxs-lookup"><span data-stu-id="28b49-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="28b49-236">Caase.com é mastermind Olá Olá espaço de trabalho remota do Azure (local de trabalho móvel) e Olá espaço de trabalho Digital (Social Intranet).</span><span class="sxs-lookup"><span data-stu-id="28b49-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="28b49-237">Ambas as soluções – realizadas com a adoção – são a base de saudação que garante que usuários Olá dessas soluções experiência mais agradável, bem-sucedida e eficiente de Olá seu toohello rota Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="28b49-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="28b49-238">Tradução holandesa e um filme de apoio aqui: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="28b49-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="28b49-239">Região de operação: com base nos Países Baixos, com alcance global</span><span class="sxs-lookup"><span data-stu-id="28b49-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="28b49-240">Status de parceiro: [ouro](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="28b49-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="28b49-241">Provedor de Serviços Microsoft Cloud: sim</span><span class="sxs-lookup"><span data-stu-id="28b49-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="28b49-242">Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos</span><span class="sxs-lookup"><span data-stu-id="28b49-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="28b49-243">Soluções de migração do Azure RemoteApp: sim, [saiba mais](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="28b49-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="28b49-244">Países Baixos:</span><span class="sxs-lookup"><span data-stu-id="28b49-244">Netherlands:</span></span>
> 
> <span data-ttu-id="28b49-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="28b49-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="28b49-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="28b49-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="28b49-247">Telefone: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="28b49-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="28b49-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="28b49-248">Nerdio</span></span>
<span data-ttu-id="28b49-249">[Nerdio para o Azure](http://getnerdio.com/nfa/) é uma plataforma de automação de TI que entrega ridiculamente simples de provisionamento, gerenciamento e a otimização completas dos ambientes de TI em Olá nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="28b49-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="28b49-250">Prepare áreas de trabalho virtuais, aplicativos remotos e servidores em apenas duas horas.</span><span class="sxs-lookup"><span data-stu-id="28b49-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="28b49-251">Administrar o ambiente Olá três cliques ou menos com o Portal de administração de Nerdio.</span><span class="sxs-lookup"><span data-stu-id="28b49-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="28b49-252">Use o dimensionamento automático inteligente e salve 40% de too60 em recursos de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="28b49-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="28b49-253">Localização primária: região de operação de Chicago, Illinois: Status do parceiro em todo o mundo: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Provedor de Serviços do Microsoft Cloud: Sim</span><span class="sxs-lookup"><span data-stu-id="28b49-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="28b49-254">Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos</span><span class="sxs-lookup"><span data-stu-id="28b49-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="28b49-255">Soluções de migração do Azure RemoteApp: sim</span><span class="sxs-lookup"><span data-stu-id="28b49-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="28b49-256">Av. Lincoln, 8001</span><span class="sxs-lookup"><span data-stu-id="28b49-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="28b49-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="28b49-257">Suite 212</span></span>
> 
> <span data-ttu-id="28b49-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="28b49-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="28b49-259">EUA</span><span class="sxs-lookup"><span data-stu-id="28b49-259">USA</span></span>
> 
> <span data-ttu-id="28b49-260">(844) 4NERDIO ext. 6</span><span class="sxs-lookup"><span data-stu-id="28b49-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="28b49-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="28b49-261">**SaaSplaza**</span></span>
<span data-ttu-id="28b49-262">O [SaaSplaza](http://www.saasplaza.com/) oferece um portfólio completo do Microsoft Dynamics (NAV, AX, GP, SL, CRM) em nuvem privada e pública (Azure).</span><span class="sxs-lookup"><span data-stu-id="28b49-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="28b49-263">Localização primária: Países Baixos</span><span class="sxs-lookup"><span data-stu-id="28b49-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="28b49-264">Região de operação: em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="28b49-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="28b49-265">Status de parceiro: [ouro](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="28b49-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="28b49-266">Provedor de Serviços Microsoft Cloud: sim</span><span class="sxs-lookup"><span data-stu-id="28b49-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="28b49-267">Oferece soluções de área de trabalho e RemoteApp com base em sessão: sim, ambos</span><span class="sxs-lookup"><span data-stu-id="28b49-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="28b49-268">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="28b49-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="28b49-269">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="28b49-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="28b49-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="28b49-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="28b49-271">Olá países baixos</span><span class="sxs-lookup"><span data-stu-id="28b49-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="28b49-272">Telefone: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="28b49-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="28b49-273">**Américas**:</span><span class="sxs-lookup"><span data-stu-id="28b49-273">**Americas**:</span></span>
> 
> <span data-ttu-id="28b49-274">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="28b49-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="28b49-275">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="28b49-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="28b49-276">San Diego</span><span class="sxs-lookup"><span data-stu-id="28b49-276">San Diego</span></span>
> 
> <span data-ttu-id="28b49-277">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="28b49-277">United States</span></span>
> 
> <span data-ttu-id="28b49-278">Telefone: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="28b49-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="28b49-279">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="28b49-279">**APAC**:</span></span>
> 
> <span data-ttu-id="28b49-280">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="28b49-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="28b49-281">\#11-08, Olá octógono</span><span class="sxs-lookup"><span data-stu-id="28b49-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="28b49-282">Cingapura 069534</span><span class="sxs-lookup"><span data-stu-id="28b49-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="28b49-283">Cingapura</span><span class="sxs-lookup"><span data-stu-id="28b49-283">Singapore</span></span>
>   
> <span data-ttu-id="28b49-284">Telefone – Cingapura: +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="28b49-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="28b49-285">Telefone – Austrália: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="28b49-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="28b49-286">Telefone – Nova Zelândia: +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="28b49-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="28b49-287">Precisa de mais ajuda?</span><span class="sxs-lookup"><span data-stu-id="28b49-287">Need more help?</span></span>
<span data-ttu-id="28b49-288">Ainda precisa de ajuda escolhendo ou tem mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="28b49-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="28b49-289">Use um dos Olá métodos tooget ajuda a seguir.</span><span class="sxs-lookup"><span data-stu-id="28b49-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="28b49-290">Envie-nos um email para [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="28b49-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="28b49-291">Entre em contato com o [Suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="28b49-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="28b49-292">Comece abrindo um [caso de Suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="28b49-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="28b49-293">Ligue para nós.</span><span class="sxs-lookup"><span data-stu-id="28b49-293">Call us.</span></span> <span data-ttu-id="28b49-294">[Encontre um número de vendas local](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="28b49-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

