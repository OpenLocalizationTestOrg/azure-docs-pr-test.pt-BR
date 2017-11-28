---
title: "Usando o SAP em máquinas virtuais do Linux | Microsoft Docs"
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
ms.openlocfilehash: 078865245989578d17b6eb0b59b379aa2056f31c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="48689-103">Usando o SAP em máquinas virtuais do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="48689-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="48689-104">Computação em Nuvem é um termo amplamente usado que está adquirindo cada vez mais importância no setor de TI, de pequenas empresas até multinacionais e grandes corporações.</span><span class="sxs-lookup"><span data-stu-id="48689-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="48689-105">O Microsoft Azure é a Plataforma de Serviços de Nuvem da Microsoft que oferece um amplo espectro de novas possibilidades.</span><span class="sxs-lookup"><span data-stu-id="48689-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="48689-106">Agora, os clientes podem provisionar e desprovisionar com rapidez os aplicativos como Serviços de Nuvem, para que não sejam limitados por restrições técnicas ou orçamentárias.</span><span class="sxs-lookup"><span data-stu-id="48689-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="48689-107">Em vez de investir tempo e dinheiro na infraestrutura de hardware, as empresas podem se concentrar no aplicativo, nos processos de negócios e em seus benefícios para clientes e usuários.</span><span class="sxs-lookup"><span data-stu-id="48689-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="48689-108">Com as máquinas virtuais do Microsoft Azure, a Microsoft oferece uma plataforma abrangente de IaaS (Infraestrutura como Serviço).</span><span class="sxs-lookup"><span data-stu-id="48689-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="48689-109">Os aplicativos baseados no SAP NetWeaver têm suporte em Máquinas Virtuais do Azure (IaaS).</span><span class="sxs-lookup"><span data-stu-id="48689-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="48689-110">Os white papers abaixo descrevem como planejar e implementar aplicativos baseados no SAP NetWeaver em máquinas virtuais do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="48689-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="48689-111">Você também pode implementar aplicativos baseados no SAP NetWeaver em [máquinas virtuais do Windows](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48689-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="48689-112">SAP NetWeaver em máquinas virtuais SUSE Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="48689-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="48689-113">Título: Testando o SAP NetWeaver em VMs SUSE Linux no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="48689-113">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="48689-114">Resumo: no momento, não há suporte oficial do SAP para execução do SAP NetWeaver em VMs Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="48689-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="48689-115">Independentemente, talvez os clientes queiram fazer alguns testes ou considerem a execução de sistemas de treinamento ou de demonstração SAP em VMs Linux do Azure, já que não há a necessidade de contatar o suporte SAP.</span><span class="sxs-lookup"><span data-stu-id="48689-115">Nevertheless customers might want to do some testing or might consider to run SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="48689-116">Este artigo deve ajudar a configurar as VMs SUSE Linux do Azure para execução de SAP e fornece algumas dicas básicas para evitar possíveis armadilhas comuns.</span><span class="sxs-lookup"><span data-stu-id="48689-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order to avoid common potential pitfalls.</span></span>

<span data-ttu-id="48689-117">Atualização: dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="48689-117">Updated: December 2015</span></span>

[<span data-ttu-id="48689-118">Esse artigo pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="48689-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

