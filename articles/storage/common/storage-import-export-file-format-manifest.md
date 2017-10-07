---
title: "formato de arquivo de manifesto de importação/exportação aaaAzure | Microsoft Docs"
description: "Saiba mais sobre o formato Olá Olá unidade do arquivo de manifesto que descreve o mapeamento de saudação entre blobs no armazenamento de BLOBs do Azure e arquivos em uma unidade em um trabalho de importação ou exportação no serviço de importação/exportação de saudação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Formato de arquivo de manifesto do serviço de Importação/Exportação do Azure
arquivo de manifesto da unidade Olá descreve o mapeamento de saudação entre blobs no armazenamento de BLOBs do Azure e os arquivos na unidade que incluem um trabalho de importação ou exportação. Para uma operação de importação, o arquivo de manifesto de saudação é criado como parte do processo de preparação de unidade Olá e é armazenado na unidade de saudação antes de unidade de saudação é enviada toohello data center do Azure. Durante uma operação de exportação, manifesto Olá é criado e armazenado na unidade de saudação por Olá serviço de importação/exportação do Azure.  
  
Para ambos importar e trabalhos de exportação, o arquivo de manifesto da unidade Olá é armazenado no hello importar ou exportar unidade; não é transmitida toohello serviço por meio de qualquer operação de API.  
  
Olá informações a seguir descrevem o formato geral de saudação de um arquivo de manifesto da unidade:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>Elementos e atributos XML do manifesto

elementos de dados de saudação e os atributos de formato XML de manifesto da unidade de hello estão especificados na Olá a tabela a seguir.  
  
