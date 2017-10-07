---
title: "Notas de versão do aaaStorSimple 8000 Series atualização 2 | Microsoft Docs"
description: "Descreve os novos recursos do hello, problemas e soluções alternativas para StorSimple 8000 Series atualização 2."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: e2c8bffd-7fc5-4b77-b632-a4f59edacc3a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 36c75aad900c7b1286a924732967b8ee519a3d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>Notas de versão da Atualização 2 da série 8000 do StorSimple
## <a name="overview"></a>Visão geral
Olá notas de versão a seguir descrevem Olá novos recursos e identificam problemas abertos críticos de saudação do StorSimple 8000 Series atualização 2. Eles também contêm uma lista de saudação software StorSimple, driver e atualizações de firmware de disco incluídas nesta versão. 

Atualização 2 pode ser a execução da versão (GA) ou atualização 0,1 por meio de atualização 1.2 o dispositivo StorSimple tooany aplicada. versão do dispositivo Olá associado com a atualização 2 é 6.3.9600.17673.

Analise Olá informações contidas na versão Olá notas antes de implantar Olá atualizar em sua solução StorSimple.

> [!IMPORTANT]
> * Demora cerca de 4 a 7 horas tooinstall essa atualização (incluindo atualizações do Windows hello). 
> * A Atualização 2 tem atualizações de software, driver LSI e firmware de SSD.
> * Para novas versões, você poderá não ver atualizações imediatamente porque fazemos uma distribuição em fases de saudação atualizações. Aguarde alguns dias e procure atualizações novamente, uma vez que elas serão disponibilizadas em breve.
> 
> 

## <a name="whats-new-in-update-2"></a>Novidades na Atualização 2
Atualização 2 apresenta Olá novos recursos a seguir.

* **Localmente afixado volumes** – em versões anteriores da série StorSimple 8000 do hello, blocos de dados foram nuvem toohello em camadas com base no uso. Não havia nenhum tooguarantee de maneira blocos permanece no local. Na atualização 2, quando você criar um volume, você pode designar um volume como dados fixados localmente e primários desse volume não serão nuvem toohello em camadas. Instantâneos de volumes localmente afixados ainda será copiado toohello nuvem para backup, de modo que Olá nuvem pode ser usado para fins de recuperação de desastres e mobilidade de dados. Além disso, você pode alterar o tipo de volume hello (ou seja, converter volumes de toolocally fixado de volumes em camadas e converter localmente fixados volumes tootiered). 
* **Aprimoramentos de dispositivo virtual StorSimple** – anteriormente, Olá StorSimple série 8000 posicionado dispositivo virtual hello como uma solução de desenvolvimento/teste ou recuperação de desastres. Havia apenas um modelo de dispositivo virtual (modelo 1100). A Atualização 2 apresenta dois modelos de dispositivo virtual: 
  
  * 8010 (anteriormente chamado de saudação 1100) – nenhuma alteração; tem uma capacidade de 30 TB e usa o armazenamento padrão do Azure.
  * 8020 – Tem uma capacidade de 64 TB e usa o armazenamento Premium do Azure para um melhor desempenho.
    
    Há um único VHD para ambos os modelos de dispositivo virtual (8010/8020). Ao iniciar o dispositivo virtual hello, ele detecta parâmetros de plataforma hello e aplica-se a versão do modelo correto hello.
* **Melhorias de rede** – atualização 2 contém Olá melhorias de rede a seguir:
  
  * Várias NICs podem ser habilitadas para nuvem Olá para que o failover pode ocorrer se uma NIC falhar.
  * Aprimoramentos de roteamento, com métricas fixas para blocos habilitados para a nuvem.
  * Nova tentativa online de recursos com falha antes de um failover.
  * Novos alertas para falhas de serviço.
