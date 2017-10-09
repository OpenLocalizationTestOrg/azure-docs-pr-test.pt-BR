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
# <a name="accessing-and-using-azure-vm-unique-id"></a>Acessando e usando a ID exclusiva da VM do Azure
A ID exclusiva da VM do Azure é um identificador de 128 bits codificado e armazenado em todos os SMBIOS da VM IaaS do Azure e, atualmente, pode ser lida usando comandos BIOS da plataforma.

A ID exclusiva da VM do Azure é uma propriedade somente leitura. A ID exclusiva da VM do Azure não mudará no desligamento para reinicialização (planejado ou não planejado), no início/parada de desalocação, na recuperação de serviço ou na restauração in-loco. No entanto, se Olá VM for um instantâneo e copiado toocreate uma nova instância, nova ID de VM do Azure está configurado.

> [!NOTE]
> Se você tiver máquinas virtuais mais antigas criadas e, em execução desde que este novo recurso foi distribuído (18 de setembro de 2014), reinicie a VM tooautomatically obter uma ID exclusiva do Azure.
> 
> 

tooaccess ID exclusiva de VM do Azure de dentro de saudação VM:

## <a name="create-a-vm"></a>Criar uma máquina virtual
Para obter mais informações, veja [Criar uma máquina virtual](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-toohello-vm"></a>Conecte-se toohello VM
Para obter mais informações, veja [SSH no Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="query-vm-unique-id"></a>Consultar ID exclusiva da VM
Comando (o exemplo usa o **Ubuntu**):

```bash
sudo dmidecode | grep UUID
```

Exemplo de resultados esperados:

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

Devido a tooBig bit Endian ordenação, hello real ID exclusiva da VM nesse caso será:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

ID exclusiva de VM do Azure pode ser usada em cenários diferentes se hello VM está em execução no Azure ou no local e pode ajudar a seus requisitos de controle geral licenciamento ou relatório que você pode ter suas implantações de IaaS do Azure. Muitos fornecedores independentes de software criar aplicativos e certifica-los no Azure podem exigir tooidentify uma VM do Azure ao longo de seu ciclo de vida e tootell se Olá VM estiver em execução no Azure, local ou em outros provedores de nuvem. Esse identificador de plataforma por exemplo pode ajudar a detectar se o software de saudação é licenciado corretamente ou ajudar toocorrelate qualquer fonte de tooits de dados VM como tooassist sobre a configuração de métricas de direito Olá para plataforma hello e tootrack e correlacionar essas métricas entre outros usos.

