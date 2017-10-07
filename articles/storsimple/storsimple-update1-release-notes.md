---
title: "Notas de versão do aaaStorSimple 8000 Series atualização 1.2 | Microsoft Docs"
description: "Descreve novos recursos do hello, problemas e soluções alternativas para o StorSimple 8000 Series atualização 1.2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>Notas de versão da Atualização 1.2 para seu dispositivo StorSimple série 8000

## <a name="overview"></a>Visão geral
Olá notas de versão a seguir descrevem Olá novos recursos e identificam os problemas abertos críticos Olá para o StorSimple 8000 Series atualização 1.2. Eles também contêm uma lista de software do StorSimple hello, driver e atualizações de firmware de disco incluídas nesta versão. 

Atualização 1.2 pode ser aplicado tooany StorSimple dispositivo executando a versão (GA), atualização 0,1, atualização 0,2 ou software de atualização 0.3. A Atualização 1.2 não estará disponível se seu dispositivo estiver executando Atualização 1 ou Atualização 1.1. Se o dispositivo está executando a versão (GA), [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) tooassist você ao instalar essa atualização.

Olá versões de software de dispositivo do tabela listas Olá correspondente tooUpdates 1, 1.1 e 1.2 a seguir.

| Se estiver executando a atualização... | esta é a versão do software do seu dispositivo. |
| --- | --- |
| Atualização 1.2 |6.3.9600.17584 |
| Atualização 1.1 |6.3.9600.17521 |
| Atualização 1.0 |6.3.9600.17491 |

Analise Olá informações contidas na versão Olá notas antes de implantar Olá atualizar em sua solução StorSimple. Para obter mais informações, consulte como muito[instalar atualização 1.2 em seu dispositivo StorSimple](storsimple-install-update-1.md). 

> [!IMPORTANT]
> * Demora cerca de 5 a 10 horas tooinstall essa atualização (incluindo as atualizações do Windows hello). 
> * A Atualização 1.2 tem atualizações de software, do driver LSI e do firmware de disco. tooinstall, siga as instruções de saudação em [instalar atualização 1.2 em seu dispositivo StorSimple](storsimple-install-update-1.md).
> * Para novas versões, você poderá não ver atualizações imediatamente porque fazemos uma distribuição em fases de saudação atualizações. Procure atualizações em poucos dias novamente, uma vez que elas serão disponibilizadas em breve.
> 
> 

## <a name="whats-new-in-update-12"></a>Novidades na Atualização 1.2
Esses recursos foram lançados com atualização 1 foi feita tooa disponível limitada de conjunto de usuários. Versão Olá 1.2 de atualização, a maioria dos usuários de StorSimple Olá veria Olá novos recursos e aprimoramentos a seguir:

