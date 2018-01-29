---
title: "Faça backup do Azure pilha | Microsoft Docs"
description: Execute um backup sob demanda na pilha do Azure com o backup em vigor.
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 9565DDFB-2CDB-40CD-8964-697DA2FFF70A
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: mabrigg
ms.openlocfilehash: 955b286967ca2bc8450e8988ec16c6a5c352aa8a
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="back-up-azure-stack"></a>Fazer backup do Azure pilha

*Aplica-se a: Azure pilha integrado sistemas e o Kit de desenvolvimento de pilha do Azure*

Execute um backup sob demanda na pilha do Azure com o backup em vigor. Se você precisar habilitar o serviço de Backup de infraestrutura, consulte [habilitar o Backup para a pilha do Azure no portal de administração](azure-stack-backup-enable-backup-console.md).

> [!Note]  
>  Ferramentas de pilha do Azure contêm o **AzSBackup início** cmdlet. Para obter instruções sobre como instalar as ferramentas, consulte [colocar em funcionamento com o PowerShell no Azure pilha](https://docs.microsoft.com/azure/azure-stack/azure-stack-powershell-configure-quickstart).

## <a name="start-azure-stack-backup"></a>Iniciar o backup de pilha do Azure

Abra o Windows PowerShell com um prompt com privilégios elevados no ambiente de gerenciamento de operador e execute os seguintes comandos:

```powershell
    cd C:\tools\AzureStack-Tools-master\Connect
    Import-Module .\AzureStack.Connect.psm1

    cd C:\tools\AzureStack-Tools-master\Infrastructure
    Import-Module .\AzureStack.Infra.psm1 
    
    Start-AzSBackup -Location $location.Name
```

## <a name="confirm-backup-completed-in-the-administration-portal"></a>Confirme o backup foi concluído no portal de administração

1. Abra o portal de administração de pilha do Azure em [https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external).
2. Selecione **mais serviços** > **backup da infra-estrutura**. Escolha **configuração** no **backup da infra-estrutura** folha.
3. Localizar o **nome** e **data de conclusão** do backup em **backups disponíveis** lista.
4. Verifique se o **estado** é **êxito**.

Você também pode confirmar que o backup foi concluído no portal de administração. Navegue até`\MASBackup\<datetime>\<backupid>\BackupInfo.xml`

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o fluxo de trabalho para se recuperar de um evento de perda de dados. Consulte [recuperação da perda de dados catastrófica de](azure-stack-backup-recover-data.md).
