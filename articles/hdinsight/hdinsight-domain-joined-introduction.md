---
title: "segurança aaaHadoop - domínio clusters HDInsight - Azure | Microsoft Docs"
description: Saiba como...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>Segurança de tooHadoop uma introdução aos clusters de HDInsight ingressado no domínio (visualização)

O Azure HDInsight até hoje dava suporte apenas a um administrador local de usuário único. Isso funcionava bem para equipes de aplicativos ou departamentos menores. Como o Hadoop baseado em cargas de trabalho obtidas mais popularidade no setor, o enterprise Olá Olá necessário para a empresa recursos de classificação, como autenticação, suporte a vários usuários e controle de acesso baseado em função baseada no active directory se tornaram cada vez mais importantes. Usando clusters HDInsight ingressado no domínio, você pode criar um domínio de Active Directory tooan HDInsight cluster associado, configure uma lista de funcionários da empresa de saudação que pode autenticar por meio do Active Directory do Azure toolog no cluster tooHDInsight. Qualquer pessoa fora da empresa Olá não pode logon ou acessam o cluster do HDInsight hello. Olá administrador de empresa pode configurar controle de acesso baseado em função para o uso da segurança de Hive [Apache Ranger](http://hortonworks.com/apache/ranger/), portanto, restringindo o acesso toodata tooonly tanto quanto necessário. Finalmente, Olá administrador pode fazer auditoria de acesso a dados Olá pelos funcionários e quaisquer alterações feitas tooaccess controlar políticas, assim, atingir um alto grau de controle de seus recursos corporativos.

> [!NOTE]
> novos recursos de saudação descritos nesta visualização estão disponíveis somente em clusters HDInsight baseados em Linux para carga de trabalho de Hive. Olá outras cargas de trabalho, como HBase, Spark, tempestade e Kafka, será habilitado em futuras versões.

> [!IMPORTANT]
> O Oozie não está habilitado no HDInsight ingressado no domínio.

## <a name="benefits"></a>Benefícios
I Enterprise Security contém quatro grandes pilares: segurança do perímetro, autenticação, autorização e criptografia.

![Pilares de benefícios de clusters HDInsight associados ao domínio](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png).

### <a name="perimeter-security"></a>Segurança de Perímetro
A segurança de perímetro no HDInsight é obtida usando redes virtuais e serviço de Gateway. Hoje, um administrador de empresa pode criar um cluster HDInsight dentro de uma rede virtual e usar grupos de segurança de rede (regras de firewall de entrada ou saída) toorestrict acesso toohello virtual rede. Apenas hello endereços IP definidos no hello entrada regras de firewall será capaz de toocommunicate com cluster do HDInsight hello, proporcionando assim a segurança de perímetro. Outra camada de segurança de perímetro é obtida com o serviço de Gateway. Olá Gateway é o serviço de saudação que atua como a primeira linha de defesa para qualquer cluster do HDInsight de toohello solicitação entrada. Ele aceita a solicitação de saudação, valida e só permite que Olá solicitação toopass toohello outros nós no cluster, proporcionando assim a segurança de perímetro tooother nós de nome e os dados no cluster hello.

### <a name="authentication"></a>Autenticação
Com essa visualização pública, um administrador de empresa pode provisionar um cluster HDInsight associado ao domínio, em uma [rede virtual](https://azure.microsoft.com/services/virtual-network/). Olá nós do cluster do HDInsight Olá sejam toohello ingressado no domínio gerenciado pela empresa hello. Isso é feito com o uso de [Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md). Todos os nós Olá cluster Olá são tooa ingressado no domínio que gerencia enterprise hello. Com essa configuração, os funcionários da empresa de saudação podem fazer logon toohello nós de cluster usando suas credenciais de domínio. Eles também podem usar seu tooauthenticate de credenciais de domínio com outros pontos de extremidade aprovados como toointeract matiz, modos de exibição do Ambari, ODBC, JDBC, PowerShell e APIs REST com cluster hello. Olá administrador tem controle total sobre limitação Olá número de usuários interagir com o cluster de saudação por esses pontos de extremidade.

### <a name="authorization"></a>Autorização
Uma prática recomendada, seguida pela maioria das empresas é que nem todos os funcionários tem acesso tooall os recursos da empresa. Da mesma forma, com esta versão, Olá administrador pode definir políticas de controle de acesso baseado em função para recursos de cluster de saudação. Por exemplo, Olá administrador pode configurar [Apache Ranger](http://hortonworks.com/apache/ranger/) tooset políticas de controle de acesso para o Hive. Essa funcionalidade garante que os funcionários sejam apenas tooaccess capaz de quantidade de dados que precisam toobe bem-sucedida em seus trabalhos. Cluster de toohello acesso SSH também é restrito toohello somente administrador.

### <a name="auditing"></a>Auditoria
Além de proteger a saudação HDInsight recursos do cluster de usuários não autorizados e dados hello, auditoria de segurança de todos os acessar os recursos de cluster toohello e Olá dados são necessário tootrack acesso não autorizado ou não intencional de recursos de saudação. Com essa visualização, Olá administrador pode exibir e todos os recursos de cluster do HDInsight de toohello de acesso e os dados de relatório. Olá administrador também pode exibir e relatório todas as alterações de políticas de controle de acesso de toohello feitas no Apache Ranger suporte para pontos de extremidade. Um cluster HDInsight domínio usa os logs de auditoria do hello familiares da interface do usuário do Apache Ranger toosearch. No back-end hello, Ranger usa [Solr Apache](http://hortonworks.com/apache/solr/) para armazenar e pesquisa de logs de saudação.

### <a name="encryption"></a>Criptografia
Proteção de dados é importante para os requisitos de conformidade e segurança organizacional de reunião e juntamente com acesso toodata impedir que os funcionários não autorizados, ele também deve ser protegido por criptografia. Ambos Olá repositórios de dados para clusters de HDInsight, blobs de armazenamento do Azure, e o armazenamento do Azure Data Lake suporte transparente no lado do servidor [criptografia de dados](../storage/common/storage-service-encryption.md) em repouso. A proteção de clusters HDInsight funcionará perfeitamente com essa criptografia do lado do servidor de dados em capacidade em repouso.

## <a name="next-steps"></a>Próximas etapas
* Para configurar um cluster HDInsight associado a um domínio, confira [Configurar clusters HDInsight associados a domínio](hdinsight-domain-joined-configure.md).
* Para gerenciar um cluster HDInsight associado a um domínio, confira [Gerenciar clusters HDInsight associados a domínio](hdinsight-domain-joined-manage.md).
* Para configurar políticas do Hive e executar consultas do Hive, confira [Configurar políticas do Hive para clusters HDInsight associados ao domínio](hdinsight-domain-joined-run-hive.md).
* Para executar consultas Hive usando SSH em clusters HDInsight adicionados ao domínio, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
