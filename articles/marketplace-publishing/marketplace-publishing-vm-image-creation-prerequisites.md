---
title: "aaaTechnical pré-requisitos para criar uma imagem de máquina virtual para hello Azure Marketplace | Microsoft Docs"
description: "Entender os requisitos para criar e implantar uma imagem de máquina virtual toohello Azure Marketplace para outros Olá toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="aca7a-103">Pré-requisitos técnicos para criar uma imagem de máquina virtual para hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="aca7a-103">Technical prerequisites for creating a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="aca7a-104">Processo Olá completamente antes de começar de ler e entender por cada etapa é executada.</span><span class="sxs-lookup"><span data-stu-id="aca7a-104">Read hello process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="aca7a-105">Tanto quanto possível, você deve preparar as informações da sua empresa e outros dados, baixe as ferramentas necessárias e/ou criar componentes técnicos antes de começar o processo de criação de oferta de saudação.</span><span class="sxs-lookup"><span data-stu-id="aca7a-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning hello offer creation process.</span></span> <span data-ttu-id="aca7a-106">Esses itens devem estar claros com a leitura deste artigo.</span><span class="sxs-lookup"><span data-stu-id="aca7a-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="aca7a-107">Baixe as ferramentas e aplicativos necessários</span><span class="sxs-lookup"><span data-stu-id="aca7a-107">Download needed tools & applications</span></span>
<span data-ttu-id="aca7a-108">Você deve ter Olá prontos antes de começar o processo de saudação de itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="aca7a-108">You should have hello following items ready before beginning hello process:</span></span>

* <span data-ttu-id="aca7a-109">Dependendo de qual sistema operacional você está visando, Olá install [cmdlets do PowerShell do Azure](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) ou [ferramenta de interface de linha de comando do Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) de saudação [Downloads do Azure](https://azure.microsoft.com/downloads/) página.</span><span class="sxs-lookup"><span data-stu-id="aca7a-109">Depending on which operating system you are targeting, install hello [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="aca7a-110">Instale o Gerenciador do Armazenamento do Azure no CodePlex.</span><span class="sxs-lookup"><span data-stu-id="aca7a-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="aca7a-111">Baixe e instale Olá, ferramenta de teste de certificação para o certificado do Azure:</span><span class="sxs-lookup"><span data-stu-id="aca7a-111">Download and install hello Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="aca7a-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="aca7a-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="aca7a-113">Precisa de uma ferramenta de certificação do computador baseado em Windows toorun hello.</span><span class="sxs-lookup"><span data-stu-id="aca7a-113">You need a Windows-based computer toorun hello certification tool.</span></span> <span data-ttu-id="aca7a-114">Se você não tiver um computador baseado em Windows disponível, você pode executar a ferramenta de saudação usando uma VM com base em Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="aca7a-114">If you do not have a Windows-based computer available, you can run hello tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="aca7a-115">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="aca7a-115">Platforms supported</span></span>
<span data-ttu-id="aca7a-116">Você pode desenvolver VMs do Azure baseadas em Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="aca7a-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="aca7a-117">Alguns elementos da saudação publicação processo--como criar um compatível com o Azure disco rígido virtual (VHD) – use diferentes ferramentas e etapas, dependendo de qual sistema operacional você está usando:</span><span class="sxs-lookup"><span data-stu-id="aca7a-117">Some elements of hello publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="aca7a-118">Se você estiver usando o Linux, consulte a seção "Criar um VHD compatível com o Azure (com base em Linux)" toohello de saudação [guia de publicação de imagem de máquina Virtual](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="aca7a-118">If you are using Linux, refer toohello “Create an Azure-compatible VHD (Linux-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="aca7a-119">Se você estiver usando o Windows, consulte a seção "Criar um VHD compatível com o Azure (baseado em Windows)" toohello de saudação [guia de publicação de imagem de máquina Virtual](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="aca7a-119">If you are using Windows, refer toohello “Create an Azure-compatible VHD (Windows-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aca7a-120">Você precisará de acesso tooa baseados em Windows máquina:</span><span class="sxs-lookup"><span data-stu-id="aca7a-120">You need access tooa Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="aca7a-121">Execute a ferramenta de validação de certificação hello.</span><span class="sxs-lookup"><span data-stu-id="aca7a-121">Run hello certification validation tool.</span></span>
> * <span data-ttu-id="aca7a-122">Crie URL de assinatura de acesso Olá VHD compartilhado para Olá envio de certificação do VHD.</span><span class="sxs-lookup"><span data-stu-id="aca7a-122">Create hello VHD shared access signature URL for hello VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="aca7a-123">Desenvolver seu VHD</span><span class="sxs-lookup"><span data-stu-id="aca7a-123">Develop your VHD</span></span>
<span data-ttu-id="aca7a-124">Você pode desenvolver VHDs do Azure na nuvem de saudação ou no local:</span><span class="sxs-lookup"><span data-stu-id="aca7a-124">You can develop Azure VHDs in hello cloud or on-premises:</span></span>

* <span data-ttu-id="aca7a-125">Desenvolvimento baseado em nuvem significa que todas as etapas de desenvolvimento são executadas remotamente em um VHD residente no Azure.</span><span class="sxs-lookup"><span data-stu-id="aca7a-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="aca7a-126">O desenvolvimento local requer o download de um VHD e desenvolvê-lo usando a infraestrutura local.</span><span class="sxs-lookup"><span data-stu-id="aca7a-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="aca7a-127">Embora isso seja possível, não é recomendável.</span><span class="sxs-lookup"><span data-stu-id="aca7a-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="aca7a-128">Observe que o desenvolvimento do Windows ou SQL local exige você toohave as chaves de licença do hello relevantes no local.</span><span class="sxs-lookup"><span data-stu-id="aca7a-128">Note that developing for Windows or SQL on-premises requires you toohave hello relevant on-premises license keys.</span></span> <span data-ttu-id="aca7a-129">Você não pode incluir ou instalar o SQL Server depois de criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="aca7a-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="aca7a-130">Você também deve basear sua oferta em uma imagem do SQL aprovada de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aca7a-130">You must also base your offer on an approved SQL image from hello Azure portal.</span></span> <span data-ttu-id="aca7a-131">Se você decidir toodevelop local, você deve executar algumas etapas diferente se você estivesse desenvolvendo na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="aca7a-131">If you decide toodevelop on-premises, you must perform some steps differently than if you were developing in hello cloud.</span></span> <span data-ttu-id="aca7a-132">Você pode encontrar informações relevantes em [Criar uma imagem de VM local](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="aca7a-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
