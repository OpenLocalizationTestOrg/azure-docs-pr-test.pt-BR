---
title: "migração do repositório Data Lake entre regiões de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre a migração entre regiões do Azure Data Lake Store."
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>Migrar o Data Lake Store entre regiões

Como o repositório Azure Data Lake ficar disponível em regiões de novo, você pode escolher toodo uma migração única, tootake aproveitar a nova região de saudação. Saiba quais tooconsider como planejar e concluir a migração de saudação.

## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Para obter mais informações, consulte [Criar sua conta gratuita do Azure hoje mesmo](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do Data Lake Store em duas regiões diferentes**. Para obter mais informações, consulte [Introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Azure Data Factory**. Para obter mais informações, consulte [tooAzure Introdução fábrica de dados](../data-factory/data-factory-introduction.md).


## <a name="migration-considerations"></a>Considerações sobre a migração

Primeiro, identifique a estratégia de migração de saudação que funciona melhor para seu aplicativo que grava, lê ou processa os dados no repositório Data Lake. Quando você escolhe uma estratégia, considere os requisitos de disponibilidade e tempo de inatividade de saudação que ocorre durante a migração do aplicativo. Por exemplo, a abordagem mais simples pode ser o modelo de migração toouse hello "comparação de precisão e shift" nuvem. Nessa abordagem, você pausar aplicativo hello em sua região existente enquanto todos os seus dados são copiados toohello nova região. Quando o processo de cópia de saudação for concluído, retomar seu aplicativo na nova região de saudação e, em seguida, excluir conta de repositório Data Lake antiga hello. Tempo de inatividade durante a migração de saudação é necessário.

tooreduce o tempo de inatividade, você pode começar imediatamente a ingestão de novos dados na nova região de saudação. Quando você tem o mínimo de dados Olá necessário, execute o aplicativo na nova região de saudação. Na tela de fundo Olá, continue dados antigos de toocopy da saudação repositório Data Lake conta toohello novo repositório Data Lake conta existente na nova região de saudação. Usando essa abordagem, você pode fazer Olá comutador toohello nova região com pouco tempo de inatividade. Quando todos os dados antigos de saudação foi copiado, exclua a conta de repositório Data Lake antiga hello.

Tooconsider outros detalhes importantes ao planejar a migração são:

* **Volume de dados**. volume de saudação de dados (em gigabytes, número de saudação de arquivos e pastas e assim por diante) afeta o tempo de saudação e recursos que necessários para a migração de saudação.

* **Nome da conta do Data Lake Store**. nome da nova conta Olá na nova região de saudação deve ser globalmente exclusivo. Por exemplo, nome de saudação da sua conta do repositório Data Lake antiga no Leste dos EUA 2 pode estar contosoeastus2.azuredatalakestore.net. Você poderá nomear sua nova conta do Data Lake Store no Norte da Europa como contosonortheu.azuredatalakestore.net.

* **Ferramentas**. Recomendamos que você use Olá [atividade de cópia do Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) toocopy arquivos de repositório Data Lake. O Data Factory dá suporte à movimentação de dados com alto desempenho e confiabilidade. Tenha em mente que a fábrica de dados copia somente hierarquia de pasta hello e conteúdo dos arquivos de saudação. Você precisa toomanually se aplicam a quaisquer listas de controle de acesso (ACLs) que você usa em Olá antigo toohello nova conta. Para obter mais informações, incluindo as metas de desempenho para cenários mais favorável, consulte Olá [atividade de cópia guia de desempenho e ajuste](../data-factory/data-factory-copy-activity-performance.md). Se você quiser dados copiados mais rapidamente, talvez seja necessário toouse unidades adicionais de movimentação de dados de nuvem. Algumas outras ferramentas, como AdlCopy, não dão suporte à cópia de dados entre regiões.  

* **Encargos de largura de banda**. Os [encargos de largura de banda](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) se aplicam, pois os dados são transferidos para fora de uma região do Azure.

* **ACLs nos dados**. Proteger seus dados na região novo Olá aplicando ACLs toofiles e pastas. Para obter mais informações, consulte [Protegendo dados armazenados no Azure Data Lake Store](data-lake-store-secure-data.md). É recomendável que você use Olá migração tooupdate e ajustar suas ACLs. Talvez você queira toouse configurações tooyour atual configurações semelhantes. Você pode exibir hello ACLs que são aplicadas tooany arquivo usando Olá portal do Azure, [cmdlets do PowerShell](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission), ou SDKs.  

* **Localização dos serviços de análise**. Para melhor desempenho, os serviços de análise, como análise Azure Data Lake ou HDInsight do Azure, devem estar no hello mesma região que seus dados.  

## <a name="next-steps"></a>Próximas etapas
* [Visão geral do Repositório Azure Data Lake](data-lake-store-overview.md)
