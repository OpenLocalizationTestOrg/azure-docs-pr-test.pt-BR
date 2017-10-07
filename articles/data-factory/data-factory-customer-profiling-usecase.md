---
title: "aaaUse caso - cliente de criação de perfil"
description: "Saiba como o Azure Data Factory é usado toocreate um controlada por dados fluxo de trabalho (pipeline) tooprofile jogos clientes."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>Caso de uso - Criação de perfil de cliente
A fábrica de dados do Azure é um dos Olá de tooimplement muitos serviços usados Cortana pacote de inteligência de aceleradores de solução.  Para obter mais informações sobre o Cortana Intelligence, visite [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics). Neste documento, descrevemos uma toohelp de casos de uso simples começar com noções básicas sobre como o Azure Data Factory pode resolver problemas comuns de análise.

## <a name="scenario"></a>Cenário
A Contoso é uma empresa de jogos que cria os jogos para várias plataformas: PCs (computadores pessoais), dispositivos de mão e consoles de jogos. Conforme players reproduzir esses jogos, grande volume de dados de log é produzido que rastreia Olá padrões de uso, estilo de jogos e preferências do usuário de saudação.  Quando combinado com dados demográficos, regionais, e dados do produto, a Contoso pode executar análise tooguide-los sobre como players de tooenhance experimentam e para direcioná-los para atualizações e de jogos compras. 

Meta da Contoso é tooidentify venda/entre-oportunidades de venda com base no histórico de jogos de saudação do seus players e adicionar o crescimento dos negócios toodrive recursos atraentes e fornecer uma melhor toocustomers de experiência. Para esse caso, usamos uma empresa de jogos como um exemplo de uma empresa. empresa de saudação deseja toooptimize seus jogos com base no comportamento dos jogadores. Esses princípios se aplicam tooany comerciais que deseja tooengage seus clientes em torno de seus produtos e serviços e aprimorar a experiência de seus clientes.

Nesta solução, a Contoso deseja tooevaluate efetividade de saudação de uma campanha de marketing lançou recentemente. Podemos começam com hello jogos bruto logs, o processo e enriquecê-los com dados de localização geográfica, associá-lo com dados de referência de publicidade e finalmente copiá-los em impacto da campanha um banco de dados do Azure SQL tooanalyze hello.

## <a name="deploy-solution"></a>Implantar Solução
Tudo o que você precisa tooaccess e experimentar esse caso de uso simples é um [assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/), uma [conta de armazenamento de BLOBs do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)e um [banco de dados do SQL Azure](../sql-database/sql-database-get-started.md). Implantar o pipeline de saudação de criação de perfil de cliente de saudação **pipelines de exemplo** bloco Olá home page de sua fábrica de dados.

1. Crie uma data factory ou abra uma existente. Consulte [copiar dados de armazenamento de Blob tooSQL banco de dados usando a fábrica de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para etapas toocreate uma fábrica de dados.
2. Em Olá **DATA FACTORY** folha Olá fábrica de dados, clique em Olá **pipelines de exemplo** lado a lado.

    ![Bloco Pipelines de exemplo](./media/data-factory-samples/SamplePipelinesTile.png)
3. Em Olá **pipelines de exemplo** folha, clique em Olá **cliente de criação de perfil** que você deseja toodeploy.

    ![Folha Pipelines de exemplo](./media/data-factory-samples/SampleTile.png)
4. Especifica definições de configuração de exemplo hello. Por exemplo, o nome e a chave da sua conta de Armazenamento do Azure, o nome do Azure SQL Server, o banco de dados, a ID de usuário a e senha.

    ![Folha Exemplo](./media/data-factory-samples/SampleBlade.png)
5. Depois que você especificar configurações de saudação, clique em **criar** toocreate/implantar Olá pipelines de exemplo e usadas pelo pipelines Olá serviços/tabelas vinculadas.
6. Você ver o status de saudação de implantação no bloco do exemplo hello clicado anteriormente Olá **pipelines de exemplo** folha.

    ![Status da Implantação](./media/data-factory-samples/DeploymentStatus.png)
7. Quando você vir Olá **implantação bem-sucedida** mensagem no bloco de saudação do exemplo hello, Olá fechar **pipelines de exemplo** folha.  
8. Em **DATA FACTORY** folha, consulte serviços vinculados, conjuntos de dados e pipelines são adicionados tooyour fábrica de dados.  

    ![Folha Data Factory](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>Visão geral da solução
Esse caso de uso simples pode ser usado como um exemplo de como você pode usar o Azure Data Factory tooingest, preparar, transformar, analisar e publicar dados.

![Fluxos de trabalho completos](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

Esta figura ilustra como Olá pipelines de dados aparecem no hello portal do Azure após terem sido implantados.

1. Olá **PartitionGameLogsPipeline** lê eventos de jogo bruto de saudação do armazenamento de blob e cria partições com base no ano, mês e dia.
2. Olá **EnrichGameLogsPipeline** une os eventos de jogos particionados com dados de referência de código de área geográfica e enriquece dados de saudação mapeando IP endereços toohello correspondentes localizações geográficas.
3. Olá **AnalyzeMarketingCampaignPipeline** pipeline usa dados Olá aprimorada e processa-os com hello toocreate Olá final saída de dados que contém a eficácia do marketing da campanha de publicidade.

Neste exemplo, a fábrica de dados é atividades tooorchestrate usados que copiar dados de entrada, transformação e dados de saudação do processo e de saída tooan de dados final hello Azure SQL Database.  Você também pode visualizar rede Olá pipelines de dados, gerenciá-los e monitorar o status do hello da interface do usuário.

## <a name="benefits"></a>Benefícios
Ao otimizar suas análises de perfil do usuário e o alinhamento com as metas de negócios, empresa de jogos é tooquickly capaz de padrões de uso coletar e analisar Olá eficiência de suas campanhas de marketing.

