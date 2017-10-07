---
title: "dados de aaaSync (visualização) | Microsoft Docs"
description: "Esta visão geral apresenta a Sincronização de Dados SQL do Azure (Visualização)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>Sincronizar dados entre vários bancos de dados locais e de nuvem com a Sincronização de Dados SQL

Sincronização de dados SQL é um serviço baseado no banco de dados SQL que lhe permite sincronizar dados Olá que bidirecional, você seleciona em vários bancos de dados SQL e instâncias do SQL Server.

Sincronização de dados é baseada em torno do conceito de saudação de um grupo de sincronização. Um grupo de sincronização é um grupo de bancos de dados que você deseja toosynchronize.

Um grupo de sincronização tem Olá propriedades a seguir:

-   Olá **esquema de sincronização** descreve quais dados estão sendo sincronizados.

-   Olá **direção de sincronização** podem ser bidirecionais ou pode fluir em uma única direção. Ou seja, Olá direção de sincronização pode ser *Hub tooMember* ou *tooHub membro*, ou ambos.

-   Olá **intervalo de sincronização** é a frequência a sincronização ocorre.

-   Olá **política de resolução de conflito** é uma diretiva de grupo de nível, que pode ser *Hub ganha* ou *wins membro*.

Sincronização de dados usa um hub e spoke topologia toosynchronize de dados. Defina um Olá bancos de dados no grupo de saudação como Olá banco de dados de Hub. rest Olá de bancos de dados de saudação são bancos de dados de membro. Sincronização ocorre apenas entre hello Hub e membros individuais.
-   Olá **banco de dados Hub** deve ser um banco de dados do SQL Azure.
-   Olá **bancos de dados de membro** pode ser bancos de dados SQL, bancos de dados local do SQL Server ou instâncias do SQL Server em máquinas virtuais do Azure.
-   Olá **banco de dados de sincronização** contém metadados hello e log para dados de sincronização. Olá banco de dados de sincronização tem toobe um banco de dados SQL localizado na Olá mesma região Olá banco de dados de Hub. Olá sincronização de banco de dados é criado de cliente e cliente de propriedade.

