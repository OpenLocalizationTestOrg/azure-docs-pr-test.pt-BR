---
title: aaaManage seus volumes StorSimple | Microsoft Docs
description: "Explica como tooadd, modificar, monitorar e excluir volumes do StorSimple e tootake-los offline, se necessário."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>Usar Olá StorSimple Manager serviço toomanage volumes
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Visão geral
Este tutorial explica como toouse Olá toocreate do serviço StorSimple Manager e gerenciar volumes no dispositivo do StorSimple hello e o dispositivo virtual StorSimple.

Olá serviço StorSimple Manager é uma extensão da saudação portal clássico do Azure que permite que você gerencie sua solução StorSimple de uma única interface da web. Em volumes de toomanaging adição, você pode usar toocreate de serviço do StorSimple Manager hello e gerenciar serviços do StorSimple, exibir e gerenciar dispositivos, exibir alertas, exibir e gerenciar políticas de backup e o catálogo de backup hello.

> [!NOTE]
> O Azure StorSimple pode criar somente volumes pequenos de provisionamento. Não é possível criar volumes parcialmente ou totalmente provisionados em um sistema do Azure StorSimple.
> 
> O provisionamento dinâmico é uma tecnologia de virtualização na qual o armazenamento disponível aparece recursos físicos tooexceed. Em vez de reservar um armazenamento suficiente antecedência, o Azure StorSimple usa tooallocate provisionamento thin suficiente requisitos de espaço atual em toomeet. a natureza elástica Olá de armazenamento em nuvem facilita essa abordagem porque StorSimple do Azure pode aumentar ou diminuir a nuvem armazenamento toomeet demandas em constante mudança.
> 
> 

