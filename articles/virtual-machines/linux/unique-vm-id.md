---
title: Obter uma ID de VM em Linux do Azure | Microsoft Docs
description: Descreve como obter e usar uma ID Exclusiva de VM Linux do Azure.
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
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="3d6c0-103">Acessando e usando a ID exclusiva da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="3d6c0-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="3d6c0-104">A ID exclusiva da VM do Azure é um identificador de 128 bits codificado e armazenado em todos os SMBIOS da VM IaaS do Azure e, atualmente, pode ser lida usando comandos BIOS da plataforma.</span><span class="sxs-lookup"><span data-stu-id="3d6c0-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="3d6c0-105">A ID exclusiva da VM do Azure é uma propriedade somente leitura.</span><span class="sxs-lookup"><span data-stu-id="3d6c0-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="3d6c0-106">A ID exclusiva da VM do Azure não mudará no desligamento para reinicialização (planejado ou não planejado), no início/parada de desalocação, na recuperação de serviço ou na restauração in-loco.</span><span class="sxs-lookup"><span data-stu-id="3d6c0-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="3d6c0-107">No entanto, se a VM for um instantâneo e se for copiada para criar uma nova instância, uma nova ID da VM do Azure será configurada.</span><span class="sxs-lookup"><span data-stu-id="3d6c0-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="3d6c0-108">Se você tiver VMs antigas criadas e em execução desde o lançamento desse novo recurso (18 de setembro de 2014), reinicie sua VM para obter automaticamente uma ID exclusiva do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d6c0-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="3d6c0-109">Para acessar a ID exclusiva da VM do Azure de dentro da VM:</span><span class="sxs-lookup"><span data-stu-id="3d6c0-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="3d6c0-110">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3d6c0-110">Create a VM</span></span>
<span data-ttu-id="3d6c0-111">Para obter mais informações, veja [Criar uma máquina virtual](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3d6c0-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="3d6c0-112">Conectar-se à VM</span><span class="sxs-lookup"><span data-stu-id="3d6c0-112">Connect to the VM</span></span>
<span data-ttu-id="3d6c0-113">Para obter mais informações, veja [SSH no Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3d6c0-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="3d6c0-114">Consultar ID exclusiva da VM</span><span class="sxs-lookup"><span data-stu-id="3d6c0-114">Query VM Unique ID</span></span>
<span data-ttu-id="3d6c0-115">Comando (o exemplo usa o **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="3d6c0-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="3d6c0-116">Exemplo de resultados esperados:</span><span class="sxs-lookup"><span data-stu-id="3d6c0-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="3d6c0-117">Devido à ordenação de bits Big Endian, a ID exclusiva da VM, neste caso, será:</span><span class="sxs-lookup"><span data-stu-id="3d6c0-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="3d6c0-118">A ID exclusiva da VM do Azure poderá ser usada em cenários diferentes se a VM estiver em execução no Azure ou no local, além de poder ajudar com os requisitos de licenciamento, de relatórios ou de rastreamento geral que você tenha em suas implantações IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d6c0-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="3d6c0-119">Muitos fornecedores independentes de software que criam aplicativos e os certificam no Azure podem exigir a identificação de uma VM do Azure durante todo seu ciclo de vida, bem como para informar se a VM está em execução no Azure, no local ou em outros provedores de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3d6c0-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="3d6c0-120">Esse identificador de plataforma pode, por exemplo, ajudar a detectar se o software está licenciado corretamente ou ajudar a correlacionar quaisquer dados da VM com sua fonte, como auxiliar na configuração das métricas certas para a plataforma certa e rastrear e correlacionar essas métricas entre outros usuários.</span><span class="sxs-lookup"><span data-stu-id="3d6c0-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>

