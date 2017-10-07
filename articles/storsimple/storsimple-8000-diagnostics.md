---
title: dispositivo de tootroubleshoot StorSimple 8000 ferramenta aaaDiagnostics | Microsoft Docs
description: "Descreve os modos do dispositivo StorSimple hello e explica como toouse do Windows PowerShell para StorSimple toochange Olá modo de dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>Use Olá ferramenta de diagnóstico do StorSimple tootroubleshoot 8000 series problemas do dispositivo

## <a name="overview"></a>Visão geral

Olá, ferramenta de diagnóstico de StorSimple diagnostica toosystem relacionados problemas, desempenho, rede e integridade dos componentes de hardware para um dispositivo StorSimple. ferramenta de diagnóstico de saudação pode ser usada em vários cenários. Esses cenários incluem a carga de trabalho de planejamento, implantação de um dispositivo StorSimple, avaliar o ambiente de rede de saudação e determinação do desempenho de saudação de um dispositivo operacional. Este artigo fornece uma visão geral da ferramenta de diagnóstico de saudação e descreve como a ferramenta Olá pode ser usada com um dispositivo StorSimple.

ferramenta de diagnóstico de saudação é usado principalmente para dispositivos de locais de série StorSimple 8000 (8100 e 8600).

## <a name="run-diagnostics-tool"></a>Execute a ferramenta de diagnóstico

Essa ferramenta pode ser executada por meio da interface do Windows PowerShell de saudação do seu dispositivo StorSimple. Há duas maneiras tooaccess Olá interface local do seu dispositivo:

* [Console serial do dispositivo usar PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
* [Acessar remotamente a ferramenta Olá por meio de saudação do Windows PowerShell para StorSimple](storsimple-remote-connect.md).

Neste artigo, vamos supor que você está conectado toohello console serial do dispositivo por meio do PuTTY.

#### <a name="toorun-hello-diagnostics-tool"></a>ferramenta de diagnóstico de saudação toorun

Depois que você se conectou a interface do Windows PowerShell toohello do dispositivo hello, execute Olá etapas toorun Olá cmdlet a seguir.
1. Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).

2. Digite hello comando a seguir:

    `Invoke-HcsDiagnostics`

    Se o parâmetro de escopo de saudação não for especificado, o cmdlet de Olá executa todos os testes de diagnóstico de saudação. Esses testes incluem a integridade de componentes de hardware, sistema, rede e desempenho. 
    
    toorun apenas um teste específico, especifique o parâmetro de escopo de hello. Por exemplo, toorun somente Olá teste de rede, tipo

    `Invoke-HcsDiagnostics -Scope Network`

3. Selecione e copie a saída de hello da saudação PuTTY janela em um arquivo de texto para análise posterior.

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>Ferramenta de diagnóstico cenários toouse Olá

Use Olá diagnóstico ferramenta tootroubleshoot Olá rede, o desempenho, o sistema e o hardware integridade do sistema de saudação. Aqui estão alguns cenários possíveis:

* **Dispositivo offline** - Seu dispositivo da série StorSimple 8000 dispositivo está offline. No entanto, na interface do Windows PowerShell hello, parece que ambos os controladores Olá estão em funcionamento.
    * Você pode usar essa ferramenta toothen determinar o estado da rede hello.
         
         > [!NOTE]
         > Não use esse desempenho de tooassess de ferramenta e as configurações de rede em um dispositivo antes de registro hello (ou configurar por meio do Assistente de instalação). Um IP válido é atribuído toohello dispositivo durante o registro e o Assistente de instalação. Você pode executar este cmdlet em um dispositivo que não está registrado para verificar a integridade do hardware e do sistema. Use o parâmetro de escopo hello, por exemplo:
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **Problemas de dispositivo persistente** -você estiver tendo problemas de dispositivo que parecem toopersist. Por exemplo, ocorre um erro ao fazer o registro. Você pode também ter problemas dispositivo depois que o dispositivo hello está operacional e registrado com êxito por um tempo.
    * Nesse caso, use essa ferramenta para uma solução de problemas preliminar antes de fazer uma solicitação de serviço o Suporte da Microsoft. É recomendável que você execute essa saída Olá ferramenta e a captura dessa ferramenta. Em seguida, você pode fornecer essa saída tooSupport tooexpedite de solução de problemas.
    * Se houver qualquer falha de um componente ou cluster de hardware, você deve fazer uma solicitação de suporte.

