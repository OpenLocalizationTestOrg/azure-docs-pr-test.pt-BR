---
title: Configurar o MPIO em um host Linux do StorSimple | Microsoft Docs
description: Configurar o MPIO no StorSimple conectado a um host Linux que esteja executando o CentOS 6.6
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
ms.openlocfilehash: add539351066f9ff94febeebfd5334773b360e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="7d008-103">Configurar o MPIO em um host do StorSimple executando o CentOS</span><span class="sxs-lookup"><span data-stu-id="7d008-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="7d008-104">Este artigo explica as etapas necessárias para a configuração do Multipathing IO (MPIO) em seu servidor host do Centos 6.6.</span><span class="sxs-lookup"><span data-stu-id="7d008-104">This article explains the steps required to configure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="7d008-105">O servidor host está conectado ao dispositivo Microsoft Azure StorSimple para alta disponibilidade por meio de iniciadores iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7d008-105">The host server is connected to your Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="7d008-106">Ele descreve detalhadamente a descoberta automática de dispositivos de vários caminhos e a configuração específica somente para volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-106">It describes in detail the automatic discovery of multipath devices and the specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="7d008-107">Este procedimento é aplicável a todos os modelos de dispositivos da série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="7d008-107">This procedure is applicable to all the models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="7d008-108">Este procedimento não pode ser usado para um dispositivo virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="7d008-109">Para saber mais, veja como configurar servidores host para seu dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="7d008-109">For more information, see how to configure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="7d008-110">Sobre vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-110">About multipathing</span></span>
<span data-ttu-id="7d008-111">O recurso de vários caminhos permite configurar vários caminhos de E/S entre um servidor host e um dispositivo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7d008-111">The multipathing feature allows you to configure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="7d008-112">Esses caminhos de E/S são conexões físicas da SAN que podem incluir cabos, switches, interfaces de rede e controladores separados.</span><span class="sxs-lookup"><span data-stu-id="7d008-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="7d008-113">Vários caminhos agregam os caminhos de E/S para a configuração de um novo dispositivo associado a todos os caminhos agregados.</span><span class="sxs-lookup"><span data-stu-id="7d008-113">Multipathing aggregates the I/O paths, to configure a new device that is associated with all of the aggregated paths.</span></span>

<span data-ttu-id="7d008-114">A finalidade de vários caminhos é dupla:</span><span class="sxs-lookup"><span data-stu-id="7d008-114">The purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="7d008-115">**Alta disponibilidade**: oferece um caminho alternativo caso qualquer elemento do caminho de E/S (como um cabo, um switch, uma interface de rede ou um controlador) falhe.</span><span class="sxs-lookup"><span data-stu-id="7d008-115">**High availability**: It provides an alternate path if any element of the I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="7d008-116">**Balanceamento de carga**: dependendo da configuração do seu dispositivo de armazenamento, ela poderá melhorar o desempenho detectando cargas nos caminhos de E/S e rebalanceando dinamicamente essas cargas.</span><span class="sxs-lookup"><span data-stu-id="7d008-116">**Load balancing**: Depending on the configuration of your storage device, it can improve the performance by detecting loads on the I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="7d008-117">Sobre componentes de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-117">About multipathing components</span></span>
<span data-ttu-id="7d008-118">Vários caminhos em Linux consiste em componentes de kernel e em componentes de espaço do usuário como mostrados na tabela abaixo.</span><span class="sxs-lookup"><span data-stu-id="7d008-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="7d008-119">**Kernel**: o componente principal é o *device-mapper* , que redireciona a E/S e oferece suporte a failover de caminhos e de grupos de caminho.</span><span class="sxs-lookup"><span data-stu-id="7d008-119">**Kernel**: The main component is the *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="7d008-120">**User-space**: são *multipath-tools* que gerenciam dispositivos de vários caminhos instruindo o módulo device-mapper de vários caminhos o que fazer.</span><span class="sxs-lookup"><span data-stu-id="7d008-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing the device-mapper multipath module what to do.</span></span> <span data-ttu-id="7d008-121">As ferramentas consistem em:</span><span class="sxs-lookup"><span data-stu-id="7d008-121">The tools consist of:</span></span>
   
   * <span data-ttu-id="7d008-122">**Multipath**: lista e configura os dispositivos de vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="7d008-123">**Vários caminhos**: daemon que executa vários caminhos e monitora os caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-123">**Multipathd**: daemon that executes multipath and monitors the paths.</span></span>
   * <span data-ttu-id="7d008-124">**Devmap-name**: fornece um device-name significativo para udev para os devmaps.</span><span class="sxs-lookup"><span data-stu-id="7d008-124">**Devmap-name**: provides a meaningful device-name to udev for devmaps.</span></span>
   * <span data-ttu-id="7d008-125">**Kpartx**: mapeia devmaps lineares para partições de dispositivo para tornar os mapas de vários caminhos particionáveis.</span><span class="sxs-lookup"><span data-stu-id="7d008-125">**Kpartx**: maps linear devmaps to device partitions to make multipath maps partitionable.</span></span>
   * <span data-ttu-id="7d008-126">**Multipath.conf**: arquivo de configuração do daemon de vários caminhos, usado para substituir a tabela de configuração interna.</span><span class="sxs-lookup"><span data-stu-id="7d008-126">**Multipath.conf**: configuration file for multipath daemon that is used to overwrite the built-in configuration table.</span></span>

