---
title: "taxa de transferência de rede VM aaaOptimize | Microsoft Docs"
description: "Saiba como taxa de transferência da rede toooptimize máquina virtual do Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="ce783-103">Otimizar a taxa de transferência de rede para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="ce783-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="ce783-104">Máquinas virtuais do Azure (VM) têm configurações de rede padrão que podem ser mais otimizadas para taxa de transferência de rede.</span><span class="sxs-lookup"><span data-stu-id="ce783-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="ce783-105">Este artigo descreve como toooptimize rede taxa de transferência do Microsoft Azure Windows e VMs do Linux, incluindo os principais distribuições como Ubuntu, CentOS e Red Hat.</span><span class="sxs-lookup"><span data-stu-id="ce783-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="ce783-106">VM Windows</span><span class="sxs-lookup"><span data-stu-id="ce783-106">Windows VM</span></span>

<span data-ttu-id="ce783-107">Se sua VM do Windows tem suporte com [acelerado rede](virtual-network-create-vm-accelerated-networking.md), habilitar esse recurso seria uma configuração ideal Olá para taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="ce783-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="ce783-108">Para todas as outras VMs do Windows, usar RSS (Receive Side Scaling) pode alcançar uma taxa de transferência máxima maior que uma VM sem RSS.</span><span class="sxs-lookup"><span data-stu-id="ce783-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="ce783-109">RSS pode ser desabilitado por padrão em uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="ce783-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="ce783-110">Concluir hello toodetermine as etapas a seguir se o RSS está habilitado e tooenable se ele está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="ce783-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="ce783-111">Digite hello `Get-NetAdapterRss` toosee de comando do PowerShell se o RSS está habilitado para um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="ce783-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="ce783-112">Em Olá seguir o exemplo de saída retornados de saudação `Get-NetAdapterRss`, RSS não está habilitado.</span><span class="sxs-lookup"><span data-stu-id="ce783-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="ce783-113">Digite hello tooenable comando RSS a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce783-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="ce783-114">o comando anterior Olá não tem uma saída.</span><span class="sxs-lookup"><span data-stu-id="ce783-114">hello previous command does not have an output.</span></span> <span data-ttu-id="ce783-115">comando Olá alterado as configurações de NIC, causando a perda de conectividade temporário para aproximadamente um minuto.</span><span class="sxs-lookup"><span data-stu-id="ce783-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="ce783-116">Aparece uma caixa de diálogo Reconnecting durante a perda de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce783-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="ce783-117">Normalmente, a conectividade for restaurada após a tentativa de terceiro hello.</span><span class="sxs-lookup"><span data-stu-id="ce783-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="ce783-118">Confirme se o RSS está habilitado no hello VM inserindo Olá `Get-NetAdapterRss` comando novamente.</span><span class="sxs-lookup"><span data-stu-id="ce783-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="ce783-119">Se for bem-sucedido, Olá saída de exemplo a seguir será retornada:</span><span class="sxs-lookup"><span data-stu-id="ce783-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="ce783-120">VM Linux</span><span class="sxs-lookup"><span data-stu-id="ce783-120">Linux VM</span></span>

<span data-ttu-id="ce783-121">RSS está sempre habilitado por padrão em uma VM do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce783-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="ce783-122">Kernels Linux lançados desde janeiro de 2017 incluem novas opções de otimização de rede que permitem que uma VM do Linux tooachieve maior rede taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="ce783-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="ce783-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ce783-123">Ubuntu</span></span>

<span data-ttu-id="ce783-124">Na otimização da ordem tooget Olá, primeiro atualize a versão mais recente com suporte de toohello, a partir de junho de 2017, o que é:</span><span class="sxs-lookup"><span data-stu-id="ce783-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="ce783-125">Após a conclusão da atualização hello, digite hello mais recente do kernel para Olá tooget comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce783-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="ce783-126">Comando opcional:</span><span class="sxs-lookup"><span data-stu-id="ce783-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="ce783-127">Kernel de visualização do Azure no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ce783-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="ce783-128">Essa visualização de Linux do Azure kernel não pode ter Olá mesmo nível de disponibilidade e confiabilidade como kernels são, em geral, versão de disponibilidade e de imagens do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ce783-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="ce783-129">Olá recurso não tem suporte, pode ter restringido recursos e pode não ser tão confiável quanto o kernel do saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="ce783-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="ce783-130">Não use este kernel para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="ce783-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="ce783-131">Desempenho de taxa de transferência significativa pode ser obtido instalando Olá proposta de kernel do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce783-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="ce783-132">tootry este kernel, adicionar essa linha too/etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="ce783-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="ce783-133">Em seguida, execute estes comandos como raiz.</span><span class="sxs-lookup"><span data-stu-id="ce783-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="ce783-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="ce783-134">CentOS</span></span>

<span data-ttu-id="ce783-135">Na otimização da ordem tooget Olá, primeiro atualize a versão mais recente com suporte de toohello, a partir de julho de 2017, o que é:</span><span class="sxs-lookup"><span data-stu-id="ce783-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="ce783-136">Após a conclusão da atualização hello, instalar hello mais recente Integration Services LIS (Linux).</span><span class="sxs-lookup"><span data-stu-id="ce783-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="ce783-137">otimização de taxa de transferência Hello está em LIS, a partir de 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="ce783-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="ce783-138">Digite hello comandos tooinstall LIS a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce783-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="ce783-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="ce783-139">Red Hat</span></span>

<span data-ttu-id="ce783-140">Na otimização da ordem tooget Olá, primeiro atualize a versão mais recente com suporte de toohello, a partir de julho de 2017, o que é:</span><span class="sxs-lookup"><span data-stu-id="ce783-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="ce783-141">Após a conclusão da atualização hello, instalar hello mais recente Integration Services LIS (Linux).</span><span class="sxs-lookup"><span data-stu-id="ce783-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="ce783-142">otimização de taxa de transferência Hello está em LIS, a partir da versão 4.2.</span><span class="sxs-lookup"><span data-stu-id="ce783-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="ce783-143">Digite hello toodownload comandos a seguir e instalá-los:</span><span class="sxs-lookup"><span data-stu-id="ce783-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="ce783-144">Saiba mais sobre o Linux Integration Services versão 4.2 para o Hyper-V exibindo Olá [página de download](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="ce783-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce783-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce783-145">Next steps</span></span>
* <span data-ttu-id="ce783-146">Agora que hello VM é otimizada, consulte o resultado de saudação com [largura de banda/taxa de transferência de teste de máquina virtual do Azure](virtual-network-bandwidth-testing.md) para seu cenário.</span><span class="sxs-lookup"><span data-stu-id="ce783-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="ce783-147">Saiba mais com as [Perguntas frequentes sobre a rede virtual do Azure](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="ce783-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
