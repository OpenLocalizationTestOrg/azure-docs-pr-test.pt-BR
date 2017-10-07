---
title: aaaImplement Oracle Data Guard em VM do Linux do Azure | Microsoft Docs
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="318bc-103">Implementar o Oracle Data Guard em VM Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="318bc-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="318bc-104">Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="318bc-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="318bc-105">Esses detalhes de guia usando Olá CLI do Azure toodeploy um Oracle 12c banco de dados de imagem da Galeria Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="318bc-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="318bc-106">Depois de criar o banco de dados de Oracle hello, este documento mostra passo a passo como tooinstall e configurar a proteção de dados na VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="318bc-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="318bc-107">Antes de começar, certifique-se que Olá que CLI do Azure foi instalado.</span><span class="sxs-lookup"><span data-stu-id="318bc-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="318bc-108">Para obter mais informações, consulte o [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="318bc-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="318bc-109">Preparar o ambiente de saudação</span><span class="sxs-lookup"><span data-stu-id="318bc-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="318bc-110">Suposições</span><span class="sxs-lookup"><span data-stu-id="318bc-110">Assumptions</span></span>

<span data-ttu-id="318bc-111">Olá tooperform instalar o Oracle Data Guard, você precisa toocreate duas VMs do Azure Olá mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="318bc-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="318bc-112">imagem do Marketplace Olá usar toocreate Olá VMs é "Oracle: Oracle-banco de dados-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="318bc-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="318bc-113">Olá VM primária (myVM1) tem uma instância do Oracle em execução.</span><span class="sxs-lookup"><span data-stu-id="318bc-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="318bc-114">Olá que VM em espera (myVM2) tenha Olá Oracle instalado somente.</span><span class="sxs-lookup"><span data-stu-id="318bc-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="318bc-115">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="318bc-115">Log in tooAzure</span></span> 

<span data-ttu-id="318bc-116">Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="318bc-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="318bc-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="318bc-117">Create a resource group</span></span>

