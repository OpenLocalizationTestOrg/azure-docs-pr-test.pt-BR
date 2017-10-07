---
title: armazenamento moderado de aaaAzure para blobs | Microsoft Docs
description: "As camadas de armazenamento para armazenamento de Blobs do Azure oferecem armazenamento econômico de dados de objetos com base em padrões de acesso. camada de armazenamento moderado de saudação é otimizada para dados acessados com menos frequência."
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 56fae3fdae31a6958ebae01fd96a0366e70ae938
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-and-cool-storage-tiers"></a>Armazenamento de Blobs do Azure: camadas de armazenamento dinâmica e estática
## <a name="overview"></a>Visão geral
O Armazenamento do Azure oferece duas camadas de armazenamento para o armazenamento de objetos de Blobs, para que você possa armazenar os dados de uma maneira mais econômica, dependendo de como os utiliza. Hello Azure **camada de armazenamento hot** é otimizado para armazenar dados acessados com frequência. Hello Azure **camada de armazenamento moderado** é otimizado para armazenar dados pouco acessados e vida longa. Dados na camada de armazenamento moderado Olá podem tolerar um pouco menor disponibilidade, mas ainda exige alta durabilidade e características semelhantes de acesso de tempo e a taxa de transferência como dados dinâmicos. Para os dados estáticos, um SLA com disponibilidade um pouco menor e custos mais altos de acesso são compensações aceitáveis, em troca de custos de armazenamento muito menores.

Atualmente, os dados armazenados na nuvem hello está aumentando em um ritmo exponencial. toomanage custos de suas crescentes necessidades de armazenamento, é útil tooorganize seus dados com base em atributos como a frequência de acesso e planejada período de retenção. Os dados armazenados na nuvem Olá podem ser diferentes em termos de como ele é gerado, processado e acessado por meio de seu ciclo de vida. Alguns dados são ativamente acessados e modificados durante seu ciclo de vida. Alguns dados são acessados com frequência no início de seu tempo de vida, com acesso descartando drasticamente como Olá anos de dados. Alguns dados permanecerá ociosos na nuvem hello e raramente, se nunca, acessada uma vez armazenados.

Cada um dos cenários de acesso a dados descritos acima se beneficia de uma camada diferenciada de armazenamento, otimizada para um padrão de acesso específico. Introdução de saudação de camadas de armazenamento ativa e interessantes, BLOBs do Azure storage agora atende a essa necessidade de camadas de armazenamento diferenciadas com separar modelos de preços.

## <a name="blob-storage-accounts"></a>Contas de armazenamento de Blobs
**Contas de armazenamento de Blobs** são contas de armazenamento especializadas para armazenar dados não estruturados como blobs (objetos) no Armazenamento do Azure. Com contas de armazenamento de Blob, você pode escolher entre toostore de camadas de armazenamento ativa e moderados seus dados acessados com menos frequência moderados a um baixo custo de armazenamento e dados de ativos de armazenamento são acessado com mais frequência um acesso mais baixo custo. Contas de armazenamento de blob são contas de armazenamento de uso geral existentes tooyour semelhantes e compartilham todos os durabilidade ótima hello, disponibilidade, escalabilidade e os recursos de desempenho que você usa atualmente, incluindo a consistência de API de 100% para blobs de bloco e blobs de acréscimo.

> [!NOTE]
> As contas de armazenamento de blobs oferecem suporte apenas aos blobs de bloco e aos blobs de acréscimo, e não aos blobs de página.
> 
> 

Contas de armazenamento de blob expõem Olá **camada de acesso** atributo, que permite a camada de armazenamento Olá toospecify como **acesso** ou **moderado** dependendo dos dados Olá armazenados em Olá conta. Se houver uma alteração no padrão de uso de saudação de seus dados, você também pode alternar entre esses níveis de armazenamento a qualquer momento.

