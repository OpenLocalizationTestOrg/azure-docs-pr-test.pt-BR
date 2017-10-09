---
title: aaaCreate um balanceador de carga interno - portal do Azure | Microsoft Docs
description: "Saiba como toocreate um interno balanceador de carga no Resource Manager usando Olá portal do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>Criar um balanceador de carga interno no hello portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Introdução à criação de um balanceador de carga interno usando o portal do Azure

Use Olá seguir etapas toocreate um balanceador de carga interno de saudação Portal do Azure.

1. Abra um navegador, navegue toohello [portal do Azure](http://portal.azure.com)e entre com sua conta do Azure.
2. No hello superior esquerda da tela hello, clique em **novo** > **rede** > **balanceador de carga**.
3. Em Olá **criar balanceador de carga** folha, insira um **nome** para o balanceador de carga.
4. Em **Esquema**, clique em **Interno**.
5. Clique em **rede Virtual**, e, em seguida, selecione Olá onde você deseja que o balanceador de carga Olá toocreate de rede virtual.

   > [!NOTE]
   > Se você não vir a rede virtual hello, você deseja toouse, verifique Olá **local** você está usando para o balanceador de carga hello e alterá-lo adequadamente.

6. Clique em **sub-rede**e selecione a sub-rede Olá onde você deseja que o balanceador de carga toocreate hello.
7. Em **atribuição de endereço IP**, clique em **dinâmico** ou **estático**, dependendo se você quiser Olá endereço IP para Olá carga toobe da balanceador fixo (estático) ou não.

   > [!NOTE]
   > Se você selecionar toouse um endereço IP estático, você terá tooprovide um endereço Olá balanceador de carga.

8. Em **grupo de recursos** especifique nome de Olá de um novo grupo de recursos para o balanceador de carga hello, ou clique em **selecionar existentes** e selecione um grupo de recursos existente.
9. Clique em **Criar**.

## <a name="configure-load-balancing-rules"></a>Configuração de regras de balanceamento de carga

Após Olá criação de Balanceador de carga, navegue até tooconfigure de recurso de Balanceador de carga toohello-lo.
Você precisará tooconfigure primeiro um pool de endereços de back-end e uma investigação antes de configurar uma regra de balanceamento de carga.

### <a name="step-1-configure-a-back-end-pool"></a>Etapa 1: Configurar um pool de back-end

1. No portal do Azure de Olá, clique em **procurar** > **balanceadores de carga**e, em seguida, clique em balanceador de carga Olá criado acima.
2. Em Olá **configurações** folha, clique em **pools de back-end**.
3. Em Olá **pools de endereços de back-end** folha, clique em **adicionar**.
4. Em Olá **Adicionar pool de back-end** folha, insira um **nome** para pool de back-end hello e clique **Okey**.

### <a name="step-2-configure-a-probe"></a>Etapa 2: Configurar uma investigação

1. No portal do Azure de Olá, clique em **procurar** > **balanceadores de carga**e, em seguida, clique em balanceador de carga Olá criado acima.
2. Em Olá **configurações** folha, clique em **testes**.
3. Em Olá **testes** folha, clique em **adicionar**.
4. Em Olá **adicionar teste** folha, insira um **nome** para investigação hello.
5. Em **Protocolo**, selecione **HTTP** (para os sites da Web) ou **TCP** (para outros aplicativos baseados no TCP).
6. Em **porta**, especifique Olá porta toouse ao acessar a investigação de saudação.
7. Em **caminho** (para HTTP testes somente), especifique Olá caminho toouse como um teste.
8. Em **intervalo** especificar com que frequência tooprobe Olá aplicativo.
9. Em **limite não íntegro**, especifique o número de tentativas devem falhar antes Olá máquina de virtual de back-end está marcada como não íntegra.
10. Clique em **Okey** toocreate investigação.

### <a name="step-3-configure-load-balancing-rules"></a>Etapa 3: Configurar regras de balanceamento de carga

1. No portal do Azure de Olá, clique em **procurar** > **balanceadores de carga**e, em seguida, clique em balanceador de carga Olá criado acima.
2. Em Olá **configurações** folha, clique em **regras de balanceamento de carga**.
3. Em Olá **regras de balanceamento de carga** folha, clique em **adicionar**.
4. Em Olá **regra de balanceamento de carga de adicionar** folha, insira um **nome** para regra de saudação.
5. Em **Protocolo**, selecione **HTTP** (para os sites da Web) ou **TCP** (para outros aplicativos baseados no TCP).
6. Em **porta**, especificar tooin balanceador de carga de saudação de conexão de clientes de porta de saudação.
7. Em **porta de back-end**, especifique Olá porta toobe usado no pool de back-end de saudação (geralmente, porta do balanceador de carga hello e a porta de back-end de saudação são Olá mesmo).
8. Em **pool de back-end**, selecione Olá back-end pool que você criou anteriormente.
9. Em **persistência de sessão**, selecione como você deseja toopersist sessões.
10. Em **tempo limite de ociosidade (minutos)**, especifique o tempo limite de ociosidade hello.
11. Em **IP flutuante (retorno de servidor direto)**, clique em **Desabilitado** ou **Habilitado**.
12. Clique em **OK**.

## <a name="next-steps"></a>Próximas etapas

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)

