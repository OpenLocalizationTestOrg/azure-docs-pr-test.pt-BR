---
title: "Olá aaaInstall serviço de mobilidade de replicação do VMware tooAzure | Microsoft Docs"
description: "Este artigo descreve como tooinstall Olá agente de serviço de mobilidade para VMware tooAzure replicação com o serviço do Azure Site Recovery hello."
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
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="23372-103">Etapa 10: Instalar o serviço de mobilidade Olá</span><span class="sxs-lookup"><span data-stu-id="23372-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="23372-104">Este artigo descreve como tooconfigure configurações de origem e de destino durante a replicação local tooAzure de máquinas virtuais VMware, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="23372-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="23372-105">Olá serviço de mobilidade captura gravações de dados em um computador e as encaminha toohello servidor de processo.</span><span class="sxs-lookup"><span data-stu-id="23372-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="23372-106">Ele deve ser instalado em cada computador que você deseja tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="23372-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="23372-107">Você pode instalar o manual de serviço de mobilidade hello, usando uma instalação por push do servidor de processo de recuperação de Site hello quando a replicação é habilitada, ou usar uma ferramenta do System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="23372-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="23372-108">Se você usar a instalação por push, o serviço de saudação está instalado na VM de saudação quando a replicação está habilitada.</span><span class="sxs-lookup"><span data-stu-id="23372-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="23372-109">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="23372-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="23372-110">Instalar manualmente</span><span class="sxs-lookup"><span data-stu-id="23372-110">Install manually</span></span>

1. <span data-ttu-id="23372-111">Verificar Olá [pré-requisitos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para instalação manual.</span><span class="sxs-lookup"><span data-stu-id="23372-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="23372-112">Execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para instalação manual usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="23372-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="23372-113">Se você preferir tooinstall da linha de comando hello, execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="23372-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="23372-114">Instalar saudação do servidor de processo</span><span class="sxs-lookup"><span data-stu-id="23372-114">Install from hello process server</span></span>

<span data-ttu-id="23372-115">Se você quiser toopush instalação de serviço de mobilidade Olá saudação do servidor de processo quando você habilita a replicação para uma máquina virtual, você precisa de uma conta que pode ser usada por tooaccess do servidor de processo Olá Olá VM.</span><span class="sxs-lookup"><span data-stu-id="23372-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="23372-116">Olá conta só é usada para a instalação por push hello.</span><span class="sxs-lookup"><span data-stu-id="23372-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="23372-117">Você deve ter [criado uma conta](vmware-walkthrough-prepare-vmware.md) que pode ser usado para a instalação por push.</span><span class="sxs-lookup"><span data-stu-id="23372-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="23372-118">Você especificar conta Olá que desejar toouse quando você definir configurações de origem durante a implantação da recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="23372-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="23372-119">Em seguida, execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se desejar que o serviço de mobilidade Olá toopush em VMs que executam o Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="23372-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="23372-120">Outros métodos</span><span class="sxs-lookup"><span data-stu-id="23372-120">Other methods</span></span>

<span data-ttu-id="23372-121">Saiba mais sobre [instalando usando o Gerenciador de configuração de serviço de mobilidade Olá](site-recovery-install-mobility-service-using-sccm.md), ou usando [DSC de automação do Azure](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="23372-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23372-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23372-122">Next steps</span></span>

<span data-ttu-id="23372-123">Vá muito[etapa 11: habilitar a replicação](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="23372-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
