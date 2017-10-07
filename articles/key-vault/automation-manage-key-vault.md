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
# <a name="managing-azure-key-vault-using-azure-automation"></a>Gerenciar o Cofre da Chave do Azure usando a Automação do Azure
Este guia apresentará toohello serviço de automação do Azure e como ela pode ser usado toosimplify gerenciamento de suas chaves e segredos no cofre de chaves do Azure.

## <a name="what-is-azure-automation"></a>O que é Automação do Azure?
[Automação do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processos e por uma configuração de estado desejada. Usando a automação do Azure, as tarefas manuais repetidas, demoradas e propensas a erros podem ser toovalue de tempo para a sua organização, eficiência e confiabilidade de tooincrease automatizada.

Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades. Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.

Reduzir a sobrecarga operacional e liberar IT e DevOps equipe toofocus no trabalho que adiciona valor comercial, movendo o toobe de tarefas de gerenciamento de nuvem executados automaticamente pela automação do Azure.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Como a Automação do Azure pode ajudar a gerenciar o cofre da chave do Azure?
Cofre de chaves podem ser gerenciado na automação do Azure usando Olá [cmdlets do Cofre de chaves AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) e [cmdlets do Cofre de chaves clássico do Azure](https://msdn.microsoft.com/library/azure/dn868052.aspx). Olá módulo do Azure para gerenciar o Cofre de chaves clássico está disponível automaticamente na automação do Azure, e você pode importar Olá [AzureRM KeyVault módulo](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) na automação do Azure, para que você possa executar muitas gerenciamento seu Cofre de chaves tarefas no serviço de saudação. Esses cmdlets na automação do Azure com os cmdlets de saudação para outros serviços do Azure, as tarefas complexas tooautomate também podem ser emparelhados por serviços do Azure e 3º sistemas de terceiros.

Com hello Azure Key Vault cmdlets, você pode executar essas tarefas, entre outros: 

* Criar e configurar um cofre de chaves
* Criar ou importar uma chave
* Criar ou atualizar um segredo
* Atualizar os atributos de uma chave
* Obter uma chave ou um segredo
* Excluir uma chave ou um segredo

Aqui estão alguns exemplos de uso do PowerShell toomanage Cofre de chaves:  

* [Cofre da Chave do Azure - passo a passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Configurando um Cofre da Chave do Azure](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de automação do Azure e como ela pode ser usado toomanage Cofre de chaves do Azure, siga essas toolearn links mais informações sobre a automação do Azure.

* Consulte Olá automação do Azure [Tutorial de Introdução](../automation/automation-first-runbook-graphical.md).
* Consulte Olá [scripts do PowerShell do Azure Key Vault](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

