---
title: aaaStorSimple localmente fixados volumes perguntas Frequentes | Microsoft Docs
description: "Fornece respostas toofrequently frequentes dúvidas sobre o StorSimple localmente fixados volumes."
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 7a2f4b1a-4ac9-4ce1-9359-bd40a9cbbb5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/11/2017
ms.author: manuaery
ms.openlocfilehash: 6a0c742acea836c2b960cb604e4010bcb08c3169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>Volume localmente afixado do StorSimple: perguntas frequentes
## <a name="overview"></a>Visão geral
Olá seguem perguntas e respostas que você possa ter quando você criar um volume StorSimple fixado localmente, converter um volume do volume em camadas tooa fixado localmente (e vice-versa), ou fazer backup e restaurar um volume localmente afixado.

Perguntas e respostas são organizadas em categorias a seguir de saudação

* Criação de um volume localmente afixado
* Backup de um volume localmente afixado
* Converter um volume de tooa localmente afixado volume em camadas
* Restauração de um volume localmente afixado
* Failover de um volume localmente afixado

## <a name="questions-about-creating-a-locally-pinned-volume"></a>Perguntas sobre a criação de um volume localmente afixado
**P.** O que é o tamanho máximo de saudação de um volume localmente afixado que pode criar em dispositivos da série 8000 Olá?

**Um** em dispositivos que executam o StorSimple 8000 Series atualização 3.0, você pode provisionar volumes em camadas até too200 TB no dispositivo 8100 Olá ou volumes localmente afixados backup too8.5 TB. No dispositivo 8600 maior de saudação, você pode provisionar volumes localmente afixados backup too22.5 TB ou volumes em camadas até too500 TB.    
Em dispositivos que executam StorSimple 8000 Series atualização 2. x, você pode provisionar volumes em camadas até too200 TB no dispositivo Olá 8100 ou volumes localmente afixados até too8 TB. No dispositivo 8600 maior de saudação, você pode provisionar volumes localmente afixados até too20 TB ou volumes em camadas até too500 TB.   

**P.** Atualizei meu tooUpdate de dispositivo 8100 2.0 recentemente e quando tento toocreate um volume localmente afixado, tamanho máximo disponível da saudação é apenas 6 TB e não 8 TB. Por que não consigo criar um volume de 8 TB?

**Um** se o dispositivo está executando a atualização 2.0, você pode provisionar volumes localmente afixados até too8 TB ou volumes em camadas até too200 TB em Olá dispositivo 8100. Se o dispositivo já tem em camadas volumes, Olá espaço disponível para criar um volume localmente afixado será proporcionalmente menor do que esse limite máximo. Por exemplo, se 100 TB de volumes em camadas já tiver sido provisionado no seu dispositivo 8100 (que é metade de saudação capacidade hierárquica), tamanho máximo de saudação de um volume local que você pode criar no dispositivo Olá 8100 serão TB too4 reduzido (aproximadamente metade das máximo de saudação localmente fixados a capacidade de volume).

Como espaço local no dispositivo Olá Olá usado toohost conjunto de volumes em camadas de trabalho, espaço disponível de saudação para a criação de um volume localmente afixado é reduzido se dispositivo Olá tem hierárquico volumes. Por outro lado, a criação de um volume localmente afixado proporcionalmente reduz o espaço disponível de saudação para volumes em camadas. Olá tabelas a seguir resume a capacidade disponível em camadas de saudação em dispositivos Olá 8100 e 8600 quando volumes localmente afixados são criados.

####<a name="update-30"></a>Atualização 3.0 
| Capacidade provisionada para volumes localmente afixados | Capacidade disponível toobe provisionado para volumes em camadas - 8100 | Capacidade disponível toobe provisionado para volumes em camadas - 8600 |
| --- | --- | --- |
| 0 |200 TB |500 TB |
| 1 TB |176,5 TB |477,8 TB |
| 4 TB |105,9 TB |411,1 TB |
| 8,5 TB |0 TB |311,1 TB |
| 10 TB |ND |277,8 TB |
| 15 TB |ND |166,7 TB |
| 22,5 TB |ND |0 TB |

