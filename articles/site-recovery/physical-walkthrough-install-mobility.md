---
title: "Olá aaaInstall serviço de mobilidade de replicação do servidor físico tooAzure | Microsoft Docs"
description: "Este artigo descreve como tooinstall Olá agente de serviço de mobilidade em servidores físicos replicando tooAzure com o serviço do Azure Site Recovery hello."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="5961c-103">Etapa 9: Instale o serviço de mobilidade Olá</span><span class="sxs-lookup"><span data-stu-id="5961c-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="5961c-104">Este artigo descreve como tooinstall o componente de serviço Olá mobilidade durante a replicação local tooAzure de servidores físicos do Windows/Linux, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5961c-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="5961c-105">Olá serviço de mobilidade captura gravações de dados em um computador e as encaminha toohello servidor de processo.</span><span class="sxs-lookup"><span data-stu-id="5961c-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="5961c-106">Ele deve ser instalado em cada servidor que você deseja tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5961c-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="5961c-107">Você pode instalar o serviço de mobilidade Olá manualmente ou recuperação de Site usando uma instalação por push de saudação processar servidor quando a replicação é habilitada, ou usando uma ferramenta como o System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="5961c-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="5961c-108">Se você usar a instalação por push, o serviço de saudação está instalado no servidor de saudação quando você habilitar a replicação.</span><span class="sxs-lookup"><span data-stu-id="5961c-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="5961c-109">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5961c-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="5961c-110">Instalar manualmente</span><span class="sxs-lookup"><span data-stu-id="5961c-110">Install manually</span></span>

1. <span data-ttu-id="5961c-111">Verificar Olá [pré-requisitos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para instalação manual.</span><span class="sxs-lookup"><span data-stu-id="5961c-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="5961c-112">Execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para instalação manual usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="5961c-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="5961c-113">Se você preferir tooinstall da linha de comando hello, execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="5961c-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="5961c-114">Instalar saudação do servidor de processo</span><span class="sxs-lookup"><span data-stu-id="5961c-114">Install from hello process server</span></span>

<span data-ttu-id="5961c-115">Olá toopush instalação do serviço de mobilidade saudação do servidor de processo quando você habilitar a replicação para uma máquina, é necessário uma conta que pode ser usada por máquina de saudação tooaccess do servidor de processo hello.</span><span class="sxs-lookup"><span data-stu-id="5961c-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="5961c-116">Olá conta só é usada para a instalação por push hello.</span><span class="sxs-lookup"><span data-stu-id="5961c-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="5961c-117">Se você não tiver criado uma conta, faça isso usando estas diretrizes:</span><span class="sxs-lookup"><span data-stu-id="5961c-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="5961c-118">Você pode usar uma conta local ou de domínio</span><span class="sxs-lookup"><span data-stu-id="5961c-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="5961c-119">Para Windows, se você não estiver usando uma conta de domínio, você precisa toodisable controle de acesso de usuário remoto na máquina local hello.</span><span class="sxs-lookup"><span data-stu-id="5961c-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="5961c-120">toodo, Olá registrar em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar entrada DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1.</span><span class="sxs-lookup"><span data-stu-id="5961c-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="5961c-121">Entrada de registro tooadd Olá para Windows de uma CLI, digite:</span><span class="sxs-lookup"><span data-stu-id="5961c-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="5961c-122">Para o Linux, a conta de Olá deve ser raiz no servidor do hello origem Linux.</span><span class="sxs-lookup"><span data-stu-id="5961c-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="5961c-123">Em seguida, execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se desejar que o serviço de mobilidade Olá toopush em VMs que executam o Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="5961c-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="5961c-124">Outros métodos de instalação</span><span class="sxs-lookup"><span data-stu-id="5961c-124">Other installation methods</span></span>

- <span data-ttu-id="5961c-125">[Saiba mais sobre](site-recovery-install-mobility-service-using-sccm.md) instalando serviço de mobilidade hello usando o Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="5961c-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="5961c-126">[Saiba mais sobre](site-recovery-automate-mobility-service-install.md) como instalar com o DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5961c-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5961c-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5961c-127">Next steps</span></span>

<span data-ttu-id="5961c-128">Vá muito[etapa 10: habilitar a replicação](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="5961c-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
