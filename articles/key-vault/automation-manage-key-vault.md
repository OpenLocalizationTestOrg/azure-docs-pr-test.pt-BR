---
title: "Gerenciar o Cofre de Chaves do Azure usando a Automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como o serviço de Automação do Azure pode ser usado para gerenciar o Cofre da Chave do Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="47fe3-103">Gerenciar o Cofre da Chave do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="47fe3-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="47fe3-104">Este guia apresentará a você o serviço de Automação do Azure e como ele pode ser usado para simplificar o gerenciamento de suas chaves e segredos no cofre da chave do Azure.</span><span class="sxs-lookup"><span data-stu-id="47fe3-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="47fe3-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="47fe3-105">What is Azure Automation?</span></span>
<span data-ttu-id="47fe3-106">[Automação do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processos e por uma configuração de estado desejada.</span><span class="sxs-lookup"><span data-stu-id="47fe3-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="47fe3-107">Com o uso da Automação do Azure, as tarefas manuais, repetidas, de execução longa e propensas a erros podem ser automatizadas para aumentar a confiabilidade, a eficiência e o tempo de retorno para sua organização.</span><span class="sxs-lookup"><span data-stu-id="47fe3-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="47fe3-108">A Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que é dimensionado para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="47fe3-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="47fe3-109">Na Automação do Azure, processos podem ser inicializados manualmente, por sistemas de terceiros ou em intervalos agendados para que as tarefas acontecem exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="47fe3-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="47fe3-110">Reduza o custo operacional e libere a equipe de TI e DevOps para se concentrar no trabalho que agrega valor de negócios, transferindo as tarefas de gerenciamento de nuvem para serem executadas automaticamente pela Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="47fe3-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="47fe3-111">Como a Automação do Azure pode ajudar a gerenciar o cofre da chave do Azure?</span><span class="sxs-lookup"><span data-stu-id="47fe3-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="47fe3-112">O Cofre de Chaves pode ser gerenciado na Automação do Azure usando os [cmdlets do Cofre de Chave AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) e os [cmdlets do Cofre de Chaves Clássico do Azure](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="47fe3-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="47fe3-113">O módulo do Azure para gerenciar o Cofre da Chave clássico está disponível automaticamente na Automação do Azure, e você pode importar o [módulo AzureRM-KeyVault](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) para a Automação do Azure, para executar muitas de suas tarefas de gerenciamento do Cofre da Chave dentro do serviço.</span><span class="sxs-lookup"><span data-stu-id="47fe3-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="47fe3-114">Você também pode combinar esses cmdlets na Automação do Azure com os cmdlets para outros serviços do Azure, para automatizar tarefas complexas nos serviços do Azure e sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="47fe3-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="47fe3-115">Com os cmdlets do Cofre de Chaves do Azure, você pode executar as seguintes tarefas, entre outras:</span><span class="sxs-lookup"><span data-stu-id="47fe3-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="47fe3-116">Criar e configurar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="47fe3-116">Create and configure a key vault</span></span>
* <span data-ttu-id="47fe3-117">Criar ou importar uma chave</span><span class="sxs-lookup"><span data-stu-id="47fe3-117">Create or import a key</span></span>
* <span data-ttu-id="47fe3-118">Criar ou atualizar um segredo</span><span class="sxs-lookup"><span data-stu-id="47fe3-118">Create or update a secret</span></span>
* <span data-ttu-id="47fe3-119">Atualizar os atributos de uma chave</span><span class="sxs-lookup"><span data-stu-id="47fe3-119">Update attributes of a key</span></span>
* <span data-ttu-id="47fe3-120">Obter uma chave ou um segredo</span><span class="sxs-lookup"><span data-stu-id="47fe3-120">Get a key or secret</span></span>
* <span data-ttu-id="47fe3-121">Excluir uma chave ou um segredo</span><span class="sxs-lookup"><span data-stu-id="47fe3-121">Delete a key or secret</span></span>

<span data-ttu-id="47fe3-122">Veja alguns exemplos de uso do PowerShell para gerenciar o Cofre da Chave:</span><span class="sxs-lookup"><span data-stu-id="47fe3-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="47fe3-123">Cofre da Chave do Azure - passo a passo</span><span class="sxs-lookup"><span data-stu-id="47fe3-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="47fe3-124">Configurando um Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="47fe3-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="47fe3-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47fe3-125">Next steps</span></span>
<span data-ttu-id="47fe3-126">Agora que você aprendeu os fundamentos de Automação do Azure e como ela pode ser usada para gerenciar o Cofre da Chave do Azure, siga estes links para obter mais informações sobre a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="47fe3-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="47fe3-127">Consulte o [Tutorial de introdução](../automation/automation-first-runbook-graphical.md)da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="47fe3-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="47fe3-128">Consulte os [scripts do PowerShell do Cofre da Chave do Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="47fe3-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

