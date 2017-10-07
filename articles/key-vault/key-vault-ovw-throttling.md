---
ms.assetid: 
title: "diretrizes de limitação de Cofre de chaves de aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a>Diretrizes de limitação do Azure Key Vault

Limitação é um processo que você iniciar o que limita o número de saudação de superutilização de tooprevent de serviço do Azure chamadas simultâneas toohello de recursos. Cofre de chave do Azure (AKV) é projetado toohandle um alto volume de solicitações. Se ocorrer um número excessivo de solicitações, a limitação de solicitações do cliente ajuda a manter o desempenho ideal e a confiabilidade do hello serviço AKV.

Limites de limitação variam com base no cenário de saudação. Por exemplo, se você estiver executando um grande volume de gravações, possibilidade de saudação para limitação é maior do que se você estiver executando apenas leituras.

## <a name="how-does-key-vault-handle-its-limits"></a>Como o Key Vault trata os próprios limites?

Limites de serviço no cofre de chaves há uso indevido de tooprevent de recursos e certifique-se de qualidade de serviço para todos os clientes do cofre da chave. Quando um limite de serviço é excedido, o Key Vault limita quaisquer solicitações adicionais desse cliente por um período de tempo. Quando isso acontece, o Cofre de chaves retorna o código de status HTTP 429 (muito muitas solicitações), e Olá solicitações falhas. Além disso, solicitações com falha que retornam uma contagem 429 para limites Olá controladas pelo Cofre de chaves. 

Se você tiver um caso comercial válido para restrições mais altas, entre em contato conosco.


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a>Como toothrottle seu aplicativo na resposta tooservice limita

Olá seguem **práticas recomendadas** para seu aplicativo de limitação:
- Reduza o número de saudação de operações por solicitação.
- Reduza a frequência de saudação de solicitações.
- Evite tentativas imediatas. 
    - Todas as solicitações se acumulam em relação a seus limites de uso.

Quando você implementa o tratamento de erros do aplicativo, use Olá HTTP Erro código 429 toodetect Olá necessário para limitação do lado do cliente. Se a solicitação de saudação falhar novamente com um código de erro HTTP 429, você ainda está encontrando um limite de serviço do Azure. Continue Olá toouse recomendado o método limitação do lado do cliente, tentar novamente a solicitação de saudação até obter êxito.

### <a name="recommended-client-side-throttling-method"></a>Método recomendado de limitação do lado do cliente

No código de erro HTTP 429, inicie a limitação do cliente usando uma abordagem de retirada exponencial:

1. Aguarde 1 segundo, tente solicitar novamente
2. Se ainda estiver limitado, aguarde 2 segundos e tente a solicitação novamente
3. Se ainda estiver limitado, aguarde 4 segundos e tente a solicitação novamente
4. Se ainda estiver limitado, aguarde 8 segundos e tente a solicitação novamente
5. Se ainda estiver limitado, aguarde 16 segundos e tente a solicitação novamente

Neste ponto, você não deve estar obtendo códigos de resposta HTTP 429.

## <a name="see-also"></a>Consulte também

Para obter uma orientação mais profunda do limitação em Olá Microsoft Cloud, consulte [limitação padrão](https://docs.microsoft.com/azure/architecture/patterns/throttling).

