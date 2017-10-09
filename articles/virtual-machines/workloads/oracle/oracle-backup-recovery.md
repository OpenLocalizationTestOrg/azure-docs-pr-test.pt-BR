---
title: "aaaBack backup e recuperar um banco de dados Oracle 12c banco de dados em uma máquina virtual de Linux do Azure | Microsoft Docs"
description: Saiba como tooback backup e recuperar um banco de dados Oracle 12c banco de dados em seu ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Fazer backup e recuperar um banco de dados Oracle Database 12c em uma máquina virtual Linux do Azure

Você pode usar toocreate CLI do Azure e gerenciar recursos do Azure em um prompt de comando ou use scripts. Neste artigo, podemos usar scripts de CLI do Azure toodeploy um banco de dados Oracle Database 12c de uma imagem da Galeria do Azure Marketplace.

Antes de começar, verifique se a CLI do Azure está instalada. Para obter mais informações, consulte Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Preparar o ambiente de saudação

### <a name="step-1-prerequisites"></a>Etapa 1: pré-requisitos

*   tooperform Olá processo backup e recuperação, você deve primeiro criar uma VM do Linux que tenha uma instância instalada do Oracle Database 12c. imagem do Marketplace Olá você usar toocreate Olá VM é denominada *Oracle: Oracle-banco de dados-Ee:12.1.0.2:latest*.

    toolearn como toocreate um banco de dados Oracle, consulte Olá [Oracle criar início rápido do banco de dados](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-toohello-vm"></a>Etapa 2: Conectar toohello VM

*   toocreate uma sessão Secure Shell (SSH) com hello VM, use Olá comando a seguir. Substitua o endereço IP hello e combinação de nome de host de saudação com hello `publicIpAddress` valor para a VM.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>Etapa 3: Preparar o banco de dados de saudação

1.  Esta etapa pressupõe que você tem uma instância do Oracle (cdb1) que é executada em uma VM chamada *myVM*.

    Executar Olá *oracle* raiz de superusuário e, em seguida, inicializar Olá ouvinte:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  (Opcional) Verifique se o banco de dados de saudação está no modo de log do arquivo:

    ```bash
    $ sqlplus / as sysdba
    SQL> SELECT log_mode FROM v$database;

    LOG_MODE
    ------------
    NOARCHIVELOG

    SQL> SHUTDOWN IMMEDIATE;
    SQL> STARTUP MOUNT;
    SQL> ALTER DATABASE ARCHIVELOG;
    SQL> ALTER DATABASE OPEN;
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  (Opcional) Crie uma confirmação de saudação do tootest de tabela:

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  Verificar ou alterar o tamanho e o local do arquivo de backup hello:

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Use tooback Oracle Recovery Manager (RMAN) o banco de dados de saudação:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>Etapa 4: backup consistente com aplicativo para VMs Linux

Os backups consistentes com aplicativo são um novo recurso do Backup do Azure. Você pode criar e selecione tooexecute scripts antes e depois Olá instantâneo VM (instantâneo pré e pós-instantâneo).

1. Baixe o arquivo JSON de saudação.

    Baixe VMSnapshotScriptPluginConfig.json em https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig. conteúdo do arquivo Hello aparência a seguir toohello semelhante:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. Crie pasta de /etc/azure Olá em Olá VM:

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Copie o arquivo JSON de saudação.

    Copie a pasta de /etc/azure toohello VMSnapshotScriptPluginConfig.json.

4. Edite o arquivo JSON de saudação.

    Editar saudação do hello VMSnapshotScriptPluginConfig.json arquivo tooinclude `PreScriptLocation` e `PostScriptlocation` parâmetros. Por exemplo:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. Crie hello arquivos de script de instantâneo pré e pós-instantâneo.

    Veja este exemplo de scripts de pré-instantâneo e pós-instantâneo para um “backup estático” (um backup offline, com desligamento e reinício):

    Para /etc/azure/pre_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    Para /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    Veja este exemplo de scripts pré-instantâneo e pós-instantâneo para um “backup dinâmico” (um backup online):

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Para /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Para /etc/azure/pre_script.sql, modifique o conteúdo de saudação do arquivo hello por seus requisitos:

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    Para /etc/azure/post_script.sql, modifique o conteúdo de saudação do arquivo hello por seus requisitos:

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. Altere as permissões de arquivo:

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Olá scripts de teste.

    scripts de saudação tootest, primeiro, entre como raiz. Em seguida, verifique se não há erros:

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Para saber mais, consulte [Backup consistente com aplicativo para VMs Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>Etapa 5: Tooback backup Olá VM os cofres de serviços de recuperação do uso do Azure

1.  Em Olá portal do Azure, procure **os cofres de serviços de recuperação**.

    ![Página Cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_01.png)

2.  Em Olá **os cofres de serviços de recuperação** folha, tooadd um novo cofre, clique em **adicionar**.

    ![Página para adicionar cofres aos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, clique em **myVault**.

    ![Página de detalhes de cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_03.png)

4.  Em Olá **myVault** folha, clique em **Backup**.

    ![Página de backup dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_04.png)

5.  Em Olá **Backup meta** folha, use Olá valores padrão **Azure** e **Máquina Virtual**. Clique em **OK**.

    ![Página de detalhes de cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_05.png)

6.  Para **Política de backup**, use **DefaultPolicy** ou selecione **Criar Nova política**. Clique em **OK**.

    ![Página de detalhes da política de backup dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_06.png)

7.  Em Olá **selecionar máquinas virtuais** folha, selecione Olá **myVM1** caixa de seleção e, em seguida, clique em **Okey**. Clique em Olá **habilitar backup** botão.

    ![Página de detalhes de backup recuperação serviços cofres itens toohello](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > Depois de clicar em **habilitar backup**, o processo de backup Olá não for iniciado até hello horário agendado expira. tooset backup de um backup imediato, completo Olá a próxima etapa.

8.  Em Olá **myVault - itens de Backup** folha, em **contagem de itens de BACKUP**, selecione a contagem de itens de backup de saudação.

    ![Página de detalhes myVault de cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_08.png)

9.  Em Olá **itens de Backup (Máquina Virtual do Azure)** folha, Olá direita da página de saudação, clique o botão de reticências de saudação (**...** ) e, em seguida, clique **Backup agora**.

    ![Comando Fazer backup agora dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_09.png)

10. Clique em Olá **Backup** botão. Aguarde Olá toofinish de processo de backup. Em seguida, ir muito[etapa 6: remover arquivos de banco de dados de saudação](#step-6-remove-the-database-files).

    tooview Olá status do trabalho de backup hello, clique em **trabalhos**.

    ![Página de trabalho dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_10.png)

    saudação de status do trabalho de backup de saudação aparece no Olá a imagem a seguir:

    ![Página de trabalho dos cofres dos Serviços de Recuperação com status](./media/oracle-backup-recovery/recovery_service_11.png)

11. Para um backup consistente com o aplicativo, resolva os erros no arquivo de log de saudação. o arquivo de log Hello está localizado em /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.

### <a name="step-6-remove-hello-database-files"></a>Etapa 6: Remover arquivos de banco de dados de saudação 
Neste artigo, você aprenderá como tootest Olá o processo de recuperação. Antes de testar o processo de recuperação hello, você tem arquivos de banco de dados tooremove hello.

1.  Remova arquivos de backup e o espaço de tabela hello:

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (Opcional) Desligar a instância do Oracle hello:

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Restaure os arquivos de saudação excluído de saudação que cofres de serviços de recuperação
Olá toorestore excluídos arquivos, Olá concluir as etapas a seguir:

1. No hello portal do Azure, procure Olá *myVault* item os cofres de serviços de recuperação. Em Olá **visão geral** folha, em **fazer Backup de itens**, selecione Olá número de itens.

    ![Itens do backup myVault dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_12.png)

2. Em **contagem de itens de BACKUP**, selecione Olá número de itens.

    ![Contagem de itens de backup de Máquina Virtual do Azure dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_13.png)

3. Em Olá **myvm1** folha, clique em **a recuperação de arquivos (visualização)**.

    ![Captura de tela de serviços de recuperação de saudação cofres de página de recuperação de arquivo](./media/oracle-backup-recovery/recovery_service_14.png)

4. Em Olá **a recuperação de arquivos (visualização)** painel, clique em **baixar Script**. Em seguida, salve a pasta de tooa de arquivo de download (. sh) de Olá no computador do cliente de saudação.

    ![Opções de salvamento do arquivo de script de download](./media/oracle-backup-recovery/recovery_service_15.png)

5. Copie toohello de arquivo hello. sh VM.

    saudação de exemplo a seguir mostra como você toouse um toomove do comando de cópia seguro (scp) Olá arquivo toohello VM. Você também pode copiar o área de transferência do hello conteúdo toohello e, em seguida, cole Olá conteúdo em um novo arquivo que está configurado no hello VM.

    > [!IMPORTANT]
    > Em Olá exemplo a seguir, certifique-se de que você atualize os valores de endereço e a pasta IP hello. os valores Hello devem mapear toohello pasta onde o arquivo hello é salvo.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Alterar o arquivo hello, para que ele pertence a raiz de saudação.

    Na Olá exemplo a seguir, altere o arquivo hello para que ele pertence a raiz de saudação. Em seguida, altere as permissões.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Olá exemplo a seguir mostra o que você verá após executar Olá precede o script. Quando for solicitado toocontinue, digite **Y**.

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. Acesso toohello montado volumes foi confirmada.

    tooexit, digite **p**e, em seguida, procure Olá montado de volumes. toocreate uma lista de saudação adicionado volumes em um prompt de comando, digite **df -k**.

    ![comando do Hello df -k](./media/oracle-backup-recovery/recovery_service_16.png)

8. Saudação de uso após o script toocopy Olá ausente arquivos toohello back pastas:

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. Olá script a seguir, usam o banco de dados do RMAN toorecover hello:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Desmonte disco hello.

    Em Olá portal do Azure, Olá **a recuperação de arquivos (visualização)** folha, clique em **desmontar discos**.

    ![Comando Desmontar discos](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>Restaurar Olá toda VM

Em vez de restaurar arquivos Olá excluído de cofres de serviços de recuperação de saudação, você pode restaurar Olá VM inteira.

### <a name="step-1-delete-myvm"></a>Etapa 1: excluir myVM

*   No portal do Azure de Olá, vá toohello **myVM1** cofre e, em seguida, selecione **excluir**.

    ![Comando Excluir cofre](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>Etapa 2: Recuperar Olá VM

1.  Vá muito**os cofres de serviços de recuperação**e, em seguida, selecione **myVault**.

    ![Entrada de myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  Em Olá **visão geral** folha, em **fazer Backup de itens**, selecione Olá número de itens.

    ![Itens de backup de myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  Em Olá **itens de Backup (Máquina Virtual do Azure)** folha, selecione **myvm1**.

    ![Página VM de Recuperação](./media/oracle-backup-recovery/recover_vm_04.png)

4.  Em Olá **myvm1** folha, clique nas reticências da saudação (**...** ) e, em seguida, clique **restaurar VM**.

    ![Comando Restaurar VM](./media/oracle-backup-recovery/recover_vm_05.png)

5.  Em Olá **Selecionar ponto de restauração** folha, item de saudação selecione que você deseja toorestore e, em seguida, clique em **Okey**.

    ![Olá Selecionar ponto de restauração](./media/oracle-backup-recovery/recover_vm_06.png)

    Se você tiver habilitado o backup consistente com aplicativo, uma barra azul vertical será exibida.

6.  Em Olá **restaurar configuração** folha, nome da máquina virtual selecione Olá, selecione o grupo de recursos hello e, em seguida, clique em **Okey**.

    ![Restaurar valores de configuração](./media/oracle-backup-recovery/recover_vm_07.png)

7.  Olá toorestore VM, clique em Olá **restaurar** botão.

8.  status de saudação tooview saudação do processo de restauração, clique em **trabalhos**e, em seguida, clique em **trabalhos de Backup**.

    ![Comando Status de trabalhos de backup](./media/oracle-backup-recovery/recover_vm_08.png)

    Olá figura a seguir mostra status Olá Olá do processo de restauração:

    ![Status do processo de restauração Olá](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>Etapa 3: Definir o endereço IP público de saudação
Após Olá que VM é restaurada, configure o endereço IP público de saudação.

1.  Na caixa de pesquisa hello, digite **endereço IP público**.

    ![Lista de endereços IP públicos](./media/oracle-backup-recovery/create_ip_00.png)

2.  Em Olá **endereços IP públicos** folha, clique em **adicionar**. Em Olá **criar endereço IP público** folha, para **nome**, selecione nome do IP público hello. Em **Grupo de recursos**, marque **Usar existente**. Em seguida, clique em **Criar**.

    ![Criar endereço IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  tooassociate Olá endereço IP público com interface de rede Olá para Olá VM, pesquise e selecione **myVMip**. Em seguida, clique em **Associar**.

    ![Associar o endereço IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  Para **Tipo de recurso**, selecione **Adaptador de rede**. Selecione Olá interface de rede que é usada pela instância do hello myVM e, em seguida, clique em **Okey**.

    ![Selecione o tipo de recurso e os valores da NIC](./media/oracle-backup-recovery/create_ip_03.png)

5.  Procure e abra a instância de saudação do myVM é movido do portal de saudação. Olá endereço IP que está associado a saudação VM aparece no hello myVM **visão geral** folha.

    ![Valor do endereço IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>Etapa 4: Conectar toohello VM

*   tooconnect toohello VM, use Olá script a seguir:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>Etapa 5: Testar se o banco de dados de saudação está acessível
*   acessibilidade tootest, Olá use script a seguir:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Banco de dados se hello **inicialização** comando gera um erro, o banco de dados do toorecover hello, consulte [etapa 6: banco de dados Use RMAN toorecover Olá](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>Etapa 6: o banco de dados (opcional) Use RMAN toorecover Olá
*   toorecover Olá banco de dados, use Olá script a seguir:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

backup de saudação e recuperação de banco de dados do hello banco de dados Oracle 12c na VM Linux do Azure está concluída.

## <a name="delete-hello-vm"></a>Excluir Olá VM

Quando não é mais necessário hello VM, você pode usar Olá grupo de recursos do comando tooremove hello, Olá VM e relacionados todos os recursos a seguir:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

[Tutorial: criar VMs altamente disponíveis](../../linux/create-cli-complete.md)

[Explorar exemplos da CLI do Azure de implantação de VM](../../linux/cli-samples.md)



