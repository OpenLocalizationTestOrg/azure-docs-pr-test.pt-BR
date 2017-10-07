---
title: "volumes do StorSimple aaaManage (atualização 3) | Microsoft Docs"
description: "Explica como tooadd, modificar, monitorar e excluir volumes do StorSimple e tootake-los offline, se necessário."
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
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>Usar Olá Gerenciador de dispositivos do StorSimple service toomanage volumes (atualização 3 ou posterior)

## <a name="overview"></a>Visão geral

Este tutorial explica como toouse Olá toocreate de serviço do Gerenciador de dispositivos do StorSimple e gerenciar volumes em dispositivos da série Olá StorSimple 8000 que executam a atualização 3 e posterior.

saudação de serviço do Gerenciador de dispositivos do StorSimple é uma extensão em Olá portal do Azure que permite que você gerencie sua solução StorSimple de uma única interface da web. Use volumes do hello toomanage portal do Azure em todos os seus dispositivos. Você também pode criar e gerenciar serviços StorSimple, gerenciar dispositivos, políticas de backup e o catálogo de backup e exibir alertas.

## <a name="volume-types"></a>Tipos de volumes

Os volumes do StorSimple podem ser:

* **Localmente afixado volumes**: dados nesses volumes permanecem no dispositivo StorSimple local de saudação em todos os momentos.
* **Em camadas volumes**: dados nesses volumes podem despejar toohello nuvem.

Um volume de arquivamento é um tipo de volume em camadas. Olá maior eliminação de duplicação parte tamanho usado para volumes de arquivamento permite que os segmentos maior de saudação dispositivo tootransfer de toohello de dados na nuvem.

