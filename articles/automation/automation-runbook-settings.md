---
title: "Configurações de runbook | Microsoft Docs"
description: "Descreve as definições de configuração de um runbook na Automação do Azure e como alterá-las usando o Portal de Gerenciamento do Azure e o Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="612bf-103">Configurações de runbook</span><span class="sxs-lookup"><span data-stu-id="612bf-103">Runbook settings</span></span>
<span data-ttu-id="612bf-104">Cada runbook na Automação do Azure tem várias configurações que ajudam a identificá-lo e a alterar seu comportamento de log.</span><span class="sxs-lookup"><span data-stu-id="612bf-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="612bf-105">Cada uma dessas configurações é descrita abaixo seguida de procedimentos sobre como modificá-las.</span><span class="sxs-lookup"><span data-stu-id="612bf-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="612bf-106">Configurações</span><span class="sxs-lookup"><span data-stu-id="612bf-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="612bf-107">Nome e descrição</span><span class="sxs-lookup"><span data-stu-id="612bf-107">Name and description</span></span>
<span data-ttu-id="612bf-108">Você não pode alterar o nome de um runbook após ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="612bf-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="612bf-109">A descrição é opcional e pode ter até 512 caracteres.</span><span class="sxs-lookup"><span data-stu-id="612bf-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="612bf-110">Marcas</span><span class="sxs-lookup"><span data-stu-id="612bf-110">Tags</span></span>
<span data-ttu-id="612bf-111">Os rótulos permitem que você atribua diferentes palavras e frases para ajudar a identificar um runbook.</span><span class="sxs-lookup"><span data-stu-id="612bf-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="612bf-112">Por exemplo, quando você envia um runbook para a [Galeria do PowerShell](https://www.powershellgallery.com/), também define rótulos específicos para identificar em quais categorias o runbook deve estar listado.</span><span class="sxs-lookup"><span data-stu-id="612bf-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="612bf-113">Você pode especificar vários rótulos para um runbook separando-os com vírgulas.</span><span class="sxs-lookup"><span data-stu-id="612bf-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="612bf-114">Registro em log</span><span class="sxs-lookup"><span data-stu-id="612bf-114">Logging</span></span>
<span data-ttu-id="612bf-115">Por padrão, os registros Detalhado e Progresso não são gravados no histórico do trabalho.</span><span class="sxs-lookup"><span data-stu-id="612bf-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="612bf-116">Você pode alterar as configurações de um runbook específico para registrar logs.</span><span class="sxs-lookup"><span data-stu-id="612bf-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="612bf-117">Para saber mais sobre esses registros, confira [Saída de Runbook e Mensagens](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="612bf-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="612bf-118">Alterando as configurações de runbook</span><span class="sxs-lookup"><span data-stu-id="612bf-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="612bf-119">Alterando as configurações de runbook com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="612bf-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="612bf-120">Você pode alterar as configurações de um runbook no portal do Azure na folha **Configurações** para o runbook.</span><span class="sxs-lookup"><span data-stu-id="612bf-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="612bf-121">No portal do Azure, selecione **Automação** e clique no nome de uma conta de automação.</span><span class="sxs-lookup"><span data-stu-id="612bf-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="612bf-122">Selecione a guia **Runbooks** .</span><span class="sxs-lookup"><span data-stu-id="612bf-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="612bf-123">Clique no nome de um runbook e você será direcionado para a folha de configurações do runbook.</span><span class="sxs-lookup"><span data-stu-id="612bf-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="612bf-124">Aqui, você pode especificar ou modificar marcas e a descrição do runbook, configurar definições de rastreamento e registro em log e acessar ferramentas de suporte para ajudar a resolver problemas.</span><span class="sxs-lookup"><span data-stu-id="612bf-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="612bf-125">Alterando as configurações de runbook com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="612bf-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="612bf-126">Você pode usar o cmdlet [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) para alterar as configurações de um runbook.</span><span class="sxs-lookup"><span data-stu-id="612bf-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="612bf-127">Se você quiser especificar várias marcas, pode fornecer uma matriz ou uma única cadeia de caracteres com valores delimitados por vírgula para o parâmetro dos Rótulos.</span><span class="sxs-lookup"><span data-stu-id="612bf-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="612bf-128">Você pode obter as marcas atuais com o [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="612bf-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="612bf-129">Os comandos de exemplo a seguir mostram como definir as propriedades de um runbook.</span><span class="sxs-lookup"><span data-stu-id="612bf-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="612bf-130">Este exemplo adiciona três rótulos aos rótulos existentes e especifica que registros detalhados devem ser registrados em log.</span><span class="sxs-lookup"><span data-stu-id="612bf-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="612bf-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="612bf-131">Next steps</span></span>
* <span data-ttu-id="612bf-132">Para aprender a criar e recuperar mensagens de erro e de saída de runbooks, confira [Saída e mensagens de Runbook](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="612bf-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="612bf-133">Para entender como adicionar um runbook que já foi desenvolvido pela comunidade ou de outra fonte, ou criar seu próprio runbook, confira [Criando ou importando um runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="612bf-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

