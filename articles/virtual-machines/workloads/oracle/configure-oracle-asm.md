---
title: "aaaSet backup Oracle ASM em uma máquina virtual de Linux do Azure | Microsoft Docs"
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
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="6541a-103">Configurar o Oracle ASM em uma máquina virtual Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="6541a-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="6541a-104">Máquinas virtuais do Azure fornecem um ambiente de computação totalmente configurável e flexível.</span><span class="sxs-lookup"><span data-stu-id="6541a-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="6541a-105">Este tutorial aborda a implantação básica da máquina virtual do Azure combinada com a instalação de saudação e a configuração do Oracle Automated Storage Management (ASM).</span><span class="sxs-lookup"><span data-stu-id="6541a-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="6541a-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="6541a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6541a-107">Criar e conectar tooan VM de banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="6541a-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="6541a-108">Instalar e configurar o Oracle Automated Storage Management</span><span class="sxs-lookup"><span data-stu-id="6541a-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="6541a-109">Instalar e configurar a infraestrutura Oracle Grid</span><span class="sxs-lookup"><span data-stu-id="6541a-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="6541a-110">Inicializar uma instalação do Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="6541a-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="6541a-111">Criar um Oracle DB gerenciado por ASM</span><span class="sxs-lookup"><span data-stu-id="6541a-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6541a-112">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6541a-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6541a-113">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6541a-114">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6541a-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="6541a-115">Preparar o ambiente de saudação</span><span class="sxs-lookup"><span data-stu-id="6541a-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="6541a-116">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6541a-116">Create a resource group</span></span>

<span data-ttu-id="6541a-117">toocreate um grupo de recursos, use Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6541a-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6541a-118">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6541a-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="6541a-119">Neste exemplo, um grupo de recursos denominado *myResourceGroup* em Olá *eastus* região.</span><span class="sxs-lookup"><span data-stu-id="6541a-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="6541a-120">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6541a-120">Create a VM</span></span>

