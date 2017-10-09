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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="12dd9-103">Fazer backup e recuperar um banco de dados Oracle Database 12c em uma máquina virtual Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="12dd9-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="12dd9-104">Você pode usar toocreate CLI do Azure e gerenciar recursos do Azure em um prompt de comando ou use scripts.</span><span class="sxs-lookup"><span data-stu-id="12dd9-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="12dd9-105">Neste artigo, podemos usar scripts de CLI do Azure toodeploy um banco de dados Oracle Database 12c de uma imagem da Galeria do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="12dd9-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="12dd9-106">Antes de começar, verifique se a CLI do Azure está instalada.</span><span class="sxs-lookup"><span data-stu-id="12dd9-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="12dd9-107">Para obter mais informações, consulte Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="12dd9-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="12dd9-108">Preparar o ambiente de saudação</span><span class="sxs-lookup"><span data-stu-id="12dd9-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="12dd9-109">Etapa 1: pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="12dd9-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="12dd9-110">tooperform Olá processo backup e recuperação, você deve primeiro criar uma VM do Linux que tenha uma instância instalada do Oracle Database 12c.</span><span class="sxs-lookup"><span data-stu-id="12dd9-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="12dd9-111">imagem do Marketplace Olá você usar toocreate Olá VM é denominada *Oracle: Oracle-banco de dados-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="12dd9-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="12dd9-112">toolearn como toocreate um banco de dados Oracle, consulte Olá [Oracle criar início rápido do banco de dados](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="12dd9-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="12dd9-113">Etapa 2: Conectar toohello VM</span><span class="sxs-lookup"><span data-stu-id="12dd9-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="12dd9-114">toocreate uma sessão Secure Shell (SSH) com hello VM, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="12dd9-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="12dd9-115">Substitua o endereço IP hello e combinação de nome de host de saudação com hello `publicIpAddress` valor para a VM.</span><span class="sxs-lookup"><span data-stu-id="12dd9-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="12dd9-116">Etapa 3: Preparar o banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="12dd9-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="12dd9-117">Esta etapa pressupõe que você tem uma instância do Oracle (cdb1) que é executada em uma VM chamada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="12dd9-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="12dd9-118">Executar Olá *oracle* raiz de superusuário e, em seguida, inicializar Olá ouvinte:</span><span class="sxs-lookup"><span data-stu-id="12dd9-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

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

2.  <span data-ttu-id="12dd9-119">(Opcional) Verifique se o banco de dados de saudação está no modo de log do arquivo:</span><span class="sxs-lookup"><span data-stu-id="12dd9-119">(Optional) Make sure hello database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="12dd9-120">(Opcional) Crie uma confirmação de saudação do tootest de tabela:</span><span class="sxs-lookup"><span data-stu-id="12dd9-120">(Optional) Create a table tootest hello commit:</span></span>

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
4.  <span data-ttu-id="12dd9-121">Verificar ou alterar o tamanho e o local do arquivo de backup hello:</span><span class="sxs-lookup"><span data-stu-id="12dd9-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="12dd9-122">Use tooback Oracle Recovery Manager (RMAN) o banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="12dd9-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="12dd9-123">Etapa 4: backup consistente com aplicativo para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="12dd9-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="12dd9-124">Os backups consistentes com aplicativo são um novo recurso do Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="12dd9-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="12dd9-125">Você pode criar e selecione tooexecute scripts antes e depois Olá instantâneo VM (instantâneo pré e pós-instantâneo).</span><span class="sxs-lookup"><span data-stu-id="12dd9-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="12dd9-126">Baixe o arquivo JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-126">Download hello JSON file.</span></span>

    <span data-ttu-id="12dd9-127">Baixe VMSnapshotScriptPluginConfig.json em https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="12dd9-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="12dd9-128">conteúdo do arquivo Hello aparência a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="12dd9-128">hello file contents look similar toohello following:</span></span>

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

