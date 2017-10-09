---
title: aaaImplement Oracle Golden Gate em uma VM do Linux do Azure | Microsoft Docs
description: Coloque rapidamente em funcionamento um Oracle Golden Gate no seu ambiente do Azure.
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="bb0da-103">Implementar Oracle Golden Gate em uma VM Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="bb0da-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="bb0da-104">Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="bb0da-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="bb0da-105">Esses detalhes de guia como toouse Olá CLI do Azure toodeploy um Oracle 12c banco de dados de imagem da Galeria hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bb0da-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="bb0da-106">Este documento mostra passo a passo como toocreate, instalar e configurar o Oracle Golden Gate em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb0da-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="bb0da-107">Antes de começar, certifique-se que Olá que CLI do Azure foi instalado.</span><span class="sxs-lookup"><span data-stu-id="bb0da-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="bb0da-108">Para obter mais informações, consulte o [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb0da-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="bb0da-109">Preparar o ambiente de saudação</span><span class="sxs-lookup"><span data-stu-id="bb0da-109">Prepare hello environment</span></span>

<span data-ttu-id="bb0da-110">instalação de Oracle Golden Gate do tooperform Olá, você precisa toocreate duas VMs do Azure Olá mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="bb0da-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="bb0da-111">imagem do Marketplace Olá usar toocreate Olá VMs é **Oracle: Oracle-banco de dados-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="bb0da-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="bb0da-112">Você também precisa toobe familiarizado com Unix editor vi e ter um entendimento básico de x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="bb0da-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="bb0da-113">a seguir Olá é um resumo da configuração do ambiente de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb0da-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="bb0da-114">**Site primário**</span><span class="sxs-lookup"><span data-stu-id="bb0da-114">**Primary site**</span></span> | <span data-ttu-id="bb0da-115">**Replicar site**</span><span class="sxs-lookup"><span data-stu-id="bb0da-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="bb0da-116">**Versão do Oracle**</span><span class="sxs-lookup"><span data-stu-id="bb0da-116">**Oracle release**</span></span> |<span data-ttu-id="bb0da-117">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="bb0da-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="bb0da-118">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="bb0da-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="bb0da-119">**Nome da máquina**</span><span class="sxs-lookup"><span data-stu-id="bb0da-119">**Machine name**</span></span> |<span data-ttu-id="bb0da-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="bb0da-120">myVM1</span></span> |<span data-ttu-id="bb0da-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="bb0da-121">myVM2</span></span> |
> | <span data-ttu-id="bb0da-122">**Sistema operacional**</span><span class="sxs-lookup"><span data-stu-id="bb0da-122">**Operating system**</span></span> |<span data-ttu-id="bb0da-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="bb0da-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="bb0da-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="bb0da-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="bb0da-125">**SID do Oracle**</span><span class="sxs-lookup"><span data-stu-id="bb0da-125">**Oracle SID**</span></span> |<span data-ttu-id="bb0da-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="bb0da-126">CDB1</span></span> |<span data-ttu-id="bb0da-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="bb0da-127">CDB1</span></span> |
> | <span data-ttu-id="bb0da-128">**Esquema de replicação**</span><span class="sxs-lookup"><span data-stu-id="bb0da-128">**Replication schema**</span></span> |<span data-ttu-id="bb0da-129">TEST</span><span class="sxs-lookup"><span data-stu-id="bb0da-129">TEST</span></span>|<span data-ttu-id="bb0da-130">TEST</span><span class="sxs-lookup"><span data-stu-id="bb0da-130">TEST</span></span> |
> | <span data-ttu-id="bb0da-131">**Golden Gate proprietário/replicar**</span><span class="sxs-lookup"><span data-stu-id="bb0da-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="bb0da-132">C ##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="bb0da-132">C##GGADMIN</span></span> |<span data-ttu-id="bb0da-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="bb0da-133">REPUSER</span></span> |
> | <span data-ttu-id="bb0da-134">**Processo de Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="bb0da-134">**Golden Gate process**</span></span> |<span data-ttu-id="bb0da-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="bb0da-135">EXTORA</span></span> |<span data-ttu-id="bb0da-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="bb0da-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="bb0da-137">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="bb0da-137">Sign in tooAzure</span></span> 

<span data-ttu-id="bb0da-138">Entrar tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) comando.</span><span class="sxs-lookup"><span data-stu-id="bb0da-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="bb0da-139">Em seguida, siga Olá na tela instruções.</span><span class="sxs-lookup"><span data-stu-id="bb0da-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="bb0da-140">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="bb0da-140">Create a resource group</span></span>

