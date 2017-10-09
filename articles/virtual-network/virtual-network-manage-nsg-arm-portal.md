---
title: "aaaManage NSGs usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toomanage existente NSGs usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Gerenciar os NSGs usando o portal de saudação

> [!div class="op_single_selector"]
> * [Portal](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [CLI do Azure](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Recuperar informações
Você pode exibir seus NSGs existentes, recuperar regras para um NSG existente e descobrir a quais recursos um NSG está associado.

### <a name="view-existing-nsgs"></a>Exibir NSGs existentes

tooview todos os existentes NSGs em uma assinatura, Olá concluir as etapas a seguir:

1. Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.

2. Clique em **Procurar >** > **Grupos de segurança de rede**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Verifique a lista de saudação do NSGs em hello **grupos de segurança de rede** folha.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Exibir NSGs em um grupo de recursos

lista de saudação do tooview de NSGs em Olá **NSG RG** grupo de recursos, Olá concluir as etapas a seguir:

1. Clique em **Grupos de recursos >** > **RG-NSG** > **...**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. Na lista de saudação de recursos, observe para itens de exibição de ícone do NSG hello, conforme mostrado no hello **recursos** folha abaixo.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Listar todas as regras de um NSG

regras de saudação tooview de um NSG denominado **NSG-front-end**completa Olá seguintes etapas:

1. De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.

2. Em Olá **configurações** , clique em **regras de segurança de entrada**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Olá **regras de segurança de entrada** folha é exibida conforme mostrado abaixo.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. Em Olá **configurações** , clique em **regras de segurança de saída** toosee Olá regras de saída.

    > [!NOTE]
    > tooview regras do padrão, clique em Olá **padrão regras** no hello superior da folha de saudação que exibe as regras de saudação.
    >

### <a name="view-nsgs-associations"></a>Exibir associações de NSGs

tooview Olá quais recursos **NSG-front-end** NSG está associado ao e completa Olá etapas a seguir:

1. De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.

2. Em Olá **configurações** , clique em **sub-redes** tooview que sub-redes são associados toohello NSG.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. Em Olá **configurações** , clique em **interfaces de rede** tooview quais NICs são associados toohello NSG.

## <a name="manage-rules"></a>Gerenciar regras
Você pode adicionar regras tooan existente NSG, editar regras existentes e remova regras.

### <a name="add-a-rule"></a>Adicionar uma regra
tooadd uma regra permitindo **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, Olá concluir as etapas a seguir:

1. De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.
2. Em Olá **configurações** , clique em **regras de segurança de entrada**.
3. Em Olá **regras de segurança de entrada** folha, clique em **adicionar**. Em seguida, no hello **Adicionar regra de segurança de entrada** folha, preencher valores hello, conforme mostrado abaixo e, em seguida, clique em **Okey**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Depois de alguns segundos, observe a nova regra Olá no hello **regras de segurança de entrada** folha.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Alterar uma regra
regra de saudação toochange criada acima tooallow Olá o tráfego de entrada **Internet** Olá completa, somente as etapas a seguir:

1. De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.
2. Em Olá **configurações** , clique em regra Olá criada acima.
3. Em Olá **https permitir** folha, alteração Olá **fonte** propriedade conforme mostrado abaixo e depois clique em **salvar**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Excluir uma regra

toodelete Olá regra criada acima e completa Olá etapas a seguir:

1. De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.
2. Em Olá **configurações** , clique em regra Olá criada acima.
3. Em Olá **https permitir** folha, clique em **excluir**e, em seguida, clique em **Sim**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>Gerenciar associações
Você pode associar um NSG toosubnets e placas de rede. Você também pode desassociar um NSG de qualquer recurso ao qual ele esteja associado.

### <a name="associate-an-nsg-tooa-nic"></a>Associar um NSG tooa NIC
Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, Olá concluir as etapas a seguir:

1. De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.
2. Em Olá **configurações** , clique em **interfaces de rede** > **associar** > **TestNICWeb1**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Desassociar um NSG de uma NIC

Olá toodissociate **NSG-front-end** NSG de saudação **TestNICWeb1** NIC, Olá concluir as etapas a seguir:

1. De Olá portal do Azure, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestNICWeb1**.

2. Em Olá **TestNICWeb1** folha, clique em **alterar a segurança...**   >  **Nenhum**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> Você também pode usar esta folha tooassociate Olá NIC tooany, existente NSG.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Desassociar um NSG de uma sub-rede

Olá toodissociate **NSG-front-end** NSG de saudação **front-end** sub-rede, Olá concluir as etapas a seguir:

1. De Olá portal do Azure, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestVNet**.

2. Em Olá **configurações** folha, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **Nenhum**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. Em Olá **front-end** folha, clique em **salvar**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Associar uma sub-rede de tooa NSG

Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, Olá concluir as etapas a seguir:

1. De Olá portal do Azure, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestVNet**.
2. Em Olá **configurações** folha, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **NSG-front-end**.
3. Em Olá **front-end** folha, clique em **salvar**.

> [!NOTE]
> Você também pode associar uma sub-rede de tooa NSG de thh NSG **configurações** folha.
>

## <a name="delete-an-nsg"></a>Excluir um NSG
Você só pode excluir um NSG se ela não está associada tooany recursos. toodelete um NSG, Olá concluir as etapas a seguir:.

1. De Olá portal do Azure, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **NSG-front-end**.
2. Em Olá **configurações** folha, clique em **interfaces de rede**.
3. Se houver qualquer NICs listadas, clique Olá NIC e siga a etapa 2 [dissociar um NSG de uma NIC](#Dissociate-an-NSG-from-a-NIC).
4. Repita a etapa 3 para cada NIC.
5. Em Olá **configurações** folha, clique em **sub-redes**.
6. Se não houver nenhuma sub-rede listada, clique em sub-rede hello e siga as etapas 2 e 3 em [dissociar um NSG de uma sub-rede](#Dissociate-an-NSG-from-a-subnet).
7. Rola esquerdo toohello **NSG-front-end** folha, em seguida, clique em **excluir** > **Sim**.

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Próximas etapas
* [Habilitar registro em log](virtual-network-nsg-manage-log.md) para NSGs.