|Elemento XML|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|`DriveManifest`|Elemento raiz|elemento de raiz Olá Olá do arquivo de manifesto. Todos os outros elementos no arquivo hello estão abaixo desse elemento.|  
|`Version`|Atributo, cadeia de caracteres|versão Olá Olá do arquivo de manifesto.|  
|`Drive`|Elemento XML aninhado|Contém manifesto de saudação para cada unidade.|  
|`DriveId`|Cadeia de caracteres|Olá identificador exclusivo para a unidade de saudação. Identificador de unidade de saudação é encontrado consultando a unidade de saudação para seu número de série. número de série da unidade de saudação geralmente é impresso na Olá fora da unidade de saudação também. Olá `DriveID` elemento deve aparecer antes de qualquer `BlobList` elemento no arquivo de manifesto hello.|  
|`StorageAccountKey`|Cadeia de caracteres|Obrigatório para os trabalhos de importação se, e somente se, `ContainerSas` não for especificado. chave da conta Olá para Olá conta de armazenamento do Azure associado ao trabalho de saudação.<br /><br /> Esse elemento é omitido do manifesto de saudação para uma operação de exportação.|  
|`ContainerSas`|Cadeia de caracteres|Obrigatório para os trabalhos de importação se, e somente se, `StorageAccountKey` não for especificado. Olá SAS do contêiner para acessar blobs Olá associados ao trabalho hello. Consulte [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) para seu formato. Esse elemento é omitido do manifesto de saudação para uma operação de exportação.|  
|`ClientCreator`|Cadeia de caracteres|Especifica o cliente de saudação que criou o arquivo XML de saudação. Esse valor não seja interpretado pelo Olá serviço de importação/exportação.|  
|`BlobList`|Elemento XML aninhado|Contém uma lista de blobs que fazem parte da importação de saudação ou trabalho de exportação. Cada blob em uma lista de blob compartilhamentos Olá mesmo metadados e propriedades.|  
|`BlobList/MetadataPath`|Cadeia de caracteres|Opcional. Especifica o caminho relativo de saudação de um arquivo em disco Olá que contém metadados de padrão de saudação serão definidos em blobs na lista de blob Olá para uma operação de importação. Opcionalmente, esses metadados podem ser substituídos de blob em blob.<br /><br /> Esse elemento é omitido do manifesto de saudação para uma operação de exportação.|  
|`BlobList/MetadataPath/@Hash`|Atributo, cadeia de caracteres|Especifica o valor de hash MD5 codificado para Base16 Olá para o arquivo de metadados de saudação.|  
|`BlobList/PropertiesPath`|Cadeia de caracteres|Opcional. Especifica o caminho relativo de saudação de um arquivo no disco de saudação que contém as propriedades de padrão de saudação que serão definidas em blobs na lista de blob Olá para uma operação de importação. Opcionalmente, essas propriedades podem ser substituídas de blob em blob.<br /><br /> Esse elemento é omitido do manifesto de saudação para uma operação de exportação.|  
|`BlobList/PropertiesPath/@Hash`|Atributo, cadeia de caracteres|Especifica o valor de hash MD5 codificado para Base16 Olá para o arquivo de propriedades de saudação.|  
|`Blob`|Elemento XML aninhado|Contém informações sobre cada blob em cada lista de blobs.|  
|`Blob/BlobPath`|Cadeia de caracteres|Olá URI toohello blob relativo, começando com o nome do contêiner de saudação. Se o blob Olá estiver no contêiner raiz, ele deve começar com `$root`.|  
|`Blob/FilePath`|Cadeia de caracteres|Especifica o arquivo de toohello de caminho relativo de saudação na unidade de saudação. Para trabalhos de exportação, caminho de blob Olá será usado para o caminho do arquivo hello se possível; *, por exemplo,*, `pictures/bob/wild/desert.jpg` serão exportados muito`\pictures\bob\wild\desert.jpg`. No entanto, devido a limitações de toohello de nomes NTFS, um blob pode ser exportado tooa arquivo com um caminho que não é o caminho de blob Olá semelhante.|  
|`Blob/ClientData`|Cadeia de caracteres|Opcional. Contém comentários do cliente hello. Esse valor não seja interpretado pelo Olá serviço de importação/exportação.|  
|`Blob/Snapshot`|Datetime|Opcional para trabalhos de exportação. Especifica o identificador de instantâneo de saudação para um instantâneo de blob exportado.|  
|`Blob/Length`|Número inteiro|Especifica o comprimento total de saudação do blob de saudação em bytes. valor de saudação pode ser a too200 GB para um blob de blocos e até too1 TB para um blob de página. Para um blob de páginas, esse valor deve ser um múltiplo de 512.|  
|`Blob/ImportDisposition`|Cadeia de caracteres|Opcional para trabalhos de importação, omitida para trabalhos de exportação. Especifica como a saudação serviço de importação/exportação deve tratar caso Olá para um trabalho de importação onde um blob com hello mesmo nome já existe. Se esse valor é omitido do manifesto de importação de saudação, o valor de padrão de saudação é `rename`.<br /><br /> os valores Hello para esse elemento incluem:<br /><br /> -   `no-overwrite`: Se um blob de destino já está presente com hello mesmo nome, operação de importação de saudação vai ignorar a importação desse arquivo.<br />-   `overwrite`: Qualquer blob de destino existente será substituído completamente pelo arquivo recém-importado hello.<br />-   `rename`: blob novo Olá será carregado com um nome modificado.<br /><br /> Olá Renomear regra é o seguinte:<br /><br /> -Se o nome do blob Olá não contém um ponto, um novo nome será gerado anexando `(2)` toohello nome original do blob; se esse novo nome também entrar em conflito com um nome de blob existente, em seguida, `(3)` está anexado no lugar de `(2)`; e assim por diante.<br />-Se o nome do blob Olá contém um ponto, parte de saudação após o último ponto de saudação é considerado nome da extensão hello. Toohello semelhante acima procedimento, `(2)` é inserida antes Olá último ponto toogenerate um novo nome; se o nome do novo Olá ainda está em conflito com um nome de blob existente, em seguida, Olá serviço tenta `(3)`, `(4)`e assim por diante, até que não conflitante nome foi encontrado.<br /><br /> Alguns exemplos:<br /><br /> blob Olá `BlobNameWithoutDot` será renomeado para:<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> blob Olá `Seattle.jpg` será renomeado para:<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|Elemento XML aninhado|Obrigatório para um blob de páginas.<br /><br /> Para a importação de uma operação, especifica uma lista de intervalos de bytes de um toobe arquivo importado. Cada intervalo de página é descrito por um deslocamento e comprimento no arquivo de origem de saudação que descreve o intervalo de páginas hello, junto com um hash MD5 da região de saudação. Olá `Hash` atributo de um intervalo de página é necessário. serviço de saudação validará hash Olá de dados blob Olá Olá corresponde Olá computada o hash MD5 do intervalo de páginas de saudação. Qualquer número de intervalos de página pode ser usado toodescribe um arquivo para uma importação, com tamanho total da saudação too1 TB. Todos os intervalos de página devem ser ordenados por deslocamento, e não há permissão para sobreposições.<br /><br /> Para uma operação de exportação, especifica um conjunto de intervalos de bytes de um blob que foram exportados toohello unidade.<br /><br /> intervalos de página Olá juntos podem abranger apenas subintervalos de um arquivo ou blob.  Saudação da parte restante do arquivo hello não coberto por qualquer intervalo de página é esperada e seu conteúdo pode ser indefinido.|  
|`PageRange`|Elemento XML|Representa um intervalo de páginas.|  
|`PageRange/@Offset`|Atributo, inteiro|Especifica o deslocamento de saudação no arquivo de transferência hello e blob Olá onde Olá especificado o intervalo de página começa. Esse valor deve ser um múltiplo de 512.|  
|`PageRange/@Length`|Atributo, inteiro|Especifica o comprimento de saudação do intervalo de página hello. Esse valor deve ser um múltiplo de 512 e não ultrapassar 4 MB.|  
|`PageRange/@Hash`|Atributo, cadeia de caracteres|Especifica o valor de hash MD5 codificado para Base16 Olá para o intervalo de páginas de saudação.|  
|`BlockList`|Elemento XML aninhado|Obrigatório para um blob de blocos com blocos nomeados.<br /><br /> Para uma operação de importação, a lista de bloqueios de saudação especifica um conjunto de blocos que serão importados para o armazenamento do Azure. Para uma operação de exportação, a lista de bloqueios de saudação especifica onde cada bloco foi armazenado no arquivo hello no disco de exportação de saudação. Cada bloco é descrito por um deslocamento no arquivo hello e um tamanho de bloco; cada bloco Além disso é nomeado por um atributo de ID de bloco e contém um hash MD5 para o bloco de saudação. Backup too50, 000 blocos podem ser usado toodescribe um blob.  Todos os blocos deverão ser ordenados pelo deslocamento e juntos devem cobrir o intervalo completo de saudação do arquivo hello, *ou seja,*, não deve haver nenhum espaço entre blocos. Se o blob Olá é não mais do que 64 MB, IDs de bloco Olá para cada bloco deve ser todas ausentes ou todos os presentes. IDs de bloco são cadeias de caracteres codificada em Base64 do toobe necessária. Consulte [Put Block](/rest/api/storageservices/put-block) para ver mais requisitos para IDs de bloco.|  
|`Block`|Elemento XML|Representa um bloco.|  
|`Block/@Offset`|Atributo, inteiro|Especifica o deslocamento de saudação onde o bloco de saudação especificado começa.|  
|`Block/@Length`|Atributo, inteiro|Especifica o número de saudação de bytes no bloco de saudação; Esse valor deve ser não mais do que 4MB.|  
|`Block/@Id`|Atributo, cadeia de caracteres|Especifica uma cadeia de caracteres que representa a ID de bloco Olá para o bloco de saudação.|  
|`Block/@Hash`|Atributo, cadeia de caracteres|Especifica o hash MD5 codificado para Base16 Olá bloco hello.|  
|`Blob/MetadataPath`|Cadeia de caracteres|Opcional. Especifica o caminho relativo de saudação de um arquivo de metadados. Durante uma importação, Olá metadados é definido no blob de destino hello. Durante uma operação de exportação, metadados de blob Olá é armazenado no arquivo de metadados de saudação na unidade de saudação.|  
|`Blob/MetadataPath/@Hash`|Atributo, cadeia de caracteres|Especifica o hash de MD5 codificado para Base16 de saudação do arquivo de metadados do blob hello.|  
|`Blob/PropertiesPath`|Cadeia de caracteres|Opcional. Especifica o caminho relativo de saudação de um arquivo de propriedades. Durante uma importação, as propriedades de saudação são definidas no blob de destino hello. Durante uma operação de exportação, propriedades de blob de saudação são armazenadas no arquivo de propriedades de saudação na unidade de saudação.|  
|`Blob/PropertiesPath/@Hash`|Atributo, cadeia de caracteres|Especifica o hash de MD5 codificado para Base16 Olá Olá de propriedades do arquivo de blob.|  
  
## <a name="next-steps"></a>Próximas etapas
 
* [API REST de Importação/Exportação do Armazenamento](/rest/api/storageimportexport/)
