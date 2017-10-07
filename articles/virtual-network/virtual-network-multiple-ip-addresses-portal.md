---
title: "aaaMultiple endereços IP para máquinas virtuais do Azure - Portal | Microsoft Docs"
description: "Saiba como tooassign vários endereços IP tooa máquina virtual usando Olá portal do Azure | Gerenciador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Atribuir vários máquinas de toovirtual de endereços IP usando Olá portal do Azure

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
Este artigo explica como toocreate uma máquina virtual (VM) por meio de saudação do Azure Resource Manager implantação do modelo usando Olá portal do Azure. Tooresources criado por meio do modelo de implantação clássico Olá não podem ser atribuídos a vários endereços IP. toolearn mais sobre modelos de implantação do Azure, leia Olá [entender os modelos de implantação](../resource-manager-deployment-model.md) artigo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Criar uma VM com vários endereços IP

Se você quiser toocreate uma VM com vários endereços IP ou um endereço IP privado estático, você deve criá-lo usando o PowerShell ou Olá CLI do Azure. Clique como Olá PowerShell ou opções de CLI na parte superior de saudação do toolearn neste artigo. Você pode criar uma VM com um único endereço IP privado dinâmico e (opcionalmente) um único endereço IP público usando o portal de hello, seguindo as etapas de Olá Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [criar uma VM do Linux](../virtual-machines/linux/quick-create-portal.md) artigos. Depois de criar hello VM, você pode alterar o tipo de endereço IP de saudação de toostatic dinâmico e adicionar mais endereços IP usando o portal de saudação seguindo as etapas em Olá [tooa VM de endereços de IP adicionar](#add) deste artigo.

## <a name="add"></a>Adicionar endereços IP tooa VM

Você pode adicionar pública e privada tooa de endereços IP NIC completando as etapas de saudação que seguem. Olá exemplos Olá seções a seguir pressupõem que você já tem uma máquina virtual com configurações de IP hello três descritas em hello [cenário](#Scenario) neste artigo, mas ele não é necessário que você faça.

### <a name="coreadd"></a>Principais etapas

1. Procure toohello portal do Azure em https://portal.azure.com e entrar nele, se necessário.
2. No portal de saudação, clique em **mais serviços** > tipo *máquinas virtuais* Olá caixa de filtro e, em seguida, clique em **máquinas virtuais**.
3. Em Olá **máquinas virtuais** folha, clique em Olá VM que você deseja tooadd IP endereços. Clique em **interfaces de rede** na folha da máquina virtual Olá que aparece e rede hello, em seguida, selecione interface que você deseja tooadd Olá IP endereços. No exemplo hello mostrado no hello após a imagem, Olá NIC denominado *myNIC* de saudação VM denominada *myVM* é selecionado:

    ![Interface de rede](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. Olá folha que aparece para Olá NIC que você selecionou, clique em **as configurações de IP**.

Olá concluído as etapas em uma das seções de saudação que seguem, com base no tipo de saudação do endereço IP que você deseja tooadd.

### <a name="add-a-private-ip-address"></a>**Adicionar um endereço IP privado**

Concluir Olá etapas tooadd um novo endereço IP privado a seguir:

1. Olá concluir as etapas em Olá [principais etapas](#coreadd) deste artigo.
2. Clique em **Adicionar**. Em Olá **configuração Adicionar IP** folha que aparece, criar uma configuração de IP denominada *4 IPConfig* com *10.0.0.7* como um *estático* IP privado de endereço, em seguida, clique em **Okey**.

    > [!NOTE]
    > Ao adicionar um endereço IP estático, você deve especificar um endereço válido, não utilizado em Olá Olá de sub-rede que NIC está conectada ao. Se o endereço de saudação que você selecionar não estiver disponível, portal Olá mostrará um X para o endereço IP hello e você precisará tooselect um diferente.

3. Depois de clicar em Okey, folha Olá será fechado e você verá Olá nova configuração de IP listada. Clique em **Okey** tooclose Olá **configuração Adicionar IP** folha.
4. Você pode clicar em **adicionar** tooadd configurações de IP adicionais, ou feche todos os endereços IP adicionando folhas toofinish.
5. IP privado de saudação adicionar endereços toohello sistema de operacional VM por etapas para seu sistema operacional no Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.

### <a name="add-a-public-ip-address"></a>Adicionar um endereço IP público

Um endereço IP público é adicionado ao associar um tooeither de recurso de endereço IP público, uma nova configuração de IP ou uma configuração de IP existente.

> [!NOTE]
> Endereços IP públicos têm um valor nominal. toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura. mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.
> 

### <a name="create-public-ip"></a>Criar um recurso de endereço IP público

Um endereço IP público é uma configuração para um recurso de endereço IP público. Se você tiver um recurso de endereço IP público que não é atualmente associados tooan configuração de IP que você deseja tooassociate configuração de IP tooan, ignorar Olá etapas a seguir e conclua as etapas de saudação em uma saudação próximas seções, você precisa. Se você não tiver um recurso de endereço IP público disponível, conclua Olá toocreate etapas um a seguir:

1. Procure toohello portal do Azure em https://portal.azure.com e entrar nele, se necessário.
3. No portal de saudação, clique em **novo** > **rede** > **endereço IP público**.
4. Em Olá **criar endereço IP público** folha que aparece, digite um **nome**, selecione um **atribuição de endereço IP** tipo, uma **assinatura**, um **Grupo de recursos**e um **local**, em seguida, clique em **criar**, conforme mostrado na figura abaixo de saudação:

    ![Criar um recurso de endereço IP público](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Olá concluir as etapas em uma das seções de saudação que seguem tooassociate Olá pública recurso tooan IP configuração do endereço IP.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Associar Olá pública recurso tooa novo IP configuração de endereço IP

1. Olá concluir as etapas em Olá [principais etapas](#coreadd) deste artigo.
2. Clique em **Adicionar**. Em Olá **configuração Adicionar IP** folha que aparece, criar uma configuração de IP denominada *4 IPConfig*. Habilitar Olá **endereço IP público** e selecione um existente, disponível público recurso de endereço IP da saudação **escolher endereço IP público** folha que aparece.

    Depois que você selecionou um recurso de endereço IP público hello, clique em **Okey** e folha Olá será fechada. Se você não tiver um endereço IP público existente, você pode criar um completando as etapas de saudação do hello [criar um recurso de endereço IP público](#create-public-ip) deste artigo. 

3. Revisão Olá nova configuração de IP. Mesmo que um endereço IP privado não foi atribuído explicitamente, um deles foi atribuído automaticamente toohello configuração de IP, porque todas as configurações de IP devem ter um endereço IP privado.
4. Você pode clicar em **adicionar** tooadd configurações de IP adicionais, ou feche todos os endereços IP adicionando folhas toofinish.
5. Adicionar Olá privada IP endereço toohello VM sistema operacional concluindo as etapas de saudação para seu sistema operacional no hello [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo. Não adicione Olá pública IP endereço toohello sistema operacional.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Associar Olá pública recurso tooan existente IP configuração de endereço IP

1. Olá concluir as etapas em Olá [principais etapas](#coreadd) deste artigo.
2. Clique em configuração de IP hello para que deseja tooadd Olá público recurso de endereço IP.
3. Na folha de IPConfig Olá que aparece, clique em **endereço IP**.
4. Em Olá **escolher endereço IP público** folha que aparece, selecione um endereço IP público.
5. Clique em **salvar** e folhas de saudação serão fechada. Se você não tiver um endereço IP público existente, você pode criar um completando as etapas de saudação do hello [criar um recurso de endereço IP público](#create-public-ip) deste artigo.
3. Revisão Olá nova configuração de IP.
4. Você pode clicar em **adicionar** tooadd configurações de IP adicionais, ou feche todos os endereços IP adicionando folhas toofinish. Não adicione Olá pública IP endereço toohello sistema operacional.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
