---
title: volumes aaaManage na matriz Virtual StorSimple | Microsoft Docs
description: "Descreve Olá Gerenciador de dispositivos do StorSimple e explica como toouse-toomanage volumes no StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>Toomanage volumes serviço Gerenciador de dispositivos de StorSimple uso Olá matriz Virtual StorSimple

## <a name="overview"></a>Visão geral

Este tutorial explica como toouse Olá toocreate de serviço do Gerenciador de dispositivos do StorSimple e gerenciar volumes no StorSimple Virtual Array.

saudação de serviço do Gerenciador de dispositivos do StorSimple é uma extensão em Olá portal do Azure que permite que você gerencie sua solução StorSimple de uma única interface da web. Em adição toomanaging compartilhamentos e volumes, você pode usar tooview de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar dispositivos, exibir alertas, exibir e gerenciar políticas de backup e o catálogo de backup hello.

## <a name="volume-types"></a>Tipos de volumes

Os volumes do StorSimple podem ser:

* **Localmente afixado**: dados nesses volumes permanece na matriz de saudação sempre e não despejar toohello nuvem.
* **Em camadas**: dados nesses volumes podem despejar toohello nuvem. Quando você cria um volume em camadas, aproximadamente 10% do espaço de saudação é provisionado na camada local hello e 90% do espaço de saudação é provisionado na nuvem hello. Por exemplo, se você provisionar um volume de 1 TB, 100 GB reside no espaço local hello e 900 GB é usado na nuvem hello quando Olá camadas de dados. Por sua vez, isso significa que se você ficar sem todo o espaço local Olá no dispositivo hello, você não pode provisionar um volume em camadas (porque Olá 10% necessário no local de saudação camada não estará disponível).

### <a name="provisioned-capacity"></a>Capacidade provisionada
Consulte toohello para máxima capacidade provisionada para cada tipo de volume a tabela a seguir.

| **Identificador de limite**                                       | **Limite**     |
|------------------------------------------------------------|---------------|
| Tamanho mínimo de um volume em camadas                            | 500 GB        |
| Tamanho máximo de um volume em camadas                            | 5 TB          |
| Tamanho mínimo de um volume fixado localmente                    | 50 GB         |
| Tamanho máximo de um volume fixado localmente                    | 500 GB        |

## <a name="hello-volumes-blade"></a>folha de Volumes Olá
Olá **Volumes** menu na sua folha de resumo de serviço do StorSimple exibe a lista de saudação de volumes de armazenamento em uma determinada matriz de StorSimple e permite que você toomanage-los.

