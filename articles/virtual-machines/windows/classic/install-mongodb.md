---
title: aaaInstall MongoDB em uma VM do Windows Azure | Microsoft Docs
description: "Saiba como tooinstall MongoDB em uma VM do Azure criado com o modelo de implantação clássico Olá executando o Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Instalar o MongoDB em uma VM do Windows no Azure
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. tooinstall e configurar usando o modelo de implantação do Gerenciador de recursos de saudação do MongoDB, consulte [neste artigo](../install-mongodb.md).

[O MongoDB][MongoDB] é um popular banco de dados NoSQL de software livre e alto desempenho. Este artigo o orienta pelo processo de criação de uma máquina virtual do Windows Server (VM) usando Olá [portal do Azure][AzurePortal]. Em seguida, você cria e anexar um disco de dados toohello VM antes de instalar e configurar o MongoDB. Se você tiver uma VM existente no Azure que deseja toouse, você pode ir direto muito[instalando e configurando o MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Criar uma máquina virtual na qual o Windows Server está em execução
Siga essas instruções toocreate uma máquina virtual.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> Você pode adicionar um ponto de extremidade para o MongoDB ao criar a máquina virtual de saudação e configurá-lo da seguinte maneira: nome-o como **Mongo**, use **TCP** como protocolo de saudação e defina os dois Olá portas públicas e privadas muito**27017**.
>
>

## <a name="attach-a-data-disk"></a>Anexar um disco de dados
tooprovide armazenamento da máquina virtual de hello, anexar um disco de dados e inicializá-lo para que o Windows pode usá-lo. Se já tiver um disco de dados, você poderá anexar esse disco ou um disco vazio.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Para obter instruções sobre como inicializar disco hello, consulte "como: inicializar um novo disco de dados no Windows Server" em [como tooattach dados de um disco máquina de virtual do Windows tooa](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Instalar e executar o MongoDB na máquina virtual de saudação
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Resumo
Neste tutorial, você aprendeu como toocreate uma máquina virtual executando o Windows Server, se conectam remotamente tooit e anexar um disco de dados.  Você também aprendeu como tooinstall e configurar o MongoDB na máquina virtual baseados em Windows de saudação. Agora você pode acessar o MongoDB na máquina de virtual baseado em Windows hello, por seguintes Olá avançado tópicos Olá [documentação do MongoDB][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

