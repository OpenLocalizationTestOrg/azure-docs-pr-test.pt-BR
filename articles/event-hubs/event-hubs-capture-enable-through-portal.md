---
title: Habilitar aaaAzure capturar de Hubs de eventos por meio do portal | Microsoft Docs
description: "Habilite o recurso de captura de Hubs de evento de saudação usando Olá portal do Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>Habilitar a captura de Hubs de evento usando Olá portal do Azure

Você pode configurar a captura no momento da criação Olá evento hub usando Olá [portal do Azure](https://portal.azure.com). Pode qualquer tooan de dados captura hello Azure [armazenamento de Blob](https://azure.microsoft.com/services/storage/blobs/) contêiner ou tooan [repositório Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) conta.

## <a name="capture-data-tooan-azure-storage-account"></a>Capturar conta de armazenamento do Azure tooan dados  

Quando você cria um hub de eventos, você pode habilitar a captura clicando Olá **na** botão Olá **criar Hub de eventos** portal folha. Em seguida, especifique uma conta de armazenamento e contêiner clicando **armazenamento do Azure** em Olá **provedor capturar** caixa. Como capturar de Hubs de evento usa a autenticação de serviço a serviço com o armazenamento, não é necessário toospecify uma cadeia de caracteres de conexão de armazenamento. Selecionador de recurso Olá seleciona automaticamente o URI do recurso Olá para sua conta de armazenamento. Se você usar o Azure Resource Manager, deverá fornecer esse URI explicitamente como uma cadeia de caracteres.

janela de tempo saudação padrão é 5 minutos. valor mínimo de saudação é 1, Olá máximo 15. Olá **tamanho** janela tem um intervalo de 10 a 500 MB.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>Capturar conta de repositório Azure Data Lake tooan dados

toocapture dados tooAzure repositório Data Lake, crie uma conta do repositório Data Lake e um hub de eventos:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Criar uma conta e pastas do Azure Data Lake Store

1. Criar uma conta do repositório Data Lake, seguindo as instruções de saudação do [Introdução ao repositório Azure Data Lake usando Olá portal do Azure](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Criar uma pasta sob esta conta, seguindo as instruções de Olá Olá [criar pastas na conta do repositório Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) seção.
3. Na folha de conta do repositório Data Lake hello, clique em **Data Explorer**.
4. Clique em **Acessar**.
5. Clique em **Adicionar**.
6. Em Olá **pesquisar por nome ou email** caixa tipo **Microsoft.EventHubs** e, em seguida, selecione essa opção. 
7. Olá **permissões** guia é exibida. Definir permissões de hello, conforme mostrado na figura a seguir de saudação:

    ![][6]

8. Clique em **OK**.
9. Agora, crie uma pasta na pasta raiz de saudação toohello pasta de destino de navegação e clicando no nome da pasta Olá.
10. Clique em **Acessar**.
11. Clique em **Adicionar**.
12. Em Olá **pesquisar por nome ou email** caixa tipo **Microsoft.EventHubs** e, em seguida, selecione essa opção.
13. Olá **permissões** guia é exibida novamente. Definir permissões de hello, conforme mostrado na figura a seguir de saudação:

    ![][5]

### <a name="create-an-event-hub"></a>Criar um Hub de Evento

1. Observe a esse hub de eventos Olá deve estar no hello mesma assinatura do Azure como Olá repositório Azure Data Lake você acabou de criar. Criar hub de eventos de hello, clicando em Olá **na** botão em **capturar** em Olá **criar Hub de eventos** portal folha. 
2. Em Olá **criar Hub de eventos** portal folha, selecione **repositório Azure Data Lake** de saudação **provedor capturar** caixa.
3. Em **selecione repositório do Data Lake**, especifique Olá conta do repositório Data Lake criado anteriormente e Olá **Data Lake caminho** campo, digite a pasta de dados Olá caminho toohello criado por você.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Adicionar ou configurar a Captura em um hub de eventos existente

Você pode configurar a Captura em hubs de eventos existentes que estejam em namespaces dos Hubs de Eventos. tooenable captura em um hub de eventos existente ou toochange as configurações de captura, clique em saudação do hello namespace tooload **Essentials** folha, em seguida, clique em hub de eventos Olá para o qual você deseja tooenable ou alterar a configuração de captura de saudação. Por fim, clique em Olá **propriedades** seção Olá abrir folha e, em seguida, edite as configurações de captura hello, conforme mostrado no hello figuras a seguir:

### <a name="azure-blob-storage"></a>Armazenamento do Blobs do Azure

![][2]

### <a name="azure-data-lake-store"></a>Repositório Azure Data Lake

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>Próximas etapas

Você também pode configurar a Captura dos Hubs de Eventos usando modelos do Azure Resource Manager. Para saber mais, confira [Habilitar Captura usando um modelo do Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).