####<a name="update-2x"></a>Atualização 2.x  
 | Capacidade provisionada para volumes localmente afixados | Capacidade disponível toobe provisionado para volumes em camadas - 8100 | Capacidade disponível toobe provisionado para volumes em camadas - 8600 |  
 | --- | --- | --- |  
 | 0 |200 TB |500 TB |  
 | 1 TB |25 TB |475 TB |  
 | 4 TB |100 TB |400 TB |  
 | 8 TB |0 TB |300 TB |  
 | 10 TB |ND |250 TB |  
 | 15 TB |ND |125 TB |  
 | 20 TB |ND |0 TB |   

**P.** Por que a criação de um volume localmente afixado é uma operação demorada? 

**A.** Os volumes localmente afixados são provisionados de forma densa. espaço toocreate no Olá camadas locais do dispositivo hello, alguns dados de volumes em camadas existentes podem ser enviados por push nuvem toohello durante o processo de provisionamento de saudação. E como isso depende do tamanho de saudação do volume de saudação sendo provisionada, os dados existentes em seu dispositivo e hello largura de banda disponível toohello nuvem, Olá tempo de saudação levado toocreate que um volume local pode ter várias horas.

**P.** Quanto tempo leva toocreate um volume localmente afixado?

**A.** Porque os volumes localmente afixados são muito provisionados, alguns dados existentes dos volumes em camadas podem ser enviada por push nuvem toohello durante o processo de provisionamento de saudação. Portanto, Olá tempo toocreate um volume localmente afixado depende de vários fatores, incluindo o tamanho de saudação do volume de hello, Olá dados em seu dispositivo e Olá largura de banda disponível. Em um dispositivo recém-instalado que não tem volumes, Olá tempo toocreate um volume localmente afixado é cerca de 10 minutos por terabyte de dados. No entanto, a criação de volumes locais pode levar várias horas, com base em fatores Olá explicados acima em um dispositivo que está em uso.

**P.** Desejo toocreate um volume localmente afixado. Há as práticas recomendadas que necessário toobe atento?

**A.** Volumes localmente afixados são adequados para cargas de trabalho que exigem garantias de locais de dados em todos os momentos e latências toocloud confidenciais. Ao considerar o uso de volumes locais para qualquer uma das suas cargas de trabalho, esteja ciente do seguinte hello:

* Volumes localmente afixados são muito provisionados e criar volumes locais afeta o espaço disponível de saudação para volumes em camadas. Portanto, sugerimos que você comece com volumes menores e escale-os verticalmente à medida que sua necessidade de armazenamento aumentar.
* Provisionamento de volumes locais é uma operação demorada que pode envolver o envio de dados existentes da nuvem de toohello volumes em camadas. Como resultado, pode ocorrer desempenho reduzido nesses volumes.
* O provisionamento de volumes locais é uma operação demorada. tempo real de saudação envolvido depende de vários fatores: Olá tamanho do volume Olá sendo provisionada, dados em seu dispositivo e a largura de banda disponível. Se você não tiver feito sua nuvem de toohello volumes existentes, criação de volume é mais lenta. Sugerimos que você crie instantâneos em nuvem dos volumes existentes antes de provisionar um volume local.
* Você pode converter os volumes toolocally fixado volumes em camadas existentes, e essa conversão envolve o provisionamento de espaço no dispositivo Olá Olá resultante volume localmente afixado (em adição toobringing dados hierárquico [se houver] da nuvem de saudação). Novamente, essa é uma operação demorada que depende dos fatores discutidos anteriormente. Sugerimos que você faça backup seu tooconversion anterior de volumes existentes que o processo de saudação será ainda mais lento se os volumes existentes não são feitos backup. O dispositivo também poderá ter desempenho reduzido durante esse processo.

