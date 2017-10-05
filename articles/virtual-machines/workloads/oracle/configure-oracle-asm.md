---
title: "Configurar o Oracle ASM em uma máquina virtual Linux do Azure | Microsoft Docs"
description: Coloque o Oracle ASM em funcionamento rapidamente no ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: 117212a2e7e3da7c3e249798eec804a652e0ef58
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="f3aa2-103">Configurar o Oracle ASM em uma máquina virtual Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="f3aa2-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="f3aa2-104">Máquinas virtuais do Azure fornecem um ambiente de computação totalmente configurável e flexível.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="f3aa2-105">Este tutorial aborda a implantação básica de máquina virtual do Azure combinada com a instalação e a configuração do Oracle ASM (Automated Storage Management).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-105">This tutorial covers basic Azure virtual machine deployment combined with the installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="f3aa2-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3aa2-107">Criar e conectar-se a uma VM do Oracle Database</span><span class="sxs-lookup"><span data-stu-id="f3aa2-107">Create and connect to an Oracle Database VM</span></span>
> * <span data-ttu-id="f3aa2-108">Instalar e configurar o Oracle Automated Storage Management</span><span class="sxs-lookup"><span data-stu-id="f3aa2-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="f3aa2-109">Instalar e configurar a infraestrutura Oracle Grid</span><span class="sxs-lookup"><span data-stu-id="f3aa2-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="f3aa2-110">Inicializar uma instalação do Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="f3aa2-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="f3aa2-111">Criar um Oracle DB gerenciado por ASM</span><span class="sxs-lookup"><span data-stu-id="f3aa2-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f3aa2-112">Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f3aa2-113">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="f3aa2-114">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-the-environment"></a><span data-ttu-id="f3aa2-115">Preparar o ambiente</span><span class="sxs-lookup"><span data-stu-id="f3aa2-115">Prepare the environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="f3aa2-116">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f3aa2-116">Create a resource group</span></span>

<span data-ttu-id="f3aa2-117">Para criar um grupo de recursos, use o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-117">To create a resource group, use the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f3aa2-118">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="f3aa2-119">Neste exemplo, um grupo de recursos chamado de *myResourceGroup* é criado na região *eastus*.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-119">In this example, a resource group named *myResourceGroup* in the *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="f3aa2-120">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f3aa2-120">Create a VM</span></span>

<span data-ttu-id="f3aa2-121">Para criar uma máquina virtual com base na imagem do Oracle Database e configurá-la para usar o Oracle ASM, use o comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-121">To create a virtual machine based on the Oracle Database image and configure it to use Oracle ASM, use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="f3aa2-122">O exemplo a seguir cria uma VM denominada myVM que tem um tamanho Standard_DS2_v2 com quatro discos de dados anexados, cada um com 50 GB.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-122">The following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="f3aa2-123">Se ainda não existirem em um local de chave padrão, o exemplo também criará chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-123">If they do not already exist in the default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="f3aa2-124">Para usar um conjunto específico de chaves, use a opção `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-124">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="f3aa2-125">Depois de criar a VM, a CLI do Azure exibe informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-125">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="f3aa2-126">Observe o valor de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-126">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="f3aa2-127">Você pode usar esse endereço para acessar a VM.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-127">You use this address to access the VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-to-the-vm"></a><span data-ttu-id="f3aa2-128">Conectar-se à VM</span><span class="sxs-lookup"><span data-stu-id="f3aa2-128">Connect to the VM</span></span>

<span data-ttu-id="f3aa2-129">Para criar uma sessão SSH com a VM e definir configurações adicionais, use o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-129">To create an SSH session with the VM and configure additional settings, use the following command.</span></span> <span data-ttu-id="f3aa2-130">Substitua o endereço IP pelo valor `publicIpAddress` para a sua VM.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-130">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="f3aa2-131">Instalar o Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="f3aa2-131">Install Oracle ASM</span></span>

<span data-ttu-id="f3aa2-132">Para instalar o Oracle ASM, conclua as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-132">To install Oracle ASM, complete the following steps.</span></span> 

