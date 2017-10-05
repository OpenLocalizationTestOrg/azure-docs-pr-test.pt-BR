---
title: "Instalar o Serviço de mobilidade para a replicação de VMware para o Azure | Microsoft Docs"
description: "Este artigo descreve como instalar o agente do Serviço de mobilidade para replicação do VMware para o Azure com o serviço Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bc520bd2ea54208889861a7a3b275e3008a05d53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="905d2-103">Etapa 10: instalar o Serviço de mobilidade manualmente</span><span class="sxs-lookup"><span data-stu-id="905d2-103">Step 10: Install the Mobility service</span></span>


<span data-ttu-id="905d2-104">Este artigo descreve como definir as configurações de origem e destino ao replicar máquinas virtuais VMware locais para Azure utilizando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="905d2-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="905d2-105">O Serviço de mobilidade captura gravações de dados em um computador e as encaminha para o servidor em processo.</span><span class="sxs-lookup"><span data-stu-id="905d2-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="905d2-106">Ele deve ser instalado em cada computador que você deseja replicar para o Azure.</span><span class="sxs-lookup"><span data-stu-id="905d2-106">It should be installed on each machine that you want to replicate to Azure.</span></span>

<span data-ttu-id="905d2-107">Instale o Serviço de mobilidade manualmente usando uma instalação por push por meio do servidor em processo do Site Recovery quando a replicação for habilitada, ou use uma ferramenta do System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="905d2-107">You can install the Mobility service manual, using a push installation from the Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="905d2-108">Se você usar a instalação por push, o serviço será instalado na VM quando a replicação for habilitada.</span><span class="sxs-lookup"><span data-stu-id="905d2-108">If you use push installation, the service is installed on the VM when replication is enabled.</span></span>

<span data-ttu-id="905d2-109">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="905d2-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="905d2-110">Instalar manualmente</span><span class="sxs-lookup"><span data-stu-id="905d2-110">Install manually</span></span>

1. <span data-ttu-id="905d2-111">Verifique os [pré-requisitos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para instalação manual.</span><span class="sxs-lookup"><span data-stu-id="905d2-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="905d2-112">Siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para a instalação manual usando o portal.</span><span class="sxs-lookup"><span data-stu-id="905d2-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="905d2-113">Se preferir instalar por meio da linha de comando, siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="905d2-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="905d2-114">Instalar por meio do servidor em processo</span><span class="sxs-lookup"><span data-stu-id="905d2-114">Install from the process server</span></span>

<span data-ttu-id="905d2-115">Se você desejar enviar a instalação do Serviço de mobilidade por push por meio do servidor em processo quando habilitar a replicação em uma VM, precisará de uma conta que pode ser usada pelo servidor em processo para acessar a VM.</span><span class="sxs-lookup"><span data-stu-id="905d2-115">If you want to push the Mobility service installation from the process server when you enable replication for a VM, you need an account that can be used by the process server to access the VM.</span></span> <span data-ttu-id="905d2-116">A conta é usada apenas para a instalação por push.</span><span class="sxs-lookup"><span data-stu-id="905d2-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="905d2-117">Você deve ter [criado uma conta](vmware-walkthrough-prepare-vmware.md) que pode ser usado para a instalação por push.</span><span class="sxs-lookup"><span data-stu-id="905d2-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="905d2-118">Em seguida, especifique a conta que você deseja usar ao definir as configurações de origem durante a implantação do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="905d2-118">You then specify the account you want to use when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="905d2-119">Em seguida, siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se desejar enviar o Serviço de mobilidade por push para VMs que executam o Windows ou o Linux.</span><span class="sxs-lookup"><span data-stu-id="905d2-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="905d2-120">Outros métodos</span><span class="sxs-lookup"><span data-stu-id="905d2-120">Other methods</span></span>

<span data-ttu-id="905d2-121">Saiba mais sobre como [instalar o Serviço de mobilidade usando o Configuration Manager](site-recovery-install-mobility-service-using-sccm.md) ou usando [DSC de Automação do Azure](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="905d2-121">Learn more about [installing the Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="905d2-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="905d2-122">Next steps</span></span>

<span data-ttu-id="905d2-123">Vá para a [Etapa 11: Habilitar a replicação](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="905d2-123">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
