---
title: aaaCreate um caminho com base em regra - Gateway de aplicativo do Azure - Portal do Azure | Microsoft Docs
description: "Saiba como toocreate uma regra de caminho para um gateway de aplicativo usando Olá portal"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Criar uma regra de caminho para um gateway de aplicativo usando o portal de saudação

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [CLI 2.0 do Azure](application-gateway-create-url-route-cli.md)

Roteamento baseado no caminho de URL permite que você tooassociate rotas com base no caminho de URL de saudação de solicitação Http. Ele verifica se há um pool de back-end de tooa rota configurado para URL Olá listado no hello Application Gateway e envia Olá toohello de tráfego de rede definida pelo pool de back-end. Um uso comum para roteamento baseado em URL é equilibrar solicitações de tooload para pools de toodifferent de diferentes tipos de conteúdo do servidor de back-end.

Roteamento baseado em URL apresenta um novo gateway de tooapplication do tipo de regra. O Gateway de Aplicativo tem dois tipos de regra: básica e com base no caminho. Olá tipo de regra básica, fornece serviço de round-robin para Olá back-end pools ao regras com base no caminho de distribuição de rodízio tooround Além disso, também leva padrão de caminho da URL de solicitação de saudação em consideração ao escolher o pool de back-end apropriado de saudação.

## <a name="scenario"></a>Cenário

Olá cenário a seguir passa por criar uma regra de caminho baseado em um gateway existente do aplicativo.
Olá cenário pressupõe que você já seguiu as etapas de saudação muito[criar um Application Gateway](application-gateway-create-gateway-portal.md).

![roteamento de url][scenario]

## <a name="createrule"></a>Criar regra de caminho baseado Olá

Uma regra de caminho requer seu próprio ouvinte, antes de criar a regra de saudação ser tooverify se você tiver um ouvinte disponível toouse.

### <a name="step-1"></a>Etapa 1

Navegue toohello [portal do Azure](http://portal.azure.com) e selecione um gateway existente do aplicativo. Clique em **Regras**

![Visão geral do Gateway de Aplicativo][1]

### <a name="step-2"></a>Etapa 2

Clique em **baseados no caminho** botão tooadd uma nova regra de caminho baseado.

### <a name="step-3"></a>Etapa 3

Olá **Adicionar regra de caminho com base em** folha tem duas seções. Olá primeira seção é onde você definiu o ouvinte Olá, nome de saudação da regra de saudação e configurações de caminho saudação padrão. configurações de caminho saudação padrão são para rotas que não pertencem a rota Olá personalizados baseados no caminho. Olá a segunda seção do hello **Adicionar regra de caminho com base em** folha é onde você define regras baseadas no caminho Olá próprios.

**Configurações Básicas**

* **Nome** -este valor é uma regra de toohello nome amigável que pode ser acessada no portal de saudação.
* **Ouvinte** -este valor é o ouvinte de saudação que é usado para a regra de saudação.
* **Padrão de pool de back-end** -essa configuração é a configuração de saudação que define Olá toobe de back-end usado para a regra padrão de saudação
* **Configurações de HTTP padrão** -essa configuração é a configuração de saudação que define Olá toobe de configurações de HTTP usado para a regra padrão de saudação.

**Regras com base no caminho**

* **Nome** -este valor é uma regra de toopath com base no nome amigável.
* **Caminhos** -essa configuração define Olá caminho Olá regra procura ao encaminhar o tráfego
* **Pool de back-end** -essa configuração é a configuração de saudação que define Olá toobe de back-end usado para a regra de saudação
* **Configuração de HTTP** -essa configuração é a configuração de saudação que define Olá toobe de configurações de HTTP usado para a regra de saudação.

> [!IMPORTANT]
> Caminhos: lista de saudação de toomatch de padrões de caminho. Cada deve começar com / e coloque-Olá somente um "\*" é permitido é final hello. Exemplos válidos são /xyz, /xyz* ou /xyz/*.  

![Folha Adicionar regra com base no caminho com informações preenchidas][2]

Adicionar uma regra de caminho com tooan gateway existente do aplicativo é um processo fácil por meio do portal hello. Depois que uma regra de caminho tiver sido criada, pode ser editado tooadd mais regras. 

![adicionando mais regras com base no caminho][3]

Essa etapa configura uma rota com base no caminho. É importante toounderstand que solicitações não são reconfiguradas, à medida que solicitações no gateway do aplicativo inspeciona solicitação hello e basic Olá url padrão envia Olá solicitação toohello apropriado back-end.

## <a name="next-steps"></a>Próximas etapas

toolearn como tooconfigure descarregamento de SSL com o Gateway de aplicativo do Azure, consulte [configurar descarregamento de SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
