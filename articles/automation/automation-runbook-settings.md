---
title: "configurações de aaaRunbook | Microsoft Docs"
description: "Descreve as definições de configuração de saudação para um runbook na automação do Azure e como toochange-las usando Olá Portal de gerenciamento do Azure e o Windows PowerShell."
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
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="e02f5-103">Configurações de runbook</span><span class="sxs-lookup"><span data-stu-id="e02f5-103">Runbook settings</span></span>
<span data-ttu-id="e02f5-104">Cada runbook na automação do Azure tem várias configurações que ajudam a toobe identificado e toochange seu comportamento de registro em log.</span><span class="sxs-lookup"><span data-stu-id="e02f5-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="e02f5-105">Cada uma dessas configurações é descrita abaixo seguida de procedimentos sobre como toomodify-los.</span><span class="sxs-lookup"><span data-stu-id="e02f5-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="e02f5-106">Configurações</span><span class="sxs-lookup"><span data-stu-id="e02f5-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="e02f5-107">Nome e descrição</span><span class="sxs-lookup"><span data-stu-id="e02f5-107">Name and description</span></span>
<span data-ttu-id="e02f5-108">Você não pode alterar o nome de saudação de um runbook após ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="e02f5-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="e02f5-109">Olá descrição é opcional e pode ser too512 caracteres.</span><span class="sxs-lookup"><span data-stu-id="e02f5-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="e02f5-110">Marcas</span><span class="sxs-lookup"><span data-stu-id="e02f5-110">Tags</span></span>
<span data-ttu-id="e02f5-111">As marcas permitem que você tooassign diferentes palavras e frases toohelp identificam um runbook.</span><span class="sxs-lookup"><span data-stu-id="e02f5-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="e02f5-112">Por exemplo, quando você envia um runbook toohello [Galeria do PowerShell](https://www.powershellgallery.com/), você especificar marcas tooidentify quais categorias Olá runbook deve ser listado nas.</span><span class="sxs-lookup"><span data-stu-id="e02f5-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="e02f5-113">Você pode especificar vários rótulos para um runbook separando-os com vírgulas.</span><span class="sxs-lookup"><span data-stu-id="e02f5-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="e02f5-114">Registro em log</span><span class="sxs-lookup"><span data-stu-id="e02f5-114">Logging</span></span>
<span data-ttu-id="e02f5-115">Por padrão, os registros detalhado e andamento não são gravados toojob histórico.</span><span class="sxs-lookup"><span data-stu-id="e02f5-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="e02f5-116">Você pode alterar configurações de saudação para um determinado runbook toolog esses registros.</span><span class="sxs-lookup"><span data-stu-id="e02f5-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="e02f5-117">Para saber mais sobre esses registros, confira [Saída de Runbook e Mensagens](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="e02f5-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="e02f5-118">Alterando as configurações de runbook</span><span class="sxs-lookup"><span data-stu-id="e02f5-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="e02f5-119">Alterando as configurações de runbook com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e02f5-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="e02f5-120">Você pode alterar as configurações de um runbook no portal do Azure de saudação do hello **configurações** folha Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="e02f5-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="e02f5-121">No portal do Azure de Olá, selecione **automação** e, em seguida, clique em nome de saudação de uma conta de automação.</span><span class="sxs-lookup"><span data-stu-id="e02f5-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="e02f5-122">Selecione Olá **Runbooks** guia.</span><span class="sxs-lookup"><span data-stu-id="e02f5-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="e02f5-123">Clique em nome de saudação de um runbook e são toohello direcionado folha de configurações de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="e02f5-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="e02f5-124">Aqui você pode especificar ou modificar marcas, Olá descrição de runbook, configurar o log e configurações de rastreamento e toohelp de ferramentas de suporte a resolver problemas de acesso.</span><span class="sxs-lookup"><span data-stu-id="e02f5-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="e02f5-125">Alterando as configurações de runbook com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e02f5-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="e02f5-126">Você pode usar o hello [AzureRmAutomationRunbook conjunto](https://msdn.microsoft.com/library/mt603786.aspx) configurações de saudação do cmdlet toochange de um runbook.</span><span class="sxs-lookup"><span data-stu-id="e02f5-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="e02f5-127">Se você quiser toospecify várias marcas, você pode fornecer uma matriz ou uma única cadeia de caracteres com parâmetro de marcas de toohello de valores delimitados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="e02f5-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="e02f5-128">Você pode obter as marcas atual com Olá Olá [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="e02f5-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="e02f5-129">Olá comandos de exemplo a seguir mostra como tooset Olá propriedades de um runbook.</span><span class="sxs-lookup"><span data-stu-id="e02f5-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="e02f5-130">Este exemplo adiciona três marcas existentes toohello marcas e especifica que registros detalhados devem ser registradas em log.</span><span class="sxs-lookup"><span data-stu-id="e02f5-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="e02f5-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e02f5-131">Next steps</span></span>
* <span data-ttu-id="e02f5-132">toolearn como mensagens de saída e o erro toocreate e recuperar de runbooks, consulte [mensagens e saída de Runbook](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="e02f5-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="e02f5-133">toounderstand como tooadd um runbook já desenvolvido pela comunidade hello ou outras fonte ou toocreate seu próprios runbook consulte [criar ou importar um Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="e02f5-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

