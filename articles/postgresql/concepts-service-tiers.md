---
title: "AAA \"As camadas de preços do Azure banco de dados PostgreSQL\""
description: "Tipo de preço no Banco de Dados do Azure para PostgreSQL"
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: article
ms.date: 05/31/2017
ms.openlocfilehash: f10389dd2ad1ff04e83b02786a407c10140a007b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Opções e desempenho do Banco de Dados do Azure para PostgreSQL: Compreenda o que está disponível em cada tipo de serviço
Quando você cria um banco de dados do Azure para o servidor PostgreSQL, você decide três opções principais recursos de saudação tooconfigure alocados para o servidor. Essas opções afetam o desempenho de saudação e a escala do servidor de saudação.
- Tipo de preço 
- Unidades de computação
- Armazenamento (GB)

Cada camada de preços tem um intervalo de desempenho toochoose de níveis (unidades de computação), dependendo dos requisitos de cargas de trabalho. Níveis mais altos de desempenho fornecem recursos adicionais para seu servidor toodeliver projetado maior taxa de transferência. Você pode alterar o nível de desempenho do servidor de saudação dentro de uma camada de preços praticamente sem tempo de inatividade do aplicativo.

> [!IMPORTANT]
> Enquanto o serviço hello está em visualização pública, não há um contrato de nível de serviço (SLA) garantida.

Dentro de um banco de dados do Azure para o servidor MySQL, você pode ter um ou mais bancos de dados. Você pode aceitar toocreate um único banco de dados por servidor tooutilize todos os recursos de hello, ou criar tooshare de bancos de dados de vários recursos hello. 

## <a name="choose-a-pricing-tier"></a>Escolher um tipo de preço
Enquanto estiver no modo visualização, o Banco de Dados do Azure para PostgreSQL oferece apenas as faixas de preço Básico e Padrão. Faixa Premium não está disponível, mas estará disponível em breve. 

Olá tabela a seguir fornece exemplos de saudação camadas melhor adequadas para cargas de trabalho de aplicativo diferente de preços.

| Tipo de preço  | Cargas de trabalho de destino |
| :----------- | :----------------|
| Basic | Mais adequada para cargas de trabalho pequenas que exigem computação e armazenamento escalonáveis sem garantia de IOPS. Os exemplos incluem servidores usados para desenvolvimento ou teste ou aplicativos de pequena escala usados com pouca frequência. |
| Standard | Olá toooption de ir para a nuvem garantem a aplicativos que precisam de IOPS com alta taxa de transferência. Entre os exemplos incluem aplicativos analíticos ou da Web. |
| Premium | Ideal para cargas de trabalho que precisam de baixa latência para transações e IO. Fornece suporte de melhor Olá para muitos usuários simultâneos. Toodatabases aplicável que oferecem suporte a aplicativos de missão crítica.<br />de preço Premium Olá não está disponível na visualização. |

toodecide sobre preço de uma camada, primeira inicialização determinando se sua carga de trabalho precisa de uma garantia IOPS. Nesse caso, use a faixa de preços Padrão.

| **Recursos do tipo de preço** | **Básico** | **Standard** |
| :------------------------ | :-------- | :----------- |
| Unidades de computação máxima | 100 | 800 | 
| Armazenamento total máximo | 1 TB | 1 TB | 
| Garantia IOPS de armazenamento | N/D  | Sim | 
| IOPS de armazenamento máximo | N/D  | 3.000 | 
| Período de retenção do backup de banco de dados | 7 dias | 35 dias | 

Durante o período de visualização Olá, você não pode alterar o tipo de preço após a criação do servidor de saudação. Olá futuras, ele é ser possível tooupgrade ou fazer o downgrade de um servidor de uma camada de tooanother da camada de preços.

