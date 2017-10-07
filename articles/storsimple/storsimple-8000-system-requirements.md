---
title: requisitos de sistema aaaStorSimple 8000 series | Microsoft Docs
description: "Descreve os requisitos e as práticas recomendadas para software, alta disponibilidade e rede para uma solução do Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: f13ccdb7cb317d72c60e9c2fe49937764d10b43e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-software-high-availability-and-networking-requirements"></a>Requisitos de software, de alta disponibilidade e de rede do StorSimple série 8000

## <a name="overview"></a>Visão geral

Bem-vindo tooMicrosoft StorSimple do Azure. Este artigo descreve os requisitos de sistema importantes e práticas recomendadas para seu dispositivo StorSimple e para clientes de armazenamento Olá Olá dispositivo acessado. Recomendamos que você analise Olá informações cuidadosamente antes de implantar o sistema StorSimple e, em seguida, voltar tooit conforme necessário durante a implantação e operação subsequente.

requisitos do sistema Olá incluem:

* **Requisitos de software para clientes de armazenamento** -descreve os sistemas operacionais de saudação com suporte e quaisquer requisitos adicionais para esses sistemas operacionais.
* **Requisitos de rede para o dispositivo StorSimple Olá** -fornece informações sobre portas de saudação que toobe necessidade aberto no tooallow seu firewall para tráfego iSCSI, nuvem ou gerenciamento.
* **Requisitos de alta disponibilidade para o StorSimple** - descreve os requisitos de alta disponibilidade e as práticas recomendadas para o dispositivo StorSimple e o computador host.

## <a name="software-requirements-for-storage-clients"></a>Requisitos de software para clientes de armazenamento

Olá seguindo os requisitos de software é Olá para clientes de armazenamento que acessam seu dispositivo StorSimple.

