---
title: aaaCreate um banco de dados Oracle em uma VM do Azure | Microsoft Docs
description: Coloque rapidamente em funcionamento um banco de dados Oracle Database 12c no ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="d4e9f-103">Criar um Banco de Dados Oracle em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="d4e9f-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="d4e9f-104">Esses detalhes de guia usando Olá CLI do Azure toodeploy uma máquina virtual do Azure de saudação [imagem da Galeria marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) em ordem toocreate um banco de dados Oracle 12c.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="d4e9f-105">Depois que o servidor de saudação for implantado, você se conecta por meio do SSH no banco de dados da Oracle Olá ordem tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="d4e9f-106">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d4e9f-107">Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d4e9f-108">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d4e9f-109">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d4e9f-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="d4e9f-110">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d4e9f-110">Create a resource group</span></span>

<span data-ttu-id="d4e9f-111">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d4e9f-112">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="d4e9f-113">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="d4e9f-114">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d4e9f-114">Create virtual machine</span></span>

<span data-ttu-id="d4e9f-115">toocreate uma máquina virtual (VM), use Olá [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="d4e9f-116">Olá, exemplo a seguir cria uma VM denominada `myVM`.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="d4e9f-117">Ele também criará chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="d4e9f-118">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="d4e9f-119">Depois de criar hello VM, CLI do Azure exibe informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="d4e9f-120">Observe o valor de saudação para `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="d4e9f-121">Usar o hello de tooaccess esse endereço VM.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-121">You use this address tooaccess hello VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a><span data-ttu-id="d4e9f-122">Conecte-se toohello VM</span><span class="sxs-lookup"><span data-stu-id="d4e9f-122">Connect toohello VM</span></span>

<span data-ttu-id="d4e9f-123">toocreate uma sessão SSH com hello VM, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="d4e9f-124">Substitua o endereço IP de saudação com hello `publicIpAddress` valor para a VM.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="d4e9f-125">Criar banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="d4e9f-125">Create hello database</span></span>

<span data-ttu-id="d4e9f-126">Olá software Oracle já está instalado na imagem do Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="d4e9f-127">Crie um banco de dados de exemplo da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="d4e9f-128">Alternar toohello *oracle* superusuário, em seguida, inicializar o ouvinte de saudação para registro em log:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="d4e9f-129">saída de Hello é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-129">hello output is similar toohello following:</span></span>

    ```bash
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

2.  <span data-ttu-id="d4e9f-130">Crie banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-130">Create hello database:</span></span>

    ```bash
    dbca -silent \
           -createDatabase \
           -templateName General_Purpose.dbc \
           -gdbname cdb1 \
           -sid cdb1 \
           -responseFile NO_VALUE \
           -characterSet AL32UTF8 \
           -sysPassword OraPasswd1 \
           -systemPassword OraPasswd1 \
           -createAsContainerDatabase true \
           -numberOfPDBs 1 \
           -pdbName pdb1 \
           -pdbAdminPassword OraPasswd1 \
           -databaseType MULTIPURPOSE \
           -automaticMemoryManagement false \
           -storageType FS \
           -ignorePreReqs
    ```

    <span data-ttu-id="d4e9f-131">Ele usa o banco de dados Olá toocreate de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="d4e9f-132">Definir variáveis do Oracle</span><span class="sxs-lookup"><span data-stu-id="d4e9f-132">Set Oracle variables</span></span>

<span data-ttu-id="d4e9f-133">Antes de você se conectar, você precisa tooset duas variáveis de ambiente: *ORACLE_HOME* e *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="d4e9f-134">Você também pode adicionar ORACLE_HOME e ORACLE_SID arquivo de. bashrc toohello de variáveis.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="d4e9f-135">Isso salvará as variáveis de ambiente Olá para futuras entradas. Confirme a seguir Olá instruções foram adicionadas toohello `~/.bashrc` arquivo usando o editor de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="d4e9f-136">Conectividade com o Oracle EM Express</span><span class="sxs-lookup"><span data-stu-id="d4e9f-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="d4e9f-137">Para uma ferramenta de gerenciamento de GUI que você pode usar o banco de dados do tooexplore hello, configure o Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="d4e9f-138">tooconnect tooOracle EM Express, você deve primeiro configurar porta Olá no Oracle.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="d4e9f-139">Conecte o banco de dados de tooyour usando sqlplus:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="d4e9f-140">Uma vez conectado, defina a porta de saudação 5502 para Express EM</span><span class="sxs-lookup"><span data-stu-id="d4e9f-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="d4e9f-141">Contêiner Olá abrir PDB1 se não já aberto, mas primeiro verificar o status de saudação:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="d4e9f-142">saída de Hello é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="d4e9f-143">Se Olá OPEN_MODE para `PDB1` não é leitura-gravação, em seguida, execute Olá seguinte comandos tooopen PDB1:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="d4e9f-144">Você precisa tootype `quit` tooend Olá sqlplus sessão e o tipo `exit` toologout saudação do usuário do oracle.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="d4e9f-145">Automatizar a inicialização e o desligamento do banco de dados</span><span class="sxs-lookup"><span data-stu-id="d4e9f-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="d4e9f-146">banco de dados do Oracle Olá por padrão não for iniciado automaticamente quando você reiniciar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="d4e9f-147">tooset backup toostart de banco de dados Oracle Olá automaticamente, primeiro entrar como raiz.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="d4e9f-148">Em seguida, crie e atualize alguns arquivos do sistema.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="d4e9f-149">Conectar-se como raiz</span><span class="sxs-lookup"><span data-stu-id="d4e9f-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="d4e9f-150">Usando seu editor favorito, edite o arquivo hello `/etc/oratab` e alterar o padrão de saudação `N` muito`Y`:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="d4e9f-151">Crie um arquivo chamado `/etc/init.d/dbora` e colar Olá conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="d4e9f-152">Altere as permissões nos arquivos com *chmod* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="d4e9f-153">Crie links simbólicos para inicialização e desligamento, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="d4e9f-154">tootest as alterações, reinicie Olá VM:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="d4e9f-155">Abrir as portas para conectividade</span><span class="sxs-lookup"><span data-stu-id="d4e9f-155">Open ports for connectivity</span></span>

<span data-ttu-id="d4e9f-156">tarefa final Olá é tooconfigure alguns pontos de extremidade externos.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="d4e9f-157">tooset backup Olá grupo de segurança de rede do Azure que protege Olá VM, primeiro a sair de sua sessão de SSH no hello VM (deve ter sido iniciada sem SSH ao reinicializar na etapa anterior).</span><span class="sxs-lookup"><span data-stu-id="d4e9f-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="d4e9f-158">ponto de extremidade de saudação do tooopen que você use o banco de dados do Oracle tooaccess Olá remotamente, crie uma regra de grupo de segurança de rede com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="d4e9f-159">ponto de extremidade de saudação do tooopen que você use tooaccess Oracle EM Express remotamente, crie uma regra de grupo de segurança de rede com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="d4e9f-160">Se necessário, obtenha o endereço IP público de saudação da VM novamente com [az rede ip público exibir](/cli/azure/network/public-ip#show) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4e9f-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="d4e9f-161">Conecte-se ao EM Express pelo navegador.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="d4e9f-162">Verifique se o seu navegador é compatível com EM Express (é necessário ter Flash instalado):</span><span class="sxs-lookup"><span data-stu-id="d4e9f-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="d4e9f-163">Você pode fazer logon usando Olá **SYS** conta e verificar Olá **como sysdba** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="d4e9f-164">Usar a senha de saudação **OraPasswd1** que podem ser definidas durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Captura de tela da página de logon Oracle OEM Express Olá](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="d4e9f-166">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="d4e9f-166">Clean up resources</span></span>

<span data-ttu-id="d4e9f-167">Depois de terminar de explorar seu primeiro banco de dados Oracle no Azure e hello VM não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d4e9f-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4e9f-168">Next steps</span></span>

<span data-ttu-id="d4e9f-169">Saiba mais sobre outras [Soluções Oracle no Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="d4e9f-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="d4e9f-170">Tente Olá [instalando e configurando o Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d4e9f-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
