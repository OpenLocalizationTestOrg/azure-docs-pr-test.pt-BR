---
title: "aaaOverview do repositório Azure Data Lake | Microsoft Docs"
description: "Entender o que é o valor de repositório Azure Data Lake e hello fornece sobre repositórios de dados"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Visão geral do Repositório Azure Data Lake
O Repositório Azure Data Lake é um repositório em hiper-escala corporativo para cargas de trabalho de análise de big data. Azure Data Lake permite toocapture dados de qualquer velocidade de tamanho, tipo e inclusão em um único local para análise operacional e exploratória.

> [!TIP]
> Saudação de uso [repositório Data Lake aprendizado](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) toostart Explorando o serviço de repositório Azure Data Lake hello.
> 
> 

Repositório Azure Data Lake pode ser acessado do Hadoop (disponível com o cluster HDInsight) usando Olá WebHDFS compatível com APIs de REST. É especificamente projetado tooenable análise em dados armazenado de saudação e é ajustado para desempenho para cenários de análise de dados. Fora da caixa hello, ele inclui todos os recursos de nível empresarial Olá — segurança, capacidade de gerenciamento, escalabilidade, confiabilidade e disponibilidade — essencial para casos de uso de empresa do mundo real.

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Alguns dos recursos principais de saudação do hello Azure Data Lake incluem o seguinte hello.

### <a name="built-for-hadoop"></a>Desenvolvido para Hadoop
armazenamento do Azure Data Lake Olá é um sistema de arquivos do Apache Hadoop compatível com Hadoop distribuídas arquivo de sistema (HDFS) e funciona com o ecossistema de Hadoop de saudação.  Aplicativos de HDInsight ou serviços que usam Olá WebHDFS API existente podem facilmente integrar repositório Data Lake. O Repositório Data Lake também expõe uma interface REST compatível com WebHDFS para os aplicativos

Os dados armazenados no Repositório Data Lake podem ser facilmente analisados usando estruturas de análise Hadoop, como o MapReduce ou o Hive. Clusters do Microsoft Azure HDInsight podem ser provisionados e configurado toodirectly acessar dados armazenados no repositório Data Lake.

### <a name="unlimited-storage-petabyte-files"></a>Armazenamento ilimitado, arquivos em petabytes
O Repositório Azure Data Lake fornece armazenamento ilimitado e é adequado para armazenar vários dados para análise. Ele não impõe qualquer limite de tamanhos de conta, tamanhos de arquivos ou quantidade de saudação de dados que podem ser armazenados em um data lake. Arquivos individuais podem variar de toopetabytes KB de tamanho tornando uma ótima opção toostore qualquer tipo de dados. Dados são armazenados permanentemente fazendo várias cópias e não há nenhum limite na duração de saudação do tempo para qual Olá dados podem ser armazenados em lake de dados hello.

### <a name="performance-tuned-for-big-data-analytics"></a>Desempenho ajustado para a análise de big data
Repositório Azure Data Lake é criado para executar sistemas analíticos que exigem a taxa de transferência de grandes tooquery e analisar grandes quantidades de dados de grande escala. lake de dados Olá espalha partes de um arquivo em um número de servidores de armazenamento individual. Isso melhora a saudação taxa de transferência de leitura ao ler arquivo hello em paralelo para executar a análise de dados.

### <a name="enterprise-ready-highly-available-and-secure"></a>Pronto para a empresa: altamente disponível e seguro
O Repositório Azure Data Lake fornece confiabilidade e disponibilidade padrão do setor. Os ativos de dados são armazenados de forma duradoura fazendo cópias redundantes tooguard contra falhas inesperadas. As empresas podem usar o Azure Data Lake em suas soluções como uma parte importante de suas plataformas de dados atuais.

