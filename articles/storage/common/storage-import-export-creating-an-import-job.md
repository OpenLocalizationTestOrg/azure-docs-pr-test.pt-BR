---
title: "aaaCreate um trabalho de importação para importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toocreate uma importação para Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Criar um trabalho de importação para Olá serviço de importação/exportação do Azure

Criar um trabalho de importação para o serviço de importação/exportação do Microsoft Azure hello usando Olá API REST envolve Olá etapas a seguir:

-   Preparando unidades com Olá, ferramenta de importação/exportação do Azure.

-   Obter Olá local toowhich tooship Olá unidade.

-   Criar trabalho de importação de saudação.

-   Saudação de envio unidades tooMicrosoft através de um serviço de transporte com suporte.

-   Atualizar o trabalho de importação de saudação com hello detalhes de envio.

 Consulte [usando Olá importação/exportação do Microsoft Azure serviço tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para obter uma visão geral do serviço de importação/exportação do hello e um tutorial que demonstra como Olá toouse [portal do Azure](https://portal.azure.com/) toocreate gerenciar importar e exportar trabalhos.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Preparando unidades com Olá, ferramenta de importação/exportação do Azure

Olá etapas tooprepare unidades para um trabalho de importação são Olá mesmo se você criar hello portal de saudação jobvia ou via Olá API REST.

Abaixo apresentamos uma breve visão geral da preparação de unidades. Consulte toohello [Azure importação ExportTool referência](storage-import-export-tool-how-to-v1.md) para obter instruções completas. Você pode baixar Olá, ferramenta de importação/exportação do Azure [aqui](http://go.microsoft.com/fwlink/?LinkID=301900).

Para preparar a unidade:

-   Identificando Olá toobe de dados importado.

-   Identificando os blobs de destino de saudação no armazenamento do Windows Azure.

-   Usando Olá ferramenta de importação/exportação do Azure toocopy tooone seus dados ou mais discos rígidos.

 Olá, ferramenta de importação/exportação do Azure também irá gerar um arquivo de manifesto para cada uma das unidades de saudação assim que for preparada. Um arquivo de manifesto contém:

-   Uma enumeração de todos os arquivos de saudação destinados para carregamento e mapeamentos de saudação do tooblobs arquivos.

-   Somas de verificação dos segmentos de saudação de cada arquivo.

-   Informações sobre tooassociate de metadados e propriedades de saudação com cada blob.

-   Uma listagem de saudação ação tootake se um blob que está sendo carregado tem Olá mesmo nome como um blob existente no contêiner de saudação. Opções possíveis são: a) substituir o blob de saudação pelo arquivo hello, b) manter o blob existente hello e ignorar o carregamento de arquivo hello, c) acrescentar um nome de sufixo toohello para que ele não está em conflito com outros arquivos.

## <a name="obtaining-your-shipping-location"></a>Obtendo o local de envio

Antes de criar um trabalho de importação, você precisa tooobtain um nome de local de envio e o endereço por chamada hello [listar locais](/rest/api/storageimportexport/listlocations) operação. `List Locations` retorna uma lista de locais e seus endereços de correspondência. Você pode selecionar um local da saudação retornada lista e seu endereço de toothat de unidades de disco rígido de destino. Você também pode usar o hello `Get Location` Olá tooobtain de operação envio diretamente o endereço para um local específico.

 Siga as próximas etapas, Olá local de envio de saudação do tooobtain:

-   Identificar o nome de saudação do local de saudação de sua conta de armazenamento. Esse valor pode ser encontrado em Olá **local** campo da conta de armazenamento Olá **painel** no portal do Azure ou consultado por meio de operação da API de gerenciamento de serviços de saudação do hello [obter armazenamento Propriedades de conta](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Recuperar o local Olá tooprocess disponível esta conta de armazenamento por chamada hello `Get Location` operação.

-   Se hello `AlternateLocations` propriedade de local de saudação contém o local de saudação em si, então é toouse okey neste local. Caso contrário, chamar hello `Get Location` operação novamente com um dos locais alternativos de saudação. local original Olá pode estar fechada temporariamente para manutenção.

## <a name="creating-hello-import-job"></a>Criar trabalho de importação de saudação
trabalho de importação toocreate hello, chamada hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação. Você precisará Olá tooprovide informações a seguir:

-   Um nome para o trabalho de saudação.

-   nome de conta de armazenamento Hello.

-   saudação de envio de nome local, obtida na etapa anterior hello.

-   Um tipo de trabalho (importação).

-   endereço de devolução Olá onde Olá unidades devem ser enviadas após a conclusão do trabalho de importação de saudação.

-   lista de saudação de unidades de trabalho de saudação. Para cada unidade, você deve incluir Olá informações que foram obtidas na etapa de preparação de unidade Olá a seguir:

    -   Id da unidade Olá

    -   chave do BitLocker Olá

    -   caminho relativo do arquivo de manifesto Olá no disco rígido Olá

    -   Olá Base16 codificado hash de MD5 do arquivo de manifesto

## <a name="shipping-your-drives"></a>Enviando suas unidades
Você deve enviar seu endereço de toohello de unidades que você obteve na etapa anterior Olá, e você deve fornecer Olá serviço de importação/exportação com hello controle o número de pacotes de saudação.

> [!NOTE]
>  Você deve enviar suas unidades por meio de um serviço de transporte compatível, que fornecerá um número de rastreamento para seu pacote.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Atualizar o trabalho de importação de saudação com as informações de envio
Depois que você tem o número de controle, chame Olá [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) Olá tooupdate de operação de envio nome da operadora, número de controle de saudação para trabalho hello e número de conta da operadora Olá para envio de retorno. Opcionalmente, você pode especificar número Olá de unidades e Olá também a data de envio.

## <a name="next-steps"></a>Próximas etapas

* [Usando a API REST do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
