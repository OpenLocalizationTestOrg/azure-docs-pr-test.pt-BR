---
title: "aaaCreate uma exportação de trabalho de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toocreate uma exportação de trabalho para Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Criar um trabalho de exportação para Olá serviço de importação/exportação do Azure
Criar um trabalho de exportação para o serviço de importação/exportação do Microsoft Azure hello usando Olá API REST envolve Olá etapas a seguir:

-   Selecionar Olá blobs tooexport.

-   Obter uma localização de envio.

-   Criar trabalho de exportação de saudação.

-   Envio tooMicrosoft suas unidades vazias por meio de um serviço de transporte com suporte.

-   Atualizar o trabalho de exportação de saudação com informações do pacote de saudação.

-   Receber Olá unidades da Microsoft.

 Consulte [usando Olá importação/exportação do Windows Azure service tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para obter uma visão geral do serviço de importação/exportação do hello e um tutorial que demonstra como Olá toouse [portal do Azure](https://portal.azure.com/) toocreate gerenciar importar e exportar trabalhos.

## <a name="selecting-blobs-tooexport"></a>Selecionar blobs tooexport
 toocreate um trabalho de exportação, você precisará tooprovide uma lista de blobs que você deseja tooexport da conta de armazenamento. Há algumas maneiras tooselect blobs toobe exportado:

-   Você pode usar um tooselect de caminho de blob relativo de um único blob e todos os seus instantâneos.

-   Você pode usar um tooselect de caminho de blob relativo um único blob, excluindo seus instantâneos.

-   Você pode usar um caminho de blob relativo e um tempo de instantâneo tooselect um único instantâneo.

-   Você pode usar um tooselect de prefixo de blob todos os blobs e instantâneos com hello fornecido prefixo.

-   Você pode exportar todos os blobs e instantâneos na conta de armazenamento hello.

 Para obter mais informações sobre como especificar blobs tooexport, consulte Olá [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.

## <a name="obtaining-your-shipping-location"></a>Obtendo o local de envio
Antes de criar um trabalho de exportação, você precisa tooobtain um nome de local de envio e o endereço por chamada hello [obter local](https://portal.azure.com) ou [listar locais](/rest/api/storageimportexport/listlocations) operação. `List Locations` retorna uma lista de locais e seus endereços de correspondência. Você pode selecionar um local da saudação retornada lista e seu endereço de toothat de unidades de disco rígido de destino. Você também pode usar o hello `Get Location` Olá tooobtain de operação envio diretamente o endereço para um local específico.

Siga as próximas etapas, Olá local de envio de saudação do tooobtain:

-   Identificar o nome de saudação do local de saudação de sua conta de armazenamento. Esse valor pode ser encontrado em Olá **local** campo da conta de armazenamento Olá **painel** em clássico Olá portal ou consultado por meio de operação da API de gerenciamento de serviços de saudação [obter Propriedades da conta de armazenamento](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Recuperar o local de saudação que estão disponíveis tooprocess esta conta de armazenamento por chamada hello `Get Location` operação.

-   Se hello `AlternateLocations` propriedade de local de saudação contém o local de saudação em si, então é toouse okey neste local. Caso contrário, chamar hello `Get Location` operação novamente com um dos locais alternativos de saudação. local original Olá pode estar fechada temporariamente para manutenção.

## <a name="creating-hello-export-job"></a>Criar trabalho de exportação de saudação
 trabalho de exportação toocreate hello, chamada hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação. Você precisará Olá tooprovide informações a seguir:

-   Um nome para o trabalho de saudação.

-   nome de conta de armazenamento Hello.

-   saudação de envio de nome local, obtido na etapa anterior hello.

-   Um tipo de trabalho (Exportação).

-   endereço de devolução Olá onde Olá unidades devem ser enviadas após a conclusão do trabalho de exportação de saudação.

-   Olá toobe de lista de blobs (ou prefixos de blob) exportado.

## <a name="shipping-your-drives"></a>Enviando suas unidades
 Em seguida, usar Olá ferramenta de importação/exportação do Azure toodetermine Olá número de unidades que precisar toosend, com base em blobs Olá selecionado toobe exportado e Olá tamanho da unidade. Consulte Olá [referência da ferramenta de importação/exportação do Azure](storage-import-export-tool-how-to-v1.md) para obter detalhes.

 Unidades de saudação do pacote em um único pacote e enviá-las toohello endereço obtido na Olá etapa anterior. Observe Olá número do seu pacote para a próxima etapa de saudação de controle.

> [!NOTE]
>  Você deve enviar suas unidades por meio de um serviço de transporte compatível, que fornecerá um número de rastreamento para seu pacote.

## <a name="updating-hello-export-job-with-your-package-information"></a>Atualizar o trabalho de exportação de saudação com as informações do pacote
 Depois que você tem o número de controle, chame Olá [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) nome da operadora operação tooupdated hello e número de controle para o trabalho de saudação. Opcionalmente, você pode especificar número de saudação de unidades, o endereço de retorno hello e data de envio de saudação.

## <a name="receiving-hello-package"></a>Pacote de saudação de recebimento
 Depois que o trabalho de exportação tiver sido processado, as unidades serão retornadas tooyou com os dados criptografados. Você pode recuperar a chave do BitLocker Olá para cada uma das unidades de saudação pela chamada hello [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_Get) operação. Você pode então desbloquear unidade hello usando Olá chave. arquivo de manifesto Olá unidade em cada unidade contém a lista de saudação dos arquivos na unidade hello, bem como o endereço original de blob Olá para cada arquivo.

## <a name="next-steps"></a>Próximas etapas

* [Usando a API REST do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
