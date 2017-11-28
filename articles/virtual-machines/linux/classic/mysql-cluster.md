---
title: aaaClusterize MySQL com conjuntos com balanceamento de carga | Microsoft Docs
description: "Configurar uma balanceamento de carga e alta disponibilidade Linux MySQL cluster criado com o modelo de implantação clássico Olá no Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="150de-103">Use conjuntos com balanceamento de carga tooclusterize MySQL no Linux</span><span class="sxs-lookup"><span data-stu-id="150de-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="150de-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e clássico.</span><span class="sxs-lookup"><span data-stu-id="150de-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="150de-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="150de-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="150de-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="150de-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="150de-107">Um [modelo do Gerenciador de recursos](https://azure.microsoft.com/documentation/templates/mysql-replication/) estará disponível se você precisa toodeploy um cluster do MySQL.</span><span class="sxs-lookup"><span data-stu-id="150de-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="150de-108">Este artigo explora e ilustra Olá abordagens diferentes disponíveis toodeploy serviços altamente disponíveis com base em Linux no Microsoft Azure, exploração de alta disponibilidade do servidor MySQL como um livro de instruções.</span><span class="sxs-lookup"><span data-stu-id="150de-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="150de-109">Há um vídeo ilustrando essa abordagem disponível no [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="150de-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="150de-110">Descrevemos uma solução de alta disponibilidade do MySQL de mestre único, dois nós e sem compartilhar nada, com base em DRBD, Corosync e Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="150de-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="150de-111">Apenas um nó executa o MySQL por vez.</span><span class="sxs-lookup"><span data-stu-id="150de-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="150de-112">Leitura e gravação da saudação recurso DRBD também são limitado tooonly um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="150de-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="150de-113">Não é necessário para uma solução de VIP como LVS, porque você usará conjuntos com balanceamento de carga em recuperação normal de saudação VIP, remoção e detecção de funcionalidade e o ponto de extremidade de round-robin tooprovide Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="150de-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="150de-114">Olá VIP é um endereço IPv4 roteado globalmente atribuído pelo Microsoft Azure quando você cria o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="150de-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="150de-115">Existem outras arquiteturas possíveis para MySQL, inclusive NBD Cluster, Percona e Galera, bem como diversas soluções de middleware, incluindo pelo menos uma disponível como uma VM no [Repositório de VM](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="150de-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="150de-116">Como essas soluções podem replicar unicast e multicast ou difusão e não contam com armazenamento compartilhado ou várias interfaces de rede, cenários de saudação devem ser fácil toodeploy no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="150de-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="150de-117">Essas arquiteturas de cluster podem ser estendidas produtos tooother como PostgreSQL e OpenLDAP de maneira semelhante.</span><span class="sxs-lookup"><span data-stu-id="150de-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="150de-118">Por exemplo, esse procedimento de balanceamento de carga sem compartilhar nada foi testado com êxito com o OpenLDAP multimestres e é possível ver isso em nosso blog Channel 9.</span><span class="sxs-lookup"><span data-stu-id="150de-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="150de-119">Prepare-se</span><span class="sxs-lookup"><span data-stu-id="150de-119">Get ready</span></span>
<span data-ttu-id="150de-120">Você precisa seguir Olá recursos e capacidades:</span><span class="sxs-lookup"><span data-stu-id="150de-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="150de-121">Conta de um Microsoft Azure com uma assinatura válida, toocreate capaz de pelo menos duas VMs (XS foi usado neste exemplo)</span><span class="sxs-lookup"><span data-stu-id="150de-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="150de-122">Uma rede e uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="150de-122">A network and a subnet</span></span>
  - <span data-ttu-id="150de-123">Um grupo de afinidades</span><span class="sxs-lookup"><span data-stu-id="150de-123">An affinity group</span></span>
  - <span data-ttu-id="150de-124">Um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="150de-124">An availability set</span></span>
  - <span data-ttu-id="150de-125">Olá capacidade toocreate VHDs em Olá mesma região que o serviço de nuvem hello e anexá-los em VMs do Linux toohello</span><span class="sxs-lookup"><span data-stu-id="150de-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="150de-126">Ambiente testado</span><span class="sxs-lookup"><span data-stu-id="150de-126">Tested environment</span></span>
* <span data-ttu-id="150de-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="150de-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="150de-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="150de-128">DRBD</span></span>
  * <span data-ttu-id="150de-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="150de-129">MySQL Server</span></span>
  * <span data-ttu-id="150de-130">Corosync e Pacemaker</span><span class="sxs-lookup"><span data-stu-id="150de-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="150de-131">Grupo de afinidade</span><span class="sxs-lookup"><span data-stu-id="150de-131">Affinity group</span></span>
<span data-ttu-id="150de-132">Criar um grupo de afinidade para a solução de saudação entrando no toohello portal clássico do Azure, selecionando **configurações**e criar um grupo de afinidade.</span><span class="sxs-lookup"><span data-stu-id="150de-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="150de-133">Recursos alocados criados posteriormente serão atribuídos toothis grupo de afinidade.</span><span class="sxs-lookup"><span data-stu-id="150de-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="150de-134">Redes</span><span class="sxs-lookup"><span data-stu-id="150de-134">Networks</span></span>
<span data-ttu-id="150de-135">Uma nova rede é criada e uma sub-rede é criada dentro da rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="150de-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="150de-136">Este exemplo usa uma rede 10.10.10.0/24 com apenas uma sub-rede /24 interna.</span><span class="sxs-lookup"><span data-stu-id="150de-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="150de-137">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="150de-137">Virtual machines</span></span>
<span data-ttu-id="150de-138">Olá primeira Ubuntu 13.10 VM é criada usando uma imagem da Galeria de Ubuntu Endorsed e é chamado `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="150de-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="150de-139">Um novo serviço de nuvem é criado no processo de hello, chamado hadb.</span><span class="sxs-lookup"><span data-stu-id="150de-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="150de-140">Esse nome ilustra Olá compartilhado, a natureza de balanceamento de carga que o serviço de saudação terá quando mais recursos são adicionados.</span><span class="sxs-lookup"><span data-stu-id="150de-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="150de-141">Olá criação de `hadb01` é normal e concluídas usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="150de-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="150de-142">Um ponto de extremidade para SSH é criado automaticamente e rede nova hello está selecionada.</span><span class="sxs-lookup"><span data-stu-id="150de-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="150de-143">Agora você pode criar uma conjunto de disponibilidade para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="150de-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="150de-144">Olá primeira máquina virtual é criado (tecnicamente, quando o serviço de nuvem Olá é criado), depois de criar hello segunda VM, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="150de-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="150de-145">Para Olá segundo VM, use Ubuntu 13.10 VM da Galeria de saudação usando o portal de saudação, mas usar um serviço de nuvem existente, `hadb.cloudapp.net`, em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="150de-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="150de-146">conjunto de disponibilidade e rede Olá deve ser selecionado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="150de-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="150de-147">Também será criado um ponto de extremidade SSH.</span><span class="sxs-lookup"><span data-stu-id="150de-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="150de-148">Depois que as duas máquinas virtuais foram criadas, tome nota da porta SSH Olá `hadb01` (TCP 22) e `hadb02` (atribuído automaticamente pelo Azure).</span><span class="sxs-lookup"><span data-stu-id="150de-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="150de-149">Armazenamento anexado</span><span class="sxs-lookup"><span data-stu-id="150de-149">Attached storage</span></span>
<span data-ttu-id="150de-150">Anexar um novo tooboth de disco VMs e criar discos de 5 GB no processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="150de-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="150de-151">discos de saudação são hospedados no contêiner VHD Olá em uso para os discos do sistema operacional principal.</span><span class="sxs-lookup"><span data-stu-id="150de-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="150de-152">Depois que os discos são criados e anexados, não há nenhuma necessidade toorestart Linux porque kernel Olá verá o novo dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="150de-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="150de-153">Este dispositivo é normalmente `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="150de-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="150de-154">Verificar `dmesg` para saída de hello.</span><span class="sxs-lookup"><span data-stu-id="150de-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="150de-155">Em cada VM, criar uma partição usando `cfdisk` (partição primária, do Linux) e gravar Olá nova tabela de partição.</span><span class="sxs-lookup"><span data-stu-id="150de-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="150de-156">Não crie um sistema de arquivos nessa partição.</span><span class="sxs-lookup"><span data-stu-id="150de-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="150de-157">Configurar o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="150de-157">Set up hello cluster</span></span>
<span data-ttu-id="150de-158">Use APT tooinstall Corosync, Pacemaker e DRBD em ambas as VMs do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="150de-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="150de-159">toodo com `apt-get`, execute hello seguinte código:</span><span class="sxs-lookup"><span data-stu-id="150de-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="150de-160">Não instale o MySQL neste momento.</span><span class="sxs-lookup"><span data-stu-id="150de-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="150de-161">Debian e Ubuntu scripts de instalação inicializar um diretório de dados MySQL em `/var/lib/mysql`, mas como diretório hello serão ser substituído por um sistema de arquivos DRBD, é necessário tooinstall MySQL mais tarde.</span><span class="sxs-lookup"><span data-stu-id="150de-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="150de-162">Verifique se (usando `/sbin/ifconfig`) que as duas máquinas virtuais estão usando endereços na sub-rede de 10.10.10.0/24 hello e que eles podem executar ping por nome.</span><span class="sxs-lookup"><span data-stu-id="150de-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="150de-163">Você também pode usar `ssh-keygen` e `ssh-copy-id` toomake-se de que as duas máquinas virtuais podem se comunicar por meio do SSH sem exigir uma senha.</span><span class="sxs-lookup"><span data-stu-id="150de-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="150de-164">Configurar DRBD</span><span class="sxs-lookup"><span data-stu-id="150de-164">Set up DRBD</span></span>
<span data-ttu-id="150de-165">Criar um recurso DRBD que usa Olá subjacente `/dev/sdc1` partição tooproduce um `/dev/drbd1` recursos que podem ser formatados usando ext3 e usados em nós primários e secundários.</span><span class="sxs-lookup"><span data-stu-id="150de-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="150de-166">Abra `/etc/drbd.d/r0.res` e Olá cópia após a definição de recurso em ambas as máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="150de-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="150de-167">Inicializar o recurso hello usando `drbdadm` em ambas as máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="150de-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="150de-168">Em Olá VM primária (`hadb01`), forçar (primária) da propriedade de recurso DRBD hello:</span><span class="sxs-lookup"><span data-stu-id="150de-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="150de-169">Se você examinar o conteúdo de saudação do proc/drbd (`sudo cat /proc/drbd`) em ambas as VMs, você deve ver `Primary/Secondary` na `hadb01` e `Secondary/Primary` em `hadb02`, consistente com a solução de saudação neste momento.</span><span class="sxs-lookup"><span data-stu-id="150de-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="150de-170">disco de 5 GB de saudação é sincronizado pela rede de 10.10.10.0/24 Olá em toocustomers sem custos.</span><span class="sxs-lookup"><span data-stu-id="150de-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="150de-171">Depois disco Olá é sincronizado, você pode criar o sistema de arquivos de saudação em `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="150de-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="150de-172">Para fins de teste, usamos ext2, mas Olá código a seguir cria um sistema de arquivos ext3:</span><span class="sxs-lookup"><span data-stu-id="150de-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="150de-173">Montar Olá DRBD recurso</span><span class="sxs-lookup"><span data-stu-id="150de-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="150de-174">Você está agora pronto toomount recursos DRBD Olá `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="150de-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="150de-175">Debian e derivativos usam `/var/lib/mysql` como diretório de dados do MySQL.</span><span class="sxs-lookup"><span data-stu-id="150de-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="150de-176">Porque você não instalou o MySQL, criar diretório hello e montar Olá DRBD recurso.</span><span class="sxs-lookup"><span data-stu-id="150de-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="150de-177">tooperform essa opção, execute Olá código a seguir `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="150de-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="150de-178">Configurar MySQL</span><span class="sxs-lookup"><span data-stu-id="150de-178">Set up MySQL</span></span>
<span data-ttu-id="150de-179">Agora você está pronto tooinstall MySQL em `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="150de-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="150de-180">Você tem duas opções para `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="150de-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="150de-181">Você pode instalar o mysql-servidor, o que criará /var/lib/mysql, preencha-o com um novo diretório de dados e, em seguida, remover o conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="150de-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="150de-182">tooperform essa opção, execute Olá código a seguir `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="150de-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="150de-183">Olá segunda opção é toofailover muito`hadb02` e, em seguida, instalar o servidor mysql existe.</span><span class="sxs-lookup"><span data-stu-id="150de-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="150de-184">Scripts de instalação vai notar a instalação existente do hello e não toque nele.</span><span class="sxs-lookup"><span data-stu-id="150de-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="150de-185">Execução hello seguinte código em `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="150de-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="150de-186">Execução hello seguinte código em `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="150de-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="150de-187">Se você não planeja toofailover DRBD agora, Olá primeira opção é mais fácil, embora indiscutivelmente menos elegante.</span><span class="sxs-lookup"><span data-stu-id="150de-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="150de-188">Depois de configurá-lo, você pode começar a trabalhar no banco de dados do MySQL.</span><span class="sxs-lookup"><span data-stu-id="150de-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="150de-189">Execução hello seguinte código em `hadb02` (ou qualquer um dos servidores de saudação está ativo, de acordo com o tooDRBD):</span><span class="sxs-lookup"><span data-stu-id="150de-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="150de-190">Esta última instrução efetivamente desabilita a autenticação para o usuário raiz de saudação nesta tabela.</span><span class="sxs-lookup"><span data-stu-id="150de-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="150de-191">Ela deve ser substituída pelas instruções GRANT de nível de produção e só é incluída para fins de ilustração.</span><span class="sxs-lookup"><span data-stu-id="150de-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="150de-192">Se você deseja que as consultas de toomake de VMs Olá externa (que é a finalidade deste guia Olá), também será preciso tooenable de rede para MySQL.</span><span class="sxs-lookup"><span data-stu-id="150de-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="150de-193">Em ambas as VMs, abra `/etc/mysql/my.cnf` e vá muito`bind-address`.</span><span class="sxs-lookup"><span data-stu-id="150de-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="150de-194">Alterar o endereço de saudação de 127.0.0.1 too0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="150de-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="150de-195">Depois de salvar o arquivo hello, emitir um `sudo service mysql restart` no principal atual.</span><span class="sxs-lookup"><span data-stu-id="150de-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="150de-196">Criar conjunto de balanceamento de carga do hello MySQL</span><span class="sxs-lookup"><span data-stu-id="150de-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="150de-197">Voltar toohello portal, vá muito`hadb01`e escolha **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="150de-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="150de-198">toocreate um ponto de extremidade, escolha MySQL (TCP 3306) na lista suspensa de saudação e selecione **conjunto com balanceamento de carga novo criar**.</span><span class="sxs-lookup"><span data-stu-id="150de-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="150de-199">Nome hello ponto de extremidade com balanceamento de carga `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="150de-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="150de-200">Definir **tempo** too5 segundos, mínimo.</span><span class="sxs-lookup"><span data-stu-id="150de-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="150de-201">Depois de criar o ponto de extremidade hello, ir muito`hadb02`, escolha **pontos de extremidade**e criar um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="150de-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="150de-202">Escolha `lb-mysql`e selecione MySQL na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="150de-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="150de-203">Você também pode usar o hello CLI do Azure para esta etapa.</span><span class="sxs-lookup"><span data-stu-id="150de-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="150de-204">Agora você tem tudo o que é necessário para uma operação manual do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="150de-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="150de-205">Olá conjunto de balanceamento de carga de teste</span><span class="sxs-lookup"><span data-stu-id="150de-205">Test hello load-balanced set</span></span>
<span data-ttu-id="150de-206">É possível executar testes de um computador externo usando qualquer cliente do MySQL ou por meio de determinados aplicativos, como phpMyAdmin em execução como um site do Azure.</span><span class="sxs-lookup"><span data-stu-id="150de-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="150de-207">Nesse caso, você usou a ferramenta de linha de comando do MySQL em outra caixa do Linux:</span><span class="sxs-lookup"><span data-stu-id="150de-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="150de-208">Executando failover manualmente</span><span class="sxs-lookup"><span data-stu-id="150de-208">Manually failing over</span></span>
<span data-ttu-id="150de-209">Você pode simular failovers desativando o MySQL, alternando o primário do DRBD e reiniciando o MySQL.</span><span class="sxs-lookup"><span data-stu-id="150de-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="150de-210">tooperform nesta tarefa, execute Olá código a seguir em hadb01:</span><span class="sxs-lookup"><span data-stu-id="150de-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="150de-211">Em seguida, em hadb02:</span><span class="sxs-lookup"><span data-stu-id="150de-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="150de-212">Depois de executar failover manualmente, você poderá repetir a consulta remota e ela deverá funcionar perfeitamente.</span><span class="sxs-lookup"><span data-stu-id="150de-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="150de-213">Configurar Corosync</span><span class="sxs-lookup"><span data-stu-id="150de-213">Set up Corosync</span></span>
<span data-ttu-id="150de-214">Corosync é infraestrutura de cluster subjacente Olá necessária para Pacemaker toowork.</span><span class="sxs-lookup"><span data-stu-id="150de-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="150de-215">De pulsação (e outras metodologias como Ultramonkey), Corosync é uma divisão de funcionalidades CRM hello, enquanto Pacemaker permanece tooHeartbeat mais semelhante na funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="150de-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="150de-216">Olá principal restrição para Corosync no Azure é que Corosync prefere multicast transmissão em unicast comunicações, mas o sistema de rede do Microsoft Azure somente dá suporte a unicast.</span><span class="sxs-lookup"><span data-stu-id="150de-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="150de-217">Felizmente, o Corosync tem um modo unicast funcional.</span><span class="sxs-lookup"><span data-stu-id="150de-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="150de-218">Olá única restrição real é que, como todos os nós não estão se comunicando entre si, é necessário nós de saudação toodefine nos arquivos de configuração, incluindo seus endereços IP.</span><span class="sxs-lookup"><span data-stu-id="150de-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="150de-219">Podemos usar arquivos de exemplo hello Corosync para Unicast e alteração de associar o endereço, listas de nó e os diretórios de log (Ubuntu usa `/var/log/corosync` enquanto o uso de arquivos de exemplo hello `/var/log/cluster`) e habilitar as ferramentas de quorum.</span><span class="sxs-lookup"><span data-stu-id="150de-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="150de-220">Use os seguintes Olá `transport: udpu` diretiva e hello definidas manualmente os endereços IP para ambos os nós.</span><span class="sxs-lookup"><span data-stu-id="150de-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="150de-221">Execução hello seguinte código em `/etc/corosync/corosync.conf` para ambos os nós:</span><span class="sxs-lookup"><span data-stu-id="150de-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="150de-222">Copie esse arquivo de configuração em ambas as VMs e inicie o Corosync em ambos os nós:</span><span class="sxs-lookup"><span data-stu-id="150de-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="150de-223">Logo depois de iniciar o serviço hello, cluster Olá deve ser estabelecido em anel atual hello e quorum deve ser constituído.</span><span class="sxs-lookup"><span data-stu-id="150de-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="150de-224">Podemos verificar essa funcionalidade por revisar os logs ou executando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="150de-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="150de-225">Você verá a saída toohello semelhante imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="150de-225">You will see output similar toohello following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="150de-227">Configurando o Pacemaker</span><span class="sxs-lookup"><span data-stu-id="150de-227">Set up Pacemaker</span></span>
<span data-ttu-id="150de-228">Usa pacemaker Olá toomonitor de cluster para recursos, define quando atingem primárias e alterna toosecondaries esses recursos.</span><span class="sxs-lookup"><span data-stu-id="150de-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="150de-229">Os recursos podem ser definidos com base em um conjunto de scripts disponíveis ou de scripts LSB (init-like), entre outras opções.</span><span class="sxs-lookup"><span data-stu-id="150de-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="150de-230">Queremos Pacemaker muito "próprios" hello DRBD recurso, o ponto de montagem Olá e serviço do MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="150de-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="150de-231">Se Pacemaker pode ativar e desativar DRBD, montar e desmontar e, em seguida, iniciar e parar o MySQL no hello direita ordem quando algo ruim acontece com hello primário, a instalação for concluída.</span><span class="sxs-lookup"><span data-stu-id="150de-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="150de-232">Ao instalar o Pacemaker pela primeira vez, a configuração deve ser bem simples, algo como:</span><span class="sxs-lookup"><span data-stu-id="150de-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="150de-233">Verifique a configuração de saudação executando `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="150de-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="150de-234">Em seguida, crie um arquivo (como `/tmp/cluster.conf`) com hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="150de-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="150de-235">Carregar arquivo de saudação em configuração hello.</span><span class="sxs-lookup"><span data-stu-id="150de-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="150de-236">Você só precisa toodo isso em um nó.</span><span class="sxs-lookup"><span data-stu-id="150de-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="150de-237">Verifique se o Pacemaker é iniciado durante a inicialização em ambos os nós:</span><span class="sxs-lookup"><span data-stu-id="150de-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="150de-238">Usando `sudo crm_mon –L`, verifique se um dos seus nós tornou mestre Olá para cluster hello e está executando todos os recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="150de-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="150de-239">Você pode usar a montagem e ps toocheck recursos Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="150de-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="150de-240">Olá captura de tela mostra a seguir `crm_mon` com um nó interrompido (saída selecionando Ctrl + C):</span><span class="sxs-lookup"><span data-stu-id="150de-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="150de-242">Essa captura de tela mostra ambos os nós, um mestre e um subordinado:</span><span class="sxs-lookup"><span data-stu-id="150de-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="150de-244">Testando</span><span class="sxs-lookup"><span data-stu-id="150de-244">Testing</span></span>
<span data-ttu-id="150de-245">Você está pronto para uma simulação de failover automático.</span><span class="sxs-lookup"><span data-stu-id="150de-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="150de-246">Há dois toodo de maneiras isso: flexíveis e rígidos.</span><span class="sxs-lookup"><span data-stu-id="150de-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="150de-247">maneira flexível Hello usa função de desligamento do cluster Olá: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="150de-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="150de-248">Se você usar isso no mestre hello, escravo Olá assume.</span><span class="sxs-lookup"><span data-stu-id="150de-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="150de-249">Lembre-se de tooset este toooff voltar.</span><span class="sxs-lookup"><span data-stu-id="150de-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="150de-250">Caso contrário, o crm_mon mostrará um nó em espera.</span><span class="sxs-lookup"><span data-stu-id="150de-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="150de-251">Olá arduamente está sendo pressionada Olá VM primária (hadb01) por meio do portal de saudação ou alterando Olá runlevel em Olá VM (ou seja, interromper, desligamento).</span><span class="sxs-lookup"><span data-stu-id="150de-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="150de-252">Isso ajuda a Corosync e Pacemaker por sinalização contínuo desse mestre Olá para baixo.</span><span class="sxs-lookup"><span data-stu-id="150de-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="150de-253">Você pode testar isso (útil para as janelas de manutenção), mas você também pode forçar o cenário de saudação congelando Olá VM.</span><span class="sxs-lookup"><span data-stu-id="150de-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="150de-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="150de-254">STONITH</span></span>
<span data-ttu-id="150de-255">Ele deve ser possível tooissue um desligamento da VM por meio de saudação CLI do Azure em vez de um script STONITH que controla um dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="150de-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="150de-256">Você pode usar `/usr/lib/stonith/plugins/external/ssh` como uma base e habilitar STONITH na configuração do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="150de-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="150de-257">CLI do Azure deve ser instalado globalmente e configurações de publicação hello e perfil deve ser carregado para o usuário de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="150de-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="150de-258">Exemplo de código para o recurso de saudação está disponível em [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="150de-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="150de-259">Alterar configuração do cluster Olá adicionando Olá muito a seguir`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="150de-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="150de-260">script Hello não executa verificações para cima/para baixo.</span><span class="sxs-lookup"><span data-stu-id="150de-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="150de-261">Olá original SSH apresentava 15 verificações de ping, mas o tempo de recuperação para uma VM do Azure pode ser mais variáveis.</span><span class="sxs-lookup"><span data-stu-id="150de-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="150de-262">Limitações</span><span class="sxs-lookup"><span data-stu-id="150de-262">Limitations</span></span>
<span data-ttu-id="150de-263">Olá seguintes limitações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="150de-263">hello following limitations apply:</span></span>

* <span data-ttu-id="150de-264">Olá script de recurso DRBD linbit que gerencia DRBD como um recurso usa Pacemaker `drbdadm down` ao desligar um nó, mesmo se o nó de saudação será apenas no modo de espera.</span><span class="sxs-lookup"><span data-stu-id="150de-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="150de-265">Isso não é ideal porque subordinado Olá não sincronizará recursos DRBD Olá enquanto mestre Olá obtém gravações.</span><span class="sxs-lookup"><span data-stu-id="150de-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="150de-266">Se o mestre de saudação não falhar generosamente, escravo Olá pode assumir um estado de sistema de arquivos mais antigo.</span><span class="sxs-lookup"><span data-stu-id="150de-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="150de-267">Existem duas maneiras em potencial de resolver isso:</span><span class="sxs-lookup"><span data-stu-id="150de-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="150de-268">Impor um `drbdadm up r0` a todos os nós de cluster por meio de um watchdog local (não clusterizado)</span><span class="sxs-lookup"><span data-stu-id="150de-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="150de-269">Editar script DRBD linbit hello, certificando-se de que `down` não for chamado no`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="150de-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="150de-270">Balanceador de carga de saudação precisa toorespond de pelo menos cinco segundos, para que os aplicativos devem estar ciente do cluster e aumentar a tolerância de tempo limite.</span><span class="sxs-lookup"><span data-stu-id="150de-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="150de-271">Outras arquiteturas, como filas no aplicativo e middleware de consulta também podem ajudar.</span><span class="sxs-lookup"><span data-stu-id="150de-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="150de-272">Ajuste do MySQL é necessário tooensure escrita feita em um ritmo gerenciável e caches são liberado toodisk com tanta frequência como toominimize possíveis perdas de memória.</span><span class="sxs-lookup"><span data-stu-id="150de-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="150de-273">Desempenho de gravação é dependente na VM interconexão no comutador virtual Olá porque esse é o mecanismo de saudação usado por DRBD tooreplicate Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="150de-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
