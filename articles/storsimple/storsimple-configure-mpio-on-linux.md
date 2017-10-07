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
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>Configurar o MPIO em um host do StorSimple executando o CentOS
Este artigo explica tooconfigure necessário de etapas de saudação e/s de múltiplos caminhos (MPIO) no servidor host Centos 6.6. servidor de host de saudação é o dispositivo do Microsoft Azure StorSimple tooyour conectado para alta disponibilidade por meio de iniciadores iSCSI. Ele descreve em detalhes Olá a descoberta automática de dispositivos multipath e configuração específica de saudação apenas para os volumes do StorSimple.

Esse procedimento é aplicável tooall modelos de saudação de dispositivos da série StorSimple 8000.

> [!NOTE]
> Este procedimento não pode ser usado para um dispositivo virtual StorSimple. Para obter mais informações, consulte como tooconfigure hospedar servidores para seu dispositivo virtual.
> 
> 

## <a name="about-multipathing"></a>Sobre vários caminhos
o recurso de vários caminhos Olá permite que você tooconfigure vários caminhos de e/s entre um servidor host e um dispositivo de armazenamento. Esses caminhos de E/S são conexões físicas da SAN que podem incluir cabos, switches, interfaces de rede e controladores separados. Múltiplos caminhos agrega caminhos de e/s hello, tooconfigure um novo dispositivo que está associado a todos os caminhos de saudação agregado.

Olá finalidade múltiplos caminhos é dupla:

* **Alta disponibilidade**: ele fornece um caminho alternativo, se falhar de qualquer elemento de caminho hello e/s (por exemplo, um cabo, switch, interface de rede ou controlador).
* **O balanceamento de carga**: dependendo da configuração de saudação do seu dispositivo de armazenamento, ela pode melhorar o desempenho de saudação detectando cargas em caminhos de e/s de saudação e rebalanceamento dinamicamente as cargas.

### <a name="about-multipathing-components"></a>Sobre componentes de vários caminhos
Vários caminhos em Linux consiste em componentes de kernel e em componentes de espaço do usuário como mostrados na tabela abaixo.

* **Kernel**: Olá principal componente é Olá *mapeador de dispositivo* que redireciona a e/s e oferece suporte a failover de caminhos e grupos de caminho.

* **Espaço do usuário**: esses são *ferramentas multipath* que gerenciar dispositivos Multipath instruindo o módulo de vários caminhos de mapeador de dispositivo de saudação que toodo. ferramentas de saudação consistem em:
   
   * **Multipath**: lista e configura os dispositivos de vários caminhos.
   * **Vários caminhos**: daemon que executa os caminhos de saudação multipath e monitores.
   * **Nome do Devmap**: fornece um tooudev significativa do nome do dispositivo para devmaps.
   * **Kpartx**: mapeia linear devmaps toodevice partições toomake multipath particionável.
   * **Multipath**: arquivo de configuração do daemon de vários caminhos que é usado toooverwrite Olá configuração interna tabela.

### <a name="about-hello-multipathconf-configuration-file"></a>Sobre o arquivo de configuração do Multipath Olá
arquivo de configuração de saudação `/etc/multipath.conf` faz muitas Olá recursos de múltiplos caminhos configurável pelo usuário. Olá `multipath` daemon kernel de comando e hello `multipathd` usar as informações encontradas neste arquivo. arquivo Hello é consultado somente durante a configuração de saudação de dispositivos multipath hello. Certifique-se de que todas as alterações são feitas antes de executar Olá `multipath` comando. Se você modificar o arquivo hello posteriormente, será necessário toostop e iniciar vários caminhos novamente para Olá alterações tootake efeito.

Olá Multipath tem cinco seções:

