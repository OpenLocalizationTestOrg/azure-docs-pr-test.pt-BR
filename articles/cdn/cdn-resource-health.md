---
title: "integridade de saudação aaaMonitor de recursos do Azure CDN | Microsoft Docs"
description: "Saiba como toomonitor Olá a integridade de seus recursos de CDN do Azure usando a integridade de recursos do Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a>Monitorar a integridade de recursos do Azure CDN Olá
  
A Azure CDN Resource Health é um subconjunto de [Azure Resource Health](../resource-health/resource-health-overview.md).  Você pode usar a integridade do recurso do Azure integridade toomonitor Olá dos recursos CDN e receber problemas de tootroubleshoot orientação acionáveis.

>[!IMPORTANT] 
>Integridade de recursos do Azure CDN contas somente no momento para integridade de saudação de entrega do CDN global e recursos da API.  A integridade de recursos do Azure CDN não verifica a pontos de extremidade de CDN individuais.
>
>sinais de saudação de feed de integridade de recursos do Azure CDN podem ser up too15 minutos atrasados.

## <a name="how-toofind-azure-cdn-resource-health"></a>Como toofind integridade de recursos do Azure CDN

1. Em Olá [portal do Azure](https://portal.azure.com), procurar tooyour perfil CDN.

2. Clique em Olá **configurações** botão.

    ![Botão Configurações](./media/cdn-resource-health/cdn-profile-settings.png)

3. Em *Suporte + solução de problemas*, clique em **Integridade de recursos**.

    ![Integridade de recursos de CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>Você também pode encontrar recursos CDN listados em Olá *integridade de recursos* lado a lado no hello *ajuda + suporte* folha.  Você pode obter rapidamente muito*ajuda + suporte* clicando hello dentro de um círculo **?** no hello canto superior direito do portal de saudação.
>
> ![Ajuda + suporte](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Mensagens específicas do Azure CDN

Integridade de recursos CDN status tooAzure relacionados pode ser encontrada abaixo.

|Mensagem | Ação recomendada |
|---|---|
|Você pode ter parado, removido ou configurado de forma errada um ou mais dos seus pontos de extremidade de CDN | Você pode ter parado, removido ou configurado de forma errada um ou mais dos seus pontos de extremidade de CDN.|
|Infelizmente, Olá serviço de gerenciamento de CDN está disponível no momento | Marque aqui para atualizações de status; Se o problema persistir após Olá esperado tempo de resolução, contate o suporte.|
|Infelizmente, os pontos de extremidade de CDN podem ser afetados por problemas existentes com alguns dos nossos provedores de CDN | Marque aqui para atualizações de status; Usar toolearn de ferramenta de solução de problemas de saudação como tootest sua origem e o ponto de extremidade CDN; Se o problema persistir após Olá esperado tempo de resolução, contate o suporte. |
|Infelizmente, as alterações de configuração de ponto de extremidade de CDN estão sofrendo atrasos de propagação | Marque aqui para atualizações de status; Se as alterações de configuração não são totalmente propagadas em tempo de saudação esperado, contate o suporte.|
|Infelizmente, que estamos enfrentando problemas ao carregar o portal suplementar Olá | Marque aqui para atualizações de status; Se o problema persistir após Olá esperado tempo de resolução, contate o suporte.|
Infelizmente, estamos tendo problemas com alguns dos nossos provedores de CDN | Marque aqui para atualizações de status; Se o problema persistir após Olá esperado tempo de resolução, contate o suporte. |

## <a name="next-steps"></a>Próximas etapas

- [Acesse a visão geral do Azure Resource Health](../resource-health/resource-health-overview.md)
- [Solucione problemas com a compactação de arquivo de CDN](./cdn-troubleshoot-compression.md)
- [Solucione problemas com erros 404](./cdn-troubleshoot-endpoint.md)