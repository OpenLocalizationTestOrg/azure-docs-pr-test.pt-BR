---
title: "formato de arquivo de log de importação/exportação aaaAzure | Microsoft Docs"
description: "Saiba mais sobre o formato Olá Olá de arquivos de log criados quando as etapas são executadas para um trabalho do serviço de importação/exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Formato de arquivo de log de serviço de Importação/Exportação do Azure
Quando Olá serviço de importação/exportação do Microsoft Azure executa uma ação em uma unidade como parte de um trabalho de importação ou exportação, os logs são gravados tooblock blobs na conta de armazenamento Olá associada ao trabalho.  
  
Há dois logs que podem ser gravados pelo Olá serviço de importação/exportação:  
  
-   log de erros de saudação sempre é gerada no evento de saudação do erro.  
  
-   Hello log detalhado não é habilitado por padrão, mas pode ser habilitado pela configuração Olá `EnableVerboseLog` propriedade em uma [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operação.  
  
## <a name="log-file-location"></a>Local do arquivo de log  
Olá os logs são gravados tooblock blobs no contêiner de saudação ou diretório virtual especificado pelo Olá `ImportExportStatesPath` configuração, que você pode definir em uma `Put Job` operação. Olá local toowhich Olá os logs são gravados depende de como a autenticação é especificada para o trabalho de hello, junto com o valor de saudação especificado para `ImportExportStatesPath`. A autenticação para o trabalho de saudação pode ser especificada por meio de uma chave de conta de armazenamento ou um contêiner de SAS (assinatura de acesso compartilhado).  
  
nome de saudação do diretório virtual ou contêiner Olá pode ser o nome padrão de saudação do `waimportexport`, ou em outro contêiner ou nome do diretório virtual que você especificar.  
  
Olá tabela a seguir mostra as opções possíveis hello:  
  
|Método de autenticação|Valor de `ImportExportStatesPath`Elemento|Local dos Blobs de Log|  
|---------------------------|----------------------------------------------|---------------------------|  
|Chave da conta de armazenamento|Valor padrão|Um contêiner denominado `waimportexport`, que é o contêiner padrão de saudação. Por exemplo:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|Chave da conta de armazenamento|Valores especificados pelo usuário|Um contêiner nomeado pelo usuário hello. Por exemplo:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|SAS do contêiner|Valor padrão|Um diretório virtual chamado `waimportexport`, que é o nome do padrão de saudação, recipiente de saudação especificado no hello SAS.<br /><br /> Por exemplo, se Olá SAS especificada para o trabalho de Olá for `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, Olá log local será`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|SAS do contêiner|Valores especificados pelo usuário|Um diretório virtual denominado pelo usuário hello, recipiente de saudação especificado no hello SAS.<br /><br /> Por exemplo, se Olá SAS especificada para o trabalho de Olá for `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, e Olá especificado o diretório virtual é denominado `mylogblobs`, Olá log local será `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
Você pode recuperar Olá URL logs detalhados e de erro Olá Olá chamada [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação. Olá logs estão disponíveis após a conclusão do processamento da unidade de saudação.  
  
## <a name="log-file-format"></a>Formato do arquivo de log  
Olá formato para ambos os logs é Olá mesmo: um blob que contém descrições XML dos eventos de Olá ocorridos ao copiar blobs entre o disco rígido hello e conta saudação do cliente.  
  
log detalhado Olá contém informações completas sobre o status de Olá Olá operação de cópia para cada blob (para um trabalho de importação) ou arquivo (para um trabalho de exportação), enquanto o log de erros de saudação contém apenas informações de saudação de blobs ou arquivos que encontraram erros durante a saudação Importar ou exportar o trabalho.  
  
formato de log detalhado de saudação é mostrado abaixo. log de erros de saudação tem Olá a mesma estrutura, mas filtra operações bem-sucedidas.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Olá tabela a seguir descreve os elementos de Olá Olá do arquivo de log.  
  
|Elemento XML|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|`DriveLog`|Elemento XML|Representa um log de unidade.|  
|`Version`|Atributo, cadeia de caracteres|versão de saudação do formato de log hello.|  
|`DriveId`|Cadeia de caracteres|Olá número de série do hardware da unidade.|  
|`Status`|Cadeia de caracteres|Status do processamento de unidade de saudação. Consulte Olá `Drive Status Codes` tabela abaixo para obter mais informações.|  
|`Blob`|Elemento XML aninhado|Representa um blob.|  
|`Blob/BlobPath`|Cadeia de caracteres|Olá URI do blob hello.|  
|`Blob/FilePath`|Cadeia de caracteres|arquivo de toohello de caminho relativo de saudação na unidade de saudação.|  
|`Blob/Snapshot`|Datetime|versão do instantâneo de saudação do blob hello, para um trabalho de exportação.|  
|`Blob/Length`|Número inteiro|tamanho total de saudação do blob de saudação em bytes.|  
|`Blob/LastModified`|Datetime|saudação de data/hora blob Olá da última modificação, para um trabalho de exportação.|  
|`Blob/ImportDisposition`|Cadeia de caracteres|Olá disposição de blob hello, para um trabalho de importação de importação.|  
|`Blob/ImportDisposition/@Status`|Atributo, cadeia de caracteres|status de saudação do hello disposição de importação.|  
|`PageRangeList`|Elemento XML aninhado|Representa uma lista de intervalos de página para um blobs de página.|  
|`PageRange`|Elemento XML|Representa um intervalo de páginas.|  
|`PageRange/@Offset`|Atributo, inteiro|Iniciando o deslocamento do intervalo de página Olá no blob hello.|  
|`PageRange/@Length`|Atributo, inteiro|Comprimento em bytes do intervalo de páginas de saudação.|  
|`PageRange/@Hash`|Atributo, cadeia de caracteres|Hash de MD5 codificado para Base16 do intervalo de página hello.|  
|`PageRange/@Status`|Atributo, cadeia de caracteres|Status do processamento do intervalo de páginas de saudação.|  
|`BlockList`|Elemento XML aninhado|Representa uma lista de blocos para um blobs de bloco.|  
|`Block`|Elemento XML|Representa um bloco.|  
|`Block/@Offset`|Atributo, inteiro|Iniciando o deslocamento do bloco de saudação no blob de saudação.|  
|`Block/@Length`|Atributo, inteiro|Comprimento em bytes do bloco de saudação.|  
|`Block/@Id`|Atributo, cadeia de caracteres|ID do bloco de saudação.|  
|`Block/@Hash`|Atributo, cadeia de caracteres|Hash de MD5 codificado para Base16 do bloco de saudação.|  
|`Block/@Status`|Atributo, cadeia de caracteres|Status do processamento de bloco hello.|  
|`Metadata`|Elemento XML aninhado|Representa os metadados do blob hello.|  
|`Metadata/@Status`|Atributo, cadeia de caracteres|Status do processamento dos metadados de blob hello.|  
|`Metadata/GlobalPath`|Cadeia de caracteres|Arquivo de metadados globais de toohello caminho relativo.|  
|`Metadata/GlobalPath/@Hash`|Atributo, cadeia de caracteres|Hash de MD5 codificado para Base16 do arquivo de metadados globais hello.|  
|`Metadata/Path`|Cadeia de caracteres|Arquivo de metadados do caminho relativo toohello.|  
|`Metadata/Path/@Hash`|Atributo, cadeia de caracteres|Hash de MD5 codificado para Base16 do arquivo de metadados de saudação.|  
|`Properties`|Elemento XML aninhado|Representa as propriedades de blob hello.|  
|`Properties/@Status`|Atributo, cadeia de caracteres|Status do processamento propriedades de blob hello, por exemplo, o arquivo não encontrado, concluído.|  
|`Properties/GlobalPath`|Cadeia de caracteres|Arquivo de propriedades globais de toohello caminho relativo.|  
|`Properties/GlobalPath/@Hash`|Atributo, cadeia de caracteres|Hash de MD5 codificado para Base16 do arquivo de propriedades globais de saudação.|  
|`Properties/Path`|Cadeia de caracteres|Arquivo de propriedades de toohello de caminho relativo.|  
|`Properties/Path/@Hash`|Atributo, cadeia de caracteres|Hash de MD5 codificado para Base16 do arquivo de propriedades de saudação.|  
|`Blob/Status`|Cadeia de caracteres|Status do processamento Olá blob.|  
  
# <a name="drive-status-codes"></a>Códigos de status da unidade  
Olá tabela a seguir lista os códigos de status de saudação para uma unidade de processamento.  
  
|Código de status|Descrição|  
|-----------------|-----------------|  
|`Completed`|Olá unidade concluiu o processamento sem erros.|  
|`CompletedWithWarnings`|Olá unidade concluiu o processamento com avisos em um ou mais blobs por disposições de importação de saudação especificados para blobs de saudação.|  
|`CompletedWithErrors`|Olá unidade foi concluída com erros em um ou mais blobs ou partes.|  
|`DiskNotFound`|Nenhum disco foi encontrado na unidade de saudação.|  
|`VolumeNotNtfs`|Olá primeiro volume de dados em disco Olá não está no formato NTFS.|  
|`DiskOperationFailed`|Falha desconhecida ocorreu ao executar operações na unidade de saudação.|  
|`BitLockerVolumeNotFound`|Nenhum volume criptografável BitLocker foi encontrado.|  
|`BitLockerNotActivated`|O BitLocker não está habilitado no volume de saudação.|  
|`BitLockerProtectorNotFound`|protetor de senha numérica de saudação não existe no volume de saudação.|  
|`BitLockerKeyInvalid`|senha numérica de saudação fornecida não é possível desbloquear o volume de saudação.|  
|`BitLockerUnlockVolumeFailed`|Falha desconhecida ocorreu durante a tentativa de volume de saudação toounlock.|  
|`BitLockerFailed`|Uma falha desconhecida ocorreu ao executar operações BitLocker.|  
|`ManifestNameInvalid`|Olá nome de arquivo de manifesto é inválido.|  
|`ManifestNameTooLong`|nome do arquivo de manifesto de saudação é muito longo.|  
|`ManifestNotFound`|arquivo de manifesto Olá não foi encontrado.|  
|`ManifestAccessDenied`|Arquivo de manifesto de toohello de acesso é negado.|  
|`ManifestCorrupted`|Olá arquivo de manifesto está corrompido (Olá conteúdo não corresponde ao seu hash).|  
|`ManifestFormatInvalid`|conteúdo do manifesto Olá não está de acordo com formato necessário toohello.|  
|`ManifestDriveIdMismatch`|unidade Olá ID no arquivo de manifesto Olá não coincide Olá leitura da unidade de saudação.|  
|`ReadManifestFailed`|Ocorreu uma falha de e/s de disco durante a leitura do manifesto de saudação.|  
|`BlobListFormatInvalid`|Olá exportar lista de blob não está de acordo com formato necessário toohello.|  
|`BlobRequestForbidden`|Acessar toohello blobs na conta de armazenamento Olá é proibido. Isso pode ser devido a chave de conta de armazenamento tooinvalid ou SAS do contêiner.|  
|`InternalError`|E ocorreu um erro interno durante o processamento da unidade de saudação.|  
  
## <a name="blob-status-codes"></a>Códigos de status de blobs  
Olá tabela a seguir lista os códigos de status de saudação para processamento de um blob.  
  
|Código de status|Descrição|  
|-----------------|-----------------|  
|`Completed`|Olá blob concluiu o processamento sem erros.|  
|`CompletedWithErrors`|Olá blob concluiu o processamento com erros em um ou mais intervalos de páginas ou blocos, metadados ou propriedades.|  
|`FileNameInvalid`|nome de arquivo Hello é inválido.|  
|`FileNameTooLong`|nome do arquivo Hello é muito longo.|  
|`FileNotFound`|não foi encontrado o arquivo Hello.|  
|`FileAccessDenied`|Arquivo de toohello de acesso é negado.|  
|`BlobRequestFailed`|Falha na solicitação de serviço de Blob Olá tooaccess Olá blob.|  
|`BlobRequestForbidden`|solicitação de serviço de Blob Olá tooaccess Olá blob é proibida. Isso pode ser devido a chave de conta de armazenamento tooinvalid ou SAS do contêiner.|  
|`RenameFailed`|Falha ao blob de saudação toorename (para um trabalho de importação) ou arquivo de saudação (para um trabalho de exportação).|  
|`BlobUnexpectedChange`|Uma alteração inesperada ocorreu com o blob de saudação (para um trabalho de exportação).|  
|`LeasePresent`|Há uma concessão no blob de saudação.|  
|`IOFailed`|Um disco ou uma falha de e/s de rede ocorreu durante o processamento de blob de saudação.|  
|`Failed`|Falha desconhecida ocorreu ao processar o blob de saudação.|  
  
## <a name="import-disposition-status-codes"></a>Códigos de status de disposição de importação  
Olá tabela a seguir lista os códigos de status de saudação para resolver uma disposição de importação.  
  
|Código de status|Descrição|  
|-----------------|-----------------|  
|`Created`|Olá blob foi criado.|  
|`Renamed`|Olá blob foi renomeado por disposição de importação de renomeação. Olá `Blob/BlobPath` elemento contém Olá URI de blob Olá renomeado.|  
|`Skipped`|Olá blob foi ignorado por `no-overwrite` disposição de importação.|  
|`Overwritten`|blob Olá substituiu um blob existente por `overwrite` disposição de importação.|  
|`Cancelled`|Uma falha anterior interrompeu o processamento da disposição de importação de saudação.|  
  
## <a name="page-rangeblock-status-codes"></a>Códigos de status do intervalo de página/bloco  
Olá tabela a seguir lista os códigos de status de saudação para processamento de um intervalo de página ou bloco.  
  
|Código de status|Descrição|  
|-----------------|-----------------|  
|`Completed`|Olá intervalo de página ou bloco concluiu o processamento sem erros.|  
|`Committed`|Olá bloco foi confirmado, mas não no hello lista completa de bloco porque outros blocos tem falha ou colocar a própria lista completa de bloco falhou.|  
|`Uncommitted`|bloco de saudação é carregado, mas não foi confirmado.|  
|`Corrupted`|Olá intervalo de página ou bloco está corrompido (Olá conteúdo não corresponde ao seu hash).|  
|`FileUnexpectedEnd`|Fim de arquivo inesperado foi encontrado.|  
|`BlobUnexpectedEnd`|Fim de blob inesperado foi encontrado.|  
|`BlobRequestFailed`|Olá solicitar o serviço Blob tooaccess Olá intervalo de página ou bloco falhou.|  
|`IOFailed`|Um disco ou uma falha de e/s de rede ocorreu durante o processamento Olá intervalo de página ou bloco.|  
|`Failed`|Falha desconhecida ocorreu ao processar Olá intervalo de página ou bloco.|  
|`Cancelled`|Uma falha anterior interrompeu o processamento do intervalo de páginas de saudação ou bloco.|  
  
## <a name="metadata-status-codes"></a>Códigos de status de metadados  
Olá tabela a seguir lista os códigos de status de saudação para metadados de blob de processamento.  
  
|Código de status|Descrição|  
|-----------------|-----------------|  
|`Completed`|Olá metadados concluiu o processamento sem erros.|  
|`FileNameInvalid`|nome do arquivo de metadados de saudação é inválido.|  
|`FileNameTooLong`|nome do arquivo de metadados de saudação é muito longo.|  
|`FileNotFound`|arquivo de metadados de saudação não foi encontrado.|  
|`FileAccessDenied`|Arquivo de metadados de toohello de acesso é negado.|  
|`Corrupted`|arquivo de metadados de saudação está corrompido (Olá conteúdo não corresponde ao seu hash).|  
|`XmlReadFailed`|conteúdo da saudação de metadados não está de acordo com formato necessário toohello.|  
|`XmlWriteFailed`|Gravando Olá metadados que XML falhou.|  
|`BlobRequestFailed`|Falha na solicitação de serviço de Blob Olá tooaccess Olá metadados.|  
|`IOFailed`|Uma falha de e/s de disco ou rede ocorreu durante o processamento de metadados de saudação.|  
|`Failed`|Falha desconhecida ocorreu ao processar metadados hello.|  
|`Cancelled`|Uma falha anterior interrompeu o processamento dos metadados de saudação.|  
  
## <a name="properties-status-codes"></a>Códigos de status das propriedades  
Olá tabela a seguir lista os códigos de status de saudação para propriedades de blob de processamento.  
  
|Código de status|Descrição|  
|-----------------|-----------------|  
|`Completed`|Propriedades de saudação concluiu o processamento sem erros.|  
|`FileNameInvalid`|nome do arquivo de propriedades de saudação é inválido.|  
|`FileNameTooLong`|nome do arquivo de propriedades de saudação é muito longo.|  
|`FileNotFound`|arquivo de propriedades de saudação não foi encontrado.|  
|`FileAccessDenied`|Arquivo de propriedades de toohello de acesso é negado.|  
|`Corrupted`|arquivo de propriedades de saudação está corrompido (Olá conteúdo não corresponde ao seu hash).|  
|`XmlReadFailed`|conteúdo das propriedades Olá não está de acordo com formato necessário toohello.|  
|`XmlWriteFailed`|Gravar propriedades Olá que XML falhou.|  
|`BlobRequestFailed`|Falha na solicitação de serviço de Blob Olá tooaccess Olá propriedades.|  
|`IOFailed`|Uma falha de e/s de disco ou rede ocorreu durante o processamento de propriedades de saudação.|  
|`Failed`|Falha desconhecida ocorreu ao processar as propriedades de saudação.|  
|`Cancelled`|Uma falha anterior interrompeu o processamento das propriedades de saudação.|  
  
## <a name="sample-logs"></a>Logs de exemplo  
a seguir Olá é um exemplo de log detalhado.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
log de erros Olá correspondente é mostrado abaixo.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 log de erros de acompanhamento Olá para um trabalho de importação contém um erro sobre um arquivo não encontrado na unidade de importação de saudação. Observe que o status de saudação dos componentes subsequentes é `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Olá seguinte o log de erros para um trabalho de exportação indica que o conteúdo do blob Olá tem foi gravado com êxito toohello unidade, mas ocorreu um erro durante a exportação de propriedades do blob hello.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Próximas etapas
 
* [API REST de Importação/Exportação do Armazenamento](/rest/api/storageimportexport/)
