---
title: "aaaSet a origem de saudação e de destino para tooAzure de replicação de servidor físico com o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá etapas tooset as configurações de origem e destino de replicação de armazenamento de tooAzure servidores físicos com hello serviço Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="a6bf3-103">Etapa 7: Configurar a origem de saudação e de destino para tooAzure de replicação de servidor físico</span><span class="sxs-lookup"><span data-stu-id="a6bf3-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="a6bf3-104">Este artigo descreve como tooconfigure configurações de origem e de destino durante a replicação local tooAzure de servidores físicos, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="a6bf3-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a6bf3-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="a6bf3-106">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="a6bf3-106">Set up hello source environment</span></span>

<span data-ttu-id="a6bf3-107">Configurar o servidor de configuração de hello, registrá-lo no cofre hello e descobrir máquinas.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="a6bf3-108">Clique em **Site Recovery** > **Etapa 1: preparar a infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="a6bf3-109">Se não tiver um servidor de configuração, clique em **+Servidor de configuração**.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="a6bf3-110">Em **Adicionar Servidor**, verifique se **Servidor de Configuração** aparece em **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="a6bf3-111">Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="a6bf3-112">Baixe a chave de registro de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-112">Download hello vault registration key.</span></span> <span data-ttu-id="a6bf3-113">Você precisará dela quando executar a Configuração Unificada.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="a6bf3-114">chave de saudação é válida por cinco dias depois que ele é gerado.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-114">hello key is valid for five days after you generate it.</span></span>

   ![Configurar origem](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="a6bf3-116">Registrar o servidor de configuração de saudação no cofre Olá</span><span class="sxs-lookup"><span data-stu-id="a6bf3-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="a6bf3-117">Seguinte Olá antes de iniciar, em seguida executar instalação unificado tooinstall Olá configuração server, Olá processo server e o servidor de destino mestre hello.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="a6bf3-118">Olá vídeo descreve como configurar componentes Olá para replicação de tooAzure de VM do VMware.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="a6bf3-119">No entanto, hello mesmo processo é válido para a replicação tooAzure servidor físico.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="a6bf3-120">No servidor de configuração de saudação VM, certifique-se de que o relógio do sistema hello está sincronizado com um [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="a6bf3-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="a6bf3-121">Ele deve ser correspondente.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-121">It should match.</span></span> <span data-ttu-id="a6bf3-122">Se ele estiver 15 minutos adiantado ou atrasado, a instalação poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="a6bf3-123">Execute a instalação como um administrador Local no computador do servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="a6bf3-124">Certifique-se de que TLS 1.0 está ativado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="a6bf3-125">também pode ser instalado o servidor de configuração de saudação [da linha de comando Olá](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="a6bf3-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="a6bf3-126">Configurar o ambiente de destino Olá</span><span class="sxs-lookup"><span data-stu-id="a6bf3-126">Set up hello target environment</span></span>

<span data-ttu-id="a6bf3-127">Antes de configurar o ambiente de destino hello, verifique se que você tem uma conta de armazenamento do Azure e a configuração da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="a6bf3-128">Clique em **preparar infraestrutura** > **destino**, e selecione Olá assinatura do Azure que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="a6bf3-129">Especifique se o seu modelo de implantação de destino é baseada no Gerenciador de Recursos ou clássico.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="a6bf3-130">A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destino](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="a6bf3-132">Se você não tiver criado uma conta de armazenamento ou de rede, clique em **+ conta de armazenamento** ou **+ rede**, toocreate embutido de rede ou a conta de um Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6bf3-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6bf3-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6bf3-133">Next steps</span></span>

<span data-ttu-id="a6bf3-134">Vá muito[etapa 8: configurar uma política de replicação](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="a6bf3-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
