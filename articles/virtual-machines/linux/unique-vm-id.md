---
title: aaaGet uma ID de VM do Linux do Azure | Microsoft Docs
description: Descreve como tooget e use um exclusivo de VM do Linux Azure ID.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="3dbbf-103">Acessando e usando a ID exclusiva da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="3dbbf-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="3dbbf-104">A ID exclusiva da VM do Azure é um identificador de 128 bits codificado e armazenado em todos os SMBIOS da VM IaaS do Azure e, atualmente, pode ser lida usando comandos BIOS da plataforma.</span><span class="sxs-lookup"><span data-stu-id="3dbbf-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="3dbbf-105">A ID exclusiva da VM do Azure é uma propriedade somente leitura.</span><span class="sxs-lookup"><span data-stu-id="3dbbf-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="3dbbf-106">A ID exclusiva da VM do Azure não mudará no desligamento para reinicialização (planejado ou não planejado), no início/parada de desalocação, na recuperação de serviço ou na restauração in-loco.</span><span class="sxs-lookup"><span data-stu-id="3dbbf-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="3dbbf-107">No entanto, se Olá VM for um instantâneo e copiado toocreate uma nova instância, nova ID de VM do Azure está configurado.</span><span class="sxs-lookup"><span data-stu-id="3dbbf-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="3dbbf-108">Se você tiver máquinas virtuais mais antigas criadas e, em execução desde que este novo recurso foi distribuído (18 de setembro de 2014), reinicie a VM tooautomatically obter uma ID exclusiva do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dbbf-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="3dbbf-109">tooaccess ID exclusiva de VM do Azure de dentro de saudação VM:</span><span class="sxs-lookup"><span data-stu-id="3dbbf-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="3dbbf-110">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3dbbf-110">Create a VM</span></span>
<span data-ttu-id="3dbbf-111">Para obter mais informações, veja [Criar uma máquina virtual](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3dbbf-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="3dbbf-112">Conecte-se toohello VM</span><span class="sxs-lookup"><span data-stu-id="3dbbf-112">Connect toohello VM</span></span>
<span data-ttu-id="3dbbf-113">Para obter mais informações, veja [SSH no Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3dbbf-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="3dbbf-114">Consultar ID exclusiva da VM</span><span class="sxs-lookup"><span data-stu-id="3dbbf-114">Query VM Unique ID</span></span>
<span data-ttu-id="3dbbf-115">Comando (o exemplo usa o **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="3dbbf-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="3dbbf-116">Exemplo de resultados esperados:</span><span class="sxs-lookup"><span data-stu-id="3dbbf-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="3dbbf-117">Devido a tooBig bit Endian ordenação, hello real ID exclusiva da VM nesse caso será:</span><span class="sxs-lookup"><span data-stu-id="3dbbf-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="3dbbf-118">ID exclusiva de VM do Azure pode ser usada em cenários diferentes se hello VM está em execução no Azure ou no local e pode ajudar a seus requisitos de controle geral licenciamento ou relatório que você pode ter suas implantações de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dbbf-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="3dbbf-119">Muitos fornecedores independentes de software criar aplicativos e certifica-los no Azure podem exigir tooidentify uma VM do Azure ao longo de seu ciclo de vida e tootell se Olá VM estiver em execução no Azure, local ou em outros provedores de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dbbf-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="3dbbf-120">Esse identificador de plataforma por exemplo pode ajudar a detectar se o software de saudação é licenciado corretamente ou ajudar toocorrelate qualquer fonte de tooits de dados VM como tooassist sobre a configuração de métricas de direito Olá para plataforma hello e tootrack e correlacionar essas métricas entre outros usos.</span><span class="sxs-lookup"><span data-stu-id="3dbbf-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

