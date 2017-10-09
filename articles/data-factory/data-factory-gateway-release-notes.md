---
title: Notas de aaaRelease do Gateway de gerenciamento de dados | Microsoft Docs
description: "Notas de versão do Gateway de Gerenciamento de Dados"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>Notas de versão para o Gateway de Gerenciamento de Dados
Um dos desafios Olá para integração de dados modernos é toomove dados tooand de toocloud local. Fábrica de dados torna essa integração com o Gateway de gerenciamento de dados, que é um agente que você pode instalar o movimento de dados local tooenable híbrida.

Consulte Olá seguintes artigos para obter informações detalhadas sobre o Gateway de gerenciamento de dados e como toouse-lo:

*  [Gateway de gerenciamento de dados](data-factory-data-management-gateway.md)
*  [Mover dados entre o local e a nuvem usando a Azure Data Factory](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>VERSÃO ATUAL (2.10.6347.7)

### <a name="enhancements-"></a>Melhorias-
- Você pode adicionar o barramento de serviço do DNS entradas toowhitelist em vez de lista branca de todos os endereços IP do Azure do seu firewall (se necessário). Você pode encontrar a entrada DNS respectiva no Portal do Azure (Data Factory -> 'Criar e Implantar' -> 'Gateways' -> "serviceUrls" (no JSON)
- Agora, o conector HDFS dá suporte ao certificado público autoassinado, permitindo que você ignore a validação de SSL.
- Corrigido: Problema com gateway offline durante a atualização (devido a distorção tooclock)



## <a name="earlier-versions"></a>Versões anteriores

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>Melhorias-
-   Você pode adicionar entradas DNS toowhitelist barramento de serviço em vez de lista branca de todos os endereços IP do Azure do seu firewall (se necessário). Mais detalhes aqui.
-   Agora você pode copiar dados para/de um blob de bloco único backup too4.75 TB, que é o tamanho de saudação máximo com suporte de blob de blocos. (o limite anterior era de 195 GB).
-   Correção: problema de memória insuficiente ao descompactar vários arquivos pequenos durante a atividade de cópia.
-   Correção: Índice fora do problema de intervalo durante a cópia do banco de dados de documento tooan local do SQL Server com o recurso idempotência.
-   Correção: o script de limpeza do SQL não funcionava no SQL Server local no Assistente de Cópia.
-   Correção: Nome da coluna espaço Olá final não funciona na atividade de cópia.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>Melhorias-
- Correção: problema com credenciais ausentes na reinicialização do computador do gateway.
- Correção: problema com o registro durante a restauração do gateway usando um arquivo de backup.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>Melhorias-
- Correção: leitura incorreta do valor nulo Decimal do Oracle como fonte.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>O que há de novo
- Os clientes podem fornecer comentários sobre a experiência de registro de gateway.
- Suporte a um novo formato de compactação: ZIP (Deflate)

### <a name="enhancements-"></a>Melhorias-
- Melhoria de desempenho para o coletor Oracle, fonte HDFS.
- Correção de bug para atualização automática do gateway, capacidade de processamento paralelo do gateway.


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>Melhorias
- Melhor e mais robusta Gateway registro experiência-agora você pode acompanhar o status do andamento durante o processo de registro de Gateway hello, que torna a experiência de registro hello mais ágil na resposta.
- Melhoria no Gateway restaurar processo - você ainda poderá recuperar o gateway mesmo se você não tiver o arquivo de backup Olá gateway com essa atualização. Isso exigiria tooreset credenciais de serviço vinculado no Portal.
- Correção de bug.

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>O que há de novo

- Agora você pode armazenar credenciais de fonte de dados localmente. Olá credenciais são criptografadas. credenciais de fonte de dados Olá podem ser recuperadas e restaurados usando o arquivo de backup de saudação que pode ser exportado do hello existente Gateway, todos os locais.

### <a name="enhancements-"></a>Melhorias-

- Experiência de registro de Gateway melhorada e mais robusta.
- Suporte a detecção automática da configuração de QuoteChar para formato de texto no Assistente para copiar e melhorar Olá formato geral a precisão da detecção.

## <a name="2361002"></a>2.3.6100.2

- Suporte à detecção automática de firstRowAsHeader e SkipLineCount no assistente de cópia para arquivos de texto em HDFS e no sistema de arquivos local.
- Aprimorar a estabilidade de saudação da conexão de rede entre o gateway e o barramento de serviço
- Algumas correções de bug


## <a name="2260721"></a>2.2.6072.1

*  Oferece suporte ao configurar o proxy HTTP para usar o gateway Olá Olá Gateway Configuration Manager. Se configurado, o Blob do Azure, a Tabela do Azure, o Azure Data Lake e o DocumentDB serão acessados por meio do proxy HTTP.
*  Cabeçalho dá suporte ao tratamento de TextFormat ao copiar dados do sistema de arquivos local e HDFS local tooAzure Blob, repositório Azure Data Lake,.
*  Oferece suporte à cópia de dados de Blob de acréscimo e blobs de página juntamente com hello já suporte para o Blob de blocos.
*  Apresenta um novo status do gateway **Online (limitado)**, que indica que essa funcionalidade principal de saudação do gateway de saudação funciona exceto o suporte da operação interativa Olá para o Assistente para cópia.
*  Melhora a robustez de saudação do registro de gateway usando a chave de registro.

## <a name="216040"></a>2.1.6040.

*  Driver do DB2 está incluído no pacote de instalação do gateway Olá agora. Não é necessário tooinstall-lo separadamente.
*  Driver de DB2 agora dá suporte a z/OS e DB2 para i (AS / 400) junto com hello plataformas já com suporte (Linux, Unix e Windows).
*  Dá suporte ao uso do Azure Cosmos DB como uma origem ou um destino para armazenamentos de dados locais
*  Dá suporte ao copiar o armazenamento de blob do/toocold/hot dados junto com hello já suporte para a conta de armazenamento de uso geral.
*  Permite que você tooconnect tooon-local do SQL Server por meio do gateway com privilégios de logon remoto.  

## <a name="2060131"></a>2.0.6013.1

*  Você pode selecionar Olá toobe de cultura do idioma usado por um gateway durante a instalação manual.

*  Quando o gateway não funciona conforme o esperado, você pode escolher toosend logs do gateway de últimos sete dias tooMicrosoft toofacilitate solução do problema de saudação. Se o gateway não está conectado toohello serviço de nuvem, você pode escolher toosave e arquivar os logs do gateway.  

*  Aprimoramentos na interface do usuário para o gerenciador de configuração de gateway:

    *  Verifique o status do gateway mais visível na guia de início de saudação.

    *  Controles reorganizados e simplificados.

    *  Você pode copiar dados de um armazenamento usando Olá [ferramenta de visualização de cópia sem código](data-factory-copy-data-wizard-tutorial.md). Confira [Cópia em Etapas](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes gerais sobre esse recurso.
*  Você pode usar dados de tooingress de Gateway de gerenciamento de dados diretamente de um banco de dados do SQL Server local no aprendizado de máquina do Azure.

*  Aprimoramentos de desempenho

    * Melhore o desempenho de exibição de Esquema/Visualização no SQL Server na ferramenta de visualização de cópia sem código.

## <a name="11259531"></a>1.12.5953.1

*  Correções de bug

## <a name="11159181"></a>1.11.5918.1

*  Tamanho máximo do log de eventos do gateway Olá foi aumentado de 1 MB too40 MB.

*  Uma caixa de diálogo de aviso é exibida caso uma reinicialização seja necessária durante a atualização automática do gateway. Você pode escolher toorestart direita, em seguida, ou posterior.

*  Em caso de falha da atualização automática, o instalador do gateway recupera a atualização automática três vezes no máximo.

*  Aprimoramentos de desempenho

    * Melhora no desempenho do carregamento de grandes tabelas de servidor local no cenário de cópia sem código.

*  Correções de bug

## <a name="11058921"></a>1.10.5892.1

*  Aprimoramentos de desempenho

*  Correções de bug

## <a name="1958652"></a>1.9.5865.2

*  Capacidade de atualização automática zero touch
*  Novo ícone de bandeja com indicadores de status do gateway
*  Capacidade muito "Atualizar agora" de cliente Olá
*  Hora de agendamento de atualização de tooset de capacidade
*  Script do PowerShell para ativar/desativar a atualização automática
*  Suporte para o formato JSON  
*  Aprimoramentos de desempenho
*  Correções de bug

## <a name="1858221"></a>1.8.5822.1

*  Melhorar a experiência de solução de problemas
*  Aprimoramentos de desempenho
*  Correções de bug

### <a name="1757951"></a>1.7.5795.1

*  Aprimoramentos de desempenho
*  Correções de bug

### <a name="1757641"></a>1.7.5764.1

*  Aprimoramentos de desempenho
*  Correções de bug

### <a name="1657351"></a>1.6.5735.1

*  Suporte à fonte/coletor do HDFS local
*  Aprimoramentos de desempenho
*  Correções de bug

### <a name="1656961"></a>1.6.5696.1

*  Aprimoramentos de desempenho
*  Correções de bug

### <a name="1656761"></a>1.6.5676.1

*  Suporte a ferramentas de diagnóstico no Gerenciador de Configurações
*  Suporte a colunas de tabela para fontes de dados tabulares do Azure Data Factory
*  Suporte a SQL DW para Azure Data Factory
*  Suporte Reclusivo em BlobSource e FileSource para o Azure Data Factory
*  Suporte a CopyBehavior – MergeFiles, PreserveHierarchy e FlattenHierarchy em BlobSink e FileSink com Cópia Binária para o Azure Data Factory
*  Suporte a relatórios de andamento de Atividade de Cópia do Azure Data Factory
*  Suporte a Validação de Conectividade de Fonte de Dados para Azure Data Factory
*  Correções de bug

### <a name="1656721"></a>1.6.5672.1

*  Suporte a nome de tabela para  fonte de dados ODBC para o Azure Data Factory
*  Aprimoramentos de desempenho
*  Correções de bug

### <a name="1656581"></a>1.6.5658.1

*  Suporte a Coletor de Arquivo para o Azure Data Factory
*  Suporte à preservação de hierarquia na cópia binária para o Azure Data Factory
*  Suporte a Idempotência de Atividade de Cópia para o Azure Data Factory
*  Correções de bug

### <a name="1656401"></a>1.6.5640.1

*  Suporte a três ou mais fontes de dados para o Azure Data Factory (ODBC, OData, HDFS)
*  Suporte ao caractere de aspas no analisador de csv para o Azure Data Factory
*  Suporte à compactação (BZip2)
*  Correções de bug

### <a name="1556121"></a>1.5.5612.1

*  Suporte a cinco bancos de dados relacionais do Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata e Sybase)
*  Suporte à compactação (Gzip e Deflate)
*  Aprimoramentos de desempenho
*  Correções de bug

### <a name="1455491"></a>1.4.5549.1

*  Adicionar suporte a fonte de dados Oracle para o Azure Data Factory
*  Aprimoramentos de desempenho
*  Correções de bug

### <a name="1454921"></a>1.4.5492.1

*  Binário unificado que dá suporte aos serviços Microsoft Azure Data Factory e Office 365 Power BI
*  Refinar o processo de configuração da interface do usuário e o registro de saudação
*  Azure Data Factory – suporte a Ingresso e Egresso do Azure para fonte de dados do SQL Server

### <a name="1253031"></a>1.2.5303.1

*  Corrigi toosupport de problema de tempo limite mais demorado conexões de fonte de dados.

### <a name="1155268"></a>1.1.5526.8

*  Requer o .NET Framework 4.5.1 como pré-requisito durante a instalação.

### <a name="1051442"></a>1.0.5144.2

*  Nenhuma alteração que afeta os cenários do Azure Data Factory.
