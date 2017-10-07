---
title: compartilhamentos de matriz Virtual StorSimple aaaManage | Microsoft Docs
description: "Descreve Olá Gerenciador de dispositivos do StorSimple e explica como toouse-toomanage compartilhamentos no StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a>Usar compartilhamentos de toomanage de serviço de Gerenciador de dispositivos de StorSimple Olá em Olá matriz Virtual StorSimple

## <a name="overview"></a>Visão geral

Este tutorial explica como toouse Olá toocreate de serviço do Gerenciador de dispositivos do StorSimple e gerenciar os compartilhamentos no StorSimple Virtual Array.

saudação de serviço do Gerenciador de dispositivos do StorSimple é uma extensão em Olá portal do Azure que permite que você gerencie sua solução StorSimple de uma única interface da web. Em adição toomanaging compartilhamentos e volumes, você pode usar tooview de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar dispositivos, exibir alertas, gerenciar políticas de backup e gerenciar o catálogo de backup hello.

## <a name="share-types"></a>Tipos de compartilhamento

Os compartilhamentos do StorSimple podem ser:

* **Localmente afixado**: dados nesses compartilhamentos permanece na matriz de saudação sempre e não despejar toohello nuvem.
* **Em camadas**: dados nesses compartilhamentos podem despejar toohello nuvem. Quando você cria um compartilhamento em camadas, aproximadamente 10% do espaço de saudação é provisionado na camada local hello e 90% do espaço de saudação é provisionado na nuvem hello. Por exemplo, se você provisionou um compartilhamento de 1 TB, 100 GB reside no espaço local hello e 900 GB é usado na nuvem hello quando Olá camadas de dados. Por sua vez, isso significa que se você ficar sem todo o espaço local Olá no dispositivo hello, você não pode provisionar um compartilhamento em camadas (porque Olá 10% necessário no local de saudação camada não estará disponível).

### <a name="provisioned-capacity"></a>Capacidade provisionada

Consulte toohello para máxima capacidade provisionada para cada tipo de compartilhamento a tabela a seguir.

| **Identificador de limite** | **Limite** |
| --- | --- |
| Tamanho mínimo de um compartilhamento em camadas |500 GB |
| Tamanho máximo de um compartilhamento em camadas |20 TB |
| Tamanho mínimo de um compartilhamento fixado localmente |50 GB |
| Tamanho máximo de um compartilhamento fixado localmente |2 TB |

## <a name="hello-shares-blade"></a>folha de compartilhamentos Olá

Olá **compartilhamentos** menu na sua folha de resumo de serviço do StorSimple exibe a lista de saudação de compartilhamentos de armazenamento em uma determinada matriz de StorSimple e permite que você toomanage-los.

