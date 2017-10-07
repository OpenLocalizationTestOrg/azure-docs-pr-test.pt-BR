---
title: aaaUnderstand e resolver erros de WebHCat no HDInsight - Azure | Microsoft Docs
description: Saiba como erros comuns tooabout retornado por WebHCat no HDInsight e tooresolve-los.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>Entenda e resolva erros recebidos do WebHCat no HDInsight

Saiba mais sobre erros recebidos ao usar WebHCat com HDInsight e como tooresolve-los. WebHCat é usado internamente por ferramentas de cliente como o PowerShell do Azure e hello Data Lake Tools para Visual Studio.

## <a name="what-is-webhcat"></a>O que é o WebHCat

O [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) é uma API REST para o [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), uma camada de gerenciamento de armazenamento e tabela para Hadoop. WebHCat está habilitado por padrão em clusters de HDInsight e é usada por vários trabalhos de toosubmit de ferramentas, obter o status do trabalho, etc. sem efetuar login no cluster toohello.

## <a name="modifying-configuration"></a>Modificando a configuração

> [!IMPORTANT]
> Vários erros de saudação listados neste documento ocorrerem porque um máximo configurado foi excedido. Quando a etapa de solução de saudação menciona que você pode alterar um valor, você deve usar uma saudação após tooperform Olá alteração:

* Para **Windows** clusters: Use um valor de saudação do script ação tooconfigure durante a criação do cluster. Para obter mais informações, consulte [Desenvolver ações de script](hdinsight-hadoop-script-actions.md).

* Para **Linux** clusters: valor de saudação toomodify Ambari de uso (web ou a API REST). Para obter mais informações, consulte [Gerenciar o HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="default-configuration"></a>Configuração padrão

Se Olá valores padrão a seguir é excedido, ela pode prejudicar o desempenho do WebHCat ou provocar erros:

| Configuração | O que faz | Valor padrão |
| --- | --- | --- |
| [yarn.scheduler.capacity.maximum-applications][maximum-applications] |Olá número máximo de trabalhos que podem estar ativas simultaneamente (em execução ou pendente) |10.000 |
| [templeton.exec.max-procs][max-procs] |número máximo de saudação de solicitações que podem ser usadas simultaneamente |20 |
| [mapreduce.jobhistory.max-age-ms][max-age-ms] |saudação de número de dias que o histórico de trabalho será retida |7 dias |

## <a name="too-many-requests"></a>Número excessivo de solicitações

**Código de status HTTP**: 429

| Causa | Resolução |
| --- | --- |
| Você excedeu solicitações simultâneas máximas Olá servidas por WebHCat por minuto (padrão de 20) |Reduzir tooensure sua carga de trabalho que você não enviar mais de Olá número máximo de solicitações simultâneas ou aumentar o limite de solicitações simultâneas Olá modificando `templeton.exec.max-procs`. Para obter mais informações, consulte [Modificar a configuração](#modifying-configuration) |

## <a name="server-unavailable"></a>Servidor indisponível

**Código de status HTTP**: 503

| Causa | Resolução |
| --- | --- |
| Esse código de status geralmente ocorre durante o failover entre Olá primário e secundário um nó principal para o cluster de saudação |Aguarde dois minutos e repita a operação de saudação |

## <a name="bad-request-content-could-not-find-job"></a>Conteúdo de solicitação incorreto: não foi possível encontrar o trabalho

**Código de status HTTP**: 400

| Causa | Resolução |
| --- | --- |
| Detalhes do trabalho foram limpos pelo histórico do trabalho Olá Limpador |período de retenção padrão Olá para o histórico de trabalho é 7 dias. período de retenção saudação padrão pode ser alterado modificando `mapreduce.jobhistory.max-age-ms`. Para obter mais informações, consulte [Modificar a configuração](#modifying-configuration) |
| Trabalho foi encerrado devido a failover tooa |Repita o envio de trabalho de backup tootwo minutos |
| Foi usada uma ID de trabalho inválida |Verifique se a id do trabalho hello está correto |

## <a name="bad-gateway"></a>Gateway inválido

**Código de status HTTP**: 502

| Causa | Resolução |
| --- | --- |
| Coleta de lixo interno está ocorrendo em Olá WebHCat processo |Espere toofinish de coleta de lixo ou reinicie o serviço WebHCat de saudação |
| Tempo limite aguardando uma resposta do hello serviço ResourceManager. Esse erro pode ocorrer quando o número de saudação de aplicativos ativos vai máximo configurado de saudação (padrão de 10.000) |Aguarde executando trabalhos toocomplete ou aumentar o limite de trabalho simultâneas de saudação modificando `yarn.scheduler.capacity.maximum-applications`. Para obter mais informações, consulte Olá [configuração modificando](#modifying-configuration) seção. |
| Tentativa de tooretrieve todos os trabalhos por meio de saudação [/jobs. GET](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) chamada ao `Fields` está definido muito`*` |Não recupere *todos* os detalhes do trabalho. Em vez disso, use `jobid` tooretrieve detalhes para trabalhos de maiores somente a certo id do trabalho. Ou não use `Fields` |
| Olá serviço WebHCat está inativo durante o failover de nó principal |Aguarde até dois minutos e repita a operação de saudação |
| Há mais de 500 trabalhos pendentes enviados por meio do WebHCat |Aguarde até que os trabalhos pendentes no momento sejam concluídos antes de enviar mais trabalhos |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
