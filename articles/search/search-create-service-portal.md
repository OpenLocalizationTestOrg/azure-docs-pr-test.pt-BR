---
title: "um serviço de pesquisa do Azure no portal de saudação do aaaCreate | Microsoft Docs"
description: "Provisione um serviço de pesquisa do Azure no portal de saudação."
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>Criar um serviço de pesquisa do Azure no portal de saudação

Este artigo explica como toocreate ou provisionar uma pesquisa do Azure do serviço no portal de saudação. Para obter instruções do PowerShell, consulte [Gerenciar o Azure Search com o PowerShell](search-manage-powershell.md).

## <a name="subscribe-free-or-paid"></a>Assinar (gratuito ou pago)

[Abra uma conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) e usar tootry créditos gratuitos out paga serviços do Azure. Depois de créditos são esgotados, manter a conta de saudação e continuar toouse livre serviços do Azure, como sites. Seu cartão de crédito nunca é cobrado a menos que você explicitamente alterar suas configurações e pergunte toobe cobrado.

Alternativamente, você pode [ativar os benefícios de assinante MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Todos os meses, uma assinatura do MSDN lhe oferece créditos que podem ser usados para serviços pagos do Azure. 

## <a name="find-azure-search"></a>Encontrar o Azure Search
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Clique em hello mais sinal ("+") no hello canto superior esquerdo.
3. Selecione **Web + Móvel** > **Azure Search**.

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>Serviço de nome hello e ponto de extremidade de URL

Um nome de serviço é parte do ponto de extremidade de URL Olá emitidas em relação ao qual as chamadas da API. Digite o nome do serviço Olá **URL** campo. 

Requisitos de nome de serviço:
   * Dois a 60 caracteres de comprimento
   * letras minúsculas, dígitos ou traços ("-")
   * Nenhum traço ("-") como Olá 2 primeiro caracteres ou último caractere único
   * sem traços consecutivos ("--")

## <a name="select-a-subscription"></a>Selecionar uma assinatura
Se você tiver mais de uma assinatura, escolha uma que também tenha serviços de armazenamento de arquivos ou dados. A pesquisa do Azure pode detecção automática armazenamento de BLOBs e tabelas do Azure, banco de dados SQL e o banco de dados do Azure Cosmos para indexação por meio de *indexadores*, mas apenas para serviços em Olá mesma assinatura.

## <a name="select-a-resource-group"></a>Selecionar um grupo de recursos
Um grupo de recursos é uma coleção de serviços e recursos do Azure que são usados juntos. Por exemplo, se você estiver usando a pesquisa do Azure tooindex um banco de dados SQL, em seguida, ambos os serviços devem fazer parte de Olá mesmo grupo de recursos.

> [!TIP]
> Excluir um grupo de recursos também exclui serviços hello dentro dele. Para projetos de protótipo utilizando vários serviços, colocando todos eles em hello mesmo grupo de recursos facilita a limpeza após a projeto hello. 

## <a name="select-a-hosting-location"></a>Selecione um local de hospedagem 
Como um serviço do Azure, a pesquisa do Azure podem ser hospedada em data centers ao redor Olá, mundo. Observe que os [preços podem variar](https://azure.microsoft.com/pricing/details/search/) de acordo com a geografia.

## <a name="select-a-pricing-tier-sku"></a>Selecionar um tipo de preço (SKU)
[A Azure Search é oferecida atualmente em vários tipos de preço](https://azure.microsoft.com/pricing/details/search/): Gratuito, Básico ou Standard. Cada tipo tem sua própria [capacidade e limites](search-limits-quotas-capacity.md). Confira [Escolher um tipo de preço ou SKU](search-sku-tier.md) para obter orientações.

Este passo a passo, escolhemos a camada padrão Olá para nosso serviço.

## <a name="create-your-service"></a>Criar seu serviço

Lembre-se toopin seu painel de serviço toohello para facilitar o acesso sempre que você entrar.

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>Dimensione seu serviço
Pode levar alguns toocreate de minutos um serviço (15 minutos ou mais dependendo da camada de saudação). Depois que o serviço é fornecido, você poderá dimensioná-lo toomeet suas necessidades. Como você escolheu a camada padrão Olá para o serviço de pesquisa do Azure, você pode dimensionar seu serviço em duas dimensões: partições e réplicas. Você escolheu camada básica hello, você só pode adicionar réplicas. Se você provisionou o serviço gratuito hello, dimensionamento não está disponível.

***Partições*** permitir que seu serviço toostore e procure por meio de mais documentos.

***Réplicas*** permitir que seu serviço toohandle uma carga maior de consultas de pesquisa.

> [!Important]
> Um serviço deve ter [duas réplicas para o SLA somente leitura e três réplicas para o SLA de leitura/gravação](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

1. Vá tooyour folha de serviço de pesquisa no hello portal do Azure.
2. No painel de navegação esquerdo hello, selecione **configurações** > **escala**.
3. Use Olá slidebar tooadd réplicas ou as partições.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> Cada camada tem diferentes [limites](search-limits-quotas-capacity.md) no número total de saudação de unidades de pesquisa permitidas em um único serviço (réplicas * partições = Total de unidades de pesquisa).

## <a name="when-tooadd-a-second-service"></a>Quando um segundo serviço de tooadd

A grande maioria dos clientes usar apenas um serviço configurado em uma camada que fornece Olá [direita equilíbrio de recursos](search-sku-tier.md). Um serviço pode hospedar vários índices, assunto toohello [limites máximos de camada Olá selecionar](search-capacity-planning.md), com cada índice isolada de outro. Na pesquisa do Azure, solicitações só podem ser direcionado tooone índice, minimizando a chance de saudação acidental ou intencional de recuperação de dados dos outros índices no hello mesmo serviço.

Embora a maioria dos clientes usar um serviço, redundância de serviço pode ser necessária se os requisitos operacionais incluem o seguinte hello:

+ Recuperação de desastre (interrupção do datacenter). A pesquisa do Azure não fornece o failover imediato no evento de saudação de uma interrupção. Para obter recomendações e diretrizes, consulte [Administração de serviço](search-manage.md).
+ A investigação de modelagem de multilocação determinou que o serviços adicionais é design ideal hello. Para obter mais informações, consulte [Design para multilocação](search-modeling-multitenant-saas-applications.md).
+ Para aplicativos globalmente implantados, você pode exigir uma instância da pesquisa do Azure em várias latência toominimize de regiões de tráfego internacional do seu aplicativo.

> [!NOTE]
> No Azure Search, não é possível segregar cargas de trabalho de indexação e de consulta; portanto, você nunca criará vários serviços para cargas de trabalho segregadas. Um índice sempre é consultado sobre serviço Olá no qual ela foi criada (você não pode criar um índice em um serviço e copie-tooanother).
>

Um segundo serviço não é necessário para alta disponibilidade. Alta disponibilidade para consultas é obtida quando você usar 2 ou mais réplicas em Olá mesmo serviço. Atualizações de réplica são sequenciais, o que significa que, pelo menos, uma está operacional quando uma atualização de serviço é distribuída. Para obter mais informações sobre tempo de atividade, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## <a name="next-steps"></a>Próximas etapas
Depois de provisionar um serviço de pesquisa do Azure, você está pronto muito[definir um índice](search-what-is-an-index.md) para que você pode carregar e pesquisar os dados.

tooaccess Olá serviço de código ou script, forneça a URL de saudação (*nome do serviço*. <name>.Search.Windows.NET) e uma chave. Chaves de administração concedem acesso completo; chaves de consulta concedem acesso somente leitura. Consulte [como toouse Azure pesquisar no .NET](search-howto-dotnet-sdk.md) tooget iniciado.

Consulte [Criar e consultar seu primeiro índice](search-get-started-portal.md) para obter um tutorial rápido baseado no portal.