### <a name="about-the-multipathconf-configuration-file"></a><span data-ttu-id="7d008-127">Sobre o arquivo de configuração multipath.conf</span><span class="sxs-lookup"><span data-stu-id="7d008-127">About the multipath.conf configuration file</span></span>
<span data-ttu-id="7d008-128">O arquivo de configuração `/etc/multipath.conf` faz com que muitos dos recursos de vários caminhos possam ser configurados pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="7d008-128">The configuration file `/etc/multipath.conf` makes many of the multipathing features user-configurable.</span></span> <span data-ttu-id="7d008-129">O comando `multipath` e o daemon de kernel `multipathd` usam informações encontradas neste arquivo.</span><span class="sxs-lookup"><span data-stu-id="7d008-129">The `multipath` command and the kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="7d008-130">O arquivo só é consultado durante a configuração dos dispositivos de vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-130">The file is consulted only during the configuration of the multipath devices.</span></span> <span data-ttu-id="7d008-131">Certifique-se de que todas as alterações sejam feitas antes de executar o comando `multipath` .</span><span class="sxs-lookup"><span data-stu-id="7d008-131">Make sure that all changes are made before you run the `multipath` command.</span></span> <span data-ttu-id="7d008-132">Se você modificar o arquivo posteriormente, precisará parar e iniciar vários caminhos novamente para que as alterações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="7d008-132">If you modify the file afterwards, you will need to stop and start multipathd again for the changes to take effect.</span></span>

<span data-ttu-id="7d008-133">O arquivo multipath.conf tem cinco seções:</span><span class="sxs-lookup"><span data-stu-id="7d008-133">The multipath.conf has five sections:</span></span>

