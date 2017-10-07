---
title: "versão mais recente de tooa aaaUpgrade de cluster HDInsight-Azure | Microsoft Docs"
description: "Saiba como tooUpgrade HDInsight cluster tooa nova versão."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>Atualizar a versão mais recente de tooa de cluster do HDInsight
tootake aproveitar Olá recursos mais recentes do HDInsight, é recomendável que os clusters HDInsight seja atualizado toolatest versão. Siga Olá abaixo diretrizes tooupgrade suas versões de cluster HDInsight.

> [!NOTE]
> Os clusters HDInsight da versão 3.2 e 3.3 estão se aproximando da data de desativação. Para obter mais informações sobre a versão com suporte do HDInsight, consulte [Versões de componente do HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).
>
>

## <a name="upgrade-tasks"></a>Tarefas de atualização
Olá fluxo de trabalho tooupgrade HDInsight Cluster é da seguinte maneira.

![Diagrama de fluxo de trabalho de atualização](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. Leia cada seção deste documento toounderstand alterações que podem ser necessárias ao atualizar seu cluster HDInsight.
2. Crie um cluster como um ambiente de teste/garantia de qualidade. Para obter mais informações sobre como criar um cluster, consulte [Saiba como toocreate HDInsight baseados em Linux clusters](hdinsight-hadoop-provision-linux-clusters.md)
3. Cópia existente de trabalhos, fontes de dados e coletores toohello novo ambiente. Consulte [tooTest copiar dados ambiente](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) para obter mais detalhes.
4. Execute testes toomake se os trabalhos funcionam conforme esperado no cluster novo Olá de validação.


Depois de ter verificado que tudo está funcionando conforme o esperado, agende o tempo de inatividade para migração de saudação. Durante esse tempo de inatividade, Olá seguintes ações:

1.  Fazer backup dos dados transitórios armazenados localmente em nós de cluster de saudação. Por exemplo, se você tiver dados armazenados diretamente em um nó principal.
2.  Exclua o cluster existente hello.
3.  Criar um cluster em Olá mesmo VNET sub-rede com mais recente (ou compatíveis) HDI versão usando Olá mesmo repositório de dados padrão que Olá cluster anterior usado. Isso permite Olá novo cluster toocontinue trabalham com os dados de produção existentes.
4.  Importe o backup de todos os dados transitórios.
5.  Iniciar trabalhos/continuar o processamento usando o novo cluster de saudação.

## <a name="next-steps"></a>Próximas etapas
* [Saiba como toocreate HDInsight baseados em Linux clusters](hdinsight-hadoop-provision-linux-clusters.md)
* [Conecte-se tooHDInsight usando SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Gerenciar um cluster baseado em Linux usando o Ambari](hdinsight-hadoop-manage-ambari.md)