> [!NOTE]
> Se você estiver usando um banco de dados local, você tem muito[configurar um agente local.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![Sincronizar dados entre bancos de dados](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>Quando a sincronização de dados toouse

Sincronização de dados é útil em casos em que dados precisam toobe atualizado toodate em vários bancos de dados do SQL Azure ou bancos de dados do SQL Server. Aqui estão os casos de uso principal Olá para sincronização de dados:

-   **Sincronização de dados híbrido:** com a sincronização de dados, você pode manter os dados sincronizados entre seus bancos de dados locais e aplicativos tooenable bancos de dados do Azure SQL. Esse recurso pode ser atraente toocustomers que estiver pensando em nuvem de toohello móvel e gostaria de tooput alguns dos seus aplicativos no Azure.

-   **Aplicativos distribuídos:** em muitos casos, é vantajoso tooseparate diferentes cargas de trabalho em bancos de dados diferentes. Por exemplo, se você tiver um banco de dados grandes de produção, mas também é necessário toorun reporting ou carga de trabalho de análise desses dados, é útil toohave um segundo banco de dados para essa carga de trabalho adicional. Essa abordagem minimiza o impacto no desempenho Olá sua carga de trabalho de produção. Você pode usar a sincronização de dados tookeep esses dois bancos de dados sincronizados.

-   **Aplicativos Distribuídos Globalmente:** Muitas empresas abrangem várias regiões e até mesmo vários países. latência de rede toominimize, é melhor toohave Feche seus dados em uma região tooyou. Com a sincronização de dados, você pode facilmente manter os bancos de dados em regiões Olá mundo sincronizados.

Não recomendamos a sincronização de dados para Olá os seguintes cenários:

-   Recuperação de desastre

-   Escala de Leitura

-   ETL (OLTP tooOLAP)

-   Migração do local do SQL Server tooAzure banco de dados SQL

## <a name="how-does-data-sync-work"></a>Como funciona a Sincronização de Dados? 

-   **Controle de alterações de dados:** A Sincronização de Dados controla alterações usando os gatilhos inserir, atualizar e excluir. Olá alterações são gravadas em uma tabela lateral no banco de dados de usuário de saudação.

-   **Sincronização de dados:** a Sincronização de Dados é criada em um modelo Hub-Spoke. Olá Hub é sincronizado com cada membro individualmente. Alterações do hello Hub são baixadas toohello membro e, em seguida, as alterações de membro de saudação são carregado toohello Hub.

-   **Resolução de conflitos:** A Sincronização de Dados fornece duas opções para a resolução de conflito, *Hub ganha* ou *Membro ganha*.
    -   Se você selecionar *Hub ganha*, alterações Olá no hub Olá sempre substituem as alterações no membro hello.
    -   Se você selecionar *wins membro*, Olá alterações em alterações de substituição de membro Olá no hub de saudação. Se houver mais de um membro, valor final Olá depende de qual membro será sincronizado pela primeira vez.

## <a name="limitations-and-considerations"></a>Limitações e considerações

### <a name="performance-impact"></a>Impacto sobre o desempenho
Sincronização de dados usa insere, atualiza e excluir disparadores tootrack alterações. Ele cria tabelas no banco de dados de usuário de saudação para controle de alterações. Essas atividades de controle de alterações têm um impacto sobre sua carga de trabalho do banco de dados. Avalie sua camada de serviço e faça a atualização necessário.

### <a name="eventual-consistency"></a>Consistência eventual
Como a Sincronização de Dados é baseada no gatilho, a consistência transacional não é garantida. A Microsoft garante que todas as alterações são feitas, eventualmente, e que a Sincronização de Dados não causa perda de dados.

### <a name="unsupported-data-types"></a>Tipos de dados sem suporte

-   FileStream

-   SQL/CLR UDT

-   XMLSchemaCollection (suporte para XML)

-   Cursor, Timestamp, Hierarchyid

### <a name="requirements"></a>Requisitos

-   Cada tabela deve ter uma chave primária.

-   Uma tabela não pode ter uma coluna de identidade não é chave primária hello.

-   nomes de saudação de objetos (bancos de dados, tabelas e colunas) não podem conter Olá caracteres imprimíveis ponto (.), colchete ([]), esquerdo ou colchete direito (]).

### <a name="limitations-on-service-and-database-dimensions"></a>Limitações nas dimensões de serviço e do banco de dados

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **Dimensões**                                                      | **Limite**              | **Solução alternativa**              |
| Número máximo de grupos de sincronização aos quais qualquer banco de dados pode pertencer.       | 5                      |                             |
| Número máximo de pontos de extremidade em um único grupo de sincronização              | 30                     | Criar vários grupos de sincronização |
| Número máximo de pontos de extremidade locais em um único grupo de sincronização. | 5                      | Criar vários grupos de sincronização |
| Nomes de coluna, tabela, esquema e banco de dados                       | 50 caracteres por nome |                             |
| Tabelas em um grupo de sincronização                                          | 500                    | Criar vários grupos de sincronização |
| Colunas em uma tabela em um grupo de sincronização                              | 1000                   |                             |
| Tamanho da linha de dados em uma tabela                                        | 24 Mb                  |                             |
| Intervalo de sincronização mínima                                           | 5 Minutos              |                             |

## <a name="common-questions"></a>Perguntas comuns

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>Com que frequência a Sincronização de Dados pode sincronizar meus dados? 
frequência mínima de saudação é a cada cinco minutos.

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>É possível usar toosync de sincronização de dados entre o SQL Server local somente bancos de dados? 
Não diretamente. Você pode sincronizar entre bancos de dados do SQL Server local indiretamente, no entanto, a criação de um banco de dados de Hub no Azure e, em seguida, adicionando o grupo de sincronização de toohello do hello local bancos de dados.
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>Posso usar dados de tooseed de sincronização de dados do meu produção tooan vazio banco de dados e, em seguida, mantê-los sincronizados? 
Sim. Crie esquema Olá manualmente no novo banco de dados de saudação por execução de scripts de saudação original. Depois de criar o esquema de hello, adicionar Olá tabelas tooa sincronização grupo toocopy Olá dados e mantê-lo sincronizado.

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>Por que vejo tabelas que eu não criei?  
A Sincronização de Dados cria tabelas secundárias no banco de dados para controle de alterações. Não as exclua, pois a Sincronização de Dados deixará de funcionar.
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>Recebi uma mensagem de erro que diz "não é possível inserir valor Olá NULL na coluna Olá \<coluna\>. A coluna não permite valores nulos”. O que isso significa e como corrigir o erro de Olá? 
Essa mensagem de erro indica que um dos dois problemas a seguir hello:
1.  Uma tabela pode estar sem uma chave primária. toofix esse problema, adicione uma tabelas de saudação do tooall de chave primária está sincronizando.
2.  Pode haver uma cláusula WHERE na instrução CREATE INDEX. A sincronização não trata essa condição. toofix esse problema, remova Olá cláusula WHERE ou alterar manualmente Olá tooall bancos de dados. 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>Como a Sincronização de Dados trata referências circulares? Ou seja, quando hello mesmo dados estão sincronizados em vários grupos de sincronização e é alterado continuamente como resultado?
A Sincronização de Dados não trata referências circulares. Ser tooavoid se-los. 

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a Sincronização de Dados SQL, veja:

-   [Introdução à Sincronização de Dados SQL](sql-database-get-started-sql-data-sync.md)

-   Concluir PowerShell exemplos que mostram como tooconfigure de sincronização de dados do SQL:
    -   [Use o PowerShell toosync entre vários bancos de dados do SQL Azure](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Use o PowerShell toosync entre um banco de dados do SQL Azure e um banco de dados do SQL Server local](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Baixar a documentação técnica do hello concluída a sincronização de dados SQL](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [Baixar a documentação da API de REST de sincronização de dados de SQL Olá](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

Para saber mais sobre o Banco de Dados SQL, veja:

-   [Visão geral do Banco de Dados SQL](sql-database-technical-overview.md)

-   [Gerenciamento de ciclo de vida do banco de dados](https://msdn.microsoft.com/library/jj907294.aspx)