2. <span data-ttu-id="12dd9-129">Crie pasta de /etc/azure Olá em Olá VM:</span><span class="sxs-lookup"><span data-stu-id="12dd9-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="12dd9-130">Copie o arquivo JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="12dd9-131">Copie a pasta de /etc/azure toohello VMSnapshotScriptPluginConfig.json.</span><span class="sxs-lookup"><span data-stu-id="12dd9-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="12dd9-132">Edite o arquivo JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="12dd9-133">Editar saudação do hello VMSnapshotScriptPluginConfig.json arquivo tooinclude `PreScriptLocation` e `PostScriptlocation` parâmetros.</span><span class="sxs-lookup"><span data-stu-id="12dd9-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="12dd9-134">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="12dd9-134">For example:</span></span>

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

5. <span data-ttu-id="12dd9-135">Crie hello arquivos de script de instantâneo pré e pós-instantâneo.</span><span class="sxs-lookup"><span data-stu-id="12dd9-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="12dd9-136">Veja este exemplo de scripts de pré-instantâneo e pós-instantâneo para um “backup estático” (um backup offline, com desligamento e reinício):</span><span class="sxs-lookup"><span data-stu-id="12dd9-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="12dd9-137">Para /etc/azure/pre_script.sh:</span><span class="sxs-lookup"><span data-stu-id="12dd9-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="12dd9-138">Para /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="12dd9-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="12dd9-139">Veja este exemplo de scripts pré-instantâneo e pós-instantâneo para um “backup dinâmico” (um backup online):</span><span class="sxs-lookup"><span data-stu-id="12dd9-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="12dd9-140">Para /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="12dd9-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="12dd9-141">Para /etc/azure/pre_script.sql, modifique o conteúdo de saudação do arquivo hello por seus requisitos:</span><span class="sxs-lookup"><span data-stu-id="12dd9-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="12dd9-142">Para /etc/azure/post_script.sql, modifique o conteúdo de saudação do arquivo hello por seus requisitos:</span><span class="sxs-lookup"><span data-stu-id="12dd9-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="12dd9-143">Altere as permissões de arquivo:</span><span class="sxs-lookup"><span data-stu-id="12dd9-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="12dd9-144">Olá scripts de teste.</span><span class="sxs-lookup"><span data-stu-id="12dd9-144">Test hello scripts.</span></span>

    <span data-ttu-id="12dd9-145">scripts de saudação tootest, primeiro, entre como raiz.</span><span class="sxs-lookup"><span data-stu-id="12dd9-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="12dd9-146">Em seguida, verifique se não há erros:</span><span class="sxs-lookup"><span data-stu-id="12dd9-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="12dd9-147">Para saber mais, consulte [Backup consistente com aplicativo para VMs Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="12dd9-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="12dd9-148">Etapa 5: Tooback backup Olá VM os cofres de serviços de recuperação do uso do Azure</span><span class="sxs-lookup"><span data-stu-id="12dd9-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="12dd9-149">Em Olá portal do Azure, procure **os cofres de serviços de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Página Cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="12dd9-151">Em Olá **os cofres de serviços de recuperação** folha, tooadd um novo cofre, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![Página para adicionar cofres aos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="12dd9-153">toocontinue, clique em **myVault**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-153">toocontinue, click **myVault**.</span></span>

    ![Página de detalhes de cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="12dd9-155">Em Olá **myVault** folha, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![Página de backup dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="12dd9-157">Em Olá **Backup meta** folha, use Olá valores padrão **Azure** e **Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="12dd9-158">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-158">Click **OK**.</span></span>

    ![Página de detalhes de cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="12dd9-160">Para **Política de backup**, use **DefaultPolicy** ou selecione **Criar Nova política**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="12dd9-161">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-161">Click **OK**.</span></span>

    ![Página de detalhes da política de backup dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="12dd9-163">Em Olá **selecionar máquinas virtuais** folha, selecione Olá **myVM1** caixa de seleção e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="12dd9-164">Clique em Olá **habilitar backup** botão.</span><span class="sxs-lookup"><span data-stu-id="12dd9-164">Click hello **Enable backup** button.</span></span>

    ![Página de detalhes de backup recuperação serviços cofres itens toohello](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="12dd9-166">Depois de clicar em **habilitar backup**, o processo de backup Olá não for iniciado até hello horário agendado expira.</span><span class="sxs-lookup"><span data-stu-id="12dd9-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="12dd9-167">tooset backup de um backup imediato, completo Olá a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="12dd9-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="12dd9-168">Em Olá **myVault - itens de Backup** folha, em **contagem de itens de BACKUP**, selecione a contagem de itens de backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![Página de detalhes myVault de cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="12dd9-170">Em Olá **itens de Backup (Máquina Virtual do Azure)** folha, Olá direita da página de saudação, clique o botão de reticências de saudação (**...** ) e, em seguida, clique **Backup agora**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Comando Fazer backup agora dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="12dd9-172">Clique em Olá **Backup** botão.</span><span class="sxs-lookup"><span data-stu-id="12dd9-172">Click hello **Backup** button.</span></span> <span data-ttu-id="12dd9-173">Aguarde Olá toofinish de processo de backup.</span><span class="sxs-lookup"><span data-stu-id="12dd9-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="12dd9-174">Em seguida, ir muito[etapa 6: remover arquivos de banco de dados de saudação](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="12dd9-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="12dd9-175">tooview Olá status do trabalho de backup hello, clique em **trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![Página de trabalho dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="12dd9-177">saudação de status do trabalho de backup de saudação aparece no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="12dd9-177">hello status of hello backup job appears in hello following image:</span></span>

    ![Página de trabalho dos cofres dos Serviços de Recuperação com status](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="12dd9-179">Para um backup consistente com o aplicativo, resolva os erros no arquivo de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="12dd9-180">o arquivo de log Hello está localizado em /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="12dd9-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="12dd9-181">Etapa 6: Remover arquivos de banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="12dd9-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="12dd9-182">Neste artigo, você aprenderá como tootest Olá o processo de recuperação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="12dd9-183">Antes de testar o processo de recuperação hello, você tem arquivos de banco de dados tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="12dd9-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="12dd9-184">Remova arquivos de backup e o espaço de tabela hello:</span><span class="sxs-lookup"><span data-stu-id="12dd9-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="12dd9-185">(Opcional) Desligar a instância do Oracle hello:</span><span class="sxs-lookup"><span data-stu-id="12dd9-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="12dd9-186">Restaure os arquivos de saudação excluído de saudação que cofres de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="12dd9-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="12dd9-187">Olá toorestore excluídos arquivos, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="12dd9-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="12dd9-188">No hello portal do Azure, procure Olá *myVault* item os cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="12dd9-189">Em Olá **visão geral** folha, em **fazer Backup de itens**, selecione Olá número de itens.</span><span class="sxs-lookup"><span data-stu-id="12dd9-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Itens do backup myVault dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="12dd9-191">Em **contagem de itens de BACKUP**, selecione Olá número de itens.</span><span class="sxs-lookup"><span data-stu-id="12dd9-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![Contagem de itens de backup de Máquina Virtual do Azure dos cofres dos Serviços de Recuperação](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="12dd9-193">Em Olá **myvm1** folha, clique em **a recuperação de arquivos (visualização)**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Captura de tela de serviços de recuperação de saudação cofres de página de recuperação de arquivo](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="12dd9-195">Em Olá **a recuperação de arquivos (visualização)** painel, clique em **baixar Script**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="12dd9-196">Em seguida, salve a pasta de tooa de arquivo de download (. sh) de Olá no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![Opções de salvamento do arquivo de script de download](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="12dd9-198">Copie toohello de arquivo hello. sh VM.</span><span class="sxs-lookup"><span data-stu-id="12dd9-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="12dd9-199">saudação de exemplo a seguir mostra como você toouse um toomove do comando de cópia seguro (scp) Olá arquivo toohello VM.</span><span class="sxs-lookup"><span data-stu-id="12dd9-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="12dd9-200">Você também pode copiar o área de transferência do hello conteúdo toohello e, em seguida, cole Olá conteúdo em um novo arquivo que está configurado no hello VM.</span><span class="sxs-lookup"><span data-stu-id="12dd9-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="12dd9-201">Em Olá exemplo a seguir, certifique-se de que você atualize os valores de endereço e a pasta IP hello.</span><span class="sxs-lookup"><span data-stu-id="12dd9-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="12dd9-202">os valores Hello devem mapear toohello pasta onde o arquivo hello é salvo.</span><span class="sxs-lookup"><span data-stu-id="12dd9-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="12dd9-203">Alterar o arquivo hello, para que ele pertence a raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="12dd9-204">Na Olá exemplo a seguir, altere o arquivo hello para que ele pertence a raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="12dd9-205">Em seguida, altere as permissões.</span><span class="sxs-lookup"><span data-stu-id="12dd9-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="12dd9-206">Olá exemplo a seguir mostra o que você verá após executar Olá precede o script.</span><span class="sxs-lookup"><span data-stu-id="12dd9-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="12dd9-207">Quando for solicitado toocontinue, digite **Y**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-207">When you're prompted toocontinue, enter **Y**.</span></span>

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

7. <span data-ttu-id="12dd9-208">Acesso toohello montado volumes foi confirmada.</span><span class="sxs-lookup"><span data-stu-id="12dd9-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="12dd9-209">tooexit, digite **p**e, em seguida, procure Olá montado de volumes.</span><span class="sxs-lookup"><span data-stu-id="12dd9-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="12dd9-210">toocreate uma lista de saudação adicionado volumes em um prompt de comando, digite **df -k**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![comando do Hello df -k](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="12dd9-212">Saudação de uso após o script toocopy Olá ausente arquivos toohello back pastas:</span><span class="sxs-lookup"><span data-stu-id="12dd9-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

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
9. <span data-ttu-id="12dd9-213">Olá script a seguir, usam o banco de dados do RMAN toorecover hello:</span><span class="sxs-lookup"><span data-stu-id="12dd9-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="12dd9-214">Desmonte disco hello.</span><span class="sxs-lookup"><span data-stu-id="12dd9-214">Unmount hello disk.</span></span>

    <span data-ttu-id="12dd9-215">Em Olá portal do Azure, Olá **a recuperação de arquivos (visualização)** folha, clique em **desmontar discos**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Comando Desmontar discos](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="12dd9-217">Restaurar Olá toda VM</span><span class="sxs-lookup"><span data-stu-id="12dd9-217">Restore hello entire VM</span></span>

<span data-ttu-id="12dd9-218">Em vez de restaurar arquivos Olá excluído de cofres de serviços de recuperação de saudação, você pode restaurar Olá VM inteira.</span><span class="sxs-lookup"><span data-stu-id="12dd9-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="12dd9-219">Etapa 1: excluir myVM</span><span class="sxs-lookup"><span data-stu-id="12dd9-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="12dd9-220">No portal do Azure de Olá, vá toohello **myVM1** cofre e, em seguida, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![Comando Excluir cofre](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="12dd9-222">Etapa 2: Recuperar Olá VM</span><span class="sxs-lookup"><span data-stu-id="12dd9-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="12dd9-223">Vá muito**os cofres de serviços de recuperação**e, em seguida, selecione **myVault**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![Entrada de myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="12dd9-225">Em Olá **visão geral** folha, em **fazer Backup de itens**, selecione Olá número de itens.</span><span class="sxs-lookup"><span data-stu-id="12dd9-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Itens de backup de myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="12dd9-227">Em Olá **itens de Backup (Máquina Virtual do Azure)** folha, selecione **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Página VM de Recuperação](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="12dd9-229">Em Olá **myvm1** folha, clique nas reticências da saudação (**...** ) e, em seguida, clique **restaurar VM**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![Comando Restaurar VM](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="12dd9-231">Em Olá **Selecionar ponto de restauração** folha, item de saudação selecione que você deseja toorestore e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![Olá Selecionar ponto de restauração](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="12dd9-233">Se você tiver habilitado o backup consistente com aplicativo, uma barra azul vertical será exibida.</span><span class="sxs-lookup"><span data-stu-id="12dd9-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="12dd9-234">Em Olá **restaurar configuração** folha, nome da máquina virtual selecione Olá, selecione o grupo de recursos hello e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![Restaurar valores de configuração](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="12dd9-236">Olá toorestore VM, clique em Olá **restaurar** botão.</span><span class="sxs-lookup"><span data-stu-id="12dd9-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="12dd9-237">status de saudação tooview saudação do processo de restauração, clique em **trabalhos**e, em seguida, clique em **trabalhos de Backup**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Comando Status de trabalhos de backup](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="12dd9-239">Olá figura a seguir mostra status Olá Olá do processo de restauração:</span><span class="sxs-lookup"><span data-stu-id="12dd9-239">hello following figure shows hello status of hello restore process:</span></span>

    ![Status do processo de restauração Olá](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="12dd9-241">Etapa 3: Definir o endereço IP público de saudação</span><span class="sxs-lookup"><span data-stu-id="12dd9-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="12dd9-242">Após Olá que VM é restaurada, configure o endereço IP público de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="12dd9-243">Na caixa de pesquisa hello, digite **endereço IP público**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-243">In hello search box, enter **public IP address**.</span></span>

    ![Lista de endereços IP públicos](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="12dd9-245">Em Olá **endereços IP públicos** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="12dd9-246">Em Olá **criar endereço IP público** folha, para **nome**, selecione nome do IP público hello.</span><span class="sxs-lookup"><span data-stu-id="12dd9-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="12dd9-247">Em **Grupo de recursos**, marque **Usar existente**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="12dd9-248">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-248">Then, click **Create**.</span></span>

    ![Criar endereço IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="12dd9-250">tooassociate Olá endereço IP público com interface de rede Olá para Olá VM, pesquise e selecione **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="12dd9-251">Em seguida, clique em **Associar**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-251">Then, click **Associate**.</span></span>

    ![Associar o endereço IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="12dd9-253">Para **Tipo de recurso**, selecione **Adaptador de rede**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="12dd9-254">Selecione Olá interface de rede que é usada pela instância do hello myVM e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="12dd9-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![Selecione o tipo de recurso e os valores da NIC](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="12dd9-256">Procure e abra a instância de saudação do myVM é movido do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="12dd9-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="12dd9-257">Olá endereço IP que está associado a saudação VM aparece no hello myVM **visão geral** folha.</span><span class="sxs-lookup"><span data-stu-id="12dd9-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![Valor do endereço IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="12dd9-259">Etapa 4: Conectar toohello VM</span><span class="sxs-lookup"><span data-stu-id="12dd9-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="12dd9-260">tooconnect toohello VM, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="12dd9-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="12dd9-261">Etapa 5: Testar se o banco de dados de saudação está acessível</span><span class="sxs-lookup"><span data-stu-id="12dd9-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="12dd9-262">acessibilidade tootest, Olá use script a seguir:</span><span class="sxs-lookup"><span data-stu-id="12dd9-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="12dd9-263">Banco de dados se hello **inicialização** comando gera um erro, o banco de dados do toorecover hello, consulte [etapa 6: banco de dados Use RMAN toorecover Olá](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="12dd9-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="12dd9-264">Etapa 6: o banco de dados (opcional) Use RMAN toorecover Olá</span><span class="sxs-lookup"><span data-stu-id="12dd9-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="12dd9-265">toorecover Olá banco de dados, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="12dd9-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="12dd9-266">backup de saudação e recuperação de banco de dados do hello banco de dados Oracle 12c na VM Linux do Azure está concluída.</span><span class="sxs-lookup"><span data-stu-id="12dd9-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="12dd9-267">Excluir Olá VM</span><span class="sxs-lookup"><span data-stu-id="12dd9-267">Delete hello VM</span></span>

<span data-ttu-id="12dd9-268">Quando não é mais necessário hello VM, você pode usar Olá grupo de recursos do comando tooremove hello, Olá VM e relacionados todos os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="12dd9-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="12dd9-269">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12dd9-269">Next steps</span></span>

[<span data-ttu-id="12dd9-270">Tutorial: criar VMs altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="12dd9-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="12dd9-271">Explorar exemplos da CLI do Azure de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="12dd9-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



