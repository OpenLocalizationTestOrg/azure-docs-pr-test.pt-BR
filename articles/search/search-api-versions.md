---
title: "versões de aaaAPI da pesquisa do Azure | Microsoft Docs"
description: "Política de versão para a biblioteca de cliente de APIs de REST de pesquisa do Azure e hello no hello .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>Versões de API na Pesquisa do Azure
O Azure Search lança atualizações de recurso regularmente. Às vezes, mas não sempre, essas atualizações exigem toopublish uma nova versão do nosso compatibilidade com versões anteriores do API toopreserve. Publicar uma nova versão permite toocontrol quando e como integrar atualizações de serviço de pesquisa no seu código.

Como regra, tentamos toopublish novas versões somente quando necessário, pois ele pode envolver alguma tooupgrade esforço sua versão de toouse uma nova API de código. Somente, publicaremos uma nova versão se precisamos toochange algum aspecto da saudação API de forma que quebras de compatibilidade com versões anteriores. Isso pode acontecer devido a recursos de tooexisting correções ou devido a novos recursos que alterar a área de superfície de API existente.

Seguimos Olá mesma regra para atualizações SDK. Olá SDK pesquisa do Azure segue Olá [controle de versão semântico](http://semver.org/) regras, que significa que sua versão tem três partes: major, minor e criar número (por exemplo, 1.1.0). Podemos lançará uma nova versão principal do hello SDK somente no caso de alterações que interromper a compatibilidade com versões anteriores. Para atualizações do recurso incondicional, iremos incrementar a versão secundária hello e para correções de bugs é apenas aumentará versão hello.

> [!NOTE]
> Sua instância de serviço de pesquisa do Azure oferece suporte a várias versões da API REST, incluindo hello mais recente. Você pode continuar toouse uma versão quando ela não é mais hello mais recente, mas é recomendável que você migre a sua versão mais recente do código toouse hello. Ao usar o hello API REST, você deve especificar a versão de API de Olá em cada solicitação feita por meio do parâmetro de versão de api de saudação. Ao usar o SDK .NET de saudação, versão de saudação do Olá SDK que você está usando determina versão correspondente de saudação do hello API REST. Se você estiver usando um SDK anterior, você pode continuar toorun que o código sem alterações mesmo se o serviço Olá é atualizado toosupport uma API mais recente versão.

## <a name="snapshot-of-current-versions"></a>Instantâneo das versões atuais
Abaixo está um instantâneo de saudação versões atuais do tooAzure de interfaces de programação todos os pesquisa.

| Interfaces | Versão principal mais recente | Status |
| --- | --- | --- |
| [SDK .NET](https://aka.ms/search-sdk) |3.0 |Disponível, liberado em novembro de 2016 |
| [Preview do SDK do .NET](https://aka.ms/search-sdk-preview) |2.0-preview |Preview, lançada em agosto de 2016 |
| [API REST do Serviço](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |Disponível |
| [Preview da API REST do Serviço](search-api-2015-02-28-preview.md) |2015-02-28-Preview |Visualização |
| [SDK do Gerenciamento do .NET](https://aka.ms/search-mgmt-sdk) |2015-08-19 |Disponível |
| [API REST de gerenciamento](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |Disponível |

Para Olá APIs REST, incluindo Olá `api-version` em cada chamada é necessária. Isso torna fácil tootarget uma versão específica, como uma visualização da API. Olá exemplo a seguir ilustra como Olá `api-version` parâmetro for especificado:

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> Embora cada solicitação tem um `api-version`, recomendamos que você use Olá mesma versão para todas as solicitações de API. Isso ocorre especificamente quando novas versões de API introduzem atributos ou operações que não são reconhecidos por versões anteriores. A combinação de versões de API pode trazer consequências indesejadas e deve ser evitada.
>
> Olá API REST do serviço e a API REST de gerenciamento têm controle de versão independentemente um do outro. Qualquer semelhança nos números de versão é uma coincidência.

Disponível (ou GA) APIs podem ser usados em produção e são o assunto tooAzure contratos de nível de serviço. Versões de visualização têm recursos experimentais que nem sempre são migrados tooa GA versão. **É altamente recomendável não usar APIs de preview em aplicativos de produção.**

## <a name="about-preview-and-generally-available-versions"></a>Sobre versões Prévias e Disponíveis para o Público em Geral
Pesquisa do Azure sempre previamente libera recursos experimentais por meio da API REST de saudação primeiro, em seguida, por meio de versões de pré-lançamento do SDK .NET de saudação.

Não há garantia de recursos de visualização toobe migrados versão tooa GA. Enquanto os recursos em uma versão de GA são considerados estável e improvável toochange com exceção de saudação de pequenas correções de compatibilidade retroativa e aprimoramentos, recursos de visualização estão disponíveis para teste e experimentação, com objetivo de saudação de coletar comentários sobre o design de recurso e a implementação.

No entanto, como recursos de visualização são toochange de assunto, é recomendável em relação a escrever código de produção que leva uma dependência em versões de visualização. Se você estiver usando uma versão mais antiga de visualização, é recomendável migrar versão do toohello disponibilidade geral (GA).

Para Olá SDK .NET: orientação para a migração de código pode ser encontrada em [atualização Olá .NET SDK](search-dotnet-sdk-migration.md).

Disponibilidade geral significa a pesquisa do Azure agora está sob um contrato de nível de serviço (SLA) do hello. Olá SLA pode ser encontrado em [contratos de nível de serviço de pesquisa do Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