## <a name="understand-hello-price"></a>Entender o preço Olá
Quando você cria um novo banco de dados do Azure para PostgreSQL dentro Olá [Portal do Azure](https://portal.azure.com/#create/Microsoft.PostgreSQLServer), clique em Olá **preço** folha e Olá custo mensal aparecerá com base nas opções de saudação selecionado. Se você não tiver uma assinatura do Azure, use Olá tooget de Calculadora de preços do Azure um preço estimado. Visite Olá [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) site, em seguida, clique em **adicionar itens**, expanda Olá **bancos de dados** categoria e escolha **banco de dados do Azure para PostgreSQL** toocustomize opções de saudação.

## <a name="choose-a-performance-level-compute-units"></a>Escolher um nível de desempenho (Unidades de Computação)
Depois de ter determinado Olá camada de preços para seu banco de dados do Azure para o servidor PostgreSQL, você está pronto toodetermine nível de desempenho de saudação selecionando Olá número de unidades de computação necessária. As Unidades de Computação 200 e 400 costumam ser um bom ponto de partida para aplicativos que exigem maior simultaneidade de usuários para suas cargas de trabalho de análise ou da Web e podem ser ajustadas incrementalmente conforme a necessidade. 

Computação unidades são uma medida de taxa de transferência de processamento de CPU que tem a garantia tooa disponível toobe única de banco de dados do Azure para servidor PostgreSQL. Uma unidade de computação é uma medida combinada de recursos de CPU e memória.  Para saber mais, veja [Explicação sobre Unidades de Computação](concepts-compute-unit-and-storage.md)

### <a name="basic-pricing-tier-performance-levels"></a>Níveis de desempenho da faixa de preço Básico:

| **Nível de desempenho** | **50** | **100** |
| :-------------------- | :----- | :------ |
| Unidades de computação máxima | 50 | 100 |
| Tamanho do armazenamento incluído | 50 GB | 50 GB |
| Tamanho máximo de armazenamento do servidor\* | 1 TB | 1 TB |

### <a name="standard-pricing-tier-performance-levels"></a>Níveis de desempenho da faixa de preço Padrão:

| **Nível de desempenho** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| Unidades de computação máxima | 100 | 200 | 400 | 800 |
| Tamanho de armazenamento incluído e IOPS provisionado | 125 GB,<br/> 375 IOPS | 125 GB,<br/> 375 IOPS | 125 GB,<br/> 375 IOPS | 125 GB,<br/> 375 IOPS |
| Tamanho máximo de armazenamento do servidor\* | 1 TB | 1 TB | 1 TB | 1 TB |
| IOPS máximo provisionado do servidor | 3.000 IOPS | 3.000 IOPS | 3.000 IOPS | 3.000 IOPS |
| IOPS máximo provisionado do servidor por GB | 3 IOPS fixos por GB | 3 IOPS fixos por GB | 3 IOPS fixos por GB | 3 IOPS fixos por GB |

\*Tamanho máximo de armazenamento do servidor se refere a tamanho de máximo de armazenamento provisionado de toohello para o servidor.

## <a name="storage"></a>Armazenamento 
configuração de armazenamento de saudação define a quantidade de saudação do armazenamento capacidade disponível tooan banco de dados para o servidor PostgreSQL. armazenamento de saudação usada pelo serviço de saudação inclui arquivos de banco de dados hello, logs de transações e logs do servidor PostgreSQL hello. Considere o tamanho de saudação do armazenamento necessário toohost seus bancos de dados e Olá requisitos de desempenho (IOPS) ao selecionar a configuração de armazenamento de saudação.

Alguma capacidade de armazenamento está incluída no mínimo com cada tipo de preço, indicado na saudação anterior tabela como "Tamanho do armazenamento incluídos". Capacidade de armazenamento adicionais pode ser adicionada ao servidor de saudação é criado, em incrementos de 125 GB, o máximo de armazenamento permitido toohello. capacidade de armazenamento adicional Olá pode ser configurada independentemente da configuração de unidades de computação hello. alterações de preço de saudação com base na quantidade de saudação de armazenamento selecionada.

configuração de IOPS de saudação em cada nível de desempenho relacionado toohello tipo de preço e tamanho de armazenamento Olá escolhido. A faixa Básico não oferece garantia de IOPS. Dentro da faixa de preços padrão Olá, a saudação IOPS dimensionar proporcionalmente toomaximum tamanho de armazenamento em uma taxa fixa de 3:1. armazenamento de saudação incluído de garantia de 125 GB para 375 provisionados IOPS, cada um com um tamanho de e/s de backup too256 KB. Você pode escolher o armazenamento adicional a too1 TB máximo, tooguarantee 3.000 provisionado IOPS.

Monitore o gráfico de métricas Olá Olá Azure portal ou gravação CLI do Azure comandos toomeasure Olá consumo de armazenamento e IOPS. Toomonitor relevante de métricas são o limite de armazenamento, porcentagem de armazenamento, armazenamento usado e porcentagem de e/s.

>[!IMPORTANT]
> Enquanto estiver no modo de visualização, escolha a quantidade de saudação do armazenamento em tempo de saudação quando o servidor de saudação é criado. Ainda não há suporte para a alteração de tamanho de armazenamento de saudação em um servidor existente. 

## <a name="scaling-a-server-up-or-down"></a>Aumentar ou diminuir um único servidor
Inicialmente, você escolhe Olá nível de desempenho e da camada de preços, quando você cria o banco de dados do Azure para PostgreSQL. Posteriormente, você pode dimensionar Olá unidades de computação para cima ou para baixo dinamicamente, dentro do intervalo de saudação do hello mesmo preço. Olá portal do Azure, deslize Olá unidades de computação na folha de camada de preços do servidor de saudação ou script-lo seguindo este exemplo: [monitorar e escala de um único servidor PostgreSQL usando a CLI do Azure](scripts/sample-scale-server-up-or-down.md)

Saudação de computação unidades de escala é feito independentemente do tamanho de armazenamento máximo Olá escolhido.

Em segundo plano hello, alterar o nível de desempenho de saudação do banco de dados cria uma réplica de banco de dados original Olá no novo nível de desempenho hello e alterna conexões toohello réplica. Nenhum dado será perdido durante esse processo. Durante a saudação breve momento em que podemos passar toohello réplica, toohello de conexões de banco de dados estão desabilitadas, portanto, algumas transações em trânsito podem ser revertidas. Essa janela varia, mas é em média inferior a quatro segundos e, em mais de 99% dos casos, de menos de 30 segundos. Se houver grandes números de transações em trânsito em conexões de momento Olá estão desabilitados, esta janela pode ser maior.

duração de saudação do processo de escala inteiro Olá depende do tamanho hello e camada de preços do servidor de saudação antes e depois alterar hello. Por exemplo, um servidor que está sendo alterado unidades de computação na faixa de preços padrão hello, deverá ser concluída dentro de alguns minutos. novas propriedades de servidor Olá Olá não são aplicadas até Olá alterações forem concluídas.

## <a name="next-steps"></a>Próximas etapas
- Para obter mais informações, consulte [Explicando Unidades de Computação](concepts-compute-unit-and-storage.md)
- Saiba como muito[monitorar e escala de um único servidor PostgreSQL usando a CLI do Azure](scripts/sample-scale-server-up-or-down.md)