* **Baixo desempenho do dispositivo** - O dispositivo StorSimple está muito lento.
    * Nesse caso, execute este cmdlet com tooperformance de conjunto de parâmetros de escopo. Analise a saída de hello. Você obtém nuvem Olá latências de leitura / gravação. Olá Use relatado latências como destino viável máximo, leve em alguma sobrecarga de processamento de dados interno do hello e implantar cargas de trabalho Olá no sistema de saudação. Para obter mais informações, vá muito[usar Olá rede teste tootroubleshoot dispositivo desempenho](#network-test).


## <a name="diagnostics-test-and-sample-outputs"></a>Saídas de exemplo e teste de diagnóstico

### <a name="hardware-test"></a>Teste de hardware

Esse teste determina o status de Olá Olá componentes de hardware, firmware USM de Olá e firmware de disco Olá em execução no seu sistema.

* componentes de hardware de saudação relatados são os componentes desse teste Olá com falha ou não estão presentes no sistema de saudação.
* versões de firmware Olá USM firmware e do disco são relatadas para Olá controlador 0, o controlador 1 e componentes compartilhados no seu sistema. Para obter uma lista completa dos componentes de hardware, vá para:

    * [Componentes no compartimento principal](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [Componentes no compartimento EBOD](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> Se os componentes com falha, relatórios de teste de hardware Olá [de log em uma solicitação de serviço com o Microsoft Support](storsimple-contact-microsoft-support.md).

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>Exemplo de saída de uma execução de teste de hardware em um dispositivo 8100

Aqui está um exemplo de saída de um dispositivo StorSimple 8100. Olá compartimento EBOD não está presente no dispositivo de modelo 8100 hello. Portanto, os componentes do controlador EBOD Olá não são relatados.

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>Teste do sistema

Esse teste relata informações do sistema hello, Olá atualizações disponíveis, informações de saudação do cluster e informações de serviço Olá para seu dispositivo.

* informações do sistema Olá incluem modelo hello, número de série do dispositivo, fuso horário, status do controlador e versão do hello detalhadas do software em execução no sistema de saudação. Olá toounderstand vários parâmetros do sistema relatados como saída de hello, ir muito[interpretar as informações do sistema](#appendix-interpreting-system-information).

* relatórios de disponibilidade de atualização de saudação se modos de saudação normais e de manutenção estão disponíveis e seus nomes de pacote associado. Se `RegularUpdates` e `MaintenanceModeUpdates` são `false`, isso indica que as atualizações de saudação não estão disponíveis. Seu dispositivo está atualizado.
* informações de cluster Olá contém informações de saudação em vários componentes lógicos de todos os grupos de cluster HCS hello e seus respectivos status. Se você vir um grupo de cluster offline nesta seção do relatório hello, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md).
* informações do serviço de saudação incluem nomes de saudação e status de todos os hello HCS e serviços de CiS em execução no seu dispositivo. Essas informações são úteis para Olá Microsoft Support na solução de problema de dispositivo de saudação.

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>Exemplo de saída de uma execução de teste do sistema em um dispositivo 8100

Aqui está um exemplo de saída do teste de sistema Olá executado em um dispositivo 8100.

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>Teste de rede

Esse teste valida Olá status de interfaces de rede Olá, portas, DNS e NTP conectividade do servidor, SSL certificado, as credenciais de conta de armazenamento, servidores de Update toohello conectividade e conectividade de proxy da web em seu dispositivo StorSimple.

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>Exemplo de saída do teste de rede quando somente DATA0 está habilitado

Aqui está um exemplo de saída do dispositivo 8100 hello. Você pode ver na saída de hello que:
* Somente as interfaces de rede DATA 0 e DATA 1 estão ativadas e configuradas.
* 2 a 5 de dados não estão habilitados no portal de saudação.
* configuração do servidor DNS Olá é válida e dispositivo Olá pode se conectar por meio do servidor DNS hello.
* Olá conectividade com o servidor NTP também é bom.
* As portas 80 e 443 estão abertas. No entanto, a porta 9354 está bloqueada. Com base em Olá [requisitos de rede do sistema](storsimple-system-requirements.md), você precisa tooopen essa porta para comunicação do barramento de serviço de saudação.
* Olá SSL é válido.
* dispositivo Olá pode se conectar a conta de armazenamento toohello: _myss8000storageacct_.
* servidores de tooUpdate conectividade Olá é válido.
* proxy da web de saudação não está configurado neste dispositivo.

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>Exemplo de saída do teste de rede quando somente DATA0 e DATA1 estão habilitados

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>Teste de desempenho

Esse teste relatórios de desempenho de saudação de nuvem por meio de latências de leitura-gravação de nuvem Olá para seu dispositivo. Essa ferramenta pode ser usada tooestablish uma linha de base de desempenho de saudação de nuvem que você pode obter com o StorSimple. Olá ferramenta Olá máximo desempenho de relatórios (melhor cenário de caso de latências de leitura / gravação) que você pode obter a conexão.

Como a ferramenta Olá relatórios Olá possível obter o desempenho máximo, podemos usar Olá relatada latências de leitura / gravação, como destinos ao implantar Olá cargas de trabalho.

teste Olá simula tamanhos de blob Olá associados a tipos de volume diferente Olá no dispositivo de saudação. Volumes normais em camadas e backups de volumes localmente fixados usam um tamanho de blob de 64 KB. Volumes em camadas com opção de arquivamento marcada usam um tamanho de dados de blob de 512 KB. Se o dispositivo tiver volumes localmente afixados e hierárquicos configurado, somente Olá teste too64 KB blob correspondente tamanho dos dados é executado.

toouse essa ferramenta, execute Olá etapas a seguir:

1.  Primeiro, crie uma mistura de volumes em camadas e em camadas com a opção de arquivamento marcada. Esta ação garante que essa ferramenta Olá executa testes Olá para 64 KB e 512 KB tamanhos de blob.

2. Execute o cmdlet de saudação depois que você criou e configurou volumes hello. Tipo:

    `Invoke-HcsDiagnostics -Scope Performance`

3. Anote as latências de leitura-gravação de Olá relatados pela ferramenta hello. Este teste pode levar vários toorun de minutos antes de relatar os resultados de saudação.

4. Se Olá latências de conexão são todos com hello intervalo esperado, hello latências relatadas pela ferramenta Olá podem ser usadas como destino viável máximo durante a implantação de cargas de trabalho de saudação. Considere uma sobrecarga para o processamento de dados interno.

    Se latências de leitura / gravação da saudação relatado pela ferramenta de diagnóstico de saudação são alta:

    1. Configurar o Storage Analytics para serviços blob e analisar Olá saída toounderstand Olá latências de saudação conta de armazenamento do Azure. Para obter instruções detalhadas, consulte muito[habilitar e configurar o Storage Analytics](../storage/common/storage-enable-and-view-metrics.md). Se as latências também são números de alta e comparável toohello recebida do Olá, ferramenta de diagnóstico de StorSimple, você precisa toolog uma solicitação de serviço com o armazenamento do Azure.

    2. Se as latências de conta de armazenamento Olá baixas, contate seu tooinvestigate do administrador de rede alguma latência problemas em sua rede.

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>Exemplo de saída de uma execução de teste de desempenho em um dispositivo 8100

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>Apêndice: interpretação das informações do sistema

Aqui está uma tabela que descreve quais Olá mapeiam vários parâmetros do Windows PowerShell em informações do sistema Olá para. 

| Parâmetro do PowerShell    | Descrição  |
|-------------------------|------------------|
| ID da instância             | Cada controlador tem um identificador exclusivo ou um GUID associado a ele.|
| Nome                    | nome amigável de saudação do dispositivo Olá conforme configurado por meio de saudação portal do Azure durante a implantação de dispositivo. nome amigável da saudação padrão é o número de série do dispositivo de saudação. |
| Modelo                   | modelo de saudação do seu dispositivo da série StorSimple 8000. modelo de saudação pode ser 8100 ou 8600.|
| SerialNumber            | número de série do dispositivo Olá é atribuído na fábrica hello e 15 caracteres. Por exemplo, 8600-SHX0991003G44HT indica:<br> 8600 – é o modelo de dispositivo de saudação.<br>SHX – é fabricação Olá o site.<br> 0991003 - É um produto específico. <br> G44HT-Olá últimos 5 dígitos são incrementados toocreate números de série exclusivos. Pode ser um conjunto não sequencial de números.|
| timeZone                | Olá fuso horário do dispositivo conforme configurado no hello portal do Azure durante a implantação de dispositivo.|
| CurrentController       | controlador de saudação que você está conectado toothrough interface de Windows PowerShell Olá do seu dispositivo StorSimple.|
| ActiveController        | controlador de saudação que está ativo no seu dispositivo e controla todas as operações de rede e disco hello. Pode ser o Controlador 0 ou Controlador 1.  |
| Controller0Status       | status de saudação do controlador 0 em seu dispositivo. status do controlador Olá pode ser normal, no modo de recuperação, ou está inacessível.|
| Controller1Status       | status de saudação do controlador 1 no seu dispositivo.  status do controlador Olá pode ser normal, no modo de recuperação, ou está inacessível.|
| SystemMode              | Olá status geral do seu dispositivo StorSimple. status do dispositivo Olá pode ser normal, manutenção, ou encerrado (corresponde toodeactivated em Olá portal do Azure).|
| FriendlySoftwareVersion | Olá cadeia de caracteres amigável que corresponde a versão do software de dispositivo toohello. Para um sistema que executa a atualização 4, versão amigável Olá seria StorSimple 8000 Series atualização 4.0.|
| HcsSoftwareVersion      | Olá HCS software versão em execução no seu dispositivo. Por exemplo, Olá tooStorSimple correspondente de versão de software do HCS 8000 Series atualização 4.0 é 6.3.9600.17820. |
| ApiVersion              | versão do software de saudação do hello API do Windows PowerShell do dispositivo HCS de saudação.|
| VhdVersion              | versão do software Olá da imagem de fábrica Olá Olá dispositivo foi fornecido com o. Se você redefinir o dispositivo toofactory padrão, ele executa esta versão do software.|
| OSVersion               | versão do software de saudação do sistema de operacional de servidor Windows hello em execução no dispositivo de saudação. o dispositivo StorSimple Olá Olá Windows Server 2012 R2 que corresponde a too6.3.9600 baseado.|
| CisAgentVersion         | versão de saudação do seu agente de Cis em execução no seu dispositivo StorSimple. Esse agente ajuda a se comunicar com o serviço StorSimple Manager Olá em execução no Azure.|
| MdsAgentVersion         | Olá versão correspondente toohello Mds agente em execução no seu dispositivo StorSimple. Esse agente move dados toohello monitoramento e diagnóstico do serviço (MDS).|
| Lsisas2Version          | Olá drivers toohello LSI correspondente de versão no seu dispositivo StorSimple.|
| Capacity                | capacidade total de saudação do dispositivo Olá em bytes.|
| RemoteManagementMode    | Indica se o dispositivo de saudação pode ser gerenciado remotamente por meio de sua interface do Windows PowerShell. |
| FipsMode                | Indica se o modo de Estados Unidos Federal Information Processing Standard (FIPS) hello está habilitado em seu dispositivo. padrão Olá FIPS 140 define algoritmo de criptografia aprovado para uso pelos sistemas de computador do Governo Federal dos EUA para proteção de saudação de dados confidenciais. Para dispositivos executando a Atualização 4 ou posterior, o modo FIPS está habilitado por padrão. |

## <a name="next-steps"></a>Próximas etapas

* Saiba Olá [sintaxe do cmdlet Invoke-HcsDiagnostics de saudação](https://technet.microsoft.com/library/mt795371.aspx).

* Saiba mais sobre como muito[solucionar problemas de implantação](storsimple-troubleshoot-deployment.md) em seu dispositivo StorSimple.
