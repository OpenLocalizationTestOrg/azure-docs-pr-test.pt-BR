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
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="9f0b3-103">Olá, ferramenta de importação/exportação do Azure de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="9f0b3-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="9f0b3-104">Olá, ferramenta de importação/exportação do Microsoft Azure retorna mensagens de erro se encontrar problemas.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="9f0b3-105">Este tópico lista alguns problemas comuns que os usuários poderão enfrentar.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="9f0b3-106">Quando uma sessão de cópia falha o que devo fazer?</span><span class="sxs-lookup"><span data-stu-id="9f0b3-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="9f0b3-107">Quando uma sessão de cópia falha, há duas opções:</span><span class="sxs-lookup"><span data-stu-id="9f0b3-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="9f0b3-108">Se o erro de saudação for reproduzível, por exemplo, se o compartilhamento de rede Olá estava offline por um curto período e agora está novamente online, você pode retomar a sessão de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="9f0b3-109">Se o erro Olá não for reproduzível, por exemplo, se você especificou o diretório do arquivo de origem errado Olá nos parâmetros de linha de comando de saudação, será necessário tooabort sessão de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="9f0b3-110">Consulte [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparando os discos rígidos para um trabalho de importação) para obter mais informações sobre como continuar e anular sessões de cópia.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="9f0b3-111">Não consigo retomar nem anular uma sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="9f0b3-112">Se a sessão de cópia Olá for Olá primeira sessão de cópia para uma unidade, mensagem de saudação do erro deve indicar: "hello primeira sessão de cópia não pode ser retomada ou anulada."</span><span class="sxs-lookup"><span data-stu-id="9f0b3-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="9f0b3-113">Nesse caso, você pode excluir o arquivo de diário antigo hello e execute novamente o comando hello.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="9f0b3-114">Se uma sessão de cópia não é hello um primeiro para uma unidade, ele pode sempre ser retomado ou anulado.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="9f0b3-115">Perdi o arquivo de diário hello, ainda posso criar trabalho Olá?</span><span class="sxs-lookup"><span data-stu-id="9f0b3-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="9f0b3-116">arquivo de diário Olá para uma unidade contém informações completas de saudação de cópia de unidade de toothis de dados, e é necessário tooadd mais arquivos toohello de unidade e será usado toocreate um trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="9f0b3-117">Se o arquivo de diário Olá for perdido, você terá tooredo todas as sessões de cópia Olá para unidade hello.</span><span class="sxs-lookup"><span data-stu-id="9f0b3-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="9f0b3-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f0b3-118">Next steps</span></span>
 
* [<span data-ttu-id="9f0b3-119">Configurar a ferramenta de importação/exportação do azure Olá</span><span class="sxs-lookup"><span data-stu-id="9f0b3-119">Setting up hello azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="9f0b3-120">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="9f0b3-120">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="9f0b3-121">Revisão do status do trabalho com arquivos de log de cópia</span><span class="sxs-lookup"><span data-stu-id="9f0b3-121">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="9f0b3-122">Reparação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="9f0b3-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="9f0b3-123">Reparação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="9f0b3-123">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
