---
title: "tootrigger de automação do Azure aaaUse um trabalho | Microsoft Docs"
description: "Saiba como toouse automação do Azure para o disparo de trabalhos do Gerenciador de dados do StorSimple (visualização particular)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Usar a automação do Azure tootrigger um trabalho (visualização particular)

Este artigo descreve como tootrigger de automação do Azure toouse um trabalho de Data do StorSimple Manager.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se você tem:

*   Azure Powershell instalado. [Baixar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Configuração tooinitialize Olá transformação de dados trabalho de configurações (instruções tooobtain essas configurações são incluídas aqui).
*   Uma definição de trabalho que foi configurada corretamente em um Recurso de Dados Híbridos dentro de um grupo de recursos.
*   Baixar `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) arquivo de repositório do github hello.
*   Baixar `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) do repositório do github hello.
*   Baixar `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) do repositório do github hello.

## <a name="step-by-step"></a>Passo a passo

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Obter as permissões do Active Directory do Azure de definição de trabalho de Olá Olá automação trabalho toorun

1. parâmetros de configuração de saudação tooretrieve para Active Directory, Olá seguintes etapas:

    1. Abra o Windows PowerShell no computador local. Verifique se o [Azure PowerShell](https://azure.microsoft.com/downloads/) está instalado.
    1. Executar Olá `Get-ConfigurationParams.ps1` script (na pasta Olá baixado anteriormente). Digite hello comando na janela do PowerShell Olá a seguir:

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        Olá ActiveDirectoryKey é uma senha que você pode usar mais tarde. Insira uma senha de sua escolha. AppName pode ser qualquer cadeia de caracteres.

2. Esse script gera Olá valores que devem ser usados ao disparar Olá runbook de automação a seguir. Anote esses valores.

    - Id do Cliente
    - ID do locatário
    - Chave de diretório ativo (mesmo que Olá fornecido acima)
    - ID da assinatura

### <a name="set-up-hello-automation-account"></a>Configurar a conta de automação de saudação

1. Faça logon em tooAzure e abra sua conta de automação.
2. Clique em **ativos** bloco tooopen Olá lista de ativos.
3. Clique em **módulos** bloco tooopen Olá lista de módulos.
4. Clique em **+ adicionar um módulo** botão e hello folha de módulo de adicionar é iniciada.

    ![Configurações da conta de automação](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. Depois que você selecionou Olá `DataTransformationApp.zip` de arquivos do computador local, clique em **Okey** tooimport módulo de saudação.

   Quando a automação do Azure importa uma conta de tooyour do módulo, ele extrai metadados sobre o módulo de saudação. Essa operação pode levar alguns minutos.

   ![Configurações da conta de automação](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. Você receberá uma notificação que o módulo hello está sendo implantado e outra notificação quando Olá processo for concluído.  Você também pode verificar o status de saudação **módulos** lado a lado.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>tooimport Olá runbook que dispara a definição de trabalho Olá

1. No portal do Azure de Olá, abra sua conta de automação.
2. Clique em **Runbooks** bloco tooopen Olá lista de runbooks.
3. Clique em **+ Adicionar um runbook** e, em seguida, em **Importar um runbook existente**.

   ![Importar um runbook existente](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. Clique em **arquivo de Runbook** e selecione Olá arquivo tooimport `Trigger-DataTransformation-Job.ps1`.
5. Clique em **criar** tooimport Olá runbook. Olá novo runbook será exibido na lista Olá runbooks para Olá conta de automação.
7. Clique no runbook **Trigger-DataTransformation-Job** e, em seguida, em **Editar**.
8. Clique em **Publicar** e em **Sim** quando solicitado para confirmação.


### <a name="toorun-hello-runbook"></a>toorun Olá runbook:
1. No portal do Azure de Olá, abra sua conta de automação.
2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.
3. Clique em **Trigger-DataTransformation-Job**.
4. Clique em **iniciar** toostart Olá runbook.

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. Em Olá **iniciar runbook** folha, insira todos os parâmetros de saudação. Clique em **Okey** toosubmit trabalho de transformação de dados de saudação.

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>Próximas etapas

[Usar os dados de interface de usuário de Gerenciador de dados StorSimple tootransform](storsimple-data-manager-ui.md).
