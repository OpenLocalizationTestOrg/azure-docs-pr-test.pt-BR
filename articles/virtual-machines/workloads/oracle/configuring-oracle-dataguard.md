---
title: Implementar o Oracle Data Guard em VM Linux do Azure | Microsoft Docs
description: Execute rapidamente um Oracle Data Guard no ambiente do Azure.
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
ms.openlocfilehash: fe8b635936c74c5154ec83d34160b9aae61c45e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="82236-103">Implementar o Oracle Data Guard em VM Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="82236-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="82236-104">A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="82236-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="82236-105">Esse guia detalha como usar a CLI do Azure para implantar um banco de dados Oracle 12c por meio da imagem na galeria do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="82236-105">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span></span> <span data-ttu-id="82236-106">Após a criação do banco de dados Oracle, este documento mostra passo a passo como instalar e configurar o Data Guard na VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="82236-106">Once the Oracle database is created, this document shows you step-by-step how to install and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="82236-107">Antes de começar, certifique-se de que a CLI do Azure foi instalada.</span><span class="sxs-lookup"><span data-stu-id="82236-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="82236-108">Para obter mais informações, consulte o [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="82236-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="82236-109">Preparar o ambiente</span><span class="sxs-lookup"><span data-stu-id="82236-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="82236-110">Suposições</span><span class="sxs-lookup"><span data-stu-id="82236-110">Assumptions</span></span>

<span data-ttu-id="82236-111">Para executar a instalação do Oracle Data Guard, você precisa criar duas VMs do Azure no mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="82236-111">To perform the Oracle Data Guard install, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="82236-112">A imagem do Marketplace usada para criar as VMs é "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="82236-112">The Marketplace image you use to create the VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="82236-113">A VM primária (myVM1) tem uma instância do Oracle em execução.</span><span class="sxs-lookup"><span data-stu-id="82236-113">The primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="82236-114">A VM em espera (myVM2) tem o software Oracle apenas instalado.</span><span class="sxs-lookup"><span data-stu-id="82236-114">The standby VM (myVM2) has the Oracle software installed only.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="82236-115">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="82236-115">Log in to Azure</span></span> 

