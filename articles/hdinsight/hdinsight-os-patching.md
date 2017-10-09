---
title: "agendamento de aplicação de patch aaaConfigure OS clusters HDInsight baseados em Linux - Azure | Microsoft Docs"
description: "Saiba como clusters de agendamento de aplicação de patch tooconfigure SO para HDInsight baseados em Linux."
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>Aplicação de patch no HDInsight 
Como um serviço gerenciado do Hadoop, HDInsight cuida de aplicação de patch Olá SO de saudação VMs subjacentes usadas pelo clusters de HDInsight. A partir de 1º de agosto de 2016, alteramos política aplicação de patch de sistema operacional do convidado de saudação para clusters HDInsight baseados em Linux (versão 3.4 ou superior). meta de saudação da nova política de saudação é toosignificantly reduzir o número de saudação de reinicializações toopatching vencimento. nova política de saudação continuará toopatch máquinas virtuais () no Linux clusters toda segunda-feira ou quinta-feira, começando em 12: 00 UTC em uma sobreposição entre nós em qualquer cluster específico. No entanto, qualquer determinada VM reiniciará apenas no máximo uma vez a cada 30 dias, devido a aplicação de patch tooguest sistema operacional. Além disso, a primeira reinicialização Olá para um cluster recém-criado não ocorrerá mais 30 dias a partir da data de criação de cluster hello. Patches será efetivos quando Olá VMs são reiniciadas.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>Como tooconfigure Olá agenda de aplicação de patch de sistema operacional para clusters HDInsight baseados em Linux
máquinas virtuais de saudação em um cluster HDInsight necessário toobe ocasionalmente reinicializado para que os patches de segurança importante que podem ser instalados. A partir de 1º de agosto de 2016, novos clusters HDInsight baseados em Linux (versão 3.4 ou superior) serão reiniciados usando Olá agenda a seguir:

1. Uma máquina virtual no cluster Olá só pode reinicializar para patches no máximo, uma vez dentro de um período de 30 dias.
2. reinicialização de saudação ocorre iniciando em 12: 00 UTC.
3. processo de reinicialização de saudação é gradativa máquinas virtuais em cluster hello, para que o cluster Olá ainda está disponível durante o processo de reinicialização de saudação.
4. a primeira reinicialização Olá para um cluster recém-criado não ocorrerá mais 30 dias após a data de criação de cluster hello.

Usando a ação de script hello descrita neste artigo, você pode modificar agendamento de aplicação de patch Olá SO da seguinte maneira:
1. Habilitar ou desabilitar reinicializações automáticas
2. Frequência de saudação do conjunto de reinicialização (dias entre reinicializações)
3. Definir Olá dia da semana hello quando ocorre uma reinicialização

> [!NOTE]
> Essa ação de script só funcionará com clusters HDInsight baseados em Linux criados após 1º de agosto de 2016. Os patches terão efeito somente após a reinicialização das VMs. 
>

## <a name="how-toouse-hello-script"></a>Como toouse Olá script 

Quando usar esse script requer Olá informações a seguir:
1. Olá local do script: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight usa esse URI toofind e execute o script de saudação em todas as máquinas virtuais de saudação em cluster hello.
  
2. Olá tipos de nós de cluster que o script hello é aplicado a: um nó principal, workernode, zookeeper. Esse script deve ser tooall aplicados tipos de nós no cluster de saudação. Se não for o tipo de nó tooa aplicado, em seguida, Olá virtual máquinas para esse tipo de nó continuarão a agenda de aplicação de patch anterior toouse hello.


3.  Parâmetro: esse script aceita três parâmetros numéricos:

    | . | Definição |
    | --- | --- |
    | Habilitar/desabilitar reinicializações automáticas |0 ou 1. Um valor 0 desabilita reinicializações automáticas, enquanto 1 habilita as reinicializações automáticas. |
    | Frequência |too90 7 (inclusivo). número de saudação de toowait dias antes de reinicializar as máquinas virtuais de saudação patches que exigem uma reinicialização. |
    | Dia da semana |1 too7 (inclusivo). Um valor de 1 indica reinicialização Olá deve ocorrer em uma segunda-feira e 7 indica um exemplo de Sunday.For, usando parâmetros de 1 a 2 de 60 resulta em automático reinicia a cada 60 dias (no máximo) na terça-feira. |
    | Persistência |Ao aplicar um cluster existente do tooan de ação de script, você pode marcar script hello persistente. Scripts persistentes são aplicadas quando workernodes novos são adicionados toohello cluster por meio de operações de dimensionamento. |

> [!NOTE]
> Você deve marcar este script persistente ao aplicar o cluster existente tooan. Caso contrário, novos nós criados por meio de operações de dimensionamento usará o padrão de saudação agenda de aplicação de patch.
Se você aplicar o script hello como parte do processo de criação de cluster hello, ele é mantido automaticamente.
>

## <a name="next-steps"></a>Próximas etapas

Para etapas específicas sobre como usar a ação de script hello, Olá Olá seções a seguir, consulte [usando a ação de script de clusters de HDInsight com base em Personalizar Linuz](hdinsight-hadoop-customize-cluster-linux.md):

* [Usar uma ação de script durante a criação do cluster](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [Aplicar um tooa de ação de script executando cluster](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
