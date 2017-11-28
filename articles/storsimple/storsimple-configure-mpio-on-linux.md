---
title: aaaConfigure MPIO no host StorSimple Linux | Microsoft Docs
description: Configurar o MPIO no host do Linux tooa StorSimple conectado executando CentOS 6.6
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="98110-103">Configurar o MPIO em um host do StorSimple executando o CentOS</span><span class="sxs-lookup"><span data-stu-id="98110-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="98110-104">Este artigo explica tooconfigure necessário de etapas de saudação e/s de múltiplos caminhos (MPIO) no servidor host Centos 6.6.</span><span class="sxs-lookup"><span data-stu-id="98110-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="98110-105">servidor de host de saudação é o dispositivo do Microsoft Azure StorSimple tooyour conectado para alta disponibilidade por meio de iniciadores iSCSI.</span><span class="sxs-lookup"><span data-stu-id="98110-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="98110-106">Ele descreve em detalhes Olá a descoberta automática de dispositivos multipath e configuração específica de saudação apenas para os volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="98110-107">Esse procedimento é aplicável tooall modelos de saudação de dispositivos da série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="98110-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="98110-108">Este procedimento não pode ser usado para um dispositivo virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="98110-109">Para obter mais informações, consulte como tooconfigure hospedar servidores para seu dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="98110-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="98110-110">Sobre vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-110">About multipathing</span></span>
<span data-ttu-id="98110-111">o recurso de vários caminhos Olá permite que você tooconfigure vários caminhos de e/s entre um servidor host e um dispositivo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="98110-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="98110-112">Esses caminhos de E/S são conexões físicas da SAN que podem incluir cabos, switches, interfaces de rede e controladores separados.</span><span class="sxs-lookup"><span data-stu-id="98110-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="98110-113">Múltiplos caminhos agrega caminhos de e/s hello, tooconfigure um novo dispositivo que está associado a todos os caminhos de saudação agregado.</span><span class="sxs-lookup"><span data-stu-id="98110-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="98110-114">Olá finalidade múltiplos caminhos é dupla:</span><span class="sxs-lookup"><span data-stu-id="98110-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="98110-115">**Alta disponibilidade**: ele fornece um caminho alternativo, se falhar de qualquer elemento de caminho hello e/s (por exemplo, um cabo, switch, interface de rede ou controlador).</span><span class="sxs-lookup"><span data-stu-id="98110-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="98110-116">**O balanceamento de carga**: dependendo da configuração de saudação do seu dispositivo de armazenamento, ela pode melhorar o desempenho de saudação detectando cargas em caminhos de e/s de saudação e rebalanceamento dinamicamente as cargas.</span><span class="sxs-lookup"><span data-stu-id="98110-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="98110-117">Sobre componentes de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-117">About multipathing components</span></span>
<span data-ttu-id="98110-118">Vários caminhos em Linux consiste em componentes de kernel e em componentes de espaço do usuário como mostrados na tabela abaixo.</span><span class="sxs-lookup"><span data-stu-id="98110-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="98110-119">**Kernel**: Olá principal componente é Olá *mapeador de dispositivo* que redireciona a e/s e oferece suporte a failover de caminhos e grupos de caminho.</span><span class="sxs-lookup"><span data-stu-id="98110-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="98110-120">**Espaço do usuário**: esses são *ferramentas multipath* que gerenciar dispositivos Multipath instruindo o módulo de vários caminhos de mapeador de dispositivo de saudação que toodo.</span><span class="sxs-lookup"><span data-stu-id="98110-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="98110-121">ferramentas de saudação consistem em:</span><span class="sxs-lookup"><span data-stu-id="98110-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="98110-122">**Multipath**: lista e configura os dispositivos de vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="98110-123">**Vários caminhos**: daemon que executa os caminhos de saudação multipath e monitores.</span><span class="sxs-lookup"><span data-stu-id="98110-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="98110-124">**Nome do Devmap**: fornece um tooudev significativa do nome do dispositivo para devmaps.</span><span class="sxs-lookup"><span data-stu-id="98110-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="98110-125">**Kpartx**: mapeia linear devmaps toodevice partições toomake multipath particionável.</span><span class="sxs-lookup"><span data-stu-id="98110-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="98110-126">**Multipath**: arquivo de configuração do daemon de vários caminhos que é usado toooverwrite Olá configuração interna tabela.</span><span class="sxs-lookup"><span data-stu-id="98110-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="98110-127">Sobre o arquivo de configuração do Multipath Olá</span><span class="sxs-lookup"><span data-stu-id="98110-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="98110-128">arquivo de configuração de saudação `/etc/multipath.conf` faz muitas Olá recursos de múltiplos caminhos configurável pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="98110-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="98110-129">Olá `multipath` daemon kernel de comando e hello `multipathd` usar as informações encontradas neste arquivo.</span><span class="sxs-lookup"><span data-stu-id="98110-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="98110-130">arquivo Hello é consultado somente durante a configuração de saudação de dispositivos multipath hello.</span><span class="sxs-lookup"><span data-stu-id="98110-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="98110-131">Certifique-se de que todas as alterações são feitas antes de executar Olá `multipath` comando.</span><span class="sxs-lookup"><span data-stu-id="98110-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="98110-132">Se você modificar o arquivo hello posteriormente, será necessário toostop e iniciar vários caminhos novamente para Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="98110-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="98110-133">Olá Multipath tem cinco seções:</span><span class="sxs-lookup"><span data-stu-id="98110-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="98110-134">**System level defaults** *(defaults)*: você pode substituir os padrões no nível do sistema.</span><span class="sxs-lookup"><span data-stu-id="98110-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="98110-135">**Na lista negra dispositivos** *(lista de bloqueios)*: você pode especificar a lista de saudação de dispositivos que não devem ser controladas pelo mapeador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="98110-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="98110-136">**Lista negra exceções** *(blacklist_exceptions)*: você pode identificar dispositivos específicos toobe tratado como dispositivos de multipath mesmo se listadas na lista de bloqueios de saudação.</span><span class="sxs-lookup"><span data-stu-id="98110-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="98110-137">**As configurações específicas de controlador de armazenamento** *(dispositivos)*: você pode especificar as configurações que serão aplicadas toodevices que possuem informações de fornecedor e do produto.</span><span class="sxs-lookup"><span data-stu-id="98110-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="98110-138">**As configurações específicas de dispositivo** *(os multicaminhos)*: você pode usar as definições de configuração Esta seção toofine ajustar Olá para LUNs individuais.</span><span class="sxs-lookup"><span data-stu-id="98110-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="98110-139">Configurar vários caminhos no host do StorSimple tooLinux conectado</span><span class="sxs-lookup"><span data-stu-id="98110-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="98110-140">Um host Linux do StorSimple dispositivo conectado tooa pode ser configurado para alta disponibilidade e balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="98110-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="98110-141">Por exemplo, se o host do Linux Olá tem duas interfaces de dispositivo de SAN e hello toohello conectado tem duas interfaces conectadas toohello SAN, de modo que essas interfaces são na mesma sub-rede de hello e, em seguida, haverá 4 caminhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="98110-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="98110-142">No entanto, se cada interface de dados na interface de dispositivo e host Olá está em uma sub-rede IP diferente (e não pode ser roteado), somente 2 caminhos estará disponíveis.</span><span class="sxs-lookup"><span data-stu-id="98110-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="98110-143">Você pode configurar vários caminhos tooautomatically descobrir todos os caminhos disponíveis do hello, escolher um algoritmo de balanceamento de carga para esses caminhos, aplique as configurações específicas para volumes de StorSimple e, em seguida, habilitar e verifique se vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="98110-144">Olá procedimento a seguir descreve como vários caminhos de tooconfigure quando um dispositivo StorSimple com duas interfaces de rede é conectado tooa host com duas interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="98110-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98110-145">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="98110-145">Prerequisites</span></span>
<span data-ttu-id="98110-146">Esta seção fornece detalhes sobre os pré-requisitos de configuração Olá para servidor CentOS e seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="98110-147">No host CentOS</span><span class="sxs-lookup"><span data-stu-id="98110-147">On CentOS host</span></span>
1. <span data-ttu-id="98110-148">Certifique-se de que seu host CentOS tenha duas interfaces de rede habilitadas.</span><span class="sxs-lookup"><span data-stu-id="98110-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="98110-149">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="98110-150">Olá exemplo a seguir mostra a saída de hello quando duas interfaces de rede (`eth0` e `eth1`) estão presentes no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="98110-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="98110-151">Instale *iSCSI-initiator-utils* em seu servidor CentOS.</span><span class="sxs-lookup"><span data-stu-id="98110-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="98110-152">Executar Olá seguindo as etapas tooinstall *utilitários de iniciador de iSCSI*.</span><span class="sxs-lookup"><span data-stu-id="98110-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="98110-153">Faça logon como `root` em seu host CentOS.</span><span class="sxs-lookup"><span data-stu-id="98110-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="98110-154">Instalar Olá *utilitários de iniciador de iSCSI*.</span><span class="sxs-lookup"><span data-stu-id="98110-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="98110-155">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="98110-156">Depois de saudação *utilitários de iniciador de iSCSI* com êxito é instalado, inicie o serviço iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="98110-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="98110-157">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="98110-158">Em ocasiões, `iscsid` , na verdade, não pode iniciar e Olá `--force` opção pode ser necessária</span><span class="sxs-lookup"><span data-stu-id="98110-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="98110-159">tooensure que o iniciador iSCSI está habilitado no momento da inicialização, use Olá `chkconfig` tooenable serviço de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="98110-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="98110-160">tooverify que ele foi corretamente de instalação, execute o comando de saudação:</span><span class="sxs-lookup"><span data-stu-id="98110-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="98110-161">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="98110-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="98110-162">Olá, o exemplo acima, você pode ver que seu ambiente iSCSI seja executado no tempo de inicialização em níveis de execução 2, 3, 4 e 5.</span><span class="sxs-lookup"><span data-stu-id="98110-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="98110-163">Instale o *device-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="98110-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="98110-164">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="98110-165">Olá instalação será iniciada.</span><span class="sxs-lookup"><span data-stu-id="98110-165">hello installation will start.</span></span> <span data-ttu-id="98110-166">Tipo **Y** toocontinue quando for solicitada a confirmação.</span><span class="sxs-lookup"><span data-stu-id="98110-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="98110-167">No dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="98110-167">On StorSimple device</span></span>
<span data-ttu-id="98110-168">O dispositivo StorSimple deve ter:</span><span class="sxs-lookup"><span data-stu-id="98110-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="98110-169">No mínimo duas interfaces habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="98110-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="98110-170">tooverify que duas interfaces estão habilitadas para iSCSI no seu dispositivo StorSimple, execute Olá Olá portal clássico do Azure para seu dispositivo StorSimple etapas:</span><span class="sxs-lookup"><span data-stu-id="98110-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="98110-171">Faça logon no portal clássico do Olá para seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="98110-172">Selecione seu serviço StorSimple Manager, clique em **dispositivos** e escolha o dispositivo StorSimple específico de saudação.</span><span class="sxs-lookup"><span data-stu-id="98110-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="98110-173">Clique em **configurar** e verifique se as configurações de interface de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="98110-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="98110-174">Uma captura de tela com duas interfaces de rede habilitadas para iSCSI é mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="98110-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="98110-175">Aqui, DATA 2 e DATA 3, ambas as interfaces 10 GbE estão habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="98110-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Configuração de DATA 2 do StorsSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configuração de DATA 3 do StorsSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="98110-178">Em Olá **configurar** página</span><span class="sxs-lookup"><span data-stu-id="98110-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="98110-179">Verifique se ambas as interfaces de rede estão habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="98110-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="98110-180">Olá **iSCSI habilitado** campo deve ser definido muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="98110-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="98110-181">Verifique se as interfaces de rede de saudação têm Olá mesma velocidade, deve ser 1 GbE ou 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="98110-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="98110-182">Observe os endereços de saudação IPv4 de interfaces habilitadas para iSCSI do hello e salve para uso posterior no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="98110-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="98110-183">interfaces de iSCSI Olá em seu dispositivo StorSimple devem ser acessíveis a partir do servidor de CentOS hello.</span><span class="sxs-lookup"><span data-stu-id="98110-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="98110-184">tooverify isso, você precisa tooprovide endereços IP hello das suas interfaces de rede habilitada para iSCSI do StorSimple em seu servidor de host.</span><span class="sxs-lookup"><span data-stu-id="98110-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="98110-185">Olá comandos usados e Olá saída correspondente com DATA2 (10.126.162.25) e DATA3 (10.126.162.26) é mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="98110-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="98110-186">Configuração de hardware</span><span class="sxs-lookup"><span data-stu-id="98110-186">Hardware configuration</span></span>
<span data-ttu-id="98110-187">É recomendável que você se conecte a saudação duas iSCSI interfaces de rede em caminhos separados para redundância.</span><span class="sxs-lookup"><span data-stu-id="98110-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="98110-188">Olá figura a seguir mostra a configuração de hardware recomendada Olá para alta disponibilidade e balanceamento de carga de criação de vários caminhos para seu servidor CentOS e o dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Configuração de hardware do MPIO para StorSimple tooLinux host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="98110-190">Conforme mostrado na saudação anterior Figura:</span><span class="sxs-lookup"><span data-stu-id="98110-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="98110-191">O dispositivo StorSimple está em uma configuração ativo-passivo com dois controladores.</span><span class="sxs-lookup"><span data-stu-id="98110-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="98110-192">Duas opções de SAN são controladores de dispositivo tooyour conectado.</span><span class="sxs-lookup"><span data-stu-id="98110-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="98110-193">Dois iniciadores iSCSI estão habilitados no seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="98110-194">Duas interfaces de rede estão habilitadas em seu host CentOS.</span><span class="sxs-lookup"><span data-stu-id="98110-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="98110-195">Olá acima configuração produzirá 4 caminhos separados entre o host de dispositivo e hello se interfaces Olá de host e os dados são roteáveis.</span><span class="sxs-lookup"><span data-stu-id="98110-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="98110-196">É recomendável que você não misture as interfaces de rede de 1 GbE e de 10 GbE para vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="98110-197">Ao usar duas interfaces de rede, ambas as interfaces Olá devem ser Olá mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="98110-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="98110-198">Em seu dispositivo StorSimple, DATA0, DATA1, DATA4 e DATA5 são interfaces de 1 GbE, enquanto DATA2 e DATA3 são interfaces de rede de 10 GbE.|</span><span class="sxs-lookup"><span data-stu-id="98110-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="98110-199">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="98110-199">Configuration steps</span></span>
<span data-ttu-id="98110-200">etapas de configuração de saudação para múltiplos caminhos envolvem configurar caminhos de saudação disponíveis para descoberta automática, especificando Olá balanceamento de carga de algoritmo toouse, habilitar vários caminhos e, finalmente, verificando a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="98110-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="98110-201">Cada uma dessas etapas é discutida em detalhes nas seções a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="98110-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="98110-202">Etapa 1: Configurar vários caminhos para a descoberta automática</span><span class="sxs-lookup"><span data-stu-id="98110-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="98110-203">dispositivos com suporte de vários caminhos de saudação podem ser descobertos e configurados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="98110-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="98110-204">Inicialize o arquivo `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="98110-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="98110-205">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="98110-206">Olá acima comando criará uma `sample/etc/multipath.conf` arquivo.</span><span class="sxs-lookup"><span data-stu-id="98110-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="98110-207">Inicie o serviço de vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-207">Start multipath service.</span></span> <span data-ttu-id="98110-208">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="98110-209">Você verá Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="98110-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="98110-210">Habilite a descoberta automática dos vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="98110-211">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="98110-212">Isto irá modificar a seção de padrões de saudação do seu `multipath.conf` conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="98110-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="98110-213">Etapa 2: Configurar vários caminhos para volumes StorSimple</span><span class="sxs-lookup"><span data-stu-id="98110-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="98110-214">Por padrão, todos os dispositivos são pretos listados no arquivo de Multipath hello e serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="98110-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="98110-215">Você precisará toocreate de lista de bloqueios exceções tooallow vários caminhos para os volumes de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="98110-216">Editar saudação `/etc/mulitpath.conf` arquivo.</span><span class="sxs-lookup"><span data-stu-id="98110-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="98110-217">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="98110-218">Localize a seção de blacklist_exceptions de saudação no arquivo de Multipath hello.</span><span class="sxs-lookup"><span data-stu-id="98110-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="98110-219">Seu dispositivo StorSimple precisa toobe listada como uma exceção de lista de bloqueios nesta seção.</span><span class="sxs-lookup"><span data-stu-id="98110-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="98110-220">Você pode remover o comentário relevantes linhas toomodify esse arquivo-lo conforme mostrado a seguir (use somente Olá modelo específico de dispositivo Olá que você está usando):</span><span class="sxs-lookup"><span data-stu-id="98110-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="98110-221">Etapa 3: Configurar vários caminhos de round robin</span><span class="sxs-lookup"><span data-stu-id="98110-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="98110-222">Esse algoritmo de balanceamento de carga usa todos os controlador de active de toohello multipaths disponível de saudação de forma equilibrada, round-robin.</span><span class="sxs-lookup"><span data-stu-id="98110-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="98110-223">Editar saudação `/etc/multipath.conf` arquivo.</span><span class="sxs-lookup"><span data-stu-id="98110-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="98110-224">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="98110-225">Em Olá `defaults` seção, Olá conjunto `path_grouping_policy` muito`multibus`.</span><span class="sxs-lookup"><span data-stu-id="98110-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="98110-226">Olá `path_grouping_policy` Especifica saudação padrão caminho agrupamento política tooapply toounspecified os multicaminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="98110-227">seção de padrões de saudação procurará conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="98110-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="98110-228">Olá valores mais comuns de `path_grouping_policy` incluem:</span><span class="sxs-lookup"><span data-stu-id="98110-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="98110-229">failover = um caminho por grupo de prioridade</span><span class="sxs-lookup"><span data-stu-id="98110-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="98110-230">multibus = todos os caminhos válidos em um grupo de prioridade</span><span class="sxs-lookup"><span data-stu-id="98110-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="98110-231">Etapa 4: Habilitar vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="98110-232">Reiniciar Olá `multipathd` daemon.</span><span class="sxs-lookup"><span data-stu-id="98110-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="98110-233">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="98110-234">saída de Hello será conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="98110-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="98110-235">Etapa 5: Verificar vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="98110-236">Primeiro, certifique-se de que é estabelecida com o dispositivo StorSimple Olá conexão iSCSI da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="98110-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="98110-237">a.</span><span class="sxs-lookup"><span data-stu-id="98110-237">a.</span></span> <span data-ttu-id="98110-238">Descubra seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-238">Discover your StorSimple device.</span></span> <span data-ttu-id="98110-239">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="98110-240">saída de Hello quando o endereço IP DATA0 é 10.126.162.25 e porta 3260 seja aberta no dispositivo do StorSimple Olá para tráfego iSCSI saída é conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="98110-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="98110-241">Saudação de cópia IQN do seu dispositivo StorSimple, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, da saudação anterior de saída.</span><span class="sxs-lookup"><span data-stu-id="98110-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="98110-242">b.</span><span class="sxs-lookup"><span data-stu-id="98110-242">b.</span></span> <span data-ttu-id="98110-243">Conecte o dispositivo de toohello usando o IQN de destino.</span><span class="sxs-lookup"><span data-stu-id="98110-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="98110-244">o dispositivo StorSimple Olá é destino de iSCSI Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="98110-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="98110-245">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="98110-246">Olá exemplo a seguir mostra a saída com um IQN de destino de `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="98110-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="98110-247">saída de Hello indica que você conectou com êxito toohello duas interfaces de rede habilitada para iSCSI em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="98110-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="98110-248">Se você vir a interface de apenas um host e dois caminhos aqui, em seguida, você precisa tooenable ambas as interfaces Olá no host para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="98110-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="98110-249">Você pode seguir Olá [instruções na documentação do Linux detalhadas](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="98110-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="98110-250">Um volume é o servidor de CentOS de toohello exposto do dispositivo do StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="98110-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="98110-251">Para obter mais informações, consulte [etapa 6: criar um volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via Olá portal clássico do Azure no seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="98110-252">Verifique se os caminhos disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="98110-252">Verify hello available paths.</span></span> <span data-ttu-id="98110-253">Tipo:</span><span class="sxs-lookup"><span data-stu-id="98110-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="98110-254">saudação de exemplo a seguir mostra a saída de saudação de duas interfaces de rede em uma interface de rede de host único do StorSimple dispositivo tooa conectado com dois caminhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="98110-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="98110-255">Solucionar problemas de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="98110-256">Esta seção fornece algumas dicas úteis se você tiver algum problema durante a configuração de vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="98110-257">P.</span><span class="sxs-lookup"><span data-stu-id="98110-257">Q.</span></span> <span data-ttu-id="98110-258">Não vejo as alterações de saudação em `multipath.conf` arquivo entrar em vigor.</span><span class="sxs-lookup"><span data-stu-id="98110-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="98110-259">R.</span><span class="sxs-lookup"><span data-stu-id="98110-259">A.</span></span> <span data-ttu-id="98110-260">Se você tiver feito qualquer toohello alterações `multipath.conf` arquivo, você precisará de serviço de múltiplos caminhos Olá toorestart.</span><span class="sxs-lookup"><span data-stu-id="98110-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="98110-261">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="98110-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="98110-262">P.</span><span class="sxs-lookup"><span data-stu-id="98110-262">Q.</span></span> <span data-ttu-id="98110-263">Posso ter habilitado duas interfaces de rede no dispositivo do StorSimple hello e duas interfaces de rede no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="98110-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="98110-264">Quando eu lista caminhos disponíveis hello, vejo apenas dois caminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="98110-265">Esperado toosee quatro caminhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="98110-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="98110-266">R.</span><span class="sxs-lookup"><span data-stu-id="98110-266">A.</span></span> <span data-ttu-id="98110-267">Certifique-se de que os caminhos de saudação dois estão em Olá mesma sub-rede e roteável.</span><span class="sxs-lookup"><span data-stu-id="98110-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="98110-268">Se as interfaces de rede de saudação estiverem em diferentes vLANs e não pode ser roteado, você verá apenas dois caminhos.</span><span class="sxs-lookup"><span data-stu-id="98110-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="98110-269">Tooverify unidirecional trata toomake-se de que você possa acessar ambas as interfaces de host de saudação de uma interface de rede no dispositivo do StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="98110-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="98110-270">Você precisará de muito[entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) como essa verificação só pode ser feita por meio de uma sessão de suporte.</span><span class="sxs-lookup"><span data-stu-id="98110-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="98110-271">P.</span><span class="sxs-lookup"><span data-stu-id="98110-271">Q.</span></span> <span data-ttu-id="98110-272">Quando eu listo os caminhos disponíveis, não vejo nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="98110-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="98110-273">R.</span><span class="sxs-lookup"><span data-stu-id="98110-273">A.</span></span> <span data-ttu-id="98110-274">Normalmente, não consegue ver todos os caminhos Multipath indica um problema com o daemon de múltiplos caminhos hello e mais provável é que qualquer problema aqui está na saudação `multipath.conf` arquivo.</span><span class="sxs-lookup"><span data-stu-id="98110-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="98110-275">Também seria vale a pena verificar que você poderá ver alguns discos depois de conectar o destino toohello, como sem resposta das listagens de vários caminhos Olá também pode significar que não tem discos.</span><span class="sxs-lookup"><span data-stu-id="98110-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="98110-276">Use Olá barramento SCSI do comando toorescan Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="98110-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="98110-277">`$ rescan-scsi-bus.sh `(parte do pacote sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="98110-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="98110-278">Digite hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="98110-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="98110-279">Ou</span><span class="sxs-lookup"><span data-stu-id="98110-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="98110-280">Eles retornarão detalhes de discos adicionados recentemente.</span><span class="sxs-lookup"><span data-stu-id="98110-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="98110-281">toodetermine se for um disco de StorSimple, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="98110-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="98110-282">Isso retornará uma cadeia de caracteres, o que determinará se é um disco StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="98110-283">Uma causa menos provável, mas possível, também poderia ser um pid iscsid obsoleto.</span><span class="sxs-lookup"><span data-stu-id="98110-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="98110-284">Use Olá toolog de comando a seguir logoff das sessões de iSCSI hello:</span><span class="sxs-lookup"><span data-stu-id="98110-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="98110-285">Repita esse comando para todas as interfaces de rede Olá conectado no destino de iSCSI hello, que é seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98110-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="98110-286">Depois que você fez logoff de todas as sessões de iSCSI hello, use a sessão de iSCSI Olá de tooreestablish IQN de destino iSCSI de hello.</span><span class="sxs-lookup"><span data-stu-id="98110-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="98110-287">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="98110-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="98110-288">P.</span><span class="sxs-lookup"><span data-stu-id="98110-288">Q.</span></span> <span data-ttu-id="98110-289">Não sei se meu dispositivo está na lista branca.</span><span class="sxs-lookup"><span data-stu-id="98110-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="98110-290">R.</span><span class="sxs-lookup"><span data-stu-id="98110-290">A.</span></span> <span data-ttu-id="98110-291">tooverify se o dispositivo está na lista de permissões, use Olá comando interativo de solução de problemas a seguir:</span><span class="sxs-lookup"><span data-stu-id="98110-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="98110-292">Para obter mais informações, vá muito[usar um comando interativo para vários caminhos de solução de problemas](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="98110-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="98110-293">Lista de comandos úteis</span><span class="sxs-lookup"><span data-stu-id="98110-293">List of useful commands</span></span>
| <span data-ttu-id="98110-294">Digite </span><span class="sxs-lookup"><span data-stu-id="98110-294">Type</span></span> | <span data-ttu-id="98110-295">Command</span><span class="sxs-lookup"><span data-stu-id="98110-295">Command</span></span> | <span data-ttu-id="98110-296">Descrição</span><span class="sxs-lookup"><span data-stu-id="98110-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98110-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="98110-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="98110-298">Iniciar o serviço iSCSI</span><span class="sxs-lookup"><span data-stu-id="98110-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="98110-299">Parar o serviço iSCSI</span><span class="sxs-lookup"><span data-stu-id="98110-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="98110-300">Reiniciar o serviço iSCSI</span><span class="sxs-lookup"><span data-stu-id="98110-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="98110-301">Descobrir os destinos disponíveis no hello especificado endereço</span><span class="sxs-lookup"><span data-stu-id="98110-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="98110-302">Faça logon no destino de iSCSI toohello</span><span class="sxs-lookup"><span data-stu-id="98110-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="98110-303">Faça logoff do destino de iSCSI Olá</span><span class="sxs-lookup"><span data-stu-id="98110-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="98110-304">Imprimir o nome do iniciador iSCSI</span><span class="sxs-lookup"><span data-stu-id="98110-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="98110-305">Verificar Olá estado de sessão de iSCSI hello e volume descoberto no host de saudação</span><span class="sxs-lookup"><span data-stu-id="98110-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="98110-306">Mostra todas as sessões de iSCSI Olá estabelecidas entre o host de saudação e o dispositivo StorSimple Olá</span><span class="sxs-lookup"><span data-stu-id="98110-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="98110-307">**Múltiplos caminhos**</span><span class="sxs-lookup"><span data-stu-id="98110-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="98110-308">Iniciar o daemon de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="98110-309">Parar o daemon de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="98110-310">Reiniciar o daemon de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="98110-311">OU</span><span class="sxs-lookup"><span data-stu-id="98110-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="98110-312">Habilitar vários caminhos daemon toostart no momento da inicialização</span><span class="sxs-lookup"><span data-stu-id="98110-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="98110-313">Inicie o console interativo de saudação para solução de problemas</span><span class="sxs-lookup"><span data-stu-id="98110-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="98110-314">Listar as conexões e dispositivos de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="98110-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="98110-315">Criar um arquivo mulitpath.conf de exemplo `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="98110-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="98110-316">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98110-316">Next steps</span></span>
<span data-ttu-id="98110-317">Como você está configurando o MPIO no host do Linux, talvez seja necessário também toohello toorefer 6.6 CentoS documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="98110-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="98110-318">Configurando o MPIO no CentOS</span><span class="sxs-lookup"><span data-stu-id="98110-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="98110-319">Guia de treinamento do Linux</span><span class="sxs-lookup"><span data-stu-id="98110-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

