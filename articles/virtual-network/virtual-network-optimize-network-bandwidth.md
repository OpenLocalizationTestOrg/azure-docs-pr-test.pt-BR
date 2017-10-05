---
title: "Otimizar a taxa de transferência de rede de VM | Microsoft Docs"
description: "Aprenda a otimizar a taxa de transferência de rede de máquina virtual do Azure."
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
ms.openlocfilehash: 914747983d4d974810836be66d6c6af343f58b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="8e85a-103">Otimizar a taxa de transferência de rede para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="8e85a-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="8e85a-104">Máquinas virtuais do Azure (VM) têm configurações de rede padrão que podem ser mais otimizadas para taxa de transferência de rede.</span><span class="sxs-lookup"><span data-stu-id="8e85a-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="8e85a-105">Este artigo descreve como otimizar a taxa de transferência de rede para VMs em Windows e Linux do Microsoft Azure, incluindo distribuições principais como o Ubuntu, CentOS e Red Hat.</span><span class="sxs-lookup"><span data-stu-id="8e85a-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="8e85a-106">VM Windows</span><span class="sxs-lookup"><span data-stu-id="8e85a-106">Windows VM</span></span>

<span data-ttu-id="8e85a-107">Se sua VM do Windows tiver suporte para [Rede Acelerada](virtual-network-create-vm-accelerated-networking.md), habilitar esse recurso será a configuração ideal para a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="8e85a-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be the optimal configuration for throughput.</span></span> <span data-ttu-id="8e85a-108">Para todas as outras VMs do Windows, usar RSS (Receive Side Scaling) pode alcançar uma taxa de transferência máxima maior que uma VM sem RSS.</span><span class="sxs-lookup"><span data-stu-id="8e85a-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="8e85a-109">RSS pode ser desabilitado por padrão em uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="8e85a-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="8e85a-110">Conclua as seguintes etapas para determinar se o RSS está habilitado e habilitá-lo se ele estiver desabilitado.</span><span class="sxs-lookup"><span data-stu-id="8e85a-110">Complete the following steps to determine whether RSS is enabled and to enable it if it's disabled.</span></span>

1. <span data-ttu-id="8e85a-111">Insira o `Get-NetAdapterRss` comando do PowerShell para ver se o RSS está habilitado para um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="8e85a-111">Enter the `Get-NetAdapterRss` PowerShell command to see if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="8e85a-112">Na saída do exemplo seguinte retornada do `Get-NetAdapterRss`, RSS não está habilitado.</span><span class="sxs-lookup"><span data-stu-id="8e85a-112">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="8e85a-113">Digite o comando a seguir para habilitar o RSS:</span><span class="sxs-lookup"><span data-stu-id="8e85a-113">Enter the following command to enable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="8e85a-114">O comando anterior não tem uma saída.</span><span class="sxs-lookup"><span data-stu-id="8e85a-114">The previous command does not have an output.</span></span> <span data-ttu-id="8e85a-115">O comando alterou configurações de NIC, causando uma perda de conectividade temporária por aproximadamente um minuto.</span><span class="sxs-lookup"><span data-stu-id="8e85a-115">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="8e85a-116">Aparece uma caixa de diálogo Reconnecting durante a perda de conectividade.</span><span class="sxs-lookup"><span data-stu-id="8e85a-116">A Reconnecting dialog box appears during the connectivity loss.</span></span> <span data-ttu-id="8e85a-117">Normalmente, a conectividade for restaurada após a terceira tentativa.</span><span class="sxs-lookup"><span data-stu-id="8e85a-117">Connectivity is typically restored after the third attempt.</span></span>
3. <span data-ttu-id="8e85a-118">Confirme se o RSS está habilitado na VM inserindo o `Get-NetAdapterRss` comando novamente.</span><span class="sxs-lookup"><span data-stu-id="8e85a-118">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="8e85a-119">Se for bem-sucedido, será retornada a seguinte saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e85a-119">If successful, the following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="8e85a-120">VM Linux</span><span class="sxs-lookup"><span data-stu-id="8e85a-120">Linux VM</span></span>

<span data-ttu-id="8e85a-121">RSS está sempre habilitado por padrão em uma VM do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e85a-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="8e85a-122">Kernels do Linux lançados desde janeiro de 2017 incluem novas opções de otimização de rede que permitem que uma VM do Linux obter maior taxa de transferência de rede.</span><span class="sxs-lookup"><span data-stu-id="8e85a-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM to achieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="8e85a-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8e85a-123">Ubuntu</span></span>

