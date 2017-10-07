---
title: aaaOptimize sua VM do Linux no Azure | Microsoft Docs
description: "Saiba algumas toomake de dicas de otimização se que você tiver configurado a VM do Linux para otimizar o desempenho no Azure"
keywords: "máquina virtual linux, linux máquina virtual, máquina virtual ubuntu"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a>Otimizar sua VM do Linux no Azure
Criar uma máquina virtual do Linux (VM) é fácil toodo de linha de comando Olá ou portal hello. Este tutorial mostra como tooensure configurá-lo toooptimize o desempenho na plataforma do Microsoft Azure hello. Este tópico usa uma VM do Ubuntu Server, mas é possível também criar uma máquina virtual do Linux usando [suas próprias imagens como modelos](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="prerequisites"></a>Pré-requisitos
Este tópico pressupõe que você já tenha uma Assinatura do Azure ativa ([inscrição de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e já tenha provisionado uma VM na sua Assinatura do Azure. Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooyour assinatura do Azure com [logon az](/cli/azure/#login) antes de [criar uma VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-os-disk"></a>Disco do sistema operacional do Azure
Depois de criar uma VM Linux no Azure, ela terá dois discos associados. **/dev/sda** é o disco do sistema operacional, **/dev/sdb** é o disco temporário.  Não use o disco do sistema operacional principal hello (**/desenvolvimento/sda**) para qualquer coisa, exceto o sistema operacional de saudação como ela é otimizada para rápido tempo de inicialização VM e fornece um bom desempenho para suas cargas de trabalho. Você deseja tooattach um ou mais discos tooyour VM tooget persistente e otimizado armazenamento para seus dados. 

## <a name="adding-disks-for-size-and-performance-targets"></a>Adicionando discos para metas de desempenho e tamanho
Com base no tamanho da VM de saudação, você pode anexar discos adicionais em uma série de too16, 32 discos em uma série D e 64 discos em uma máquina de série G - cada backup too1 TB de tamanho. Adicione discos adicionais conforme necessário para seus requisitos de IOps e espaço. Cada disco tem uma meta de desempenho de 500 IOps para o armazenamento padrão e backup too5000 IOps por disco para armazenamento Premium.  Para saber mais sobre os discos de Armazenamento Premium, consulte [Armazenamento Premium: Armazenamento de Alto Desempenho para VMs do Azure](../../storage/common/storage-premium-storage.md)

tooachieve Olá IOps mais alto em discos de armazenamento Premium, em que as configurações de cache foram definidas tooeither **ReadOnly** ou **nenhum**, você deve desabilitar **barreiras** enquanto montar o sistema de arquivos de saudação do Linux. Não é necessário barreiras como Olá grava tooPremium armazenamento feito discos são duráveis para essas configurações de cache.

* Se você usar **reiserFS**, desabilitar barreiras usando a opção de montagem Olá `barrier=none` (para habilitar as barreiras, use `barrier=flush`)
* Se você usar **ext3/ext4**, desabilitar barreiras usando a opção de montagem Olá `barrier=0` (para habilitar as barreiras, use `barrier=1`)
* Se você usar **XFS**, desabilitar barreiras usando a opção de montagem Olá `nobarrier` (para habilitar as barreiras, use a opção de saudação `barrier`)

## <a name="unmanaged-storage-account-considerations"></a>Considerações sobre a conta de armazenamento não gerenciado
ação de padrão de Hello quando você cria uma máquina virtual com hello Azure CLI 2.0 é toouse Azure gerenciados discos.  Esses discos são manipulados pelo Olá plataforma Windows Azure e não exigem qualquer etapa de preparação ou local toostore-los.  Os discos não gerenciados exigem uma conta de armazenamento e têm algumas considerações adicionais de desempenho.  Para saber mais sobre discos gerenciados, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md).  Olá seção a seguir descreve as considerações de desempenho apenas quando você usar discos não gerenciados.  Olá novamente, padrão e solução de armazenamento recomendado é discos toouse gerenciado.

Se você criar uma VM com discos não gerenciados, certifique-se de que você anexar discos de contas de armazenamento que reside no hello mesmo região tooensure sua VM próximos e minimizar a latência de rede.  Cada conta de Armazenamento Standard tem um máximo de 20k IOps e uma capacidade de tamanho de 500 TB.  Esse limite estabelece discos tooapproximately 40 usado como disco Olá SO e discos de dados que você criar. Para contas de Armazenamento Premium, não há nenhum limite máximo de IOps, mas há um limite de tamanho de 32 TB. 

Ao lidar com cargas de trabalho de IOps alto e você tiver escolhido o armazenamento padrão para os discos, talvez seja necessário discos de saudação toosplit em vários toomake de contas de armazenamento se que você não atingiu Olá 20.000 IOps limitar para contas de armazenamento padrão. Sua VM pode conter uma mistura de discos de diferentes contas de armazenamento e tooachieve de tipos de conta de armazenamento a configuração ideal.
 

## <a name="your-vm-temporary-drive"></a>Unidade temporária da VM
Por padrão, quando você cria uma VM, o Azure fornece um disco de sistema operacional (**/dev/sda**) e um disco temporário (**/dev/sdb**).  Todos os discos extras que você adicionar aparecerão como **/dev/sdc**, **/dev/sdd**, **/dev/sde** e assim por diante. Todos os dados no disco temporário (**/dev/sdb**) não são duráveis e poderão ser perdidos se eventos específicos, como redimensionamento de VM, reimplantação ou manutenção, forçarem uma reinicialização da VM.  tamanho de saudação e tipo de disco temporário é escolhido no momento da implantação de tamanho de VM de toohello relacionados. Todos unidade temporária do hello de VMs (série DS, G e DS_V2) de tamanho do hello premium contam com um SSD local de desempenho adicional de backup too48k IOps. 

## <a name="linux-swap-file"></a>Arquivo de permuta do Linux
Se sua VM do Azure for de uma imagem Ubuntu ou CoreOS, você pode usar CustomData toosend toocloud-init uma configuração de nuvem. Se você [carregou uma imagem do Linux personalizada](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que usa a inicialização de nuvem, configure também as partições de troca usando a inicialização de nuvem.

No Ubuntu imagens de nuvem, você deve usar partição de troca init nuvem tooconfigure hello. Para obter mais informações, consulte [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

Para imagens sem suporte de inicialização de nuvem, imagens VM implantadas por meio de saudação do Azure Marketplace tem um agente de Linux de VM integrado com hello sistema operacional. Esse agente permite Olá toointeract VM com vários serviços do Azure. Supondo que você implantou uma imagem padrão do hello Azure Marketplace, você precisaria toodo Olá toocorrectly a seguir configurar as configurações do arquivo de permuta Linux:

Localizar e modificar as duas entradas Olá **/etc/waagent.conf** arquivo. Eles controlam o tamanho do arquivo de permuta hello e a existência de saudação de um arquivo de permuta dedicado. Olá parâmetros você está procurando toomodify são `ResourceDisk.EnableSwap=N` e`ResourceDisk.SwapSizeMB=0` 

Alterar Olá parâmetros toohello configurações a seguir:

* ResourceDisk.EnableSwap=Y
* ResourceDisk.SwapSizeMB={size em MB toomeet suas necessidades} 

Depois que você fez Olá alterar, precisar toorestart Olá waagent ou reinicie a VM do Linux tooreflect essas alterações.  Você sabe que foram implementadas alterações hello e um arquivo de permuta foi criado quando você usa Olá `free` comando tooview de espaço livre. Olá, exemplo a seguir tem um arquivo de permuta de 512MB criado como resultado de modificação de saudação **waagent.conf** arquivo:

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a>Algoritmo de agendamento de E/S para o Armazenamento Premium
Com o kernel do Linux Olá 2.6.18, algoritmo de programação de e/s do saudação padrão foi alterado de prazo tooCFQ (algoritmo de fila justa completamente). Para padrões de E/S de acesso aleatório, há uma diferença insignificante nas diferenças de desempenho entre CFQ e Deadline.  Para discos baseada em SSD, onde o padrão de e/s de disco Olá é predominantemente sequencial, alternar novamente toohello algoritmo NOOP ou prazo pode obter um melhor desempenho de e/s.

### <a name="view-hello-current-io-scheduler"></a>Agendador do modo de exibição Olá atual e/s
Use Olá comando a seguir:  

```bash
cat /sys/block/sda/queue/scheduler
```

Você verá a seguinte saída, que indica o Agendador atual hello.  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a>Alterar dispositivo atual hello (dev/sda) de algoritmo de agendamento de e/s
Use Olá comandos a seguir:  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> Aplicar esta configuração somente para **/dev/sda** não é útil. Defina em todos os discos de dados onde a e/s sequencial domina padrão de e/s de saudação.  

Você deve ver Olá saída a seguir, indicando que **grub.cfg** foi recriado com êxito e que o Agendador de saudação padrão tiver sido atualizado tooNOOP.  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

Para Olá Redhat família de distribuição, você só precisa Olá comando a seguir:   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a>Usando RAID de Software tooachieve maior / Ops
Se suas cargas de trabalho exigem mais IOps do que um único disco pode fornecer, será necessário toouse uma configuração de RAID de software de vários discos. Como Azure já executa resiliência de disco na camada de infraestrutura local hello, você atingir o nível mais alto de saudação do desempenho de uma configuração de distribuição de RAID 0.  Provisionar e criar discos Olá ambiente do Azure e anexá-los tooyour VM Linux antes de particionamento, formatação e montar Olá unidades.  Mais detalhes sobre como configurar uma configuração de RAID de software em sua VM do Linux no azure podem ser encontrados no hello  **[configuração RAID de Software no Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**  documento.

## <a name="next-steps"></a>Próximas etapas
Lembre-se de que, com todas as discussões de otimização, você precisa de testes tooperform antes e depois de cada impacto de saudação toomeasure alteração hello alteração tem.  A otimização é um processo passo a passo que tem resultados distintos em computadores diferentes no seu ambiente.  O que funciona para uma configuração pode não funcionar para outras.

Alguns recursos de tooadditional links úteis: 

* [Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure](../../storage/common/storage-premium-storage.md)
* [Guia do usuário do agente Linux para o Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Otimizando o desempenho do MySQL nas VMs Linux do Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurar RAID de software no Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

