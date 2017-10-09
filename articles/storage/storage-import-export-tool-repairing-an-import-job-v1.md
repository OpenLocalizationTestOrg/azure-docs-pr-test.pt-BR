---
title: "aaaRepairing um trabalho de importação de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como toorepair um trabalho de importação foi criado e executado usando Olá importação/exportação do Azure service."
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
ms.openlocfilehash: a9ed81f50cffd8ae6e0cb21b25a04815c2b51ee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Reparação de um trabalho de importação
Olá serviço de importação/exportação do Microsoft Azure pode falhar toocopy alguns dos arquivos ou partes de um arquivo de toohello serviço Blob do Windows Azure. Alguns motivos para as falhas incluem:  
  
-   Arquivos corrompidos  
  
-   Unidades danificadas  
  
-   chave de conta de armazenamento Olá alterado enquanto estava sendo transferido arquivo hello.  
  
Olá, ferramenta de importação/exportação do Microsoft Azure pode ser executado com a importação de saudação arquivos de log de cópia do trabalho e ferramenta de saudação carregará arquivos ausentes hello (ou partes de um arquivo) o trabalho de importação do tooyour do Windows Azure storage conta toocomplete.  
  
## <a name="repairimport-parameters"></a>Parâmetros de RepairImport

Olá parâmetros a seguir podem ser especificados com **RepairImport**: 
  
|||  
|-|-|  
|**/r:**<RepairFile\>|**Obrigatório.** Arquivo de reparo do toohello de caminho, que controla o progresso de saudação de reparo do hello e permite que você tooresume um reparo interrompido. Cada unidade deve ter um, e somente um, arquivo de reparo. Quando você inicia um reparo para uma determinada unidade, passará no hello caminho tooa arquivo de reparo que ainda não existe. tooresume um reparo interrompido, você deve passar no nome de saudação de um arquivo de reparo existente. unidade de destino do Hello reparo arquivo correspondente toohello sempre deve ser especificada.|  
|**/logdir:**<LogDirectory\>|**Opcional** diretório de log Hello. Arquivos de log detalhados serão gravados toothis directory. Se nenhum diretório de log for especificado, diretório atual Olá será usado como diretório de log hello.|  
|**/d:**<TargetDirectories\>|**Obrigatório.** Um ou mais diretórios de separados por ponto e vírgula que contenham Olá arquivos originais que foram importados. unidade de importação de saudação também pode ser usada, mas não será necessária se locais alternativos dos arquivos originais estão disponíveis.|  
|**/bk:**<BitLockerKey\>|**Opcional** Você deve especificar a chave do BitLocker Olá se você quiser Olá ferramenta toounlock uma unidade criptografada onde os arquivos originais Olá estão disponíveis.|  
|**/sn:**<StorageAccountName\>|**Obrigatório.** nome de Olá Olá da conta de armazenamento para Olá o trabalho de importação.|  
|**/sk:**<StorageAccountKey\>|**Necessário** somente se uma SAS do contêiner não for especificada. chave de conta Olá para conta de armazenamento Olá Olá o trabalho de importação.|  
|**/csas:**<ContainerSas\>|**Necessário** se e somente se Olá chave de conta de armazenamento não for especificada. Olá SAS do contêiner para acessar blobs Olá associados ao trabalho de importação de saudação.|  
|**/CopyLogFile:**<DriveCopyLogFile\>|**Obrigatório.** Caminho toohello unidade copiar arquivo de log (log detalhado ou log de erros). arquivo Hello é gerado pelo Olá serviço de importação/exportação do Windows Azure e pode ser baixado do armazenamento de blob Olá associado ao trabalho hello. arquivo de log de cópia Olá contém informações sobre blobs com falha ou arquivos que são toobe reparado.|  
|**/PathMapFile:**<DrivePathMapFile\>|**Opcional** Arquivo de texto do caminho tooa que pode ser usado tooresolve ambiguidades se você tiver vários arquivos com hello mesmo nome que foram importados no hello mesmo trabalho. Olá primeiro tempo Olá ferramenta é executada, ela pode preencher este arquivo com todos os nomes ambíguos hello. Execuções subsequentes da ferramenta Olá usará esse ambiguidades de saudação do arquivo tooresolve.|  
  
