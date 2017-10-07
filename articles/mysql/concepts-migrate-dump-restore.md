---
title: "aaaMigrate seu banco de dados MySQL usando dump e restauração no banco de dados do Azure para MySQL | Microsoft Docs"
description: Este artigo explica dois tooback de maneiras comuns backup e restaurar bancos de dados no banco de dados do Azure para MySQL, usando ferramentas como mysqldump, MySQL Workbench e PHPMyAdmin.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: d05d483ff53483df8e005eae2d9a4f8190e8f663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-tooazure-database-for-mysql-using-dump-and-restore"></a>Migrar seu banco de dados de MySQL tooAzure banco de dados para MySQL usando dump e restore
Este artigo explica dois tooback maneiras comuns backup e restaurar bancos de dados no banco de dados do Azure para MySQL
- Despejo de memória e a restauração do hello (usando mysqldump) de linha de comando 
- Despejo e restauração usando o PHPMyAdmin 

## <a name="before-you-begin"></a>Antes de começar
toostep por este tooguide como, você precisa toohave:
- [Criar Banco de Dados do Azure para servidor MySQL - portal do Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- Utilitário da linha de comando [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html) instalado em um computador.
- MySQL Workbench [MySQL Workbench baixar](https://dev.mysql.com/downloads/workbench/), Toad, Navicat ou outros toodo de ferramenta de terceiros MySQL despejo e comandos de restauração.

## <a name="use-common-tools"></a>Usar ferramentas comuns
Use ferramentas e utilitários comuns como MySQL Workbench, mysqldump, Toad ou Navicat tooremotely se conectar e restaurar dados no banco de dados do Azure para MySQL. Use tais ferramentas em seu computador cliente com um toohello de tooconnect de conexão de internet banco de dados do Azure para MySQL. Use uma conexão SSL criptografada para práticas recomendadas de segurança, consulte também [Configurar conectividade SSL no Banco de Dados do Azure para MySQL](concepts-ssl-connection-security.md). Não é necessário local dos arquivos de despejo toomove Olá tooany nuvem especiais ao migrar tooAzure banco de dados para MySQL. 

## <a name="common-uses-for-dump-and-restore"></a>Usos comuns de despejo e restauração
Você pode usar os utilitários de MySQL como mysqldump e mysqlpump toodump e carregar bancos de dados em um banco de dados MySQL em vários cenários comuns. Em outros cenários, você pode usar o hello [de importação e exportação](concepts-migrate-import-export.md) abordagem em vez disso.

- Usar banco de dados despejos de memória quando você estiver migrando um banco de dados inteiro hello. Essa recomendação mantém ao mover uma grande quantidade de dados MySQL, ou quando você deseja interromper o serviço toominimize para aplicativos ou sites em tempo real. 
-  Verifique se que todas as tabelas no banco de dados de saudação usam o mecanismo de armazenamento de InnoDB Olá ao carregar dados no banco de dados do Azure para MySQL. O Banco de dados do Azure para MySQL dá suporte apenas ao mecanismo de armazenamento do InnoDB e, portanto, não dá suporte a mecanismos de armazenamento alternativos. Se as tabelas são configuradas com outros mecanismos de armazenamento, convertê-los em formato de mecanismo de InnoDB Olá antes da migração tooAzure banco de dados para MySQL.
   Por exemplo, se você tiver um WordPress ou aplicativo Web usando tabelas de MyISAM Olá, primeiro converta essas tabelas migrando em formato de InnoDB antes de restaurar o banco de dados de tooAzure para MySQL. Cláusula de saudação do uso `ENGINE=InnoDB` tooset Olá mecanismo usado ao criar uma nova tabela, em seguida, transfira dados Olá para compatível antes da restauração Olá Olá. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```
- problemas de compatibilidade de qualquer tooavoid, certifique-se Olá a mesma versão do MySQL é usado em sistemas de origem e destino Olá ao despejar bancos de dados. Por exemplo, se seu servidor existente do MySQL é a versão 5.7, você deve migrar tooAzure banco de dados MySQL configurado toorun versão 5.7. Olá `mysql_upgrade` comando não funciona em um banco de dados do Azure para o MySQL server e não é suportado. Se você precisar tooupgrade entre versões do MySQL, primeiro despejo ou exportar seu banco de dados de versão inferior em uma versão posterior do MySQL no seu ambiente. Em seguida, execute `mysql_upgrade`, antes de tentar migrar para um banco de dados do Azure para MySQL.

## <a name="performance-considerations"></a>Considerações sobre o desempenho
desempenho toooptimize, execute um aviso sobre essas considerações ao despejar grandes bancos de dados:
-   Saudação de uso `exclude-triggers` opção mysqldump ao despejar bancos de dados. Exclua gatilhos de comandos despejo arquivos tooavoid Olá gatilho acionados durante a saudação a restauração de dados. 
-   Evite Olá `single-transaction` opção mysqldump ao despejar bancos de dados muito grandes. Despejar muitas tabelas em uma única transação faz com que o armazenamento extra e toobe de recursos de memória consumida durante a restauração e pode causar atrasos de desempenho ou restrições de recursos.
-   Inserções de vários valores de uso ao carregar com sobrecarga de execução de instrução SQL toominimize ao despejar bancos de dados. Ao usar arquivos de despejo gerados pelo utilitário mysqldump, inserções de vários valores são habilitadas por padrão. 
-  Saudação de uso `order-by-primary` opção mysqldump ao despejar bancos de dados, para que os dados de saudação são executados na ordem de chave primária.
-   Saudação de uso `disable-keys` opção mysqldump ao despejar dados, restrições de chave estrangeira toodisable antes de carga. Desabilitar as verificações de chave estrangeira proporciona ganhos de desempenho. Habilitar restrições de saudação e verifique se a dados saudação após a integridade referencial do hello carga tooensure.
-   Use tabelas particionadas, quando apropriado.
-   Carregar dados em paralelo. Evite muito paralelismo que poderia causar toohit um limite de recursos e monitorar recursos usando Olá métricas disponíveis no portal do Azure de saudação. 
-   Saudação de uso `defer-table-indexes` opção mysqlpump ao despejar bancos de dados, para que a criação de índice ocorre após os dados de tabelas são carregados.

## <a name="create-a-backup-file-from-hello-command-line-using-mysqldump"></a>Criar um arquivo de backup de saudação de linha de comando usando mysqldump
tooback backup de banco de dados MySQL existente no local de saudação servidor local ou em uma máquina virtual, execute Olá comando a seguir: 
```bash
$ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
```

Olá parâmetros tooprovide são:
- [uname] Seu nome de usuário do banco de dados 
- [senha] Olá senha para seu banco de dados (Observe que não há nenhum espaço entre -p e a senha de saudação) 
- nome de saudação [dbname] do banco de dados 
- nome do arquivo hello [backupfile.sql] para o backup do banco de dados 
- [-opt] Olá mysqldump opção 

Por exemplo, tooback um banco de dados denominado 'testdb' em seu servidor MySQL com nome de usuário de saudação 'testuser' e testdb_backup.sql de arquivo de tooa nenhuma senha, use Olá comando a seguir. Olá comando faz backup Olá `testdb` banco de dados em um arquivo chamado `testdb_backup.sql`, que contém todas as instruções SQL de saudação necessário toore-criar o banco de dados de saudação. 

```bash
$ mysqldump -u root -p testdb > testdb_backup.sql
```
tooselect tabelas específicas no seu tooback de banco de dados para cima, nomes de tabela lista Olá separados por espaços. Por exemplo, tooback somente tabelas table1 e table2 de saudação 'testdb', siga este exemplo: 
```bash
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

Alterne de banco de dados de tooback mais de um banco de dados ao mesmo tempo, use hello – e nomes de banco de dados lista Olá separados por espaços. 
```bash
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```
tooback backup todos os bancos de dados de saudação no servidor de saudação ao mesmo tempo, você deve usar o hello - opção de todos os bancos de dados.
```
$ mysqldump -u root -p --all-databases > alldb_backup.sql 
```

## <a name="create-a-database-on-hello-target-azure-database-for-mysql-server"></a>Criar um banco de dados no banco de dados de destino de Olá para o MySQL server
Crie um banco de dados vazio no destino Olá banco de dados do Azure para onde você deseja toomigrate Olá dados do MySQL server. Use uma ferramenta como o Workbench do MySQL, Toad Navicat toocreate Olá banco de dados ou. banco de dados de saudação pode ter Olá mesmo nome como Olá banco de dados independente Olá despejada dados ou você pode criar um banco de dados com um nome diferente.

tooget conectado, localize informações de conexão de saudação na página de propriedades de saudação do banco de dados do Azure para MySQL.
![Localizar informações de conexão de saudação em Olá portal do Azure](./media/concepts-migrate-dump-restore/1_server-properties-name-login.png)

Adicione informações de conexão de saudação em seu ambiente de trabalho do MySQL.
![Cadeia de conexão do MySQL Workbench](./media/concepts-migrate-dump-restore/2_setup-new-connection.png)


## <a name="restore-your-mysql-database-using-command-line-or-mysql-workbench"></a>Restaurar o banco de dados MySQL usando a linha de comando ou o MySQL Workbench
Depois que você criou o banco de dados de destino hello, você pode usar o comando do mysql Olá MySQL Workbench toorestore Olá dados ou em Olá específico recém-criado banco de dados do arquivo de despejo de saudação.
```bash
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```
Neste exemplo, restaure dados saudação no hello recém-criado banco de dados no destino Olá banco de dados do Azure para o MySQL server.
```bash
$ mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p testdb < testdb_backup.sql
```

## <a name="export-using-phpmyadmin"></a>Exportar usando PHPMyAdmin
tooexport, você pode usar o hello comuns ferramenta phpMyAdmin, que você pode já ter instalado localmente em seu ambiente. tooexport banco de dados MySQL usando PHPMyAdmin:
- Abra o phpMyAdmin.
- Selecione o banco de dados. Clique em nome de banco de dados de saudação na lista Olá Olá esquerda. 
- Clique em Olá **exportar** link. Uma nova página é exibida tooview despejo de saudação do banco de dados.
- Na área de exportação de Olá, clique em hello **Selecionar tudo** toochoose Olá tabelas no banco de dados. 
- No hello área de opções do SQL, clique em opções apropriadas hello. 
- Clique em Olá **Salvar como arquivo** opção e compactação correspondente Olá opção e clique em Olá **vá** botão. Uma caixa de diálogo deve aparecer uma solicitação você toosave Olá arquivo localmente.

## <a name="import-using-phpmyadmin"></a>Importar usando PHPMyAdmin
Importar o banco de dados é tooexporting semelhante. Olá seguintes ações:
- Abra o phpMyAdmin. 
- Na página de instalação do phpMyAdmin hello, clique em **adicionar** tooadd banco de dados do Azure para o MySQL server. Forneça detalhes de conexão de saudação e informações de logon.
- Criar um banco de dados nomeado apropriadamente e selecione esquerda Olá da tela hello. toorewrite Olá banco de dados existente, clique em nome do banco de dados hello, marque todas as caixas de seleção de saudação ao lado dos nomes de tabela hello e selecione **Drop** toodelete Olá tabelas existentes. 
- Clique em Olá **SQL** página de saudação do link tooshow onde você pode digitar em comandos SQL, ou de carregar seu arquivo SQL. 
- Saudação de uso **procurar** arquivo de banco de dados do botão toofind hello. 
- Clique em Olá **vá** botão backup de saudação tooexport, executar comandos SQL hello e recriar o banco de dados.

## <a name="next-steps"></a>Próximas etapas
[Aplicativos tooAzure banco de dados de conexão para MySQL](./howto-connection-string.md)
