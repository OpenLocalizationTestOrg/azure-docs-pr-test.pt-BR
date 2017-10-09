---
title: aaaManage seus volumes do StorSimple (U2) | Microsoft Docs
description: "Explica como tooadd, modificar, monitorar e excluir volumes do StorSimple e tootake-los offline, se necessário."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>Usar Olá StorSimple Manager serviço toomanage volumes (atualização 2)
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Visão geral
Este tutorial explica como toouse Olá toocreate do serviço StorSimple Manager e gerenciar volumes no dispositivo do StorSimple hello e o dispositivo virtual StorSimple com atualização 2 instalado.

Olá serviço StorSimple Manager é uma extensão em Olá portal clássico do Azure que permite que você gerencie sua solução StorSimple de uma única interface da web. Em volumes de toomanaging adição, você pode usar toocreate de serviço do StorSimple Manager hello e gerenciar serviços do StorSimple, exibir e gerenciar dispositivos, exibir alertas, exibir e gerenciar políticas de backup e o catálogo de backup hello.

## <a name="volume-types"></a>Tipos de volumes
Os volumes do StorSimple podem ser:

* **Localmente afixado volumes**: dados nesses volumes permanecem no dispositivo StorSimple local de saudação em todos os momentos.
* **Em camadas volumes**: dados nesses volumes podem despejar toohello nuvem.

Um volume de arquivamento é um tipo de volume em camadas. Olá maior eliminação de duplicação parte tamanho usado para volumes de arquivamento permite que os segmentos maior de saudação dispositivo tootransfer de toohello de dados na nuvem. 

