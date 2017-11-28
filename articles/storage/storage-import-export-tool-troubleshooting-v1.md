---
title: "Solucionando problemas da Ferramenta de Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba mais sobre alguns dos problemas comuns enfrentados ao usar a Ferramenta de Importação/Exportação do Azure e como lidar com eles."
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
ms.openlocfilehash: 43b5d5a57df6bdda57a31ff0330ec6eff7aa732c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-azure-importexport-tool"></a><span data-ttu-id="1b26f-103">Solução de problemas da Ferramenta de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="1b26f-103">Troubleshooting the Azure Import/Export Tool</span></span>
<span data-ttu-id="1b26f-104">A Ferramenta de Importação/Exportação do Microsoft Azure retorna mensagens de erro em caso de problemas.</span><span class="sxs-lookup"><span data-stu-id="1b26f-104">The Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="1b26f-105">Este tópico lista alguns problemas comuns que os usuários poderão enfrentar.</span><span class="sxs-lookup"><span data-stu-id="1b26f-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="1b26f-106">Quando uma sessão de cópia falha o que devo fazer?</span><span class="sxs-lookup"><span data-stu-id="1b26f-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="1b26f-107">Quando uma sessão de cópia falha, há duas opções:</span><span class="sxs-lookup"><span data-stu-id="1b26f-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="1b26f-108">Se o erro for com nova tentativa, por exemplo, se o compartilhamento de rede ficou offline por um curto período e agora está online novamente, será possível retomar a sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="1b26f-108">If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session.</span></span> <span data-ttu-id="1b26f-109">Se o erro for sem nova tentativa, por exemplo, se você especificou o diretório do arquivo de origem incorreto nos parâmetros de linha de comando, você precisará anular a sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="1b26f-109">If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session.</span></span> <span data-ttu-id="1b26f-110">Consulte [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparando os discos rígidos para um trabalho de importação) para obter mais informações sobre como continuar e anular sessões de cópia.</span><span class="sxs-lookup"><span data-stu-id="1b26f-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="1b26f-111">Não consigo retomar nem anular uma sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="1b26f-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="1b26f-112">Se a sessão de cópia for a primeira sessão de cópia de uma unidade, a mensagem de erro deverá indicar: “A primeira sessão de cópia não pode ser continuada nem anulada”.</span><span class="sxs-lookup"><span data-stu-id="1b26f-112">If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="1b26f-113">Nesse caso, é possível excluir o arquivo de diário antigo e executar o comando novamente.</span><span class="sxs-lookup"><span data-stu-id="1b26f-113">In this case, you can delete the old journal file and rerun the command.</span></span>  
  
 <span data-ttu-id="1b26f-114">Se uma sessão de cópia não for a primeira de uma unidade, ela poderá sempre ser continuada ou anulada.</span><span class="sxs-lookup"><span data-stu-id="1b26f-114">If a copy session is not the first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-the-journal-file-can-i-still-create-the-job"></a><span data-ttu-id="1b26f-115">Perdi o arquivo de diário. Ainda posso criar o trabalho?</span><span class="sxs-lookup"><span data-stu-id="1b26f-115">I lost the journal file, can I still create the job?</span></span>  
 <span data-ttu-id="1b26f-116">O arquivo de diário de uma unidade contém as informações completas da cópia de dados para essa unidade. Ele é necessário para adicionar mais arquivos à unidade e será usado para criar um trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="1b26f-116">The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job.</span></span> <span data-ttu-id="1b26f-117">Em caso de perda do arquivo de diário, você precisará refazer todas as sessões de cópia da unidade.</span><span class="sxs-lookup"><span data-stu-id="1b26f-117">If the journal file is lost, you will have to redo all the copy sessions for the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1b26f-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b26f-118">Next steps</span></span>
 
* [<span data-ttu-id="1b26f-119">Configurando a Ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="1b26f-119">Setting up the azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="1b26f-120">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="1b26f-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="1b26f-121">Revisão do status do trabalho com arquivos de log de cópia</span><span class="sxs-lookup"><span data-stu-id="1b26f-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="1b26f-122">Reparação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="1b26f-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="1b26f-123">Reparação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="1b26f-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