## <a name="hello-volumes-page"></a>página de Volumes Olá
Olá **Volumes** página permite que você toomanage Olá os volumes de armazenamento que são provisionados no dispositivo do Microsoft Azure StorSimple Olá para os seus iniciadores (servidores). Ele exibe a lista de saudação de volumes em seu dispositivo StorSimple.

 ![Página Volumes](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

Um volume consiste em uma série de atributos:

* **Nome** – um nome descritivo que deve ser exclusivo e ajuda a identificar o volume de saudação. Esse nome também é usado em relatórios de monitoramento ao filtrar um volume específico.
* **Status** – Pode ser online ou offline. Se um volume estiver offline, não é visível tooinitiators (servidores) que têm permissão de acesso toouse Olá volume.
* **Capacidade** – Especifica como grande volume de saudação é, conforme percebido pelo iniciador da saudação (servidor). Capacidade Especifica a quantidade total de saudação de dados que podem ser armazenados pelo iniciador da saudação (servidor). Os volumes são provisionados de forma dinâmica e ocorre a eliminação de duplicação de dados. Isso implica que o dispositivo não pré-aloca a capacidade de armazenamento físico internamente ou na nuvem de saudação de acordo com a capacidade de volume tooconfigured. a capacidade de volume Olá é alocada e consumida sob demanda.
* **Tipo** – o tipo de volume Olá pode ser em camadas ou arquivamento (um subtipo de em camadas)
* **Acesso** – Especifica os iniciadores de saudação (servidores) que têm permissão de acesso toothis volume. Os iniciadores que não são membros de registro de controle de acesso (ACR) que está associado ao volume de saudação não poderão ver o volume de saudação.
* **Monitoramento** – Especifica se um volume está sendo monitorado. Um volume terá o monitoramento ativado por padrão quando ele é criado. O monitoramento será, no entanto, desabilitado para um clone de volume. tooenable monitoramento para um volume, siga as instruções de saudação no Monitor de um volume.

Olá associadas a um volume as tarefas mais comuns são:

* Adicionar um volume
* Modificar um volume
* Excluir um volume
* Colocar um volume offline
* Monitorar um volume

## <a name="add-a-volume"></a>Adicionar um volume
Você [criou um volume](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) durante a implantação da solução StorSimple. Adicionar um volume é um procedimento semelhante.

### <a name="tooadd-a-volume"></a>tooadd um volume
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** guia.
2. Selecione um contêiner de volume e clique em seta Olá Olá linha tooaccess Olá volumes correspondentes associadas ao contêiner de saudação.
3. Clique em **adicionar** final Olá Olá página. Inicia o Assistente adicionar um volume de saudação.
   
     ![Configurações básicas do assistente para Adicionar volume](./media/storsimple-manage-volumes/AddVolume1.png)
4. Em hello Assistente de adição de um volume, em **configurações básicas**, Olá a seguir:
   
   1. Digite um **Nome** para o seu volume.
   2. Especifique a saudação **capacidade provisionada** para seu volume em GB ou TB. capacidade de saudação deve estar entre 1 GB e 64 TB para um dispositivo físico. capacidade máxima de saudação que pode ser provisionada para um volume em um dispositivo virtual StorSimple é de 30 TB.
   3. Selecione Olá **tipo de uso** para seu volume. Se você estiver usando Olá volume em camadas para dados de arquivamento, selecionando Olá **usar este volume para dados de arquivamento acessados com frequência menos** caixa de seleção altera o tamanho do bloco de eliminação de duplicação de saudação para seu volume too512 KB. Se você não selecionar essa opção, o volume em camadas correspondente de saudação usará um tamanho de bloco de 64 KB. Um tamanho de bloco de eliminação de duplicação maior permite a transferência de saudação do hello dispositivo tooexpedite da nuvem de toohello grandes de dados de arquivamento. (Volumes em camadas foram chamados anteriormente volumes principais.)
   4. Clique no ícone de seta Olá ![ícone de seta](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **configurações adicionais** página.
      
        ![Configurações adicionais do assistente para Adicionar volume](./media/storsimple-manage-volumes/AddVolume2.png)
5. Em **Configurações Adicionais**, adicione um novo registro de controle de acesso (ACR):
   
   1. Selecione um registro de controle de acesso (ACR) na lista suspensa de saudação. Como opção, você também pode abrir um novo ACR. ACRs determinam quais hosts podem acessar seus volumes por correspondência Olá IQN de host com o listado no registro de saudação.
   2. Recomendamos que você habilite um backup padrão selecionando Olá **habilitar um backup padrão para este volume** caixa de seleção.
   3. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-volumes/HCS_CheckIcon.png) volume de saudação toocreate com hello especificado as configurações.

Novo volume agora está pronto toouse.

## <a name="modify-a-volume"></a>Modificar um volume
Modificar um volume quando precisar tooexpand-lo ou alterar Olá hosts que acessam o volume de saudação.

> [!IMPORTANT]
> * Se você modificar o tamanho do volume Olá no dispositivo Olá, tamanho do volume Olá precisa toobe alterado no host de saudação também.
> * etapas do lado do host Olá descritas aqui são para o Windows Server 2012 (2012R2). Procedimentos para Linux ou para outros sistemas operacionais host serão diferentes. Consulte tooyour instruções do sistema operacional de host ao modificar o volume de saudação em um host executando outro sistema operacional.
> 
> 

### <a name="toomodify-a-volume"></a>toomodify um volume
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêiner de Volume** guia. Esta página lista em um formato tabular, todos os contêineres de volume Olá que estão associados ao dispositivo hello.
2. Selecione um contêiner de volume e clique em lista de saudação toodisplay de todos os volumes Olá Olá contêiner.
3. Em Olá **Volumes** , selecione um volume e clique em **modificar**.
4. Em Olá Assistente para modificar volume, em **configurações básicas**, você pode fazer a seguir hello:
   
   * Editar saudação **nome** e **tipo** se desejar toomodify um volume de arquivamento de tooan de volume em camadas selecionando Olá **usar este volume para dados de arquivamento acessados com frequência menos** tamanho da caixa de seleção toochange Olá eliminação de duplicação parte para seu volume too512 KB.
   * Aumentar Olá **capacidade provisionada**. Olá **capacidade provisionada** só pode ser aumentado. Não é possível reduzir um volume depois que ele é criado.
     
     > [!NOTE]
     > Você não pode alterar o contêiner de volume Olá depois que ele é atribuído um volume tooa.
     > 
     > 
5. Em **configurações adicionais**, você pode fazer a seguir hello:
   
   * Modificar ACRs hello, desde que o volume de saudação está offline. Se o volume de saudação estiver online, você precisará tootake-lo primeiro offline. Consulte as etapas toohello [colocar um volume offline](#take-a-volume-offline) toomodifying anterior Olá ACR.
   * Modifique a lista de saudação de ACRs depois Olá volume estiver offline.
     
     > [!NOTE]
     > Não é possível alterar Olá **habilitar um backup padrão para este volume** opção para o volume de saudação.
     > 
     > 
6. Salvar as alterações clicando o ícone de verificação de saudação ![check-icon](./media/storsimple-manage-volumes/HCS_CheckIcon.png). Olá portal clássico do Azure exibirá uma mensagem de volume de atualização. Ele exibirá uma mensagem de êxito quando o volume de saudação foi atualizado com êxito.
7. Se você está expandindo um volume, conclua Olá seguindo as etapas em seu computador de host do Windows:
   
   1. Vá muito**gerenciamento do computador** ->**gerenciamento de disco**.
   2. Clique com o botão direito do mouse em **Gerenciamento de Disco** e selecione **Examinar Discos Novamente**.
   3. Na lista de saudação de discos, selecione o volume Olá atualizados, com o botão direito e selecione **estender Volume**. Olá estender Volume assistente é iniciado. Clique em **Avançar**.
   4. Conclua o Assistente de saudação, aceitando os valores padrão de saudação. Concluído o Assistente de saudação, volume Olá deve mostrar Olá maior tamanho.

![Vídeo disponível](./media/storsimple-manage-volumes/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como tooexpand um volume, clique em [aqui](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="take-a-volume-offline"></a>Colocar um volume offline
Talvez seja necessário tootake um volume offline quando você estiver planejando toomodify-lo ou exclua-lo. Quando um volume está offline, não está disponível para acesso de leitura / gravação. Você precisará tootake Olá volume offline no host hello, bem como no dispositivo de saudação. Execute Olá seguindo as etapas tootake um volume offline.

### <a name="tootake-a-volume-offline"></a>tootake um volume offline
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

### <a name="toodelete-a-volume"></a>toodelete um volume
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** guia.
2. Selecione o contêiner de volume de saudação que tem o volume a saudação ser toodelete. Clique em Olá Olá de tooaccess de contêiner de volume **Volumes** página.
3. Todos os volumes de saudação associados a este contêiner são exibidos em um formato tabular. Verificar o status de saudação do volume Olá deseja toodelete. Se o volume Olá toodelete desejado não estiver offline, etapas-lo offline Olá primeiro, o seguinte [colocar um volume offline](#take-a-volume-offline).
4. Depois de saudação volume estiver offline, clique em **excluir** final Olá Olá página.
5. Quando solicitado a confirmar, clique em **Sim**. volume de saudação será excluída e Olá **Volumes** página mostrará a lista de saudação atualizada de volumes no contêiner de saudação.

## <a name="monitor-a-volume"></a>Monitorar um volume
Monitoramento de volume permite estatísticas de toocollect relacionados de I/O para um volume. Monitoramento é habilitado por padrão para Olá primeiros 32 volumes que você criar. O monitoramento de volumes adicionais é desabilitado por padrão. Monitoramento de volumes clonados também será desabilitado por padrão.

Execute Olá tooenable as etapas a seguir ou desabilitar o monitoramento para um volume.

### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable ou desabilite o monitoramento de volume
1. Em Olá **dispositivos** página, selecione o dispositivo hello, clique duas vezes nele e, em seguida, clique em Olá **contêineres de Volume** guia.
2. Selecione Olá contêiner de volume no qual Olá volume reside e clique em Olá Olá de tooaccess de contêiner de volume **Volumes** página.
3. Todos os volumes de saudação associados a este contêiner são listados na exibição tabular hello. Clique e selecione o volume de saudação ou clone de volume.
4. Final Olá Olá página, clique em **modificar**.
5. No Assistente para modificar Volume de hello, em **configurações básicas**, selecione **habilitar** ou **desabilitar** de saudação **monitoramento** lista suspensa.
   
    ![Modificar as Configurações Básicas de um volume](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[clonar um volume StorSimple](storsimple-clone-volume.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

