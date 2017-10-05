---
title: Implementar Oracle Golden Gate em uma VM Linux do Azure | Microsoft Docs
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
ms.openlocfilehash: a05711357d345267647c02e42336fd37c09e1bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="6c3ef-103">Implementar Oracle Golden Gate em uma VM Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="6c3ef-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="6c3ef-104">A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="6c3ef-105">Esse guia detalha como usar a CLI do Azure para implantar um banco de dados Oracle 12c por meio da imagem na galeria do Marketplace do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-105">This guide details how to use the Azure CLI to deploy an Oracle 12c database from the Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="6c3ef-106">Este documento mostra passo a passo sobre como criar, instalar e configurar o Oracle Golden Gate em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-106">This document shows you step-by-step how to create, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="6c3ef-107">Antes de começar, certifique-se de que a CLI do Azure foi instalada.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="6c3ef-108">Para obter mais informações, consulte o [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="6c3ef-109">Preparar o ambiente</span><span class="sxs-lookup"><span data-stu-id="6c3ef-109">Prepare the environment</span></span>

<span data-ttu-id="6c3ef-110">Para executar a instalação do Oracle Golden Gate, você precisa criar duas VMs do Azure no mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-110">To perform the Oracle Golden Gate installation, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="6c3ef-111">A imagem do Marketplace usada para criar as VMs é **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-111">The Marketplace image you use to create the VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="6c3ef-112">Você também precisa estar familiarizado com Unix editor vi e ter um entendimento básico de x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-112">You also need to be familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="6c3ef-113">Este é um resumo da configuração do ambiente:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-113">The following is a summary of the environment configuration:</span></span>
> 
> |  | <span data-ttu-id="6c3ef-114">**Site primário**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-114">**Primary site**</span></span> | <span data-ttu-id="6c3ef-115">**Replicar site**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="6c3ef-116">**Versão do Oracle**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-116">**Oracle release**</span></span> |<span data-ttu-id="6c3ef-117">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="6c3ef-118">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="6c3ef-119">**Nome da máquina**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-119">**Machine name**</span></span> |<span data-ttu-id="6c3ef-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="6c3ef-120">myVM1</span></span> |<span data-ttu-id="6c3ef-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="6c3ef-121">myVM2</span></span> |
> | <span data-ttu-id="6c3ef-122">**Sistema operacional**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-122">**Operating system**</span></span> |<span data-ttu-id="6c3ef-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="6c3ef-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="6c3ef-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="6c3ef-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="6c3ef-125">**SID do Oracle**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-125">**Oracle SID**</span></span> |<span data-ttu-id="6c3ef-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="6c3ef-126">CDB1</span></span> |<span data-ttu-id="6c3ef-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="6c3ef-127">CDB1</span></span> |
> | <span data-ttu-id="6c3ef-128">**Esquema de replicação**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-128">**Replication schema**</span></span> |<span data-ttu-id="6c3ef-129">TEST</span><span class="sxs-lookup"><span data-stu-id="6c3ef-129">TEST</span></span>|<span data-ttu-id="6c3ef-130">TEST</span><span class="sxs-lookup"><span data-stu-id="6c3ef-130">TEST</span></span> |
> | <span data-ttu-id="6c3ef-131">**Golden Gate proprietário/replicar**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="6c3ef-132">C ##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="6c3ef-132">C##GGADMIN</span></span> |<span data-ttu-id="6c3ef-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="6c3ef-133">REPUSER</span></span> |
> | <span data-ttu-id="6c3ef-134">**Processo de Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="6c3ef-134">**Golden Gate process**</span></span> |<span data-ttu-id="6c3ef-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="6c3ef-135">EXTORA</span></span> |<span data-ttu-id="6c3ef-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="6c3ef-136">REPORA</span></span>|


### <a name="sign-in-to-azure"></a><span data-ttu-id="6c3ef-137">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="6c3ef-137">Sign in to Azure</span></span> 

<span data-ttu-id="6c3ef-138">Entre na sua assinatura do Azure como comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-138">Sign in to your Azure subscription with the [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="6c3ef-139">Em seguida, execute as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-139">Then follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="6c3ef-140">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6c3ef-140">Create a resource group</span></span>

<span data-ttu-id="6c3ef-141">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-141">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6c3ef-142">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e a partir do qual podem ser gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="6c3ef-143">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `westus`.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-143">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="6c3ef-144">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="6c3ef-144">Create an availability set</span></span>