<span data-ttu-id="8e85a-124">Para obter a otimização, primeiro atualize para a versão mais recente com suporte, a partir de junho de 2017, que é:</span><span class="sxs-lookup"><span data-stu-id="8e85a-124">In order to get the optimization, first update to the latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="8e85a-125">Depois que a atualização for concluída, digite os seguintes comandos para obter o kernel mais recente:</span><span class="sxs-lookup"><span data-stu-id="8e85a-125">After the update is complete, enter the following commands to get the latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="8e85a-126">Comando opcional:</span><span class="sxs-lookup"><span data-stu-id="8e85a-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="8e85a-127">Kernel de visualização do Azure no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8e85a-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="8e85a-128">Esse núcleo de Visualização do Linux do Azure pode não ter o mesmo nível de disponibilidade e confiabilidade que imagens e kernels do Marketplace em versão de disponibilidade, em geral.</span><span class="sxs-lookup"><span data-stu-id="8e85a-128">This Azure Linux Preview kernel may not have the same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="8e85a-129">O recurso não tem suporte, pode ter recursos restritos e pode não estar tão confiável quanto o kernel padrão.</span><span class="sxs-lookup"><span data-stu-id="8e85a-129">The feature is not supported, may have constrained capabilities, and may not be as reliable as the default kernel.</span></span> <span data-ttu-id="8e85a-130">Não use este kernel para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="8e85a-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="8e85a-131">O desempenho de taxa de transferência significativo pode ser obtido pela instalação do kernel do Linux do Azure proposto.</span><span class="sxs-lookup"><span data-stu-id="8e85a-131">Significant throughput performance can be achieved by installing the proposed Azure Linux kernel.</span></span> <span data-ttu-id="8e85a-132">Para testar este kernel, adicione esta linha a /etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="8e85a-132">To try this kernel, add this line to /etc/apt/sources.list</span></span>

```bash
#add this to the end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="8e85a-133">Em seguida, execute estes comandos como raiz.</span><span class="sxs-lookup"><span data-stu-id="8e85a-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="8e85a-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="8e85a-134">CentOS</span></span>

<span data-ttu-id="8e85a-135">Para obter a otimização, primeiro atualize para a versão mais recente com suporte, a partir de julho de 2017, que é:</span><span class="sxs-lookup"><span data-stu-id="8e85a-135">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="8e85a-136">Depois que a atualização for concluída, instale o LIS (Linux Integration Services) mais recente.</span><span class="sxs-lookup"><span data-stu-id="8e85a-136">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="8e85a-137">A otimização de taxa de transferência é feita no LIS, a partir da versão 4.2.2-2.</span><span class="sxs-lookup"><span data-stu-id="8e85a-137">The throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="8e85a-138">Digite os seguintes comandos para instalar o LIS:</span><span class="sxs-lookup"><span data-stu-id="8e85a-138">Enter the following commands to install LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="8e85a-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="8e85a-139">Red Hat</span></span>

<span data-ttu-id="8e85a-140">Para obter a otimização, primeiro atualize para a versão mais recente com suporte, a partir de julho de 2017, que é:</span><span class="sxs-lookup"><span data-stu-id="8e85a-140">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="8e85a-141">Depois que a atualização for concluída, instale o LIS (Linux Integration Services) mais recente.</span><span class="sxs-lookup"><span data-stu-id="8e85a-141">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="8e85a-142">A otimização de taxa de transferência é feita no LIS, a partir da versão 4.2.</span><span class="sxs-lookup"><span data-stu-id="8e85a-142">The throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="8e85a-143">Digite os comandos a seguir para baixar e instalá-los:</span><span class="sxs-lookup"><span data-stu-id="8e85a-143">Enter the following commands to download and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="8e85a-144">Saiba mais sobre o Linux Integration Services versão 4.2 para o Hyper-V exibindo a [página de download](https://www.microsoft.com/download/details.aspx?id=55106).</span><span class="sxs-lookup"><span data-stu-id="8e85a-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e85a-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e85a-145">Next steps</span></span>
* <span data-ttu-id="8e85a-146">Agora que a VM está otimizada, veja o resultado com [Teste de Largura de Banda/Taxa de Transferência da VM do Azure](virtual-network-bandwidth-testing.md) para seu cenário.</span><span class="sxs-lookup"><span data-stu-id="8e85a-146">Now that the VM is optimized, see the result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="8e85a-147">Saiba mais com as [Perguntas frequentes sobre a rede virtual do Azure](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="8e85a-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
