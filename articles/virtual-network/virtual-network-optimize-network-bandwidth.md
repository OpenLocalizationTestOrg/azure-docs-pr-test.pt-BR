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
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Otimizar a taxa de transferência de rede para máquinas virtuais do Azure

Máquinas virtuais do Azure (VM) têm configurações de rede padrão que podem ser mais otimizadas para taxa de transferência de rede. Este artigo descreve como toooptimize rede taxa de transferência do Microsoft Azure Windows e VMs do Linux, incluindo os principais distribuições como Ubuntu, CentOS e Red Hat.

## <a name="windows-vm"></a>VM Windows

Se sua VM do Windows tem suporte com [acelerado rede](virtual-network-create-vm-accelerated-networking.md), habilitar esse recurso seria uma configuração ideal Olá para taxa de transferência. Para todas as outras VMs do Windows, usar RSS (Receive Side Scaling) pode alcançar uma taxa de transferência máxima maior que uma VM sem RSS. RSS pode ser desabilitado por padrão em uma VM do Windows. Concluir hello toodetermine as etapas a seguir se o RSS está habilitado e tooenable se ele está desabilitado.

1. Digite hello `Get-NetAdapterRss` toosee de comando do PowerShell se o RSS está habilitado para um adaptador de rede. Em Olá seguir o exemplo de saída retornados de saudação `Get-NetAdapterRss`, RSS não está habilitado.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Digite hello tooenable comando RSS a seguir:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    o comando anterior Olá não tem uma saída. comando Olá alterado as configurações de NIC, causando a perda de conectividade temporário para aproximadamente um minuto. Aparece uma caixa de diálogo Reconnecting durante a perda de conectividade de saudação. Normalmente, a conectividade for restaurada após a tentativa de terceiro hello.
3. Confirme se o RSS está habilitado no hello VM inserindo Olá `Get-NetAdapterRss` comando novamente. Se for bem-sucedido, Olá saída de exemplo a seguir será retornada:

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>VM Linux

RSS está sempre habilitado por padrão em uma VM do Linux do Azure. Kernels Linux lançados desde janeiro de 2017 incluem novas opções de otimização de rede que permitem que uma VM do Linux tooachieve maior rede taxa de transferência.

### <a name="ubuntu"></a>Ubuntu

Na otimização da ordem tooget Olá, primeiro atualize a versão mais recente com suporte de toohello, a partir de junho de 2017, o que é:
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Após a conclusão da atualização hello, digite hello mais recente do kernel para Olá tooget comandos a seguir:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

Comando opcional:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Kernel de visualização do Azure no Ubuntu
> [!WARNING]
> Essa visualização de Linux do Azure kernel não pode ter Olá mesmo nível de disponibilidade e confiabilidade como kernels são, em geral, versão de disponibilidade e de imagens do Marketplace. Olá recurso não tem suporte, pode ter restringido recursos e pode não ser tão confiável quanto o kernel do saudação padrão. Não use este kernel para cargas de trabalho de produção.

Desempenho de taxa de transferência significativa pode ser obtido instalando Olá proposta de kernel do Linux do Azure. tootry este kernel, adicionar essa linha too/etc/apt/sources.list

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Em seguida, execute estes comandos como raiz.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

Na otimização da ordem tooget Olá, primeiro atualize a versão mais recente com suporte de toohello, a partir de julho de 2017, o que é:
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Após a conclusão da atualização hello, instalar hello mais recente Integration Services LIS (Linux).
otimização de taxa de transferência Hello está em LIS, a partir de 4.2.2-2. Digite hello comandos tooinstall LIS a seguir:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

Na otimização da ordem tooget Olá, primeiro atualize a versão mais recente com suporte de toohello, a partir de julho de 2017, o que é:
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Após a conclusão da atualização hello, instalar hello mais recente Integration Services LIS (Linux).
otimização de taxa de transferência Hello está em LIS, a partir da versão 4.2. Digite hello toodownload comandos a seguir e instalá-los:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Saiba mais sobre o Linux Integration Services versão 4.2 para o Hyper-V exibindo Olá [página de download](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Próximas etapas
* Agora que hello VM é otimizada, consulte o resultado de saudação com [largura de banda/taxa de transferência de teste de máquina virtual do Azure](virtual-network-bandwidth-testing.md) para seu cenário.
* Saiba mais com as [Perguntas frequentes sobre a rede virtual do Azure](virtual-networks-faq.md)