* **Aprimoramentos de atualização** – atualizar 1.2 e versões anteriores, série StorSimple 8000 do hello foi atualizada por meio de dois canais: Windows Update para clustering, iSCSI e assim por diante e Microsoft Update para binários e firmware.
    A Atualização 2 usa o Microsoft Update para todos os pacotes de atualização. Isso deve levar tempo tooless a aplicação de patch ou fazer failovers. 
* **Atualizações de firmware** – hello seguintes firmware atualizações estão incluídas:
  
  * LSI: lsi_sas2.sys Versão do Produto 2.00.72.10
  * Somente SSD (não há atualizações de HDD): XMGG, XGEG, KZ50, F6C2 e VR08
* **Suporte proativo** – Microsoft toopull informações adicionais de diagnóstico de dispositivo Olá habilita a atualização 2. Quando a nossa equipe de operações identifica dispositivos que estão tendo problemas, estamos melhores toocollect equipado informações de dispositivo de saudação e diagnosticar problemas. **Aceitando a atualização 2, nos permite tooprovide esse suporte pró-ativo**.    

## <a name="issues-fixed-in-update-2"></a>Problemas corrigidos na Atualização 2
Olá tabelas a seguir fornece um resumo dos problemas que foram corrigidos em 2 de atualizações.    

| Não. | Recurso | Problema | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- |
| 1 |Interfaces de rede |Após uma atualização tooUpdate 1, Olá serviço StorSimple Manager relatou que portas de Data2 e Data3 Olá falha em um controlador. Esse problema foi corrigido. |Sim |Não |
| 2 |Atualizações |Após uma atualização tooUpdate 1, alertas de alarme audível ocorreram no hello portal clássico do Azure em vários dispositivos. Esse problema foi corrigido. |Sim |Não |
| 3 |Autenticação Openstack |Ao usar o Openstack como seu provedor de serviços de nuvem, você poderá receber um erro informando que sua cadeia de caracteres de autenticação de nuvem é muito longa. Esse problema foi corrigido. |Sim |Não |

## <a name="known-issues-in-update-2"></a>Problemas conhecidos na Atualização 2
Olá, a tabela a seguir fornece um resumo dos problemas conhecidos nesta versão.