- <span data-ttu-id="7d008-134">**System level defaults** *(defaults)*: você pode substituir os padrões no nível do sistema.</span><span class="sxs-lookup"><span data-stu-id="7d008-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="7d008-135">**Blacklisted devices** *(blacklist)*: você pode especificar a lista de dispositivos que não devem ser controlados pelo device-mapper.</span><span class="sxs-lookup"><span data-stu-id="7d008-135">**Blacklisted devices** *(blacklist)*: You can specify the list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="7d008-136">**Blacklist exceptions** *(blacklist_exceptions)*: você pode identificar dispositivos específicos a serem tratados como dispositivos de vários caminhos, mesmo se relacionados na lista negra.</span><span class="sxs-lookup"><span data-stu-id="7d008-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices to be treated as multipath devices even if listed in the blacklist.</span></span>
- <span data-ttu-id="7d008-137">**Storage controller specific settings** *(devices)*: você pode especificar as definições de configuração que serão aplicadas a dispositivos com informações sobre o fornecedor e o produto.</span><span class="sxs-lookup"><span data-stu-id="7d008-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied to devices that have Vendor and Product information.</span></span>
- <span data-ttu-id="7d008-138">**Device specific settings** *(multipaths)*: você pode usar esta seção para ajustar as definições de configuração para LUNs individuais.</span><span class="sxs-lookup"><span data-stu-id="7d008-138">**Device specific settings** *(multipaths)*: You can use this section to fine-tune the configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-to-linux-host"></a><span data-ttu-id="7d008-139">Configurar vários caminhos no StorSimple conectado ao host Linux</span><span class="sxs-lookup"><span data-stu-id="7d008-139">Configure multipathing on StorSimple connected to Linux host</span></span>
<span data-ttu-id="7d008-140">Um dispositivo StorSimple conectado a um host Linux pode ser configurado para alta disponibilidade e balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="7d008-140">A StorSimple device connected to a Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="7d008-141">Por exemplo, se o host Linux tiver duas interfaces conectadas à SAN e o dispositivo tem duas interfaces conectadas à SAN, de modo que essas interfaces estejam na mesma sub-rede, então haverá 4 caminhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7d008-141">For example, if the Linux host has two interfaces connected to the SAN and the device has two interfaces connected to the SAN such that these interfaces are on the same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="7d008-142">No entanto, se cada interface DATA na interface do dispositivo e do host estiver em uma sub-rede IP diferente (e não roteável), então somente dois caminhos estarão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7d008-142">However, if each DATA interface on the device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="7d008-143">Você pode configurar vários caminhos para descobrir automaticamente todos os caminhos disponíveis, escolher um algoritmo de balanceamento de carga para esses caminhos, aplicar as configurações específicas a volumes só do StorSimple e então habilitar e verificar vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-143">You can configure multipathing to automatically discover all the available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="7d008-144">O procedimento a seguir descreve como configurar vários caminhos quando um dispositivo StorSimple com duas interfaces de rede está conectado a um host com duas interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="7d008-144">The following procedure describes how to configure multipathing when a StorSimple device with two network interfaces is connected to a host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d008-145">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7d008-145">Prerequisites</span></span>
<span data-ttu-id="7d008-146">Esta seção detalha os pré-requisitos de configuração para o servidor CentOS e seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-146">This section details the configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="7d008-147">No host CentOS</span><span class="sxs-lookup"><span data-stu-id="7d008-147">On CentOS host</span></span>
1. <span data-ttu-id="7d008-148">Certifique-se de que seu host CentOS tenha duas interfaces de rede habilitadas.</span><span class="sxs-lookup"><span data-stu-id="7d008-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="7d008-149">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="7d008-150">O exemplo a seguir mostra a saída quando duas interfaces de rede (`eth0` e `eth1`) estiverem presentes no host.</span><span class="sxs-lookup"><span data-stu-id="7d008-150">The following example shows the output when two network interfaces (`eth0` and `eth1`) are present on the host.</span></span>
   
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
2. <span data-ttu-id="7d008-151">Instale *iSCSI-initiator-utils* em seu servidor CentOS.</span><span class="sxs-lookup"><span data-stu-id="7d008-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="7d008-152">Execute as etapas a seguir para instalar o *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="7d008-152">Perform the following steps to install *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="7d008-153">Faça logon como `root` em seu host CentOS.</span><span class="sxs-lookup"><span data-stu-id="7d008-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="7d008-154">Instale o *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="7d008-154">Install the *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="7d008-155">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="7d008-156">Após a instalação bem-sucedida do *iSCSI-Initiator-utils* , inicie o serviço iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7d008-156">After the *iSCSI-Initiator-utils* is successfully installed, start the iSCSI service.</span></span> <span data-ttu-id="7d008-157">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="7d008-158">Em algumas ocasiões, talvez o `iscsid` não seja realmente iniciado e a opção `--force` poderá ser necessária</span><span class="sxs-lookup"><span data-stu-id="7d008-158">On occasions, `iscsid` may not actually start and the `--force` option may be needed</span></span>
   4. <span data-ttu-id="7d008-159">Para garantir que o iniciador iSCSI esteja habilitado no momento da inicialização, use o comando `chkconfig` para habilitar o serviço.</span><span class="sxs-lookup"><span data-stu-id="7d008-159">To ensure that your iSCSI initiator is enabled during boot time, use the `chkconfig` command to enable the service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="7d008-160">Para verificar se ele foi configurado corretamente, execute o comando:</span><span class="sxs-lookup"><span data-stu-id="7d008-160">To verify that that it was properly setup, run the command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="7d008-161">Um exemplo de saída é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7d008-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="7d008-162">No exemplo acima, você pode ver que o seu ambiente iSCSI será executado no momento da inicialização em níveis de execução 2, 3, 4 e 5.</span><span class="sxs-lookup"><span data-stu-id="7d008-162">From the above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="7d008-163">Instale o *device-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="7d008-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="7d008-164">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="7d008-165">A instalação será iniciada.</span><span class="sxs-lookup"><span data-stu-id="7d008-165">The installation will start.</span></span> <span data-ttu-id="7d008-166">Digite **S** para continuar quando a confirmação for solicitada.</span><span class="sxs-lookup"><span data-stu-id="7d008-166">Type **Y** to continue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="7d008-167">No dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="7d008-167">On StorSimple device</span></span>
