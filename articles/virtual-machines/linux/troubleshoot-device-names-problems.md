---
title: "os nomes de dispositivo VM aaaLinux são alterados no Azure | Microsoft Docs"
description: "Explica Olá por nomes de dispositivo são alterados e fornecem uma solução para esse problema."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Solução de problemas: os nomes de dispositivo de VM do Linux são alterados

artigo Olá explica por que os nomes do dispositivo são alterados depois de reiniciar uma máquina virtual do Linux (VM), ou anexar novamente os discos de saudação. Ele também fornece uma solução de saudação para esse problema.

## <a name="symptom"></a>Sintoma

Você pode enfrentar Olá os problemas a seguir ao executar VMs do Linux no Microsoft Azure.

- Olá VM falha tooboot após uma reinicialização.

- Se os discos de dados for desanexados e reanexados, nomes de dispositivos de saudação para discos são alterados.

- Um aplicativo ou script que faz referência a um disco usando o nome do dispositivo falha. Localizar esse Olá nome do dispositivo de disco de saudação é alterado.

## <a name="cause"></a>Causa

Caminhos de dispositivo no Linux não há garantia toobe consistente entre as reinicializações. Nomes de dispositivo consistem em números principais (letra) e secundários.  Quando o driver de dispositivo de armazenamento de Linux Olá detecta um novo dispositivo, ele atribui tooit de números de dispositivo principais e secundárias do intervalo de saudação disponíveis. Quando um dispositivo é removido, números de saudação do dispositivo são liberada toobe reutilizado posteriormente.

Olá problema ocorre porque hello dispositivo varredura no Linux agendada pelo subsistema de SCSI Olá ocorre de maneira assíncrona. nomes de caminho de dispositivo final Olá podem variar entre as reinicializações. 

## <a name="solution"></a>Solução

tooresolve esse problema, use a nomenclatura persistente. Há quatro toopersistent de métodos de nomenclatura - por rótulo de sistema de arquivos, uuid, por id e pelo caminho. É recomendável o rótulo do sistema de arquivos de saudação e métodos UUID para VMs do Linux do Azure. 

A maioria das distribuições também fornecem a saudação **nofail** ou **nobootwait** fstab opções. Essas opções permitem tooboot um sistema, mesmo se o disco de saudação falhar toomount na inicialização. Verifique a documentação da distribuição Olá para obter mais informações sobre esses parâmetros. Para obter mais informações sobre como tooconfigure toouse uma VM do Linux um UUID quando você adiciona um disco de dados, consulte [conectar toohello novo disco de VM do Linux toomount Olá](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Quando hello Azure Linux é instalado em uma máquina virtual, ele usa Udev regras tooconstruct um conjunto de links simbólicos em **/dev/disk/azure**. Essas regras Udev podem ser usadas por aplicativos e discos de tooidentify scripts são anexado toohello VM, seu tipo, Olá LUN.

## <a name="more-information"></a>Mais informações

### <a name="identify-disk-luns"></a>Identificar LUNs de disco

Um aplicativo pode usar LUNs toofind todos os discos de saudação anexado e criação de links simbólicos. agente do Linux Azure Olá agora inclui udev regras configuradas links simbólicos em dispositivos de toohello um LUN, da seguinte maneira:

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

Informações de LUN também podem ser recuperadas de convidado do Linux hello usando lsscsi ou uma ferramenta semelhante, da seguinte maneira.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Essas informações de LUN de convidado podem ser usadas com a assinatura do Azure metadados tooidentify Olá local no armazenamento do Azure de saudação VHD que armazena dados de partição de saudação. Por exemplo, use Olá az cli:

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Descobrir UUIDs de sistema de arquivos usando o blkid

Um script ou aplicativo pode ler a saída de saudação do blkid ou semelhantes fontes de informações e criar links simbólicos em **dev** para uso. saída de Hello mostrará Olá UUIDs de todos os discos anexados toohello VM e hello dispositivo arquivo toowhich estão associadas:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

regras de udev waagent Olá construir um conjunto de links simbólicos em **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


aplicativo Hello pode usar essas informações identificar o dispositivo de disco de inicialização de saudação e disco de recurso (efêmero) hello. No Azure, aplicativos devem consultar muito**/dev/disk/azure/root-part1** ou **/dev/disk/azure-resource-part1** toodiscover essas partições.

Se não houver partições adicionais na lista de blkid hello, eles residem em um disco de dados. Aplicativos podem manter Olá UUID para essas partições e use um caminho como Olá abaixo do nome de dispositivo de saudação toodiscover em tempo de execução:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Obter regras de armazenamento do Azure mais recentes Olá

toohello regras de armazenamento do Azure mais recentes, execute os seguintes comandos:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Para obter mais informações, consulte Olá artigos a seguir:

- [Ubuntu: usando UUID](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: nomenclatura persistente](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: o que UUIDs podem fazer por você](https://www.linux.com/news/what-uuids-can-do-you)

- [UDev: Introdução tooDevice gerenciamento no sistema de Linux modernos](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