<span data-ttu-id="6c3ef-145">Esta etapa é opcional, mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-145">The following step is optional but recommended.</span></span> <span data-ttu-id="6c3ef-146">Para obter mais informações, confira [Guia de conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="6c3ef-147">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6c3ef-147">Create a virtual machine</span></span>

<span data-ttu-id="6c3ef-148">Crie uma VM com o comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-148">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="6c3ef-149">O exemplo a seguir cria duas VMs, chamadas `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-149">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="6c3ef-150">Crie chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="6c3ef-151">Para usar um conjunto específico de chaves, use a opção `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-151">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="6c3ef-152">Criar myVM1 (primário):</span><span class="sxs-lookup"><span data-stu-id="6c3ef-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="6c3ef-153">Quando a VM tiver sido criada, a CLI do Azure mostra informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-153">After the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="6c3ef-154">(Anote `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-154">(Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="6c3ef-155">Esse endereço é usado para acessar a VM.)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-155">This address is used to access the VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="6c3ef-156">Criar myVM2 (replicação):</span><span class="sxs-lookup"><span data-stu-id="6c3ef-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="6c3ef-157">Anote o `publicIpAddress` também após ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-157">Take note of the `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="6c3ef-158">Abrir a porta TCP para conectividade</span><span class="sxs-lookup"><span data-stu-id="6c3ef-158">Open the TCP port for connectivity</span></span>

<span data-ttu-id="6c3ef-159">A próxima etapa é configurar pontos de extremidade externos, que permitem acessar remotamente o banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-159">The next step is to configure external endpoints,  which enable you to access the Oracle database remotely.</span></span> <span data-ttu-id="6c3ef-160">Para configurar os pontos de extremidade externos, execute os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-160">To configure the external endpoints, run the following commands.</span></span>

#### <a name="open-the-port-for-myvm1"></a><span data-ttu-id="6c3ef-161">Abrir porta para myVM1:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-161">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="6c3ef-162">O resultado deve ser semelhante à seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-162">The results should look similar to the following response:</span></span>

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

#### <a name="open-the-port-for-myvm2"></a><span data-ttu-id="6c3ef-163">Abra a porta para myVM2:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-163">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="6c3ef-164">Conectar-se à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6c3ef-164">Connect to the virtual machine</span></span>

<span data-ttu-id="6c3ef-165">Use o seguinte comando para criar uma sessão SSH com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-165">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="6c3ef-166">Substitua o endereço IP pelo `publicIpAddress` de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-166">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="6c3ef-167">Crie banco de dados myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-167">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="6c3ef-168">O software Oracle já está instalado na imagem do Marketplace, portanto, a próxima etapa é instalar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-168">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="6c3ef-169">Execute o software como o superusuário 'oracle':</span><span class="sxs-lookup"><span data-stu-id="6c3ef-169">Run the software as the 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="6c3ef-170">Crie o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-170">Create the database:</span></span>

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
<span data-ttu-id="6c3ef-171">A saída deve ser semelhante à seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-171">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="6c3ef-172">Defina as variáveis ORACLE_SID e ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-172">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="6c3ef-173">Opcionalmente, você pode adicionar ORACLE_HOME e ORACLE_SID ao arquivo .bashrc, de maneira que essas configurações sejam salvas para logons futuros:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-173">Optionally, you can add ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="6c3ef-174">Iniciar o Oracle listener</span><span class="sxs-lookup"><span data-stu-id="6c3ef-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-the-database-on-myvm2-replicate"></a><span data-ttu-id="6c3ef-175">Crie banco de dados myVM2 (replicação)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-175">Create the database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="6c3ef-176">Crie o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-176">Create the database:</span></span>

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
<span data-ttu-id="6c3ef-177">Defina as variáveis ORACLE_SID e ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-177">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="6c3ef-178">Opcionalmente, você pode adicionar ORACLE_HOME e ORACLE_SID ao arquivo .bashrc, de maneira que essas configurações sejam salvas para logons futuros.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-178">Optionally, you can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="6c3ef-179">Iniciar o Oracle listener</span><span class="sxs-lookup"><span data-stu-id="6c3ef-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="6c3ef-180">Configurar o Golden Gate</span><span class="sxs-lookup"><span data-stu-id="6c3ef-180">Configure Golden Gate</span></span> 
<span data-ttu-id="6c3ef-181">Para configurar Golden Gate, execute as etapas nesta seção.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-181">To configure Golden Gate, take the steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="6c3ef-182">Habilitar o modo de log de arquivo morto em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="6c3ef-183">Habilite o registro em log forçado e verifique se há pelo menos um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="6c3ef-184">Baixar o software de Golden Gate</span><span class="sxs-lookup"><span data-stu-id="6c3ef-184">Download Golden Gate software</span></span>
<span data-ttu-id="6c3ef-185">Para baixar e preparar o software de Oracle Golden Gate, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-185">To download and prepare the Oracle Golden Gate software, complete the following steps:</span></span>

1. <span data-ttu-id="6c3ef-186">Baixe o arquivo **fbo_ggs_Linux_x64_shiphome.zip** da [página de download do Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-186">Download the **fbo_ggs_Linux_x64_shiphome.zip** file from the [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="6c3ef-187">Sob o título do download **12.x.x.x do Oracle GoldenGate para Oracle Linux x86-64**, deve haver um conjunto de arquivos. zip para download.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-187">Under the download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files to download.</span></span>

2. <span data-ttu-id="6c3ef-188">Depois de baixar os arquivos .zip para o computador cliente, você poderá usar o protocolo SCP para copiar os arquivos na sua VM:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-188">After you download the .zip files to your client computer, use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="6c3ef-189">Mova os arquivos .zip para a pasta **/opt**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-189">Move the .zip files to the **/opt** folder.</span></span> <span data-ttu-id="6c3ef-190">Em seguida, altere o proprietário dos arquivos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-190">Then change the owner of the files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="6c3ef-191">Descompacte os arquivos (instale o utilitário unzip do Linux se ele ainda não estiver instalado):</span><span class="sxs-lookup"><span data-stu-id="6c3ef-191">Unzip the files (install the Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="6c3ef-192">Alterar permissão:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-the-client-and-vm-to-run-x11-for-windows-clients-only"></a><span data-ttu-id="6c3ef-193">Prepare o cliente e a VM para executar X11 (somente para clientes Windows)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-193">Prepare the client and VM to run x11 (for Windows clients only)</span></span>
<span data-ttu-id="6c3ef-194">Esta é uma etapa opcional.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-194">This is an optional step.</span></span> <span data-ttu-id="6c3ef-195">Essa é uma etapa opcional, você pode ignorá-la se estiver usando um cliente do Linux ou já tiver a instalação do x11.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="6c3ef-196">Baixe o PuTTY e o Xming em seu computador Windows:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-196">Download PuTTY and Xming to your Windows computer:</span></span>

  * [<span data-ttu-id="6c3ef-197">Baixar PuTTY</span><span class="sxs-lookup"><span data-stu-id="6c3ef-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="6c3ef-198">Baixar Xming</span><span class="sxs-lookup"><span data-stu-id="6c3ef-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="6c3ef-199">Depois de instalar o PuTTY, na pasta PuTTY (por exemplo, C:\Arquivos de Programa\PuTTY), execute puttygen.exe (Gerador de Chave PuTTY).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-199">After you install PuTTY, in the PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="6c3ef-200">No Gerador de Chave PuTTY:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="6c3ef-201">Para gerar uma chave, selecione o botão **Gerar**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-201">To generate a key, select the **Generate** button.</span></span>
  - <span data-ttu-id="6c3ef-202">Copie o conteúdo da chave (**Ctrl+C**).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-202">Copy the contents of the key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="6c3ef-203">Selecione o botão **Salvar chave privada**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-203">Select the **Save private key** button.</span></span>
  - <span data-ttu-id="6c3ef-204">Ignore o aviso que aparece e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-204">Ignore the warning that appears, and then select **OK**.</span></span>

    ![Captura de tela da página do gerador de chave PuTTY](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="6c3ef-206">Em sua VM, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="6c3ef-207">Crie um arquivo chamado **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="6c3ef-208">Cole o conteúdo da chave nesse arquivo e salve-o.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-208">Paste the contents of the key in this file, and then save the file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6c3ef-209">A chave deve conter a cadeia de caracteres `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-209">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="6c3ef-210">Além disso, o conteúdo da chave deve ser uma única linha de texto.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-210">Also, the contents of the key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="6c3ef-211">Inicie o PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-211">Start PuTTY.</span></span> <span data-ttu-id="6c3ef-212">No painel **Categoria**, selecione **Conexão** > **SSH** > **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-212">In the **Category** pane, select **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="6c3ef-213">Na caixa **Arquivo de chave privada para autenticação**, navegue até a chave que você gerou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-213">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

  ![Captura de tela da página Instalar chave privada](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="6c3ef-215">No painel **Categoria**, selecione **Conexão** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-215">In the **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="6c3ef-216">Em seguida, selecione a caixa **Habilitar encaminhamento X11**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-216">Then select the **Enable X11 forwarding** box.</span></span>

  ![Captura de tela da página Habilitar X11](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="6c3ef-218">No painel **Categoria**, vá para **Sessão**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-218">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="6c3ef-219">Insira as informações do host e selecione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-219">Enter the host information, and then select **Open**.</span></span>

  ![Captura de tela da página de sessão](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="6c3ef-221">Instalar o software de Golden Gate</span><span class="sxs-lookup"><span data-stu-id="6c3ef-221">Install Golden Gate software</span></span>

<span data-ttu-id="6c3ef-222">Para instalar o Oracle Golden Gate, conclua as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-222">To install Oracle Golden Gate, complete the following steps:</span></span>

1. <span data-ttu-id="6c3ef-223">Entre como oracle.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-223">Sign in as oracle.</span></span> <span data-ttu-id="6c3ef-224">(Você deve ser capaz de entrar sem inserir uma senha.) Verifique se Xming está em execução antes de iniciar a instalação.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-224">(You should be able to sign in without being prompted for a password.) Make sure that Xming is running before you begin the installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="6c3ef-225">Selecione 'Oracle GoldenGate para o banco de dados Oracle 12c'.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-225">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="6c3ef-226">Em seguida, selecione **Avançar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-226">Then select **Next** to continue.</span></span>

  ![Captura de tela da página Selecionar Instalação do instalador](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="6c3ef-228">Altere o local do software.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-228">Change the software location.</span></span> <span data-ttu-id="6c3ef-229">Em seguida, selecione a caixa **Iniciar Gerenciador** e insira o local do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-229">Then select  the **Start Manager** box and enter the database location.</span></span> <span data-ttu-id="6c3ef-230">Selecione **Avançar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-230">Select **Next** to continue.</span></span>

  ![Captura de tela da página Selecionar Instalação](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="6c3ef-232">Altere o diretório de inventário e, em seguida, selecione **Avançar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-232">Change the inventory directory, and then select **Next** to continue.</span></span>

  ![Captura de tela da página Selecionar Instalação](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="6c3ef-234">Na tela de **Resumo**, selecione **Instalar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-234">On the **Summary** screen, select **Install** to continue.</span></span>

  ![Captura de tela da página Selecionar Instalação do instalador](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="6c3ef-236">Pode ser solicitado que você execute um script como 'root'.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-236">You might be prompted to run a script as 'root'.</span></span> <span data-ttu-id="6c3ef-237">Nesse caso, abra uma sessão separada, ssh para a VM, sudo para a raiz e, em seguida, execute o script.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-237">If so, open a separate session, ssh to the VM, sudo to root, and then run the script.</span></span> <span data-ttu-id="6c3ef-238">Selecione **OK** para continuar.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-238">Select **OK** continue.</span></span>

  ![Captura de tela da página Selecionar Instalação](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="6c3ef-240">Quando a instalação for concluída, selecione **Fechar** para concluir o processo.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-240">When the installation has finished, select **Close** to complete the process.</span></span>

  ![Captura de tela da página Selecionar Instalação](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="6c3ef-242">Configuração de serviço no myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-242">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="6c3ef-243">Criar ou atualizar o arquivo tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-243">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="6c3ef-244">Crie as contas de usuário e de proprietário de Golden Gate.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-244">Create the Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6c3ef-245">A conta do proprietário deve ter o prefixo de C##.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-245">The owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA to C##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="6c3ef-246">Crie a conta de usuário de teste Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-246">Create the Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="6c3ef-247">Configure o arquivo de parâmetro de extração.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-247">Configure the extract parameter file.</span></span>

 <span data-ttu-id="6c3ef-248">Inicie a interface de linha de comando de Golden Gate (ggsci):</span><span class="sxs-lookup"><span data-stu-id="6c3ef-248">Start the Golden gate command-line interface (ggsci):</span></span>

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
5. <span data-ttu-id="6c3ef-249">Adicione o seguinte para o arquivo de parâmetro de EXTRAÇÃO (usando comandos vi).</span><span class="sxs-lookup"><span data-stu-id="6c3ef-249">Add the following to the EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="6c3ef-250">Pressione a tecla Esc, ': wq!'</span><span class="sxs-lookup"><span data-stu-id="6c3ef-250">Press Esc key, ':wq!'</span></span> <span data-ttu-id="6c3ef-251">para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-251">to save file.</span></span> 

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
6. <span data-ttu-id="6c3ef-252">Registrar extrair – extrair integrado:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-252">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="6c3ef-253">Configurar pontos de verificação de extração e iniciar a extração em tempo real:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-253">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request to MANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="6c3ef-254">Nesta etapa, você deve encontrar o SCN inicial, que será usado mais tarde, em uma seção diferente:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-254">In this step, you find the starting SCN, which will be used later, in a different section:</span></span>

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

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="6c3ef-255">Configuração de serviço no myVM2 (replicação)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-255">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="6c3ef-256">Criar ou atualizar o arquivo tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-256">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="6c3ef-257">Crie uma conta de replicação:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-257">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba to repuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="6c3ef-258">Crie uma conta de usuário de teste Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-258">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="6c3ef-259">Arquivo de parâmetro de réplicas para replicar as alterações:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-259">REPLICAT parameter file to replicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="6c3ef-260">Conteúdo do arquivo de parâmetro REPORA:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-260">Content of REPORA parameter file:</span></span>

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

5. <span data-ttu-id="6c3ef-261">Configure um ponto de verificação de réplicas:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-261">Set up a replicat checkpoint:</span></span>

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

### <a name="set-up-the-replication-myvm1-and-myvm2"></a><span data-ttu-id="6c3ef-262">Configurar a replicação (myVM1 e myVM2)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-262">Set up the replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="6c3ef-263">1. Configurar a replicação em myVM2 (replicação)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-263">1. Set up the replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="6c3ef-264">Atualize o arquivo com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-264">Update the file with the following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="6c3ef-265">Em seguida, reinicie o serviço do Gerenciador:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-265">Then restart the Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-the-replication-on-myvm1-primary"></a><span data-ttu-id="6c3ef-266">2. Configurar a replicação em myVM1 (primário)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-266">2. Set up the replication on myVM1 (primary)</span></span>

<span data-ttu-id="6c3ef-267">Inicie o carregamento inicial e verifique se há erros:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-267">Start the initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="6c3ef-268">3. Configurar a replicação em myVM2 (replicação)</span><span class="sxs-lookup"><span data-stu-id="6c3ef-268">3. Set up the replication on myVM2 (replicate)</span></span>

<span data-ttu-id="6c3ef-269">Alteração de número SCN com o número obtido antes:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-269">Change the SCN number with the number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="6c3ef-270">A replicação foi iniciada e você pode testá-la, inserindo novos registros em tabelas de TESTE.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-270">The replication has begun, and you can test it by inserting new records to TEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="6c3ef-271">Exibir o status do trabalho e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="6c3ef-271">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="6c3ef-272">Exibir relatórios</span><span class="sxs-lookup"><span data-stu-id="6c3ef-272">View reports</span></span>
<span data-ttu-id="6c3ef-273">Para exibir relatórios em myVM1, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-273">To view reports on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="6c3ef-274">Para exibir relatórios em myVM2, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-274">To view reports on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="6c3ef-275">Exibir o status e histórico</span><span class="sxs-lookup"><span data-stu-id="6c3ef-275">View status and history</span></span>
<span data-ttu-id="6c3ef-276">Para exibir o status e histórico em myVM1, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-276">To view status and history on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="6c3ef-277">Para exibir o status e histórico em myVM2, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6c3ef-277">To view status and history on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="6c3ef-278">Isso conclui a instalação e configuração do Golden Gate no Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-278">This completes the installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="6c3ef-279">Excluir a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6c3ef-279">Delete the virtual machine</span></span>

<span data-ttu-id="6c3ef-280">Quando não é mais necessário, o comando a seguir pode ser usado para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6c3ef-280">When it's no longer needed, the following command can be used to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="6c3ef-281">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c3ef-281">Next steps</span></span>

[<span data-ttu-id="6c3ef-282">Tutorial Criar máquinas virtuais altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="6c3ef-282">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="6c3ef-283">Explorar as amostras de CLI de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="6c3ef-283">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