Para obter mais informações sobre como muito[criar um volume localmente afixado](storsimple-manage-volumes-u2.md#add-a-volume)

**P.** Posso criar vários volumes fixados localmente no hello simultaneamente?

**A.** Sim, mas os trabalhos de criação e expansão de volumes localmente afixados são processados em sequência.

Volumes localmente afixados são muito provisionados e isso exige a criação de espaço local no dispositivo de saudação (que pode resultar em dados existentes de volumes em camadas toobe enviada por push de nuvem toohello durante o processo de provisionamento de saudação). Portanto, se um trabalho de provisionamento estiver em andamento, outros trabalhos de criação de volumes locais serão enfileirados até o trabalho ser concluído.

Da mesma forma, se um volume local existente está sendo expandido ou um volume em camadas está sendo convertido tooa localmente fixados volume, hello criação de um novo volume localmente afixado está na fila até que o trabalho de saudação anterior seja concluído. Expandir o tamanho de saudação de um volume localmente afixado envolve a expansão de saudação do espaço de local existente Olá para esse volume. Conversão de um volume em camadas toolocally fixado também envolve a criação de saudação de espaço local para Olá resultante volume localmente afixado. Em ambas essas operações, a criação ou a expansão do espaço local é um trabalho de longa execução.

Você pode exibir esses trabalhos no hello **trabalhos** página de saudação serviço Azure StorSimple Manager. Olá trabalho ativamente está sendo processado é continuamente atualizada tooreflect progresso de saudação do provisionamento de espaço. Olá restantes volume localmente afixado trabalhos é marcado como em execução, mas seu progresso é interrompido e elas são aplicadas na ordem de saudação que entraram na fila.

**P.** Exclui um volume localmente afixado. Por que não vejo espaço Olá recuperada refletidas no espaço disponível hello quando tento toocreate um novo volume? 

**A.** Se você excluir um volume localmente afixado, espaço para novos volumes Olá pode não ser atualizado imediatamente. Olá serviço StorSimple Manager atualiza disponível de espaço local Olá aproximadamente a cada hora. Sugerimos que você aguarde uma hora antes de tentar de novo volume do toocreate hello.

**P.** Há suporte para volumes localmente afixados no dispositivo de nuvem Olá?

**A.** Não há suporte para volumes fixados localmente no dispositivo de nuvem da saudação (8010 e 8020 dispositivos tooas anteriormente chamado hello dispositivo virtual StorSimple).

**P.** É possível usar toocreate de cmdlets do PowerShell do Azure hello e gerenciar volumes fixados localmente? 

**A.** Não, você não pode criar volumes localmente afixados por meio de cmdlets do Azure PowerShell (qualquer volume criado por meio do Azure PowerShell é em camadas). Também sugerimos que você não use toomodify de cmdlets do PowerShell do Azure Olá as propriedades de um volume localmente afixado, conforme será ter Olá indesejado efeitos da modificação Olá tootiered de tipo de volume.

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>Perguntas sobre o backup de um volume localmente afixado
**P.** Há suporte a instantâneos locais de volumes localmente afixados?

**A.** Sim, você pode criar instantâneos locais de volumes localmente afixados. No entanto, é altamente recomendável que você regularmente os volumes localmente afixados tooensure de instantâneos de nuvem que seus dados sejam protegidos em backup Olá eventualidade de um desastre.

**P.** Há diretrizes para o gerenciamento de instantâneos locais para volumes localmente afixados?

**A.** Frequência de instantâneos locais junto com uma alta taxa de rotatividade de dados de saudação localmente volume afixado pode fazer com que o espaço local no hello dispositivo toobe consumido rapidamente e resultar em dados dos volumes em camadas que estão sendo enviados por push toohello nuvem. Portanto, sugerimos que minimizar o número de saudação de instantâneos locais.

**P.** Recebi um alerta informando que meus instantâneos locais de volumes localmente afixados podem ser invalidados. Quando isso acontece?

**A.** Frequência de instantâneos locais junto com uma alta taxa de rotatividade de dados de saudação localmente volume afixado pode causar o espaço local em Olá dispositivo toobe consumido rapidamente. Se camadas de saudação local do dispositivo de saudação são usadas, uma interrupção de nuvem estendida pode resultar em dispositivo Olá fiquem cheios e volume de toohello de gravações de entrada pode resultar em invalidação de instantâneos da saudação (como nenhum espaço existe tooupdate Olá instantâneos toorefer toohello mais antigos blocos de dados que foram substituídos). Tal uma saudação situação gravações toohello volume continuarão toobe servido, mas os instantâneos locais Olá podem ser inválidos. Não há nenhum instantâneo de nuvem impacto tooyour existente.

Aviso de alerta de saudação é toonotify você que tal situação pode surgir e certifique-se de que endereço Olá mesmo oportunamente revisando os instantâneos locais agenda tootake menos instantâneos locais frequentes ou excluir instantâneos locais mais antigos que não estão mais Necessário.

Se os instantâneos locais Olá sejam invalidados, você receberá um alerta de informações notificando que os instantâneos locais para a política de backup específico Olá Olá foram invalidados junto com a lista de saudação de carimbos de hora de instantâneos locais de saudação que foram invalidados. Esses instantâneos serão excluídos automaticamente e não será capaz de tooview em Olá **catálogos de Backup** página Olá portal clássico do Azure.

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>Perguntas sobre a conversão de um volume de tooa localmente afixado volume em camadas
**P.** Eu estou observando alguns lentidão no dispositivo de saudação durante a conversão de um volume do volume em camadas tooa fixado localmente. Por que isso está acontecendo? 

**A.** o processo de conversão Olá envolve duas etapas: 

1. Provisionamento de espaço no dispositivo Olá Olá volume ser convertido em breve fixado localmente.
2. Baixar todos os dados em camadas de saudação nuvem tooensure local garante.

Essas duas etapas são longos executando operações que dependem do tamanho de saudação do volume de hello está sendo convertido, os dados no dispositivo hello e largura de banda disponível. Como alguns dados de volumes em camadas existentes podem despejar toohello nuvem como parte do processo de provisionamento de saudação, seu dispositivo pode experimentar desempenho reduzido durante esse tempo. Além disso, o processo de conversão de saudação pode ser mais lento se:

* Os volumes existentes não foi feitos backup de nuvem toohello; Portanto, sugerimos que você fazer backup de seu tooinitiating anterior de volumes uma conversão.
* As políticas de limitação de largura de banda que foram aplicadas, o que poderá restringir a nuvem de toohello de largura de banda disponível Olá; Portanto, recomendamos que você tenha um dedicado de 40 Mbps ou mais nuvem toohello de conexão.
* o processo de conversão Olá pode levar várias horas devido toohello vários fatores explicados acima. Portanto, sugerimos que você executar esta operação durante horários não picos ou em um fim de semana tooavoid Olá impacto sobre consumidores finais.

Para obter mais informações sobre como muito[converter um volume do volume em camadas tooa fixado localmente](storsimple-manage-volumes-u2.md#change-the-volume-type)

**P.** Posso cancelar a operação de conversão de volume Olá?

**A.** Não, você não pode Olá Cancelar operação de conversão de saudação depois de iniciada. Como discutido na pergunta anterior de saudação, esteja ciente das Olá possíveis problemas de desempenho que você pode encontrar durante o processo de saudação e siga práticas recomendadas de saudação listadas acima, ao planejar sua conversão.

**P.** Se a operação de conversão de saudação falhar, o que acontece toomy volume?

**A.** Conversão de volume pode falhar devido a problemas de conectividade de toocloud. dispositivo de Olá eventualmente pode parar o processo de conversão de saudação após uma série de toobring tentativas malsucedidas de dados hierárquico da nuvem de saudação. Nesse cenário, o tipo de volume Olá continuará toobe Olá fonte volume tipo anterior tooconversion, e:

* Um alerta crítico será gerado toonotify de falha de conversão de volume hello. Para obter mais informações sobre [toolocally relacionados fixado volumes de alertas](storsimple-manage-alerts.md#locally-pinned-volume-alerts)
* Se você estiver convertendo um volume em camadas tooa fixado localmente, o volume Olá continuará tooexhibit propriedades de um volume em camadas que dados ainda podem residir na nuvem de saudação. Sugerimos que você resolver os problemas de conectividade hello e, em seguida, repita a operação de conversão de saudação.
* Da mesma forma, quando a conversão de um tooa localmente afixado em camadas falha do volume, embora o volume de saudação será marcado como um volume localmente afixado, ela funcionará como um volume em camadas (porque os dados podem ter vazados toohello nuvem). No entanto, ele continuará espaço toooccupy nas camadas de local de saudação do dispositivo hello. Esse espaço não estará disponível para outros volumes localmente afixados. Sugerimos que você repita tooensure esta operação que Olá volume conversão seja concluída e Olá o espaço local no dispositivo Olá a ser recuperada.

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>Perguntas sobre como restaurar um volume localmente afixado
**P.** Os volumes localmente afixados são restaurados instantaneamente?

**A.** Sim, os volumes localmente afixados são restaurados instantaneamente. Assim que as informações de metadados de saudação para o volume de saudação são extraídas da nuvem de saudação como parte da operação de restauração Olá, o volume de hello está online e pode ser acessado pelo host hello. No entanto, garantias locais para volume Olá dados não estarão presentes até que todos os dados de saudação foi baixado da nuvem hello e você pode enfrentar um desempenho reduzido nesses volumes durante saudação restauração de saudação.

**P.** Quanto tempo leva toorestore um volume localmente afixado?

**A.** Volumes localmente afixados serão restaurados instantaneamente e colocados online, assim como informações de metadados de volume Olá são recuperadas da nuvem Olá, enquanto os dados de volume Olá continuam toobe baixado em segundo plano de saudação. Esta última parte da operação de restauração de hello – voltando garantias local Olá Olá para dados de volume - é uma operação demorada e pode levar várias horas para todos os toobe de dados Olá torna local novamente. Olá tempo toocomplete hello mesmo depende de vários fatores, como tamanho de saudação do volume hello está sendo restaurado e Olá largura de banda disponível. Se o volume original de saudação que está sendo restaurado foi excluído, mais tempo será levado toocreate Olá local espaço Olá dispositivo como parte da operação de restauração de saudação.

**P.** Preciso de toorestore meu existente localmente fixados instantâneo mais antigo de tooan de volume (obtido quando o volume de saudação foi em camadas). Volume Olá voltará como camadas nesse caso?

**A.** Não, o volume de saudação será restaurado como um volume localmente afixado. Embora Olá instantâneo tempo toohello de datas ao volume Olá foi hierárquico, ao restaurar volumes existentes, o StorSimple sempre usa o tipo de saudação do volume no disco hello como existe atualmente.

**P.** Eu estendido Meu volume localmente afixado recentemente, mas agora preciso toorestore Olá dados tooa hora do volume Olá menor em tamanho. Restauração redimensionará volume atual hello e será necessário tooextend tamanho de saudação do volume Olá após a conclusão da restauração Olá?

**A.** Sim, restauração Olá será redimensionado o volume de saudação e você precisará tooextend Olá tamanho do hello volume após a restauração de saudação.

**P.** Pode alterar o tipo de saudação de um volume durante a restauração?

**R.**não, você não pode alterar o tipo de volume Olá durante a restauração.

* Volumes que tenham sido excluídos são restaurados como tipo de saudação armazenado no instantâneo de saudação.
* Os volumes existentes são restaurados com base em seu tipo atual, independentemente do tipo hello armazenado no instantâneo de saudação (consulte Perguntas toohello dois anterior).

**P.** Preciso toorestore Meu volume localmente afixado mas selecionei um ponto incorreto no instantâneo de tempo. Posso cancelar a operação de restauração atual Olá?

**A.** Sim, você pode cancelar uma operação de restauração em andamento. estado de saudação do volume Olá será revertido estado toohello no início de saudação da restauração de saudação. No entanto, todas as gravações feitas toohello volume enquanto restauração Olá estava em andamento serão perdidas.

**P.** Comecei uma operação de restauração em um de meus volumes localmente afixados e agora há um instantâneo no catálogo de lista de pendências que não me lembro de ter criado. Para que isso é usado?

**A.** Isso é Olá temporário instantâneo é criado a operação de restauração anterior toohello e é usado para reversão no caso de restauração Olá foi cancelada ou falha. Não exclua esse instantâneo; ele serão automaticamente excluído quando Olá restauração for concluída. Isso poderá ocorrer se o trabalho de restauração tiver apenas volumes fixados localmente ou uma combinação de volumes fixados e em camadas. Se o trabalho de restauração de saudação inclui apenas os volumes em camadas, em seguida, esse comportamento não ocorrerá.

**P.** Posso clonar um volume localmente afixado?

**A.** Sim, pode. No entanto, volume Olá localmente fixado será clonada como um volume em camadas por padrão. Para obter mais informações sobre como muito[clonar um volume localmente afixado](storsimple-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>Perguntas sobre como fazer o failover de um volume localmente afixado
**P.** Preciso de toofail em meu dispositivo físico do dispositivo tooanother. O failover será feito nos volumes localmente afixados como localmente afixados ou em camadas?

**A.** Dependendo da versão do software de dispositivo de destino Olá Olá, volumes afixados localmente serão submetidos a failover como:

* Localmente afixado se estiver executando o dispositivo de destino Olá StorSimple 8000 series atualização 2
* Em camadas se estiver executando o dispositivo de destino Olá StorSimple 8000 série atualização 1. x
* Em camadas se o dispositivo de destino Olá appliance de nuvem hello (atualização de versão 2 do software ou atualização 1. x)

Mais informações sobre [o failover e a DR de volumes fixos localmente entre versões](storsimple-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**P.** Os volumes localmente afixados são restaurados instantaneamente durante a RD (recuperação de desastre)?

**A.** Sim, os volumes localmente afixados são restaurados instantaneamente durante o failover. Assim como informações de metadados de saudação para o volume de saudação são extraídas da nuvem de saudação como parte da operação de failover de saudação, o volume de Olá é colocada online no dispositivo de destino hello e pode ser acessado pelo host hello. Enquanto isso, dados de volume de saudação continuarão toodownload no plano de fundo Olá, e você pode enfrentar desempenho reduzido nesses volumes durante Olá Olá failover.

**P.** Consulte o trabalho de failover Olá concluído, como pode rastrear progresso de saudação do volume localmente afixado que está sendo restaurado no dispositivo de destino Olá?

**A.** Durante uma operação de failover, o trabalho de failover hello está marcado como concluído depois que todos os volumes de saudação no conjunto de failover de saudação foram instantaneamente restaurados e colocados online no dispositivo de destino de saudação. Isso inclui todos os volumes localmente afixados falha podem ter sido No entanto, garantias de locais de dados Olá só estarão disponíveis quando todos os dados de saudação para o volume de saudação foi baixado. Você pode acompanhar esta progresso para cada volume localmente afixado falhou com monitoramento Olá correspondente trabalhos de restauração que são criados como parte do failover de saudação. Esses trabalhos de restauração individuais só serão criados para volumes localmente afixados.

**P.** Pode alterar o tipo de saudação de um volume durante o failover?

**A.** Não, você não pode alterar o tipo de volume Olá durante um failover. Se você estiver realizando o failover tooanother físico dispositivo que está executando a atualização de série StorSimple 8000 2 de volumes de saudação realizarão failover com base no tipo de volume Olá armazenado no instantâneo de saudação. Durante o failover tooany outra versão do dispositivo, consulte a pergunta de toohello acima em tipo de volume Olá após um failover.

**P.** Podem falhar em um contêiner de volume com o dispositivo de nuvem toohello volumes fixados localmente?

**A.** Sim, pode. Olá localmente afixado volumes serão submetidos a failover como volumes em camadas. Mais informações sobre [o failover e a DR de volumes fixos localmente entre versões](storsimple-device-failover-disaster-recovery.md#considerations-for-device-failover)