<span data-ttu-id="7d008-168">O dispositivo StorSimple deve ter:</span><span class="sxs-lookup"><span data-stu-id="7d008-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="7d008-169">No mínimo duas interfaces habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7d008-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="7d008-170">Para verificar se duas interfaces são habilitadas para iSCSI em seu dispositivo StorSimple, execute as seguintes etapas no Portal Clássico do Azure do seu dispositivo StorSimple:</span><span class="sxs-lookup"><span data-stu-id="7d008-170">To verify that two interfaces are iSCSI-enabled on your StorSimple device, perform the following steps in the Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="7d008-171">Faça logon no Portal Clássico do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-171">Log into the classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="7d008-172">Selecione o serviço StorSimple Manager, clique em **Dispositivos** e escolha o dispositivo StorSimple específico.</span><span class="sxs-lookup"><span data-stu-id="7d008-172">Select your StorSimple Manager service, click **Devices** and choose the specific StorSimple device.</span></span> <span data-ttu-id="7d008-173">Clique em **Configurar** e verifique as configurações da interface de rede.</span><span class="sxs-lookup"><span data-stu-id="7d008-173">Click **Configure** and verify the network interface settings.</span></span> <span data-ttu-id="7d008-174">Uma captura de tela com duas interfaces de rede habilitadas para iSCSI é mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="7d008-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="7d008-175">Aqui, DATA 2 e DATA 3, ambas as interfaces 10 GbE estão habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7d008-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Configuração de DATA 2 do StorsSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configuração de DATA 3 do StorsSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="7d008-178">Na página **Configurar**</span><span class="sxs-lookup"><span data-stu-id="7d008-178">In the **Configure** page</span></span>
     
     1. <span data-ttu-id="7d008-179">Verifique se ambas as interfaces de rede estão habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7d008-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="7d008-180">O campo **Habilitada para iSCSI** deve ser definido como **Sim**.</span><span class="sxs-lookup"><span data-stu-id="7d008-180">The **iSCSI enabled** field should be set to **Yes**.</span></span>
     2. <span data-ttu-id="7d008-181">Verifique se as interfaces de rede têm a mesma velocidade, ambas devem ser de 1 GbE ou de 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="7d008-181">Ensure that the network interfaces have the same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="7d008-182">Anote os endereços IPv4 das interfaces habilitadas para iSCSI e salve-os para uso posterior no host.</span><span class="sxs-lookup"><span data-stu-id="7d008-182">Note the IPv4 addresses of the iSCSI-enabled interfaces and save for later use on the host.</span></span>
* <span data-ttu-id="7d008-183">As interfaces iSCSI em seu dispositivo StorSimple devem poder ser acessadas do servidor CentOS.</span><span class="sxs-lookup"><span data-stu-id="7d008-183">The iSCSI interfaces on your StorSimple device should be reachable from the CentOS server.</span></span>
      <span data-ttu-id="7d008-184">Para verificar isso, você precisa fornecer os endereços IP das interfaces da rede habilitadas para iSCSI do StorSimple em seu servidor host.</span><span class="sxs-lookup"><span data-stu-id="7d008-184">To verify this, you need to provide the IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="7d008-185">Os comandos usados e a saída correspondente com DATA2 (10.126.162.25) e DATA3 (10.126.162.26) são mostrados abaixo:</span><span class="sxs-lookup"><span data-stu-id="7d008-185">The commands used and the corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="7d008-186">Configuração de hardware</span><span class="sxs-lookup"><span data-stu-id="7d008-186">Hardware configuration</span></span>
<span data-ttu-id="7d008-187">É recomendável que você conecte as duas interfaces de rede iSCSI em caminhos separados para redundância.</span><span class="sxs-lookup"><span data-stu-id="7d008-187">We recommend that you connect the two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="7d008-188">A figura a seguir mostra a configuração de hardware recomendada para vários caminhos de alta disponibilidade e de balanceamento de carga para seu servidor CentOS e o dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-188">The figure below shows the recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Configuração de hardware do MPIO para StorSimple para o host Linux](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="7d008-190">Como mostrado na figura anterior:</span><span class="sxs-lookup"><span data-stu-id="7d008-190">As shown in the preceding figure:</span></span>

