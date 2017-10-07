---
title: "grupos de segurança de rede aaaCreate - portal do Azure | Microsoft Docs"
description: "Saiba como toocreate e implantar grupos de segurança de rede usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74ecc7db06bb69f2041aa64d7b38b63eb379a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-portal"></a>Criar grupos de segurança usando o portal do Azure de saudação de rede

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação. Você também pode [criar NSGs no modelo de implantação clássico Olá](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

exemplo Hello PowerShell comandos abaixo esperam um ambiente simples já foi criado com base no cenário de saudação acima. Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste Olá implantando [este modelo](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), clique em **implantar tooAzure**, substitua os valores de parâmetro padrão Olá Se necessário e siga as instruções de saudação em Olá portal. Olá etapas a seguir use **NSG RG** como nome de saudação do modelo de saudação de grupo de recursos Olá foi implantada.

## <a name="create-hello-nsg-frontend-nsg"></a>Criar hello NSG NSG-front-end
Olá toocreate **NSG-front-end** NSG conforme mostrado no cenário de saudação acima, siga as etapas de saudação abaixo.

1. Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.
2. Clique em **Procurar >** > **Grupos de segurança de rede**.
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. Em Olá **grupos de segurança de rede** folha, clique em **adicionar**.
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. Em Olá **criar grupo de segurança de rede** folha, criar um NSG denominado *NSG-front-end* em Olá *RG NSG* grupo de recursos e depois clique em **criar**.
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>Criar regras em um NSG existente
regras de toocreate em um NSG existente da saudação portal do Azure, siga as etapas de saudação abaixo.

1. Clique em **Procurar >** > **Grupos de segurança de rede**.
2. Na lista de saudação do NSGs, clique em **NSG-front-end** > **regras de segurança de entrada**
   
    ![Portal do Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. Na lista de saudação do **regras de segurança de entrada**, clique em **adicionar**.
   
    ![Portal do Azure - Adicionar regra](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. Em Olá **Adicionar regra de segurança de entrada** folha, criar uma regra denominada *web regra* com prioridade de *200* permitindo o acesso por meio de *TCP* tooport *80* tooany VM de qualquer fonte e, em seguida, clique em **Okey**. Observe como a maioria destas configurações já é o valor padrão.
   
    ![Portal do Azure - Configurações de regra](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. Depois de alguns segundos, você verá a nova regra Olá no hello NSG.
   
    ![Portal do Azure - Nova regra](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. Repita as etapas too6 toocreate uma regra de entrada denominada *regra rdp* com uma prioridade de *250* permitindo o acesso por meio de *TCP* tooport *3389* tooany VM de qualquer fonte.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Associar Olá NSG toohello front-end sub-rede
1. Clique em **Procurar >** > **Grupos de recursos** > **RG-NSG**.
2. Em Olá **RG NSG** folha, clique em **...**   >  **TestVNet**.
   
    ![Portal do Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. Em Olá **configurações** folha, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **NSG-front-end**.
   
    ![Portal do Azure - Configurações de sub-rede](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. Em Olá **front-end** folha, clique em **salvar**.
   
    ![Portal do Azure - Configurações de sub-rede](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Criar hello back-end NSG NSG
Olá toocreate **back-end NSG** NSG e associá-la toohello **back-end** sub-rede, siga Olá etapas abaixo.

1. Olá Repita as etapas em [criar hello FrontEnd NSG NSG](#Create-the-NSG-FrontEnd-NSG) toocreate um NSG denominado *back-end NSG*
2. Olá Repita as etapas em [criar regras em um NSG existente](#Create-rules-in-an-existing-NSG) toocreate Olá **entrada** regras na tabela de saudação abaixo.
   
   | Regra de entrada | Regra de saída |
   | --- | --- |
   | ![Portal do Azure - regra de entrada](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal do Azure - regra de saída](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. Olá Repita as etapas em [associar sub-rede front-end do hello NSG toohello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate Olá **back-end NSG** NSG toohello **back-end** sub-rede.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[gerenciar NSGs existentes](virtual-network-manage-nsg-arm-portal.md)
* [Habilite o registro em log](virtual-network-nsg-manage-log.md) para NSGs.