## <a name="using-hello-repairimport-command"></a>Usando o comando RepairImport de saudação  
toorepair importar dados por fluxo de dados de saudação pela rede hello, você deve especificar diretórios de saudação que contêm Olá arquivos originais que você estava importando usando Olá `/d` parâmetro. Você também deve especificar o arquivo de log de cópia de saudação que você baixou da conta de armazenamento. Uma linha de comando típica toorepair um trabalho de importação com falhas parciais é semelhante a:  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
a seguir Olá é um exemplo de um arquivo de log de cópia. Nesse caso, uma parte de 64K de um arquivo foi corrompida na unidade de saudação que foi enviada para o trabalho de importação hello. Como essa é a única falha de saudação indicada, rest Olá de blobs Olá trabalho Olá foram importados com êxito.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
Quando esse log de cópia for passado toohello ferramenta de importação/exportação do Azure, ferramenta Olá tentará toofinish importação Olá desse arquivo copiando o conteúdo ausente Olá pela rede hello. Seguindo o exemplo hello acima, Olá ferramenta procurará arquivo original Olá `\animals\koala.jpg` nos diretórios de saudação dois `C:\Users\bob\Pictures` e `X:\BobBackup\photos`. Se hello arquivo `C:\Users\bob\Pictures\animals\koala.jpg` existir, Olá, ferramenta de importação/exportação do Azure copiará o intervalo de blob correspondente do dados toohello ausente Olá `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>Resolvendo conflitos ao usar RepairImport  
Em algumas situações, a ferramenta de saudação não pode ser capaz de toofind ou arquivo necessário do hello aberto para um dos motivos a seguir de saudação: não foi possível encontrar o arquivo hello, Olá arquivo não está acessível, o nome de arquivo hello é ambíguo ou Olá conteúdo do arquivo hello não está mais correto.  
  
Um erro ambíguo poderá ocorrer se a ferramenta hello está tentando toolocate `\animals\koala.jpg` e há um arquivo com esse nome em `C:\Users\bob\pictures` e `X:\BobBackup\photos`. Ou seja, ambos `C:\Users\bob\pictures\animals\koala.jpg` e `X:\BobBackup\photos\animals\koala.jpg` existe em unidades de trabalho de importação hello.  
  
Olá `/PathMapFile` opção permitirá tooresolve esses erros. Você pode especificar o nome de saudação do arquivo de saudação que será contém a lista de saudação de arquivos que Olá ferramenta não foi capaz de identificar toocorrectly. Olá, a seguir é uma linha de comando de exemplo que preenche `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
Olá ferramenta gravará os caminhos de arquivo problemáticos Olá muito`9WM35C2V_pathmap.txt`, um em cada linha. Por exemplo, arquivo hello pode conter Olá entradas a seguir depois de executar o comando hello:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Para cada arquivo na lista de hello, você deve tentar toolocate e abra Olá arquivo tooensure é ferramenta toohello disponíveis. Se desejar que a ferramenta de saudação tootell explicitamente onde toofind um arquivo, você pode modificar caminho Olá mapear o arquivo e adicionar Olá caminho tooeach arquivo em Olá mesma linha, separada por um caractere de tabulação:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
Depois de fazer ferramenta do hello arquivos necessários toohello disponível, ou arquivo de mapa de caminho de atualização hello, você pode executar novamente o processo de importação de saudação do hello ferramenta toocomplete.  
  
## <a name="next-steps"></a>Próximas etapas
 
* [Configurando Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup-v1.md)   
* [Preparação de discos rígidos para um trabalho de importação](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Revisão do status do trabalho com arquivos de log de cópia](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Reparação de um trabalho de exportação](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Olá, ferramenta de importação/exportação do Azure de solução de problemas](storage-import-export-tool-troubleshooting-v1.md)