* <span data-ttu-id="7d008-191">O dispositivo StorSimple está em uma configuração ativo-passivo com dois controladores.</span><span class="sxs-lookup"><span data-stu-id="7d008-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="7d008-192">Dois switches de SAN estão conectados aos seus controladores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7d008-192">Two SAN switches are connected to your device controllers.</span></span>
* <span data-ttu-id="7d008-193">Dois iniciadores iSCSI estão habilitados no seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="7d008-194">Duas interfaces de rede estão habilitadas em seu host CentOS.</span><span class="sxs-lookup"><span data-stu-id="7d008-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="7d008-195">A configuração acima gerará quatro caminhos separados entre o dispositivo e o host se o host e as interfaces de dados forem roteáveis.</span><span class="sxs-lookup"><span data-stu-id="7d008-195">The above configuration will yield 4 separate paths between your device and the host if the host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7d008-196">É recomendável que você não misture as interfaces de rede de 1 GbE e de 10 GbE para vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="7d008-197">Quando você estiver usando duas interfaces de rede, ambas as interfaces deverão ser do tipo idêntico.</span><span class="sxs-lookup"><span data-stu-id="7d008-197">When using two network interfaces, both the interfaces should be the identical type.</span></span>
> * <span data-ttu-id="7d008-198">Em seu dispositivo StorSimple, DATA0, DATA1, DATA4 e DATA5 são interfaces de 1 GbE, enquanto DATA2 e DATA3 são interfaces de rede de 10 GbE.|</span><span class="sxs-lookup"><span data-stu-id="7d008-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="7d008-199">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="7d008-199">Configuration steps</span></span>
<span data-ttu-id="7d008-200">As etapas de configuração para vários caminhos envolvem a configuração dos caminhos disponíveis para a descoberta automática, especificando o algoritmo de balanceamento de carga a ser usado, habilitando vários caminhos e, por fim, verificando a configuração.</span><span class="sxs-lookup"><span data-stu-id="7d008-200">The configuration steps for multipathing involve configuring the available paths for automatic discovery, specifying the load-balancing algorithm to use, enabling multipathing and finally verifying the configuration.</span></span> <span data-ttu-id="7d008-201">Cada uma das etapas acima será discutida nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="7d008-201">Each of these steps is discussed in detail in the following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="7d008-202">Etapa 1: Configurar vários caminhos para a descoberta automática</span><span class="sxs-lookup"><span data-stu-id="7d008-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="7d008-203">Os dispositivos multipath-supported podem ser automaticamente descobertos e configurados.</span><span class="sxs-lookup"><span data-stu-id="7d008-203">The multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="7d008-204">Inicialize o arquivo `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="7d008-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="7d008-205">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="7d008-206">O comando acima criará um arquivo `sample/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="7d008-206">The above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="7d008-207">Inicie o serviço de vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-207">Start multipath service.</span></span> <span data-ttu-id="7d008-208">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="7d008-209">Você verá esta saída:</span><span class="sxs-lookup"><span data-stu-id="7d008-209">You will see the following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="7d008-210">Habilite a descoberta automática dos vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="7d008-211">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="7d008-212">Isso modificará a seção de padrões de seu `multipath.conf` como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="7d008-212">This will modify the defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="7d008-213">Etapa 2: Configurar vários caminhos para volumes StorSimple</span><span class="sxs-lookup"><span data-stu-id="7d008-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="7d008-214">Por padrão, todos os dispositivos estão na lista negra no arquivo multipath.conf e serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="7d008-214">By default, all devices are black listed in the multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="7d008-215">Será necessário criar exceções de lista negra para permitir vários caminhos para volumes desde dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-215">You will need to create blacklist exceptions to allow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="7d008-216">Edite o arquivo `/etc/mulitpath.conf` .</span><span class="sxs-lookup"><span data-stu-id="7d008-216">Edit the `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="7d008-217">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="7d008-218">Localize a seção blacklist_exceptions no arquivo multipath.conf.</span><span class="sxs-lookup"><span data-stu-id="7d008-218">Locate the blacklist_exceptions section in the multipath.conf file.</span></span> <span data-ttu-id="7d008-219">Seu dispositivo StorSimple precisa estar relacionado como uma exceção de lista negra nesta seção.</span><span class="sxs-lookup"><span data-stu-id="7d008-219">Your StorSimple device needs to be listed as a blacklist exception in this section.</span></span> <span data-ttu-id="7d008-220">Você pode retirar o comentário de linhas relevantes neste arquivo para modificá-lo como mostrado abaixo (use somente o modelo específico do dispositivo que você estiver usando):</span><span class="sxs-lookup"><span data-stu-id="7d008-220">You can uncomment relevant lines in this file to modify it as shown below (use only the specific model of the device you are using):</span></span>
   
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

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="7d008-221">Etapa 3: Configurar vários caminhos de round robin</span><span class="sxs-lookup"><span data-stu-id="7d008-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="7d008-222">Esse algoritmo de balanceamento de carga usa todos os vários caminhos disponíveis para o controlador ativo em um round robin balanceado.</span><span class="sxs-lookup"><span data-stu-id="7d008-222">This load-balancing algorithm uses all the available multipaths to the active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="7d008-223">Edite o arquivo `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="7d008-223">Edit the `/etc/multipath.conf` file.</span></span> <span data-ttu-id="7d008-224">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="7d008-225">Na seção `defaults`, defina a `path_grouping_policy` como `multibus`.</span><span class="sxs-lookup"><span data-stu-id="7d008-225">Under the `defaults` section, set the `path_grouping_policy` to `multibus`.</span></span> <span data-ttu-id="7d008-226">A `path_grouping_policy` especifica a política de agrupamento de caminho padrão a ser aplicada a vários caminhos não especificados.</span><span class="sxs-lookup"><span data-stu-id="7d008-226">The `path_grouping_policy` specifies the default path grouping policy to apply to unspecified multipaths.</span></span> <span data-ttu-id="7d008-227">A seção de padrões terá a aparência mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="7d008-227">The defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="7d008-228">Os valores mais comuns de `path_grouping_policy` incluem:</span><span class="sxs-lookup"><span data-stu-id="7d008-228">The most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="7d008-229">failover = um caminho por grupo de prioridade</span><span class="sxs-lookup"><span data-stu-id="7d008-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="7d008-230">multibus = todos os caminhos válidos em um grupo de prioridade</span><span class="sxs-lookup"><span data-stu-id="7d008-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="7d008-231">Etapa 4: Habilitar vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="7d008-232">Reinicie o daemon `multipathd` .</span><span class="sxs-lookup"><span data-stu-id="7d008-232">Restart the `multipathd` daemon.</span></span> <span data-ttu-id="7d008-233">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="7d008-234">A saída será como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="7d008-234">The output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="7d008-235">Etapa 5: Verificar vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="7d008-236">Primeiro, verifique se a conexão iSCSI foi estabelecida como dispositivo StorSimple da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7d008-236">First make sure that iSCSI connection is established with the StorSimple device as follows:</span></span>
   
   <span data-ttu-id="7d008-237">a.</span><span class="sxs-lookup"><span data-stu-id="7d008-237">a.</span></span> <span data-ttu-id="7d008-238">Descubra seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-238">Discover your StorSimple device.</span></span> <span data-ttu-id="7d008-239">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on the device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="7d008-240">A saída quando o endereço IP de DATA0 é 10.126.162.25 e a porta 3260 está aberta no dispositivo StorSimple para o tráfego iSCSI de saída como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="7d008-240">The output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on the StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="7d008-241">Copie o IQN do seu dispositivo StorSimple, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, desde a saída anterior.</span><span class="sxs-lookup"><span data-stu-id="7d008-241">Copy the IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from the preceding output.</span></span>

   <span data-ttu-id="7d008-242">b.</span><span class="sxs-lookup"><span data-stu-id="7d008-242">b.</span></span> <span data-ttu-id="7d008-243">Conecte-se ao dispositivo usando o IQN de destino.</span><span class="sxs-lookup"><span data-stu-id="7d008-243">Connect to the device using target IQN.</span></span> <span data-ttu-id="7d008-244">O dispositivo StorSimple é o destino iSCSI aqui.</span><span class="sxs-lookup"><span data-stu-id="7d008-244">The StorSimple device is the iSCSI target here.</span></span> <span data-ttu-id="7d008-245">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="7d008-246">O exemplo a seguir mostra a saída com um destino IQN do `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="7d008-246">The following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="7d008-247">A saída indica que você se conectou com êxito às duas interfaces de rede habilitadas para iSCSI em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7d008-247">The output indicates that you have successfully connected to the two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="7d008-248">Se você vir somente uma interface de host e dois caminhos aqui, precisará habilitar ambas as interfaces no host para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7d008-248">If you see only one host interface and two paths here, then you need to enable both the interfaces on host for iSCSI.</span></span> <span data-ttu-id="7d008-249">Você pode seguir as [instruções detalhadas na documentação do Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="7d008-249">You can follow the [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="7d008-250">Um volume é exposto ao servidor CentOS do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-250">A volume is exposed to the CentOS server from the StorSimple device.</span></span> <span data-ttu-id="7d008-251">Para saber mais, veja como [Etapa 6: Criar um volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) por meio do Portal Clássico do Azure em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via the Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="7d008-252">Verifique os caminhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7d008-252">Verify the available paths.</span></span> <span data-ttu-id="7d008-253">Tipo:</span><span class="sxs-lookup"><span data-stu-id="7d008-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="7d008-254">O exemplo a seguir mostra a saída de duas interfaces de rede em um dispositivo StorSimple conectado a uma interface de rede de host com dois caminhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7d008-254">The following example shows the output for two network interfaces on a StorSimple device connected to a single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        The following example shows the output for two network interfaces on a StorSimple device connected to two host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After the paths are configured, refer to the specific instructions on your host operating system (Centos 6.6) to mount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="7d008-255">Solucionar problemas de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="7d008-256">Esta seção fornece algumas dicas úteis se você tiver algum problema durante a configuração de vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="7d008-257">P.</span><span class="sxs-lookup"><span data-stu-id="7d008-257">Q.</span></span> <span data-ttu-id="7d008-258">Não vejo as alterações no arquivo `multipath.conf` entrarem em vigor.</span><span class="sxs-lookup"><span data-stu-id="7d008-258">I do not see the changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="7d008-259">R.</span><span class="sxs-lookup"><span data-stu-id="7d008-259">A.</span></span> <span data-ttu-id="7d008-260">Se você tiver alguma alteração no arquivo `multipath.conf` , precisará reiniciar o serviço de vários caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-260">If you have made any changes to the `multipath.conf` file, you will need to restart the multipathing service.</span></span> <span data-ttu-id="7d008-261">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7d008-261">Type the following command:</span></span>

    service multipathd restart

<span data-ttu-id="7d008-262">P.</span><span class="sxs-lookup"><span data-stu-id="7d008-262">Q.</span></span> <span data-ttu-id="7d008-263">Habilitei duas interfaces de rede no dispositivo StorSimple e duas interfaces de rede no host.</span><span class="sxs-lookup"><span data-stu-id="7d008-263">I have enabled two network interfaces on the StorSimple device and two network interfaces on the host.</span></span> <span data-ttu-id="7d008-264">Quando eu listo os caminhos disponíveis, vejo apenas dois caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-264">When I list the available paths, I see only two paths.</span></span> <span data-ttu-id="7d008-265">Eu esperava ver quatro caminhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7d008-265">I expected to see four available paths.</span></span>

<span data-ttu-id="7d008-266">R.</span><span class="sxs-lookup"><span data-stu-id="7d008-266">A.</span></span> <span data-ttu-id="7d008-267">Verifique se os dois caminhos estão na mesma sub-rede e se são roteáveis.</span><span class="sxs-lookup"><span data-stu-id="7d008-267">Make sure that the two paths are on the same subnet and routable.</span></span> <span data-ttu-id="7d008-268">Se as interfaces de rede estiverem em vLANs diferentes e se não forem roteáveis, você verá somente dois caminhos.</span><span class="sxs-lookup"><span data-stu-id="7d008-268">If the network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="7d008-269">Uma maneira de verificar isso é garantir que você possa acessar as interfaces de host de uma interface de rede no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-269">One way to verify this is to make sure that you can reach both the host interfaces from a network interface on the StorSimple device.</span></span> <span data-ttu-id="7d008-270">Você precisará [contatar o Suporte da Microsoft](storsimple-contact-microsoft-support.md) , já que essa verificação só poderá ser feita por meio de uma sessão de suporte.</span><span class="sxs-lookup"><span data-stu-id="7d008-270">You will need to [contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="7d008-271">P.</span><span class="sxs-lookup"><span data-stu-id="7d008-271">Q.</span></span> <span data-ttu-id="7d008-272">Quando eu listo os caminhos disponíveis, não vejo nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="7d008-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="7d008-273">R.</span><span class="sxs-lookup"><span data-stu-id="7d008-273">A.</span></span> <span data-ttu-id="7d008-274">Normalmente, não ver todos os vários caminhos sugere um problema com o daemon de vários caminhos e é mais provável que qualquer problema aqui esteja no arquivo `multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="7d008-274">Typically, not seeing any multipathed paths suggests a problem with the multipathing daemon, and it’s most likely that any problem here lies in the `multipath.conf` file.</span></span>

