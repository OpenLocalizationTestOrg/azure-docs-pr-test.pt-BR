---
title: "instalação do driver de aaaAzure série N para Linux | Microsoft Docs"
description: "Como tooset drivers de GPU NVIDIA para VMs série N executando o Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="9bd61-103">Instalar drivers NVIDIA GPU em VMs da série N que executam o Linux</span><span class="sxs-lookup"><span data-stu-id="9bd61-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="9bd61-104">tootake as vantagens dos recursos GPU de saudação da série de N Azure VMs que executam o Linux, instalar os drivers gráficos NVIDIA com suporte.</span><span class="sxs-lookup"><span data-stu-id="9bd61-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="9bd61-105">Este artigo apresenta etapas de instalação do driver depois que você implanta uma VM da série N.</span><span class="sxs-lookup"><span data-stu-id="9bd61-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="9bd61-106">Também há informações de instalação de driver disponíveis para [VMs do Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9bd61-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="9bd61-107">Para obter as especificações de VMs da série N, as capacidades de armazenamento e os detalhes de disco, consulte [Tamanhos de VM Linux para GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9bd61-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="9bd61-108">Instalar drivers GRID para VMs NV</span><span class="sxs-lookup"><span data-stu-id="9bd61-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="9bd61-109">drivers de grade NVIDIA tooinstall em VMs NV, fazer uma conexão de SSH tooeach VM e siga as etapas de saudação distribuição do Linux.</span><span class="sxs-lookup"><span data-stu-id="9bd61-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="9bd61-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9bd61-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="9bd61-111">Executar Olá `lspci` comando.</span><span class="sxs-lookup"><span data-stu-id="9bd61-111">Run hello `lspci` command.</span></span> <span data-ttu-id="9bd61-112">Verifique se o cartão Olá M60 NVIDIA ou cartões são visíveis como dispositivos PCI.</span><span class="sxs-lookup"><span data-stu-id="9bd61-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="9bd61-113">Instale as atualizações.</span><span class="sxs-lookup"><span data-stu-id="9bd61-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="9bd61-114">Desabilite o driver de kernel Nouveau Olá, é incompatível com o driver NVIDIA hello.</span><span class="sxs-lookup"><span data-stu-id="9bd61-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="9bd61-115">(Apenas usar Olá NVIDIA driver em VMs NV.) toodo isso, crie um arquivo em `/etc/modprobe.d `chamado `nouveau.conf` com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9bd61-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="9bd61-116">Reinicializar Olá VM e reconecte.</span><span class="sxs-lookup"><span data-stu-id="9bd61-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="9bd61-117">Saia do servidor X:</span><span class="sxs-lookup"><span data-stu-id="9bd61-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="9bd61-118">Baixe e instale o driver de grade hello:</span><span class="sxs-lookup"><span data-stu-id="9bd61-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="9bd61-119">Quando você for questionado se deseja toorun Olá nvidia xconfig utilitário tooupdate seu arquivo de configuração de X, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="9bd61-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="9bd61-120">Após a conclusão da instalação, copie /etc/nvidia/gridd.conf.template tooa novo arquivo gridd.conf no local /etc/hosts nvidia /</span><span class="sxs-lookup"><span data-stu-id="9bd61-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="9bd61-121">Adicionar Olá seguir muito`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="9bd61-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="9bd61-122">Reinicialize Olá VM e continuar a instalação do tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="9bd61-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="9bd61-123">Baseado em CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="9bd61-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="9bd61-124">Atualização de kernel hello e DKMS.</span><span class="sxs-lookup"><span data-stu-id="9bd61-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="9bd61-125">Desabilite o driver de kernel Nouveau Olá, é incompatível com o driver NVIDIA hello.</span><span class="sxs-lookup"><span data-stu-id="9bd61-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="9bd61-126">(Apenas usar Olá NVIDIA driver em VMs NV.) toodo isso, crie um arquivo em `/etc/modprobe.d `chamado `nouveau.conf` com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9bd61-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="9bd61-127">Reinicializar Olá VM, reconecte e instalar hello mais recentes serviços de integração do Linux para Hyper-v:</span><span class="sxs-lookup"><span data-stu-id="9bd61-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="9bd61-128">Reconecte toohello VM e executar Olá `lspci` comando.</span><span class="sxs-lookup"><span data-stu-id="9bd61-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="9bd61-129">Verifique se o cartão Olá M60 NVIDIA ou cartões são visíveis como dispositivos PCI.</span><span class="sxs-lookup"><span data-stu-id="9bd61-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="9bd61-130">Baixe e instale o driver de grade hello:</span><span class="sxs-lookup"><span data-stu-id="9bd61-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="9bd61-131">Quando você for questionado se deseja toorun Olá nvidia xconfig utilitário tooupdate seu arquivo de configuração de X, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="9bd61-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="9bd61-132">Após a conclusão da instalação, copie /etc/nvidia/gridd.conf.template tooa novo arquivo gridd.conf no local /etc/hosts nvidia /</span><span class="sxs-lookup"><span data-stu-id="9bd61-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="9bd61-133">Adicionar Olá seguir muito`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="9bd61-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="9bd61-134">Reinicialize Olá VM e continuar a instalação do tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="9bd61-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="9bd61-135">Verificar a instalação de drivers</span><span class="sxs-lookup"><span data-stu-id="9bd61-135">Verify driver installation</span></span>


<span data-ttu-id="9bd61-136">tooquery Olá estado do dispositivo GPU, SSH toohello VM e hello execução [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o driver de saudação de utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9bd61-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="9bd61-137">A seguir toohello semelhante saída é exibida:</span><span class="sxs-lookup"><span data-stu-id="9bd61-137">Output similar toohello following appears:</span></span>

![Status do dispositivo NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="9bd61-139">Servidor X11</span><span class="sxs-lookup"><span data-stu-id="9bd61-139">X11 server</span></span>
<span data-ttu-id="9bd61-140">Se você precisar de um X11 servidor para conexões remotas tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) é recomendada, pois permite aceleração de elementos gráficos.</span><span class="sxs-lookup"><span data-stu-id="9bd61-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="9bd61-141">Olá BusID do dispositivo Olá M60 deve ser adicionado manualmente toohello xconfig arquivo (`etc/X11/xorg.conf` no Ubuntu 16.04 LTS, `/etc/X11/XF86config` em 7.3 CentOS ou Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="9bd61-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="9bd61-142">Adicionar um `"Device"` seção a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="9bd61-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="9bd61-143">Além disso, atualize seu `"Screen"` seção toouse este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9bd61-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="9bd61-144">Olá BusID pode ser encontrado, executando</span><span class="sxs-lookup"><span data-stu-id="9bd61-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="9bd61-145">Olá BusID pode alterar quando uma máquina virtual é realocada ou reinicializada.</span><span class="sxs-lookup"><span data-stu-id="9bd61-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="9bd61-146">Portanto, talvez você queira toouse uma saudação de tooupdate script BusID na configuração de saudação X11 quando uma VM é reiniciada.</span><span class="sxs-lookup"><span data-stu-id="9bd61-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="9bd61-147">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9bd61-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="9bd61-148">Esse arquivo pode ser invocado como raiz na inicialização criando uma entrada para ele em `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="9bd61-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="9bd61-149">Instalar drivers CUDA Tesla para VMs NC</span><span class="sxs-lookup"><span data-stu-id="9bd61-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="9bd61-150">Aqui são drivers NVIDIA tooinstall etapas em VMs do Linux NC do hello NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="9bd61-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="9bd61-151">Os desenvolvedores de C e C++, opcionalmente, podem instalar aplicativos de acelerado de GPU do Olá completos Kit de ferramentas toobuild.</span><span class="sxs-lookup"><span data-stu-id="9bd61-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="9bd61-152">Para obter mais informações, consulte Olá [CUDA guia de instalação](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="9bd61-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="9bd61-153">Os links de download do driver CUDA fornecidos aqui são atuais no momento da publicação.</span><span class="sxs-lookup"><span data-stu-id="9bd61-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="9bd61-154">Para os drivers mais recentes de CUDA hello, visite Olá [NVIDIA](http://www.nvidia.com/) site.</span><span class="sxs-lookup"><span data-stu-id="9bd61-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="9bd61-155">tooinstall CUDA Toolkit, fazer uma conexão de SSH tooeach VM.</span><span class="sxs-lookup"><span data-stu-id="9bd61-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="9bd61-156">tooverify que Olá sistema tem uma GPU compatível com CUDA, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9bd61-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="9bd61-157">Você verá a saída toohello semelhantes (mostrando uma placa NVIDIA Tesla K80) de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9bd61-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![Saída do comando lspci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="9bd61-159">Em seguida, execute os comandos de instalação específicos para a sua distribuição.</span><span class="sxs-lookup"><span data-stu-id="9bd61-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="9bd61-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9bd61-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="9bd61-161">Baixe e instale drivers CUDA hello.</span><span class="sxs-lookup"><span data-stu-id="9bd61-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="9bd61-162">instalação de saudação pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="9bd61-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="9bd61-163">toooptionally instalação Olá completa CUDA Kit de ferramentas, tipo:</span><span class="sxs-lookup"><span data-stu-id="9bd61-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="9bd61-164">Reinicialize Olá VM e continuar a instalação do tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="9bd61-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="9bd61-165">Baseado em CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="9bd61-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="9bd61-166">Obtenha atualizações.</span><span class="sxs-lookup"><span data-stu-id="9bd61-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="9bd61-167">Reconecte toohello VM e instalar hello mais recentes serviços de integração do Linux para Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="9bd61-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9bd61-168">Se você instalou uma imagem com base em CentOS HPC em uma VM NC24r, ignore tooStep 3.</span><span class="sxs-lookup"><span data-stu-id="9bd61-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="9bd61-169">Como drivers de RDMA do Azure e serviços de integração do Linux são pré-instalado na imagem hello, LIS não devem ser atualizado e atualizações de kernel estão desabilitadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="9bd61-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="9bd61-170">Reconectar toohello VM e continuar a instalação com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9bd61-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  <span data-ttu-id="9bd61-171">instalação de saudação pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="9bd61-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="9bd61-172">toooptionally instalação Olá completa CUDA Kit de ferramentas, tipo:</span><span class="sxs-lookup"><span data-stu-id="9bd61-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="9bd61-173">Reinicialize Olá VM e continuar a instalação do tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="9bd61-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="9bd61-174">Verificar a instalação de drivers</span><span class="sxs-lookup"><span data-stu-id="9bd61-174">Verify driver installation</span></span>


<span data-ttu-id="9bd61-175">tooquery Olá estado do dispositivo GPU, SSH toohello VM e hello execução [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o driver de saudação de utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9bd61-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="9bd61-176">A seguir toohello semelhante saída é exibida:</span><span class="sxs-lookup"><span data-stu-id="9bd61-176">Output similar toohello following appears:</span></span>

![Status do dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="9bd61-178">Atualizações de driver CUDA</span><span class="sxs-lookup"><span data-stu-id="9bd61-178">CUDA driver updates</span></span>

<span data-ttu-id="9bd61-179">É recomendável que você atualize periodicamente os drivers CUDA após a implantação.</span><span class="sxs-lookup"><span data-stu-id="9bd61-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="9bd61-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9bd61-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="9bd61-181">Baseado em CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="9bd61-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="9bd61-182">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9bd61-182">Troubleshooting</span></span>

* <span data-ttu-id="9bd61-183">Há um problema conhecido com drivers CUDA nas VMs série N Azure executando o kernel do Linux 4.4.0-75 Olá no Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="9bd61-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="9bd61-184">Se você estiver atualizando de uma versão anterior do kernel, atualizar tooat menos 4.4.0-77 de versão do kernel.</span><span class="sxs-lookup"><span data-stu-id="9bd61-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="9bd61-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9bd61-185">Next steps</span></span>

* <span data-ttu-id="9bd61-186">Para obter mais informações sobre Olá GPUs NVIDIA Olá VMs da série de N, consulte:</span><span class="sxs-lookup"><span data-stu-id="9bd61-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="9bd61-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para VMs NC do Azure)</span><span class="sxs-lookup"><span data-stu-id="9bd61-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="9bd61-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para VMs NV do Azure)</span><span class="sxs-lookup"><span data-stu-id="9bd61-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="9bd61-189">toocapture uma imagem de VM do Linux com os drivers NVIDIA instalados, consulte [como toogeneralize e capturar uma máquina virtual Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9bd61-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
