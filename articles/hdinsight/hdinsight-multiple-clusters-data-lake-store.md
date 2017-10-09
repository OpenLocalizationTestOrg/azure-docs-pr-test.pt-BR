---
title: "aaaUse HDInsight vários clusters com uma conta do repositório Azure Data Lake - Azure | Microsoft Docs"
description: "Saiba como toouse mais de um HDInsight cluster com uma única conta do repositório Data Lake"
keywords: "armazenamento hdinsight, hdfs, dados estruturados, dados não estruturados, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>Usar múltiplos clusters HDInsight com uma conta do Azure Data Lake Store

A partir da versão 3.5 do HDInsight, você pode criar clusters de HDInsight com contas do repositório Azure Data Lake como sistema de arquivos saudação padrão.
O Data Lake Store dá suporte a armazenamento ilimitado, o que o torna ideal não apenas para hospedagem de grandes quantidades de dados, mas também para hospedar vários clusters HDInsight que compartilham uma única conta do Data Lake Store. Para instructionson como toocreate uma HDInsight cluster com repositório Data Lake como armazenamento hello, consulte [HDInsight criar clusters com repositório Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Este artigo fornece ao administrador de armazenamento em Data Lake recomendações toohello para configurar uma única e compartilhada Data Lake armazenar conta que pode ser usado em vários **active** clusters HDInsight. Essas recomendações se aplicam a toohosting Hadoop segura, bem como não seguro vários clusters em uma conta do repositório Data Lake compartilhada.


## <a name="data-lake-store-file-and-folder-level-acls"></a>ACLs no nível de pasta e de arquivo do Data Lake Store

Olá restante deste artigo pressupõe que você tenha um bom conhecimento de nível de arquivo e pasta ACLs no repositório Azure Data Lake, que é descrito em detalhes em [controle de acesso no repositório Azure Data Lake](../data-lake-store/data-lake-store-access-control.md).

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>Configuração do Data Lake Store para vários clusters HDInsight
Vamos levar uma hierarquia de pastas de dois níveis recomendações de saudação do tooexplain para usar múltiplos clusters de HDInsight com uma conta do repositório Data Lake. Considere a possibilidade de ter uma conta do repositório Data Lake com estrutura de pastas de saudação **clusters/Finanças**. Com essa estrutura, todos os clusters Olá exigidos pela organização de finanças Olá podem usar /clusters/finance como local de armazenamento de saudação. Em Olá futuro, se outra organização, digamos que Marketing, quer a clusters de HDInsight toocreate usando Olá a mesma conta de repositório Data Lake, eles podem criar /clusters/marketing. Por enquanto, usaremos apenas **/clusters/finance**.

tooenable este toobe da estrutura de pasta efetivamente usado pelo clusters de HDInsight, administrador do repositório Data Lake Olá deve atribuir as permissões apropriadas, conforme descrito na tabela de saudação. permissões Olá mostradas na tabela Olá correspondem tooAccess ACLs e ACLs não padrão. 


|Pasta  |Permissões  |usuário proprietário  |grupo proprietário  | Usuário nomeado | Permissões de usuário nomeado | Grupo nomeado | Permissões de grupo nomeado |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x--x  |admin |admin  |Entidade de serviço |--x  |FINGRP   |r-x         |
|/clusters | rwxr-x--x |admin |admin |Entidade de serviço |--x  |FINGRP |r-x         |
|/clusters/finance | rwxr-x--t |admin |FINGRP  |Entidade de serviço |rwx  |-  |-     |

Na tabela de saudação

- **administrador** é criador hello e administrador de conta do repositório Data Lake do hello.
- **Entidade de serviço** é hello Azure Active Directory (AAD) entidade de serviço associada à conta de saudação.
- **FINGRP** é um grupo de usuário criado no AAD que contém usuários do hello organização de finanças.

Para obter instruções sobre como toocreate um aplicativo AAD (que também cria uma entidade de serviço), consulte [criar um aplicativo AAD](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application). Para obter instruções sobre como toocreate um grupo de usuários no AAD, consulte [gerenciar grupos no Active Directory do Azure](../active-directory/active-directory-accessmanagement-manage-groups.md).

Tooconsider alguns pontos-chave.

- estrutura de pasta de nível de saudação dois (**/clusters/Finanças/**) deve ser criado e provisionado com as permissões adequadas pelo administrador do repositório Data Lake Olá **antes de** usando a conta de armazenamento Olá para clusters. Essa estrutura não é criada automaticamente durante a criação de clusters.
- exemplo Hello acima recomenda a configuração Olá possui o grupo de **clusters/Finanças** como **FINGRP** e permitindo **r-x** acessar a hierarquia de pasta inteira toohello tooFINGRP iniciando na raiz de saudação. Isso garante que membros de saudação do FINGRP podem navegar a partir da raiz de estrutura de pastas de saudação.
- No caso de Olá quando diferentes entidades de serviço AAD pode criar clusters em **clusters/Finanças**, Olá Autoadesivas bits (quando definido em Olá **Finanças** pasta) garante que as pastas criadas por um serviço Entidade de segurança não pode ser excluída por outros hello.
- Depois que a estrutura de pasta hello e permissões entram em vigor, o processo de criação de cluster HDInsight cria um loaction de armazenamento de cluster específicos em **/clusters/Finanças/**. Por exemplo, armazenamento Olá para um cluster com hello nome fincluster01 poderia ser **/clusters/finance/fincluster01**. Olá propriedade e permissões para pastas de saudação criadas pelo cluster do HDInsight é mostrado na tabela de saudação aqui.

    |Pasta  |Permissões  |usuário proprietário  |grupo proprietário  | Usuário nomeado | Permissões de usuário nomeado | Grupo nomeado | Permissões de grupo nomeado |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/clusters/finanace/ fincluster01 | rwxr-x---  |Entidade de Serviço |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>Recomendações para dados de entrada e saída do trabalho

Nós recomendamos que o trabalho de tooa de dados de entrada e Olá saídas de um trabalho ser armazenado em uma pasta fora **/clusters**. Isso garante que mesmo se a pasta de cluster específico de saudação for excluído tooreclaim espaço de armazenamento, entradas de trabalho de saudação e saídas ainda estão disponíveis para uso futuro. Nesse caso, verifique se hierarquia de pastas Olá para armazenar Olá trabalho entradas e saídas permite que o nível apropriado de acesso para Olá entidade de serviço.

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>Limite de clusters compartilhando uma única conta de armazenamento

limite saudação do número de saudação de clusters que podem compartilhar uma única conta do repositório Data Lake depende da carga de trabalho Olá sendo executada em um desses clusters. Ter muitos clusters ou cargas de trabalho muito pesadas em clusters de saudação que compartilham uma conta de armazenamento pode causar Olá armazenamento conta ingresso/egresso tooget limitada.

## <a name="support-for-default-acls"></a>Suporte para ACLs padrão

Ao criar uma entidade de serviço com acesso de usuário nomeado (conforme mostrado na tabela de saudação acima), é recomendável **não** adicionando Olá-usuário nomeado com um padrão de ACL. O provisionamento de acesso de usuário nomeado usando ACLs padrão resultados na atribuição de saudação do 770 permissões para usuário proprietário, o grupo de propriedade e outros. Embora esse valor padrão de 770 não retire as permissões do usuário proprietário (7) ou grupo proprietário (7), ele retira todas as permissões para outros (0). Isso resulta em um problema conhecido com um determinado caso de uso que é discutido em detalhes no hello [problemas conhecidos e soluções alternativas](#known-issues-and-workarounds) seção.

## <a name="known-issues-and-workarounds"></a>Problemas conhecidos e limitações

Esta seção lista Olá problemas para usar o HDInsight com repositório Data Lake e suas soluções alternativas.

### <a name="publicly-visible-localized-yarn-resources"></a>Recursos localizados do YARN visíveis publicamente

Quando uma nova conta de armazenamento do Azure Data Lake é criada, o diretório raiz de saudação é provisionado automaticamente com too770 de conjunto de bits de permissão de acesso ACL. pasta raiz de saudação possui usuário é definir toohello usuário que criou a conta de hello (Olá repositório Data Lake administrador) e grupo proprietário Olá é definido toohello de grupo primário Olá usuário que criou a conta de saudação. Nenhum acesso é fornecido para "outros".

Essas configurações são conhecidas tooaffect um específico HDInsight caso de uso capturado no [YARN 247](https://hwxmonarch.atlassian.net/browse/YARN-247). Envios de trabalho podem falhar com um toothis semelhante de mensagem de erro:

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

Conforme indicado na Olá que YARN JIRA anteriormente, vinculado ao localizar recursos públicos, hello localizador valida que todos os Olá recursos solicitados são realmente públicos Verificando suas permissões no sistema de arquivos remoto hello. Qualquer LocalResource que não satisfaz essa condição é rejeitado para localização. Olá verificação de permissões, inclui toohello de acesso de leitura de arquivo para "outros". Esse cenário não funciona fora da caixa ao hospedar clusters HDInsight no Azure Data Lake, desde que o Azure Data Lake nega o acesso de todos os demais "outros" no nível da pasta raiz.

#### <a name="workaround"></a>Solução alternativa
Conjunto de leitura-permissões de execução para **outros** pela hierarquia de hello, por exemplo, no  **/** , **/clusters** e **clusters/Finanças**  conforme mostrado na tabela de saudação acima.

## <a name="see-also"></a>Consulte também

* [Criar um cluster HDInsight com o Repositório Data Lake como armazenamento](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


