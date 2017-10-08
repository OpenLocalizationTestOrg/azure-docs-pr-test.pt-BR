---
title: "remoção de aaaAutomate de grupos de recursos | Microsoft Docs"
description: "Versão de fluxo de trabalho do PowerShell de um cenário de automação do Azure, incluindo runbooks tooremove todos os recursos de grupos em sua assinatura."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Cenário da Automação do Azure - automatize a remoção de grupos de recursos
Muitos clientes criam mais de um grupo de recursos. Alguns podem ser usados para gerenciar aplicativos de produção e outros podem ser usados como ambientes de desenvolvimento, teste e preparo. Automatizar a implantação de saudação desses recursos é uma coisa, mas que está sendo toodecommission capaz de um grupo de recursos com um clique de botão de saudação é outra. Você pode simplificar essa tarefa comum de gerenciamento usando a Automação do Azure. Isso é útil se você estiver trabalhando com uma assinatura do Azure que tem um limite de gastos por meio de uma oferta de membro como o MSDN ou Olá programa Microsoft Partner Network Cloud Essentials.

Este cenário se baseia em um runbook do PowerShell e é projetado tooremove um ou mais grupos de recursos que você especificar na sua assinatura. configuração padrão Olá Olá runbook é tootest antes de continuar. Isso garante que não acidentalmente excluir grupo de recursos de saudação antes que você está pronto toocomplete esse procedimento.   

## <a name="getting-hello-scenario"></a>Obtendo o cenário de saudação
Este cenário consiste em um runbook do PowerShell que você pode baixar do hello [Galeria do PowerShell](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). Você também pode importá-lo diretamente do hello [Galeria de Runbook](automation-runbook-gallery.md) em Olá portal do Azure.<br><br>

| Runbook | Descrição |
| --- | --- |
| Remove-ResourceGroup |Remove um ou mais grupos de recursos do Azure e recursos associados de assinatura de saudação. |

<br>
Olá, parâmetros de entrada a seguir é definida para este runbook:

| Parâmetro | Descrição |
| --- | --- |
| NameFilter (Obrigatório) |Especifica um nome filtro toolimit Olá recursos grupos que você pretenda sobre a exclusão. Você pode passar vários valores usando uma lista separada por vírgulas.<br>filtro de saudação não diferencia maiusculas de minúsculas e corresponderá a qualquer grupo de recursos que contém a cadeia de caracteres de saudação. |
| PreviewMode (opcional) |Olá runbook toosee quais grupos de recursos serão excluídos, mas não executa nenhuma ação é executado.<br>saudação padrão é **true** toohelp evitar a exclusão acidental de um ou mais grupos de recursos passado toohello runbook. |

## <a name="install-and-configure-this-scenario"></a>Instalar e configurar esse cenário
### <a name="prerequisites"></a>Pré-requisitos
Este runbook autentica usando Olá [conta executar como do Azure](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-hello-runbooks"></a>Instalar e publicar runbooks Olá
Depois de baixar o runbook hello, você pode importá-lo usando o procedimento Olá [importar runbook procedimentos](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Publica o runbook Olá depois que ele foi importado com êxito para a sua conta de automação.

## <a name="using-hello-runbook"></a>Usando o runbook Olá
Olá seguinte irá orientá-lo por meio da execução de saudação desse runbook e ajuda que você se familiarize com como ele funciona. Você só testará Olá runbook neste exemplo, não realmente excluir o grupo de recursos de saudação.  

1. Em Olá portal do Azure, abra sua conta de automação e clique em **Runbooks**.
2. Selecione Olá **remover ResourceGroup** runbook e clique em **iniciar**.
3. Quando você inicia o runbook hello, Olá **iniciar Runbook** folha é aberto e você pode configurar os parâmetros de saudação. Digite nomes de saudação de grupos de recursos em sua assinatura que você pode usar para teste e não causará nenhum dano se excluído acidentalmente.<br> ![Parâmetros Remove-ResouceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Certifique-se de **Previewmode** está definido muito**true** tooavoid excluindo Olá selecionada de grupos de recursos.  **Observação** que este runbook não removerá o grupo de recursos de saudação que contém a conta de automação de saudação que está executando este runbook.  
   >
   >
4. Depois de configurar todos os valores de parâmetro hello, clique em **Okey**, e o runbook hello será enfileirado para execução.  

detalhes de saudação tooview de saudação **remover ResourceGroup** trabalho de runbook no hello portal do Azure, selecione **trabalhos** em Olá runbook. parâmetros de entrada do Hello trabalho Resumo exibe hello e saída de hello fluxo além toogeneral informações sobre o trabalho de saudação e todas as exceções que ocorreram.<br> ![Status de trabalho do runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Olá **resumo do trabalho** inclui mensagens de fluxos de saída, aviso e erro hello. Selecione **saída** tooview detalhadas resultados da execução de runbook hello.<br> ![Resultados da saída do runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>Próximas etapas
* tooget começou a criar seu próprio runbook, consulte [criar ou importar um runbook na automação do Azure](automation-creating-importing-runbook.md).
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md).
