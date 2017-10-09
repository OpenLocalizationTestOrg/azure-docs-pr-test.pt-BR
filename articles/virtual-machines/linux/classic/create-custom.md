---
title: "aaaCreate uma VM do Linux clássica usando Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual de Linux com hello Azure CLI 1.0 usando Olá modelo de implantação clássico"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>Como tooCreate uma VM do Linux clássica com hello 1.0 da CLI do Azure
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para a versão do Gerenciador de recursos de hello, consulte [aqui](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este tópico descreve como toocreate uma máquina virtual do Linux (VM) com o uso de hello Azure CLI 1.0 Olá modelo de implantação clássico. Podemos usar uma imagem do Linux do hello disponível **imagens** no Azure. comandos de saudação 1.0 da CLI do Azure oferecem Olá opções de configuração, entre outros:

* Conexão de rede virtual do hello VM tooa
* Adicionar serviço de nuvem existente do hello VM tooan
* Adicionar conta de armazenamento existente do hello VM tooan
* Adicionar conjunto de disponibilidade Olá VM tooan ou local

> [!IMPORTANT]
> Se você quiser toouse sua VM uma rede virtual para que possa conectar tooit diretamente pelo nome de host ou configurar conexões entre locais, certifique-se de que especificar rede virtual hello quando você cria Olá VM. Uma VM pode ser configurado toojoin uma rede virtual somente quando você cria Olá VM. Para mais detalhes sobre redes virtuais, consulte [Visão geral da rede virtual do Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>Como toocreate uma VM do Linux usando Olá modelo de implantação clássico
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

