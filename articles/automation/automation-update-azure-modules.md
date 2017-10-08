---
title: "aaaUpdate Azure módulos na automação do Azure | Microsoft Docs"
description: "Este artigo descreve como você pode atualizar módulos comuns do Azure PowerShell fornecidos por padrão na Automação do Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>Como módulos do PowerShell do Azure tooupdate na automação do Azure

módulos do PowerShell do Azure mais comuns Olá são fornecidos por padrão em cada conta de automação.  atualizações de equipe do Azure Olá Olá regularmente, módulos do Azure para Olá conta de automação fornecemos uma maneira para você tooupdate módulos Olá conta hello quando novas versões estão disponíveis no portal de saudação.  

Porque módulos são atualizados regularmente por grupo de produtos hello, as alterações podem ocorrer com cmdlets de saudação incluído, que pode afetar negativamente seus runbooks dependendo do tipo de saudação de alteração, como renomear um parâmetro ou substituição de um cmdlet inteiramente. tooavoid afetar seus runbooks e hello processos automatizar, é altamente recomendável que você deseja testa e valida antes de continuar.  Se você não tiver uma conta de automação dedicada destinada para essa finalidade, considere a criação de uma forma que você pode testar vários cenários diferentes e permutações durante o desenvolvimento de saudação de seus runbooks, em alterações de tooiterative de adição, como atualização Olá Módulos do PowerShell.  Depois que os resultados de saudação são validados e você aplicou as alterações necessárias, prosseguir com a coordenação de migração de saudação de todos os runbooks que necessária a modificação e executar atualização Olá conforme descrito abaixo em produção.     

## <a name="updating-azure-modules"></a>Atualizando os módulos do Azure

1. Olá módulos folha da sua conta de automação é uma opção chamada **atualização Azure módulos**.  Ela está sempre habilitada.<br><br> ![Opção Atualizar Módulos do Azure na folha Módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Clique em **atualização Azure módulos** e você verá uma notificação de confirmação que pergunta se você quiser toocontinue.<br><br> ![Notificação de Atualizar Módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Clique em **Sim** e começará o processo de atualização de módulo hello.  o processo de atualização Olá leva cerca de saudação do tooupdate 15 a 20 minutos seguintes módulos:

  * As tabelas
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Se os módulos de saudação já estão ativas toodate, processo Olá será concluída em alguns segundos.  Quando o processo de atualização de saudação for concluído, você será notificado.<br><br> ![Status da atualização de Atualizar Módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Automação do Azure usará mais recentes de módulos Olá na sua conta de automação quando um novo trabalho agendado é executado.    

Se você usar os cmdlets desses módulos do PowerShell do Azure no seu toomanage runbooks do Azure recursos, em seguida, você desejará tooperform esse processo de atualização de cada mês ou então tooassure tiver Olá módulos mais recentes.

## <a name="next-steps"></a>Próximas etapas

* toolearn mais informações sobre os módulos de integração e como toocreate módulos personalizados toofurther integrar a automação com outros sistemas, serviços ou soluções, consulte [módulos de integração](automation-integration-modules.md).

* Considere a integração de controle de origem usando [GitHub corporativo](automation-scenario-source-control-integration-with-github-ent.md) ou [do Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally gerenciar e controlar versões do seu portfólio de runbook e a configuração de automação.  
