---
title: "Configurar a origem e o destino para replicação de servidor físico para Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas para definir as configurações de origem e destino para replicação de servidores físicos para armazenamento do Azure com o serviço do Azure Site Recovery"
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
ms.openlocfilehash: e89bbf5a2c1d71852e49da43d3106a05ebfc28a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-the-source-and-target-for-physical-server-replication-to-azure"></a><span data-ttu-id="7a534-103">Etapa 7: Configurar a origem e o destino para replicação de servidor físico para Azure</span><span class="sxs-lookup"><span data-stu-id="7a534-103">Step 7: Set up the source and target for physical server replication to Azure</span></span>

<span data-ttu-id="7a534-104">Este artigo descreve como definir as configurações de origem e destino ao replicar servidores físicos locais para Azure utilizando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a534-104">This article describes how to configure source and target settings when replicating on-premises physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="7a534-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7a534-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="7a534-106">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="7a534-106">Set up the source environment</span></span>

<span data-ttu-id="7a534-107">Configure o servidor de configuração, registre-o no cofre e descubra computadores.</span><span class="sxs-lookup"><span data-stu-id="7a534-107">Set up the configuration server, register it in the vault, and discover machines.</span></span>

1. <span data-ttu-id="7a534-108">Clique em **Site Recovery** > **Etapa 1: preparar a infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="7a534-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="7a534-109">Se não tiver um servidor de configuração, clique em **+Servidor de configuração**.</span><span class="sxs-lookup"><span data-stu-id="7a534-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="7a534-110">Em **Adicionar Servidor**, verifique se **Servidor de Configuração** aparece em **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="7a534-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="7a534-111">Baixe o arquivo de instalação Configuração Unificada da Recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="7a534-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="7a534-112">Baixe a chave do registro do cofre.</span><span class="sxs-lookup"><span data-stu-id="7a534-112">Download the vault registration key.</span></span> <span data-ttu-id="7a534-113">Você precisará dela quando executar a Configuração Unificada.</span><span class="sxs-lookup"><span data-stu-id="7a534-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="7a534-114">A chave é válida por cinco dias após ser gerada.</span><span class="sxs-lookup"><span data-stu-id="7a534-114">The key is valid for five days after you generate it.</span></span>

   ![Configurar origem](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="7a534-116">Registrar o servidor de configuração no cofre</span><span class="sxs-lookup"><span data-stu-id="7a534-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="7a534-117">Faça o descrito a seguir antes de começar, então execute a Configuração Unificada para instalar o servidor de configuração, o servidor de processo e o servidor de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="7a534-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span> <span data-ttu-id="7a534-118">O vídeo descreve a configuração dos componentes para VM do VMware para replicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a534-118">The video describes setting up the components for VMware VM to Azure replication.</span></span> <span data-ttu-id="7a534-119">No entanto, o mesmo processo é válido ao servidor físico para replicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a534-119">However, the same process is valid for physical server to Azure replication.</span></span>

- <span data-ttu-id="7a534-120">Na VM do servidor de configuração, certifique-se de que o relógio do sistema esteja sincronizado com um [Servidor de Horário](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="7a534-120">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="7a534-121">Ele deve ser correspondente.</span><span class="sxs-lookup"><span data-stu-id="7a534-121">It should match.</span></span> <span data-ttu-id="7a534-122">Se ele estiver 15 minutos adiantado ou atrasado, a instalação poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="7a534-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="7a534-123">Execute a instalação como um Administrador Local na máquina do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="7a534-123">Run setup as a Local Administrator on the configuration server machine.</span></span>
- <span data-ttu-id="7a534-124">Verifique se TLS 1.0 está habilitado na VM.</span><span class="sxs-lookup"><span data-stu-id="7a534-124">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="7a534-125">O servidor de configuração também pode ser instalado [da linha de comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="7a534-125">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-the-target-environment"></a><span data-ttu-id="7a534-126">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="7a534-126">Set up the target environment</span></span>

<span data-ttu-id="7a534-127">Antes de configurar o ambiente de destino, certifique-se de ter uma conta de armazenamento do Azure e uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="7a534-127">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="7a534-128">Clique em **Preparar infraestrutura** > **Destino** e selecione a assinatura do Azure que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="7a534-128">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="7a534-129">Especifique se o seu modelo de implantação de destino é baseada no Gerenciador de Recursos ou clássico.</span><span class="sxs-lookup"><span data-stu-id="7a534-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="7a534-130">A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.</span><span class="sxs-lookup"><span data-stu-id="7a534-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destino](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="7a534-132">Se não tiver criado uma conta de armazenamento ou de rede, clique em **+Conta de armazenamento** ou **+Rede** para criar uma conta do Gerenciador de Recursos ou embutida de rede.</span><span class="sxs-lookup"><span data-stu-id="7a534-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a534-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a534-133">Next steps</span></span>

<span data-ttu-id="7a534-134">Vá para [Etapa 8: Configurar uma política de replicação](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="7a534-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
