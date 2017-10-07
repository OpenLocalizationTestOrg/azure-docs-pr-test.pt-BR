---
title: "aaaManage Cofre de chaves do Azure usando a automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automação do Azure pode ser usado toomanage Cofre de chaves do Azure."
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
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="48a0e-103">Gerenciar o Cofre da Chave do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="48a0e-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="48a0e-104">Este guia apresentará toohello serviço de automação do Azure e como ela pode ser usado toosimplify gerenciamento de suas chaves e segredos no cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="48a0e-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="48a0e-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="48a0e-105">What is Azure Automation?</span></span>
<span data-ttu-id="48a0e-106">[Automação do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processos e por uma configuração de estado desejada.</span><span class="sxs-lookup"><span data-stu-id="48a0e-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="48a0e-107">Usando a automação do Azure, as tarefas manuais repetidas, demoradas e propensas a erros podem ser toovalue de tempo para a sua organização, eficiência e confiabilidade de tooincrease automatizada.</span><span class="sxs-lookup"><span data-stu-id="48a0e-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="48a0e-108">Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="48a0e-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="48a0e-109">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="48a0e-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="48a0e-110">Reduzir a sobrecarga operacional e liberar IT e DevOps equipe toofocus no trabalho que adiciona valor comercial, movendo o toobe de tarefas de gerenciamento de nuvem executados automaticamente pela automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="48a0e-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="48a0e-111">Como a Automação do Azure pode ajudar a gerenciar o cofre da chave do Azure?</span><span class="sxs-lookup"><span data-stu-id="48a0e-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="48a0e-112">Cofre de chaves podem ser gerenciado na automação do Azure usando Olá [cmdlets do Cofre de chaves AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) e [cmdlets do Cofre de chaves clássico do Azure](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="48a0e-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="48a0e-113">Olá módulo do Azure para gerenciar o Cofre de chaves clássico está disponível automaticamente na automação do Azure, e você pode importar Olá [AzureRM KeyVault módulo](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) na automação do Azure, para que você possa executar muitas gerenciamento seu Cofre de chaves tarefas no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="48a0e-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="48a0e-114">Esses cmdlets na automação do Azure com os cmdlets de saudação para outros serviços do Azure, as tarefas complexas tooautomate também podem ser emparelhados por serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="48a0e-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="48a0e-115">Com hello Azure Key Vault cmdlets, você pode executar essas tarefas, entre outros:</span><span class="sxs-lookup"><span data-stu-id="48a0e-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="48a0e-116">Criar e configurar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="48a0e-116">Create and configure a key vault</span></span>
* <span data-ttu-id="48a0e-117">Criar ou importar uma chave</span><span class="sxs-lookup"><span data-stu-id="48a0e-117">Create or import a key</span></span>
* <span data-ttu-id="48a0e-118">Criar ou atualizar um segredo</span><span class="sxs-lookup"><span data-stu-id="48a0e-118">Create or update a secret</span></span>
* <span data-ttu-id="48a0e-119">Atualizar os atributos de uma chave</span><span class="sxs-lookup"><span data-stu-id="48a0e-119">Update attributes of a key</span></span>
* <span data-ttu-id="48a0e-120">Obter uma chave ou um segredo</span><span class="sxs-lookup"><span data-stu-id="48a0e-120">Get a key or secret</span></span>
* <span data-ttu-id="48a0e-121">Excluir uma chave ou um segredo</span><span class="sxs-lookup"><span data-stu-id="48a0e-121">Delete a key or secret</span></span>

<span data-ttu-id="48a0e-122">Aqui estão alguns exemplos de uso do PowerShell toomanage Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="48a0e-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="48a0e-123">Cofre da Chave do Azure - passo a passo</span><span class="sxs-lookup"><span data-stu-id="48a0e-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="48a0e-124">Configurando um Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="48a0e-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="48a0e-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48a0e-125">Next steps</span></span>
<span data-ttu-id="48a0e-126">Agora que você aprendeu as Noções básicas de saudação de automação do Azure e como ela pode ser usado toomanage Cofre de chaves do Azure, siga essas toolearn links mais informações sobre a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="48a0e-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="48a0e-127">Consulte Olá automação do Azure [Tutorial de Introdução](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="48a0e-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="48a0e-128">Consulte Olá [scripts do PowerShell do Azure Key Vault](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="48a0e-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