<span data-ttu-id="82236-116">Faça logon na sua assinatura do Azure com o comando [az login](/cli/azure/#login) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="82236-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="82236-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="82236-117">Create a resource group</span></span>

<span data-ttu-id="82236-118">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="82236-118">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="82236-119">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="82236-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="82236-120">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `westus`.</span><span class="sxs-lookup"><span data-stu-id="82236-120">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="82236-121">Criar conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="82236-121">Create availability set</span></span>

<span data-ttu-id="82236-122">Esta etapa é opcional, mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="82236-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="82236-123">Para saber mais, confira [Conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="82236-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="82236-124">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="82236-124">Create virtual machine</span></span>

<span data-ttu-id="82236-125">Crie uma VM com o comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="82236-125">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="82236-126">O exemplo a seguir cria duas VMs chamadas `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="82236-126">The following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="82236-127">Criar chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="82236-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="82236-128">Para usar um conjunto específico de chaves, use a opção `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="82236-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="82236-129">Criar myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="82236-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="82236-130">Após a criação da VM, a CLI do Azure mostra informações semelhantes ao exemplo a seguir: anote o `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="82236-130">Once the VM has been created, the Azure CLI shows information similar to the following example: Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="82236-131">Esse endereço é usado para acessar a VM.</span><span class="sxs-lookup"><span data-stu-id="82236-131">This address is used to access the VM.</span></span>

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

<span data-ttu-id="82236-132">Criar myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="82236-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="82236-133">Anote também o `publicIpAddress` após sua criação.</span><span class="sxs-lookup"><span data-stu-id="82236-133">Take note of the `publicIpAddress` as well once it created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="82236-134">Abrir a porta TCP para conectividade</span><span class="sxs-lookup"><span data-stu-id="82236-134">Open the TCP port for connectivity</span></span>

<span data-ttu-id="82236-135">A etapa serve para configurar os pontos de extremidade externos, o que permite o acesso remoto ao BD Oracle. Execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="82236-135">The step is to configure external endpoints, which allows accessing the Oracle DB remotely, you execute the following command.</span></span>

<span data-ttu-id="82236-136">Abrir porta para myVM1</span><span class="sxs-lookup"><span data-stu-id="82236-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="82236-137">O resultado deve ser semelhante à seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="82236-137">Result should look similar to the following response:</span></span>

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

<span data-ttu-id="82236-138">Abrir porta para myVM2</span><span class="sxs-lookup"><span data-stu-id="82236-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-virtual-machine"></a><span data-ttu-id="82236-139">Conectar-se à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="82236-139">Connect to virtual machine</span></span>

<span data-ttu-id="82236-140">Use o seguinte comando para criar uma sessão SSH com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="82236-140">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="82236-141">Substitua o endereço IP pelo `publicIpAddress` de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="82236-141">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="82236-142">Criar banco de dados myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="82236-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="82236-143">O software Oracle já está instalado na imagem do Marketplace, portanto, a próxima etapa é instalar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="82236-143">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> <span data-ttu-id="82236-144">a primeira etapa é executar como superusuário 'oracle'.</span><span class="sxs-lookup"><span data-stu-id="82236-144">the first step is running as the 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="82236-145">criar o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="82236-145">create the database:</span></span>

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
<span data-ttu-id="82236-146">A saída deve ser semelhante à seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="82236-146">Outputs should look similar to the following response:</span></span>

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

<span data-ttu-id="82236-147">Defina as variáveis ORACLE_SID e ORACLE_HOME</span><span class="sxs-lookup"><span data-stu-id="82236-147">Set the ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="82236-148">Você também pode ter adicionado ORACLE_HOME e ORACLE_SID ao arquivo .bashrc, de maneira que essas configurações sejam salvas para logons futuros.</span><span class="sxs-lookup"><span data-stu-id="82236-148">Optionally, You can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="82236-149">Configurações do Data Guard</span><span class="sxs-lookup"><span data-stu-id="82236-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="82236-150">Habilite o modo de Log de arquivo morto em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="82236-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="82236-151">Habilite o registro em log forçado e verifique se há pelo menos um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="82236-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="82236-152">Criar logs de restauração em espera</span><span class="sxs-lookup"><span data-stu-id="82236-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="82236-153">Ative o Flashback (que realizou a recuperação muito mais cedo) e defina STANDBY_FILE_MANAGEMENT para automático</span><span class="sxs-lookup"><span data-stu-id="82236-153">Turn on Flashback (which made the recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT to auto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="82236-154">Configuração de serviço no myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="82236-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="82236-155">Editar ou criar o arquivo tnsnames.ora, que está localizado na pasta $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="82236-155">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="82236-156">Adicione as seguintes entradas</span><span class="sxs-lookup"><span data-stu-id="82236-156">Add the following entries</span></span>

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

<span data-ttu-id="82236-157">Editar ou criar o arquivo listener.ora, que está localizado na pasta $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="82236-157">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="82236-158">Adicione as seguintes entradas</span><span class="sxs-lookup"><span data-stu-id="82236-158">Add the following entries</span></span>

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

<span data-ttu-id="82236-159">Iniciar o ouvinte</span><span class="sxs-lookup"><span data-stu-id="82236-159">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="82236-160">Configuração de serviço no myVM2 (Em espera)</span><span class="sxs-lookup"><span data-stu-id="82236-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="82236-161">Editar ou criar o arquivo tnsnames.ora, que está localizado na pasta $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="82236-161">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="82236-162">Adicione as seguintes entradas</span><span class="sxs-lookup"><span data-stu-id="82236-162">Add the following entries</span></span>

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

<span data-ttu-id="82236-163">Editar ou criar o arquivo listener.ora, que está localizado na pasta $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="82236-163">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="82236-164">Adicione as seguintes entradas</span><span class="sxs-lookup"><span data-stu-id="82236-164">Add the following entries</span></span>

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

<span data-ttu-id="82236-165">Iniciar o ouvinte</span><span class="sxs-lookup"><span data-stu-id="82236-165">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="82236-166">Habilitar o agente do Data Guard</span><span class="sxs-lookup"><span data-stu-id="82236-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-to-myvm2-standby"></a><span data-ttu-id="82236-167">Restaurar banco de dados para myVM2 (Em espera)</span><span class="sxs-lookup"><span data-stu-id="82236-167">Restore database to myVM2 (Standby)</span></span>

<span data-ttu-id="82236-168">Criar um arquivo de parâmetro '/ tmp/initcdb1_stby.ora' com o seguinte conteúdo</span><span class="sxs-lookup"><span data-stu-id="82236-168">Create a parameter file '/tmp/initcdb1_stby.ora' with the followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="82236-169">Criar pastas</span><span class="sxs-lookup"><span data-stu-id="82236-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="82236-170">Criar arquivo de senha</span><span class="sxs-lookup"><span data-stu-id="82236-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="82236-171">Iniciar o banco de dados em myVM2</span><span class="sxs-lookup"><span data-stu-id="82236-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="82236-172">Restaurar o banco de dados usando o utilitário RMAN</span><span class="sxs-lookup"><span data-stu-id="82236-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="82236-173">Executar os seguintes comandos em RMAN</span><span class="sxs-lookup"><span data-stu-id="82236-173">Execute the following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="82236-174">Habilitar o agente do Data Guard</span><span class="sxs-lookup"><span data-stu-id="82236-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="82236-175">Configurar o agente do Data Guard em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="82236-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="82236-176">Inicie o gerenciador do Data Guard e faça logon usando SYS e a senha (não usando a autenticação do sistema operacional).</span><span class="sxs-lookup"><span data-stu-id="82236-176">Start the Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="82236-177">Realizar o seguinte</span><span class="sxs-lookup"><span data-stu-id="82236-177">Perform the followings</span></span>

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

<span data-ttu-id="82236-178">Analisar a configuração</span><span class="sxs-lookup"><span data-stu-id="82236-178">Review the configuration</span></span>
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

<span data-ttu-id="82236-179">Isso conclui a configuração do Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="82236-179">This completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="82236-180">A próxima seção mostra como testar a conectividade e alternar</span><span class="sxs-lookup"><span data-stu-id="82236-180">The next section shows you how to test the connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="82236-181">Conectar o banco de dados do computador cliente</span><span class="sxs-lookup"><span data-stu-id="82236-181">Connect database from client machine</span></span>

<span data-ttu-id="82236-182">Atualizar ou criar o arquivo tnsnames.ora no computador cliente, que normalmente está localizado em $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="82236-182">Update or create the tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="82236-183">Substitua o IP por seu `publicIpAddress` para myVM1 e myVM2</span><span class="sxs-lookup"><span data-stu-id="82236-183">Replace the IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="82236-184">Iniciar o sqlplus</span><span class="sxs-lookup"><span data-stu-id="82236-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="82236-185">Testar configurações do Data Guard</span><span class="sxs-lookup"><span data-stu-id="82236-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="82236-186">Alternância de banco de dados em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="82236-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="82236-187">Para alternar do primário para o em espera (cdb1 para cdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="82236-187">To switch from primary to standby (cdb1 to cdb1_stby)</span></span>

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

<span data-ttu-id="82236-188">Agora você certamente poderá se conectar ao banco de dados em espera</span><span class="sxs-lookup"><span data-stu-id="82236-188">You should now be able to connect to the standby database</span></span>

<span data-ttu-id="82236-189">Iniciar o sqlplus</span><span class="sxs-lookup"><span data-stu-id="82236-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="82236-190">Nova alternância de banco de dados em myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="82236-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="82236-191">Para voltar, execute o seguinte em myVM2</span><span class="sxs-lookup"><span data-stu-id="82236-191">To switch back, run the followings on myVM2</span></span>
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

<span data-ttu-id="82236-192">Você certamente poderá se conectar novamente ao banco de dados primário</span><span class="sxs-lookup"><span data-stu-id="82236-192">Once again, You should now be able to connect to the primary database</span></span>

<span data-ttu-id="82236-193">Iniciar o sqlplus</span><span class="sxs-lookup"><span data-stu-id="82236-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="82236-194">Isso conclui a instalação e a configuração do Data Guard no Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="82236-194">This completed the installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="82236-195">Excluir máquina virtual</span><span class="sxs-lookup"><span data-stu-id="82236-195">Delete virtual machine</span></span>

<span data-ttu-id="82236-196">Quando não é mais necessário, o comando a seguir pode ser usado para remover o Grupo de Recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="82236-196">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="82236-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82236-197">Next steps</span></span>

[<span data-ttu-id="82236-198">Tutorial Criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="82236-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="82236-199">Explorar as amostras de CLI de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="82236-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