| Não. | Recurso | Problema | Comentários/solução alternativa | Aplica-se o dispositivo toophysical | Aplica-se o dispositivo toovirtual |
| --- | --- | --- | --- | --- | --- |
| 1 |Quorum de disco |Em casos raros, se a maioria de saudação dos discos no compartimento EBOD de saudação de um dispositivo 8600 é desconectada, resultando em nenhum quorum de disco, em seguida, pool de armazenamento Olá ficará offline. Ele permanecerá offline, mesmo se Olá discos sejam reconectados. |Você precisará tooreboot dispositivo de saudação. Se Olá problema persistir, entre em contato com o Microsoft Support para as próximas etapas. |Sim |Não |
| 2 |ID de controlador incorreta |Quando a substituição do controlador é executada, o controlador 0 pode aparecer como controlador 1. Durante a substituição do controlador, quando Olá imagem é carregada do nó do par hello, Olá ID do controlador inicialmente poderá ser exibido como ID. do controlador do par de saudação Em casos raros, esse comportamento pode ser percebido após uma reinicialização do sistema. |Nenhuma ação do usuário é necessária. Esta situação se resolverá após a conclusão da substituição do controlador hello. |Sim |Não |
| 3 |Contas de armazenamento |Usar conta de armazenamento de Olá Olá armazenamento serviço toodelete é um cenário sem suporte. Isso levará tooa situação na qual os dados de usuário não podem ser recuperados. | |Sim |Sim |
| 4 |Failover de dispositivo |Vários failovers de um contêiner de volume do hello, não há suporte para os mesmos dispositivos de destino toodifferent de fonte de dispositivo. O failover de dispositivos de toomultiple um único dispositivo inativo tornará contêineres de volume de saudação em Olá failover primeiro dispositivo perdem a propriedade de dados. Após o failover, esses contêineres de volume aparecerá ou ter um comportamento diferente quando você exibi-los em Olá portal clássico do Azure. | |Sim |Não |
| 5 |Instalação |Durante o adaptador StorSimple para SharePoint, você precisa tooprovide um IP do dispositivo na ordem para Olá install toofinish com êxito. | |Sim |Não |
| 6 |Proxy Web |Se a configuração de proxy web tiver HTTPS como Olá especificado protocolo, em seguida, a comunicação de serviço no dispositivo será afetada e dispositivo Olá ficará offline. Pacotes de suporte também serão gerados no processo de hello, consome recursos significativos em seu dispositivo. |Certifique-se de que URL do proxy web hello possui HTTP conforme Olá protocolo especificado. Para obter mais informações, vá muito[configurar o proxy da web para seu dispositivo](storsimple-configure-web-proxy.md). |Sim |Não |
| 7 |Proxy Web |Se você configurar e habilitar o proxy da web em um dispositivo registrado, você precisará controlador ativo do toorestart Olá em seu dispositivo. | |Sim |Não |
| 8 |Latência de nuvem alta e alta carga de trabalho de E/S |Quando seu dispositivo StorSimple encontra uma combinação de latências de nuvem muita alta (ordem de segundos) e alta carga de trabalho de e/s, os volumes de dispositivos Olá entram em um estado degradado e hello e/ss pode falhar com um erro "o dispositivo não está pronto". |Você será necessário toomanually controladores de dispositivo de saudação de reinicialização ou executar um toorecover de failover do dispositivo dessa situação. |Sim |Não |
| 9 |Azure PowerShell |Quando você usa o cmdlet do StorSimple Olá **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - espera primeiro 1 -** tooselect Olá primeiro objeto para que você possa criar um novo **VolumeContainer** do objeto, Olá cmdlet retorna todos os objetos de saudação. |Encapsular Olá cmdlet entre parênteses, da seguinte maneira: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - primeiro 1 - espera** |Sim |Sim |
| 10 |Migração |Quando vários contêineres de volume são passados para a migração, Olá ETA para o backup mais recente é preciso para o contêiner de volume primeiro hello. Além disso, migração paralela será iniciado após hello 4 backups no contêiner de volume primeiro Olá são migrados. |É recomendável que você migre um contêiner de volume por vez. |Sim |Não |
| 11 |Migração |Após a restauração de saudação volumes não são adicionados toohello backup hello ou política de grupo do disco virtual. |Você precisará tooadd política de backup esses tooa volumes nos backups de toocreate de ordem. |Sim |Sim |
| 12 |Migração |Após a conclusão da migração Olá, o dispositivo da série Olá 5000/7000 não deve acessar Olá migrados contêineres de dados. |É recomendável que você exclua Olá migrados contêineres de dados após a migração de saudação concluída e confirmada. |Sim |Não |
| 13 |Clonagem e recuperação de desastre |Um dispositivo StorSimple com atualização 1 não é possível clonar ou executar o dispositivo de tooa de recuperação de desastres executando o software de pré-atualização 1. |Você precisará tooupdate Olá destino dispositivo tooUpdate 1 tooallow essas operações |Sim |Sim |
| 14 |Migração |O backup de configuração para a migração poderá falhar em um dispositivo da série 5000-7000 quando houver grupos de volumes sem volumes associados. |Excluir todos os grupos de volume vazios Olá sem volumes associados e, em seguida, repita o backup de configuração de saudação. |Sim |Não |
| 15 |Cmdlets do Azure PowerShell e volumes fixados localmente |Não é possível criar um volume fixado localmente por meio de cmdlets do Azure PowerShell. (Qualquer volume criado por meio do Azure PowerShell será organizado em camadas.) |Sempre use volumes de tooconfigure localmente afixado em serviço Olá StorSimple Manager. |Sim |Não |
| 16 |Espaço disponível para volumes fixados localmente |Se você excluir um volume localmente afixado, espaço para novos volumes Olá pode não ser atualizado imediatamente. atualizações de serviço do StorSimple Manager Olá Olá espaço local disponível aproximadamente a cada hora. |Aguarde uma hora antes de tentar de novo volume do toocreate hello. |Sim |Não |
| 17 |Volumes fixados localmente |O trabalho de restauração expõe Olá temporário de backup de instantâneo em Olá catálogo de Backup, mas apenas para a duração de saudação do trabalho de restauração hello. Além disso, ele expõe um grupo de disco virtual com o prefixo **tmpCollection** em Olá **políticas de Backup** página, mas somente durante Olá Olá o trabalho de restauração. |Isso poderá ocorrer se o trabalho de restauração tiver apenas volumes fixados localmente ou uma combinação de volumes fixados e em camadas. Se o trabalho de restauração de saudação inclui apenas os volumes em camadas, em seguida, esse comportamento não ocorrerá. Nenhuma intervenção do usuário é necessária. |Sim |Não |
| 18 |Volumes fixados localmente |Se você cancelar um trabalho de restauração e um failover de controlador ocorre imediatamente depois disso, o trabalho de restauração Olá mostrará **falha** em vez de **cancelado**. Se um trabalho de restauração falhará e um failover de controlador ocorre imediatamente depois disso, o trabalho de restauração Olá mostrará **cancelado** em vez de **falha**. |Isso poderá ocorrer se o trabalho de restauração tiver apenas volumes fixados localmente ou uma combinação de volumes fixados e em camadas. Se o trabalho de restauração de saudação inclui apenas os volumes em camadas, em seguida, esse comportamento não ocorrerá. Nenhuma intervenção do usuário é necessária. |Sim |Não |
| 19 |Volumes fixados localmente |Se você cancelar um trabalho de restauração ou se uma restauração falha e ocorre um failover de controlador, um trabalho de restauração adicionais será exibido no hello **trabalhos** página. |Isso poderá ocorrer se o trabalho de restauração tiver apenas volumes fixados localmente ou uma combinação de volumes fixados e em camadas. Se o trabalho de restauração de saudação inclui apenas os volumes em camadas, em seguida, esse comportamento não ocorrerá. Nenhuma intervenção do usuário é necessária. |Sim |Não |
| 20 |Volumes fixados localmente |Se você tentar tooconvert um volume em camadas (criado e clonado com atualização 1.2 ou anterior) tooa localmente fixados volume e seu dispositivo está ficando sem espaço ou há falta de nuvem e hello clone(s) pode estar corrompido. |Esse problema ocorre apenas com volumes que foram criados e clonados com software anterior à Atualização 2. Isso deve ser um cenário incomum. | | |
| 21 |Conversão de volume |Não atualizar Olá ACRs tooa anexado volume enquanto uma conversão de volume está em andamento (toolocally hierárquico fixado ou vice-versa). Atualizar Olá ACRs poderia resultar em corrupção de dados. |Se necessário, atualize a conversão do volume Olá ACRs toohello anterior e não fazer outras atualizações ACR durante a conversão hello está em andamento. | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Atualizações de controlador e firmware na Atualização 2
Esta versão atualiza o driver hello e firmware de disco Olá em seu dispositivo.

* Para obter mais informações sobre o firmware de LSI Olá atualização, consulte o artigo da base de dados de Conhecimento da Microsoft 3121900. 
* Para obter mais informações sobre o firmware de disco Olá atualização, consulte o artigo da base de dados de Conhecimento da Microsoft 3121899.

## <a name="virtual-device-updates-in-update-2"></a>Atualizações do dispositivo virtual na Atualização 2
Esta atualização não pode ser o dispositivo virtual toohello aplicado. Novos dispositivos virtuais precisará toobe criado. 

## <a name="next-step"></a>Próxima etapa
Saiba como muito[instalar 2](storsimple-install-update-2.md) em seu dispositivo StorSimple.