<span data-ttu-id="6541a-121">toocreate uma máquina virtual com base na imagem do banco de dados Oracle hello e configurá-lo toouse Oracle ASM, use Olá [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6541a-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="6541a-122">Olá, exemplo a seguir cria uma VM denominada myVM que é um tamanho de Standard_DS2_v2 com quatro discos de dados anexado de 50 GB.</span><span class="sxs-lookup"><span data-stu-id="6541a-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="6541a-123">Se eles ainda não existir no local de chave saudação padrão, ele também cria chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="6541a-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="6541a-124">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="6541a-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="6541a-125">Depois de criar hello VM, CLI do Azure exibe informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="6541a-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="6541a-126">Observe o valor de saudação para `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="6541a-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="6541a-127">Usar o hello de tooaccess esse endereço VM.</span><span class="sxs-lookup"><span data-stu-id="6541a-127">You use this address tooaccess hello VM.</span></span>

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

### <a name="connect-toohello-vm"></a><span data-ttu-id="6541a-128">Conecte-se toohello VM</span><span class="sxs-lookup"><span data-stu-id="6541a-128">Connect toohello VM</span></span>

<span data-ttu-id="6541a-129">toocreate uma sessão SSH com hello VM e definir configurações adicionais, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="6541a-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="6541a-130">Substitua o endereço IP de saudação com hello `publicIpAddress` valor para a VM.</span><span class="sxs-lookup"><span data-stu-id="6541a-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="6541a-131">Instalar o Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="6541a-131">Install Oracle ASM</span></span>

<span data-ttu-id="6541a-132">tooinstall Oracle ASM Olá concluir as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="6541a-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="6541a-133">Para saber mais sobre como instalar o ASM do Oracle, confira [Downloads do Oracle ASMLib para Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span><span class="sxs-lookup"><span data-stu-id="6541a-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="6541a-134">É necessário toologin como raiz em ordem toocontinue com instalação ASM:</span><span class="sxs-lookup"><span data-stu-id="6541a-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="6541a-135">Execute esses comandos adicionais componentes do Oracle ASM tooinstall:</span><span class="sxs-lookup"><span data-stu-id="6541a-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="6541a-136">Verifique se o Oracle ASM está instalado:</span><span class="sxs-lookup"><span data-stu-id="6541a-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="6541a-137">saída de Hello desse comando deve listar Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="6541a-138">ASM requer usuários e funções na ordem toofunction corretamente.</span><span class="sxs-lookup"><span data-stu-id="6541a-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="6541a-139">Olá comandos a seguir cria grupos e contas de usuário de pré-requisito hello:</span><span class="sxs-lookup"><span data-stu-id="6541a-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="6541a-140">Verifique se os usuários e grupos foram criados corretamente:</span><span class="sxs-lookup"><span data-stu-id="6541a-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="6541a-141">Olá saída desse comando deve listar seguinte Olá usuários e grupos:</span><span class="sxs-lookup"><span data-stu-id="6541a-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="6541a-142">Crie uma pasta para o usuário *grade* e alterar o proprietário de saudação:</span><span class="sxs-lookup"><span data-stu-id="6541a-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="6541a-143">Configurar o Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="6541a-143">Set up Oracle ASM</span></span>

<span data-ttu-id="6541a-144">Para este tutorial, o usuário de padrão de saudação é *grade* e saudação padrão grupo é *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="6541a-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="6541a-145">Certifique-se de que Olá *oracle* usuário faz parte do grupo de asmadmin hello.</span><span class="sxs-lookup"><span data-stu-id="6541a-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="6541a-146">tooset a instalação com a Oracle ASM, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="6541a-147">Configurando o driver de biblioteca do Oracle ASM Olá envolve a definição de usuário padrão de saudação (grade) e o grupo padrão (asmadmin), bem como configurar Olá unidade toostart na inicialização (escolha y) e tooscan para discos de inicialização (escolha y).</span><span class="sxs-lookup"><span data-stu-id="6541a-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="6541a-148">É necessário tooanswer Olá prompts de saudação comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="6541a-149">saída de Hello desse comando deve ter toohello semelhante a seguir, parando com toobe prompts respondida.</span><span class="sxs-lookup"><span data-stu-id="6541a-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="6541a-150">Exibir a configuração de disco hello:</span><span class="sxs-lookup"><span data-stu-id="6541a-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="6541a-151">saída de Hello desse comando deve ser semelhante toohello seguir a lista de discos disponíveis</span><span class="sxs-lookup"><span data-stu-id="6541a-151">hello output of this command should look similar toohello following listing of available disks</span></span>

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

3. <span data-ttu-id="6541a-152">Formatar o disco */desenvolvimento/sdc* executando Olá comando a seguir e responder Olá prompts com:</span><span class="sxs-lookup"><span data-stu-id="6541a-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="6541a-153">*n* para a nova partição</span><span class="sxs-lookup"><span data-stu-id="6541a-153">*n* for new partition</span></span>
   - <span data-ttu-id="6541a-154">*p* para a partição primária</span><span class="sxs-lookup"><span data-stu-id="6541a-154">*p* for primary partition</span></span>
   - <span data-ttu-id="6541a-155">*1* primeira partição do tooselect Olá</span><span class="sxs-lookup"><span data-stu-id="6541a-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="6541a-156">Pressione `enter` para primeiro cilindro do saudação padrão</span><span class="sxs-lookup"><span data-stu-id="6541a-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="6541a-157">Pressione `enter` para último cilindro do saudação padrão</span><span class="sxs-lookup"><span data-stu-id="6541a-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="6541a-158">Pressione *w* tabela de partição toowrite Olá alterações toohello</span><span class="sxs-lookup"><span data-stu-id="6541a-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="6541a-159">Saída Olá para o comando de fdisk hello usando respostas Olá fornecidas acima, deverá parecer como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
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
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="6541a-160">Repita Olá precede o comando fdisk para `/dev/sdd`, `/dev/sde`, e `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="6541a-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="6541a-161">Verifique a configuração de disco hello:</span><span class="sxs-lookup"><span data-stu-id="6541a-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="6541a-162">saída de saudação do comando Olá deve ter aparência Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-162">hello output of hello command should look like hello following:</span></span>

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

6. <span data-ttu-id="6541a-163">Verificar status do serviço Oracle ASM hello e iniciar o serviço do Oracle ASM hello:</span><span class="sxs-lookup"><span data-stu-id="6541a-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="6541a-164">saída de saudação do comando Olá deve ter aparência Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="6541a-165">Crie discos do Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="6541a-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="6541a-166">saída de saudação do comando Olá deve ter aparência Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="6541a-167">Liste os discos do Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="6541a-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="6541a-168">saída de saudação do comando Olá deve listar off Olá seguintes discos Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="6541a-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="6541a-169">Alterar as senhas de saudação para usuários de raiz, oracle e grade hello.</span><span class="sxs-lookup"><span data-stu-id="6541a-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="6541a-170">**Anote essas novas senhas** como eles serão usados posteriormente, durante a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="6541a-171">Alterar permissões de pasta hello:</span><span class="sxs-lookup"><span data-stu-id="6541a-171">Change hello folder permission:</span></span>

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

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="6541a-172">Baixe e prepare a infraestrutura em grade do Oracle</span><span class="sxs-lookup"><span data-stu-id="6541a-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="6541a-173">toodownload e preparar o software de infraestrutura de grade Oracle hello, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="6541a-174">Fazer o download de infraestrutura de grade Oracle Olá [página de download do Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="6541a-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="6541a-175">Em download de saudação intitulada **banco de dados Oracle 12c versão 1 grade infraestrutura (12.1.0.2.0) para Linux x86-64**, baixar arquivos. zip de saudação dois.</span><span class="sxs-lookup"><span data-stu-id="6541a-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="6541a-176">Depois de baixar o computador cliente do hello. zip arquivos tooyour, você pode usar o protocolo de cópia seguro (SCP) toocopy Olá arquivos tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="6541a-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="6541a-177">SSH volta para sua VM Oracle no Azure em arquivos do pedido toomove hello. zip em Olá / Escolher pasta.</span><span class="sxs-lookup"><span data-stu-id="6541a-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="6541a-178">Em seguida, altere o proprietário de saudação do arquivos hello:</span><span class="sxs-lookup"><span data-stu-id="6541a-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="6541a-179">Descompacte arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-179">Unzip hello files.</span></span> <span data-ttu-id="6541a-180">(Instalação Olá Linux Descompacte ferramenta se ele ainda não estiver instalado.)</span><span class="sxs-lookup"><span data-stu-id="6541a-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="6541a-181">Alterar permissão:</span><span class="sxs-lookup"><span data-stu-id="6541a-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="6541a-182">Atualize o espaço de troca configurado.</span><span class="sxs-lookup"><span data-stu-id="6541a-182">Update configured swap space.</span></span> <span data-ttu-id="6541a-183">Componentes de grade Oracle necessário pelo menos 6,8 GB de espaço de permuta tooinstall grade.</span><span class="sxs-lookup"><span data-stu-id="6541a-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="6541a-184">tamanho de arquivo de permuta Olá padrão para as imagens da Oracle Linux no Azure é apenas 2048MB.</span><span class="sxs-lookup"><span data-stu-id="6541a-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="6541a-185">Você precisa tooincrease `ResourceDisk.SwapSizeMB` em Olá `/etc/waagent.conf` de arquivo e reiniciar serviço de WALinuxAgent Olá Olá atualizado configurações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="6541a-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="6541a-186">Como é um arquivo somente leitura, é necessário o acesso de gravação do toochange arquivo permissões tooenable.</span><span class="sxs-lookup"><span data-stu-id="6541a-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="6541a-187">Procurar `ResourceDisk.SwapSizeMB` e altere o valor de saudação muito**8192**.</span><span class="sxs-lookup"><span data-stu-id="6541a-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="6541a-188">Você precisará toopress `insert` tooenter no modo de inserção, tipo de valor de saudação do **8192** e, em seguida, pressione `esc` tooreturn toocommand modo.</span><span class="sxs-lookup"><span data-stu-id="6541a-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="6541a-189">alterações de saudação toowrite e arquivo hello quit, digite `:wq` e pressione `enter`.</span><span class="sxs-lookup"><span data-stu-id="6541a-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6541a-190">É altamente recomendável que você sempre use `WALinuxAgent` tooconfigure espaço de permuta para que ele é sempre criado no hello efêmera disco local (disco temporário) para melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="6541a-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="6541a-191">Para obter mais informações, consulte [como tooadd uma permuta de arquivo em máquinas virtuais do Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="6541a-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="6541a-192">Preparar seu cliente local e a VM toorun x11</span><span class="sxs-lookup"><span data-stu-id="6541a-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="6541a-193">Configurar o Oracle ASM requer uma interface gráfica toocomplete Olá instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="6541a-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="6541a-194">Estamos usando Olá x11 protocolo toofacilitate esta instalação.</span><span class="sxs-lookup"><span data-stu-id="6541a-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="6541a-195">Se você estiver usando um sistema de cliente (Mac ou Linux) que já tenha X11 recursos habilitada e configurada - você pode ignorar essa configuração e instalação máquinas tooWindows exclusivo.</span><span class="sxs-lookup"><span data-stu-id="6541a-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="6541a-196">[Baixar o PuTTY](http://www.putty.org/) e [baixar Xming](https://xming.en.softonic.com/) tooyour computador com Windows.</span><span class="sxs-lookup"><span data-stu-id="6541a-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="6541a-197">Você precisará toocomplete instalação de saudação de ambos os aplicativos com os valores padrão de saudação antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="6541a-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="6541a-198">Depois de instalar o PuTTY, abra um prompt de comando, altere para Olá PuTTY pasta (por exemplo, C:\Program Files\PuTTY) e execute `puttygen.exe` em ordem toogenerate uma chave.</span><span class="sxs-lookup"><span data-stu-id="6541a-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="6541a-199">No Gerador de Chave PuTTY:</span><span class="sxs-lookup"><span data-stu-id="6541a-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="6541a-200">Gerar uma chave selecionando Olá `Generate` botão.</span><span class="sxs-lookup"><span data-stu-id="6541a-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="6541a-201">Copie o conteúdo de saudação da chave de saudação (Ctrl + C).</span><span class="sxs-lookup"><span data-stu-id="6541a-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="6541a-202">Selecione Olá `Save private key` botão.</span><span class="sxs-lookup"><span data-stu-id="6541a-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="6541a-203">Ignorar aviso Olá sobre como proteger a chave de saudação com uma senha e, em seguida, selecione `OK`.</span><span class="sxs-lookup"><span data-stu-id="6541a-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![Captura de tela do Gerador de Chaves PuTTY](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="6541a-205">Em sua VM, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="6541a-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="6541a-206">Crie um arquivo chamado `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="6541a-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="6541a-207">Cole o conteúdo de saudação da chave Olá neste arquivo e, em seguida, salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="6541a-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6541a-208">chave de saudação deve conter a cadeia de caracteres de saudação `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="6541a-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="6541a-209">Além disso, o conteúdo de saudação da chave Olá deve ser uma única linha de texto.</span><span class="sxs-lookup"><span data-stu-id="6541a-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="6541a-210">No sistema cliente, inicie o PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6541a-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="6541a-211">Em Olá **categoria** painel, ir muito**Conexão** > **SSH** > **Auth**. Em Olá **arquivo de chave privada para autenticação** caixa, procure toohello chave gerada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6541a-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Captura de tela de opções de autenticação SSH Olá](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="6541a-213">Em Olá **categoria** painel, ir muito**Conexão** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="6541a-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="6541a-214">Selecione Olá **ativar X11 encaminhamento** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="6541a-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Captura de tela da saudação SSH X11 opções de encaminhamento](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="6541a-216">Em Olá **categoria** painel, ir muito**sessão**.</span><span class="sxs-lookup"><span data-stu-id="6541a-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="6541a-217">Insira sua VM do Oracle ASM `<publicIPaddress>` na caixa de diálogo de nome de host hello, preencha um novo `Saved Session` nome e, em seguida, clique em `Save`.</span><span class="sxs-lookup"><span data-stu-id="6541a-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="6541a-218">Uma vez salvo, clique em `open` tooconnect tooyour Oracle ASM VM.</span><span class="sxs-lookup"><span data-stu-id="6541a-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="6541a-219">Olá primeira vez que você se conectar será avisado não armazenado em cache no registro do sistema remoto hello.</span><span class="sxs-lookup"><span data-stu-id="6541a-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="6541a-220">Clique em `yes` tooadd-lo e continuar.</span><span class="sxs-lookup"><span data-stu-id="6541a-220">Click on `yes` tooadd it and continue.</span></span>

   ![Captura de tela de opções de sessão PuTTY Olá](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="6541a-222">Instalar a infraestrutura em grade do Oracle</span><span class="sxs-lookup"><span data-stu-id="6541a-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="6541a-223">tooinstall infra-estrutura de grade da Oracle, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="6541a-224">Entre como **grade**.</span><span class="sxs-lookup"><span data-stu-id="6541a-224">Sign in as **grid**.</span></span> <span data-ttu-id="6541a-225">(Você deve ser capaz de toosign em sem inserir uma senha.)</span><span class="sxs-lookup"><span data-stu-id="6541a-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="6541a-226">Se você estiver executando o Windows, verifique se que você iniciou Xming antes de começar a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="6541a-227">O instalador da Infraestrutura em grade do Oracle 12c versão 1 é aberto.</span><span class="sxs-lookup"><span data-stu-id="6541a-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="6541a-228">(Ele pode levar alguns minutos para Olá instalador toostart).</span><span class="sxs-lookup"><span data-stu-id="6541a-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="6541a-229">Em Olá **Selecionar opção de instalação** , selecione **instalar e configurar a infraestrutura de grade Oracle para um servidor autônomo**.</span><span class="sxs-lookup"><span data-stu-id="6541a-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Captura de tela da página de selecionar a opção de instalação do instalador Olá](./media/oracle-asm/install01.png)

3. <span data-ttu-id="6541a-231">Em Olá **selecionar idiomas de produto** página, certifique-se de **inglês** ou idioma Olá desejado está selecionado.</span><span class="sxs-lookup"><span data-stu-id="6541a-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="6541a-232">Clique em `next`.</span><span class="sxs-lookup"><span data-stu-id="6541a-232">Click `next`.</span></span>

4. <span data-ttu-id="6541a-233">Em Olá **criar grupo de discos do ASM** página:</span><span class="sxs-lookup"><span data-stu-id="6541a-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="6541a-234">Insira um nome para o grupo de discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="6541a-235">Em **Redundância**, selecione **Externa**.</span><span class="sxs-lookup"><span data-stu-id="6541a-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="6541a-236">Em **Tamanho da Unidade de Alocação**, selecione **4**.</span><span class="sxs-lookup"><span data-stu-id="6541a-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="6541a-237">Em **Adicionar Discos**, selecione **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="6541a-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="6541a-238">Clique em `next`.</span><span class="sxs-lookup"><span data-stu-id="6541a-238">Click `next`.</span></span>

5. <span data-ttu-id="6541a-239">Em Olá **especificar ASM senha** página, selecione Olá **usar as mesmas senhas para essas contas** opção e digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="6541a-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Captura de tela de página de especificar senha de ASM do instalador de saudação](./media/oracle-asm/install04.png)

6. <span data-ttu-id="6541a-241">Em Olá **especificar opções de gerenciamento** página, ter Olá opção tooconfigure EM controle de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6541a-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="6541a-242">Vamos ignorar essa opção - clique `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6541a-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="6541a-243">Em Olá **grupos privilegiados do sistema operacional** página, use as configurações padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="6541a-244">Clique em `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6541a-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="6541a-245">Em Olá **especificar local de instalação** página, use as configurações padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="6541a-246">Clique em `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6541a-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="6541a-247">Em Olá **Criar inventário** página, altere Olá Directory inventário muito`/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="6541a-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="6541a-248">Clique em `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6541a-248">Click `next` toocontinue.</span></span>

   ![Captura da página de criar inventário do instalador Olá](./media/oracle-asm/install08.png)

10. <span data-ttu-id="6541a-250">Em Olá **configuração de execução de script raiz** página, selecione Olá **automaticamente executar scripts de configuração** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="6541a-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="6541a-251">Em seguida, selecione Olá **usar credenciais de usuário "raiz"** opção e digite a senha do usuário raiz hello.</span><span class="sxs-lookup"><span data-stu-id="6541a-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Captura de tela da página de configuração de execução de script do instalador Olá raiz](./media/oracle-asm/install09.png)

11. <span data-ttu-id="6541a-253">Em Olá **executar verificações de pré-requisito** página, a instalação atual do hello falhará com erros.</span><span class="sxs-lookup"><span data-stu-id="6541a-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="6541a-254">Este é um comportamento esperado.</span><span class="sxs-lookup"><span data-stu-id="6541a-254">This is an expected behavior.</span></span> <span data-ttu-id="6541a-255">Selecione `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="6541a-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="6541a-256">Em Olá **Script de correção** caixa de diálogo, clique em `OK`.</span><span class="sxs-lookup"><span data-stu-id="6541a-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="6541a-257">Em Olá **resumo** página, examine as configurações selecionadas e, em seguida, clique em `Install`.</span><span class="sxs-lookup"><span data-stu-id="6541a-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Captura de tela da página de resumo do instalador Olá](./media/oracle-asm/install12.png)

14. <span data-ttu-id="6541a-259">Uma caixa de diálogo de aviso será exibida informando os scripts de configuração precisa toobe executar como um usuário com privilégios.</span><span class="sxs-lookup"><span data-stu-id="6541a-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="6541a-260">Clique em `Yes` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6541a-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="6541a-261">Em Olá **concluir** , clique em `Close` toofinish instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="6541a-262">Configurar a sua instalação do Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="6541a-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="6541a-263">tooset a instalação com a Oracle ASM, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="6541a-264">Verifique se você ainda está conectado como **grade**, da sua sessão X11.</span><span class="sxs-lookup"><span data-stu-id="6541a-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="6541a-265">Talvez seja necessário toohit `enter` toorevive Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="6541a-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="6541a-266">Em seguida, inicie Olá Oracle Automated Storage Management Assistente de configuração:</span><span class="sxs-lookup"><span data-stu-id="6541a-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="6541a-267">O assistente de configuração do Oracle ASM é aberto.</span><span class="sxs-lookup"><span data-stu-id="6541a-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="6541a-268">Em Olá **configurar ASM: grupos de discos** caixa de diálogo, clique em Olá `Create` botão e, em seguida, clique em `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="6541a-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="6541a-269">Em Olá **criar grupo de discos** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="6541a-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="6541a-270">Inserir nome do grupo de disco Olá **dados**.</span><span class="sxs-lookup"><span data-stu-id="6541a-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="6541a-271">Em **Selecionar discos membros**, selecione **ORCL_DATA** e **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="6541a-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="6541a-272">Em **Tamanho da Unidade de Alocação**, selecione **4**.</span><span class="sxs-lookup"><span data-stu-id="6541a-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="6541a-273">Clique em `ok` toocreate grupo de discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="6541a-274">Clique em `ok` tooclose janela de confirmação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Captura de tela da caixa de diálogo Criar grupo de discos Olá](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="6541a-276">Em Olá **configurar ASM: grupos de discos** caixa de diálogo, clique em Olá `Create` botão e, em seguida, clique em `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="6541a-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="6541a-277">Em Olá **criar grupo de discos** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="6541a-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="6541a-278">Inserir nome do grupo de disco Olá **FRA**.</span><span class="sxs-lookup"><span data-stu-id="6541a-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="6541a-279">Em **Redundância**, selecione **Externa (nenhuma)**.</span><span class="sxs-lookup"><span data-stu-id="6541a-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="6541a-280">Em **Selecionar discos membros**, selecione **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="6541a-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="6541a-281">Em **Tamanho da Unidade de Alocação**, selecione **4**.</span><span class="sxs-lookup"><span data-stu-id="6541a-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="6541a-282">Clique em `ok` toocreate grupo de discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="6541a-283">Clique em `ok` tooclose janela de confirmação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Captura de tela da caixa de diálogo Criar grupo de discos Olá](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="6541a-285">Selecione **Exit** tooclose o Assistente de configuração do ASM.</span><span class="sxs-lookup"><span data-stu-id="6541a-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![Captura de tela de Olá configurar ASM: caixa de diálogo de grupos de discos com o botão de saída](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="6541a-287">Criar banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="6541a-287">Create hello database</span></span>

<span data-ttu-id="6541a-288">Olá software de banco de dados Oracle já está instalado na imagem do hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6541a-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="6541a-289">toocreate um banco de dados, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="6541a-290">Alternar superusuário do usuários toohello Oracle e, em seguida, inicializar o ouvinte de saudação para registro em log:</span><span class="sxs-lookup"><span data-stu-id="6541a-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="6541a-291">O assistente de configuração do banco de dados é aberto.</span><span class="sxs-lookup"><span data-stu-id="6541a-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="6541a-292">Em Olá **operação de banco de dados** , clique em `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="6541a-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="6541a-293">Em Olá **modo de criação de** página:</span><span class="sxs-lookup"><span data-stu-id="6541a-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="6541a-294">Insira um nome para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="6541a-295">Para **Tipo de armazenamento**, verifique se **ASM (Automatic Storage Management )** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="6541a-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="6541a-296">Para **local dos arquivos de banco de dados**, use o padrão de saudação ASM sugerido local.</span><span class="sxs-lookup"><span data-stu-id="6541a-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="6541a-297">Para **área de recuperação rápida**, use o padrão de saudação ASM sugerido local.</span><span class="sxs-lookup"><span data-stu-id="6541a-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="6541a-298">digite uma **Senha administrativa** e **confirme a senha**.</span><span class="sxs-lookup"><span data-stu-id="6541a-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="6541a-299">certifique-se de que `create as container database` esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="6541a-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="6541a-300">digite um valor `pluggable database name`.</span><span class="sxs-lookup"><span data-stu-id="6541a-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="6541a-301">Em Olá **resumo** página, examine as configurações selecionadas e, em seguida, clique em `Finish` o banco de dados do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6541a-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Captura de tela da página de resumo de saudação](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="6541a-303">Olá banco de dados foi criado.</span><span class="sxs-lookup"><span data-stu-id="6541a-303">hello Database has been created.</span></span> <span data-ttu-id="6541a-304">Em Olá **concluir** página, você tem Olá opção toounlock contas adicionais toouse esse banco de dados e alterar senhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="6541a-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="6541a-305">Se você desejar toodo isso, selecione **gerenciamento de senha** -caso contrário, clique em `close`.</span><span class="sxs-lookup"><span data-stu-id="6541a-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="6541a-306">Excluir Olá VM</span><span class="sxs-lookup"><span data-stu-id="6541a-306">Delete hello VM</span></span>

<span data-ttu-id="6541a-307">Você configurou com êxito o Oracle Automated Storage Management na imagem de banco de dados Oracle de saudação do hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6541a-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="6541a-308">Quando você não precisa mais essa VM, você pode usar o hello grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6541a-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="6541a-309">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6541a-309">Next steps</span></span>

[<span data-ttu-id="6541a-310">Tutorial: configurar o Oracle DataGuard</span><span class="sxs-lookup"><span data-stu-id="6541a-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="6541a-311">Tutorial: configurar o Oracle GoldenGate</span><span class="sxs-lookup"><span data-stu-id="6541a-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="6541a-312">Examine [Projetar um Oracle DB](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="6541a-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