- **System level defaults** *(defaults)*: você pode substituir os padrões no nível do sistema.
- **Na lista negra dispositivos** *(lista de bloqueios)*: você pode especificar a lista de saudação de dispositivos que não devem ser controladas pelo mapeador de dispositivo.
- **Lista negra exceções** *(blacklist_exceptions)*: você pode identificar dispositivos específicos toobe tratado como dispositivos de multipath mesmo se listadas na lista de bloqueios de saudação.
- **As configurações específicas de controlador de armazenamento** *(dispositivos)*: você pode especificar as configurações que serão aplicadas toodevices que possuem informações de fornecedor e do produto.
- **As configurações específicas de dispositivo** *(os multicaminhos)*: você pode usar as definições de configuração Esta seção toofine ajustar Olá para LUNs individuais.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>Configurar vários caminhos no host do StorSimple tooLinux conectado
Um host Linux do StorSimple dispositivo conectado tooa pode ser configurado para alta disponibilidade e balanceamento de carga. Por exemplo, se o host do Linux Olá tem duas interfaces de dispositivo de SAN e hello toohello conectado tem duas interfaces conectadas toohello SAN, de modo que essas interfaces são na mesma sub-rede de hello e, em seguida, haverá 4 caminhos disponíveis. No entanto, se cada interface de dados na interface de dispositivo e host Olá está em uma sub-rede IP diferente (e não pode ser roteado), somente 2 caminhos estará disponíveis. Você pode configurar vários caminhos tooautomatically descobrir todos os caminhos disponíveis do hello, escolher um algoritmo de balanceamento de carga para esses caminhos, aplique as configurações específicas para volumes de StorSimple e, em seguida, habilitar e verifique se vários caminhos.

Olá procedimento a seguir descreve como vários caminhos de tooconfigure quando um dispositivo StorSimple com duas interfaces de rede é conectado tooa host com duas interfaces de rede.

## <a name="prerequisites"></a>Pré-requisitos
Esta seção fornece detalhes sobre os pré-requisitos de configuração Olá para servidor CentOS e seu dispositivo StorSimple.

### <a name="on-centos-host"></a>No host CentOS
1. Certifique-se de que seu host CentOS tenha duas interfaces de rede habilitadas. Tipo:
   
    `ifconfig`
   
    Olá exemplo a seguir mostra a saída de hello quando duas interfaces de rede (`eth0` e `eth1`) estão presentes no host de saudação.
   
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
2. Instale *iSCSI-initiator-utils* em seu servidor CentOS. Executar Olá seguindo as etapas tooinstall *utilitários de iniciador de iSCSI*.
   
   1. Faça logon como `root` em seu host CentOS.
   2. Instalar Olá *utilitários de iniciador de iSCSI*. Tipo:
      
       `yum install iscsi-initiator-utils`
   3. Depois de saudação *utilitários de iniciador de iSCSI* com êxito é instalado, inicie o serviço iSCSI hello. Tipo:
      
       `service iscsid start`
      
       Em ocasiões, `iscsid` , na verdade, não pode iniciar e Olá `--force` opção pode ser necessária
   4. tooensure que o iniciador iSCSI está habilitado no momento da inicialização, use Olá `chkconfig` tooenable serviço de saudação do comando.
      
       `chkconfig iscsi on`
   5. tooverify que ele foi corretamente de instalação, execute o comando de saudação:
      
       `chkconfig --list | grep iscsi`
      
       Um exemplo de saída é mostrado abaixo.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       Olá, o exemplo acima, você pode ver que seu ambiente iSCSI seja executado no tempo de inicialização em níveis de execução 2, 3, 4 e 5.
3. Instale o *device-mapper-multipath*. Tipo:
   
    `yum install device-mapper-multipath`
   
    Olá instalação será iniciada. Tipo **Y** toocontinue quando for solicitada a confirmação.

### <a name="on-storsimple-device"></a>No dispositivo StorSimple
O dispositivo StorSimple deve ter:

