---
title: "aaaImport e exportação no banco de dados do Azure para MySQL | Microsoft Docs"
description: Este artigo explica formas tooimport e exportar bancos de dados no banco de dados do Azure para MySQL, usando ferramentas como o Workbench do MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>Migrar o banco de dados MySQL usando importação e exportação
Este artigo explica dois tooimporting de abordagens comuns e exportando dados tooan banco de dados do Azure para o MySQL server usando o Workbench do MySQL. 

## <a name="before-you-begin"></a>Antes de começar
toostep por este tooguide como, você precisa:
- Um Banco de Dados do Azure para MySQL Server, seguindo [Criar um Banco de Dados do Azure para MySQL Server usando o portal do Azure](quickstart-create-mysql-server-database-using-azure-portal.md).
- MySQL Workbench [baixado](https://dev.mysql.com/downloads/workbench/), ou outra MySQL ferramenta tooimport e exportação.

## <a name="use-common-tools"></a>Usar ferramentas comuns
Use ferramentas comuns, como MySQL Workbench, Toad ou Navicat tooremotely se conectar e importar ou exportar dados no banco de dados do Azure para MySQL. 

Use tais ferramentas em seu computador cliente com um tooAzure de tooconnect de conexão de Internet banco de dados para MySQL. Use uma conexão criptografada por SSL para as melhores práticas de segurança, conforme descrito em [Configurar a conectividade SSL no Banco de Dados do Azure para MySQL](concepts-ssl-connection-security.md).

Você não precisa toomove importação e exportação local dos arquivos tooany nuvem especiais ao migrar tooAzure banco de dados para MySQL. 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>Criar um banco de dados em Olá banco de dados do Azure para o MySQL server
Crie um banco de dados vazio no hello banco de dados do Azure para onde você deseja toomigrate Olá dados do MySQL server. Use uma ferramenta como o Workbench do MySQL, Toad Navicat toocreate Olá banco de dados ou. banco de dados de saudação pode ter Olá mesmo nome como o banco de dados de saudação que contém dados saudação despejada, ou você pode criar um banco de dados com um nome diferente.

tooget conectado, localizar as informações de conexão de saudação em Olá **propriedades** painel no banco de dados do Azure para MySQL.

![Localizar informações de conexão de saudação em Olá portal do Azure](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

Adicione tooMySQL informações de conexão Olá Workbench.

![Cadeia de conexão do MySQL Workbench](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>Determinar quando toouse importar e exportar técnicas em vez de um despejo de memória e a restauração
Use o MySQL ferramentas tooimport e exportar bancos de dados no banco de dados MySQL no hello cenários a seguir. Em outros cenários, você pode se beneficiar do uso Olá [de despejo e restaurar](concepts-migrate-dump-restore.md) abordagem em vez disso. 

- Quando você precisar tooselectively escolha alguns tooimport de tabelas no banco de dados MySQL existente no banco de dados MySQL, é melhor toouse Olá importar e exportar técnica.  Fazendo isso, você pode omitir todas as tabelas de saudação migração toosave tempo e recursos desnecessárias. Por exemplo, usar Olá `--include-tables` ou `--exclude-tables` alternar com [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) e hello `--tables` alternar com [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables).
- Quando você estiver movendo objetos de banco de dados de saudação diferentes de tabelas, crie-os explicitamente. Incluir restrições (chave primária, chave estrangeira, índices), exibições, funções, procedimentos, disparadores, e objetos de qualquer outro banco de dados que você deseja toomigrate.
- Quando estiver migrando dados de fontes de dados externas que não sejam um banco de dados MySQL, crie arquivos simples e importe-os usando [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html).

Certifique-se de que todas as tabelas no banco de dados de saudação usam o mecanismo de armazenamento de InnoDB hello quando você estiver carregando dados no banco de dados do Azure para MySQL. Banco de dados do Azure para MySQL oferece suporte a apenas Olá InnoDB mecanismo de armazenamento, ele não oferece suporte a mecanismos de armazenamento alternativo. Se suas tabelas exigem mecanismos de armazenamento alternativo, ser tooconvert-se de que eles toouse formato do mecanismo de InnoDB Olá antes da migração de saudação tooAzure banco de dados MySQL. 

Por exemplo, se você tiver um aplicativo web ou WordPress que usa o mecanismo de MyISAM hello, primeiro converta Olá tabelas ao migrar dados de saudação em tabelas de InnoDB. Em seguida, restaure tooAzure banco de dados para MySQL. Cláusula de saudação do uso `ENGINE=INNODB` tooset Olá mecanismo para criar uma tabela e, em seguida, transfira os dados de saudação para compatível antes da migração Olá Olá. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>Recomendações de desempenho para importação e exportação
-   Crie índices clusterizados e chaves primárias antes de carregar os dados. Carregue os dados na ordem de chave primária. 
-   Atrase a criação de índices secundários até os dados serem carregados. Crie todos os índices secundários após o carregamento. 
-   Desabilite as restrições de chave estrangeira antes do carregamento. Desabilitar as verificações de chave estrangeira proporciona ganhos significativos de desempenho. Habilitar restrições de saudação e verifique se a dados saudação após a integridade referencial do hello carga tooensure.
-   Carregar dados em paralelo. Evite muito paralelismo que poderia causar toohit um limite de recursos e monitorar recursos usando as métricas de saudação disponíveis no portal do Azure de saudação. 
-   Use tabelas particionadas, quando apropriado.

## <a name="import-and-export-by-using-mysql-workbench"></a>Importar e exportar usando o MySQL Workbench
Há duas maneiras tooexport e importar dados no Workbench do MySQL. Cada uma tem uma finalidade diferente. 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>Dados da tabela de exportar e importar os assistentes no menu de contexto do Pesquisador de objetos Olá
![Assistentes do Workbench do MySQL no menu de contexto do Pesquisador de objetos Olá](./media/concepts-migrate-import-export/p1.png)

Assistentes de saudação para dados de tabela oferece suporte para importação e operações de exportação usando arquivos CSV e JSON. Eles incluem várias opções de configuração, como separadores, seleção de coluna e seleção de codificação. Execute cada assistente em MySQL Servers locais ou remotamente conectados. ação de importação de saudação inclui a tabela, coluna e mapeamento de tipo. 

Você pode acessar esses assistentes no menu de contexto do Pesquisador de objetos Olá clicando em uma tabela. Em seguida, escolha **Assistente de Exportação de Dados de Tabela** ou **Assistente de Importação de Dados de Tabela**. 

#### <a name="table-data-export-wizard"></a>Assistente de Exportação de Dados de Tabela
Olá, exemplo a seguir exporta arquivo CSV do hello tabela tooa: 
1. Clique com botão direito índice Olá Olá toobe de banco de dados exportado. 
2. Selecione **Assistente de Exportação de Dados de Tabela**. Selecione Olá colunas toobe exportado, deslocamento da linha (se houver) e count (se houver). 
3. Em Olá **selecionar dados para exportação** , clique em **próximo**. Selecione o caminho do arquivo hello, CSV ou JSON tipo de arquivo. Selecione também o separador de linha hello, método de colocar cadeias de caracteres e o separador de campo. 
4. Em Olá **local do arquivo de saída selecione** , clique em **próximo**. 
5. Em Olá **exportar dados** , clique em **próximo**.

#### <a name="table-data-import-wizard"></a>Assistente de Importação de Dados de Tabela
Olá exemplo a seguir importa Olá tabela de um arquivo CSV:
1. Clique com botão direito índice Olá Olá toobe de banco de dados importado. 
2. Procurar tooand selecione Olá toobe do arquivo CSV importado e, em seguida, clique em **próximo**. 
3. Selecione a tabela de destino da saudação (nova ou existente) e marque ou desmarque Olá **Truncate table antes da importação** caixa de seleção. Clique em **Avançar**.
4. Selecione a codificação e hello toobe colunas importada e, em seguida, clique em **próximo**. 
5. Em Olá **importar dados** , clique em **próximo**. Assistente de saudação importa dados de saudação adequadamente.

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>Dados do SQL exportam e importar assistentes do painel de navegação da saudação
Usar um assistente tooexport ou importe SQL gerada no Workbench do MySQL ou gerados a partir de comando de mysqldump hello. Acessar esses assistentes de saudação **navegador** painel ou selecionando **Server** no menu principal da saudação. Em seguida, selecione **Exportação de Dados** ou **Importação de Dados**. 

#### <a name="data-export"></a>Exportação de Dados
![Exportação de dados do MySQL Workbench usando o painel de navegação da saudação](./media/concepts-migrate-import-export/p2.png)

Você pode usar o hello **de exportação de dados** guia tooexport seus dados do MySQL. 
1. Selecione cada esquema que você deseja tooexport, opcionalmente escolher objetos de esquema específico e tabelas de cada esquema e gerar exportação hello. Opções de configuração incluem a exportação tooa projeto pasta ou arquivo SQL autossuficiente, despejo de eventos e rotinas armazenadas ou ignorar dados da tabela. 
 
   Como alternativa, use **exportar um conjunto de resultados** tooexport um resultado específico definido Olá SQL editor tooanother formato, como JSON, CSV, HTML e XML. 
3. Selecione Olá tooexport de objetos de banco de dados e configurar opções relacionadas à saudação.
4. Clique em **atualização** objetos atuais do tooload hello.
5. Opcionalmente, abra Olá **opções avançadas** guia toorefine operação de exportação de saudação. Por exemplo, adicione bloqueios de tabela, use instruções de substituição em vez de inserção e identificadores de aspas com caracteres de acento grave.
6. Clique em **iniciar exportação** toobegin processo de exportação de saudação.


#### <a name="data-import"></a>Importação de Dados
![Importação de Dados do MySQL Workbench usando o Navegador de Gerenciamento](./media/concepts-migrate-import-export/p3.png)

Você pode usar o hello **importação de dados** guia tooimport ou restaurar dados exportados da operação de exportação de dados de saudação ou do comando de mysqldump hello. 
1. Escolha a pasta do projeto hello ou arquivos independente do SQL, escolha Olá esquema tooimport em ou escolha **novo** toodefine um novo esquema. 
2. Clique em **iniciar Importar** toobegin processo de importação de saudação.

## <a name="next-steps"></a>Próximas etapas
Como outra abordagem de migração, leia [Migrar o banco de dados MySQL usando o despejo e a restauração no Banco de Dados do Azure para MySQL](concepts-migrate-dump-restore.md). 
