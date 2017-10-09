---
title: "aaaImplement Oracle Data Guard em uma máquina virtual de Linux do Azure | Microsoft Docs"
description: Execute rapidamente o Oracle Data Guard no ambiente do Azure.
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="c437b-103">Implementar o Oracle Data Guard em uma máquina virtual Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="c437b-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="c437b-104">CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="c437b-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="c437b-105">Este artigo descreve como toouse CLI do Azure toodeploy um banco de dados Oracle 12c banco de dados de imagem do hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c437b-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="c437b-106">Este artigo mostra, passo a passo, como tooinstall e configurar a proteção de dados em uma máquina virtual do Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="c437b-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="c437b-107">Antes de começar, verifique se a CLI do Azure está instalada.</span><span class="sxs-lookup"><span data-stu-id="c437b-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="c437b-108">Para obter mais informações, consulte Olá [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c437b-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="c437b-109">Preparar o ambiente de saudação</span><span class="sxs-lookup"><span data-stu-id="c437b-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="c437b-110">Suposições</span><span class="sxs-lookup"><span data-stu-id="c437b-110">Assumptions</span></span>

<span data-ttu-id="c437b-111">tooinstall Oracle Data Guard, você precisa toocreate duas VMs do Azure Olá mesmo conjunto de disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="c437b-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="c437b-112">Olá VM primária (myVM1) tem uma instância do Oracle em execução.</span><span class="sxs-lookup"><span data-stu-id="c437b-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="c437b-113">Olá que VM em espera (myVM2) tenha Olá Oracle instalado somente.</span><span class="sxs-lookup"><span data-stu-id="c437b-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="c437b-114">imagem do Marketplace que você use toocreate Olá VMs Hello for Oracle: Oracle-banco de dados-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="c437b-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="c437b-115">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="c437b-115">Sign in tooAzure</span></span> 

<span data-ttu-id="c437b-116">Entrar tooyour assinatura do Azure usando Olá [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="c437b-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="c437b-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c437b-117">Create a resource group</span></span>

<span data-ttu-id="c437b-118">Criar um grupo de recursos usando Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c437b-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c437b-119">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c437b-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="c437b-120">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westus` local:</span><span class="sxs-lookup"><span data-stu-id="c437b-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="c437b-121">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c437b-121">Create an availability set</span></span>

<span data-ttu-id="c437b-122">A criação de um conjunto de disponibilidade é opcional, mas é recomendável.</span><span class="sxs-lookup"><span data-stu-id="c437b-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="c437b-123">Para obter mais informações, confira [Diretrizes de conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="c437b-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="c437b-124">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c437b-124">Create a virtual machine</span></span>

<span data-ttu-id="c437b-125">Criar uma máquina virtual usando Olá [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c437b-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="c437b-126">Olá, exemplo a seguir cria duas VMs denominadas `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="c437b-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="c437b-127">Ele também criará chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="c437b-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="c437b-128">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="c437b-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="c437b-129">Criar myVM1 (primário):</span><span class="sxs-lookup"><span data-stu-id="c437b-129">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="c437b-130">Depois de criar hello VM, CLI do Azure mostra informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c437b-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="c437b-131">Observe o valor de saudação do `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="c437b-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="c437b-132">Usar o hello de tooaccess esse endereço VM.</span><span class="sxs-lookup"><span data-stu-id="c437b-132">You use this address tooaccess hello VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="c437b-133">Criar myVM2 (em espera):</span><span class="sxs-lookup"><span data-stu-id="c437b-133">Create myVM2 (standby):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="c437b-134">Observe o valor de saudação do `publicIpAddress` depois de criar myVM2.</span><span class="sxs-lookup"><span data-stu-id="c437b-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="c437b-135">Abra a porta TCP para conectividade Olá</span><span class="sxs-lookup"><span data-stu-id="c437b-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="c437b-136">Esta etapa configura pontos de extremidade externos, o que permite que o banco de dados do acesso remoto toohello Oracle.</span><span class="sxs-lookup"><span data-stu-id="c437b-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="c437b-137">Abra a porta Olá para myVM1:</span><span class="sxs-lookup"><span data-stu-id="c437b-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="c437b-138">resultado de saudação deverá ser semelhante toohello resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-138">hello result should look similar toohello following response:</span></span>

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

<span data-ttu-id="c437b-139">Abra a porta Olá para myVM2:</span><span class="sxs-lookup"><span data-stu-id="c437b-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="c437b-140">Conecte-se a máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="c437b-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="c437b-141">A seguir Olá Use o comando toocreate uma sessão SSH com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c437b-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="c437b-142">Substitua o endereço IP de saudação com hello `publicIpAddress` valor para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c437b-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="c437b-143">Criar banco de dados de saudação myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="c437b-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="c437b-144">Olá software Oracle já está instalado na imagem do Marketplace hello, portanto Olá próxima etapa é o banco de dados do tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="c437b-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="c437b-145">Alterne o superusuário do Oracle toohello:</span><span class="sxs-lookup"><span data-stu-id="c437b-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="c437b-146">Crie banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="c437b-146">Create hello database:</span></span>

```bash
$ dbca -silent \
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
<span data-ttu-id="c437b-147">Saídas devem parecer semelhante toohello resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-147">Outputs should look similar toohello following response:</span></span>

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="c437b-148">Definir variáveis ORACLE_SID e ORACLE_HOME hello:</span><span class="sxs-lookup"><span data-stu-id="c437b-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="c437b-149">Opcionalmente, você pode adicionar ORACLE_HOME e ORACLE_SID toohello /home/oracle/.bashrc arquivo, para que essas configurações são salvas para futuras logons:</span><span class="sxs-lookup"><span data-stu-id="c437b-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="c437b-150">Configurar o Data Guard</span><span class="sxs-lookup"><span data-stu-id="c437b-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="c437b-151">Habilitar o modo de log de arquivo morto em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="c437b-151">Enable archive log mode on myVM1 (primary)</span></span>

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
```
<span data-ttu-id="c437b-152">Habilite o registro em log forçado e verifique se há pelo menos um arquivo de log:</span><span class="sxs-lookup"><span data-stu-id="c437b-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="c437b-153">Criar logs de restauração em espera:</span><span class="sxs-lookup"><span data-stu-id="c437b-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="c437b-154">Ativar a reversão (o que torna muito mais fácil a recuperação) e definir o modo de espera\_arquivo\_tooauto de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c437b-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="c437b-155">Saia do SQL*Plus depois disso.</span><span class="sxs-lookup"><span data-stu-id="c437b-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="c437b-156">Configuração de serviço no myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="c437b-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="c437b-157">Editar ou criar o arquivo tnsnames.ora hello, o que está na pasta Olá $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="c437b-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="c437b-158">Adicione Olá entradas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-158">Add hello following entries:</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="c437b-159">Editar ou criar o arquivo listener.ora hello, o que está na pasta Olá $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="c437b-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="c437b-160">Adicione Olá entradas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-160">Add hello following entries:</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="c437b-161">Habilite o Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="c437b-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="c437b-162">Inicie o ouvinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="c437b-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="c437b-163">Configuração de serviço no myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="c437b-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="c437b-164">SSH toomyVM2:</span><span class="sxs-lookup"><span data-stu-id="c437b-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="c437b-165">Faça logon como Oracle:</span><span class="sxs-lookup"><span data-stu-id="c437b-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="c437b-166">Editar ou criar o arquivo tnsnames.ora hello, o que está na pasta Olá $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="c437b-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="c437b-167">Adicione Olá entradas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-167">Add hello following entries:</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="c437b-168">Editar ou criar o arquivo listener.ora hello, o que está na pasta Olá $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="c437b-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="c437b-169">Adicione Olá entradas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-169">Add hello following entries:</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="c437b-170">Inicie o ouvinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="c437b-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="c437b-171">Restaurar Olá toomyVM2 de banco de dados (em espera)</span><span class="sxs-lookup"><span data-stu-id="c437b-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="c437b-172">Crie hello parâmetro arquivo /tmp/initcdb1_stby.ora com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="c437b-173">Crie as pastas:</span><span class="sxs-lookup"><span data-stu-id="c437b-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="c437b-174">Crie um arquivo de senha:</span><span class="sxs-lookup"><span data-stu-id="c437b-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="c437b-175">Inicie o banco de dados de saudação em myVM2:</span><span class="sxs-lookup"><span data-stu-id="c437b-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="c437b-176">Restaure o banco de dados de saudação usando a ferramenta RMAN hello:</span><span class="sxs-lookup"><span data-stu-id="c437b-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="c437b-177">Execute Olá RMAN comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="c437b-178">Verá mensagens semelhantes toohello seguinte quando Olá comando for concluído.</span><span class="sxs-lookup"><span data-stu-id="c437b-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="c437b-179">Saia da RMAN.</span><span class="sxs-lookup"><span data-stu-id="c437b-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="c437b-180">Opcionalmente, você pode adicionar ORACLE_HOME e ORACLE_SID toohello /home/oracle/.bashrc arquivo, para que essas configurações são salvas para futuras logons:</span><span class="sxs-lookup"><span data-stu-id="c437b-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="c437b-181">Habilite o Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="c437b-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="c437b-182">Configurar o Data Guard Broker em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="c437b-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="c437b-183">Inicie o Data Guard Manager e faça logon usando SYS e uma senha.</span><span class="sxs-lookup"><span data-stu-id="c437b-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="c437b-184">(Não use a autenticação do SO.) Execute o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c437b-184">(Do not use OS authentication.) Perform hello following:</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="c437b-185">Configuração de saudação de revisão:</span><span class="sxs-lookup"><span data-stu-id="c437b-185">Review hello configuration:</span></span>
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

<span data-ttu-id="c437b-186">Você concluiu a instalação do Oracle Data Guard hello.</span><span class="sxs-lookup"><span data-stu-id="c437b-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="c437b-187">Olá próxima seção mostra a você como tootest Olá conectividade e passar.</span><span class="sxs-lookup"><span data-stu-id="c437b-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="c437b-188">Conectar o banco de dados de saudação da máquina do cliente Olá</span><span class="sxs-lookup"><span data-stu-id="c437b-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="c437b-189">Atualizar ou criar o arquivo tnsnames.ora de saudação do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="c437b-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="c437b-190">Esse arquivo geralmente está em $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="c437b-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="c437b-191">Substitua os endereços IP hello com seu `publicIpAddress` valores para myVM1 e myVM2:</span><span class="sxs-lookup"><span data-stu-id="c437b-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

<span data-ttu-id="c437b-192">Inicie o SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="c437b-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="c437b-193">Configuração de proteção de dados de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="c437b-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="c437b-194">Opção de banco de dados de saudação em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="c437b-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="c437b-195">tooswitch de toostandby primário (cdb1 toocdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="c437b-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="c437b-196">Agora você pode conectar o banco de dados em espera toohello.</span><span class="sxs-lookup"><span data-stu-id="c437b-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="c437b-197">Inicie o SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="c437b-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="c437b-198">Passar o banco de dados de saudação em myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="c437b-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="c437b-199">tooswitch, execute o seguinte de saudação em myVM2:</span><span class="sxs-lookup"><span data-stu-id="c437b-199">tooswitch over, run hello following on myVM2:</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="c437b-200">Novamente, agora você deve ser toohello tooconnect capaz de banco de dados primário.</span><span class="sxs-lookup"><span data-stu-id="c437b-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="c437b-201">Inicie o SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="c437b-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="c437b-202">Você acabou de instalação hello e a configuração de proteção de dados no Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="c437b-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="c437b-203">Excluir a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="c437b-203">Delete hello virtual machine</span></span>

<span data-ttu-id="c437b-204">Quando você não precisa hello VM, você pode usar Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c437b-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c437b-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c437b-205">Next steps</span></span>

[<span data-ttu-id="c437b-206">Tutorial: criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="c437b-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="c437b-207">Explorar exemplos da CLI do Azure de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="c437b-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
