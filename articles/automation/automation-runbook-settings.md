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
# <a name="runbook-settings"></a>Configurações de runbook
Cada runbook na automação do Azure tem várias configurações que ajudam a toobe identificado e toochange seu comportamento de registro em log. Cada uma dessas configurações é descrita abaixo seguida de procedimentos sobre como toomodify-los.

## <a name="settings"></a>Configurações
### <a name="name-and-description"></a>Nome e descrição
Você não pode alterar o nome de saudação de um runbook após ele ter sido criado. Olá descrição é opcional e pode ser too512 caracteres.

### <a name="tags"></a>Marcas
As marcas permitem que você tooassign diferentes palavras e frases toohelp identificam um runbook. Por exemplo, quando você envia um runbook toohello [Galeria do PowerShell](https://www.powershellgallery.com/), você especificar marcas tooidentify quais categorias Olá runbook deve ser listado nas. Você pode especificar vários rótulos para um runbook separando-os com vírgulas.

### <a name="logging"></a>Registro em log
Por padrão, os registros detalhado e andamento não são gravados toojob histórico. Você pode alterar configurações de saudação para um determinado runbook toolog esses registros. Para saber mais sobre esses registros, confira [Saída de Runbook e Mensagens](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Alterando as configurações de runbook

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>Alterando as configurações de runbook com hello portal do Azure
Você pode alterar as configurações de um runbook no portal do Azure de saudação do hello **configurações** folha Olá runbook.

1. No portal do Azure de Olá, selecione **automação** e, em seguida, clique em nome de saudação de uma conta de automação.
2. Selecione Olá **Runbooks** guia.
3. Clique em nome de saudação de um runbook e são toohello direcionado folha de configurações de runbook hello. Aqui você pode especificar ou modificar marcas, Olá descrição de runbook, configurar o log e configurações de rastreamento e toohelp de ferramentas de suporte a resolver problemas de acesso.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Alterando as configurações de runbook com o Windows PowerShell
Você pode usar o hello [AzureRmAutomationRunbook conjunto](https://msdn.microsoft.com/library/mt603786.aspx) configurações de saudação do cmdlet toochange de um runbook. Se você quiser toospecify várias marcas, você pode fornecer uma matriz ou uma única cadeia de caracteres com parâmetro de marcas de toohello de valores delimitados por vírgulas. Você pode obter as marcas atual com Olá Olá [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).

Olá comandos de exemplo a seguir mostra como tooset Olá propriedades de um runbook. Este exemplo adiciona três marcas existentes toohello marcas e especifica que registros detalhados devem ser registradas em log.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Próximas etapas
* toolearn como mensagens de saída e o erro toocreate e recuperar de runbooks, consulte [mensagens e saída de Runbook](automation-runbook-output-and-messages.md) 
* toounderstand como tooadd um runbook já desenvolvido pela comunidade hello ou outras fonte ou toocreate seu próprios runbook consulte [criar ou importar um Runbook](automation-creating-importing-runbook.md) 

