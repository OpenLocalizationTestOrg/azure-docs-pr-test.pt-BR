---
title: "Implementar o Oracle Data Guard em uma máquina virtual Linux do Azure | Microsoft Docs"
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
ms.openlocfilehash: 11492b85e95ddb39489e36c572af2a168b4c7af8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="10810-103">Implementar o Oracle Data Guard em uma máquina virtual Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="10810-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="10810-104">A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="10810-104">Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="10810-105">Este artigo descreve como usar a CLI do Azure para implantar um banco de dados Oracle Database 12c da imagem do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="10810-105">This article describes how to use Azure CLI to deploy an Oracle Database 12c database from the Azure Marketplace image.</span></span> <span data-ttu-id="10810-106">Este artigo mostra a você passo a passo como instalar e configurar o Data Guard em uma VM (máquina virtual) do Azure.</span><span class="sxs-lookup"><span data-stu-id="10810-106">This article then shows you, step by step, how to install and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="10810-107">Antes de começar, verifique se a CLI do Azure está instalada.</span><span class="sxs-lookup"><span data-stu-id="10810-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="10810-108">Para obter mais informações, consulte o [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="10810-108">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="10810-109">Preparar o ambiente</span><span class="sxs-lookup"><span data-stu-id="10810-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="10810-110">Suposições</span><span class="sxs-lookup"><span data-stu-id="10810-110">Assumptions</span></span>

<span data-ttu-id="10810-111">Para instalar o Oracle Data Guard, você precisa criar duas VMs do Azure no mesmo conjunto de disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="10810-111">To install Oracle Data Guard, you need to create two Azure VMs on the same availability set:</span></span>

- <span data-ttu-id="10810-112">A VM primária (myVM1) tem uma instância do Oracle em execução.</span><span class="sxs-lookup"><span data-stu-id="10810-112">The primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="10810-113">A VM em espera (myVM2) tem o software Oracle apenas instalado.</span><span class="sxs-lookup"><span data-stu-id="10810-113">The standby VM (myVM2) has the Oracle software installed only.</span></span>

<span data-ttu-id="10810-114">A imagem do Marketplace usada para criar as VMs é Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="10810-114">The Marketplace image that you use to create the VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="10810-115">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="10810-115">Sign in to Azure</span></span> 

<span data-ttu-id="10810-116">Entre na sua assinatura do Azure usando o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="10810-116">Sign in to your Azure subscription by using the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="10810-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="10810-117">Create a resource group</span></span>

<span data-ttu-id="10810-118">Crie um grupo de recursos usando o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="10810-118">Create a resource group by using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="10810-119">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="10810-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="10810-120">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `westus`:</span><span class="sxs-lookup"><span data-stu-id="10810-120">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="10810-121">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="10810-121">Create an availability set</span></span>

<span data-ttu-id="10810-122">A criação de um conjunto de disponibilidade é opcional, mas é recomendável.</span><span class="sxs-lookup"><span data-stu-id="10810-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="10810-123">Para obter mais informações, confira [Diretrizes de conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="10810-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="10810-124">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="10810-124">Create a virtual machine</span></span>

<span data-ttu-id="10810-125">Crie uma VM com o comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="10810-125">Create a VM by using the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="10810-126">O exemplo a seguir cria duas VMs, chamadas `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="10810-126">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="10810-127">Ele também criará chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="10810-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="10810-128">Para usar um conjunto específico de chaves, use a opção `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="10810-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="10810-129">Criar myVM1 (primário):</span><span class="sxs-lookup"><span data-stu-id="10810-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="10810-130">Depois de criar a VM, a CLI do Azure exibe informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="10810-130">After you create the VM, Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="10810-131">Observe o valor de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="10810-131">Note the value of `publicIpAddress`.</span></span> <span data-ttu-id="10810-132">Você pode usar esse endereço para acessar a VM.</span><span class="sxs-lookup"><span data-stu-id="10810-132">You use this address to access the VM.</span></span>

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

<span data-ttu-id="10810-133">Criar myVM2 (em espera):</span><span class="sxs-lookup"><span data-stu-id="10810-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="10810-134">Observe o valor de `publicIpAddress` depois de criar myVM2.</span><span class="sxs-lookup"><span data-stu-id="10810-134">Note the value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="10810-135">Abrir a porta TCP para conectividade</span><span class="sxs-lookup"><span data-stu-id="10810-135">Open the TCP port for connectivity</span></span>

<span data-ttu-id="10810-136">Esta etapa configura pontos de extremidade externos, que permitem o acesso remoto ao banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="10810-136">This step configures external endpoints, which allow remote access to the Oracle database.</span></span>

<span data-ttu-id="10810-137">Abrir porta para myVM1:</span><span class="sxs-lookup"><span data-stu-id="10810-137">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="10810-138">O resultado deve ser semelhante à resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="10810-138">The result should look similar to the following response:</span></span>

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

<span data-ttu-id="10810-139">Abra a porta para myVM2:</span><span class="sxs-lookup"><span data-stu-id="10810-139">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="10810-140">Conectar-se à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="10810-140">Connect to the virtual machine</span></span>

<span data-ttu-id="10810-141">Use o seguinte comando para criar uma sessão SSH com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="10810-141">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="10810-142">Substitua o endereço IP pelo valor de `publicIpAddress` de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="10810-142">Replace the IP address with the `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="10810-143">Crie banco de dados myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="10810-143">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="10810-144">O software Oracle já está instalado na imagem do Marketplace, portanto, a próxima etapa é instalar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="10810-144">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="10810-145">Mude para o superusuário Oracle:</span><span class="sxs-lookup"><span data-stu-id="10810-145">Switch to the Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="10810-146">Crie o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="10810-146">Create the database:</span></span>

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
<span data-ttu-id="10810-147">A saída deve ser semelhante à seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="10810-147">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="10810-148">Defina as variáveis ORACLE_SID e ORACLE_HOME:</span><span class="sxs-lookup"><span data-stu-id="10810-148">Set the ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="10810-149">Opcionalmente, você pode adicionar ORACLE_HOME e ORACLE_SID ao arquivo /home/oracle/.bashrc, de maneira que essas configurações sejam salvas para logons futuros:</span><span class="sxs-lookup"><span data-stu-id="10810-149">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="10810-150">Configurar o Data Guard</span><span class="sxs-lookup"><span data-stu-id="10810-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="10810-151">Habilitar o modo de log de arquivo morto em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="10810-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="10810-152">Habilite o registro em log forçado e verifique se há pelo menos um arquivo de log:</span><span class="sxs-lookup"><span data-stu-id="10810-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="10810-153">Criar logs de restauração em espera:</span><span class="sxs-lookup"><span data-stu-id="10810-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="10810-154">Ligue o Flashback (que facilita muito a recuperação) e defina STANDBY\_FILE\_MANAGEMENT como automático.</span><span class="sxs-lookup"><span data-stu-id="10810-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT to auto.</span></span> <span data-ttu-id="10810-155">Saia do SQL*Plus depois disso.</span><span class="sxs-lookup"><span data-stu-id="10810-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="10810-156">Configuração de serviço no myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="10810-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="10810-157">Edite ou crie o arquivo tnsnames.ora, que está na pasta $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="10810-157">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="10810-158">Adicione as seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="10810-158">Add the following entries:</span></span>

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

<span data-ttu-id="10810-159">Edite ou crie o arquivo listener.ora, que está na pasta $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="10810-159">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="10810-160">Adicione as seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="10810-160">Add the following entries:</span></span>

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

<span data-ttu-id="10810-161">Habilite o Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="10810-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="10810-162">Inicie o ouvinte:</span><span class="sxs-lookup"><span data-stu-id="10810-162">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="10810-163">Configuração de serviço no myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="10810-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="10810-164">SSH para myVM2:</span><span class="sxs-lookup"><span data-stu-id="10810-164">SSH to myVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="10810-165">Faça logon como Oracle:</span><span class="sxs-lookup"><span data-stu-id="10810-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="10810-166">Edite ou crie o arquivo tnsnames.ora, que está na pasta $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="10810-166">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="10810-167">Adicione as seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="10810-167">Add the following entries:</span></span>

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

<span data-ttu-id="10810-168">Edite ou crie o arquivo listener.ora, que está na pasta $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="10810-168">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="10810-169">Adicione as seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="10810-169">Add the following entries:</span></span>

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

<span data-ttu-id="10810-170">Inicie o ouvinte:</span><span class="sxs-lookup"><span data-stu-id="10810-170">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-the-database-to-myvm2-standby"></a><span data-ttu-id="10810-171">Restaure banco de dados para myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="10810-171">Restore the database to myVM2 (standby)</span></span>

<span data-ttu-id="10810-172">Crie o arquivo de parâmetro /tmp/initcdb1_stby.ora com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="10810-172">Create the parameter file /tmp/initcdb1_stby.ora with the following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="10810-173">Crie as pastas:</span><span class="sxs-lookup"><span data-stu-id="10810-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="10810-174">Crie um arquivo de senha:</span><span class="sxs-lookup"><span data-stu-id="10810-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="10810-175">Inicie o banco de dados em myVM2:</span><span class="sxs-lookup"><span data-stu-id="10810-175">Start the database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="10810-176">Restaure o banco de dados usando a ferramenta RMAN:</span><span class="sxs-lookup"><span data-stu-id="10810-176">Restore the database by using the RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="10810-177">Executar os seguintes comandos na RMAN:</span><span class="sxs-lookup"><span data-stu-id="10810-177">Run the following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="10810-178">Você verá mensagens semelhantes à seguinte quando o comando for concluído.</span><span class="sxs-lookup"><span data-stu-id="10810-178">You should see messages similar to the following when the command is completed.</span></span> <span data-ttu-id="10810-179">Saia da RMAN.</span><span class="sxs-lookup"><span data-stu-id="10810-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="10810-180">Opcionalmente, você pode adicionar ORACLE_HOME e ORACLE_SID ao arquivo /home/oracle/.bashrc, de maneira que essas configurações sejam salvas para logons futuros:</span><span class="sxs-lookup"><span data-stu-id="10810-180">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="10810-181">Habilite o Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="10810-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="10810-182">Configurar o Data Guard Broker em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="10810-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="10810-183">Inicie o Data Guard Manager e faça logon usando SYS e uma senha.</span><span class="sxs-lookup"><span data-stu-id="10810-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="10810-184">(Não use a autenticação do SO.) Realize o que é descrito a seguir:</span><span class="sxs-lookup"><span data-stu-id="10810-184">(Do not use OS authentication.) Perform the following:</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="10810-185">Examine a configuração:</span><span class="sxs-lookup"><span data-stu-id="10810-185">Review the configuration:</span></span>
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

<span data-ttu-id="10810-186">Você concluiu a configuração do Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="10810-186">You've completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="10810-187">A próxima seção mostra como testar a conectividade e fazer transições.</span><span class="sxs-lookup"><span data-stu-id="10810-187">The next section shows you how to test the connectivity and switch over.</span></span>

### <a name="connect-the-database-from-the-client-machine"></a><span data-ttu-id="10810-188">Conectar o banco de dados do computador cliente</span><span class="sxs-lookup"><span data-stu-id="10810-188">Connect the database from the client machine</span></span>

<span data-ttu-id="10810-189">Atualizar ou criar o arquivo tnsnames.ora no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="10810-189">Update or create the tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="10810-190">Esse arquivo geralmente está em $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="10810-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="10810-191">Substitua os endereços IP pelos valores de `publicIpAddress` para myVM1 e myVM2:</span><span class="sxs-lookup"><span data-stu-id="10810-191">Replace the IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="10810-192">Inicie o SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="10810-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-the-data-guard-configuration"></a><span data-ttu-id="10810-193">Testar as configurações do Data Guard</span><span class="sxs-lookup"><span data-stu-id="10810-193">Test the Data Guard configuration</span></span>

### <a name="switch-over-the-database-on-myvm1-primary"></a><span data-ttu-id="10810-194">Realizar a transição do banco de dados em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="10810-194">Switch over the database on myVM1 (primary)</span></span>

<span data-ttu-id="10810-195">Para mudar de primário para em espera (cdb1 para cdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="10810-195">To switch from primary to standby (cdb1 to cdb1_stby):</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="10810-196">Agora você pode se conectar ao banco de dados em espera.</span><span class="sxs-lookup"><span data-stu-id="10810-196">You can now connect to the standby database.</span></span>

<span data-ttu-id="10810-197">Inicie o SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="10810-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-the-database-on-myvm2-standby"></a><span data-ttu-id="10810-198">Realizar a transição do banco de dados em myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="10810-198">Switch over the database on myVM2 (standby)</span></span>

<span data-ttu-id="10810-199">Para realizar a transição, execute o seguinte em myVM2:</span><span class="sxs-lookup"><span data-stu-id="10810-199">To switch over, run the following on myVM2:</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="10810-200">Novamente, você agora deve ser capaz de se conectar ao banco de dados primário.</span><span class="sxs-lookup"><span data-stu-id="10810-200">Once again, you should now be able to connect to the primary database.</span></span>

<span data-ttu-id="10810-201">Inicie o SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="10810-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="10810-202">Você concluiu a instalação e configuração do Data Guard no Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="10810-202">You've finished the installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="10810-203">Excluir a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="10810-203">Delete the virtual machine</span></span>

<span data-ttu-id="10810-204">Quando a VM não for mais necessária, o comando abaixo poderá ser usado para remover o grupo de recursos, a VM e todos os recursos relacionados:</span><span class="sxs-lookup"><span data-stu-id="10810-204">When you no longer need the VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="10810-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10810-205">Next steps</span></span>

[<span data-ttu-id="10810-206">Tutorial: criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="10810-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="10810-207">Explorar exemplos da CLI do Azure de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="10810-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
