---
title: "Instalar o Serviço de mobilidade para a replicação de servidor físico para o Azure | Microsoft Docs"
description: "Este artigo descreve como instalar o agente do Serviço de mobilidade em servidores físicos que são replicados para o Azure com o serviço Azure Site Recovery."
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
ms.openlocfilehash: d73267d7a64221a3138af19e9a2d5dd15809b927
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="609d6-103">Etapa 9: instalar o Serviço de mobilidade manualmente</span><span class="sxs-lookup"><span data-stu-id="609d6-103">Step 9: Install the Mobility service</span></span>


<span data-ttu-id="609d6-104">Este artigo descreve como instalar o componente do Serviço de mobilidade durante a replicação de servidores físicos Windows/Linux locais para o Azure, usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="609d6-104">This article describes how to install the Mobility service component when replicating on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="609d6-105">O Serviço de mobilidade captura gravações de dados em um computador e as encaminha para o servidor em processo.</span><span class="sxs-lookup"><span data-stu-id="609d6-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="609d6-106">Ele deve ser instalado em cada servidor que você deseja replicar para o Azure.</span><span class="sxs-lookup"><span data-stu-id="609d6-106">It should be installed on each server that you want to replicate to Azure.</span></span>

<span data-ttu-id="609d6-107">Instale o Serviço de mobilidade manualmente, usando uma instalação por push por meio do servidor em processo do Site Recovery quando a replicação for habilitada ou usando uma ferramenta como o System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="609d6-107">You can install the Mobility service manually, or using a push installation from the Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="609d6-108">Se você usar a instalação por push, o serviço será instalado no servidor quando você habilitar a replicação.</span><span class="sxs-lookup"><span data-stu-id="609d6-108">If you use push installation, the service is installed on the server when you enable replication.</span></span>

<span data-ttu-id="609d6-109">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="609d6-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="609d6-110">Instalar manualmente</span><span class="sxs-lookup"><span data-stu-id="609d6-110">Install manually</span></span>

1. <span data-ttu-id="609d6-111">Verifique os [pré-requisitos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para instalação manual.</span><span class="sxs-lookup"><span data-stu-id="609d6-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="609d6-112">Siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para a instalação manual usando o portal.</span><span class="sxs-lookup"><span data-stu-id="609d6-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="609d6-113">Se preferir instalar por meio da linha de comando, siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="609d6-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="609d6-114">Instalar por meio do servidor em processo</span><span class="sxs-lookup"><span data-stu-id="609d6-114">Install from the process server</span></span>

<span data-ttu-id="609d6-115">Se você desejar enviar a instalação do Serviço de mobilidade por push por meio do servidor em processo quando habilitar a replicação em um computador, precisará de uma conta que pode ser usada pelo servidor em processo para acessar o computador.</span><span class="sxs-lookup"><span data-stu-id="609d6-115">If you want to push the Mobility service installation from the process server when you enable replication for a machine, you need an account that can be used by the process server to access the machine.</span></span> <span data-ttu-id="609d6-116">A conta é usada apenas para a instalação por push.</span><span class="sxs-lookup"><span data-stu-id="609d6-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="609d6-117">Se você não tiver criado uma conta, faça isso usando estas diretrizes:</span><span class="sxs-lookup"><span data-stu-id="609d6-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="609d6-118">Você pode usar uma conta local ou de domínio</span><span class="sxs-lookup"><span data-stu-id="609d6-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="609d6-119">Para Windows, se não estiver usando uma conta de domínio, precisará desabilitar o controle de Acesso de Usuário Remoto no computador local.</span><span class="sxs-lookup"><span data-stu-id="609d6-119">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="609d6-120">Para fazer isso, no registro, em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicione a entrada DWORD **LocalAccountTokenFilterPolicy** com um valor de 1.</span><span class="sxs-lookup"><span data-stu-id="609d6-120">To do this, in the register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="609d6-121">Se desejar adicionar a entrada do Registro do Windows por meio de uma CLI, digite:</span><span class="sxs-lookup"><span data-stu-id="609d6-121">If you want to add the registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="609d6-122">Para Linux, a conta deve ser a raiz no servidor Linux de origem.</span><span class="sxs-lookup"><span data-stu-id="609d6-122">For Linux, the account should be root on the source Linux server.</span></span>

2. <span data-ttu-id="609d6-123">Em seguida, siga [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se desejar enviar o Serviço de mobilidade por push para VMs que executam o Windows ou o Linux.</span><span class="sxs-lookup"><span data-stu-id="609d6-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="609d6-124">Outros métodos de instalação</span><span class="sxs-lookup"><span data-stu-id="609d6-124">Other installation methods</span></span>

- <span data-ttu-id="609d6-125">[Saiba mais sobre](site-recovery-install-mobility-service-using-sccm.md) como instalar o Serviço de mobilidade usando o Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="609d6-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing the Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="609d6-126">[Saiba mais sobre](site-recovery-automate-mobility-service-install.md) como instalar com o DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="609d6-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="609d6-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="609d6-127">Next steps</span></span>

<span data-ttu-id="609d6-128">Acesse a [Etapa 10: Habilitar a replicação](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="609d6-128">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