<span data-ttu-id="7d008-275">Também vale a pena verificar se você realmente pode ver alguns discos depois de se conectar ao destino, já que nenhuma resposta das listagens de vários caminhos também poderia significar que você não tem discos.</span><span class="sxs-lookup"><span data-stu-id="7d008-275">It would also be worth checking that you can actually see some disks after connecting to the target, as no response from the multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="7d008-276">Use o comando a seguir para examinar novamente o barramento SCSI:</span><span class="sxs-lookup"><span data-stu-id="7d008-276">Use the following command to rescan the SCSI bus:</span></span>
  
    <span data-ttu-id="7d008-277">`$ rescan-scsi-bus.sh `(parte do pacote sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="7d008-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="7d008-278">Digite os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7d008-278">Type the following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="7d008-279">Ou</span><span class="sxs-lookup"><span data-stu-id="7d008-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="7d008-280">Eles retornarão detalhes de discos adicionados recentemente.</span><span class="sxs-lookup"><span data-stu-id="7d008-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="7d008-281">Para determinar se ele é um disco StorSimple, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7d008-281">To determine whether it is a StorSimple disk, use the following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="7d008-282">Isso retornará uma cadeia de caracteres, o que determinará se é um disco StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="7d008-283">Uma causa menos provável, mas possível, também poderia ser um pid iscsid obsoleto.</span><span class="sxs-lookup"><span data-stu-id="7d008-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="7d008-284">Use o comando a seguir para fazer logoff das sessões iSCSI:</span><span class="sxs-lookup"><span data-stu-id="7d008-284">Use the following command to log off from the iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="7d008-285">Repita esse comando para todas as interfaces de rede conectadas no destino iSCSI, que é o seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d008-285">Repeat this command for all the connected network interfaces on the iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="7d008-286">Depois de fazer logoff de todas as sessões iSCSI, use o IQN de destino iSCSI para restabelecer a sessão iSCSI.</span><span class="sxs-lookup"><span data-stu-id="7d008-286">Once you have logged off from all the iSCSI sessions, use the iSCSI target IQN to reestablish the iSCSI session.</span></span> <span data-ttu-id="7d008-287">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7d008-287">Type the following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="7d008-288">P.</span><span class="sxs-lookup"><span data-stu-id="7d008-288">Q.</span></span> <span data-ttu-id="7d008-289">Não sei se meu dispositivo está na lista branca.</span><span class="sxs-lookup"><span data-stu-id="7d008-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="7d008-290">R.</span><span class="sxs-lookup"><span data-stu-id="7d008-290">A.</span></span> <span data-ttu-id="7d008-291">Para verificar se seu dispositivo está na lista branca, use o seguinte comando interativo de solução de problemas:</span><span class="sxs-lookup"><span data-stu-id="7d008-291">To verify whether your device is whitelisted, use the following troubleshooting interactive command:</span></span>

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


<span data-ttu-id="7d008-292">Para saber mais, veja como [usar o comando interativo de solução de problemas para múltiplos caminhos](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="7d008-292">For more information, go to [use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="7d008-293">Lista de comandos úteis</span><span class="sxs-lookup"><span data-stu-id="7d008-293">List of useful commands</span></span>
| <span data-ttu-id="7d008-294">Digite </span><span class="sxs-lookup"><span data-stu-id="7d008-294">Type</span></span> | <span data-ttu-id="7d008-295">Command</span><span class="sxs-lookup"><span data-stu-id="7d008-295">Command</span></span> | <span data-ttu-id="7d008-296">Descrição</span><span class="sxs-lookup"><span data-stu-id="7d008-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d008-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="7d008-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="7d008-298">Iniciar o serviço iSCSI</span><span class="sxs-lookup"><span data-stu-id="7d008-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="7d008-299">Parar o serviço iSCSI</span><span class="sxs-lookup"><span data-stu-id="7d008-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="7d008-300">Reiniciar o serviço iSCSI</span><span class="sxs-lookup"><span data-stu-id="7d008-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="7d008-301">Descobrir os destinos disponíveis no endereço especificado</span><span class="sxs-lookup"><span data-stu-id="7d008-301">Discover available targets on the specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="7d008-302">Fazer logon no destino iSCSI</span><span class="sxs-lookup"><span data-stu-id="7d008-302">Log in to the iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="7d008-303">Faça logoff do destino iSCSI</span><span class="sxs-lookup"><span data-stu-id="7d008-303">Log out from the iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="7d008-304">Imprimir o nome do iniciador iSCSI</span><span class="sxs-lookup"><span data-stu-id="7d008-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="7d008-305">Verificar o estado da sessão de iSCSI e o volume descoberto no host</span><span class="sxs-lookup"><span data-stu-id="7d008-305">Check the state of the iSCSI session and volume discovered on the host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="7d008-306">Mostra todas as sessões de iSCSI estabelecidas entre o host e o dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="7d008-306">Shows all the iSCSI sessions established between the host and the StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="7d008-307">**Múltiplos caminhos**</span><span class="sxs-lookup"><span data-stu-id="7d008-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="7d008-308">Iniciar o daemon de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="7d008-309">Parar o daemon de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="7d008-310">Reiniciar o daemon de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="7d008-311">Ou</span><span class="sxs-lookup"><span data-stu-id="7d008-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="7d008-312">Habilitar daemon de vários caminhos para iniciar no momento da inicialização</span><span class="sxs-lookup"><span data-stu-id="7d008-312">Enable multipath daemon to start at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="7d008-313">Inicie o console interativo para solução de problemas</span><span class="sxs-lookup"><span data-stu-id="7d008-313">Start the interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="7d008-314">Listar as conexões e dispositivos de vários caminhos</span><span class="sxs-lookup"><span data-stu-id="7d008-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="7d008-315">Criar um arquivo mulitpath.conf de exemplo `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="7d008-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="7d008-316">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7d008-316">Next steps</span></span>
<span data-ttu-id="7d008-317">Já que você está configurando o MPIO no host Linux, talvez também seja necessário consultar os seguintes documentos do CentoS 6.6:</span><span class="sxs-lookup"><span data-stu-id="7d008-317">As you are configuring MPIO on Linux host, you may also need to refer to the following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="7d008-318">Configurando o MPIO no CentOS</span><span class="sxs-lookup"><span data-stu-id="7d008-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="7d008-319">Guia de treinamento do Linux</span><span class="sxs-lookup"><span data-stu-id="7d008-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