| Sistemas operacionais com suporte | Versão necessária | Requisitos/observações adicionais |
| --- | --- | --- |
| Windows Server |2008 R2 SP1, 2012, 2012 R2, 2016 |Volumes StorSimple iSCSI são suportados para uso em apenas Olá seguintes tipos de disco do Windows:<ul><li>Volume simples em disco básico</li><li>Volume simples e espelhado em disco dinâmico</li></ul>Há suporte para apenas Olá iniciadores de software iSCSI presentes nativamente no sistema operacional de saudação. Não há suporte para iniciadores iSCSI de hardware.<br></br>O provisionamento dinâmico do Windows Server 2012 e 2016, bem como de recursos ODX terá suporte se você estiver usando um volume iSCSI do StorSimple.<br><br>O StorSimple pode criar volumes com provisionamento dinâmico e provisionamento completo. Não é possível criar volumes parcialmente provisionados.<br><br>Reformatar um volume de provisionamento dinâmico pode levar muito tempo. É recomendável excluir volume hello e, em seguida, criar um novo em vez de reformatar. No entanto, se você ainda preferir tooreformat um volume:<ul><li>Execute Olá comando antes de atrasos de reclamação de espaço do hello reformatar tooavoid a seguir: <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Depois de saudação formatação for concluída, comando a seguir do uso Olá toore habilitar recuperação de espaço:<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>Aplique o hotfix de saudação do Windows Server 2012 conforme descrito em [2878635 KB](https://support.microsoft.com/kb/2870270) tooyour computador com Windows Server.</li></ul></li></ul></ul> Se você estiver configurando o Gerenciador de instantâneos do StorSimple ou do adaptador StorSimple para SharePoint, vá muito[requisitos de Software para os componentes opcionais](#software-requirements-for-optional-components). |
| VMware ESX |5.5 e 6.0 |Compatível com o VMware vSphere como cliente iSCSI. O recurso de bloco VAAI é compatível com o VMware vSphere nos dispositivos StorSimple. |
| Linux RHEL/CentOS |5, 6 e 7 |Suporte para os clientes Linux iSCSI com o iniciador open-iSCSI versões 5, 6 e 7. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> O IBM AIX não é suportado atualmente com o StorSimple.


## <a name="software-requirements-for-optional-components"></a>Requisitos de software para os componentes opcionais

Olá, requisitos de software a seguir é para componentes de StorSimple opcionais hello (Gerenciador de instantâneos do StorSimple e adaptador StorSimple para SharePoint).

| Componente | Plataforma de host | Requisitos/observações adicionais |
| --- | --- | --- |
| Gerenciador de instantâneos do StorSimple |Windows Server 2008 R2 SP1, 2012, 2012 R2 |O uso do Gerenciador de Instantâneos do StorSimple no Windows Server é necessário para fazer backup/restauração dos discos dinâmicos espelhados e quaisquer backups consistentes com o aplicativo.<br> Há suporte para o StorSimple Snapshot Manager apenas no Windows Server 2008 R2 SP1 (64 bits), no Windows Server 2012 R2 e no Windows Server 2012.<ul><li>Se você estiver usando o Windows Server 2012, instale o .NET 3.5 – 4.5 antes de instalar o StorSimple Snapshot Manager.</li><li>Se você estiver usando o Windows Server 2008 R2 SP1, você deve instalar o Windows Management Framework 3.0 antes de instalar o StorSimple Snapshot Manager.</li></ul> |
| Adaptador do StorSimple para SharePoint |Windows Server 2008 R2 SP1, 2012, 2012 R2 |<ul><li>Há suporte para o adaptador StorSimple para SharePoint somente no SharePoint 2010 e no SharePoint 2013.</li><li>O RBS exige o SQL Server Enterprise Edition, versão 2008 R2 ou 2012.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>Requisitos de rede para seu dispositivo StorSimple

Seu dispositivo StorSimple é um dispositivo bloqueado. No entanto, as portas necessário toobe aberto no tooallow seu firewall para tráfego de gerenciamento, iSCSI e nuvem. Olá tabela a seguir lista portas Olá que precisam toobe aberta em seu firewall. Nessa tabela, *na* ou *entrada* refere-se toohello direção na qual a solicitações de cliente recebidas acessar seu dispositivo. *Out* ou *saída* refere-se toohello direção na qual o seu dispositivo StorSimple envia dados externamente, além da implantação Olá: por exemplo, a saída toohello da Internet.

| Nº da porta<sup>1,2</sup> | Entrada ou saída | Escopo da porta | Obrigatório | Observações |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |Saída |WAN |Não |<ul><li>Porta de saída é usada para atualizações de tooretrieve de acesso à Internet.</li><li>proxy da web de saída de saudação é configurável pelo usuário.</li><li>atualizações do sistema tooallow, essa porta também deve estar aberta para Olá IPs fixos do controlador.</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |Saída |WAN |Sim |<ul><li>Porta de saída é usada para acessar dados em nuvem hello.</li><li>proxy da web de saída de saudação é configurável pelo usuário.</li><li>atualizações do sistema tooallow, essa porta também deve estar aberta para Olá IPs fixos do controlador.</li><li>Esta porta também é usada em ambos os controladores Olá para coleta de lixo.</li></ul> |
| UDP 53 (DNS) |Saída |WAN |Em alguns casos; consulte as observações. |Esta porta só será necessária se você estiver usando um servidor DNS baseado na Internet. |
| UDP 123 (NTP) |Saída |WAN |Em alguns casos; consulte as observações. |Esta porta é necessária apenas se você estiver usando um servidor NTP baseado na Internet. |
| TCP 9354 |Saída |WAN |Sim |porta de saída de saudação é usada por Olá toocommunicate de dispositivo StorSimple com hello serviço do Gerenciador de dispositivos do StorSimple. |
| 3260 (iSCSI) |Nesse |LAN |Não |Esta porta é usada tooaccess dados por iSCSI. |
| 5985 |Nesse |LAN |Não |Porta de entrada é usada pelo Gerenciador de instantâneos StorSimple toocommunicate com o dispositivo StorSimple hello.<br>Esta porta também é usada quando você se conectar remotamente tooWindows PowerShell para StorSimple via HTTP. |
| 5986 |Nesse |LAN |Não |Esta porta é usada quando você se conectar remotamente tooWindows PowerShell para StorSimple em HTTPS. |

<sup>1</sup> toobe aberto em não precisa de nenhuma porta de entrada hello Internet pública.

<sup>2</sup> se várias portas transportarem uma configuração de gateway, a ordem de tráfego roteado de saída de hello será determinada com base na ordem de roteamento de porta do hello descrito em [porta roteamento](#routing-metric), abaixo.

<sup>3</sup> controlador Olá IPs fixo em seu dispositivo StorSimple deve ser roteável e capaz de tooconnect toohello Internet diretamente ou por meio de saudação configurado proxy da web. endereços IP de Olá fixo são usados para manutenção de dispositivo de toohello atualizações hello. Se os controladores de dispositivo de saudação não podem conectar toohello IPs fixos de Internet por meio de hello, não será capaz de tooupdate seu dispositivo StorSimple.

> [!IMPORTANT]
> Verifique se o firewall Olá não modificar ou descriptografar qualquer tráfego SSL entre o dispositivo StorSimple hello e o Azure.


### <a name="url-patterns-for-firewall-rules"></a>Padrões de URL para regras de firewall

Os administradores de rede geralmente podem configurar regras com base em Olá Olá de toofilter de padrões de URL de entrada e o tráfego de saída de hello avançadas do firewall. Seu dispositivo StorSimple e hello serviço do Gerenciador de dispositivos de StorSimple dependem de outros aplicativos da Microsoft, como o Azure Service Bus, controle de acesso do Azure Active Directory, contas de armazenamento e servidores do Microsoft Update. padrões de URL Olá associados a esses aplicativos podem ser usados tooconfigure as regras de firewall. É importante toounderstand que podem alterar os padrões de URL Olá associados a esses aplicativos. Isso por sua vez exigem Olá toomonitor de administrador de rede e atualizar regras de firewall para o StorSimple como e quando necessário.

É recomendável que você defina suas regras de firewall para tráfego de saída, com base nos endereços IP fixos do StorSimple e, na maioria dos casos, de modo flexível. No entanto, você pode usar informações de saudação abaixo tooset avançadas de regras de firewall que são ambientes seguros toocreate necessários.

> [!NOTE]
> dispositivo de saudação (origem) IPs deve sempre ser definido interfaces de rede tooall Olá habilitado. destino de saudação IPs deve ser definido muito[intervalos IP do datacenter do Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).


#### <a name="url-patterns-for-azure-portal"></a>Padrões de URL para o Portal do Azure

| Padrão de URL | Componente/funcionalidade | IPs de dispositivo |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*`<br>`https://login.windows.net` |Serviço do Gerenciador de Dispositivos StorSimple<br>Access Control Service<br>Barramento de Serviço do Azure<br>Serviço de autenticação |Interfaces de rede habilitadas para nuvem |
| `https://*.backup.windowsazure.com` |Registro de dispositivos |Somente DATA 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revogação de certificado |Interfaces de rede habilitadas para nuvem |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Contas de armazenamento e monitoramento do Azure |Interfaces de rede habilitadas para nuvem |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Servidores do Microsoft Update<br> |IPs fixados pelo controlador somente |
| `http://*.deploy.akamaitechnologies.com` |CDN do Akamai |IPs fixados pelo controlador somente |
| `https://*.partners.extranet.microsoft.com/*`<br>`https://dcupload.microsoft.com/`<br>`https://*.support.microsoft.com/` |Pacote de suporte |Interfaces de rede habilitadas para nuvem |

#### <a name="url-patterns-for-azure-government-portal"></a>Padrões de URL para o portal Azure Governamental

| Padrão de URL | Componente/funcionalidade | IPs de dispositivo |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*`<br>`https://login-us.microsoftonline.com` |Serviço do Gerenciador de Dispositivos StorSimple<br>Access Control Service<br>Barramento de Serviço do Azure<br>Serviço de autenticação |Interfaces de rede habilitadas para nuvem |
| `https://*.backup.windowsazure.us` |Registro de dispositivos |Somente DATA 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revogação de certificado |Interfaces de rede habilitadas para nuvem |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Contas de armazenamento e monitoramento do Azure |Interfaces de rede habilitadas para nuvem |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Servidores do Microsoft Update<br> |IPs fixados pelo controlador somente |
| `http://*.deploy.akamaitechnologies.com` |CDN do Akamai |IPs fixados pelo controlador somente |
| `https://*.partners.extranet.microsoft.com/*`<br>`https://dcupload.microsoft.com/`<br>`https://*.support.microsoft.com/` |Pacote de suporte |Interfaces de rede habilitadas para nuvem |

### <a name="routing-metric"></a>Métrica de roteamento

Uma métrica de roteamento está associada com interfaces de saudação e gateway Olá Olá toohello de dados especificado para rotear redes. Métrica de roteamento é usada pelo Olá roteamento protocolo toocalculate Olá melhor caminho tooa dado de destino, se ele conhecer vários caminhos existem toohello mesmo destino. Olá inferior Olá roteamento métrica, Olá Olá preferência maior.

No hello contexto do StorSimple, se várias interfaces de rede e gateways configurado toochannel tráfego, métricas de roteamento Olá entram toodetermine Olá relativo ordem de execução no qual Olá interfaces obter usadas. métrica de roteamento Olá não pode ser alterada pelo usuário hello. No entanto, você pode usar Olá `Get-HcsRoutingTable` tooprint cmdlet Olá tabela de roteamento (e métricas) em seu dispositivo StorSimple. Mais informações sobre o cmdlet Get-HcsRoutingTable em [Troubleshooting StorSimple deployment](storsimple-troubleshoot-deployment.md)(Solucionando problemas de implantação do StorSimple).

Olá métrica algoritmo de roteamento usado para a atualização 2 e versões posteriores pode ser explicado como.

* Um conjunto de valores predefinidos atribuiu toonetwork interfaces.
* Considere uma tabela de exemplo mostrada abaixo com valores atribuídos toohello várias interfaces de rede quando eles são habilitados para a nuvem ou nuvem-desabilitado, mas com um gateway configurado. Os valores de saudação Observação atribuídos aqui são apenas os valores de exemplo.

    | Interface de rede | Habilitado para nuvem | Desabilitado para a nuvem com o gateway |
    |-----|---------------|---------------------------|
    | Dados 0  | 1            | -                        |
    | Dados 1  | 2            | 20                       |
    | Dados 2  | 3            | 30                       |
    | Dados 3  | 4            | 40                       |
    | Dados 4  | 5            | 50                       |
    | Dados 5  | 6            | 60                       |


* ordem de saudação tráfego de nuvem hello será roteado por meio das interfaces de rede de saudação é:
  
    *Dados 0 > Dados 1 > Dados 2 > Dados 3 > Dados 4 > Dados 5*
  
    Isso pode ser explicado por Olá exemplo a seguir.
  
    Considere um dispositivo do StorSimple com duas interfaces de rede habilitadas para a nuvem, Data 0 e Data 5. Data 1 a 4 são desabilitados para a nuvem, mas têm um gateway configurado. ordem de saudação tráfego será roteado para este dispositivo será:
  
    *Dados 0 (1) > Dados 5 (6) > Dados 1 (20) > Dados 2 (30) > Dados 3 (40) > Dados 4 (50)*
  
    *Olá números entre parênteses indicam métricas roteamento do respectivos hello.*
  
    Se a Data 0 falhar, o tráfego de nuvem Olá será roteado até dados 5. Considerando que um gateway é configurado em outra rede, se a Data 0 e Data 5 foram toofail, tráfego de nuvem Olá passará por Data 1.
* Se uma interface de rede habilitados para a nuvem falhar, em seguida, são 3 tentativas com 30 segundo atraso tooconnect toohello interface. Se todas as tentativas de saudação falharem, tráfego Olá é roteado toohello próximo disponível habilitado para a nuvem interface conforme determinado pela tabela de roteamento de saudação. Se todos os Olá habilitado para a nuvem interfaces de rede falharem, dispositivo Olá irão falhar toohello outro controlador (nenhuma reinicialização neste caso).
* Se houver uma falha de VIP para uma interface de rede habilitada para iSCSI, haverá três tentativas com um atraso de 2 segundos. Esse comportamento foi Olá mesmo de versões anteriores do hello. Se todas as interfaces de rede iSCSI Olá falharem, um failover de controlador ocorrerá (acompanha por uma reinicialização).
* Um alerta também será gerado no dispositivo do StorSimple quando houver uma falha de VIP. Para obter mais informações, vá muito[referência rápida de alerta](storsimple-8000-manage-alerts.md).
* Quanto às repetições, o iSCSI terá precedência sobre a nuvem.
  
    Considere Olá exemplo a seguir: StorSimple um dispositivo tem duas interfaces de rede habilitadas, dados 0 e 1 de dados. Data 0 é habilitado para a nuvem, enquanto Data 1 é habilitado para a nuvem e para iSCSI. Nenhuma outra interface de rede neste dispositivo é habilitada para a nuvem ou para iSCSI.
  
    Se falhar de dados 1, considerando-última interface de rede iSCSI hello, isso resultará em um tooData de failover do controlador 1 Olá no outro controlador.

### <a name="networking-best-practices"></a>Práticas recomendadas de rede

Além disso toohello acima requisitos de rede, para desempenho ideal de saudação da sua solução StorSimple, cumpra toohello práticas recomendadas a seguir:

* Verifique se o dispositivo StorSimple tem uma largura de banda dedicada de 40 Mbps (ou mais) disponível sempre. Essa largura de banda não deve ser compartilhada (ou alocação deve ser garantida por meio do uso de saudação das políticas de QoS) com outros aplicativos.
* Certifique-se de que toohello de conectividade de rede da Internet está disponível em todos os momentos. Esporádicos ou não confiáveis Internet conexões toohello dispositivos, não incluindo nenhuma conectividade com a Internet natureza, resulta em uma configuração sem suporte.
* Isole o tráfego iSCSI e nuvem Olá tendo interfaces de rede em seu dispositivo para acesso iSCSI e nuvem dedicadas. Para obter mais informações, consulte como muito[modificar interfaces de rede](storsimple-8000-modify-device-config.md#modify-network-interfaces) em seu dispositivo StorSimple.
* Não use uma configuração do LACP (Protocolo de controle de agregação de links) para as suas interfaces de rede. Essa é uma configuração sem suporte.

## <a name="high-availability-requirements-for-storsimple"></a>Requisitos de alta disponibilidade para o StorSimple

plataforma de hardware de saudação que acompanha a solução do StorSimple Olá possui recursos de disponibilidade e confiabilidade que fornecem uma base para uma infraestrutura de armazenamento altamente disponível e tolerante a falhas no seu datacenter. No entanto, existem requisitos e práticas recomendadas que você deve cumprir toohelp garantem a disponibilidade de saudação da sua solução StorSimple. Antes de implantar StorSimple, revise atentamente Olá seguindo os requisitos e práticas recomendadas para o dispositivo StorSimple hello e conectar os computadores de host.

Para obter mais informações sobre como monitorar e manter componentes de hardware de saudação do seu dispositivo StorSimple, ir muito[usar componentes de hardware toomonitor do serviço de Gerenciador de dispositivos de StorSimple hello e status](storsimple-8000-monitor-hardware-status.md) e [ Substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>Requisitos de alta disponibilidade e procedimentos para seu dispositivo StorSimple

Olá revisar informações a seguir atentamente tooensure Olá alta disponibilidade do seu dispositivo StorSimple.

#### <a name="pcms"></a>PCMs

Os dispositivos StorSimple incluem módulos redundantes, intercambiáveis e de refrigeração (PCMs). Cada PCM possui suficiente serviço de tooprovide de capacidade para Olá todo chassi. alta disponibilidade tooensure, ambos os PCMs deve ser instalada.

* Conecte-se a disponibilidade de tooprovide PCMs toodifferent power fontes se uma fonte de alimentação falhar.
* Se um PCM falhar, solicite uma substituição imediatamente.
* Remover um PCM com defeito somente quando você tem de substituição hello e está pronto tooinstall-lo.
* Não remova os dois PCMs simultaneamente. módulo do PCM Olá inclui o módulo de bateria de backup hello. Remover ambos de saudação PCMs resultará em um desligamento sem proteção de bateria e estado do dispositivo Olá não serão salvas. Para obter mais informações sobre a bateria hello, vá muito[módulo de bateria de backup Olá manter](storsimple-8000-battery-replacement.md#maintain-the-backup-battery-module).

#### <a name="controller-modules"></a>Módulos do controlador

Os dispositivos StorSimple incluem módulos de controlador redundantes e intercambiáveis. módulos do controlador Olá operam em um modo ativo/passivo. A qualquer momento determinado, um módulo do controlador está ativo e fornece serviço, durante a saudação outro módulo do controlador está passivo. módulo do controlador passivo Hello está ligado e se torna operacional se o módulo do controlador ativo Olá falha ou for removido. Cada módulo do controlador tem suficiente serviço de tooprovide de capacidade para Olá todo chassi. Os módulos do controlador devem ser instalado tooensure alta disponibilidade.

* Certifique-se de que os dois módulos do controlador estejam sempre instalados.
* Se um módulo do controlador falhar, solicite uma substituição imediatamente.
* Remover um módulo do controlador com falha somente quando você tem de substituição hello e está pronto tooinstall-lo. Remover um módulo por longos períodos afetar o fluxo de ar Olá e, portanto, Olá resfriamento do sistema de saudação.
* Certifique-se de que os módulos de saudação rede conexões tooboth controlador são idênticos e hello, interfaces de rede conectadas possuem uma configuração de rede idênticos.
* Se um módulo do controlador falha ou precisa de substituição, certifique-se de que Olá outro módulo do controlador está em um estado ativo antes de substituir o módulo do controlador com falha hello. tooverify que um controlador está ativo, ir muito[identificar controlador ativo do hello em seu dispositivo](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device).
* Não remova os módulos do controlador no hello simultaneamente. Se um failover de controlador estiver em andamento, não desligue Olá módulo do controlador em espera ou remova-o do chassi de saudação.
* Após o failover do controlador, aguarde pelo menos cinco minutos antes de remover um dos módulos de controlador.

#### <a name="network-interfaces"></a>Interfaces de rede

Cada módulo de controlador do dispositivo StorSimple tem quatro interfaces de rede Ethernet de 1 Gigabit e duas de 10 Gigabits.

* Certifique-se de que módulos do controlador Olá rede conexões tooboth são idênticos e interfaces de rede de saudação interfaces do módulo do controlador Olá são conectado toohave uma configuração de rede idênticos.
* Quando possível, implante conexões de rede entre a disponibilidade do serviço tooensure opções diferentes no evento de saudação de uma falha de dispositivo de rede.
* Ao desconectar Olá somente ou Olá última restante interface habilitada com iSCSI (com IPs atribuídos), desabilitar a interface Olá primeiro e, em seguida, desconecte os cabos de saudação. Se a interface Olá estiver desconectado, primeiro, isso causará Olá controlador ativo toofail sobre o controlador passivo toohello. Se o controlador passivo Olá também tem suas interfaces correspondentes desconectados, os dois controladores Olá serão reiniciado várias vezes antes de se estabelecer em um controlador.
* Conecte-se pelo menos duas redes de toohello de interfaces de dados de cada módulo do controlador.
* Se você habilitou as interfaces do hello duas de 10 GbE, implante-as em diferentes comutadores.
* Quando possível, use o MPIO nos servidores tooensure que servidores Olá podem tolerar um link, rede ou falhas de interface.

Para obter mais informações sobre a rede de alta disponibilidade e desempenho do seu dispositivo, vá muito[instalar seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [instalar seu dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

#### <a name="ssds-and-hdds"></a>SSDs e HDDs

Dispositivos StorSimple incluem discos de estado sólido (SSDs) e unidades de disco rígido (HDDs) protegidos com espaços espelhados. Uso de espaços espelhados garante que o dispositivo Olá tootolerate capaz de falha de saudação de um ou mais SSDs ou HDDs.

* Certifique-se de que todos os módulos SSD e HDD estejam instalados.
* Se um SSD ou HDD falhar, solicite uma substituição imediatamente.
* Se um SSD ou HDD falha ou exige substituição, certifique-se de que você remova apenas Olá SSD ou HDD que exige substituição.
* Não remova mais de um SSD ou HDD do sistema hello em qualquer ponto no tempo.
  Uma falha de dois ou mais discos de determinado tipo (HDD, SSD) ou uma falha consecutiva em um curto período pode resultar em mau funcionamento do sistema e possível perda de dados. Se isso ocorrer, [entre em contato com o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md) para obter assistência.
* Durante a substituição, monitore Olá **componentes compartilhados** em Olá **a integridade do Hardware** folha para Olá unidades no hello SSDs e HDDs. Um status de verificação verde indica que os discos Olá estão íntegros ou Okey, enquanto o ponto de um ponto de exclamação vermelho indica uma falha SSD ou HDD.
* É recomendável que você configure instantâneos na nuvem para todos os volumes que você precisa tooprotect em caso de falha do sistema.

#### <a name="ebod-enclosure"></a>Compartimento EBOD

Modelo do dispositivo StorSimple 8600 inclui um compartimento Extended Bunch de discos (EBOD) no compartimento primário do toohello de adição. Um EBOD contém controladores EBOD e HDDs (unidades de disco rígido) protegidos por espaços espelhados. Uso de espaços espelhados garante que o dispositivo Olá tootolerate capaz de falha de saudação de um ou mais HDDs. Olá compartimento EBOD é conectado toohello o compartimento principal por meio de cabos SAS redundantes.

* Certifique-se de que ambos os módulos do controlador EBOD, ambos os cabos SAS e todas as unidades de disco rígido Olá estão instalados em todos os momentos.
* Se um módulo do controlador de compartimento EBOD falhar, solicite uma substituição imediatamente.
* Se um módulo do controlador de compartimento EBOD falhar, certifique-se de que Olá outro módulo do controlador está ativo antes de substituir o módulo com falha hello. tooverify que um controlador está ativo, ir muito[identificar controlador ativo do hello em seu dispositivo](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device).
* Durante uma substituição de módulo do controlador EBOD, monitorar continuamente o status de saudação de componente Olá Olá serviço do Gerenciador de dispositivos de StorSimple acessando **Monitor** > **a integridade do Hardware** .
* Se um cabo SAS falha ou precisa de substituição (Microsoft Support deve ser envolvido toomake desta decisão), certifique-se de que você remova apenas cabo SAS Olá que exige substituição.
* Não simultaneamente Remova ambos os cabos SAS do sistema de saudação em qualquer ponto no tempo.

### <a name="high-availability-recommendations-for-your-host-computers"></a>Recomendações de alta disponibilidade para os computadores de host

Leia com atenção essas melhores práticas tooensure Olá alta disponibilidade do dispositivo do hosts conectados tooyour StorSimple.

* Defina o StorSimple com as [configurações de cluster de servidores de arquivos com dois nós][1]. Removendo pontos únicos de falha e a criação de redundância no lado do host hello, a solução inteira Olá torna-se altamente disponível.
* Use continuamente disponíveis (CA) de compartilhamentos disponíveis com o Windows Server 2012 (SMB 3.0) para alta disponibilidade durante o failover dos controladores de armazenamento hello. Para obter informações adicionais para configurar clusters de servidor de arquivos e compartilhamentos continuamente disponíveis com o Windows Server 2012, consulte toothis [demonstração em vídeo](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares).

## <a name="next-steps"></a>Próximas etapas

* [Saiba mais sobre os limites do sistema StorSimple](storsimple-8000-limits.md).
* [Saiba como toodeploy sua solução StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx
