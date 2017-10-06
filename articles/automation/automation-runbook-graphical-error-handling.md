---
title: "aaaError tratamento em runbooks gráficos de automação do Azure | Microsoft Docs"
description: "Este artigo descreve como lógica em runbooks de automação do Azure gráficas de tratamento de erro de tooimplement."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Tratamento de erros em runbooks gráficos na Automação do Azure

Um tooconsider principal de design do runbook chave é identificar problemas diferentes que pode ter um runbook. Esses problemas podem incluir sucesso, estados de erro esperado e as condições de erro inesperado.

Runbooks deve incluir o tratamento de erros. toovalidate Olá a saída de uma atividade ou manipular um erro com runbooks gráficos, use uma atividade de código do Windows PowerShell, defina a lógica condicional no link de saída de saudação da atividade de saudação ou aplicar outro método.          

Geralmente, se houver um erro não fatal que ocorre com uma atividade de runbook, qualquer atividade que segue é processada, independentemente de erro de saudação. Erro de saudação é provavelmente toogenerate uma exceção, mas próxima atividade de saudação ainda é permitida toorun. Essa é maneira Olá PowerShell é projetado toohandle erros.    

tipos de saudação do PowerShell erros que podem ocorrer durante a execução são finalizando ou não fatal. diferenças de Olá entre os erros de finalização e finalização não são da seguinte maneira:

* **Erro fatal**: um erro grave durante a execução é interrompida comando hello (ou a execução do script) completamente. Os exemplos incluem cmdlets inexistentes, erros de sintaxe que impedem a execução de um cmdlet ou outros erros fatais.

* **Erro não fatal**: um erro não grave que permite a execução toocontinue apesar da falha de saudação. Os exemplos incluem erros operacionais como erros de arquivo não encontrado e problemas de permissões.

Runbooks gráficos foram aprimorados com tratamento de erros de tooinclude Olá recurso de automação do Azure. Agora você pode ativar exceções em erros de não finalização e criar links de erro entre atividades. Esse processo permite que um autor de runbook toocatch erros e gerencie as condições realizadas ou inesperadas.  

## <a name="when-toouse-error-handling"></a>Quando o tratamento de erros toouse

Sempre que houver uma atividade crítica que gera um erro ou exceção, é importante tooprevent Olá próxima atividade no runbook de erro de saudação do processamento e toohandle adequadamente. Isso é particularmente crítico quando seus runbooks dão suporte a uma empresa ou a um processo de operações de serviço.

Para cada atividade que pode gerar um erro, o autor de runbook Olá pode adicionar um link de erro apontando tooany outra atividade.  atividade de destino Olá pode ser de qualquer tipo, incluindo atividades de código, chamar um cmdlet, chamar outro runbook e assim por diante.

Além disso, a atividade de destino Olá também pode ter links de saída. Esses links são links regulares ou erro. Isso significa que o autor de runbook Olá pode implementar lógica complexa de tratamento de erros sem recorrer tooa atividade de código. Olá recomendado prática é toocreate um runbook dedicado de tratamento de erros com funcionalidade comum, mas não é obrigatório. Lógica de tratamento de erros em uma atividade de código do PowerShell não é Olá apenas a opção.  

Por exemplo, considere um runbook que tenta toostart uma VM e instalar um aplicativo. Se hello VM não iniciar corretamente, ele executa duas ações:

1. Ele envia uma notificação sobre esse problema.
2. Ele inicia outro runbook que provisiona automaticamente uma nova VM em vez disso.

Uma solução é toohave um link de erro apontando atividade tooan que identificadores etapa um. Por exemplo, você pode conectar Olá **Write-Warning** cmdlet tooan atividade para a etapa dois, como Olá **AzureRmAutomationRunbook início** cmdlet.

Você também pode generalizar esse comportamento para uso em runbooks muitos colocando essas duas atividades em um runbook de tratamento de erro separada e a seguinte orientação Olá sugerido anteriormente. Antes de chamar esse runbook de tratamento de erros, você pode construir uma mensagem personalizada de dados Olá no runbook original hello e passá-lo como um runbook de tratamento de erros do parâmetro toohello.

## <a name="how-toouse-error-handling"></a>Como o tratamento de erros toouse

Cada atividade tem um parâmetro de configuração que transforma exceções em erros de não finalização. Por padrão, essa configuração é desabilitada. É recomendável que você habilite essa configuração em qualquer atividade onde você deseja toohandle erros.  

Ao habilitar essa configuração, você está garantindo que erros de não finalização e finalização na atividade de saudação são tratados como erros de não finalização e podem ser tratados com um link de erro.  

Depois de configurar essa configuração, você cria uma atividade que trata o erro hello. Se uma atividade produz um erro, Olá, em seguida, a saída de erro links são seguidos e links regulares Olá não são, mesmo se a atividade de saudação produz saída regular também.<br><br> ![Exemplo de link de erro de runbook de automação](media/automation-runbook-graphical-error-handling/error-link-example.png)

Saudação de exemplo a seguir, um runbook recupera uma variável que contém o nome do computador de saudação de uma máquina virtual. Ele tentará toostart Olá VM com a próxima atividade de saudação.<br><br> ![Exemplo de tratamento de erro de runbook de automação](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

Olá **Get-AutomationVariable** atividade e **AzureRmVm início** serão configurado tooconvert tooerrors de exceções.  Se houver problemas ao fazer a saudação inicial ou variável Olá VM e erros são gerados.<br><br> ![Configurações de atividade de tratamento de erros de runbook de automação](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

Links de erro de fluxo desses tooa atividades único **gerenciamento erro** atividade (uma atividade de código). Esta atividade é configurada com uma expressão simple do PowerShell que usa Olá *gerar* toostop de palavra-chave processamento, juntamente com *$Error.Exception.Message* tooget mensagem de saudação que descreve Olá exceção atual.<br><br> ![Exemplo de código de tratamento de erros de runbook de automação](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>Próximas etapas

* toolearn mais sobre links e tipos de link runbooks gráficos, consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md#links-and-workflow).

* toolearn mais sobre a execução do runbook, como trabalhos de runbook toomonitor e outros detalhes técnicos, consulte [acompanhar um trabalho de runbook](automation-runbook-execution.md).