* No mínimo duas interfaces habilitadas para iSCSI. tooverify que duas interfaces estão habilitadas para iSCSI no seu dispositivo StorSimple, execute Olá Olá portal clássico do Azure para seu dispositivo StorSimple etapas:
  
  1. Faça logon no portal clássico do Olá para seu dispositivo StorSimple.
  2. Selecione seu serviço StorSimple Manager, clique em **dispositivos** e escolha o dispositivo StorSimple específico de saudação. Clique em **configurar** e verifique se as configurações de interface de rede de saudação. Uma captura de tela com duas interfaces de rede habilitadas para iSCSI é mostrada abaixo. Aqui, DATA 2 e DATA 3, ambas as interfaces 10 GbE estão habilitadas para iSCSI.
     
      ![Configuração de DATA 2 do StorsSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configuração de DATA 3 do StorsSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      Em Olá **configurar** página
     
     1. Verifique se ambas as interfaces de rede estão habilitadas para iSCSI. Olá **iSCSI habilitado** campo deve ser definido muito**Sim**.
     2. Verifique se as interfaces de rede de saudação têm Olá mesma velocidade, deve ser 1 GbE ou 10 GbE.
     3. Observe os endereços de saudação IPv4 de interfaces habilitadas para iSCSI do hello e salve para uso posterior no host de saudação.
* interfaces de iSCSI Olá em seu dispositivo StorSimple devem ser acessíveis a partir do servidor de CentOS hello.
      tooverify isso, você precisa tooprovide endereços IP hello das suas interfaces de rede habilitada para iSCSI do StorSimple em seu servidor de host. Olá comandos usados e Olá saída correspondente com DATA2 (10.126.162.25) e DATA3 (10.126.162.26) é mostrado abaixo:
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>Configuração de hardware
É recomendável que você se conecte a saudação duas iSCSI interfaces de rede em caminhos separados para redundância. Olá figura a seguir mostra a configuração de hardware recomendada Olá para alta disponibilidade e balanceamento de carga de criação de vários caminhos para seu servidor CentOS e o dispositivo StorSimple.

![Configuração de hardware do MPIO para StorSimple tooLinux host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Conforme mostrado na saudação anterior Figura:

* O dispositivo StorSimple está em uma configuração ativo-passivo com dois controladores.
* Duas opções de SAN são controladores de dispositivo tooyour conectado.
* Dois iniciadores iSCSI estão habilitados no seu dispositivo StorSimple.
* Duas interfaces de rede estão habilitadas em seu host CentOS.

Olá acima configuração produzirá 4 caminhos separados entre o host de dispositivo e hello se interfaces Olá de host e os dados são roteáveis.

> [!IMPORTANT]
> * É recomendável que você não misture as interfaces de rede de 1 GbE e de 10 GbE para vários caminhos. Ao usar duas interfaces de rede, ambas as interfaces Olá devem ser Olá mesmo tipo.
> * Em seu dispositivo StorSimple, DATA0, DATA1, DATA4 e DATA5 são interfaces de 1 GbE, enquanto DATA2 e DATA3 são interfaces de rede de 10 GbE.|
> 
> 

## <a name="configuration-steps"></a>Etapas da configuração
etapas de configuração de saudação para múltiplos caminhos envolvem configurar caminhos de saudação disponíveis para descoberta automática, especificando Olá balanceamento de carga de algoritmo toouse, habilitar vários caminhos e, finalmente, verificando a configuração de saudação. Cada uma dessas etapas é discutida em detalhes nas seções a seguir de saudação.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>Etapa 1: Configurar vários caminhos para a descoberta automática
dispositivos com suporte de vários caminhos de saudação podem ser descobertos e configurados automaticamente.

1. Inicialize o arquivo `/etc/multipath.conf` . Tipo:
   
     `mpathconf --enable`
   
    Olá acima comando criará uma `sample/etc/multipath.conf` arquivo.
2. Inicie o serviço de vários caminhos. Tipo:
   
    `service multipathd start`
   
    Você verá Olá saída a seguir:
   
    `Starting multipathd daemon:`
3. Habilite a descoberta automática dos vários caminhos. Tipo:
   
    `mpathconf --find_multipaths y`
   
    Isto irá modificar a seção de padrões de saudação do seu `multipath.conf` conforme mostrado abaixo:
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>Etapa 2: Configurar vários caminhos para volumes StorSimple
Por padrão, todos os dispositivos são pretos listados no arquivo de Multipath hello e serão ignorados. Você precisará toocreate de lista de bloqueios exceções tooallow vários caminhos para os volumes de dispositivos de StorSimple.

1. Editar saudação `/etc/mulitpath.conf` arquivo. Tipo:
   
    `vi /etc/multipath.conf`
2. Localize a seção de blacklist_exceptions de saudação no arquivo de Multipath hello. Seu dispositivo StorSimple precisa toobe listada como uma exceção de lista de bloqueios nesta seção. Você pode remover o comentário relevantes linhas toomodify esse arquivo-lo conforme mostrado a seguir (use somente Olá modelo específico de dispositivo Olá que você está usando):
   
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

### <a name="step-3-configure-round-robin-multipathing"></a>Etapa 3: Configurar vários caminhos de round robin
Esse algoritmo de balanceamento de carga usa todos os controlador de active de toohello multipaths disponível de saudação de forma equilibrada, round-robin.

1. Editar saudação `/etc/multipath.conf` arquivo. Tipo:
   
    `vi /etc/multipath.conf`
2. Em Olá `defaults` seção, Olá conjunto `path_grouping_policy` muito`multibus`. Olá `path_grouping_policy` Especifica saudação padrão caminho agrupamento política tooapply toounspecified os multicaminhos. seção de padrões de saudação procurará conforme mostrado abaixo.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> Olá valores mais comuns de `path_grouping_policy` incluem:
> 
> * failover = um caminho por grupo de prioridade
> * multibus = todos os caminhos válidos em um grupo de prioridade
> 
> 

### <a name="step-4-enable-multipathing"></a>Etapa 4: Habilitar vários caminhos
1. Reiniciar Olá `multipathd` daemon. Tipo:
   
    `service multipathd restart`
2. saída de Hello será conforme mostrado abaixo:
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>Etapa 5: Verificar vários caminhos
1. Primeiro, certifique-se de que é estabelecida com o dispositivo StorSimple Olá conexão iSCSI da seguinte maneira:
   
   a. Descubra seu dispositivo StorSimple. Tipo:
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    saída de Hello quando o endereço IP DATA0 é 10.126.162.25 e porta 3260 seja aberta no dispositivo do StorSimple Olá para tráfego iSCSI saída é conforme mostrado abaixo:
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    Saudação de cópia IQN do seu dispositivo StorSimple, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, da saudação anterior de saída.

   b. Conecte o dispositivo de toohello usando o IQN de destino. o dispositivo StorSimple Olá é destino de iSCSI Olá aqui. Tipo:

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    Olá exemplo a seguir mostra a saída com um IQN de destino de `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`. saída de Hello indica que você conectou com êxito toohello duas interfaces de rede habilitada para iSCSI em seu dispositivo.

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

    Se você vir a interface de apenas um host e dois caminhos aqui, em seguida, você precisa tooenable ambas as interfaces Olá no host para iSCSI. Você pode seguir Olá [instruções na documentação do Linux detalhadas](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).

2. Um volume é o servidor de CentOS de toohello exposto do dispositivo do StorSimple hello. Para obter mais informações, consulte [etapa 6: criar um volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via Olá portal clássico do Azure no seu dispositivo StorSimple.

3. Verifique se os caminhos disponíveis hello. Tipo:

      ```
      multipath –l
      ```

      saudação de exemplo a seguir mostra a saída de saudação de duas interfaces de rede em uma interface de rede de host único do StorSimple dispositivo tooa conectado com dois caminhos disponíveis.

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

## <a name="troubleshoot-multipathing"></a>Solucionar problemas de vários caminhos
Esta seção fornece algumas dicas úteis se você tiver algum problema durante a configuração de vários caminhos.

P. Não vejo as alterações de saudação em `multipath.conf` arquivo entrar em vigor.

R. Se você tiver feito qualquer toohello alterações `multipath.conf` arquivo, você precisará de serviço de múltiplos caminhos Olá toorestart. Digite hello comando a seguir:

    service multipathd restart

P. Posso ter habilitado duas interfaces de rede no dispositivo do StorSimple hello e duas interfaces de rede no host de saudação. Quando eu lista caminhos disponíveis hello, vejo apenas dois caminhos. Esperado toosee quatro caminhos disponíveis.

R. Certifique-se de que os caminhos de saudação dois estão em Olá mesma sub-rede e roteável. Se as interfaces de rede de saudação estiverem em diferentes vLANs e não pode ser roteado, você verá apenas dois caminhos. Tooverify unidirecional trata toomake-se de que você possa acessar ambas as interfaces de host de saudação de uma interface de rede no dispositivo do StorSimple hello. Você precisará de muito[entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) como essa verificação só pode ser feita por meio de uma sessão de suporte.

P. Quando eu listo os caminhos disponíveis, não vejo nenhuma saída.

R. Normalmente, não consegue ver todos os caminhos Multipath indica um problema com o daemon de múltiplos caminhos hello e mais provável é que qualquer problema aqui está na saudação `multipath.conf` arquivo.

Também seria vale a pena verificar que você poderá ver alguns discos depois de conectar o destino toohello, como sem resposta das listagens de vários caminhos Olá também pode significar que não tem discos.

* Use Olá barramento SCSI do comando toorescan Olá a seguir:
  
    `$ rescan-scsi-bus.sh `(parte do pacote sg3_utils)
* Digite hello comandos a seguir:
  
    `$ dmesg | grep sd*`
     
     Ou
  
    `$ fdisk –l`
  
    Eles retornarão detalhes de discos adicionados recentemente.
* toodetermine se for um disco de StorSimple, use Olá comandos a seguir:
  
    `cat /sys/block/<DISK>/device/model`
  
    Isso retornará uma cadeia de caracteres, o que determinará se é um disco StorSimple.

Uma causa menos provável, mas possível, também poderia ser um pid iscsid obsoleto. Use Olá toolog de comando a seguir logoff das sessões de iSCSI hello:

    iscsiadm -m node --logout -p <Target_IP>

Repita esse comando para todas as interfaces de rede Olá conectado no destino de iSCSI hello, que é seu dispositivo StorSimple. Depois que você fez logoff de todas as sessões de iSCSI hello, use a sessão de iSCSI Olá de tooreestablish IQN de destino iSCSI de hello. Digite hello comando a seguir:

    iscsiadm -m node --login -T <TARGET_IQN>


P. Não sei se meu dispositivo está na lista branca.

R. tooverify se o dispositivo está na lista de permissões, use Olá comando interativo de solução de problemas a seguir:

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


Para obter mais informações, vá muito[usar um comando interativo para vários caminhos de solução de problemas](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).

## <a name="list-of-useful-commands"></a>Lista de comandos úteis
| Digite  | Command | Descrição |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |Iniciar o serviço iSCSI |
| &nbsp; |`service iscsid stop` |Parar o serviço iSCSI |
| &nbsp; |`service iscsid restart` |Reiniciar o serviço iSCSI |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |Descobrir os destinos disponíveis no hello especificado endereço |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Faça logon no destino de iSCSI toohello |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Faça logoff do destino de iSCSI Olá |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |Imprimir o nome do iniciador iSCSI |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Verificar Olá estado de sessão de iSCSI hello e volume descoberto no host de saudação |
| &nbsp; |`iscsi –m session` |Mostra todas as sessões de iSCSI Olá estabelecidas entre o host de saudação e o dispositivo StorSimple Olá |
|  | | |
| **Múltiplos caminhos** |`service multipathd start` |Iniciar o daemon de vários caminhos |
| &nbsp; |`service multipathd stop` |Parar o daemon de vários caminhos |
| &nbsp; |`service multipathd restart` |Reiniciar o daemon de vários caminhos |
| &nbsp; |`chkconfig multipathd on` </br> OU </br> `mpathconf –with_chkconfig y` |Habilitar vários caminhos daemon toostart no momento da inicialização |
| &nbsp; |`multipathd –k` |Inicie o console interativo de saudação para solução de problemas |
| &nbsp; |`multipath –l` |Listar as conexões e dispositivos de vários caminhos |
| &nbsp; |`mpathconf --enable` |Criar um arquivo mulitpath.conf de exemplo `/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>Próximas etapas
Como você está configurando o MPIO no host do Linux, talvez seja necessário também toohello toorefer 6.6 CentoS documentos a seguir:

* [Configurando o MPIO no CentOS](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Guia de treinamento do Linux](http://linux-training.be/files/books/LinuxAdm.pdf)