> [!NOTE]
> Camada de armazenamento Olá alteração pode resultar em encargos adicionais. Consulte Olá [preços e faturamento](storage-blob-storage-tiers.md#pricing-and-billing) seção para obter mais detalhes.
> 
> 

Cenários de uso de exemplo para a camada de armazenamento ativa Olá incluem:

* Dados que estão em uso ativo ou toobe esperado acessados (gravados e lidos do) com frequência.
* Dados transferidos para a camada de armazenamento moderado de toohello migração eventual e processamento.

Cenários de uso de exemplo para a camada de armazenamento moderado Olá incluem:

* Conjuntos de dados de backup, arquivamento e recuperação de desastre.
* Conteúdo de mídia mais antigo não exibidos mais frequentemente mas é esperado toobe disponível imediatamente quando acessados.
* Grandes conjuntos de dados que precisam de toobe armazenado custo efetivamente enquanto estão sendo coletados mais dados para processamento futuro. (*por exemplo*, armazenamento de longo prazo de dados científicos; dados brutos de telemetria de uma instalação de manufatura)
* Dados originais (brutos) que devem ser preservados, mesmo após serem processados em formato utilizável final. (*Por exemplo*, arquivos de mídia brutos após transcodificação em outros formatos)
* Dados de conformidade e arquivamento que precisa toobe armazenados por um longo período e quase nunca é acessada. (*por exemplo*, filmagens de câmeras de segurança, raios X/ressonâncias magnéticas antigos para organizações de serviços de saúde, gravações de áudio e transcrições de chamadas de clientes para serviços financeiros)

Confira [Sobre contas de armazenamento do Azure](storage-create-storage-account.md) para saber mais sobre contas de armazenamento.

Para aplicativos que exigem apenas bloqueiam ou anexar o armazenamento de blob, é recomendável usar contas de armazenamento de Blob, tootake aproveitar Olá diferenciados modelo de preços de armazenamento em camadas. No entanto, entendemos que isso talvez não seja possível em determinadas circunstâncias onde usando o armazenamento de propósito geral contas seria Olá toogo de maneira, como:

* É necessário toouse tabelas, filas, ou arquivos e desejar que seus blobs armazenados em Olá a mesma conta de armazenamento. Observe que não há nenhuma vantagem técnica toostoring no Olá a que mesma conta, além de ter Olá mesmo chaves compartilhadas.
* Você ainda precisa de modelo de implantação do toouse Olá clássico. Contas de armazenamento de blob só estão disponíveis por meio do modelo de implantação do Azure Resource Manager hello.
* É necessário toouse blobs de página. As contas de armazenamento de blobs não dão suporte a blobs de página. Geralmente, é recomendável usar blobs de bloco, a menos que você tenha uma necessidade específica para blobs de página.
* Usar uma versão de hello [API de REST de serviços de armazenamento](https://msdn.microsoft.com/library/azure/dd894041.aspx) que é anterior ao 2014-02-14 ou uma biblioteca de cliente com uma versão inferior a 4. x e não é possível atualizar seu aplicativo.

> [!NOTE]
> Contas de armazenamento de Blobs atualmente têm suporte em todas as regiões do Azure.
> 
> 

## <a name="comparison-between-hello-storage-tiers"></a>Comparação entre as camadas de armazenamento Olá
Olá tabela a seguir realça comparação Olá entre duas camadas de armazenamento hello:

<table border="1" cellspacing="0" cellpadding="0" style="border: 1px solid #000000;">
<col width="250">
<col width="250">
<col width="250">
<tbody>
<tr>
    <td><strong><center></center></strong></td>
    <td><strong><center>Camada de armazenamento dinâmica</center></strong></td>
    <td><strong><center>Camada de armazenamento estática</center></strong></td
</tr>
<tr>
    <td><strong><center>Disponibilidade</center></strong></td>
    <td><center>99.9%</center></td>
    <td><center>99%</center></td>
</tr>
<tr>
    <td><strong><center>Disponibilidade<br>(Leituras de RA-GRS)</center></strong></td>
    <td><center>99.99%</center></td>
    <td><center>99.9%</center></td>
</tr>
<tr>
    <td><strong><center>Encargos de uso</center></strong></td>
    <td><center>Custos de armazenamento maiores<br>Custos de acesso e de transações menores</center></td>
    <td><center>Custos de armazenamento menores<br>Custos de acesso e de transações maiores</center></td>
</tr>
<tr>
    <td><strong><center>Tamanho mínimo de objeto<center></strong></td>
    <td colspan="2"><center>N/D</center></td>
</tr>
<tr>
    <td><strong><center>Duração mínima de armazenamento<center></strong></td>
    <td colspan="2"><center>N/D</center></td>
</tr>
<tr>
    <td><strong><center>Latência<br>(Tempo toofirst byte)<center></strong></td>
    <td colspan="2"><center>milissegundos</center></td>
</tr>
<tr>
    <td><strong><center>Metas de escalabilidade e desempenho<center></strong></td>
    <td colspan="2"><center>Igual ao das contas de armazenamento de finalidade geral</center></td>
</tr>
</tbody>
</table>

> [!NOTE]
> Armazenamento de blob contas suporte Olá mesmo destinos de desempenho e escalabilidade, como contas de armazenamento de propósito geral. Confira [Metas de desempenho e de escalabilidade do Armazenamento do Azure](storage-scalability-targets.md) para saber mais.
> 
> 

## <a name="pricing-and-billing"></a>Preços e cobrança
Contas de armazenamento de blob usam um novo modelo de preços para o armazenamento de blob com base na camada de armazenamento de saudação. Ao usar uma conta de armazenamento de Blob, Olá cobrança considerações a seguir se aplicam:

* **Os custos de armazenamento**: além toohello a quantidade de dados armazenados, custo de saudação do armazenamento de dados varia dependendo da camada de armazenamento de saudação. Olá gigabytes custo é menor para a camada de armazenamento moderado Olá que para a camada de armazenamento ativa hello.
* **Os custos de acesso a dados**: para dados na camada de armazenamento moderado hello, será cobrado uma taxa de acesso de dados por gigabyte para leituras e gravações.
* **Custos de transação**: há um encargo por transação para ambas as camadas. No entanto, custo por transação de saudação para a camada de armazenamento moderado Olá é maior do que para a camada de armazenamento ativa hello.
* **Os custos de transferência de dados de replicação geográfica**: isso se aplica apenas tooaccounts com replicação geográfica configurada, incluindo GRS e RA-GRS. A transferência de dados de replicação geográfica acarreta um encargo por gigabyte.
* **Custos de transferência de dados de saída**: transferências de dados de saída (dados que são transferidos para fora de uma região do Azure) acarretam a cobrança por uso de largura de banda por gigabyte, de forma consistente com as contas de armazenamento de finalidade geral.
* **Camada de armazenamento Olá alteração**: alterando a camada de armazenamento de saudação de toohot moderado incorrerá em uma tooreading de custo igual todos os dados de saudação existentes na conta de armazenamento Olá para cada transição. Olá outro lado, alterar a camada de armazenamento de saudação de hot toocool será em gratuito.

> [!NOTE]
> Em ordem tooallow usuários tootry out Olá novas camadas de armazenamento e validar pós-lançamento de funcionalidade, custos Olá para mudar a camada de armazenamento de saudação do toohot moderado serão cobrado desativado até 30 de junho de 2016. A partir de 1º de julho de 2016, o custo de saudação será tooall aplicada transições de toohot moderado. Para obter mais detalhes sobre Olá modelo para contas de armazenamento de Blob de preços, consulte [preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/) página. Para obter mais detalhes sobre os dados de saída de hello encargos de transferência, consulte [detalhes de preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/) página.
> 
> 

## <a name="quick-start"></a>Início rápido
Nesta seção, demonstraremos Olá os seguintes cenários usando Olá portal do Azure:

* Como toocreate uma conta de armazenamento de Blob.
* Como toomanage uma conta de armazenamento de Blob.

### <a name="using-hello-azure-portal"></a>Usando Olá portal do Azure
#### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Criar uma conta de armazenamento de Blob usando Olá portal do Azure
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, selecione **novo** > **dados + armazenamento** > **conta de armazenamento**.
3. Insira um nome para a conta de armazenamento.
   
    Esse nome deve ser exclusivo; ele é usado como parte da URL de saudação usados objetos de saudação tooaccess na conta de armazenamento hello.  
4. Selecione **Gerenciador de recursos** como modelo de implantação de saudação.
   
    Armazenamento em camadas pode ser usado somente com contas de armazenamento do Gerenciador de recursos; Isso é hello recomendado o modelo de implantação para novos recursos. Para obter mais informações, confira Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).  
5. Na lista de lista suspensa de tipo de conta hello, selecione **armazenamento de Blob**.
   
    Isso é onde você pode selecionar o tipo de saudação da conta de armazenamento. Em camadas de armazenamento não está disponível no armazenamento de propósito geral. só está disponível no hello conta do tipo de armazenamento de Blob.     
   
    Observe que, quando você seleciona essa opção, nível de desempenho de saudação é definido tooStandard. Em camadas de armazenamento não está disponível com o nível de desempenho Premium Olá.
6. Selecionar opção de replicação Olá Olá conta de armazenamento: **LRS**, **GRS**, ou **RA-GRS**. saudação padrão é **RA-GRS**.
   
    LRS = armazenamento redundante localmente; GRS = armazenamento com redundância geográfica (2 regiões); RA-GRS é o armazenamento com redundância geográfica com acesso de leitura (2 regiões com leitura acesso toohello segundo).
   
    Para obter mais detalhes sobre as opções de replicação do Armazenamento do Azure, verifique a [Replicação do Armazenamento do Azure](storage-redundancy.md).
7. Nível de armazenamento adequado Olá Select para suas necessidades: Olá conjunto **camada de acesso** tooeither **moderado** ou **acesso**. saudação padrão é **acesso**.
8. Selecione a assinatura Olá no qual você deseja toocreate Olá nova conta de armazenamento.
9. Especifique um novo grupo de recursos ou selecione um grupo de recursos existente. Para saber mais sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
10. Selecione a região Olá para sua conta de armazenamento.
11. Clique em **criar** toocreate conta de armazenamento de saudação.

#### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Alterar a camada de armazenamento de saudação de uma conta de armazenamento de Blob usando Olá portal do Azure
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. conta de armazenamento do toonavigate tooyour, selecione todos os recursos e selecione sua conta de armazenamento.
3. Na folha de configurações de saudação, clique em **configuração** tooview e/ou alteração de configuração de conta hello.
4. Nível de armazenamento adequado Olá Select para suas necessidades: Olá conjunto **camada de acesso** tooeither **moderado** ou **acesso**.
5. Clique em Salvar na parte superior de saudação da folha de saudação.

> [!NOTE]
> Camada de armazenamento Olá alteração pode resultar em encargos adicionais. Consulte Olá [preços e faturamento](storage-blob-storage-tiers.md#pricing-and-billing) seção para obter mais detalhes.
> 
> 

## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>Avaliando e migrando as contas de armazenamento tooBlob
Olá, o objetivo desta seção é toohelp usuários toomake um smooth transição toousing contas de armazenamento de Blob. Há dois cenários de usuário:

* Você tem uma conta de finalidade geral de armazenamento existente e deseja tooevaluate tooa uma alteração de conta de armazenamento de Blob com a camada de armazenamento adequada hello.
* Decidiu toouse uma conta de armazenamento de Blob ou já tiver um e deseja tooevaluate se você deve usar a camada de armazenamento ativa ou moderado hello.

Em ambos os casos, Olá prioritária é tooestimate Olá custo de armazenar e acessar os dados armazenados em uma conta de armazenamento de Blob e comparação que seus custos atuais.

### <a name="evaluating-blob-storage-account-tiers"></a>Avaliando camadas de conta de armazenamento de Blobs
Em ordem tooestimate hello, custo de armazenar e acessar dados armazenados em uma conta de armazenamento de Blob, você será necessário tooevaluate seu padrão de uso existentes ou aproximado seu padrão de uso esperado. Em geral, você desejará tooknow:

* Consumo de armazenamento: quanto dados são armazenados e como isso é alterado mensalmente?
* O armazenamento padrão de acesso - a quantidade de dados está sendo lida do e conta toohello escrito (incluindo os novos dados)? Quantas transações são usadas para acesso a dados e que tipo de transações são elas?

#### <a name="monitoring-existing-storage-accounts"></a>Monitorando contas de armazenamento existentes
toomonitor reunir esses dados e contas de armazenamento existente, você pode fazer uso de análise de armazenamento do Azure que executa logs e fornece dados de métrica para uma conta de armazenamento.
Análise de armazenamento pode armazenar métricas que incluem dados de estatísticas e a capacidade de transações agregadas sobre solicitações toohello serviço de armazenamento de Blob para contas de armazenamento para fins gerais, bem como as contas de armazenamento de Blob.
Esses dados são armazenados em tabelas conhecidas no hello mesma conta de armazenamento.

Para obter mais detalhes, confira [Sobre métricas de análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343258.aspx) e [Esquema de tabela de métricas da análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343264.aspx)

> [!NOTE]
> Contas de armazenamento de blob expõem um ponto de extremidade do serviço de tabela de saudação apenas para armazenar e acessar dados de métricas de saudação para essa conta.
> 
> 

consumo de armazenamento toomonitor Olá para Olá serviço de armazenamento de Blob, você precisará tooenable as métricas de capacidade de saudação.
Com esta opção habilitada, dados de capacidade são gravados diariamente para serviço de Blob de uma conta de armazenamento e registrados como uma entrada de tabela que é gravada toohello *$MetricsCapacityBlob* tabela dentro Olá mesmo conta de armazenamento.

padrão de acesso de dados toomonitor Olá para Olá serviço de armazenamento de Blob, você precisará tooenable Olá transação métricas de hora em um nível de API.
Com esta opção habilitada, por API transações agregadas a cada hora e registradas como uma entrada de tabela que é gravada toohello *$MetricsHourPrimaryTransactionsBlob* tabela dentro Olá mesmo conta de armazenamento. Olá *$MetricsHourSecondaryTransactionsBlob* registros da tabela Olá transações toohello ponto de extremidade secundário no caso de contas de armazenamento de RA-GRS.

> [!NOTE]
> Caso você tenha uma conta de armazenamento para uso geral na qual armazenou discos de máquina virtual e blobs de páginas junto com dados de blob de bloqueio e anexação, esse processo de previsão não se aplica. Isso ocorre porque você terá nenhuma maneira de distinção de capacidade e transação métricas com base apenas no tipo de saudação do blob para bloqueiam e acrescentar blobs que podem ser migrados tooa conta de armazenamento de Blob.
> 
> 

tooget uma boa aproximação do padrão de acesso e consumo de dados, é recomendável escolher um período de retenção para métricas de saudação é representativo do seu uso regular e extrapolar.
Uma opção é dados de métricas de saudação tooretain para 7 dias e os dados de coleta Olá toda semana, para análise no final de saudação do mês de saudação.
Outra opção é dados de métricas de saudação tooretain para Olá últimos 30 dias e de coletar e analisar dados de saudação final de saudação do período de 30 dias hello.

Para obter detalhes sobre como habilitar, coletar e exibir dados de métricas, confira [Habilitando métricas do Armazenamento do Azure e exibindo dados de métricas](storage-enable-and-view-metrics.md).

> [!NOTE]
> O armazenamento, acesso e download de dados de análise também serão cobrados, assim como os dados de usuário comuns.
> 
> 

#### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Utilizando os custos de tooestimate de métricas de uso
##### <a name="storage-costs"></a>Custos de armazenamento
Olá última entrada na tabela de métricas de capacidade de saudação *$MetricsCapacityBlob* com a chave de linha de saudação *'dados'* mostra Olá a capacidade de armazenamento consumida pelos dados de usuário.
Olá última entrada na tabela de métricas de capacidade de saudação *$MetricsCapacityBlob* com a chave de linha de saudação *'análise'* mostra Olá consumida por Olá logs de análise de capacidade de armazenamento.

Essa capacidade total consumida por ambos os logs analíticos e dados de usuário (se habilitado), em seguida, pode ser tooestimate Olá custo de armazenamento de dados na conta de armazenamento Olá usado.
Olá mesmo método também pode ser usado para estimar os custos de armazenamento de bloco e blobs nas contas de armazenamento para fins gerais de acréscimo.

##### <a name="transaction-costs"></a>Custos de transação
soma de saudação do *'TotalBillableRequests'*, todas as entradas para uma API em transação Olá tabela de métricas indica Olá total de transações de API em particular. *Por exemplo,*, Olá número total de *'GetBlob'* transações em um determinado período podem ser calculadas pela soma de saudação do total de solicitações faturáveis para todas as entradas com a chave de linha de saudação *' usuário; GetBlob'*.

Ordem tooestimate os custos de transações para contas de armazenamento de Blob, você precisará toobreak para transações de saudação em três grupos desde que eles são cobrados de forma diferente.

* Transações de gravação, como *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* e *'CopyBlob'*.
* Transações de exclusão, como *'DeleteBlob'* e *'DeleteContainer'*.
* Todas as outras transações.

Ordem tooestimate os custos de transações para contas de armazenamento de uso geral, é necessário tooaggregate todas as transações, independentemente da operação de saudação/API.

##### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Custos de transferência de dados de acesso aos dados e de replicação geográfica
Enquanto a análise de armazenamento não oferece ler quantidade Olá de dados e gravado tooa conta de armazenamento, ele pode ser estimado aproximadamente examinando a tabela de métricas de transação de saudação.
soma de saudação do *'TotalIngress'* todas as entradas para uma API em métricas de transação Olá tabela indica a quantidade total Olá dos dados de entrada em bytes para essa API em particular.
Da mesma forma soma de saudação do *'TotalEgress'* indica a quantidade total de saudação de dados de saída, em bytes.

Ordem tooestimate Olá dados custos de acesso para contas de armazenamento de Blob, você precisará toobreak para transações de saudação em dois grupos.

* quantidade de saudação dados recuperados da conta de armazenamento Olá pode ser estimada examinando a soma de saudação do *'TotalEgress'* para principalmente Olá *'GetBlob'* e *'CopyBlob'* operações.
* quantidade de saudação gravadas toohello conta de armazenamento de dados pode ser estimada examinando a soma de saudação do *'TotalIngress'* para principalmente Olá *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* e *'AppendBlock'* operações.

Olá custo da transferência de dados de replicação geográfica para contas de armazenamento também podem ser calculadas usando estimativa Olá para quantidade Olá dos dados gravados no caso de uma conta de armazenamento GRS ou RA-GRS de Blob.

> [!NOTE]
> Para obter um exemplo mais detalhado sobre como calcular custos de Olá para usar a camada de armazenamento ativa ou moderado Olá, dê uma olhada em Olá perguntas frequentes sobre intitulada *'quais são os níveis de acesso dinâmico e legal e como deve determinar quais um toouse'?* em Olá [página de preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).
> 
> 

### <a name="migrating-existing-data"></a>Migração de dados existentes
Uma conta de Armazenamento de Blobs é especializada no armazenamento exclusivo de blobs de bloco e de acréscimo. Contas de armazenamento de uso geral existentes, que permitem que você toostore tabelas, filas, arquivos e discos, bem como blobs, não podem ser convertido tooBlob contas de armazenamento. toouse Olá camadas de armazenamento, será necessário toocreate novas contas de armazenamento de Blob e migrar os dados existentes em contas Olá recém-criado.

Você pode usar o hello dados existentes de toomigrate métodos a seguir em contas de armazenamento de Blob de dispositivos de armazenamento local, de provedores de armazenamento de nuvem de terceiros ou de suas contas de armazenamento de uso geral existentes no Azure:

#### <a name="azcopy"></a>AzCopy
AzCopy é um utilitário de linha de comando do Windows desenvolvido para alto desempenho cópia dos dados tooand do armazenamento do Azure. Você pode usar AzCopy toocopy dados em sua conta de armazenamento de Blob de suas contas de armazenamento de uso geral existentes ou tooupload de dispositivos de armazenamento local em sua conta de armazenamento de Blob.

Para obter mais detalhes, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).

#### <a name="data-movement-library"></a>Biblioteca de movimentação de dados
Biblioteca do movimento de dados de armazenamento do Azure para .NET baseia-se na estrutura movimentação de dados de núcleo de saudação que habilita o AzCopy. biblioteca de saudação foi projetada para alto desempenho, tooAzCopy semelhante de operações de transferência de dados confiáveis e fácil. Isso permite que os benefícios tootake Olá recursos fornecidos pelo AzCopy em seu aplicativo nativo sem a necessidade de toodeal com em execução e monitoramento de instâncias externas do AzCopy.

Para obter mais detalhes, consulte [Biblioteca de Movimentação dos Dados do Armazenamento do Azure para .Net](https://github.com/Azure/azure-storage-net-data-movement)

#### <a name="rest-api-or-client-library"></a>API REST ou biblioteca de cliente
Você pode criar um aplicativo personalizado toomigrate seus dados em uma conta de armazenamento de Blob usando uma das bibliotecas de cliente do Azure hello ou Olá API REST de serviços de armazenamento do Azure. O Armazenamento do Azure fornece bibliotecas de cliente avançadas para várias linguagens e plataformas, como .NET, Java, C++, Node.JS, PHP, Ruby e Python. bibliotecas de cliente Olá oferecem recursos avançados, como a lógica de repetição, registro em log e carregamentos paralelos. Você também pode desenvolver diretamente em Olá API REST, que podem ser chamados por qualquer linguagem que faz solicitações HTTP/HTTPS.

Para obter mais detalhes, consulte [Introdução ao armazenamento de Blobs do Azure](storage-dotnet-how-to-use-blobs.md).

> [!NOTE]
> BLOBs criptografados usando a criptografia de cliente armazenam metadados relacionados à criptografia armazenado com hello blob. É absolutamente essencial que qualquer mecanismo de cópia deve garantir que Olá metadados de blob e especialmente Olá metadados relacionados à criptografia, será preservado. Se você copiar blobs Olá sem esses metadados, conteúdo de blob Olá não será recuperável novamente. Para obter mais detalhes sobre os metadados relacionados à criptografia, confira [Criptografia no Lado do Cliente do Armazenamento do Azure](storage-client-side-encryption.md).
> 
> 

## <a name="faqs"></a>Perguntas frequentes
1. **As contas de armazenamento existentes ainda estão disponíveis?**
   
    Sim, as contas de armazenamento existentes ainda estão disponíveis, e seus preços ou funcionalidade não foram alterados.  Eles não têm Olá capacidade toochoose uma camada de armazenamento e não terá recursos de camadas no hello futuras.
2. **Por que e quando devo começar a usar contas de armazenamento de Blobs?**
   
    Contas de armazenamento de blob são especializadas para armazenar blobs e nos permitirá toointroduce novos recursos centrados no blob. No futuro, contas de armazenamento de Blob são Olá recomendada em armazenamento de blobs, como recursos futuros como armazenamento hierárquico e camadas será introduzida com base nesse tipo de conta. No entanto, é o tooyou quando você gostaria que toomigrate com base em seus requisitos de negócios.
3. **Pode converter meu tooa de conta de armazenamento conta de armazenamento de Blob existente?**
   
    Não. Conta de armazenamento de blob é um tipo diferente da conta de armazenamento e você precisará toocreate-novo e migrar os dados conforme explicado anteriormente.
4. **Posso armazenar objetos em ambas as camadas de armazenamento em Olá mesma conta?**
   
    Olá *'Camada de acesso'* atributo que indica a camada de armazenamento de saudação é definida em um nível de conta e se aplica a objetos tooall nessa conta. Você não pode definir o atributo de nível de acesso de saudação em nível de objeto.
5. **Posso alterar a camada de armazenamento de saudação da minha conta de armazenamento de Blob?**
   
    Sim. Será toochange capaz de camada de armazenamento Olá por configuração Olá *'Camada de acesso'* atributo na conta de armazenamento hello. Camada de armazenamento Olá alteração será aplicada tooall objetos armazenados na conta de saudação. Camada de armazenamento de saudação de alteração de hot toocool não incorrerá em quaisquer encargos, enquanto a alteração de toohot moderado incorrerá uma por custo GB para ler todos os dados de saudação na conta de saudação.
6. **Frequência alterar a camada de armazenamento de saudação da minha conta de armazenamento de Blob?**
   
    Enquanto estamos não impõem uma limitação na frequência da camada de armazenamento Olá pode ser alterada, esteja ciente de que a alteração de camada de armazenamento Olá toohot moderado incorrerão em significativos encargos. Não é recomendável alterar a camada de armazenamento de saudação com frequência.
7. **Blobs Olá na camada de armazenamento moderado Olá comportará de forma diferente de Olá aqueles na camada de armazenamento ativa Olá?**
   
    BLOBs na camada de armazenamento ativa Olá têm Olá latência mesmo como blobs nas contas de armazenamento de propósito geral. BLOBs na camada de armazenamento moderado Olá tem uma latência semelhante (em milissegundos) como blobs nas contas de armazenamento de propósito geral.
   
    BLOBs na camada de armazenamento moderado Olá terá um ligeiramente menor nível de serviço de disponibilidade (SLA) de saudação blobs armazenados na camada de armazenamento ativa hello. Para obter mais detalhes, confira [SLA para armazenamento](https://azure.microsoft.com/support/legal/sla/storage).
8. **Posso armazenar os blobs de página e discos de máquinas virtuais em contas de armazenamento de Blob?**
   
    As contas de armazenamento de blobs oferecem suporte apenas aos blobs de bloco e aos blobs de acréscimo, e não aos blobs de página. Discos de máquina virtual do Azure são apoiados por blobs de página e consequentemente contas de armazenamento de Blob não podem ser usado toostore discos da máquina virtual. No entanto é possível toostore backups de discos de máquina virtual de saudação como blobs de bloco em uma conta de armazenamento de Blob.
9. **Será necessário toochange minhas contas de armazenamento do Blob de toouse aplicativos existentes?**
   
    Contas de Armazenamento de Blobs são 100% consistentes com API com contas de armazenamento de uso geral para blobs de bloco e de acréscimo. Contanto que seu aplicativo está usando blobs de bloco ou blobs de acréscimo e você estiver usando a versão 2014-02-14 Olá Olá [API de REST de serviços de armazenamento](https://msdn.microsoft.com/library/azure/dd894041.aspx) ou maior do seu aplicativo deve funcionar. Se você estiver usando uma versão mais antiga do protocolo de saudação, em seguida, você precisará tooupdate sua versão nova do aplicativo toouse Olá assim como toowork perfeitamente com os dois tipos de contas de armazenamento. Em geral, é sempre recomendável usar a versão mais recente do hello, independentemente de qual tipo de conta de armazenamento que você usa.
10. **Haverá uma alteração na experiência do usuário?**
    
    Contas de armazenamento de blob são contas de armazenamento de uso geral tooa muito semelhante para o armazenamento de bloco e blobs de acréscimo e dar suporte a todos os recursos principais de saudação do armazenamento do Azure, incluindo alta durabilidade e disponibilidade, escalabilidade, desempenho e segurança. Diferentes contas de armazenamento de tooBlob específico de recursos e as restrições de saudação e suas camadas de armazenamento foram explicadas acima, tudo permanece else hello mesmo.

## <a name="next-steps"></a>Próximas etapas
### <a name="evaluate-blob-storage-accounts"></a>Avaliar as contas de armazenamento de Blobs
[Verificar a disponibilidade das contas de armazenamento de blobs por região](https://azure.microsoft.com/regions/#services)

[Avaliar o uso de suas contas de armazenamento atuais, habilitando as métricas do Armazenamento do Azure](storage-enable-and-view-metrics.md)

[Verificar preços do armazenamento de blobs por região](https://azure.microsoft.com/pricing/details/storage/)

[Verificar os preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Começar a usar as contas de Armazenamento de Blob
[Introdução ao Armazenamento de Blobs do Azure](storage-dotnet-how-to-use-blobs.md)

[Movendo dados tooand do armazenamento do Azure](storage-moving-data.md)

[Transferência de dados com hello AzCopy utilitário de linha de comando](storage-use-azcopy.md)

[Navegue e explore suas contas de armazenamento](http://storageexplorer.com/)

