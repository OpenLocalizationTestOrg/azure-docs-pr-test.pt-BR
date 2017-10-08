---
title: "Visão geral de DSC de automação de aaaAzure | Microsoft Docs"
description: "Uma visão geral da DSC (Configuração do Estado Desejado) da Automação do Azure, seus termos e problemas conhecidos"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell dsc, configuração de estado desejada, powershell dsc azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Visão geral do DSC da Automação do Azure

DSC de automação do Azure é um serviço do Azure que permite que você toowrite, gerenciar e compilar a configuração de estado desejado (DSC) da PowerShell [configurações](https://msdn.microsoft.com/powershell/dsc/configurations), importar [recursos DSC](https://msdn.microsoft.com/powershell/dsc/resources)e atribuir nós de tootarget de configurações, todos na nuvem hello.

## <a name="why-use-azure-automation-dsc"></a>Por que usar o DSC de Automação do Azure

O DSC de automação do Azure oferece várias vantagens a usar o DSC fora do Azure.

### <a name="built-in-pull-server"></a>Servidor de pull interno

Automação do Azure fornece um [servidor de pull de DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) para que nós de destino recebem automaticamente as configurações, está de acordo com o estado de toohello desejado e relatar sobre sua conformidade.
servidor de pull internos de saudação na automação do Azure elimina Olá necessidade tooset backup e manter seu próprio servidor de pull.
Automação do Azure pode máquinas de Windows ou Linux físicas ou virtuais, na nuvem de saudação ou no local de destino.

### <a name="management-of-all-your-dsc-artifacts"></a>Gerenciamento de todos os seus artefatos de DSC

DSC de automação do Azure coloca Olá a mesma camada de gerenciamento muito[configuração de estado desejado do PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) como a automação do Azure oferece para o script do PowerShell.

De saudação portal do Azure, ou do PowerShell, você pode gerenciar todos os seus DSC configurações, recursos e nós de destino.

![Captura de tela da folha de automação do Azure Olá](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Importar dados de relatórios para o Log Analytics

Nós que são gerenciados com DSC de automação do Azure envio detalhada status dados toohello pull internos servidor de relatório.
Você pode configurar o DSC de automação do Azure toosend este espaço de trabalho de análise de logs do Microsoft Operations Management Suite (OMS) de tooyour de dados.
toolearn como toosend DSC status dados tooyour espaço de trabalho de análise de Log, consulte [Forward Azure DSC de automação reporting dados tooOMS análise de Log](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Vídeo de introdução

Preferir assistir tooreading? Dê uma olhada nos Olá seguindo o vídeo de maio de 2015, quando DSC de automação do Azure foi anunciada pela primeira vez.

>[!NOTE]
>Enquanto Olá conceitos e ciclo de vida discutidos neste vídeo são corretos, DSC de automação do Azure avançou muito desde que este vídeo foi gravado.
>Ele agora está disponível, tem uma interface de usuário muito mais amplo em Olá portal do Azure e oferece suporte a vários recursos adicionais.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Próximas etapas

* toolearn como tooonboard toobe de nós gerenciados com DSC de automação do Azure, consulte [máquinas de integração para o gerenciamento de DSC de automação do Azure](automation-dsc-onboarding.md)
* tooget iniciado usando a DSC de automação do Azure, consulte [guia de Introdução ao DSC de automação do Azure](automation-dsc-getting-started.md)
* toolearn sobre configurações de DSC de compilação para que você possa atribuir tootarget nós, consulte [compilando configurações no DSC de automação do Azure](automation-dsc-compile.md)
* Para referência de cmdlet do PowerShell para a DSC de Automação do Azure, consulte [cmdlets da DSC de Automação do Azure](/powershell/module/azurerm.automation/#automation)
* Para obter informações sobre preços, consulte [Preços da DSC de Automação do Azure](https://azure.microsoft.com/pricing/details/automation/)
* toosee um exemplo de como usar o DSC de automação do Azure em um pipeline de implantação contínua, consulte [tooIaaS implantação contínua DSC de automação do Azure VMs usando e Chocolatey](automation-dsc-cd-chocolatey.md)
