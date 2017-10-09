---
title: "Olá aaaTroubleshooting ferramenta de importação/exportação do Azure | Microsoft Docs"
description: "Saiba mais sobre alguns dos problemas comuns de saudação vistos ao usar Olá, ferramenta de importação/exportação do Azure e como toohandle-los."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 5445cefe2703edf4d9d285f761433b7b66d8cb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Olá, ferramenta de importação/exportação do Azure de solução de problemas
Olá, ferramenta de importação/exportação do Microsoft Azure retorna mensagens de erro se encontrar problemas. Este tópico lista alguns problemas comuns que os usuários poderão enfrentar.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Quando uma sessão de cópia falha o que devo fazer?  
 Quando uma sessão de cópia falha, há duas opções:  
  
 Se o erro de saudação for reproduzível, por exemplo, se o compartilhamento de rede Olá estava offline por um curto período e agora está novamente online, você pode retomar a sessão de cópia de saudação. Se o erro Olá não for reproduzível, por exemplo, se você especificou o diretório do arquivo de origem errado Olá nos parâmetros de linha de comando de saudação, será necessário tooabort sessão de cópia de saudação. Consulte [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparando os discos rígidos para um trabalho de importação) para obter mais informações sobre como continuar e anular sessões de cópia.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>Não consigo retomar nem anular uma sessão de cópia.  
 Se a sessão de cópia Olá for Olá primeira sessão de cópia para uma unidade, mensagem de saudação do erro deve indicar: "hello primeira sessão de cópia não pode ser retomada ou anulada." Nesse caso, você pode excluir o arquivo de diário antigo hello e execute novamente o comando hello.  
  
 Se uma sessão de cópia não é hello um primeiro para uma unidade, ele pode sempre ser retomado ou anulado.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>Perdi o arquivo de diário hello, ainda posso criar trabalho Olá?  
 arquivo de diário Olá para uma unidade contém informações completas de saudação de cópia de unidade de toothis de dados, e é necessário tooadd mais arquivos toohello de unidade e será usado toocreate um trabalho de importação. Se o arquivo de diário Olá for perdido, você terá tooredo todas as sessões de cópia Olá para unidade hello.  
  
## <a name="next-steps"></a>Próximas etapas
 
* [Configurar a ferramenta de importação/exportação do azure Olá](storage-import-export-tool-setup-v1.md)   
* [Preparação de discos rígidos para um trabalho de importação](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Revisão do status do trabalho com arquivos de log de cópia](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Reparação de um trabalho de importação](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Reparação de um trabalho de exportação](storage-import-export-tool-repairing-an-export-job-v1.md)
