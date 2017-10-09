---
title: "aaaManage armazenamento do Azure usando a automação do Azure"
description: "Saiba mais sobre como Olá serviço de automação do Azure pode ser usado toomanage armazenamento do Azure em grande escala."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 15e34128ffb0ba3315b5260442f628b5978c5197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="8cf2d-103">Gerenciando o armazenamento do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="8cf2d-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="8cf2d-104">Este guia apresentará toohello serviço de automação do Azure e como ela pode ser usado toosimplify gerenciamento de seus blobs, tabelas e filas do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="8cf2d-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="8cf2d-105">What is Azure Automation?</span></span>
<span data-ttu-id="8cf2d-106">[Automação do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="8cf2d-107">Usando a automação do Azure, de longa duração, manual, propensas a erros e frequentemente repetido tarefas podem ser automatizados tooincrease confiabilidade e eficiência e reduzir o tempo toovalue para sua organização.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="8cf2d-108">Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades que sua organização cresce.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="8cf2d-109">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="8cf2d-110">Reduzir a sobrecarga operacional e liberar IT / DevOps equipe toofocus no trabalho que adiciona valor comercial, movendo o toobe de tarefas de gerenciamento de nuvem executados automaticamente pela automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="8cf2d-111">Como a Automação do Azure ajuda a gerenciar o Armazenamento do Azure?</span><span class="sxs-lookup"><span data-stu-id="8cf2d-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="8cf2d-112">Armazenamento do Azure pode ser gerenciado na automação do Azure usando cmdlets do PowerShell Olá que estão disponíveis em [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="8cf2d-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="8cf2d-113">Automação do Azure tem esses cmdlets do PowerShell de armazenamento disponíveis sem necessidade de hello, para que você poderá executar todo o blob, tabela e tarefas de gerenciamento de fila no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="8cf2d-114">Esses cmdlets na automação do Azure com os cmdlets de saudação para outros serviços do Azure, as tarefas complexas tooautomate também podem ser emparelhados por serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="8cf2d-115">Olá [Galeria de runbook de automação do Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contém uma variedade de produtos equipe e comunidade runbooks tooget iniciado automatizar o gerenciamento de armazenamento do Azure, outros serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="8cf2d-116">A galeria de runbooks inclui:</span><span class="sxs-lookup"><span data-stu-id="8cf2d-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="8cf2d-117">Remover os Blobs de Armazenamento do Azure que têm determinados dias de idade usando o serviço de automação</span><span class="sxs-lookup"><span data-stu-id="8cf2d-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="8cf2d-118">Baixar um Blob do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8cf2d-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="8cf2d-119">Fazer backup de todos os discos para uma única VM do Azure ou para todas as VMs em um Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="8cf2d-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="8cf2d-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8cf2d-120">Next Steps</span></span>
<span data-ttu-id="8cf2d-121">Agora que você aprendeu as Noções básicas de saudação de automação do Azure e como ela pode ser usado toomanage blobs de armazenamento do Azure, tabelas e filas, siga essas toolearn links mais informações sobre a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf2d-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="8cf2d-122">Consulte o tutorial de automação do Azure Olá [criar ou importar um runbook na automação do Azure](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="8cf2d-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

