---
title: "Visão geral de aaaRedirect para Gateway de aplicativo do Azure | Microsoft Docs"
description: "Saiba mais sobre a funcionalidade de redirecionamento de saudação no Azure Application Gateway"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Visão geral do redirecionamento do Gateway de Aplicativo

Um cenário comum para muitos aplicativos da web é toosupport automática HTTP tooHTTPS redirecionamento tooensure que toda a comunicação entre o aplicativo e seus usuários ocorre em um caminho criptografado. No Olá anterior, os clientes já utilizada técnicas, como criar um pool de back-end dedicado cujo único propósito é tooredirect solicitações recebidas no tooHTTPS HTTP.  Gateway de aplicativo agora oferece suporte ao tráfego de tooredirect de capacidade em Olá Application Gateway. Isso simplifica a configuração do aplicativo, otimiza o uso do recurso hello e dá suporte a novos cenários de redirecionamento, incluindo global e baseados no caminho de redirecionamento. Suporte ao redirecionamento de Gateway de aplicativo não está limitado tooHTTP -> redirecionamento HTTPS autônomo. Esse é um mecanismo de redirecionamento genérico, que permite o redirecionamento do tráfego recebido no ouvinte de tooanother um ouvinte no Application Gateway. Ele também dá suporte a redirecionamento tooan site externo também. Suporte ao redirecionamento de Gateway de aplicativos oferece Olá recursos a seguir:

1. Redirecionamento global do ouvinte de tooanother um ouvinte no hello Gateway. Isso permite que o redirecionamento de tooHTTPS HTTP em um site.
2. Redirecionamento baseado em caminho. Esse tipo de redirecionamento permite que o redirecionamento de tooHTTPS HTTP somente em uma área do site específico, por exemplo uma área de carrinho de compras é denotado por carrinho / *.
3. Redirecione o site tooexternal.

![redirecionamento](./media/application-gateway-redirect-overview/redirect.png)

Com essa alteração, os clientes precisariam toocreate um novo objeto de configuração de redirecionamento, que especifica o ouvinte de destino Olá ou redirecionamento de toowhich site externo é desejado. elemento de configuração Olá também oferece suporte a opções tooenable acrescentando o caminho de URI hello e URL de redirecionamento toohello de cadeia de caracteres de consulta. Os clientes também podem escolher se o redirecionamento é um redirecionamento temporário (código de status HTTP 302) ou permanente (código de status HTTP 301). Depois de criado essa configuração de redirecionamento é anexado toohello ouvinte de origem por meio de uma nova regra. Ao usar uma regra básica, configuração de redirecionamento hello está associada um ouvinte de origem e é um redirecionamento global. Quando uma regra de caminho é usada, configuração de redirecionamento de saudação é definida no mapa de caminho de URL hello e, portanto, só se aplica toohello área de caminho específico de um site.

### <a name="next-steps"></a>Próximas etapas

[Como configurar o redirecionamento de URL em um gateway de aplicativo](application-gateway-configure-redirect-powershell.md)
