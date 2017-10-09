---
title: "aaaRepairing um trabalho de exportação de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como toorepair um trabalho de exportação foi criado e executado usando Olá importação/exportação do Azure service."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e54bc66495c8a3473b8ec51bb254bce8bdc9eab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>Reparação de um trabalho de exportação
Depois que um trabalho de exportação for concluída, você pode executar Olá, ferramenta de importação/exportação do Microsoft Azure local para:  
  
1.  Baixe os arquivos que o serviço de importação/exportação do Azure Olá foi tooexport não é possível.  
  
2.  Valide arquivos Olá na unidade Olá foram exportados corretamente.  
  
Você deve ter conectividade tooAzure armazenamento toouse essa funcionalidade.  
  
saudação de comando para reparar um trabalho de importação é **RepairExport**.

## <a name="repairexport-parameters"></a>Parâmetros de RepairExport

Olá parâmetros a seguir podem ser especificados com **RepairExport**:  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|**/r:<RepairFile\>**|Obrigatório. Arquivo de reparo do toohello de caminho, que controla o progresso de saudação de reparo do hello e permite que você tooresume um reparo interrompido. Cada unidade deve ter um, e somente um, arquivo de reparo. Quando você inicia um reparo para uma determinada unidade, passará no hello caminho tooa arquivo de reparo que ainda não existe. tooresume um reparo interrompido, você deve passar no nome de saudação de um arquivo de reparo existente. unidade de destino do Hello reparo arquivo correspondente toohello sempre deve ser especificada.|  
|**/logdir:<LogDirectory\>**|Opcional. diretório de log Hello. Arquivos de log detalhados serão gravados toothis directory. Se nenhum diretório de log for especificado, diretório atual Olá será usado como diretório de log hello.|  
|**/d:<TargetDirectory\>**|Obrigatório. Olá diretório toovalidate e reparo. Isso geralmente é o diretório raiz de saudação da unidade de exportação hello, mas pode também ser um compartilhamento de arquivos de rede que contém uma cópia dos arquivos hello exportada.|  
|**/bk:<BitLockerKey\>**|Opcional. Você deve especificar a chave do BitLocker Olá se você quiser Olá ferramenta toounlock uma unidade criptografada onde hello exportada arquivos são armazenados.|  
|**/sn:<StorageAccountName\>**|Obrigatório. trabalho de exportação de nome de Olá Olá da conta de armazenamento para hello.|  
|**/sk:<StorageAccountKey\>**|**Necessário** somente se uma SAS do contêiner não for especificada. trabalho de exportação da chave da conta Olá para conta de armazenamento Olá Olá.|  
|**/csas:<ContainerSas\>**|**Necessário** se e somente se Olá chave de conta de armazenamento não for especificada. Olá SAS do contêiner para acessar blobs Olá associados ao trabalho de exportação de saudação.|  
|**/CopyLogFile:<DriveCopyLogFile\>**|Obrigatório. Olá caminho toohello unidade copiar arquivo do log. arquivo Hello é gerado pelo Olá serviço de importação/exportação do Windows Azure e pode ser baixado do armazenamento de blob Olá associado ao trabalho hello. arquivo de log de cópia Olá contém informações sobre blobs com falha ou arquivos que são toobe reparado.|  
|**/ManifestFile:<DriveManifestFile\>**|Opcional. arquivo de manifesto da unidade de exportação toohello caminho Hello. Esse arquivo é gerado pelo serviço de importação/exportação do Windows Azure hello e armazenado na unidade de exportação hello e, opcionalmente em um blob na conta de armazenamento Olá associado ao trabalho hello.<br /><br /> Olá conteúdo Olá arquivos na unidade de exportação Olá será verificado com hello os hashes MD5 contidos nesse arquivo. Todos os arquivos que são determinado toobe corrompido será baixado e reescrito toohello diretórios de destino.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>Usando RepairExport modo toocorrect falha exportações  
Você pode usar arquivos toodownload do hello ferramenta de importação/exportação do Azure que falha tooexport. arquivo de log de cópia Olá conterá uma lista dos arquivos que não tooexport.  
  
as causas das falhas de exportação Olá incluem hello seguintes possibilidades:  
  
-   Unidades danificadas  
  
-   chave de conta de armazenamento Olá alterado durante o processo de transferência Olá  
  
ferramenta de saudação toorun **RepairExport** modo, você primeiro precisa de unidade de saudação tooconnect contendo Olá arquivos exportados tooyour computador. Em seguida, execute Olá, ferramenta de importação/exportação do Azure, especificando Olá caminho toothat unidade com hello `/d` parâmetro. Também é necessário o arquivo de log de cópia da unidade do toohello caminho Olá toospecify que você baixou. Hello seguinte exemplo de linha de comando abaixo executa Olá ferramenta toorepair todos os arquivos que falharam tooexport:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
a seguir Olá é um exemplo de um arquivo de log de cópia que mostra um bloco em Olá blob falhado tooexport:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
arquivo de log de cópia Olá indica que ocorreu uma falha enquanto Olá serviço de importação/exportação do Windows Azure baixava um dos arquivos de toohello blocos do blob Olá na unidade de exportação de saudação. Olá outros componentes do arquivo hello baixado com êxito e tamanho do arquivo hello foi definido corretamente. Nesse caso, ferramenta Olá abrir arquivo hello na unidade hello, baixar bloco Olá Olá da conta de armazenamento e grave-o intervalo de arquivo toohello partir do deslocamento 65536 com comprimento 65536.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>Usando RepairExport toovalidate conteúdo da unidade  
Você também pode usar a importação/exportação do Azure com hello **RepairExport** opção toovalidate Olá conteúdo na unidade hello está correto. arquivo de manifesto de saudação em cada unidade de exportação contém MD5s para conteúdo de saudação da unidade de saudação.  
  
Olá serviço de importação/exportação do Azure também pode salvar os arquivos de manifesto Olá tooa conta de armazenamento durante o processo de exportação hello. Hello local dos arquivos de manifesto hello está disponível por meio de saudação [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação quando o trabalho Olá tiver sido concluído. Consulte [formato do arquivo de manifesto do serviço de importação/exportação](storage-import-export-file-format-metadata-and-properties.md) para obter mais informações sobre o formato de saudação de um arquivo de manifesto da unidade.  
  
Olá exemplo a seguir mostra como toorun Olá ferramenta de importação/exportação do Azure com hello **/ManifestFile** e **/CopyLogFile** parâmetros:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
Olá seguinte é um exemplo de um arquivo de manifesto:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
Depois de terminar processo de reparo Olá, ferramenta Olá lerá cada arquivo referenciado no arquivo de manifesto hello e verificar a integridade do arquivo hello com hashes MD5 de saudação. Para o manifesto Olá acima, ele percorrerá Olá componentes a seguir.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Qualquer componente com falha de verificação de saudação será baixado pela ferramenta hello e reescrito toohello mesmo arquivo na unidade de saudação.  
  
## <a name="next-steps"></a>Próximas etapas
 
* [Configurando Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup-v1.md)   
* [Preparação de discos rígidos para um trabalho de importação](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Revisão do status do trabalho com arquivos de log de cópia](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Reparação de um trabalho de importação](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Olá, ferramenta de importação/exportação do Azure de solução de problemas](storage-import-export-tool-troubleshooting-v1.md)
