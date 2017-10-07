---
title: "aaaCreate uma VM com um endereço IP público estático - portal do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM com um estático público endereço IP usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>Criar uma VM com um endereço IP público estático usando Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [CLI do Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modelo](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Clássico)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>Criar uma VM com um IP público estático

endereço de uma VM com um endereço IP público estático toocreate em Olá portal do Azure, Olá concluir as etapas a seguir:

1. Em um navegador, navegue toohello [portal do Azure](https://portal.azure.com) e, se necessário, entre com sua conta do Azure.
2. No canto superior esquerdo de saudação do portal de saudação, clique em **novo**>>**de computação**>**Windows Server 2012 R2 Datacenter**.
3. Em Olá **selecionar um modelo de implantação** , selecione **Gerenciador de recursos de** e clique em **criar**.
4. Em Olá **Noções básicas de** folha, insira informações de VM Olá, conforme mostrado abaixo e, em seguida, clique em **Okey**.
   
    ![Portal do Azure - Noções básicas](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. Em Olá **escolher um tamanho de** folha, clique em **A1 padrão** conforme mostrado abaixo e, em seguida, clique em **selecione**.
   
    ![Portal do Azure - Escolha um tamanho](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. Em hello **configurações** folha, clique em **endereço IP público**, em seguida, em hello **criar endereço IP público** folha, em **atribuição**, clique em **Estático** conforme mostrado abaixo. E em seguida, clique em **OK**.
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. Em Olá **configurações** folha, clique em **Okey**.
8. Saudação de revisão **resumo** folha, conforme mostrado abaixo e depois clique em **Okey**.
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Observe o novo bloco Olá no seu painel.
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. Quando Olá VM é criada, Olá **configurações** folha será exibida conforme mostrado abaixo
    
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