![Folha Volumes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

Um volume consiste em uma série de atributos:

* **Nome do volume** – um nome descritivo que deve ser exclusivo e ajuda a identificar o volume de saudação.
* **Status** – Pode ser online ou offline. Se o volume estiver offline, não é visível tooinitiators (servidores) que têm permissão de acesso toouse Olá volume.
* **Tipo** – indica se o volume de saudação é **em camadas** (Olá padrão) ou **localmente afixado**.
* **Capacidade** – Especifica Olá quantidade de dados usados como toohello em comparação com a quantidade total de dados que podem ser armazenados pelo iniciador da saudação (servidor).
* **Backup** – no caso de Olá matriz Virtual StorSimple, todos os volumes são habilitados automaticamente para o backup.
* **Conectado hosts** – Especifica os iniciadores de saudação (servidores) que têm permissão de acesso toothis volume.

![Detalhes dos volumes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

Use as instruções de saudação este Olá tooperform tutorial tarefas a seguir:

* Adicionar um volume
* Modificar um volume
* Colocar um volume offline
* Excluir um volume

## <a name="add-a-volume"></a>Adicionar um volume

1. Na folha resumida do serviço do StorSimple de saudação, clique em **+ Adicionar volume** na barra de comandos de saudação. Isso abre a saudação **Adicionar volume** folha.
   
    ![Adicionar volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. Em Olá **Adicionar volume** folha, Olá a seguir:
   
   * Em Olá **nome do Volume** campo, digite um nome exclusivo para seu volume. nome da saudação deve ser uma cadeia de caracteres com 3 caracteres too127.
   * Em Olá **tipo** suspensa lista, especifique se toocreate um **em camadas** ou **localmente afixado** volume. Para as cargas de trabalho que exigem garantias locais, latências baixas e um melhor desempenho, selecione **Volume fixado localmente**. Para todos os outros dados, selecione volume **Em camadas**.
   * Em Olá **capacidade** , especifique o tamanho de saudação do volume de saudação. Um volume em camadas deve ter entre 500 GB e 5 TB e um volume fixado localmente deve ter entre 50 GB e 500 GB.
   * * Clique em **conectado hosts**, selecione um acesso controle ACR (registro) correspondente toohello iniciador iSCSI que você deseja tooconnect toothis volume e, em seguida, clique em **selecione**.
3. tooadd um novo host conectado, clique em **adicionar novo**, insira um nome de host de saudação e o iSCSI IQN (nome qualificado) e depois clique em **adicionar**.
   
    ![Adicionar volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. Quando você tiver terminado de configurar o volume, clique em **Criar**. Um volume será criado com hello especificado as configurações e você verá uma notificação de êxito na criação de Olá Olá mesmo. Por padrão, backup será habilitado para o volume de saudação.
5. tooconfirm que Olá volume foi criado com êxito, vá toohello **Volumes** folha. Você deve ver o volume de saudação listado.
   
    ![Criação do volume bem-sucedida](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>Modificar um volume

Modifique um volume quando você precisa toochange Olá hosts que acessam o volume de saudação. Olá outros atributos de um volume não podem ser modificados após a criação de volume hello.

#### <a name="toomodify-a-volume"></a>toomodify um volume

1. De saudação **Volumes** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá volume desejar toomodify reside.
2. **Selecione** Olá volume e clique em **conectado hosts** tooview Olá host conectado no momento e modificá-lo tooa outro servidor.
   
    ![Editar volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. Salvar as alterações clicando Olá **salvar** barra de comandos. As configurações especificadas serão aplicadas e você verá uma notificação.

## <a name="take-a-volume-offline"></a>Colocar um volume offline

Talvez seja necessário tootake um volume offline quando você estiver planejando toomodify-lo ou exclua-lo. Quando um volume está offline, não está disponível para acesso de leitura / gravação. Você precisará tootake Olá volume offline no host hello, bem como no dispositivo de saudação.

#### <a name="tootake-a-volume-offline"></a>tootake um volume offline

1. Certifique-se de que o volume de saudação em questão não está em uso antes de colocá-lo offline.
2. Olá primeiro coloque volume offline no host de saudação. Isso eliminará qualquer risco potencial de corrupção de dados no volume de saudação. Para etapas específicas, consulte as instruções de toohello para seu sistema operacional do host.
3. Depois de volume Olá Olá host estiver offline, coloque o volume de saudação na matriz de saudação offline executando Olá etapas a seguir:
   
   * De saudação **Volumes** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá volume desejar tootake offline reside.
   * **Selecione** Olá volume e clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **colocar offline**.
     
        ![Volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * Revise as informações de Olá Olá **colocar offline** folha e confirmar a aceitação da operação de saudação. Clique em **colocar offline** tootake volume de saudação offline. Você verá uma notificação de operação de saudação em andamento.
   * tooconfirm volume Olá com êxito foi colocado offline, vá toohello **Volumes** folha. Você deve ver o status de saudação do volume de saudação como offline.
     
       ![Confirmação de volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>Excluir um volume

> [!IMPORTANT]
> Você pode excluir um volume apenas se ele estiver offline.
> 
> 

Concluir Olá etapas toodelete um volume a seguir.

#### <a name="toodelete-a-volume"></a>toodelete um volume

1. De saudação **Volumes** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá volume desejar toodelete reside.
2. **Selecione** Olá volume e clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **excluir**.
   
    ![Excluir volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. Verificar o status de saudação do volume Olá deseja toodelete. Se o volume Olá toodelete desejado não estiver offline, etapas-lo offline Olá primeiro, o seguinte [colocar um volume offline](#take-a-volume-offline).
4. Quando for solicitada a confirmação no hello **excluir** folha, aceite a confirmação de saudação e clique em **excluir**. volume de saudação será excluída e Olá **Volumes** folha mostrará a lista de saudação atualizada de volumes em matriz virtual hello.

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[clonar um volume StorSimple](storsimple-virtual-array-clone.md).

