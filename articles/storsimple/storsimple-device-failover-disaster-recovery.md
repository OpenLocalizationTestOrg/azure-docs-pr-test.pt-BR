---
title: "aaaStorSimple failover e recuperação de desastres | Microsoft Docs"
description: "Saiba como toofail através de seu tooitself de dispositivo StorSimple, outro dispositivo físico ou um dispositivo virtual."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>Failover e recuperação de desastres para o seu dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este tutorial descreve Olá etapas necessárias toofail de um dispositivo StorSimple no evento de saudação de um desastre. Um failover permitirá que você toomigrate seus dados de um dispositivo de origem em Olá datacenter tooanother físico ou até mesmo um dispositivo virtual localizado no hello mesma ou em um local geográfico diferente. 

Recuperação de desastres (DR) é organizada por meio do recurso de failover de dispositivo hello e é iniciada do hello **dispositivos** página. Esta página tabula todos Olá StorSimple dispositivos conectados tooyour o serviço StorSimple Manager. Para cada dispositivo, nome amigável hello, status, capacidade provisionada e máximo, o tipo e o modelo são exibidos.

![Página Dispositivos](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

Guia de saudação neste tutorial se aplica a dispositivos físicos e virtuais de tooStorSimple em todas as versões de software.

## <a name="disaster-recovery-dr-and-device-failover"></a>Recuperação de desastres (DR) e failover de dispositivo
Em um cenário de recuperação de desastre, dispositivo primário Olá parará de funcionar. Nessa situação, você pode mover dados de nuvem de saudação associados Olá falha dispositivo tooanother dispositivo usando o dispositivo primário hello como Olá *fonte* e especificando outro dispositivo como Olá *destino*. Você pode selecionar um ou mais volumes contêineres toomigrate toohello dispositivo de destino. Esse processo é chamado tooas Olá *failover*. 

Durante o failover hello, contêineres de volume de saudação do dispositivo de origem de saudação alterar a propriedade e são transferidos toohello dispositivo de destino. Depois que os contêineres de volume Olá alterar a propriedade, esses são excluídos do dispositivo de origem hello. Após a conclusão da exclusão Olá, o dispositivo de destino hello, em seguida, pode ser feito novamente.

Normalmente após uma recuperação de desastres, o backup mais recente da saudação é o dispositivo de destino de toohello do toorestore usado Olá dados. No entanto, se houver várias políticas de backup para Olá mesmo volume, política de backup Olá com maior o número de volumes Olá obtém separada e backup mais recente de saudação da política é usada toorestore Olá dados no dispositivo de destino de saudação.

Por exemplo, se houver duas políticas de backup (um padrão e uma personalizada) *defaultPol*, *customPol* com hello detalhes a seguir:

* *defaultPol*: um volume, *vol1*, é executada diariamente a partir de 22h30.
* *customPol*: quatro volumes, *vol1*, *vol2*, *vol3*, *vol4*, são executados diariamente a partir de 22h.

Nesse caso, *customPol* será usada, pois ela tem mais volumes, e priorizamos o controle de falhas. Olá o backup mais recente dessa política é usada toorestore dados.

## <a name="considerations-for-device-failover"></a>Considerações para failover de dispositivo
Evento de saudação de um desastre, você poderá toofail em seu dispositivo StorSimple:

* dispositivo físico tooa 
* tooitself
* dispositivo virtual tooa

Para qualquer failover do dispositivo, mantenha seguir de saudação mente:

* Olá pré-requisitos para DR são que todos os volumes de saudação em contêineres de volume Olá estão offline e contêineres de volume Olá tem um tipo de instantâneo em nuvem. 
* Olá destino disponíveis para DR são dispositivos que têm tooaccommodate de espaço suficiente Olá contêineres de volume selecionados. 
* Olá dispositivos que estão conectado tooyour de serviço, mas não atendem aos critérios de saudação do suficiente espaço não estarão disponível como dispositivos de destino.
* Após a recuperação de desastres, por tempo limitado, Olá desempenho de acesso a dados pode ser afetado significativamente, como dispositivo Olá será necessário tooaccess Olá dados da nuvem hello e armazená-lo localmente.

#### <a name="device-failover-across-software-versions"></a>Failover de dispositivo em versões de software
Um serviço StorSimple Manager em uma implantação pode ter vários dispositivos físicos e virtuais, todos executando versões de software diferentes. Dependendo da versão do software hello, tipos de volumes de saudação em dispositivos Olá também podem ser diferentes. Por exemplo, um dispositivo que executa a Atualização 2 ou superior teria volumes em camadas e fixados localmente (com o arquivamento sendo um subconjunto de volumes em camadas). Um dispositivo de pré-atualização 2 em Olá outro lado pode ter hierárquico e volumes de arquivamento. 

Use Olá toodetermine tabela a seguir se é possível realizar failover tooanother dispositivo que executa um comportamento de versão e hello de software diferente dos tipos de volume durante a recuperação de desastres.

| Failover de | Permitido para dispositivo físico | Permitido para dispositivo virtual |
| --- | --- | --- |
| Atualização 2 toopre-atualização 1 (versão, 0.1, 0.2, 0.3) |Não |Não |
| Atualização 2 tooUpdate 1 (1, 1.1, 1.2) |Sim <br></br>Se usando fixado localmente ou em camadas volumes ou uma combinação dos dois, Olá volumes são sempre failover como em camadas. |Sim<br></br>Se usando volumes fixados localmente, o failover desses volumes é realizado em camadas. |
| Atualização 2 tooUpdate 2 (versão posterior) |Sim<br></br>Se usar volumes localmente fixados ou em camadas ou uma combinação dos dois, Olá volumes são sempre submetidos a failover como Olá iniciando o tipo de volume; em camadas como em camadas e localmente afixado localmente fixados. |Sim<br></br>Se usando volumes fixados localmente, o failover desses volumes é realizado em camadas. |

#### <a name="partial-failover-across-software-versions"></a>Failover parcial em versões de software
Siga este guia se você pretende tooperform um failover parcial usando um dispositivo de origem do StorSimple em execução 1 tooa pré-atualização destino que executam a atualização 1 ou posterior. 

| Failover parcial de | Permitido para dispositivo físico | Permitido para dispositivo virtual |
| --- | --- | --- |
| Pré-atualização 1 (versão, 0.1, 0.2, 0.3) tooUpdate 1 ou posterior |Sim, consulte abaixo para dica de prática recomendada hello. |Sim, consulte abaixo para dica de prática recomendada hello. |

> [!TIP]
> Houve uma alteração de formato dos metadados e dados de nuvem na Atualização 1 e versões posteriores. Portanto, não recomendamos um failover parcial de pré-atualização 1 tooUpdate 1 ou versões posteriores. Se você precisar tooperform um failover parcial, é recomendável que você primeiro aplica a atualização 1 ou posterior em ambos os dispositivos de saudação (origem e destino) e continue com a saudação failover. 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>O failover de dispositivo físico tooanother
Execute seu dispositivo físico do dispositivo tooa destino de Olá toorestore as etapas a seguir.

1. Verifique se o contêiner de volume Olá que desejar toofail pela associou os instantâneos em nuvem.
2. Em Olá **dispositivos** , clique em Olá **contêineres de Volume** guia.
3. Selecione um contêiner de volume que deseja toofail tooanother dispositivo. Clique em Olá volume contêiner toodisplay Olá lista de volumes neste contêiner. Selecione um volume e clique em **colocar Offline** tootake volume de saudação offline. Repita esse processo para todos os volumes de saudação no contêiner de volume hello.
4. Etapa anterior Olá Repita para todos os contêineres de volume de Olá você gostaria que toofail de dispositivo tooanother.
5. Em Olá **dispositivos** , clique em **Failover**.
6. No Assistente de saudação for aberto, em **escolha toofail de contêiner de volume em**:
   
   1. Na lista de saudação de contêineres de volume, selecione os contêineres de volume Olá você gostaria que toofail sobre.
      **Olá apenas contêineres de volume com instantâneos de nuvem associados e volumes offline são exibidos.**
   2. Em **escolher um dispositivo de destino** para volumes de saudação nos contêineres de saudação selecionado, selecione um dispositivo de destino da lista suspensa de saudação de dispositivos disponíveis. Somente os dispositivos de saudação que possuem capacidade disponível da saudação são exibidos na lista suspensa de saudação.
   3. Por fim, examine todas as configurações de failover de saudação em **confirmar failover**. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
7. Um trabalho de failover é criado que pode ser monitorado por meio de saudação **trabalhos** página. Se o contêiner de volume de saudação failover tiver volumes locais, você verá os trabalhos de restauração individuais para cada volume local (não para volumes em camadas) no contêiner de saudação. Esses trabalhos de restauração pode levar algum tempo toocomplete. É provável que esse trabalho de failover Olá pode ser concluído anteriormente. Observe que esses volumes terá garantia local somente depois Olá restauração trabalhos sejam concluídos. Após a conclusão do failover Olá, vá toohello **dispositivos** página.                                            
   
   1. Selecione o dispositivo de saudação que foi usado como dispositivo de destino Olá para o processo de failover hello.
   2. Vá toohello **contêineres de Volume** página. Todos os contêineres de volume hello, junto com os volumes de saudação do dispositivo antigo do hello, devem ser listados.

## <a name="failover-using-a-single-device"></a>Failover usando um único dispositivo
Execute Olá etapas a seguir se você tiver apenas um único tooperform de dispositivo e a necessidade de um failover.

1. Tire instantâneos em nuvem de todos os volumes de saudação em seu dispositivo.
2. Redefina o dispositivo toofactory padrão. Siga Olá detalhadas instruções [como configurações de padrão tooreset um toofactory de dispositivo StorSimple](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Configure o seu dispositivo e registre-o novamente no serviço StorSimple Manager.
4. Em Olá **dispositivos** página, o dispositivo antigo Olá deve aparecer como **Offline**. Olá dispositivo registrado recentemente deve aparecer como **Online**.
5. Para o novo dispositivo de hello, conclua mínimos de configuração de dispositivo Olá Olá primeiro. 
   
   > [!IMPORTANT]
   > **Se a configuração mínima de saudação não for concluída primeiro, sua DR falhará como resultado de um bug na implementação atual de saudação. Esse problema será corrigido em uma versão posterior.**
   > 
   > 
6. Selecione o dispositivo antigo da saudação (status off-line) e clique em **Failover**. No Assistente de saudação que é apresentado, failover nesse dispositivo e especifique o dispositivo de destino hello como dispositivo registrado recentemente hello. Para obter instruções detalhadas, consulte muito[failover de dispositivo físico tooanother](#fail-over-to-another-physical-device).
7. Será criado um trabalho de restauração de dispositivo que você pode monitorar de saudação **trabalhos** página.
8. Depois que o trabalho de saudação for concluída com êxito, acessar o novo dispositivo de saudação e navegar toohello **contêineres de Volume** página. Todos os contêineres de volume de saudação do dispositivo antigo Olá agora devem ser migrados toohello novo dispositivo.

## <a name="fail-over-tooa-storsimple-virtual-device"></a>O failover de dispositivo virtual do StorSimple tooa
Você deve ter um StorSimple dispositivo virtual criado e configurado toorunning anterior deste procedimento. Se executar a atualização 2, considere o uso de um dispositivo virtual 8020 para Olá DR que tem 64 TB e usa o armazenamento Premium. 

Execute Olá seguindo as etapas toorestore Olá dispositivo tooa destino dispositivo virtual StorSimple.

1. Verifique se o contêiner de volume Olá que desejar toofail pela associou os instantâneos em nuvem.
2. Em Olá **dispositivos** , clique em Olá **contêineres de Volume** guia.
3. Selecione um contêiner de volume que deseja toofail tooanother dispositivo. Clique em Olá volume contêiner toodisplay Olá lista de volumes neste contêiner. Selecione um volume e clique em **colocar Offline** tootake volume de saudação offline. Repita esse processo para todos os volumes de saudação no contêiner de volume hello.
4. Etapa anterior Olá Repita para todos os contêineres de volume de Olá você gostaria que toofail de dispositivo tooanother.
5. Em Olá **dispositivos** , clique em **Failover**.
6. No Assistente de saudação for aberto, em **escolha toofailover de contêiner de volume**, conclua Olá seguinte:
   
    a. Na lista de saudação de contêineres de volume, selecione os contêineres de volume Olá você gostaria que toofail sobre.
   
    **Olá apenas contêineres de volume com instantâneos de nuvem associados e volumes offline são exibidos.**
   
    b. Em **escolha um dispositivo de destino para volumes de saudação nos contêineres de saudação selecionado**, selecione Olá dispositivo virtual StorSimple da lista suspensa de saudação de dispositivos disponíveis. **Somente os dispositivos de saudação que possuem capacidade suficiente são exibidos na lista suspensa de saudação.**  
7. Por fim, examine todas as configurações de failover de saudação em **confirmar failover**. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
8. Após a conclusão do failover Olá, vá toohello **dispositivos** página.
   
    a. Selecione Olá dispositivo virtual StorSimple que foi usado como dispositivo de destino Olá para o processo de failover hello.
   
    b. Vá toohello **contêineres de Volume** página. Todos os contêineres de volume hello, junto com os volumes de saudação do dispositivo antigo Olá agora devem ser listados.

![Vídeo disponível](./media/storsimple-device-failover-disaster-recovery/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como você pode restaurar uma falha de dispositivo virtual do dispositivo físico tooa na nuvem hello, clique em [aqui](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/).

## <a name="failback"></a>Failback
A partir da Atualização 3, o StorSimple também dá suporte para failback. Após a conclusão do failover hello, hello ações a seguir ocorrem:

* contêineres de volume de saudação que fizeram failover são limpos do dispositivo de origem hello.
* Um trabalho em segundo plano por contêiner de volume (failover) é iniciado no dispositivo de origem hello. Se você tentar toofailback enquanto Olá trabalho está em andamento, você receberá um efeito de toothat de notificação. Você precisará toowait até que o trabalho de saudação seja concluída toostart Olá failback. 
  
    Olá tempo toocomplete Olá a exclusão de contêineres de volume depende de vários fatores, como a quantidade de dados, a idade dos dados hello, número de backups e largura de banda de rede do hello disponível para a operação de saudação. Se você estiver planejando failbacks/failovers de teste, será recomendável testar contêineres de volume com menos dados (Gbs). Na maioria dos casos, você pode iniciar 24 horas após a conclusão do failover Olá Olá failback. 

## <a name="frequently-asked-questions"></a>Perguntas frequentes
P. **O que acontece se Olá DR falha ou se tiver êxito parcial?**

R. Se Olá DR falhar, recomendamos que você tente novamente. Olá pela segunda vez, DR sabe o que foi feito e quando o processo de saudação paralisado Olá primeira vez. Olá o processo de recuperação de desastres inicia a partir desse ponto em diante. 

P. **Excluir um dispositivo enquanto Olá failover do dispositivo está em andamento?**

R. Você não pode excluir um dispositivo enquanto uma DR está em andamento. Você só pode excluir o dispositivo após a conclusão da saudação DR.

P.    **Quando a coleta de lixo Olá inicia no dispositivo de origem Olá para que Olá de dados local no dispositivo de origem é excluído?**

R. Coleta de lixo será habilitada no dispositivo de origem Olá somente depois que o dispositivo Olá é limpa completamente. Limpeza de saudação inclui limpeza de objetos que falharam do dispositivo de origem hello como objetos de backup (não de dados), volumes, contêineres de volume e políticas.

P. **O que acontece se Olá excluir trabalho associado aos contêineres de volume Olá no dispositivo de origem Olá falha?**

R.  Se Olá excluir trabalho falhar, você precisará toomanually a exclusão do disparador Olá Olá de contêineres de volume. Em Olá **dispositivos** , selecione o dispositivo de origem e clique em **contêineres de Volume**. Contêineres de volume Olá Select que falharam em e em inferior Olá Olá página, clique em **excluir**. Depois que você excluiu todos os Olá falha em contêineres de volume no dispositivo de origem hello, você pode iniciar Olá failback.

## <a name="business-continuity-disaster-recovery-bcdr"></a>BCDR (recuperação de desastre de continuidade de negócios)
Um cenário de recuperação (BCDR) de desastres de continuidade de negócios ocorre quando Olá data center inteiro do Azure para de funcionar. Isso pode afetar o serviço StorSimple Manager e Olá associados dispositivos StorSimple.

Se não houver dispositivos StorSimple que foram registrados antes de um desastre ocorreu, em seguida, esses dispositivos StorSimple talvez seja necessário tooundergo redefinição de fábrica. Após o desastre hello, o dispositivo StorSimple Olá será mostrado como offline. o dispositivo StorSimple Olá deve ser excluído do portal hello e uma redefinição de fábrica deve ser feita, seguido por um novo registro.

## <a name="next-steps"></a>Próximas etapas
* Depois de executar um failover, talvez seja necessário muito[desativar ou excluir seu dispositivo StorSimple](storsimple-deactivate-and-delete-device.md).
* Para obter informações sobre como toouse Olá StorSimple Manager service, ir muito[Use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