![Folha Compartilhamentos](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

Um compartilhamento consiste em uma série de atributos:

* **Nome do compartilhamento** – um nome descritivo que deve ser exclusivo e ajuda a identificar o compartilhamento de saudação.
* **Status** – Pode ser online ou offline. Se um compartilhamento estiver offline, os usuários de compartilhamento de saudação não será capaz de tooaccess-lo.
* **Tipo** – indica se o compartilhamento de saudação é **em camadas** (Olá padrão) ou **localmente afixado**.
* **Capacidade** – Especifica Olá quantidade de dados usados como toohello em comparação com a quantidade total de dados que podem ser armazenados no compartilhamento de saudação.
* **Descrição** – uma configuração opcional que ajudam a descrever compartilhamento hello.
* **Permissões** -compartilhamento toohello de permissões de NTFS de saudação que pode ser gerenciado pelo Windows Explorer.
* **Backup** – no caso de Olá matriz Virtual StorSimple, todos os compartilhamentos são habilitados automaticamente para o backup.

![Detalhes de compartilhamentos](./media/storsimple-virtual-array-manage-shares/share-details.png)

Use as instruções de saudação este Olá tooperform tutorial tarefas a seguir:

* Adicionar um compartilhamento
* Modificar um compartilhamento
* Colocar um compartilhamento offline
* Excluir um compartilhamento

## <a name="add-a-share"></a>Adicionar um compartilhamento

1. Na folha resumida do serviço do StorSimple de saudação, clique em **+ Adicionar compartilhamento** na barra de comandos de saudação. Isso abre a saudação **Adicionar compartilhamento** folha.

    ![Adicionar compartilhamento](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. Em Olá **Adicionar compartilhamento** folha, Olá a seguir:
   
    1. Em Olá **nome de compartilhamento** campo, digite um nome exclusivo para o compartilhamento. nome da saudação deve ser uma cadeia de caracteres com 3 caracteres too127.

    2. Um recurso opcional **descrição** para compartilhamento de saudação. Descrição de saudação ajudará a identificar os proprietários do compartilhamento hello.

    3. Em Olá **tipo** suspensa lista, especifique se toocreate um **em camadas** ou **localmente afixado** compartilhar. Para cargas de trabalho que exigem garantias locais, latências menores e um melhor desempenho, selecione um compartilhamento **Fixado localmente** . Para todos os outros dados, selecione compartilhamento **Em camadas** .

    4. Em Olá **capacidade** , especifique o tamanho de saudação do compartilhamento de saudação do. Um compartilhamento em camadas deve ter entre 500 GB e 20 TB e um compartilhamento fixo local deve ter entre 50 GB e 2 GB.

    5. Em Olá **definir padrão permissões completas** campo, atribua Olá permissões toohello do usuário ou grupo Olá que acessa esse compartilhamento. Especificar nome de saudação do Olá Olá de usuário ou grupo no  _john@contoso.com_  formato. É recomendável que você use um tooaccess de privilégios de administrador do usuário grupo (em vez de um único usuário) tooallow esses compartilhamentos. Depois que você atribuiu permissões de saudação aqui, você pode usar Explorador de arquivos toomodify essas permissões.
3. Quando você tiver terminado de configurar o compartilhamento, clique em **Criar**. Será criado um compartilhamento com hello especificado as configurações e você verá uma notificação. Por padrão, o backup será habilitado para compartilhamento de saudação.
4. tooconfirm que Olá compartilhamento foi criado com êxito, vá toohello **compartilhamentos** folha. Você deve ver Olá compartilhar listados.
   
    ![Criação do compartilhamento bem-sucedida](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a>Modificar um compartilhamento

Modificar um compartilhamento quando precisar de descrição de saudação do toochange do compartilhamento de saudação. Outras propriedades de compartilhamento não podem ser modificadas após a criação do compartilhamento de saudação.

#### <a name="toomodify-a-share"></a>toomodify um compartilhamento

1. De saudação **compartilhamentos** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá compartilhamento desejar toomodify reside.
2. **Selecione** Olá descrição do compartilhamento tooview Olá atual e modificá-lo.
3. Salvar as alterações clicando Olá **salvar** barra de comandos. As configurações especificadas serão aplicadas e você verá uma notificação.
   
    ![ Editar compartilhamento](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a>Colocar um compartilhamento offline

Talvez seja necessário tootake um compartilhamento offline quando você estiver planejando toomodify-lo ou exclua-lo. Quando um compartilhamento está offline, não fica disponível para acesso de leitura e gravação. Você precisará tootake Olá compartilhamento offline no host hello, bem como no dispositivo de saudação.

#### <a name="tootake-a-share-offline"></a>tootake um compartilhamento offline

1. Certifique-se de que compartilham Olá em questão não está em uso antes de colocá-lo offline.
2. Assumir Olá compartilhamento matriz de saudação offline executando Olá etapas a seguir:
   
    1. De saudação **compartilhamentos** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá reside compartilhamento desejar tootake off-line.

    2. **Selecione** compartilhamento hello e clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **colocar offline**.
     
        ![Compartilhamento offline](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. Revise as informações de Olá Olá **colocar offline** folha e confirmar a aceitação da operação de saudação. Clique em **colocar offline** tootake compartilhamento de saudação offline. Você verá uma notificação de operação de saudação em andamento.

    4. tooconfirm que Olá compartilhamento foi realizado com êxito toohello off-line, vá **compartilhamentos** folha. Você deve ver o status de saudação do compartilhamento de saudação como off-line.

## <a name="delete-a-share"></a>Excluir um compartilhamento

> [!IMPORTANT]
> Você somente pode excluir um compartilhamento se ele está offline.


Olá concluir etapas toodelete um compartilhamento a seguir.

#### <a name="toodelete-a-share"></a>toodelete um compartilhamento

1. De saudação **compartilhamentos** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual compartilhamento Olá desejar toodelete reside.
2. **Selecione** compartilhamento hello e clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **excluir**.
   
    ![Excluir compartilhamento](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. Verificar o status de saudação do compartilhamento Olá deseja toodelete. Se você deseja toodelete de compartilhamento de saudação não estiver offline, primeiro coloque-o offline. Siga as etapas de saudação em [colocar um compartilhamento offline](#take-a-share-offline).
4. Quando for solicitada a confirmação no hello **excluir** folha, aceite a confirmação de saudação e clique em **excluir**. compartilhamento de saudação será excluída e Olá **compartilhamentos** folha mostra a lista de saudação atualizada de compartilhamentos em matriz virtual hello.

## <a name="next-steps"></a>Próximas etapas
Saiba como muito[clonar um compartilhamento de StorSimple](storsimple-virtual-array-clone.md).