* **Migração de dispositivos da série 7000 5000 série too8000** – esta versão apresenta um novo recurso de migração que permite Olá StorSimple 7000 5000 série appliance usuários toomigrate seu dispositivo físico do tooa StorSimple 8000 séries de dados ou um dispositivo virtual. o recurso de migração Olá tem dois principais propostas de valor:                                                                  
  
  * **Continuidade dos negócios**, habilitando a migração de dados existentes nos dispositivos da série 7000 5000 série dispositivos too8000.
  * **Melhor ofertas de recurso de dispositivos da série 8000 do hello**, como eficiente gerenciamento centralizado de vários dispositivos por meio do serviço StorSimple Manager, melhor a classe de hardware e atualizar firmware, dispositivos virtuais, mobilidade de dados e recursos no roteiro futuro hello.
    
    Consulte toohello [guia de migração](http://www.microsoft.com/download/details.aspx?id=47322) para obter detalhes sobre como toomigrate um dispositivo da série StorSimple 7000 5000 série tooan 8000. 
* **Disponibilidade no hello Portal do Azure governamental** – StorSimple agora está disponível no portal do Azure Government hello. Consulte como muito[implantar um dispositivo StorSimple no hello Portal do Azure governamental](storsimple-deployment-walkthrough-gov.md).
* **Suporte para outros provedores de serviços de nuvem** – hello outros provedores de serviços de nuvem com suporte são Amazon S3, Amazon S3 com RRS, HP e OpenStack (beta).
* **Atualizar toolatest APIs de armazenamento** – com esta versão, o StorSimple foi atualizada do serviço de armazenamento do Azure mais recente toohello APIs. Dispositivos da série StorSimple 8000 que executam versões do software de pré-atualização 1 (versão, 0.1, 0.2 e 0,3) estão usando versões do hello APIs do serviço de armazenamento do Azure com mais de 17 de julho de 2009. Conforme indicado na Olá atualizado [comunicado sobre remoção de versões de serviço de armazenamento](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx), por 1 de agosto de 2016, essas APIs serão substituídas. É essencial que você aplique Olá StorSimple 8000 Series atualização 1 anterior tooAugust 1, 2016. Se você não toodo, portanto, os dispositivos de StorSimple deixarão de funcionar corretamente.
* **Suporte de zona redundante armazenamento (ZRS)** – com hello toohello atualização mais recente versão Olá APIs de armazenamento, série StorSimple 8000 do hello oferecerá suporte a armazenamento com redundância de zona (ZRS) em adição tooLocally armazenamento redundante (LRS) e com redundância geográfica GRS (armazenamento). Consulte toothis [artigo sobre opções de redundância de armazenamento do Azure](../storage/common/storage-redundancy.md) para obter detalhes ZRS.
* **Avançado a experiência de implantação e atualização inicial** – nesta versão, Olá instalação e processos de atualização foram aprimorados. instalação de Olá por meio do Assistente de instalação de saudação é o usuário de toohello de comentários de tooprovide aprimorado se as configurações de firewall e de configuração de rede Olá estão incorretas. Cmdlets de diagnósticos adicionais foram fornecidos toohelp você a solucionar o problema de rede do dispositivo de saudação. Consulte Olá [artigo de implantação de solução de problemas](storsimple-troubleshoot-deployment.md) para obter mais informações sobre Olá novos cmdlets de diagnóstico usados para solucionar problemas.

## <a name="issues-fixed-in-update-12"></a>Problemas corrigidos na Atualização 1.2
Olá, a tabela a seguir fornece um resumo dos problemas que foram corrigidos nas atualizações 1, 1.1 e 1.2.    

| Não. | Recurso | Problema | Corrigido na Atualização | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Windows PowerShell para StorSimple |Quando um usuário acessados remotamente o dispositivo StorSimple hello usando o Windows PowerShell para StorSimple e, em seguida, iniciado o Assistente de instalação hello, uma falha ocorreu, assim como Data 0 foi de entrada de IP. Agora, esse bug foi corrigido na Atualização 1. |Atualização 1 |Sim |Sim |
| 2 |Redefinição de fábrica |Em alguns casos, quando você executar uma redefinição de fábrica, Olá dispositivo StorSimple ficou preso e exibida esta mensagem: **toofactory redefinição está em andamento (fase 8)**. Isso aconteceu, se você pressionou CTRL + C enquanto Olá cmdlet estava em andamento. Agora esse bug foi corrigido. |Atualização 1 |Sim |Não |
| 3 |Redefinição de fábrica |Após a redefinição de fábrica do controlador duplo com falha, foram autorizados tooproceed com o registro do dispositivo. Isso resultava em uma configuração de sistema sem suporte. Na Atualização 1, uma mensagem de erro é mostrada e o registro é bloqueado em um dispositivo que tenha uma redefinição de fábrica com falha. |Atualização 1 |Sim |Não |
| 4 |Redefinição de fábrica |Em alguns casos, foram gerados alertas de incompatibilidade falso positivos. Os alertas de incompatibilidade incorretos não serão mais gerados em dispositivos com a  Atualização 1 em execução. |Atualização 1 |Sim |Não |
| 5 |Redefinição de fábrica |Se uma redefinição de fábrica tiver sido interrompida toocompletion anterior, Olá modo de recuperação do dispositivo inserido e não permitiu que você tooaccess do Windows PowerShell para StorSimple. Agora esse bug foi corrigido. |Atualização 1 |Sim |Não |
| 6 |Recuperação de desastre |Um bug de recuperação de desastre foi corrigido no qual DR falhará durante a descoberta de saudação de backups no dispositivo de destino hello. |Atualização 1 |Sim |Sim |
| 7 |LEDs de monitoramento |Em determinadas circunstâncias, LEDs de monitoramento no hello parte posterior do dispositivo não indicam o status correto. LED azul de saudação foi desativada. Os LEDs de DADOS 0 e 1 ficavam piscando mesmo quando essas interfaces não estavam configuradas. Olá problema foi corrigido e LEDs de monitoramento agora indicam o status correto hello. |Atualização 1 |Sim |Não |
| 8 |LEDs de monitoramento |Em determinadas circunstâncias, após a aplicação da atualização 1, luz Olá azul no controlador ativo Olá desativada tornando controlador ativo do disco rígido tooidentify hello. Esse problema foi corrigido nesta versão do patch. |Atualização 1.2 |Sim |Não |
| 9 |Interfaces de rede |Nas versões anteriores, um dispositivo StorSimple configurado com um gateway não roteável podia ficar offline. Nesta versão, a métrica roteamento Olá para Data 0 foi feita hello mais baixo; Portanto, mesmo que outras interfaces de rede são habilitados para a nuvem, todo o tráfego de nuvem saudação do dispositivo hello será roteado por meio de dados 0. |Atualização 1 |Sim |Sim |
| 10 |Backups |Um bug na atualização 1 que causou backups toofail após 24 dias foi corrigido no patch Olá versão 1.1 da atualização. |Atualização 1.1 |Sim |Sim |
| 11 |Backups |Um bug nas versões anteriores resultou em baixo desempenho dos instantâneos de nuvem com baixas taxas de alteração. Esse bug foi corrigido nesta versão do patch. |Atualização 1.2 |Sim |Sim |
| 12 |Atualizações |Foi corrigido um bug na atualização 1 relatou uma falha na atualização e causado Olá controladores toogo no modo de recuperação, nesta versão de patch. |Atualização 1.2 |Sim |Sim |

## <a name="known-issues-in-update-12"></a>Problemas conhecidos na Atualização 1.2
Olá, a tabela a seguir fornece um resumo dos problemas conhecidos nesta versão.

| Não. | Recurso | Problema | Comentários/soluções alternativas | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Quorum de disco |Em casos raros, se a maioria de saudação dos discos no compartimento EBOD de saudação de um dispositivo 8600 é desconectada, resultando em nenhum quorum de disco, em seguida, pool de armazenamento Olá estarão offline. Ele permanecerá offline, mesmo se Olá discos sejam reconectados. |Você precisará tooreboot dispositivo de saudação. Se Olá problema persistir, entre em contato com o Microsoft Support para as próximas etapas. |Sim |Não |
| 2 |ID de controlador incorreta |Quando a substituição do controlador é executada, o controlador 0 pode aparecer como controlador 1. Durante a substituição do controlador, quando Olá imagem é carregada do nó do par hello, Olá ID do controlador inicialmente poderá ser exibido como ID. do controlador do par de saudação Em casos raros, esse comportamento pode ser percebido após uma reinicialização do sistema. |Nenhuma ação do usuário é necessária. Esta situação se resolverá após a conclusão da substituição do controlador hello. |Sim |Não |
| 3 |Contas de armazenamento |Usar conta de armazenamento de Olá Olá armazenamento serviço toodelete é um cenário sem suporte. Isso levará tooa situação na qual os dados de usuário não podem ser recuperados. |Sim |Sim | |
| 4 |Failover de dispositivo |Vários failovers de um contêiner de volume do hello, não há suporte para os mesmos dispositivos de destino toodifferent de fonte de dispositivo. Failover de dispositivo dos dispositivos de toomultiple único dispositivo inativo tornará contêineres de volume de saudação em Olá failover primeiro dispositivo perdem a propriedade de dados. Após o failover, esses contêineres de volume aparecerá ou ter um comportamento diferente quando você exibi-los em Olá portal clássico do Azure. | |Sim |Não |
| 5 |Instalação |Durante o adaptador StorSimple para SharePoint, você precisa tooprovide um IP do dispositivo na ordem para Olá install toofinish com êxito. | |Sim |Não |
| 6 |Proxy Web |Se a configuração de proxy web tiver HTTPS como Olá especificado protocolo, em seguida, a comunicação de serviço no dispositivo será afetada e dispositivo Olá ficará offline. Pacotes de suporte também serão gerados no processo de hello, consome recursos significativos em seu dispositivo. |Certifique-se de que URL do proxy web hello possui HTTP conforme Olá protocolo especificado. Para obter mais informações, vá muito[configurar o proxy da web para seu dispositivo](storsimple-configure-web-proxy.md). |Sim |Não |
| 7 |Proxy Web |Se você configurar e habilitar o proxy da web em um dispositivo registrado, você precisará controlador ativo do toorestart Olá em seu dispositivo. | |Sim |Não |
| 8 |Latência de nuvem alta e alta carga de trabalho de E/S |Quando seu dispositivo StorSimple encontra uma combinação de latências de nuvem muita alta (ordem de segundos) e alta carga de trabalho de e/s, os volumes de dispositivos Olá entram em um estado degradado e hello e/ss pode falhar com um erro "o dispositivo não está pronto". |Você será necessário toomanually controladores de dispositivo de saudação de reinicialização ou executar um toorecover de failover do dispositivo dessa situação. |Sim |Não |
| 9 |Azure PowerShell |Quando você usa o cmdlet do StorSimple Olá **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - espera primeiro 1 -** tooselect Olá primeiro objeto para que você possa criar um novo **VolumeContainer** do objeto, Olá cmdlet retorna todos os objetos de saudação. |Encapsular Olá cmdlet entre parênteses, da seguinte maneira: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - primeiro 1 - espera** |Sim |Sim |
| 10 |Migração |Quando vários contêineres de volume são passados para a migração, Olá ETA para o backup mais recente é preciso para o contêiner de volume primeiro hello. Além disso, migração paralela será iniciado após hello 4 backups no contêiner de volume primeiro Olá são migrados. |É recomendável que você migre um contêiner de volume por vez. |Sim |Não |
| 11 |Migração |Após a restauração de saudação volumes não são adicionados toohello backup hello ou política de grupo do disco virtual. |Você precisará tooadd política de backup esses tooa volumes nos backups de toocreate de ordem. |Sim |Sim |
| 12 |Migração |Após a conclusão da migração Olá, o dispositivo da série Olá 5000/7000 não deve acessar Olá migrados contêineres de dados. |É recomendável que você exclua Olá migrados contêineres de dados após a migração de saudação concluída e confirmada. |Sim |Não |
| 13 |Clonagem e recuperação de desastre |Um dispositivo StorSimple com atualização 1 não é possível clonar ou executar dispositivo tooa de recuperação de desastres executando o software de pré-atualização 1. |Você precisará tooupdate Olá destino dispositivo tooUpdate 1 tooallow essas operações |Sim |Sim |
| 14 |Migração |O backup de configuração para a migração poderá falhar em um dispositivo da série 5000-7000 quando houver grupos de volumes sem volumes associados. |Excluir todos os grupos de volume vazios Olá sem volumes associados e, em seguida, repita o backup de configuração de saudação. |Sim |Não |

## <a name="physical-device-updates-in-update-12"></a>Atualizações de dispositivo físico na Atualização 1.2
Se a atualização de patch 1.2 é aplicado tooa dispositivo físico (executando versões anteriores tooUpdate 1), versão do software Olá alterará too6.3.9600.17584.

## <a name="controller-and-firmware-updates-in-update-12"></a>Atualizações de controlador e firmware na Atualização 1.2
Esta versão atualiza o driver hello e firmware de disco Olá em seu dispositivo.

* Para obter mais informações sobre a atualização do controlador SAS hello, consulte [atualização 1 para controladores SAS LSI no dispositivo do Microsoft Azure StorSimple](https://support.microsoft.com/kb/3043005). 
* Para obter mais informações sobre a atualização de firmware de disco hello, consulte [atualização 1 do firmware do disco para o dispositivo do Microsoft Azure StorSimple](https://support.microsoft.com/kb/3063416).

## <a name="virtual-device-updates-in-update-12"></a>Atualizações do dispositivo virtual na Atualização 1.2
Esta atualização não pode ser o dispositivo virtual toohello aplicado. Novos dispositivos virtuais precisará toobe criado. 

## <a name="next-steps"></a>Próximas etapas
* [Instalar a Atualização 1.2 no seu dispositivo](storsimple-install-update-1.md).