Se necessário, você pode alterar o tipo de volume de saudação de tootiered local ou de toolocal em camadas. Para obter mais informações, vá muito[alterar o tipo de volume Olá](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volumes fixados localmente
Volumes localmente afixados são totalmente provisionados volumes que não camada de dados na nuvem toohello, garantindo assim local garante de dados primários, independentemente de conectividade de nuvem. Dados em volumes afixados localmente não são deduplicados nem compactados; no entanto, instantâneos de volumes afixados localmente são deduplicados. 

Volumes afixados localmente são totalmente provisionados; portanto, você deve ter espaço suficiente no dispositivo ao criá-los. Você pode provisionar volumes localmente afixados até tooa o tamanho máximo de 8 TB no dispositivo Olá StorSimple 8100 e 20 TB em dispositivo 8600 de saudação. StorSimple reserva espaço local restantes em Olá no dispositivo de saudação de instantâneos, metadados e processamento de dados. Você pode aumentar o tamanho de saudação de um volume localmente afixado toohello espaço máximo disponível, mas não é possível diminuir o tamanho de saudação de um volume depois de criado.

Quando você cria um volume localmente afixado, o espaço disponível de saudação para criação de volumes em camadas é reduzido. Olá inverso também é verdadeiro: se você tiver volumes em camadas existentes, Olá espaço para criar localmente fixados volumes será menor do que os limites máximos Olá mencionados acima. Para obter mais informações sobre volumes locais, consulte toohello [perguntas frequentes sobre volumes localmente afixados](storsimple-local-volume-faq.md).   

### <a name="tiered-volumes"></a>Volumes hierárquicos
Volumes em camadas são volumes escassamente provisionados no qual Olá frequentemente dados acessados permanece local no dispositivo hello e menos dados usados com frequência é automaticamente hierárquico toohello nuvem. O provisionamento dinâmico é uma tecnologia de virtualização na qual o armazenamento disponível aparece recursos físicos tooexceed. Em vez de reservar um armazenamento suficiente antecedência, StorSimple usa tooallocate provisionamento thin suficiente requisitos de espaço atual em toomeet. a natureza elástica Olá de armazenamento em nuvem facilita essa abordagem porque StorSimple pode aumentar ou diminuir a nuvem armazenamento toomeet demandas em constante mudança.

Se você estiver usando Olá volume em camadas para dados de arquivamento, selecionando Olá **usar este volume para dados de arquivamento acessados com frequência menos** caixa de seleção altera o tamanho do bloco de eliminação de duplicação de saudação para seu volume too512 KB. Se você não selecionar essa opção, o volume em camadas correspondente de saudação usará um tamanho de bloco de 64 KB. Um tamanho de bloco de eliminação de duplicação maior permite a transferência de saudação do hello dispositivo tooexpedite da nuvem de toohello grandes de dados de arquivamento.

> [!NOTE]
> Arquivamento volumes criados com uma versão de pré-atualização 2 do StorSimple serão importados como em camadas com hello arquivamento caixa de seleção.
> 
> 

### <a name="provisioned-capacity"></a>Capacidade provisionada
Consulte toohello para máxima capacidade provisionada para cada tipo de dispositivo e o volume a tabela a seguir. (Observe que os volumes afixados localmente não estão disponíveis em um dispositivo virtual.)

|  | Tamanho máximo do volume em camadas | Tamanho máximo de volume afixado localmente |
| --- | --- | --- |
| **Dispositivos físicos** | | |
| 8100 |64 TB |8 TB |
| 8600 |64 TB |20 TB |
| **Dispositivos virtuais** | | |
| 8010 |30 TB |N/D |
| 8020 |64 TB |N/D |

## <a name="hello-volumes-page"></a>página de Volumes Olá
Olá **Volumes** página permite que você toomanage Olá os volumes de armazenamento que são provisionados no dispositivo do Microsoft Azure StorSimple Olá para os seus iniciadores (servidores). Ele exibe a lista de saudação de volumes em seu dispositivo StorSimple.

 ![Página Volumes](./media/storsimple-manage-volumes-u2/VolumePage.png)

Um volume consiste em uma série de atributos:

* **Nome do volume** – um nome descritivo que deve ser exclusivo e ajuda a identificar o volume de saudação. Esse nome também é usado em relatórios de monitoramento ao filtrar um volume específico.
* **Status** – Pode ser online ou offline. Se o volume estiver offline, não é visível tooinitiators (servidores) que têm permissão de acesso toouse Olá volume.
* **Capacidade** – Especifica a quantidade total de saudação de dados que podem ser armazenados pelo iniciador da saudação (servidor). Volumes localmente fixados são totalmente provisionados e residem no dispositivo do StorSimple hello. Volumes em camadas são escassamente provisionados e eliminação de duplicação de dados de saudação. Com volumes de provisionamento thin, seu dispositivo não pré-aloca a capacidade de armazenamento físico internamente ou na nuvem de saudação de acordo com a capacidade de volume tooconfigured. a capacidade de volume Olá é alocada e consumida sob demanda.
* **Tipo** – indica se o volume de saudação é **em camadas** (Olá padrão) ou **localmente afixado**.
* **Backup** – indica se uma política de backup padrão existe para o volume de saudação.
* **Acesso** – Especifica os iniciadores de saudação (servidores) que têm permissão de acesso toothis volume. Os iniciadores que não são membros de registro de controle de acesso (ACR) que está associado ao volume de saudação não poderão ver o volume de saudação.
* **Monitoramento** – Especifica se um volume está sendo monitorado. Um volume terá o monitoramento ativado por padrão quando ele é criado. O monitoramento será, no entanto, desabilitado para um clone de volume. tooenable monitoramento para um volume, siga as instruções de saudação em [monitorar um volume](#monitor-a-volume). 

Use as instruções de saudação este Olá tooperform tutorial tarefas a seguir:

* Adicionar um volume 
* Modificar um volume 
* Alterar o tipo de volume Olá
* Excluir um volume 
* Colocar um volume offline 
* Monitorar um volume 

## <a name="add-a-volume"></a>Adicionar um volume
Você [criou um volume](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) durante a implantação da solução StorSimple. Adicionar um volume é um procedimento semelhante.

#### <a name="tooadd-a-volume"></a>tooadd um volume
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** guia.
2. Selecione um contêiner de volume na lista de saudação e clique duas vezes nele tooaccess Olá volumes associados ao contêiner de saudação.
3. Clique em **adicionar** final Olá Olá página. Inicia o Assistente adicionar um volume de saudação.
   
     ![Configurações básicas do assistente para Adicionar volume](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. Em hello Assistente de adição de um volume, em **configurações básicas**, Olá a seguir:
   
   1. Digite um **Nome** para o seu volume.
   2. Selecione um **tipo de uso** da lista suspensa de saudação. Para cargas de trabalho que exigem dados toobe disponível localmente no dispositivo de saudação em todos os momentos, selecione **localmente afixado**. Para todos os outros tipos de dados, selecione **Em camadas**. (**Em camadas** é saudação padrão.)
   3. Se você selecionou **em camadas** na etapa 2, você pode selecionar Olá **usar este volume para dados de arquivamento acessados com frequência menos** caixa de seleção tooconfigure um volume de arquivamento.
   4. Digite hello **capacidade provisionada** para seu volume em GB ou TB. Consulte [Capacidade provisionada](#provisioned-capacity) para tamanhos máximos de cada dispositivo e tipo de volume. Examinar Olá **capacidade disponível** toodetermine quanto armazenamento está realmente disponível no seu dispositivo.
5. Clique no ícone de seta Olá![Ícone de seta](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). Se você estiver configurando um volume localmente afixado, você verá a seguinte mensagem de saudação.
   
    ![Tipo de mensagem Alterar volume](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. Clique no ícone de seta Olá ![ícone de seta](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)novamente toogo toohello **configurações adicionais** página.
   
    ![Configurações adicionais do assistente para Adicionar volume](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. Em **Configurações Adicionais**, adicione um novo registro de controle de acesso (ACR):
   
   1. Selecione um registro de controle de acesso (ACR) na lista suspensa de saudação. Como opção, você também pode abrir um novo ACR. ACRs determinam quais hosts podem acessar seus volumes por correspondência Olá IQN de host com o listado no registro de saudação. Se você não especificar um ACR, você verá a seguinte mensagem de saudação.
      
        ![Especifique um ACR](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. Recomendamos que você selecione Olá **habilitar um backup padrão para este volume** caixa de seleção.
   3. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) volume de saudação toocreate com hello especificado as configurações.

Novo volume agora está pronto toouse.

> [!NOTE]
> Se você cria um volume afixado localmente e, em seguida, cria outro localmente fixados volume imediatamente depois disso, os trabalhos de criação de volume Olá são executados sequencialmente. trabalho de criação de volume primeiro Olá deve concluir antes de começar o próximo trabalho de criação de volume hello.
> 
> 

## <a name="modify-a-volume"></a>Modificar um volume
Modificar um volume quando precisar tooexpand-lo ou alterar Olá hosts que acessam o volume de saudação.

> [!IMPORTANT]
> * Se você modificar o tamanho do volume Olá no dispositivo Olá, tamanho do volume Olá precisa toobe alterado no host de saudação também. 
> * etapas do lado do host Olá descritas aqui são para o Windows Server 2012 (2012R2). Procedimentos para Linux ou para outros sistemas operacionais host serão diferentes. Consulte tooyour instruções do sistema operacional de host ao modificar o volume de saudação em um host executando outro sistema operacional. 
> 
> 

#### <a name="toomodify-a-volume"></a>toomodify um volume
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** guia.
2. Selecione um contêiner de volume na lista de saudação e clique duas vezes nele volumes de saudação tooview associados ao contêiner de saudação.
3. Selecione um volume e final Olá Olá página, clique em **modificar**. Olá Modificar volume assistente é iniciado.
4. Em Olá Assistente para modificar volume, em **configurações básicas**, você pode fazer a seguir hello:
   
   * Editar saudação **nome**.
   * Converter Olá **tipo de uso** de tootiered localmente afixado ou de toolocally hierárquico fixado (consulte [alterar o tipo de volume Olá](#change-the-volume-type) para obter mais informações).
   * Aumentar Olá **capacidade provisionada**. Olá **capacidade provisionada** só pode ser aumentado. Não é possível reduzir um volume depois que ele é criado.
5. Em **configurações adicionais**, você pode modificar Olá ACR, desde que o volume de saudação está offline. Se o volume de saudação estiver online, você precisará tootake-lo primeiro offline. Consulte as etapas toohello [colocar um volume offline](#take-a-volume-offline) toomodifying anterior Olá ACR.
   
   > [!NOTE]
   > Não é possível alterar Olá **habilitar um backup padrão** opção para o volume de saudação.
   > 
   > 
6. Salvar as alterações clicando o ícone de verificação de saudação ![check-icon](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). Olá portal clássico do Azure exibirá uma mensagem de volume de atualização. Ele exibirá uma mensagem de êxito quando o volume de saudação foi atualizado com êxito.
7. Se você está expandindo um volume, conclua Olá seguindo as etapas em seu computador de host do Windows:
   
   1. Vá muito**gerenciamento do computador** ->**gerenciamento de disco**.
   2. Clique com o botão direito do mouse em **Gerenciamento de Disco** e selecione **Examinar Discos Novamente**.
   3. Na lista de saudação de discos, selecione o volume Olá atualizados, com o botão direito e selecione **estender Volume**. Olá estender Volume assistente é iniciado. Clique em **Avançar**.
   4. Conclua o Assistente de saudação, aceitando os valores padrão de saudação. Concluído o Assistente de saudação, volume Olá deve mostrar Olá maior tamanho.
      
      > [!NOTE]
      > Se você expandir um volume localmente afixado e, em seguida, expanda outro localmente fixados volume logo depois, trabalhos de expansão de volume Olá são executados sequencialmente. trabalho de expansão de volume primeiro Olá deve concluir antes de começar o próximo trabalho de expansão de volume hello.
      > 
      > 

![Vídeo disponível](./media/storsimple-manage-volumes-u2/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como tooexpand um volume, clique em [aqui](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="change-hello-volume-type"></a>Alterar o tipo de volume Olá
Você pode alterar o tipo de volume de saudação do toolocally hierárquico fixado ou de tootiered localmente afixado. No entanto, essa conversão não deve ser uma ocorrência frequente. Algumas das razões para a conversão de um volume em camadas toolocally fixado são:

* Garantias locais sobre disponibilidade e desempenho dos dados
* Eliminação de latências de nuvem e problemas de conectividade de nuvem.

Normalmente, esses são pequenos volumes existentes que você deseja tooaccess com frequência. Um volume afixado localmente é totalmente provisionado quando é criado. Se você estiver convertendo um volume do volume em camadas tooa fixado localmente, StorSimple verifica se você tem espaço suficiente em seu dispositivo antes de começar a conversão de saudação. Se você tiver espaço suficiente, você receberá um erro e operação hello será cancelada. 

> [!NOTE]
> Antes de começar uma conversão de em camadas toolocally fixado, certifique-se de que você considere Olá requisitos de espaço de outras cargas de trabalho. 
> 
> 

Talvez você queira toochange tooa um volume localmente afixado em camadas volume se você precisar de mais espaço tooprovision outros volumes. Quando você converte Olá localmente afixado volume tootiered, Olá capacidade disponível no aumento de dispositivo Olá por tamanho de saudação da capacidade de saudação liberada. Se problemas de conectividade impedir que a conversão de saudação de um volume de saudação tipo local toohello hierárquico tipo, hello volume local exibirá propriedades de um volume em camadas até que a conversão de saudação é concluída. Isso ocorre porque alguns dados podem ter vazados toohello nuvem. Esses dados derramados continuarão toooccupy o espaço local no dispositivo Olá que não pode ser liberado até que a operação de saudação é reiniciada e concluída.

> [!NOTE]
> Converter um volume pode levar algum tempo e não é possível cancelar uma conversão depois de iniciada. volume Olá permanecerá online durante a conversão de Olá e fazer o backup, mas você não pode expandir ou restaurar o volume de saudação enquanto conversão Olá estiver ocorrendo.  
> 
> 

Conversão de um volume em camadas tooa localmente afixado pode afetar adversamente o desempenho do dispositivo. Além disso, Olá fatores a seguir pode aumentar o tempo de saudação que leva a conversão de saudação toocomplete:

* Não há largura de banda suficiente.
* Não há backup atual.

efeitos de saudação toominimize que esses fatores podem ter:

* Examine suas políticas de limitação de largura de banda e certifique-se de que uma largura de banda dedicada de 40 Mbps está disponível.
* Agende a conversão de saudação do horário de pico.
* Pegue um instantâneo antes de iniciar a conversão de saudação.

Se você estiver convertendo vários volumes (suporte a cargas de trabalho diferentes), você deve priorizar conversão do volume Olá para que os volumes de prioridade mais altos são convertidos primeiro. Por exemplo, é necessário converter os volumes que hospedam VMs (máquinas virtuais) ou volumes com cargas de trabalho do SQL antes de converter volumes com cargas de trabalho de compartilhamento de arquivos.

#### <a name="toochange-hello-volume-type"></a>tipo de volume Olá toochange
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** guia.
2. Selecione um contêiner de volume na lista de saudação e clique duas vezes nele volumes de saudação tooview associados ao contêiner de saudação.
3. Selecione um volume e final Olá Olá página, clique em **modificar**. Olá Modificar volume assistente é iniciado.
4. Em Olá **configurações básicas** página, altere o tipo de uso de saudação selecionando o novo tipo de saudação do hello **tipo de uso** lista suspensa.
   
   * Se você estiver alterando o tipo de saudação muito**localmente afixado**, StorSimple irá verificar toosee se não houver capacidade suficiente.
   * Se você estiver alterando o tipo de saudação muito**em camadas** e esse volume será usado para dados de arquivamento, selecione Olá **usar este volume para dados de arquivamento acessados com frequência menos** caixa de seleção.
     
       ![Caixa de seleção Arquivo Morto](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. Clique no ícone de seta Olá ![ícone de seta](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toogo toohello **configurações adicionais** página. Se você estiver configurando um volume localmente afixado, hello seguinte mensagem será exibida.
   
    ![Tipo de mensagem Alterar volume](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. Clique no ícone de seta Olá ![Ícone de seta](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) novamente, toocontinue.
7. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) processo de conversão de saudação toostart. Olá portal do Azure exibirá uma mensagem de volume de atualização. Ele exibirá uma mensagem de êxito quando o volume de saudação foi atualizado com êxito.

## <a name="take-a-volume-offline"></a>Colocar um volume offline
Talvez seja necessário tootake um volume offline quando você estiver planejando toomodify-lo ou exclua-lo. Quando um volume está offline, não está disponível para acesso de leitura / gravação. Você precisará tootake Olá volume offline no host hello, bem como no dispositivo de saudação. 

#### <a name="tootake-a-volume-offline"></a>tootake um volume offline
1. Certifique-se de que o volume de saudação em questão não está em uso antes de colocá-lo offline.
2. Olá primeiro coloque volume offline no host de saudação. Isso eliminará qualquer risco potencial de corrupção de dados no volume de saudação. Para etapas específicas, consulte as instruções de toohello para seu sistema operacional do host.
3. Depois de saudação host estiver offline, coloque o volume de saudação no dispositivo Olá off-line executando Olá etapas a seguir:
   
   1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** Olá guia **contêineres de Volume** guia listas em um formato tabular todos os Olá contêineres de volume que estão associados ao dispositivo hello.
   2. Selecione um contêiner de volume e clique em lista de saudação toodisplay de todos os volumes Olá Olá contêiner.
   3. Selecione um volume e clique em **Colocar offline**.
   4. Quando solicitado a confirmar, clique em **Sim**. volume Olá agora deve estar offline.
      
      Depois que um volume estiver offline, Olá **colocar Online** opção ficará disponível.

> [!NOTE]
> Olá **colocar Offline** comando envia um toohello dispositivo tootake Olá volume offline. Se os hosts ainda estiverem usando o volume de hello, isso resulta em interrupções nas conexões, mas colocar offline o volume de saudação não falhará. 
> 
> 

## <a name="delete-a-volume"></a>Excluir um volume
> [!IMPORTANT]
> Você pode excluir um volume apenas se ele estiver offline.
> 
> 

Concluir Olá etapas toodelete um volume a seguir.

#### <a name="toodelete-a-volume"></a>toodelete um volume
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** guia.
2. Selecione o contêiner de volume de saudação que tem o volume a saudação ser toodelete. Clique em Olá Olá de tooaccess de contêiner de volume **Volumes** página.
3. Todos os volumes de saudação associados a este contêiner são exibidos em um formato tabular. Verificar o status de saudação do volume Olá deseja toodelete. Se o volume Olá toodelete desejado não estiver offline, etapas-lo offline Olá primeiro, o seguinte [colocar um volume offline](#take-a-volume-offline).
4. Depois de saudação volume estiver offline, clique em **excluir** final Olá Olá página.
5. Quando solicitado a confirmar, clique em **Sim**. volume de saudação será excluída e Olá **Volumes** página mostrará a lista de saudação atualizada de volumes no contêiner de saudação.
   
   > [!NOTE]
   > Se você excluir um volume localmente afixado, espaço para novos volumes Olá pode não ser atualizado imediatamente. Olá serviço StorSimple Manager atualiza disponível de espaço local Olá periodicamente. Sugerimos que você aguarde alguns minutos antes de tentar de novo volume do toocreate hello.<br> Além disso, se você excluir um volume localmente afixado e, em seguida, excluir outro localmente fixados volume logo depois, trabalhos de exclusão do volume de saudação são executados sequencialmente. trabalho de exclusão de volume primeiro Olá deve concluir antes de começar o próximo trabalho de exclusão de volume hello.
   > 
   > 

## <a name="monitor-a-volume"></a>Monitorar um volume
Monitoramento de volume permite estatísticas de toocollect relacionados de I/O para um volume. Monitoramento é habilitado por padrão para Olá primeiros 32 volumes que você criar. O monitoramento de volumes adicionais é desabilitado por padrão. Monitoramento de volumes clonados também será desabilitado por padrão.

Execute Olá tooenable as etapas a seguir ou desabilitar o monitoramento para um volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable ou desabilite o monitoramento de volume
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** guia.
2. Selecione Olá contêiner de volume no qual Olá volume reside e clique em Olá Olá de tooaccess de contêiner de volume **Volumes** página.
3. Todos os volumes de saudação associados a este contêiner são listados na exibição tabular hello. Clique e selecione o volume de saudação ou clone de volume.
4. Final Olá Olá página, clique em **modificar**.
5. No Assistente para modificar Volume de hello, em **configurações básicas**, selecione **habilitar** ou **desabilitar** de saudação **monitoramento** lista suspensa.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[clonar um volume StorSimple](storsimple-clone-volume.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

