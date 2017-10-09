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
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a>Instalar drivers NVIDIA GPU em VMs da série N que executam o Linux

tootake as vantagens dos recursos GPU de saudação da série de N Azure VMs que executam o Linux, instalar os drivers gráficos NVIDIA com suporte. Este artigo apresenta etapas de instalação do driver depois que você implanta uma VM da série N. Também há informações de instalação de driver disponíveis para [VMs do Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


Para obter as especificações de VMs da série N, as capacidades de armazenamento e os detalhes de disco, consulte [Tamanhos de VM Linux para GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a>Instalar drivers GRID para VMs NV

drivers de grade NVIDIA tooinstall em VMs NV, fazer uma conexão de SSH tooeach VM e siga as etapas de saudação distribuição do Linux. 

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Executar Olá `lspci` comando. Verifique se o cartão Olá M60 NVIDIA ou cartões são visíveis como dispositivos PCI.

2. Instale as atualizações.

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. Desabilite o driver de kernel Nouveau Olá, é incompatível com o driver NVIDIA hello. (Apenas usar Olá NVIDIA driver em VMs NV.) toodo isso, crie um arquivo em `/etc/modprobe.d `chamado `nouveau.conf` com hello conteúdo a seguir:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. Reinicializar Olá VM e reconecte. Saia do servidor X:

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. Baixe e instale o driver de grade hello:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. Quando você for questionado se deseja toorun Olá nvidia xconfig utilitário tooupdate seu arquivo de configuração de X, selecione **Sim**.

7. Após a conclusão da instalação, copie /etc/nvidia/gridd.conf.template tooa novo arquivo gridd.conf no local /etc/hosts nvidia /

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. Adicionar Olá seguir muito`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Reinicialize Olá VM e continuar a instalação do tooverify hello.


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Baseado em CentOS 7.3 ou Red Hat Enterprise Linux 7.3


1. Atualização de kernel hello e DKMS.
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. Desabilite o driver de kernel Nouveau Olá, é incompatível com o driver NVIDIA hello. (Apenas usar Olá NVIDIA driver em VMs NV.) toodo isso, crie um arquivo em `/etc/modprobe.d `chamado `nouveau.conf` com hello conteúdo a seguir:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. Reinicializar Olá VM, reconecte e instalar hello mais recentes serviços de integração do Linux para Hyper-v:
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. Reconecte toohello VM e executar Olá `lspci` comando. Verifique se o cartão Olá M60 NVIDIA ou cartões são visíveis como dispositivos PCI.
 
5. Baixe e instale o driver de grade hello:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. Quando você for questionado se deseja toorun Olá nvidia xconfig utilitário tooupdate seu arquivo de configuração de X, selecione **Sim**.

7. Após a conclusão da instalação, copie /etc/nvidia/gridd.conf.template tooa novo arquivo gridd.conf no local /etc/hosts nvidia /
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. Adicionar Olá seguir muito`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Reinicialize Olá VM e continuar a instalação do tooverify hello.

### <a name="verify-driver-installation"></a>Verificar a instalação de drivers


tooquery Olá estado do dispositivo GPU, SSH toohello VM e hello execução [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o driver de saudação de utilitário de linha de comando. 

A seguir toohello semelhante saída é exibida:

![Status do dispositivo NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a>Servidor X11
Se você precisar de um X11 servidor para conexões remotas tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) é recomendada, pois permite aceleração de elementos gráficos. Olá BusID do dispositivo Olá M60 deve ser adicionado manualmente toohello xconfig arquivo (`etc/X11/xorg.conf` no Ubuntu 16.04 LTS, `/etc/X11/XF86config` em 7.3 CentOS ou Red Hat Enterprise Server 7.3). Adicionar um `"Device"` seção a seguir toohello semelhante:
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
Além disso, atualize seu `"Screen"` seção toouse este dispositivo.
 
Olá BusID pode ser encontrado, executando

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
Olá BusID pode alterar quando uma máquina virtual é realocada ou reinicializada. Portanto, talvez você queira toouse uma saudação de tooupdate script BusID na configuração de saudação X11 quando uma VM é reiniciada. Por exemplo:

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

Esse arquivo pode ser invocado como raiz na inicialização criando uma entrada para ele em `/etc/rc.d/rc3.d`.


## <a name="install-cuda-drivers-for-nc-vms"></a>Instalar drivers CUDA Tesla para VMs NC

Aqui são drivers NVIDIA tooinstall etapas em VMs do Linux NC do hello NVIDIA CUDA Toolkit 8.0. 

Os desenvolvedores de C e C++, opcionalmente, podem instalar aplicativos de acelerado de GPU do Olá completos Kit de ferramentas toobuild. Para obter mais informações, consulte Olá [CUDA guia de instalação](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).


> [!NOTE]
> Os links de download do driver CUDA fornecidos aqui são atuais no momento da publicação. Para os drivers mais recentes de CUDA hello, visite Olá [NVIDIA](http://www.nvidia.com/) site.
>

tooinstall CUDA Toolkit, fazer uma conexão de SSH tooeach VM. tooverify que Olá sistema tem uma GPU compatível com CUDA, execute Olá comando a seguir:

```bash
lspci | grep -i NVIDIA
```
Você verá a saída toohello semelhantes (mostrando uma placa NVIDIA Tesla K80) de exemplo a seguir:

![Saída do comando lspci](./media/n-series-driver-setup/lspci.png)

Em seguida, execute os comandos de instalação específicos para a sua distribuição.

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Baixe e instale drivers CUDA hello.
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  instalação de saudação pode levar vários minutos.

2. toooptionally instalação Olá completa CUDA Kit de ferramentas, tipo:

  ```bash
  sudo apt-get install cuda
  ```

3. Reinicialize Olá VM e continuar a instalação do tooverify hello.

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Baseado em CentOS 7.3 ou Red Hat Enterprise Linux 7.3

1. Obtenha atualizações. 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. Reconecte toohello VM e instalar hello mais recentes serviços de integração do Linux para Hyper-V.

  > [!IMPORTANT]
  > Se você instalou uma imagem com base em CentOS HPC em uma VM NC24r, ignore tooStep 3. Como drivers de RDMA do Azure e serviços de integração do Linux são pré-instalado na imagem hello, LIS não devem ser atualizado e atualizações de kernel estão desabilitadas por padrão.
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. Reconectar toohello VM e continuar a instalação com hello comandos a seguir:

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

  instalação de saudação pode levar vários minutos. 

4. toooptionally instalação Olá completa CUDA Kit de ferramentas, tipo:

  ```bash
  sudo yum install cuda
  ```

5. Reinicialize Olá VM e continuar a instalação do tooverify hello.


### <a name="verify-driver-installation"></a>Verificar a instalação de drivers


tooquery Olá estado do dispositivo GPU, SSH toohello VM e hello execução [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o driver de saudação de utilitário de linha de comando. 

A seguir toohello semelhante saída é exibida:

![Status do dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a>Atualizações de driver CUDA

É recomendável que você atualize periodicamente os drivers CUDA após a implantação.

#### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Baseado em CentOS 7.3 ou Red Hat Enterprise Linux 7.3

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a>Solucionar problemas

* Há um problema conhecido com drivers CUDA nas VMs série N Azure executando o kernel do Linux 4.4.0-75 Olá no Ubuntu 16.04 LTS. Se você estiver atualizando de uma versão anterior do kernel, atualizar tooat menos 4.4.0-77 de versão do kernel. 



## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre Olá GPUs NVIDIA Olá VMs da série de N, consulte:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para VMs NC do Azure)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para VMs NV do Azure)

* toocapture uma imagem de VM do Linux com os drivers NVIDIA instalados, consulte [como toogeneralize e capturar uma máquina virtual Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
