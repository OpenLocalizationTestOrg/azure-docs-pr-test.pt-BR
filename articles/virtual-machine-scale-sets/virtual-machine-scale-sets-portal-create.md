---
title: "aaaCreate um conjunto de escala de máquinas virtuais usando Olá portal do Azure | Microsoft Docs"
description: Implantar conjuntos de escala usando o portal do Azure.
keywords: "conjuntos de escala de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>Como toocreate um conjunto de escala de máquinas virtuais com hello portal do Azure
Este tutorial mostra como é fácil toocreate um conjunto de escala de máquinas virtuais em apenas alguns minutos, usando Olá portal do Azure. Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Escolha a imagem VM de saudação do marketplace Olá
No portal de saudação, você pode implantar facilmente uma escala com CentOS, CoreOS, Debian, abra Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server ou imagens do Windows Server.

Navega pela primeira vez, toohello [portal do Azure](https://portal.azure.com) em um navegador da web. Clique em `New`, procure `scale set`e, em seguida, selecione Olá `Virtual machine scale set` entrada:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Criar conjunto de escala Olá
Agora você pode usar as configurações padrão de saudação e rapidamente criar conjunto de escala de saudação.

* Em Olá `Basics` folha, insira um nome para o conjunto de escala hello. Esse nome se torna Olá base do hello FQDN saudação do balanceador de carga na frente do conjunto de escala hello, portanto certifique-se de nome hello é exclusivo em todos os Azure.
* Selecione o tipo de OS desejado, insira o nome de usuário desejado e selecione o tipo de autenticação que prefere. Se você escolher uma senha, ela deve ser no mínimo 12 caracteres e atender aos três das quatro seguintes requisitos de complexidade Olá: caractere minúscula, caractere um maiusculo, um número e um caractere especial. Veja mais sobre os [requisitos de nome de usuário e senha](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). Se você escolher `SSH public key`, ser tooonly se colar na sua chave pública, não com sua chave privada:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Escolha se você seria como grupo de posicionamento único tooa de conjunto de escala de saudação toolimit ou se ele deve abranger vários grupos de posicionamento. Permitir que o conjunto de escala Olá toospan grupos de posicionamento permite escala define mais de 100 VMs de capacidade (até too1, 000) com certas limitações. Para obter mais informações, veja [esta documentação](./virtual-machine-scale-sets-placement-groups.md).
* Digite o nome do grupo de recursos desejado e a localização e clique em `OK`.
* Em Olá `Virtual machine scale set service settings` folha: insira o rótulo de nome de domínio desejado (base de saudação de saudação FQDN Olá balanceador de carga na frente do conjunto de escala de saudação). Este rótulo deve ser exclusivo em todo o Azure.
* Escolha a imagem de disco do sistema operacional desejada, a contagem de instâncias e o tamanho da máquina.
* Escolha o tipo de disco desejado: gerenciado ou não. Para obter mais informações, veja [esta documentação](./virtual-machine-scale-sets-managed-disks.md). Se você escolher o conjunto de escala Olá toohave se estender por vários grupos de posicionamento, essa opção não estará disponível porque o disco gerenciado é necessário para grupos de posicionamento de toospan de conjuntos de escala.
* Habilitar ou desabilitar o dimensionamento automático e configurar, se habilitado:

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* Em Olá `Summary` folha, quando a validação é feita, clique em `OK` conjunto de escala de saudação toostart de implantação.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Conecte-se tooa VM no conjunto de escala Olá
Se você escolheu toolimit sua escala definido tooa grupo de posicionamento único, conjunto de escala de saudação é implantado com NAT regras configuradas toolet toohello escala configurar facilmente se conectar (se não, tooconnect toohello VMs em escala Olá definido, você provavelmente precisa toocreate um jumpbox em Olá mesma rede virtual que o conjunto de escala Olá). toosee-los, navegar toohello `Inbound NAT Rules` guia saudação do balanceador de carga para o conjunto de escala hello:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

Você pode conectar tooeach VM em escala Olá definido usando essas regras NAT. Por exemplo, para um conjunto de escala do Windows, se houver uma regra NAT na porta de entrada 50000, você pode conectar toothat máquina via RDP em `<load-balancer-ip-address>:50000`. Para um conjunto de escala do Linux, deveria conectar usando o comando Olá `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Próximas etapas
Para documentação sobre como escala toodeploy define da saudação CLI, consulte [esta documentação](virtual-machine-scale-sets-cli-quick-create.md).

Para documentação sobre como dimensionar toodeploy define do PowerShell, consulte [esta documentação](virtual-machine-scale-sets-windows-create.md).

Para documentação sobre como dimensionar toodeploy define do Visual Studio, consulte [esta documentação](virtual-machine-scale-sets-vs-create.md).

Para obter a documentação geral, confira Olá [página de visão geral da documentação para conjuntos de escala](virtual-machine-scale-sets-overview.md).

Para obter informações gerais, confira Olá [página principal para conjuntos de escala](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