<span data-ttu-id="f3aa2-133">Para saber mais sobre como instalar o ASM do Oracle, confira [Downloads do Oracle ASMLib para Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="f3aa2-134">Você precisa fazer logon como raiz para continuar com a instalação do ASM:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-134">You need to login as root in order to continue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="f3aa2-135">Execute esses comandos adicionais para instalar os componentes do Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-135">Run these additional commands to install Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="f3aa2-136">Verifique se o Oracle ASM está instalado:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="f3aa2-137">A saída desse comando deve listar os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-137">The output of this command should list the following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="f3aa2-138">O ASM exige funções e usuários específicos para funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-138">ASM requires specific users and roles in order to function correctly.</span></span> <span data-ttu-id="f3aa2-139">Os seguintes comandos criam os grupos e as contas de usuário de pré-requisito:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-139">The following commands create the pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="f3aa2-140">Verifique se os usuários e grupos foram criados corretamente:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="f3aa2-141">A saída desse comando deve listar os seguintes usuários e grupos:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-141">The output of this command should list the following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="f3aa2-142">Crie uma pasta para a *grade* de usuários e altere o proprietário:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-142">Create a folder for user *grid* and change the owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="f3aa2-143">Configurar o Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="f3aa2-143">Set up Oracle ASM</span></span>

<span data-ttu-id="f3aa2-144">Para este tutorial, o usuário padrão é *grade* e o grupo padrão é *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-144">For this tutorial, the default user is *grid* and the default group is *asmadmin*.</span></span> <span data-ttu-id="f3aa2-145">Verifique se o usuário *oracle* faz parte do grupo asmadmin.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-145">Ensure that the *oracle* user is part of the asmadmin group.</span></span> <span data-ttu-id="f3aa2-146">Para configurar a instalação do Oracle ASM, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-146">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="f3aa2-147">A configuração do driver de biblioteca do Oracle ASM envolve a definição do usuário padrão (grade) e do grupo padrão (asmadmin), bem como a configuração da unidade para iniciar na inicialização (escolher y) e verificar se há discos na inicialização (escolher y).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-147">Setting up the Oracle ASM library driver involves defining the default user (grid) and default group (asmadmin) as well as configuring the drive to start on boot (choose y) and to scan for disks on boot (choose y).</span></span> <span data-ttu-id="f3aa2-148">Você precisa para responder aos prompts do seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-148">You need to answer the prompts from the following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="f3aa2-149">A saída desse comando deve ser semelhante ao seguinte, parando com os prompts a serem respondidos.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-149">The output of this command should look similar to the following, stopping with prompts to be answered.</span></span>

    ```bash
   Configuring the Oracle ASM library driver.

   This will configure the on-boot properties of the Oracle ASM library
   driver. The following questions will determine whether the driver is
   loaded on boot and what permissions it will have. The current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user to own the driver interface []: grid
   Default group to own the driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="f3aa2-150">Veja a configuração de disco:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-150">View the disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="f3aa2-151">A saída desse comando deve ser semelhante à seguinte listagem de discos disponíveis</span><span class="sxs-lookup"><span data-stu-id="f3aa2-151">The output of this command should look similar to the following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="f3aa2-152">Formate o disco */dev/sdc* executando o seguinte comando e respondendo aos prompts com:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-152">Format disk */dev/sdc* by running the following command and answering the prompts with:</span></span>
   - <span data-ttu-id="f3aa2-153">*n* para a nova partição</span><span class="sxs-lookup"><span data-stu-id="f3aa2-153">*n* for new partition</span></span>
   - <span data-ttu-id="f3aa2-154">*p* para a partição primária</span><span class="sxs-lookup"><span data-stu-id="f3aa2-154">*p* for primary partition</span></span>
   - <span data-ttu-id="f3aa2-155">*1* para selecionar a primeira partição</span><span class="sxs-lookup"><span data-stu-id="f3aa2-155">*1* to select the first partition</span></span>
   - <span data-ttu-id="f3aa2-156">pressione `enter` para o primeiro cilindro padrão</span><span class="sxs-lookup"><span data-stu-id="f3aa2-156">press `enter` for the default first cylinder</span></span>
   - <span data-ttu-id="f3aa2-157">pressione `enter` para o último cilindro padrão</span><span class="sxs-lookup"><span data-stu-id="f3aa2-157">press `enter` for the default last cylinder</span></span>
   - <span data-ttu-id="f3aa2-158">pressione *w* para gravar as alterações na tabela de partição</span><span class="sxs-lookup"><span data-stu-id="f3aa2-158">press *w* to write the changes to the partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="f3aa2-159">Usando as respostas fornecidas acima, a saída para o comando fdisk deve ficar semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-159">Using the answers provided above, the output for the fdisk command should look like the following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide to write them.
   After that, of course, the previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   The device presents a logical sector size that is smaller than
   the physical sector size. Aligning to a physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off the mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   The partition table has been altered!

   Calling ioctl() to re-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="f3aa2-160">Repita o comando fdisk anterior para `/dev/sdd`, `/dev/sde` e `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-160">Repeat the preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="f3aa2-161">Verifique a configuração de disco:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-161">Check the disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="f3aa2-162">A saída do comando deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-162">The output of the command should look like the following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="f3aa2-163">Verifique o status do serviço Oracle ASM e inicie o serviço Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-163">Check the Oracle ASM service status and start the Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="f3aa2-164">A saída do comando deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-164">The output of the command should look like the following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing the Oracle ASMLib driver:                     [  OK  ]
   Scanning the system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="f3aa2-165">Crie discos do Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="f3aa2-166">A saída do comando deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-166">The output of the command should look like the following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="f3aa2-167">Liste os discos do Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="f3aa2-168">A saída do comando deve listar os seguintes discos do Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-168">The output of the command should list off the following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="f3aa2-169">Altere as senhas para os usuários de raiz, da oracle e de grade.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-169">Change the passwords for the root, oracle, and grid users.</span></span> <span data-ttu-id="f3aa2-170">**Anote essas novas senhas** pois elas serão usadas posteriormente, durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-170">**Make note of these new passwords** as you are using them later during the installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="f3aa2-171">Altere a permissão de pasta:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-171">Change the folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="f3aa2-172">Baixe e prepare a infraestrutura em grade do Oracle</span><span class="sxs-lookup"><span data-stu-id="f3aa2-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="f3aa2-173">Para baixar e preparar o software de infraestrutura em grade do Oracle, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-173">To download and prepare the Oracle Grid Infrastructure software, complete the following steps:</span></span>

1. <span data-ttu-id="f3aa2-174">Baixe a infraestrutura em grade do Oracle da [página de download do Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-174">Download Oracle Grid Infrastructure from the [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="f3aa2-175">No download intitulado **Banco de Dados Oracle 12c versão 1 Infraestrutura em Grade (12.1.0.2.0) para Linux x86-64**, baixe os dois arquivos .zip.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-175">Under the download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download the two .zip files.</span></span>

2. <span data-ttu-id="f3aa2-176">Depois de baixar os arquivos .zip para o computador cliente, você poderá usar o protocolo SCP para copiar os arquivos na VM:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-176">After you download the .zip files to your client computer, you can use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="f3aa2-177">SSH de volta para a Oracle VM no Azure a fim de mover os arquivos .zip para a pasta /opt.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-177">SSH back into your Oracle VM in Azure in order to move the .zip files into the /opt folder.</span></span> <span data-ttu-id="f3aa2-178">Em seguida, altere o proprietário dos arquivos:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-178">Then, change the owner of the files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="f3aa2-179">Descompacte os arquivos.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-179">Unzip the files.</span></span> <span data-ttu-id="f3aa2-180">(Instale a ferramenta de descompactação do Linux se ela ainda não estiver instalada.)</span><span class="sxs-lookup"><span data-stu-id="f3aa2-180">(Install the Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="f3aa2-181">Alterar permissão:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="f3aa2-182">Atualize o espaço de troca configurado.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-182">Update configured swap space.</span></span> <span data-ttu-id="f3aa2-183">Os componentes do Oracle Grid precisam de, pelo menos, 6,8 GB de espaço de troca para instalar o Grid.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-183">Oracle Grid components need at least 6.8 GB of swap space to install Grid.</span></span> <span data-ttu-id="f3aa2-184">O tamanho do arquivo de permuta padrão para as imagens da Oracle Linux no Azure é de apenas 2.048 MB.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-184">The default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="f3aa2-185">Você precisa aumentar o `ResourceDisk.SwapSizeMB` no arquivo `/etc/waagent.conf` e reiniciar o serviço WALinuxAgent para que as configurações atualizadas entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-185">You need to increase `ResourceDisk.SwapSizeMB` in the `/etc/waagent.conf` file and restart the WALinuxAgent service in order for the updated settings to take effect.</span></span> <span data-ttu-id="f3aa2-186">Como ele é um arquivo somente leitura, você precisa alterar as permissões de arquivo para habilitar o acesso de gravação.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-186">Because it is a read-only file, you need to change file permissions to enable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="f3aa2-187">Pesquise o `ResourceDisk.SwapSizeMB` e altere o valor para **8.192**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-187">Search for `ResourceDisk.SwapSizeMB` and change the value to **8192**.</span></span> <span data-ttu-id="f3aa2-188">Será necessário pressionar `insert` para entrar no modo de inserção, digitar o valor de **8.192** e, em seguida, pressionar `esc` para retornar ao modo de comando.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-188">You will need to press `insert` to enter insert mode, type in the value of **8192** and then press `esc` to return to command mode.</span></span> <span data-ttu-id="f3aa2-189">Para gravar as alterações e encerre o arquivo, digite `:wq` e pressione `enter`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-189">To write the changes and quit the file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f3aa2-190">É altamente recomendável que você sempre use o `WALinuxAgent` para configurar o espaço de troca, de forma que ele seja sempre criado no disco efêmero local (disco temporário) para um desempenho melhor.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-190">We highly recommend that you always use `WALinuxAgent` to configure swap space so that it's always created on the local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="f3aa2-191">Para obter mais informações sobre isso, consulte [Como adicionar um arquivo de permuta em máquinas virtuais Linux do Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-191">For more information on, see [How to add a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-to-run-x11"></a><span data-ttu-id="f3aa2-192">Preparar seu cliente local e a VM para executar x11</span><span class="sxs-lookup"><span data-stu-id="f3aa2-192">Prepare your local client and VM to run x11</span></span>
<span data-ttu-id="f3aa2-193">A configuração do Oracle ASM exige uma interface gráfica para concluir a instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-193">Configuring Oracle ASM requires a graphical interface to complete the install and configuration.</span></span> <span data-ttu-id="f3aa2-194">Estamos usando o protocolo x11 para facilitar essa instalação.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-194">We are using the x11 protocol to facilitate this installation.</span></span> <span data-ttu-id="f3aa2-195">Se você estiver usando um sistema de cliente (Mac ou Linux) que já tenha os recursos X11 habilitados e configurados, você poderá ignorar esta configuração e instalação exclusivas para computadores Windows.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive to Windows machines.</span></span> 

1. <span data-ttu-id="f3aa2-196">[Baixe o PuTTY](http://www.putty.org/) e o [Xming](https://xming.en.softonic.com/) em seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) to your Windows computer.</span></span> <span data-ttu-id="f3aa2-197">Você precisará concluir a instalação desses dois aplicativos com os valores padrão antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-197">You will need to complete the installation of both of these applications with the default values before proceeding.</span></span>

2. <span data-ttu-id="f3aa2-198">Depois de instalar o PuTTY, abra um prompt de comando, altere para a pasta PuTTY (por exemplo, C:\Program Files\PuTTY) e execute `puttygen.exe` para gerar uma chave.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-198">After you install PuTTY, open a command prompt, change into the PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order to generate a key.</span></span>

3. <span data-ttu-id="f3aa2-199">No Gerador de Chave PuTTY:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="f3aa2-200">Gere uma chave selecionando o botão `Generate`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-200">Generate a key by selecting the `Generate` button.</span></span>
   2. <span data-ttu-id="f3aa2-201">Copie o conteúdo da chave (Ctrl+C).</span><span class="sxs-lookup"><span data-stu-id="f3aa2-201">Copy the contents of the key (Ctrl+C).</span></span>
   3. <span data-ttu-id="f3aa2-202">Selecione o botão `Save private key`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-202">Select the `Save private key` button.</span></span>
   4. <span data-ttu-id="f3aa2-203">Ignore o aviso sobre proteger a chave com uma frase secreta e, em seguida, selecione `OK`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-203">Ignore the warning about securing the key with a passphrase, and then select `OK`.</span></span>

   ![Captura de tela do Gerador de Chaves PuTTY](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="f3aa2-205">Em sua VM, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="f3aa2-206">Crie um arquivo chamado `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="f3aa2-207">Cole o conteúdo da chave nesse arquivo e salve-o.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-207">Paste the contents of the key in this file, and then save the file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f3aa2-208">A chave deve conter a cadeia de caracteres `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-208">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="f3aa2-209">Além disso, o conteúdo da chave deve ser uma única linha de texto.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-209">Also, the contents of the key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="f3aa2-210">No sistema cliente, inicie o PuTTY.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="f3aa2-211">No painel **Categoria**, vá para **Conexão** > **SSH** > **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-211">In the **Category** pane, go to **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="f3aa2-212">Na caixa **Arquivo de chave privada para autenticação**, navegue até a chave que você gerou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-212">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

   ![Captura de tela das opções de autenticação SSH](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="f3aa2-214">No painel **Categoria**, vá para **Conexão** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-214">In the **Category** pane, go to **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="f3aa2-215">Selecione a caixa de seleção **Habilitar encaminhamento X11**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-215">Select the **Enable X11 forwarding** check box.</span></span>

   ![Captura de tela das opções de encaminhamento X11 do SSH](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="f3aa2-217">No painel **Categoria**, vá para **Sessão**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-217">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="f3aa2-218">Insira sua VM Oracle ASM `<publicIPaddress>` na caixa de diálogo nome do host, preencha um novo nome `Saved Session` e, em seguida, clique em `Save`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-218">Enter your Oracle ASM VM `<publicIPaddress>` in the host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="f3aa2-219">Uma vez salvo, clique em `open` para se conectar à sua máquina virtual Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-219">Once saved, click on `open` to connect to your Oracle ASM virtual machine.</span></span>  <span data-ttu-id="f3aa2-220">Na primeira vez que se conectar você será avisado de que o sistema remoto não está em cache no registro.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-220">The first time you connect you are warned  the remote system is not cached in your registry.</span></span> <span data-ttu-id="f3aa2-221">Clique em `yes` para adicioná-lo e continuar.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-221">Click on `yes` to add it and continue.</span></span>

   ![Captura de tela das opções de sessão do PuTTY](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="f3aa2-223">Instalar a infraestrutura em grade do Oracle</span><span class="sxs-lookup"><span data-stu-id="f3aa2-223">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="f3aa2-224">Para instalar a infraestrutura em grade do Oracle, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-224">To install Oracle Grid Infrastructure, complete the following steps:</span></span>

1. <span data-ttu-id="f3aa2-225">Entre como **grade**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-225">Sign in as **grid**.</span></span> <span data-ttu-id="f3aa2-226">(Você deve ser capaz de entrar sem inserir uma senha.)</span><span class="sxs-lookup"><span data-stu-id="f3aa2-226">(You should be able to sign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="f3aa2-227">Se estiver executando o Windows, verifique se você iniciou o Xming antes de começar a instalação.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-227">If you are running Windows, make sure you have started Xming before you begin the installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="f3aa2-228">O instalador da Infraestrutura em grade do Oracle 12c versão 1 é aberto.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-228">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="f3aa2-229">(Pode levar alguns minutos para iniciar o instalador.)</span><span class="sxs-lookup"><span data-stu-id="f3aa2-229">(It might take a few minutes for the  installer to start.)</span></span>

2. <span data-ttu-id="f3aa2-230">Na página **Selecionar Opção de Instalação** , selecione **Instalar e Configurar a Infraestrutura em grade do Oracle para um Servidor Autônomo**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-230">On the **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Captura de tela da página Selecionar opção de instalação do instalador](./media/oracle-asm/install01.png)

3. <span data-ttu-id="f3aa2-232">Na página **Selecionar Idiomas do Produto**, verifique se **Inglês** ou o idioma desejado está selecionado.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-232">On the **Select Product Languages** page, ensure **English** or the language that you want is selected.</span></span>  <span data-ttu-id="f3aa2-233">Clique em `next`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-233">Click `next`.</span></span>

4. <span data-ttu-id="f3aa2-234">Na página **Criar grupo de discos ASM**:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-234">On the **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="f3aa2-235">Insira um nome para o grupo de discos.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-235">Enter a name for the disk group.</span></span>
   - <span data-ttu-id="f3aa2-236">Em **Redundância**, selecione **Externa**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-236">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="f3aa2-237">Em **Tamanho da Unidade de Alocação**, selecione **4**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-237">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="f3aa2-238">Em **Adicionar Discos**, selecione **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-238">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="f3aa2-239">Clique em `next`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-239">Click `next`.</span></span>

5. <span data-ttu-id="f3aa2-240">Na página **Especificar Senha ASM**, selecione a opção **Usar as mesmas senhas para essas contas** e digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-240">On the **Specify ASM Password** page, select the **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Captura de tela da página Especificar Senha de ASM do instalador](./media/oracle-asm/install04.png)

6. <span data-ttu-id="f3aa2-242">Na página **Especificar opções de gerenciamento**, você tem a opção de configurar o controle de nuvem EM.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-242">On the **Specify Management Options** page, you have the option to configure EM Cloud Control.</span></span> <span data-ttu-id="f3aa2-243">Vamos ignorar essa opção – clique em `next` para continuar.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-243">We are skipping this option - click `next` to continue.</span></span> 

7. <span data-ttu-id="f3aa2-244">Na página **Grupos Privilegiados do Sistema Operacional**, use as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-244">On the **Privileged Operating System Groups** page, use the default settings.</span></span> <span data-ttu-id="f3aa2-245">Clique em `next` para continuar.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-245">Click `next` to continue.</span></span>

8. <span data-ttu-id="f3aa2-246">Na página **Especificar Local de Instalação**, use as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-246">On the **Specify Installation Location** page, use the default settings.</span></span> <span data-ttu-id="f3aa2-247">Clique em `next` para continuar.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-247">Click `next` to continue.</span></span>

9. <span data-ttu-id="f3aa2-248">Na página **Criar inventário**, altere o diretório de inventário para `/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-248">On the **Create Inventory** page, change the Inventory Directory to `/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="f3aa2-249">Clique em `next` para continuar.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-249">Click `next` to continue.</span></span>

   ![Captura de tela da página Criar Inventário do Instalador](./media/oracle-asm/install08.png)

10. <span data-ttu-id="f3aa2-251">Na página **Configuração de execução de script de raiz**, marque a caixa de seleção **Executar scripts de configuração automaticamente**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-251">On the **Root script execution configuration** page, select the **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="f3aa2-252">Em seguida, selecione a opção **Usar credenciais de usuário "raiz"** e digite a senha do usuário raiz.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-252">Then, select the **Use "root" user credential** option, and enter the root user password.</span></span>

    ![Captura de tela da página Configuração de execução de script de raiz do instalador](./media/oracle-asm/install09.png)

11. <span data-ttu-id="f3aa2-254">Na página **Realizar verificações de pré-requisito**, a instalação atual falhará com erros.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-254">On the **Perform Prerequisite Checks** page, the current setup will fail with errors.</span></span> <span data-ttu-id="f3aa2-255">Este é um comportamento esperado.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-255">This is an expected behavior.</span></span> <span data-ttu-id="f3aa2-256">Selecione `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-256">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="f3aa2-257">Na caixa de diálogo **Script de Correção**, clique em `OK`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-257">In the **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="f3aa2-258">Na página **Resumo**, examine suas configurações selecionadas e clique em `Install`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-258">On the **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Captura de tela da página Resumo do instalador](./media/oracle-asm/install12.png)

14. <span data-ttu-id="f3aa2-260">Uma caixa de diálogo de aviso será exibida informando a você que os scripts de configuração precisam ser executados como um usuário com privilégios.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-260">A warning dialog box appears informing you configuration scripts need to be run as a privileged user.</span></span> <span data-ttu-id="f3aa2-261">Clique em `Yes` para continuar.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-261">Click `Yes` to continue.</span></span>

15. <span data-ttu-id="f3aa2-262">Na página **Concluir**, clique em `Close` para terminar a instalação.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-262">On the **Finish** page, click `Close` to finish the installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="f3aa2-263">Configurar a sua instalação do Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="f3aa2-263">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="f3aa2-264">Para configurar a instalação do Oracle ASM, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-264">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="f3aa2-265">Verifique se você ainda está conectado como **grade**, da sua sessão X11.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-265">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="f3aa2-266">Talvez seja necessário pressionar `enter` para reviver terminal.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-266">You might need to hit `enter` to revive the terminal.</span></span> <span data-ttu-id="f3aa2-267">Em seguida, inicie o Assistente de configuração do Oracle Automated Storage Management:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-267">Then launch the Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="f3aa2-268">O assistente de configuração do Oracle ASM é aberto.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-268">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="f3aa2-269">Na caixa de diálogo **Configurar ASM: grupos de disco**, clique no botão `Create` e, em seguida, clique em `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-269">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="f3aa2-270">Na caixa de diálogo **Criar Grupo de Discos**:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-270">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="f3aa2-271">Insira o nome do grupo de disco **DATA**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-271">Enter the disk group name **DATA**.</span></span>
   - <span data-ttu-id="f3aa2-272">Em **Selecionar discos membros**, selecione **ORCL_DATA** e **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-272">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="f3aa2-273">Em **Tamanho da Unidade de Alocação**, selecione **4**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-273">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="f3aa2-274">Clique em `ok` para criar o grupo de discos.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-274">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="f3aa2-275">Clique em `ok` para fechar a janela de confirmação.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-275">Click `ok` to close the confirmation window.</span></span>

   ![Captura de tela da caixa de diálogo Criar Grupo de Discos](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="f3aa2-277">Na caixa de diálogo **Configurar ASM: grupos de disco**, clique no botão `Create` e, em seguida, clique em `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-277">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="f3aa2-278">Na caixa de diálogo **Criar Grupo de Discos**:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-278">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="f3aa2-279">Insira o nome do grupo de disco **FRA**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-279">Enter the disk group name **FRA**.</span></span>
   - <span data-ttu-id="f3aa2-280">Em **Redundância**, selecione **Externa (nenhuma)**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-280">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="f3aa2-281">Em **Selecionar discos membros**, selecione **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-281">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="f3aa2-282">Em **Tamanho da Unidade de Alocação**, selecione **4**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-282">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="f3aa2-283">Clique em `ok` para criar o grupo de discos.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-283">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="f3aa2-284">Clique em `ok` para fechar a janela de confirmação.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-284">Click `ok` to close the confirmation window.</span></span>

   ![Captura de tela da caixa de diálogo Criar Grupo de Discos](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="f3aa2-286">Selecione **Sair** para fechar o assistente de configuração do ASM.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-286">Select **Exit** to close ASM Configuration Assistant.</span></span>

   ![Captura de tela da caixa de diálogo Configurar ASM: grupos de discos com o botão Sair](./media/oracle-asm/asm05.png)

## <a name="create-the-database"></a><span data-ttu-id="f3aa2-288">Criar o banco de dados</span><span class="sxs-lookup"><span data-stu-id="f3aa2-288">Create the database</span></span>

<span data-ttu-id="f3aa2-289">O software do Oracle Database já está instalado na imagem do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-289">The Oracle database software is already installed on the Azure Marketplace image.</span></span> <span data-ttu-id="f3aa2-290">Para criar um banco de dados, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-290">To create a database, complete the following steps:</span></span>

1. <span data-ttu-id="f3aa2-291">Mude usuários para o superusuário oracle e inicialize o ouvinte para registro em log:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-291">Switch users to the Oracle superuser, and then initialize the listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="f3aa2-292">O assistente de configuração do banco de dados é aberto.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-292">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="f3aa2-293">Na página **Operação do Banco de dados**, clique em `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-293">On the **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="f3aa2-294">Na página **Modo de Criação**:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-294">On the **Creation Mode** page:</span></span>

   - <span data-ttu-id="f3aa2-295">Insira um nome para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-295">Enter a name for the database.</span></span>
   - <span data-ttu-id="f3aa2-296">Para **Tipo de armazenamento**, verifique se **ASM (Automatic Storage Management )** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-296">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="f3aa2-297">Para **Local dos Arquivos de Banco de Dado**, use o local padrão sugerido pelo ASM.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-297">For **Database Files Location**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="f3aa2-298">Para **Área de recuperação rápida**, use o local padrão sugerido pelo ASM.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-298">For **Fast Recovery Area**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="f3aa2-299">digite uma **Senha administrativa** e **confirme a senha**.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-299">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="f3aa2-300">certifique-se de que `create as container database` esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-300">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="f3aa2-301">digite um valor `pluggable database name`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-301">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="f3aa2-302">Na página **Resumo**, examine suas configurações selecionadas e, em seguida, clique em `Finish` para criar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-302">On the **Summary** page, review your selected settings, and then click `Finish` to create the database.</span></span>

   ![Captura de tela da página Resumo](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="f3aa2-304">O Banco de dados foi criado.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-304">The Database has been created.</span></span> <span data-ttu-id="f3aa2-305">Na página **Concluir**, você tem a opção de desbloquear contas adicionais para usar esse banco de dados e alterar as senhas.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-305">On the **Finish** page, you have the option to unlock additional accounts to use this database and change the passwords.</span></span> <span data-ttu-id="f3aa2-306">Se você quiser fazer isso, selecione **Gerenciamento de Senhas** – caso contrário, clique em `close`.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-306">If you wish to do so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-the-vm"></a><span data-ttu-id="f3aa2-307">Excluir a VM</span><span class="sxs-lookup"><span data-stu-id="f3aa2-307">Delete the VM</span></span>

<span data-ttu-id="f3aa2-308">Você configurou com êxito o Oracle Automated Storage Management na imagem do Oracle DB do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f3aa2-308">You have successfully configured Oracle Automated Storage Management on the Oracle DB image from the Azure Marketplace.</span></span>  <span data-ttu-id="f3aa2-309">Quando essa VM não for mais necessária, o comando abaixo poderá ser usado para remover o grupo de recursos, a VM e todos os recursos relacionados:</span><span class="sxs-lookup"><span data-stu-id="f3aa2-309">When you no longer need this VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f3aa2-310">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f3aa2-310">Next steps</span></span>

[<span data-ttu-id="f3aa2-311">Tutorial: configurar o Oracle DataGuard</span><span class="sxs-lookup"><span data-stu-id="f3aa2-311">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="f3aa2-312">Tutorial: configurar o Oracle GoldenGate</span><span class="sxs-lookup"><span data-stu-id="f3aa2-312">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="f3aa2-313">Examine [Projetar um Oracle DB](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="f3aa2-313">Review [Architect an Oracle DB](oracle-design.md)</span></span>