<span data-ttu-id="bb0da-141">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bb0da-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bb0da-142">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e a partir do qual podem ser gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bb0da-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="bb0da-143">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westus` local.</span><span class="sxs-lookup"><span data-stu-id="bb0da-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="bb0da-144">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="bb0da-144">Create an availability set</span></span>

<span data-ttu-id="bb0da-145">Olá após a etapa é opcional, mas recomendado.</span><span class="sxs-lookup"><span data-stu-id="bb0da-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="bb0da-146">Para obter mais informações, confira [Guia de conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="bb0da-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="bb0da-147">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bb0da-147">Create a virtual machine</span></span>

<span data-ttu-id="bb0da-148">Criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bb0da-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="bb0da-149">Olá, exemplo a seguir cria duas VMs denominadas `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="bb0da-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="bb0da-150">Crie chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="bb0da-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="bb0da-151">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="bb0da-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="bb0da-152">Criar myVM1 (primário):</span><span class="sxs-lookup"><span data-stu-id="bb0da-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="bb0da-153">Depois de Olá que VM foi criada, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="bb0da-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="bb0da-154">(Observe Olá `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="bb0da-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="bb0da-155">Esse endereço é usado tooaccess Olá VM).</span><span class="sxs-lookup"><span data-stu-id="bb0da-155">This address is used tooaccess hello VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="bb0da-156">Criar myVM2 (replicação):</span><span class="sxs-lookup"><span data-stu-id="bb0da-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="bb0da-157">Anote Olá `publicIpAddress` também após ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="bb0da-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="bb0da-158">Abra a porta TCP para conectividade Olá</span><span class="sxs-lookup"><span data-stu-id="bb0da-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="bb0da-159">Olá próxima etapa é tooconfigure pontos de extremidade externos, que permitem o banco de dados do Oracle tooaccess Olá remotamente.</span><span class="sxs-lookup"><span data-stu-id="bb0da-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="bb0da-160">tooconfigure Olá pontos de extremidade externos, execute Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="bb0da-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="bb0da-161">Abra a porta Olá para myVM1:</span><span class="sxs-lookup"><span data-stu-id="bb0da-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="bb0da-162">Olá resultados são semelhante toohello resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb0da-162">hello results should look similar toohello following response:</span></span>

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

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="bb0da-163">Abra a porta Olá para myVM2:</span><span class="sxs-lookup"><span data-stu-id="bb0da-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="bb0da-164">Conecte-se a máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="bb0da-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="bb0da-165">A seguir Olá Use o comando toocreate uma sessão SSH com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb0da-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="bb0da-166">Substitua o endereço IP de saudação com hello `publicIpAddress` de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb0da-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="bb0da-167">Criar banco de dados de saudação myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="bb0da-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="bb0da-168">Olá software Oracle já está instalado na imagem do Marketplace hello, portanto Olá próxima etapa é o banco de dados do tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="bb0da-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="bb0da-169">Execute software hello como superusuário de 'oracle' hello:</span><span class="sxs-lookup"><span data-stu-id="bb0da-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="bb0da-170">Crie banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb0da-170">Create hello database:</span></span>

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
<span data-ttu-id="bb0da-171">Saídas devem parecer semelhante toohello resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb0da-171">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="bb0da-172">Definir variáveis ORACLE_SID e ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="bb0da-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="bb0da-173">Opcionalmente, você pode adicionar ORACLE_HOME e ORACLE_SID toohello. bashrc arquivo, para que essas configurações são salvas para futuras entradas:</span><span class="sxs-lookup"><span data-stu-id="bb0da-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="bb0da-174">Iniciar o Oracle listener</span><span class="sxs-lookup"><span data-stu-id="bb0da-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="bb0da-175">Criar banco de dados de saudação myVM2 (replicação)</span><span class="sxs-lookup"><span data-stu-id="bb0da-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="bb0da-176">Crie banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb0da-176">Create hello database:</span></span>

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
<span data-ttu-id="bb0da-177">Definir variáveis ORACLE_SID e ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="bb0da-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="bb0da-178">Opcionalmente, você pode ORACLE_HOME e ORACLE_SID toohello. bashrc arquivo adicionado, para que essas configurações são salvas para futuras entradas.</span><span class="sxs-lookup"><span data-stu-id="bb0da-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="bb0da-179">Iniciar o Oracle listener</span><span class="sxs-lookup"><span data-stu-id="bb0da-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="bb0da-180">Configurar o Golden Gate</span><span class="sxs-lookup"><span data-stu-id="bb0da-180">Configure Golden Gate</span></span> 
<span data-ttu-id="bb0da-181">tooconfigure Golden Gate etapas Olá nesta seção.</span><span class="sxs-lookup"><span data-stu-id="bb0da-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="bb0da-182">Habilitar o modo de log de arquivo morto em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="bb0da-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="bb0da-183">Habilite o registro em log forçado e verifique se há pelo menos um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="bb0da-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="bb0da-184">Baixar o software de Golden Gate</span><span class="sxs-lookup"><span data-stu-id="bb0da-184">Download Golden Gate software</span></span>
<span data-ttu-id="bb0da-185">toodownload e preparar o software Oracle Golden Gate hello, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb0da-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="bb0da-186">Baixar Olá **fbo_ggs_Linux_x64_shiphome.zip** arquivo hello [página de download do Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="bb0da-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="bb0da-187">Em Olá baixar título **12.x.x.x do Oracle GoldenGate para Oracle Linux x86-64**, deve haver um conjunto de toodownload de arquivos. zip.</span><span class="sxs-lookup"><span data-stu-id="bb0da-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="bb0da-188">Depois de baixar o computador cliente do hello. zip arquivos tooyour, use o protocolo de cópia seguro (SCP) toocopy Olá arquivos tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="bb0da-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="bb0da-189">Mover hello. zip arquivos toohello **/opt** pasta.</span><span class="sxs-lookup"><span data-stu-id="bb0da-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="bb0da-190">Em seguida, altere o proprietário de saudação dos arquivos de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bb0da-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="bb0da-191">Descompacte arquivos hello (Olá instalação Linux Descompacte utilitário se ele ainda não estiver instalado):</span><span class="sxs-lookup"><span data-stu-id="bb0da-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="bb0da-192">Alterar permissão:</span><span class="sxs-lookup"><span data-stu-id="bb0da-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="bb0da-193">Preparar o cliente hello e VM toorun x11 (para clientes do Windows somente)</span><span class="sxs-lookup"><span data-stu-id="bb0da-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="bb0da-194">Esta é uma etapa opcional.</span><span class="sxs-lookup"><span data-stu-id="bb0da-194">This is an optional step.</span></span> <span data-ttu-id="bb0da-195">Essa é uma etapa opcional, você pode ignorá-la se estiver usando um cliente do Linux ou já tiver a instalação do x11.</span><span class="sxs-lookup"><span data-stu-id="bb0da-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="bb0da-196">Baixe o PuTTY e Xming tooyour computador com Windows:</span><span class="sxs-lookup"><span data-stu-id="bb0da-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="bb0da-197">Baixar PuTTY</span><span class="sxs-lookup"><span data-stu-id="bb0da-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="bb0da-198">Baixar Xming</span><span class="sxs-lookup"><span data-stu-id="bb0da-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="bb0da-199">Depois de instalar o PuTTY, em Olá PuTTY pasta (por exemplo, C:\Program Files\PuTTY), execute puttygen.exe (gerador de chave PuTTY).</span><span class="sxs-lookup"><span data-stu-id="bb0da-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="bb0da-200">No Gerador de Chave PuTTY:</span><span class="sxs-lookup"><span data-stu-id="bb0da-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="bb0da-201">toogenerate uma saudação de chave, selecione **gerar** botão.</span><span class="sxs-lookup"><span data-stu-id="bb0da-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="bb0da-202">Copiar conteúdo de saudação da chave de saudação (**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="bb0da-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="bb0da-203">Selecione Olá **salva a chave privada** botão.</span><span class="sxs-lookup"><span data-stu-id="bb0da-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="bb0da-204">Ignorar aviso de saudação que aparece e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="bb0da-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Captura de tela da página de gerador de chave PuTTY Olá](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="bb0da-206">Em sua VM, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="bb0da-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="bb0da-207">Crie um arquivo chamado **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="bb0da-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="bb0da-208">Cole o conteúdo de saudação da chave Olá neste arquivo e, em seguida, salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="bb0da-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bb0da-209">chave de saudação deve conter a cadeia de caracteres de saudação `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="bb0da-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="bb0da-210">Além disso, o conteúdo de saudação da chave Olá deve ser uma única linha de texto.</span><span class="sxs-lookup"><span data-stu-id="bb0da-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="bb0da-211">Inicie o PuTTY.</span><span class="sxs-lookup"><span data-stu-id="bb0da-211">Start PuTTY.</span></span> <span data-ttu-id="bb0da-212">Em Olá **categoria** painel, selecione **Conexão** > **SSH** > **Auth**. Em Olá **arquivo de chave privada para autenticação** caixa, procure toohello chave gerada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bb0da-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Captura de tela da página de definir a chave privada de saudação](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="bb0da-214">Em Olá **categoria** painel, selecione **Conexão** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="bb0da-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="bb0da-215">Em seguida, selecione Olá **ativar X11 encaminhamento** caixa.</span><span class="sxs-lookup"><span data-stu-id="bb0da-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Captura de tela da página de habilitar X11 Olá](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="bb0da-217">Em Olá **categoria** painel, ir muito**sessão**.</span><span class="sxs-lookup"><span data-stu-id="bb0da-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="bb0da-218">Insira as informações de host hello e, em seguida, selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="bb0da-218">Enter hello host information, and then select **Open**.</span></span>

  ![Captura de tela da página de sessão Olá](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="bb0da-220">Instalar o software de Golden Gate</span><span class="sxs-lookup"><span data-stu-id="bb0da-220">Install Golden Gate software</span></span>

<span data-ttu-id="bb0da-221">tooinstall Oracle Golden Gate, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb0da-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="bb0da-222">Entre como oracle.</span><span class="sxs-lookup"><span data-stu-id="bb0da-222">Sign in as oracle.</span></span> <span data-ttu-id="bb0da-223">(Você deve ser capaz de toosign em sem inserir uma senha.) Certifique-se de que Xming está em execução antes de começar a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb0da-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="bb0da-224">Selecione 'Oracle GoldenGate para o banco de dados Oracle 12c'.</span><span class="sxs-lookup"><span data-stu-id="bb0da-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="bb0da-225">Em seguida, selecione **próximo** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="bb0da-225">Then select **Next** toocontinue.</span></span>

  ![Captura de tela da página de selecione instalação do instalador Olá](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="bb0da-227">Alterar o local de saudação do software.</span><span class="sxs-lookup"><span data-stu-id="bb0da-227">Change hello software location.</span></span> <span data-ttu-id="bb0da-228">Em seguida, selecione Olá **iniciar Gerenciador** caixa e insira o local do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb0da-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="bb0da-229">Selecione **próximo** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="bb0da-229">Select **Next** toocontinue.</span></span>

  ![Captura de tela da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="bb0da-231">Altere o diretório de inventário hello e, em seguida, selecione **próximo** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="bb0da-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Captura de tela da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="bb0da-233">Em Olá **resumo** tela, selecione **instalar** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="bb0da-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Captura de tela da página de selecione instalação do instalador Olá](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="bb0da-235">Você pode ser solicitado toorun um script como 'root'.</span><span class="sxs-lookup"><span data-stu-id="bb0da-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="bb0da-236">Nesse caso, abra uma sessão separada, ssh toohello VM, sudo tooroot e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="bb0da-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="bb0da-237">Selecione **OK** para continuar.</span><span class="sxs-lookup"><span data-stu-id="bb0da-237">Select **OK** continue.</span></span>

  ![Captura de tela da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="bb0da-239">Quando a instalação Olá terminar, selecione **fechar** toocomplete processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb0da-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Captura de tela da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="bb0da-241">Configuração de serviço no myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="bb0da-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="bb0da-242">Criar ou atualizar o arquivo tnsnames.ora de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb0da-242">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="bb0da-243">Crie hello Golden Gate contas de usuário e de proprietário.</span><span class="sxs-lookup"><span data-stu-id="bb0da-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bb0da-244">conta de proprietário de Olá deve ter o prefixo de C# #.</span><span class="sxs-lookup"><span data-stu-id="bb0da-244">hello owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="bb0da-245">Crie conta de usuário de teste de Golden Gate hello:</span><span class="sxs-lookup"><span data-stu-id="bb0da-245">Create hello Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="bb0da-246">Configure o arquivo de parâmetro de extração de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb0da-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="bb0da-247">Inicie a interface de linha de comando de portão dourada hello (ggsci):</span><span class="sxs-lookup"><span data-stu-id="bb0da-247">Start hello Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="bb0da-248">Adicione Olá toohello EXTRAIA o arquivo de parâmetro a seguir (por meio de comandos vi).</span><span class="sxs-lookup"><span data-stu-id="bb0da-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="bb0da-249">Pressione a tecla Esc, ': wq!'</span><span class="sxs-lookup"><span data-stu-id="bb0da-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="bb0da-250">arquivo toosave.</span><span class="sxs-lookup"><span data-stu-id="bb0da-250">toosave file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="bb0da-251">Registrar extrair – extrair integrado:</span><span class="sxs-lookup"><span data-stu-id="bb0da-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="bb0da-252">Configurar pontos de verificação de extração e iniciar a extração em tempo real:</span><span class="sxs-lookup"><span data-stu-id="bb0da-252">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="bb0da-253">Nesta etapa, você deve encontrar hello iniciando SCN, que será usado mais tarde, em uma seção diferente:</span><span class="sxs-lookup"><span data-stu-id="bb0da-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="bb0da-254">Configuração de serviço no myVM2 (replicação)</span><span class="sxs-lookup"><span data-stu-id="bb0da-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="bb0da-255">Criar ou atualizar o arquivo tnsnames.ora de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb0da-255">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="bb0da-256">Crie uma conta de replicação:</span><span class="sxs-lookup"><span data-stu-id="bb0da-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="bb0da-257">Crie uma conta de usuário de teste Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="bb0da-257">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="bb0da-258">Alterações de tooreplicate de arquivo de parâmetro de réplicas:</span><span class="sxs-lookup"><span data-stu-id="bb0da-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="bb0da-259">Conteúdo do arquivo de parâmetro REPORA:</span><span class="sxs-lookup"><span data-stu-id="bb0da-259">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="bb0da-260">Configure um ponto de verificação de réplicas:</span><span class="sxs-lookup"><span data-stu-id="bb0da-260">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="bb0da-261">Configurar a replicação de saudação (myVM1 e myVM2)</span><span class="sxs-lookup"><span data-stu-id="bb0da-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="bb0da-262">1. Configurar a replicação de saudação em myVM2 (replicação)</span><span class="sxs-lookup"><span data-stu-id="bb0da-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="bb0da-263">Atualize o arquivo de saudação com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="bb0da-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="bb0da-264">Reinicie o serviço de Gerenciador de saudação:</span><span class="sxs-lookup"><span data-stu-id="bb0da-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="bb0da-265">2. Configurar a replicação de saudação em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="bb0da-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="bb0da-266">Inicie o carregamento inicial hello e verifique se há erros:</span><span class="sxs-lookup"><span data-stu-id="bb0da-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="bb0da-267">3. Configurar a replicação de saudação em myVM2 (replicação)</span><span class="sxs-lookup"><span data-stu-id="bb0da-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="bb0da-268">Alterar Olá número SCN com número de saudação obtido antes de:</span><span class="sxs-lookup"><span data-stu-id="bb0da-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="bb0da-269">replicação de saudação foi iniciado e você pode testá-lo pela inserção de novas tabelas tooTEST de registros.</span><span class="sxs-lookup"><span data-stu-id="bb0da-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="bb0da-270">Exibir o status do trabalho e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="bb0da-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="bb0da-271">Exibir relatórios</span><span class="sxs-lookup"><span data-stu-id="bb0da-271">View reports</span></span>
<span data-ttu-id="bb0da-272">tooview relata myVM1, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb0da-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="bb0da-273">tooview relata myVM2, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb0da-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="bb0da-274">Exibir o status e histórico</span><span class="sxs-lookup"><span data-stu-id="bb0da-274">View status and history</span></span>
<span data-ttu-id="bb0da-275">tooview status e o histórico no myVM1, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb0da-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="bb0da-276">tooview status e o histórico no myVM2, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb0da-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="bb0da-277">Isso conclui a saudação instalação e configuração de porta de Golden em Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="bb0da-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="bb0da-278">Excluir a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="bb0da-278">Delete hello virtual machine</span></span>

<span data-ttu-id="bb0da-279">Quando ele não for mais necessário, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, VM e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="bb0da-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="bb0da-280">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb0da-280">Next steps</span></span>

[<span data-ttu-id="bb0da-281">Tutorial Criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="bb0da-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="bb0da-282">Explorar as amostras de CLI de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="bb0da-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
