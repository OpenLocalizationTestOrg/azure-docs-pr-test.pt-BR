---
title: "Amostra de script do Azure PowerShell – calcular o tamanho total de cobrança de um contêiner de blobs | Microsoft Docs"
description: "Calcule o tamanho total de um contêiner no armazenamento de Blobs do Azure para fins de cobrança."
services: storage
documentationcenter: na
author: fhryo-msft
manager: cbrooks
editor: tysonn
ms.assetid: 
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: sample
ms.date: 11/07/2017
ms.author: fryu
ms.openlocfilehash: c37b416578a76e9b12e29d68e413d851796ccc6f
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="calculate-the-total-billing-size-of-a-blob-container"></a>Calcular o tamanho total de cobrança de um contêiner de blob

Este script calcula o tamanho de um contêiner no armazenamento de Blobs do Azure com a finalidade de estimar os custos de cobrança. O script soma o tamanho dos blobs no contêiner.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

> [!NOTE]
> Este script do PowerShell calcula o tamanho de um contêiner para fins de cobrança. Caso esteja calculando o tamanho do contêiner para outros fins, consulte [Calcular o tamanho total de um contêiner do armazenamento de Blobs](../scripts/storage-blobs-container-calculate-size-powershell.md) para obter um script mais simples que fornece uma estimativa.

## <a name="determine-the-size-of-the-blob-container"></a>Determinar o tamanho do contêiner de blob

O tamanho total do contêiner de blob inclui o tamanho do próprio contêiner e o tamanho de todos os blobs no contêiner.

O exemplo de seções a seguir descreve como a capacidade de armazenamento é calculada para contêineres de blob e blobs. Na seção a seguir, Len(X) significa o número de caracteres na cadeia de caracteres.

### <a name="blob-containers"></a>Contêineres de blob

O cálculo a seguir descreve como estimar a quantidade de armazenamento consumida por contêiner de blob:

`
48 bytes + Len(ContainerName) * 2 bytes +
For-Each Metadata[3 bytes + Len(MetadataName) + Len(Value)] +
For-Each Signed Identifier[512 bytes]
`

A seguir, encontra-se a divisão:
* 48 bytes de sobrecarga para cada contêiner inclui a Hora da última modificação, as Permissões, as Configurações públicas e alguns metadados do sistema.

* O nome do contêiner é armazenado como Unicode. Portanto, multiplique o número de caracteres por dois.

* Para cada bloco de metadados do contêiner de blob armazenado, armazenamos o comprimento do nome (ASCII) mais o comprimento do valor da cadeia de caracteres.

* Os 512 bytes por Identificador Assinado incluem o nome do identificador assinado, a hora de início, a hora de expiração e as permissões.

### <a name="blobs"></a>Blobs

Os cálculos a seguir mostram como estimar a quantidade de armazenamento consumido por blob.

* Blob de blocos (instantâneo ou blob de base):

   `
   124 bytes + Len(BlobName) * 2 bytes +
   For-Each Metadata[3 bytes + Len(MetadataName) + Len(Value)] +
   8 bytes + number of committed and uncommitted blocks * Block ID Size in bytes +
   SizeInBytes(data in unique committed data blocks stored) +
   SizeInBytes(data in uncommitted data blocks)
   `

* Blob de páginas (instantâneo ou blob de base):

   `
   124 bytes + Len(BlobName) * 2 bytes +
   For-Each Metadata[3 bytes + Len(MetadataName) + Len(Value)] +
   number of nonconsecutive page ranges with data * 12 bytes +
   SizeInBytes(data in unique pages stored)
   `

A seguir, encontra-se a divisão:

* 124 bytes de sobrecarga para blob, que inclui:
    - Hora da Última Modificação
    - Tamanho
    - Cache-Control
    - Tipo de conteúdo
    - Content-Language
    - Codificação de conteúdo
    - Content-MD5
    - Permissões
    - Informações do instantâneo
    - Concessão
    - Alguns metadados do sistema

* O nome do blob é armazenado como Unicode, portanto, multiplique o número de caracteres por dois.

* Para cada bloco de metadados armazenados, adicione o comprimento do nome (armazenado como ASCII) mais o comprimento do valor de cadeia de caracteres.

* Para os blobs de bloco:
    * 8 bytes para a lista de blocos.
    * Número de blocos vezes o tamanho da ID do bloco em bytes.
    * O tamanho dos dados em todos os blocos confirmados e não confirmados. 
    
    >[!NOTE]
    >Quando os instantâneos são usados, esse tamanho inclui apenas os dados exclusivos para esse blob de instantâneo ou de base. Se os blocos não confirmados não forem usados após uma semana, eles serão coletados como lixo. Depois disso, eles não contam para cobrança.

* Para blobs de página:
    * O número de intervalos de página não consecutivos que têm dados vezes 12 bytes. Esse é o número de intervalos de páginas únicos que você vê ao chamar a API **GetPageRanges**.

    * O tamanho dos dados em bytes de todas as páginas armazenadas. 
    
    >[!NOTE]
    >Quando instantâneos são usados, esse tamanho inclui apenas as páginas exclusivas para o blob de base ou o blob de instantâneo que está sendo contado.

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/storage/calculate-container-size/calculate-container-size-ex.ps1 "Calculate container size")]

## <a name="next-steps"></a>Próximas etapas

- Consulte [Calcular o tamanho total de um contêiner do armazenamento de Blobs](../scripts/storage-blobs-container-calculate-size-powershell.md) para obter um script simples que fornece uma estimativa do tamanho do contêiner.

- Para obter mais informações sobre a Cobrança do Azure Storage, consulte [Noções básicas sobre a Cobrança do Armazenamento do Microsoft Azure](https://blogs.msdn.microsoft.com/windowsazurestorage/2010/07/08/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity/).

- Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.4.1).

- Encontre exemplos adicionais de script do PowerShell de Armazenamento em [Amostras do PowerShell para Armazenamento do Azure](../blobs/storage-samples-blobs-powershell.md).
