---
title: "aaaUsing SAP em máquinas virtuais do Linux | Microsoft Docs"
description: "Saiba como usar o SAP em VMs (máquinas virtuais) do Linux no Microsoft Azure"
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: fd4aad83d99ef5286488aaab6552fd67a5e35a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="dbb63-103">Usando o SAP em máquinas virtuais do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="dbb63-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="dbb63-104">Computação em nuvem é um termo amplamente usado que está adquirindo cada vez mais importância no hello setor de TI de empresas de pequenas porte a empresas toolarge e multinacional.</span><span class="sxs-lookup"><span data-stu-id="dbb63-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="dbb63-105">Microsoft Azure é hello plataforma de serviços de nuvem da Microsoft que oferece uma ampla variedade de novas possibilidades.</span><span class="sxs-lookup"><span data-stu-id="dbb63-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="dbb63-106">Agora, os clientes estão toorapidly capaz de provisionar e provisionamento de aplicativos como serviços de nuvem, para que eles não são limitado tootechnical ou restrições de orçamentos.</span><span class="sxs-lookup"><span data-stu-id="dbb63-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="dbb63-107">Em vez de investir tempo e dinheiro na infraestrutura de hardware, as empresas podem concentrar no aplicativo hello, processos de negócios e seus benefícios para os clientes e usuários.</span><span class="sxs-lookup"><span data-stu-id="dbb63-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="dbb63-108">Com as máquinas virtuais do Microsoft Azure, a Microsoft oferece uma plataforma abrangente de IaaS (Infraestrutura como Serviço).</span><span class="sxs-lookup"><span data-stu-id="dbb63-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="dbb63-109">Os aplicativos baseados no SAP NetWeaver têm suporte em Máquinas Virtuais do Azure (IaaS).</span><span class="sxs-lookup"><span data-stu-id="dbb63-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="dbb63-110">Olá white papers abaixo descrevem como tooplan e implementar SAP NetWeaver com base em aplicativos em máquinas virtuais do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb63-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="dbb63-111">Você também pode implementar aplicativos baseados no SAP NetWeaver em [máquinas virtuais do Windows](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dbb63-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="dbb63-112">SAP NetWeaver em máquinas virtuais SUSE Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="dbb63-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="dbb63-113">título: aaaTesting SAP NetWeaver nas máquinas virtuais do Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="dbb63-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="dbb63-114">Resumo: no momento, não há suporte oficial do SAP para execução do SAP NetWeaver em VMs Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb63-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="dbb63-115">Mesmo assim, os clientes poderão toodo alguns testes ou considere toorun sistemas de treinamento ou demonstração SAP em VMs do Linux do Azure como não há necessidade de contatar o suporte do SAP.</span><span class="sxs-lookup"><span data-stu-id="dbb63-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="dbb63-116">Este artigo deve ajudar a configurar as VMs do Azure SUSE Linux para executar o SAP e fornece algumas dicas básicas em ordem tooavoid possíveis armadilhas comuns.</span><span class="sxs-lookup"><span data-stu-id="dbb63-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="dbb63-117">Atualização: dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="dbb63-117">Updated: December 2015</span></span>

[<span data-ttu-id="dbb63-118">Esse artigo pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="dbb63-118">This article can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