Se necessário, você pode alterar o tipo de volume de saudação de tootiered local ou de toolocal em camadas. Para obter mais informações, vá muito[alterar o tipo de volume Olá](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volumes fixados localmente

Volumes localmente afixados são totalmente provisionados volumes que não camada de dados na nuvem toohello, garantindo assim local garante de dados primários, independentemente de conectividade de nuvem. Dados em volumes afixados localmente não são deduplicados nem compactados; no entanto, instantâneos de volumes afixados localmente são deduplicados. 

Volumes afixados localmente são totalmente provisionados; portanto, você deve ter espaço suficiente no dispositivo ao criá-los. Você pode provisionar volumes localmente afixados até tooa o tamanho máximo de 8 TB no dispositivo Olá StorSimple 8100 e 20 TB em dispositivo 8600 de saudação. StorSimple reserva espaço local restantes em Olá no dispositivo de saudação de instantâneos, metadados e processamento de dados. Você pode aumentar o tamanho de saudação de um volume localmente afixado toohello espaço máximo disponível, mas não é possível diminuir o tamanho de saudação de um volume depois de criado.

Quando você cria um volume localmente afixado, o espaço disponível de saudação para criação de volumes em camadas é reduzido. Olá inverso também é verdadeiro: se você tiver volumes em camadas existentes, Olá espaço para criar localmente fixados volumes será menor do que os limites máximos Olá mencionados acima. Para obter mais informações sobre volumes locais, consulte toohello [perguntas frequentes sobre volumes localmente afixados](storsimple-8000-local-volume-faq.md).

### <a name="tiered-volumes"></a>Volumes hierárquicos

Volumes em camadas são volumes escassamente provisionados no qual Olá frequentemente dados acessados permanece local no dispositivo hello e menos dados usados com frequência é automaticamente hierárquico toohello nuvem. O provisionamento dinâmico é uma tecnologia de virtualização na qual o armazenamento disponível aparece recursos físicos tooexceed. Em vez de reservar um armazenamento suficiente antecedência, StorSimple usa tooallocate provisionamento thin suficiente requisitos de espaço atual em toomeet. a natureza elástica Olá de armazenamento em nuvem facilita essa abordagem porque StorSimple pode aumentar ou diminuir a nuvem armazenamento toomeet demandas em constante mudança.

Se você estiver usando Olá volume em camadas para dados de arquivamento, selecione Olá **usar este volume para dados de arquivamento acessados com frequência menos** tamanho da parte caixa de seleção toochange Olá eliminação de duplicação para seu volume too512 KB. Se você não selecionar essa opção, o volume em camadas correspondente de saudação usará um tamanho de bloco de 64 KB. Um tamanho de bloco de eliminação de duplicação maior permite a transferência de saudação do hello dispositivo tooexpedite da nuvem de toohello grandes de dados de arquivamento.


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

## <a name="hello-volumes-blade"></a>folha de volumes Olá

Olá **Volumes** folha permite que volumes de armazenamento de saudação toomanage que são provisionados no dispositivo do Microsoft Azure StorSimple Olá para os seus iniciadores (servidores). Ele exibe a lista de saudação de volumes Olá StorSimple dispositivos conectados tooyour serviço.

 ![Página Volumes](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

Um volume consiste em uma série de atributos:

* **Nome do volume** – um nome descritivo que deve ser exclusivo e ajuda a identificar o volume de saudação. Esse nome também é usado em relatórios de monitoramento ao filtrar um volume específico. Após criar o volume de saudação, ela não pode ser renomeada.
* **Status** – Pode ser online ou offline. Se o volume estiver offline, não é visível tooinitiators (servidores) que têm permissão de acesso toouse Olá volume.
* **Capacidade** – Especifica a quantidade total de saudação de dados que podem ser armazenados pelo iniciador da saudação (servidor). Volumes localmente fixados são totalmente provisionados e residem no dispositivo do StorSimple hello. Volumes em camadas são escassamente provisionados e eliminação de duplicação de dados de saudação. Com volumes de provisionamento thin, seu dispositivo não pré-aloca a capacidade de armazenamento físico internamente ou na nuvem de saudação de acordo com a capacidade de volume tooconfigured. a capacidade de volume Olá é alocada e consumida sob demanda.
* **Tipo** – indica se o volume de saudação é **em camadas** (Olá padrão) ou **localmente afixado**.

Use as instruções de saudação este Olá tooperform tutorial tarefas a seguir:

* Adicionar um volume 
* Modificar um volume 
* Alterar o tipo de volume Olá
* Excluir um volume 
* Colocar um volume offline 
* Monitorar um volume 

## <a name="add-a-volume"></a>Adicionar um volume

Você [criou um volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) durante a implantação do dispositivo StorSimple da série 8000. Adicionar um volume é um procedimento semelhante.

#### <a name="tooadd-a-volume"></a>tooadd um volume

1. Da lista tabular de saudação de dispositivos Olá Olá **dispositivos** folha, selecione seu dispositivo. Clique em **+ Adicionar volume**.

    ![Adicionar um novo volume](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. Em Olá **adicionar um volume** folha:
   
    1. Olá **Selecione dispositivo** campo será preenchido automaticamente com o dispositivo atual.

    2. Da lista suspensa de saudação, selecione o contêiner de volume de saudação em que você precisa tooadd um volume.

    3.  Digite uma **Nome** para o seu volume. Após criar o volume de Olá, você não pode renomear o volume de saudação.

    4. Na lista suspensa de hello, selecione Olá **tipo** para seu volume. Para cargas de trabalho que exigem garantias locais, menos latências e um melhor desempenho, selecione um volume **Fixado localmente** . Para todos os outros dados, selecione um volume **Em camadas** . Se estiver usando esse volume para dados de arquivamento, marque **Usar este volume para dados de arquivamento acessados com menos frequência**.
      
       Um volume em camadas é provisionado por completo e pode ser criado rapidamente. Selecionando **usar este volume para dados de arquivamento acessados com frequência menos** de volume em camadas direcionado para o tamanho de bloco de eliminação de duplicação dados de arquivamento alterações Olá para seu volume too512 KB. Se esse campo não estiver marcado, o volume de em camadas correspondente Olá usa um tamanho de bloco de 64 KB. Um tamanho de bloco de eliminação de duplicação maior permite a transferência de saudação do hello dispositivo tooexpedite da nuvem de toohello grandes de dados de arquivamento.
       
       Um volume localmente afixado é muito provisionado e garante que os dados primários de saudação no volume de saudação permanece dispositivo toohello local e não despejar toohello nuvem.  Se você criar um volume localmente afixado, Olá dispositivo verificará o espaço disponível nas camadas local Olá tooprovision volume de saudação do hello solicitado tamanho. operação Olá de criação de um volume localmente afixado pode envolver o despejo de dados existentes da nuvem de toohello dispositivo hello e tempo Olá volume de saudação toocreate pode ser longo. tempo total de saudação depende do tamanho de saudação do volume Olá provisionado, largura de banda disponível e dados Olá em seu dispositivo.

    5. Especifique a saudação **capacidade provisionada** para seu volume. Tome nota da capacidade de saudação que está disponível com base no tipo de volume de saudação selecionado. Olá especificado o tamanho do volume não deve exceder o espaço disponível de saudação.
      
       Você pode provisionar volumes em camadas até too200 TB no dispositivo 8100 Olá ou volumes localmente afixados backup too8.5 TB. No dispositivo 8600 maior de saudação, você pode provisionar volumes localmente afixados backup too22.5 TB ou volumes em camadas até too500 TB. Como espaço local no dispositivo Olá Olá toohost necessário trabalho conjunto de volumes em camadas, criação de volumes localmente afixados afeta Olá espaço disponível para provisionar volumes em camadas. Portanto, se você criar um volume fixado localmente, o espaço disponível para a criação de volumes em camadas será reduzido. Da mesma forma, se for criado um volume em camadas, espaço disponível de saudação para a criação de volumes localmente afixados é reduzido.
      
       Se você provisionar um volume localmente afixado de 8,5 TB (tamanho máximo permitido) em seu dispositivo 8100, você ter esgotado todo Olá local o espaço disponível no dispositivo de saudação. Você não pode criar qualquer volume em camadas desse ponto em diante, pois não há nenhum espaço local no conjunto de trabalho de Olá Olá dispositivo toohost de saudação hierárquico de volume. Volumes em camadas existentes também afetam o espaço de saudação disponível. Por exemplo, se você tiver um dispositivo 8100 que já tem volumes em camadas de 106 TB, somente 4 TB de espaço estarão disponíveis para volumes fixados localmente.

    6. Em Olá **conectado hosts** , clique em seta hello. 

        ![Hosts conectados](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. Em Olá **conectado hosts** folha, escolha um ACR existente ou adicionar um novo ACR. Se você escolher um novo ACR, forneça um **nome** para seu ACR, forneça Olá **iSCSI Qualified Name, nome** (IQN) do seu host do Windows. Se você não tiver Olá IQN, vá muito[Get hello IQN de um host do Windows Server](#get-the-iqn-of-a-windows-server-host). Clique em **Criar**. Um volume é criado com hello especificado as configurações.

        ![Clicar em Criar](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

Novo volume agora está pronto toouse.

> [!NOTE]
> Se você cria um volume afixado localmente e, em seguida, cria outro localmente fixados volume imediatamente depois disso, os trabalhos de criação de volume Olá são executados sequencialmente. trabalho de criação de volume primeiro Olá deve concluir antes de começar o próximo trabalho de criação de volume hello.

## <a name="modify-a-volume"></a>Modificar um volume

Modificar um volume quando precisar tooexpand-lo ou alterar Olá hosts que acessam o volume de saudação.

> [!IMPORTANT]
> * Se você modificar o tamanho do volume Olá no dispositivo Olá, tamanho do volume Olá precisa toobe alterado no host de saudação também.
> * etapas do lado do host Olá descritas aqui são para o Windows Server 2012 (2012R2). Procedimentos para Linux ou para outros sistemas operacionais host serão diferentes. Consulte tooyour instruções do sistema operacional de host ao modificar o volume de saudação em um host executando outro sistema operacional.

#### <a name="toomodify-a-volume"></a>toomodify um volume

1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **dispositivos**. Na listagem tabular de saudação de dispositivos Olá, selecione o dispositivo de Olá que tem o volume de saudação que você pretende toomodify. Clique em **Configurações > Volumes**.

    ![Vá tooVolumes folha](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. De Olá tabular de lista de volumes, selecione o volume de hello e tooinvoke Olá contexto menu de atalho. Selecione **colocar offline** tootake volume de saudação modificará offline.

    ![Selecionar e colocar o volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Em Olá **colocar offline** folha, examine o impacto de saudação de colocar offline o volume de saudação e selecione Olá caixa de seleção correspondente. Verifique se o volume correspondente de saudação no host de saudação está off-line pela primeira vez. Para obter informações sobre como tootake um volume offline no servidor host conectado tooStorSimple, consulte toooperating instruções específicas do sistema. Clique em **Colocar offline**.

    ![Examinar o impacto de colocar um volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Depois que o volume de saudação estiver offline (conforme mostrado por status de saudação do volume), selecione o volume de saudação e tooinvoke Olá contexto menu de atalho. Selecione **Modificar volume**.

    ![Selecionar Modificar volume](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. Em Olá **Modificar volume** folha, você pode fazer Olá as seguintes alterações:
   
   1. Olá volume **nome** não pode ser editado.
   2. Converter Olá **tipo** de tootiered localmente afixado ou de toolocally hierárquico fixado (consulte [alterar o tipo de volume Olá](#change-the-volume-type) para obter mais informações).
   3. Aumentar Olá **capacidade provisionada**. Olá **capacidade provisionada** só pode ser aumentado. Não é possível reduzir um volume depois que ele é criado.
   4. Em **conectado hosts**, você pode modificar Olá ACR. toomodify um ACR, volume Olá deve estar offline.

       ![Examinar o impacto de colocar um volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. Clique em **salvar** toosave suas alterações. Quando solicitado a confirmar, clique em **Sim**. Olá portal do Azure exibirá uma mensagem de volume de atualização. Ele exibirá uma mensagem de êxito quando o volume de saudação foi atualizado com êxito.

    ![Examinar o impacto de colocar um volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. Se você está expandindo um volume, conclua Olá seguindo as etapas em seu computador de host do Windows:
   
   1. Vá muito**gerenciamento do computador** ->**gerenciamento de disco**.
   2. Clique com o botão direito do mouse em **Gerenciamento de Disco** e selecione **Examinar Discos Novamente**.
   3. Na lista de saudação de discos, selecione o volume Olá atualizados, com o botão direito e selecione **estender Volume**. Olá estender Volume assistente é iniciado. Clique em **Avançar**.
   4. Conclua o Assistente de saudação, aceitando os valores padrão de saudação. Concluído o Assistente de saudação, volume Olá deve mostrar Olá maior tamanho.
      
      > [!NOTE]
      > Se você expandir um volume localmente afixado e, em seguida, expanda outro localmente fixados volume logo depois, trabalhos de expansão de volume Olá são executados sequencialmente. trabalho de expansão de volume primeiro Olá deve concluir antes de começar o próximo trabalho de expansão de volume hello.
      

## <a name="change-hello-volume-type"></a>Alterar o tipo de volume Olá

Você pode alterar o tipo de volume de saudação do toolocally hierárquico fixado ou de tootiered localmente afixado. No entanto, essa conversão não deve ser uma ocorrência frequente.

### <a name="tiered-toolocal-volume-conversion-considerations"></a>Considerações sobre conversão de volume em camadas toolocal

Algumas das razões para a conversão de um volume em camadas toolocally fixado são:

* Garantias locais sobre disponibilidade e desempenho dos dados
* Eliminação de latências de nuvem e problemas de conectividade de nuvem.

Normalmente, esses são pequenos volumes existentes que você deseja tooaccess com frequência. Um volume afixado localmente é totalmente provisionado quando é criado. 

Se você estiver convertendo um volume do volume em camadas tooa fixado localmente, StorSimple verifica se você tem espaço suficiente em seu dispositivo antes de começar a conversão de saudação. Se você tiver espaço suficiente, você receberá um erro e operação hello será cancelada. 

> [!NOTE]
> Antes de começar uma conversão de em camadas toolocally fixado, certifique-se de que você considere Olá requisitos de espaço de outras cargas de trabalho. 

Conversão de um volume em camadas tooa localmente afixado pode afetar adversamente o desempenho do dispositivo. Além disso, Olá fatores a seguir pode aumentar o tempo de saudação que leva a conversão de saudação toocomplete:

* Não há largura de banda suficiente.
* Não há backup atual.

efeitos de saudação toominimize que esses fatores podem ter:

* Examine suas políticas de limitação de largura de banda e certifique-se de que uma largura de banda dedicada de 40 Mbps está disponível.
* Agende a conversão de saudação do horário de pico.
* Pegue um instantâneo antes de iniciar a conversão de saudação.

Se você estiver convertendo vários volumes (suporte a cargas de trabalho diferentes), você deve priorizar conversão do volume Olá para que os volumes de prioridade mais altos são convertidos primeiro. Por exemplo, é necessário converter os volumes que hospedam VMs (máquinas virtuais) ou volumes com cargas de trabalho do SQL antes de converter volumes com cargas de trabalho de compartilhamento de arquivos.

### <a name="local-tootiered-volume-conversion-considerations"></a>Considerações sobre conversão de volume local tootiered

Talvez você queira toochange tooa um volume localmente afixado em camadas volume se você precisar de mais espaço tooprovision outros volumes. Quando você converte Olá localmente afixado volume tootiered, Olá capacidade disponível no aumento de dispositivo Olá por tamanho de saudação da capacidade de saudação liberada. Se problemas de conectividade impedir que a conversão de saudação de um volume de saudação tipo local toohello hierárquico tipo, hello volume local exibirá propriedades de um volume em camadas até Olá conversão seja concluída. Isso ocorre porque alguns dados podem ter vazados toohello nuvem. Esses dados derramados continuam toooccupy o espaço local no dispositivo Olá que não pode ser liberado até que a operação de saudação é reiniciada e concluída.

> [!NOTE]
> Converter um volume pode levar algum tempo e não é possível cancelar uma conversão depois de iniciada. volume Olá permanecerá online durante a conversão de Olá e fazer o backup, mas você não pode expandir ou restaurar o volume de saudação enquanto conversão Olá estiver ocorrendo.


#### <a name="toochange-hello-volume-type"></a>tipo de volume Olá toochange

1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **dispositivos**. Na listagem tabular de saudação de dispositivos Olá, selecione o dispositivo de Olá que tem o volume de saudação que você pretende toomodify. Clique em **Configurações > Volumes**.

    ![Vá tooVolumes folha](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. De Olá tabular de lista de volumes, selecione o volume de hello e tooinvoke Olá contexto menu de atalho. Selecione **Modificar**.

    ![Selecionar Modificar no menu de contexto](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. Em Olá **Modificar volume** folha, altere o tipo de volume de saudação selecionando o novo tipo de saudação do hello **tipo** lista suspensa.
   
   * Se você estiver alterando o tipo de saudação muito**localmente afixado**, StorSimple irá verificar toosee se não houver capacidade suficiente.
   * Se você estiver alterando o tipo de saudação muito**em camadas** e esse volume será usado para dados de arquivamento, selecione Olá **usar este volume para dados de arquivamento acessados com frequência menos** caixa de seleção.
   * Se você estiver configurando um volume localmente afixado como em camadas ou _o contrário_, hello seguinte mensagem será exibida.
   
    ![Mensagem Alterar tipo de volume](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. Clique em **salvar** toosave alterações de saudação. Quando solicitado a confirmar, clique em **Sim** toostart processo de conversão de saudação. 

    ![Salvar e confirmar](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. Olá portal do Azure exibe uma notificação para a criação de trabalho Olá que atualizará o volume de saudação. Clique Olá notificação toomonitor Olá status do trabalho de conversão de volume hello.

    ![Trabalho de conversão de volume](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>Colocar um volume offline

Talvez seja necessário tootake um volume offline quando você estiver planejando toomodify ou excluir o volume de saudação. Quando um volume está offline, não está disponível para acesso de leitura / gravação. Você deve colocar o volume de Olá offline no host de saudação e dispositivo hello.

#### <a name="tootake-a-volume-offline"></a>tootake um volume offline

1. Certifique-se de que o volume de saudação em questão não está em uso antes de colocá-lo offline.
2. Olá primeiro coloque volume offline no host de saudação. Isso eliminará qualquer risco potencial de corrupção de dados no volume de saudação. Para etapas específicas, consulte as instruções de toohello para seu sistema operacional do host.
3. Depois de saudação host estiver offline, coloque o volume de saudação no dispositivo Olá off-line executando Olá etapas a seguir:
   
    1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **dispositivos**. Na listagem tabular de saudação de dispositivos Olá, selecione o dispositivo de Olá que tem o volume de saudação que você pretende toomodify. Clique em **Configurações > Volumes**.

        ![Vá tooVolumes folha](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. De Olá tabular de lista de volumes, selecione o volume de hello e tooinvoke Olá contexto menu de atalho. Selecione **colocar offline** tootake volume de saudação modificará offline.

        ![Selecionar e colocar o volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Em Olá **colocar offline** folha, examine o impacto de saudação de colocar offline o volume de saudação e selecione Olá caixa de seleção correspondente. Clique em **Colocar offline**. 

    ![Examinar o impacto de colocar um volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      Você será notificado quando Olá volume está offline. status do volume Olá também atualiza tooOffline.
      
4. Depois que um volume estiver offline, se você selecionar volume hello e o botão direito do mouse, **colocar Online** opção ficará disponível no menu de contexto de saudação.

> [!NOTE]
> Olá **colocar Offline** comando envia um toohello dispositivo tootake Olá volume offline. Se os hosts ainda estiverem usando o volume de hello, isso resulta em interrupções nas conexões, mas colocar offline o volume de saudação não falhará.

## <a name="delete-a-volume"></a>Excluir um volume

> [!IMPORTANT]
> Você pode excluir um volume apenas se ele estiver offline.

Concluir Olá etapas toodelete um volume a seguir.

#### <a name="toodelete-a-volume"></a>toodelete um volume

1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **dispositivos**. Na listagem tabular de saudação de dispositivos Olá, selecione o dispositivo de Olá que tem o volume de saudação que você pretende toomodify. Clique em **Configurações > Volumes**.

    ![Vá tooVolumes folha](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Verificar o status de saudação do volume Olá deseja toodelete. Se o volume de saudação que você deseja toodelete não estiver offline, primeiro coloque-o offline. Siga as etapas de saudação em [colocar um volume offline](#take-a-volume-offline).
4. Após Olá volume estiver offline, selecione o volume de saudação, tooinvoke Olá contexto menu de atalho e selecione **excluir**.

    ![Selecionar Excluir no menu de contexto](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. Em Olá **excluir** folha, revise e Olá selecione a caixa de seleção com impacto de saudação da exclusão de um volume. Quando você excluir um volume, todos os dados de saudação que reside no volume hello serão perdidos. 

    ![Salvar e confirmar as alterações](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. Depois de saudação volume for excluído, Olá tabela lista de volumes atualizações tooindicate exclusão de saudação.

    ![Lista de volumes atualizada](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > Se você excluir um volume localmente afixado, espaço para novos volumes Olá pode não ser atualizado imediatamente. Olá serviço do Gerenciador de dispositivos de StorSimple atualiza Olá local espaço periodicamente. Sugerimos que você aguarde alguns minutos antes de tentar de novo volume do toocreate hello.
   >
   > Além disso, se você excluir um volume localmente afixado e, em seguida, excluir outro localmente fixados volume logo depois, trabalhos de exclusão do volume de saudação são executados sequencialmente. trabalho de exclusão de volume primeiro Olá deve concluir antes de começar o próximo trabalho de exclusão de volume hello.

## <a name="monitor-a-volume"></a>Monitorar um volume

Monitoramento de volume permite estatísticas de toocollect relacionados de I/O para um volume. Monitoramento é habilitado por padrão para Olá primeiros 32 volumes que você criar. O monitoramento de volumes adicionais é desabilitado por padrão. 

> [!NOTE]
> O monitoramento de volumes clonados está desabilitado por padrão.


Execute Olá tooenable as etapas a seguir ou desabilitar o monitoramento para um volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable ou desabilite o monitoramento de volume

1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **dispositivos**. Na listagem tabular de saudação de dispositivos Olá, selecione o dispositivo de Olá que tem o volume de saudação que você pretende toomodify. Clique em **Configurações > Volumes**.
2. De Olá tabular de lista de volumes, selecione o volume de hello e tooinvoke Olá contexto menu de atalho. Selecione **Modificar**.
3. Em Olá **Modificar volume** folha, para **monitoramento** selecione **habilitar** ou **desabilitar** tooenable ou desabilitar o monitoramento.

    ![Desabilitar o monitoramento](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**. Olá portal do Azure exibe uma notificação para atualizar o volume hello e, em seguida, uma mensagem de êxito, depois que o volume de saudação é atualizado com êxito.

## <a name="next-steps"></a>Próximas etapas

* Saiba como muito[clonar um volume StorSimple](storsimple-8000-clone-volume-u2.md).
* Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

