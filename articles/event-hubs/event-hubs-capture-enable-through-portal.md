---
title: Habilitar a Captura de Hubs de Eventos do Azure por meio do portal | Microsoft Docs
description: Habilite o recurso Captura de Hubs de Eventos usando o portal do Azure.
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a>Habilitar a Captura de Hubs de Evento usando o portal do Azure

Você pode configurar Captura na hora da criação do hub de eventos usando o [portal do Azure](https://portal.azure.com). Ou pode capturar os dados em um contêiner do [Armazenamento de Blobs](https://azure.microsoft.com/services/storage/blobs/) do Azure ou em uma conta do [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

## <a name="capture-data-to-an-azure-storage-account"></a>Capturar dados em uma conta do Armazenamento do Azure  

Quando você cria um hub de eventos, você pode habilitar a captura clicando o **em** no botão de **criar Hub de eventos** folha portal. Em seguida, especifique uma Conta de Armazenamento e um contêiner clicando em **Armazenamento do Azure** na caixa **Provedor da Captura**. Já que a Captura dos Hubs de Eventos usa a autenticação de serviços com o armazenamento, você não precisa especificar uma cadeia de conexão de armazenamento. O seletor de recurso seleciona automaticamente o URI do recurso para sua conta de armazenamento. Se você usar o Azure Resource Manager, deverá fornecer esse URI explicitamente como uma cadeia de caracteres.

A janela de tempo padrão é de 5 minutos. O valor mínimo é 1, o máximo é 15. A janela **Tamanho** tem um intervalo de 10 a 500 MB.

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a>Capturar dados em uma conta do Azure Data Lake Store

Para capturar dados em um Azure Data Lake Store, você pode criar uma conta do Data Lake Store e um hub de eventos:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Criar uma conta e pastas do Azure Data Lake Store

1. Crie uma conta do Data Lake Store seguindo as instruções em [Introdução ao Azure Data Lake Store usando o portal do Azure](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Crie uma pasta nessa conta seguindo as instruções na seção [Criar pastas na conta do Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).
3. Na folha de conta do repositório Data Lake, clique em **Data Explorer**.
4. Clique em **Acessar**.
5. Clique em **Adicionar**.
6. Na caixa **Pesquisar por nome ou email**, digite **Microsoft.EventHubs** e selecione essa opção. 
7. A guia **Permissões** aparecerá. Defina as permissões conforme mostrado na figura abaixo:

    ![][6]

8. Clique em **OK**.
9. Agora, crie uma pasta na pasta raiz navegando até a pasta de destino e clicando em seu nome.
10. Clique em **Acessar**.
11. Clique em **Adicionar**.
12. Na caixa **Pesquisar por nome ou email**, digite **Microsoft.EventHubs** e selecione essa opção.
13. A guia **Permissões** é exibida novamente. Defina as permissões conforme mostrado na figura abaixo:

    ![][5]

### <a name="create-an-event-hub"></a>Criar um Hub de Evento

1. Observe que o hub de eventos deve estar na mesma assinatura do Azure que o Azure Data Lake Store recém-criado. Criar o hub de eventos, clicando no **na** botão em **capturar** no **criar Hub de eventos** portal folha. 
2. No **criar Hub de eventos** portal folha, selecione **repositório Azure Data Lake** do **provedor capturar** caixa.
3. Em **Azure Data Lake Store**, especifique a conta do Data Lake Store criada anteriormente e, no campo **Caminho do Data Lake**, digite o caminho para a pasta de dados criada.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Adicionar ou configurar a Captura em um hub de eventos existente

Você pode configurar a Captura em hubs de eventos existentes que estejam em namespaces dos Hubs de Eventos. Para habilitar a Captura em um hub de eventos existente ou alterar as configurações da Captura, clique no namespace para carregar a folha **Essentials** e clique no Hub de Eventos para o qual você deseja habilitar ou alterar a configuração da Captura. Por fim, clique no **propriedades** seção da folha de abrir e editar as configurações de captura, conforme as figuras a seguir:

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
