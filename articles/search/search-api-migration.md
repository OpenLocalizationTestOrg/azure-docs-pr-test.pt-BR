---
title: "aaaUpgrading toohello API REST de serviço de pesquisa do Azure versão 2016-09-01 | Microsoft Docs"
description: "Atualizando toohello API REST de serviço de pesquisa do Azure versão 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>Atualizando toohello API REST de serviço de pesquisa do Azure versão 2016-09-01
Se você estiver usando a versão 2015-02-28 ou 2015-02-28-visualização de saudação [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), este artigo o ajudará a atualizar seu aplicativo toouse Olá próximo disponível versão da API, 2016-09-01.

Versão 2016-09-01 do hello API REST contém algumas alterações de versões anteriores. Elas são principalmente compatíveis com versões anteriores. Portanto, a alteração do código deve exigir apenas um mínimo de esforço, dependendo da versão que você estava usando antes. Consulte [tooupgrade etapas](#UpgradeSteps) para obter instruções sobre como toochange seu código toouse Olá nova versão da API.

> [!NOTE]
> Sua instância de serviço de pesquisa do Azure oferece suporte a várias versões da API REST, incluindo hello mais recente. Você pode continuar toouse uma versão quando ela não é mais hello mais recente, mas é recomendável que você migre a sua versão mais recente do código toouse hello.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>O que há de novo na versão 2016-09-01
Versão 2016-09-01 é segunda versão disponível Olá de saudação API de REST do serviço de pesquisa do Azure. Os novos recursos nesta versão da API incluem:

* [Analisadores personalizados](https://aka.ms/customanalyzers), que permite a você tootake controle sobre o processo de saudação de conversão de texto em tokens indexáveis e pesquisáveis.
* [Armazenamento de BLOBs do Azure](search-howto-indexing-azure-blob-storage.md) e [armazenamento de tabela do Azure](search-howto-indexing-azure-tables.md) indexadores, que permitem que você tooeasily importar dados do armazenamento do Azure para pesquisa do Azure em uma agenda ou sob demanda.
* [Mapeamentos de campo](search-indexer-field-mappings.md), que permite a você toocustomize como o indexadores importar dados para pesquisa do Azure.
* ETags, que permitem que você tooupdate definições de saudação de índices, indexadores e fontes de dados de uma maneira segura de simultaneidade. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Etapas tooupgrade
Se você estiver atualizando da versão 2015-02-28, você provavelmente não terá toomake qualquer código de tooyour alterações, diferente de número de versão do toochange hello. situações de somente Olá em que talvez seja necessário código toochange são quando:

* O código falha quando propriedades não reconhecidas são retornadas em uma resposta da API. Por padrão, o aplicativo deve ignorar propriedades que não entende.
* O código de persistir as solicitações da API e tenta tooresend-los toohello nova versão da API. Por exemplo, isso pode acontecer se o seu aplicativo persistir tokens de continuação retornados de saudação API de pesquisa (para obter mais informações, procure `@search.nextPageParameters` em Olá [referência de API de pesquisa](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Se qualquer uma destas situações aplicar tooyou, em seguida, talvez seja necessário toochange seu código adequadamente. Caso contrário, nenhuma alteração deve ser necessária a menos que você deseje toostart usando Olá [novos recursos](#WhatsNew) da versão 2016-09-01.

Se você estiver atualizando da versão 2015-02-28-visualização, Olá acima também se aplica, mas você também deve estar ciente de que alguns recursos de visualização não estão disponíveis na versão 2016-09-01:

* Suporte de indexador do Armazenamento de Blobs do Azure para arquivos CSV e blobs que contêm matrizes JSON.
* Sinônimos
* Consultas "Mais como esta"

Se seu código usa esses recursos, não será capaz de tooupgrade too2016-09-01 sem remover o uso deles.

> [!IMPORTANT]
> Lembre-se de que as APIs de visualização servem para teste e avaliação, e não devem ser usadas em ambientes de produção.
> 
> 

## <a name="conclusion"></a>Conclusão
Se você precisar de mais detalhes sobre o uso Olá API de REST do serviço de pesquisa do Azure, consulte Olá atualizado recentemente [referência da API](https://msdn.microsoft.com/library/azure/dn798935.aspx) no MSDN.

Apreciamos seus comentários sobre o Azure Search. Se você encontrar problemas, sinta-se livre tooask nos para obter ajuda sobre Olá [Fórum do MSDN de pesquisa do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) ou [StackOverflow](http://stackoverflow.com/). Se você estiver fazendo uma pergunta sobre o Azure pesquisar em StackOverflow, tootag se tornar com `azure-search`.

Obrigado por usar a Pesquisa do Azure!