<span data-ttu-id="318bc-118">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="318bc-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="318bc-119">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="318bc-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="318bc-120">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westus` local.</span><span class="sxs-lookup"><span data-stu-id="318bc-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="318bc-121">Criar conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="318bc-121">Create availability set</span></span>

<span data-ttu-id="318bc-122">Esta etapa é opcional, mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="318bc-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="318bc-123">Para saber mais, confira [Conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="318bc-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="318bc-124">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="318bc-124">Create virtual machine</span></span>

<span data-ttu-id="318bc-125">Criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="318bc-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="318bc-126">Olá, exemplo a seguir cria 2 VMs denominadas `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="318bc-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="318bc-127">Criar chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="318bc-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="318bc-128">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="318bc-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="318bc-129">Criar myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="318bc-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="318bc-130">Uma vez Olá VM foi criada, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir: Anote Olá `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="318bc-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="318bc-131">Esse endereço é usado tooaccess Olá VM.</span><span class="sxs-lookup"><span data-stu-id="318bc-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="318bc-132">Criar myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="318bc-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="318bc-133">Anote Olá `publicIpAddress` também uma vez ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="318bc-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="318bc-134">Abra a porta TCP para conectividade Olá</span><span class="sxs-lookup"><span data-stu-id="318bc-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="318bc-135">a etapa de saudação é tooconfigure pontos de extremidade externos, que permite acessar remotamente o hello banco de dados Oracle, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="318bc-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="318bc-136">Abrir porta para myVM1</span><span class="sxs-lookup"><span data-stu-id="318bc-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="318bc-137">Resultado deverá ser semelhante toohello resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="318bc-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="318bc-138">Abrir porta para myVM2</span><span class="sxs-lookup"><span data-stu-id="318bc-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="318bc-139">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="318bc-139">Connect toovirtual machine</span></span>

<span data-ttu-id="318bc-140">A seguir Olá Use o comando toocreate uma sessão SSH com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="318bc-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="318bc-141">Substitua o endereço IP de saudação com hello `publicIpAddress` de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="318bc-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="318bc-142">Criar banco de dados myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="318bc-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="318bc-143">Olá software Oracle já está instalado na imagem do Marketplace hello, portanto Olá próxima etapa é o banco de dados do tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="318bc-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="318bc-144">primeira etapa do Hello está sendo executado como superusuário do hello 'oracle'.</span><span class="sxs-lookup"><span data-stu-id="318bc-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="318bc-145">Crie banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="318bc-145">create hello database:</span></span>

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
<span data-ttu-id="318bc-146">Saídas devem parecer semelhante toohello resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="318bc-146">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="318bc-147">Definir variáveis ORACLE_SID e ORACLE_HOME Olá</span><span class="sxs-lookup"><span data-stu-id="318bc-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="318bc-148">Opcionalmente, você pode ORACLE_HOME e ORACLE_SID toohello. bashrc arquivo adicionado, para que essas configurações são salvas para logons futuros.</span><span class="sxs-lookup"><span data-stu-id="318bc-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="318bc-149">Configurações do Data Guard</span><span class="sxs-lookup"><span data-stu-id="318bc-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="318bc-150">Habilite o modo de Log de arquivo morto em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="318bc-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="318bc-151">Habilite o registro em log forçado e verifique se há pelo menos um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="318bc-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="318bc-152">Criar logs de restauração em espera</span><span class="sxs-lookup"><span data-stu-id="318bc-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="318bc-153">Ativar a reversão (que fez recuperação Olá muito anteriormente) e defina STANDBY_FILE_MANAGEMENT tooauto</span><span class="sxs-lookup"><span data-stu-id="318bc-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="318bc-154">Configuração de serviço no myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="318bc-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="318bc-155">Editar ou criar o arquivo tnsnames.ora hello, o que está localizado na pasta de ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="318bc-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="318bc-156">Adicionar Olá entradas a seguir</span><span class="sxs-lookup"><span data-stu-id="318bc-156">Add hello following entries</span></span>

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

<span data-ttu-id="318bc-157">Editar ou criar o arquivo listener.ora hello, o que está localizado na pasta de ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="318bc-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="318bc-158">Adicionar Olá entradas a seguir</span><span class="sxs-lookup"><span data-stu-id="318bc-158">Add hello following entries</span></span>

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

<span data-ttu-id="318bc-159">Iniciar o ouvinte de saudação</span><span class="sxs-lookup"><span data-stu-id="318bc-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="318bc-160">Configuração de serviço no myVM2 (Em espera)</span><span class="sxs-lookup"><span data-stu-id="318bc-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="318bc-161">Editar ou criar o arquivo tnsnames.ora hello, o que está localizado na pasta de ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="318bc-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="318bc-162">Adicionar Olá entradas a seguir</span><span class="sxs-lookup"><span data-stu-id="318bc-162">Add hello following entries</span></span>

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

<span data-ttu-id="318bc-163">Editar ou criar o arquivo listener.ora hello, o que está localizado na pasta de ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="318bc-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="318bc-164">Adicionar Olá entradas a seguir</span><span class="sxs-lookup"><span data-stu-id="318bc-164">Add hello following entries</span></span>

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

<span data-ttu-id="318bc-165">Iniciar o ouvinte de saudação</span><span class="sxs-lookup"><span data-stu-id="318bc-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="318bc-166">Habilitar o agente do Data Guard</span><span class="sxs-lookup"><span data-stu-id="318bc-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="318bc-167">Restaurar o banco de dados toomyVM2 (espera)</span><span class="sxs-lookup"><span data-stu-id="318bc-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="318bc-168">Criar um arquivo de parâmetro ' / tmp/initcdb1_stby.ora' com conteúdo do seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="318bc-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="318bc-169">Criar pastas</span><span class="sxs-lookup"><span data-stu-id="318bc-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="318bc-170">Criar arquivo de senha</span><span class="sxs-lookup"><span data-stu-id="318bc-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="318bc-171">Iniciar o banco de dados em myVM2</span><span class="sxs-lookup"><span data-stu-id="318bc-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="318bc-172">Restaurar o banco de dados usando o utilitário RMAN</span><span class="sxs-lookup"><span data-stu-id="318bc-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="318bc-173">Executar Olá RMAN comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="318bc-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="318bc-174">Habilitar o agente do Data Guard</span><span class="sxs-lookup"><span data-stu-id="318bc-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="318bc-175">Configurar o agente do Data Guard em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="318bc-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="318bc-176">Inicie o Gerenciador de proteção de dados hello e faça logon usando SYS e a senha (não usando a autenticação do sistema operacional do).</span><span class="sxs-lookup"><span data-stu-id="318bc-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="318bc-177">Execute o seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="318bc-177">Perform hello followings</span></span>

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

<span data-ttu-id="318bc-178">Configuração de saudação de revisão</span><span class="sxs-lookup"><span data-stu-id="318bc-178">Review hello configuration</span></span>
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

<span data-ttu-id="318bc-179">Isso concluído a instalação Oracle Data Guard hello.</span><span class="sxs-lookup"><span data-stu-id="318bc-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="318bc-180">Olá próxima seção mostra como tootest Olá conectividade e alternando</span><span class="sxs-lookup"><span data-stu-id="318bc-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="318bc-181">Conectar o banco de dados do computador cliente</span><span class="sxs-lookup"><span data-stu-id="318bc-181">Connect database from client machine</span></span>

<span data-ttu-id="318bc-182">Atualizar ou criar o arquivo tnsnames.ora de saudação do computador cliente, que normalmente está localizado em ORACLE_HOME\network\admin $.</span><span class="sxs-lookup"><span data-stu-id="318bc-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="318bc-183">Substituir saudação IP com o `publicIpAddress` para myVM1 e myVM2</span><span class="sxs-lookup"><span data-stu-id="318bc-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="318bc-184">Iniciar o sqlplus</span><span class="sxs-lookup"><span data-stu-id="318bc-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="318bc-185">Testar configurações do Data Guard</span><span class="sxs-lookup"><span data-stu-id="318bc-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="318bc-186">Alternância de banco de dados em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="318bc-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="318bc-187">tooswitch de toostandby primário (cdb1 toocdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="318bc-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

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

<span data-ttu-id="318bc-188">Agora você deve ser toohello tooconnect capaz de banco de dados em espera</span><span class="sxs-lookup"><span data-stu-id="318bc-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="318bc-189">Iniciar o sqlplus</span><span class="sxs-lookup"><span data-stu-id="318bc-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="318bc-190">Nova alternância de banco de dados em myVM2 (em espera)</span><span class="sxs-lookup"><span data-stu-id="318bc-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="318bc-191">tooswitch novamente, execute o seguinte Olá no myVM2</span><span class="sxs-lookup"><span data-stu-id="318bc-191">tooswitch back, run hello followings on myVM2</span></span>
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

<span data-ttu-id="318bc-192">Novamente, agora você deve ser toohello tooconnect capaz de banco de dados primário</span><span class="sxs-lookup"><span data-stu-id="318bc-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="318bc-193">Iniciar o sqlplus</span><span class="sxs-lookup"><span data-stu-id="318bc-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="318bc-194">Isso concluído Olá instalação e configuração de proteção de dados em Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="318bc-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="318bc-195">Excluir máquina virtual</span><span class="sxs-lookup"><span data-stu-id="318bc-195">Delete virtual machine</span></span>

<span data-ttu-id="318bc-196">Quando não é mais necessário, Olá comando a seguir pode ser usado tooremove Olá grupo de recursos, VM, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="318bc-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="318bc-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="318bc-197">Next steps</span></span>

[<span data-ttu-id="318bc-198">Tutorial Criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="318bc-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="318bc-199">Explorar as amostras de CLI de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="318bc-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