Repositório data Lake também fornece segurança de classe empresarial para dados armazenado de saudação. Para saber mais, consulte [Protegendo dados no Repositório Azure Data Lake](#DataLakeStoreSecurity).

### <a name="all-data"></a>Todos os dados
O Repositório Azure Data Lake pode armazenar quaisquer dados em formato nativo, como estão, sem exigir transformações prévias. Repositório data Lake não exigem um toobe esquema definido antes do carregamento de dados hello, deixando-os dados de saudação do toohello framework analíticos individuais toointerpret e defina um esquema em tempo de saudação da análise de saudação. Sendo toostore capaz de arquivos de formatos e tamanhos arbitrários torna possível para o repositório Data Lake toohandle estruturado, dados estruturados e não estruturados.

Os contêineres para dados do Repositório Azure Data Lake são basicamente pastas e arquivos. Operar em dados Olá armazenado usando SDKs, o Portal do Azure e o Azure Powershell. Como colocar seus dados no repositório de saudação usando essas interfaces e contêineres apropriados hello, você pode armazenar qualquer tipo de dados. Repositório data Lake não executa nenhuma manipulação especial de dados com base no tipo de saudação de dados que ele armazena.

## <a name="DataLakeStoreSecurity"></a>Protegendo os dados no Repositório Azure Data Lake
Repositório Azure Data Lake usa o Azure Active Directory para autenticação e listas de controle de acesso (ACLs) toomanage acessar tooyour dados.

| Recurso | Descrição |
| --- | --- |
| Autenticação |Repositório Azure Data Lake integra-se com o Azure Active Directory (AAD) para o gerenciamento de identidade e acesso para todos os dados de saudação armazenados no repositório Azure Data Lake. Devido à integração hello, benefícios do Azure Data Lake de todos os recursos do AAD, incluindo autenticação multifator, acesso condicional, controle de acesso baseado em função, o monitoramento de uso do aplicativo, segurança de monitoramento e alertas, etc. Repositório Azure Data Lake dá suporte a saudação protocolo OAuth 2.0 para autenticação com na interface REST do hello. |
| Controle de acesso |Repositório Azure Data Lake fornece controle de acesso, dando suporte a permissões de estilo POSIX expostas pelo Olá WebHDFS protocolo. Em Olá Data Lake repositório Public Preview (versão atual do hello), as ACLs podem ser habilitadas na pasta raiz de hello, subpastas e arquivos individuais. Para saber mais sobre como funcionam as ACLs no contexto do Data Lake Store, veja [Controle de acesso no Data Lake ](data-lake-store-access-control.md). |
| Criptografia |Repositório data Lake também fornece criptografia de dados que são armazenados na conta de saudação. Você pode especificar configurações de criptografia Olá durante a criação de uma conta do repositório Data Lake. Você pode escolher toohave seus dados criptografados ou optar por sem criptografia. Para obter mais informações sobre como tooprovide relacionadas à criptografia configuração, consulte [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md). |

Deseja toolearn mais sobre como proteger os dados no repositório Data Lake. Siga os links de saudação abaixo.

* Para obter instruções sobre como toosecure dados no repositório Data Lake, consulte [proteção de dados no repositório Azure Data Lake](data-lake-store-secure-data.md).
* Prefere vídeos? [Assista a este vídeo](https://mix.office.com/watch/1q2mgzh9nn5lx) em como toosecure dados armazenados no repositório Data Lake.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Aplicativos compatíveis com o Repositório Azure Data Lake
Repositório Azure Data Lake é compatível com os componentes de origem abertos no ecossistema do Hadoop hello. Ele também se integra perfeitamente com outros serviços do Azure. Isso torna o Repositório Data Lake uma opção perfeita para suas necessidades de armazenamento de dados. Siga os links de saudação abaixo toolearn mais informações sobre como o repositório Data Lake pode ser usado com os componentes de software livre, bem como outros serviços do Azure.

* Confira [Aplicativos e serviços compatíveis com o Repositório Azure Data Lake](data-lake-store-compatible-oss-other-applications.md) para obter uma lista de aplicativos de software livre interoperáveis com o Repositório Data Lake.
* Consulte [integração com outros serviços do Azure](data-lake-store-integrate-with-other-services.md) toounderstand como repositório Data Lake pode ser usado com outros Azure services tooenable uma grande variedade de cenários.
* Consulte [cenários para usar o repositório Data Lake](data-lake-store-data-scenarios.md) toolearn como toouse Data Lake armazenam em cenários como ingestão de dados, processamento de dados, fazer download de dados e visualização de dados.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>O que é o sistema de arquivos do Azure Data Lake Store (adl://)?
Repositório data Lake podem ser acessados por meio do novo sistema de arquivos de hello, Olá AzureDataLakeFilesystem (publicitário: / /), em ambientes de Hadoop (disponíveis com o cluster HDInsight). Aplicativos e serviços que usam publicitário: / são tootake capaz de aproveitar mais otimização de desempenho que não estão disponíveis em WebHDFS. Como resultado, fornece repositório Data Lake Olá tooeither flexibilidade se beneficiar melhor desempenho de saudação com hello recomendado a opção de usar publicitário: / / ou manter o código existente pelo continuando toouse Olá WebHDFS API diretamente. HDInsight do Azure aproveita totalmente Olá AzureDataLakeFilesystem tooprovide Olá melhor desempenho no repositório Data Lake.

Você pode acessar seus dados Olá repositório Data Lake usando `adl://<data_lake_store_name>.azuredatalakestore.net`. Para obter mais informações sobre como tooaccess Olá Olá repositório Data Lake dados, consulte [exibir propriedades de saudação armazenaram dados](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>Como posso começar a usar o Repositório Azure Data Lake?
Consulte [começar com o uso do repositório Data Lake hello Azure Portal](data-lake-store-get-started-portal.md), em como tooprovision usando um repositório Data Lake Olá Portal do Azure. Depois de ter provisionado Azure Data Lake, você pode aprender como toouse ofertas de dados grande, como análise Azure Data Lake ou do Azure HDInsight com repositório Data Lake. Você também pode criar um toocreate de aplicativo .NET uma conta do repositório Azure Data Lake e executar operações como dados de carregamento de dados de download, etc.

* [Introdução à Análise Data Lake do Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Introdução ao Repositório Azure Data Lake usando o SDK do .NET](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Vídeos do Repositório Data Lake
Se você preferir assistir vídeos toolearn, o repositório Data Lake fornece vídeos em uma variedade de recursos.

* [Criar uma conta do Repositório Azure Data Lake](https://mix.office.com/watch/1k1cycy4l4gen)
* [Usar Olá Data Explorer tooManage dados no repositório Azure Data Lake](https://mix.office.com/watch/icletrxrh6pc)
* [Conecte-se o repositório do análise Azure Data Lake tooAzure Data Lake](https://mix.office.com/watch/qwji0dc9rx9k)
* [Acessar o Repositório Data Lake por meio da Análise Data Lake](https://mix.office.com/watch/1n0s45up381a8)
* [Conecte-se o repositório Data Lake do Azure HDInsight tooAzure](https://mix.office.com/watch/l93xri2yhtp2)
* [Acessar o Repositório Azure Data Lake usando Hive e Pig](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [Use DistCp (cópia Distributed Hadoop) toocopy dados tooand do repositório Azure Data Lake](https://mix.office.com/watch/1liuojvdx6sie)
* [Usar Apache Sqoop toomove dados entre fontes relacionais e repositório Azure Data Lake](https://mix.office.com/watch/1butcdjxmu114)
* [Orquestração de dados usando o Azure Data Factory para o Repositório Azure Data Lake](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Protegendo dados em Olá repositório Azure Data Lake](https://mix.office.com/watch/1q2mgzh9nn5lx)

