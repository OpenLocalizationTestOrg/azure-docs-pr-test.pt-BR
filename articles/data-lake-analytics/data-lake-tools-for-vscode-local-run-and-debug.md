---
title: "Ferramentas do Azure Data Lake: execução local e depuração local do U-SQL com o Visual Studio Code | Microsoft Docs"
description: "Saiba como depurar toouse Azure Data Lake Tools para toolocal de código do Visual Studio, executar e local."
Keywords: "O VScode, ferramentas do Azure Data Lake, execução, depuração Local, locais de depuração, visualizar o arquivo de armazenamento, Local carregar toostorage caminho"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>Execução local e depuração local do U-SQL com o Visual Studio Code

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que ter Olá pré-requisitos no local a seguir antes de começar estes procedimentos:
- Ferramenta do Azure Data Lake para Visual Studio Code. Para obter instruções, veja [Usar as Ferramentas do Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- C# para o código do Visual Studio (se você deseja depurar local tooperform um U-SQL).

   ![Instalar o C# nas Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > Olá execução local U-SQL e recursos de depuração atualmente oferecem suporte apenas aos usuários do Windows. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Configurar o ambiente de execução local Olá U-SQL

1. Selecione a paleta de comando Ctrl + Shift + P tooopen hello e, em seguida, digite **publicitário: baixar LocalRun dependência** pacotes de saudação do toodownload.  

   ![Baixe os pacotes de dependência de LocalRun publicitário Olá](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Localize os pacotes de dependência de saudação do caminho Olá mostrado no hello **saída** painel e, em seguida, instalar BuildTools e Win10SDK 10240. Aqui está um caminho de exemplo:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Localize os pacotes de dependência Olá](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, siga as instruções do Assistente de saudação.   

  ![Instalar BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240, siga as instruções do Assistente de saudação.  

  ![Instalar Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Defina variável de ambiente hello. Saudação de conjunto **SCOPE_CPP_SDK** variável de ambiente:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Reinicie Olá SO toomake-se de que as configurações de variável de ambiente de saudação entrem em vigor.  

   ![Certifique-se a variável de ambiente SCOPE_CPP_SDK hello está instalado](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Iniciar serviço de execução local hello e enviar a conta local do hello U-SQL trabalho tooa 
Para o usuário pela primeira vez hello, você está Olá toodownload solicitadas publicitário: dependência de LocalRun baixar pacotes se eles não ainda estiverem instalados.
1. Selecione a paleta de comando Ctrl + Shift + P tooopen hello e, em seguida, digite **publicitário: Iniciar serviço de execução Local**.
2. Selecione **aceitar** tooaccept Olá Microsoft Software License Terms para Olá primeira vez. 

   ![Aceitar Olá Microsoft Software License Terms](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. Olá cmd console será aberto. Para usuários pela primeira vez, você precisa tooenter **3**e, em seguida, localize o caminho de pasta local Olá para seus dados de entrada e saída. Para outras opções, você pode usar valores padrão de saudação. 

   ![Ferramentas do Data Lake para Visual Studio Code cmd de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Selecione a paleta de comando Ctrl + Shift + P tooopen hello, digite **publicitário: Enviar trabalho**e, em seguida, selecione **Local** conta local do tooyour toosubmit Olá trabalho.

   ![Ferramentas do Data Lake para Visual Studio Code selecionar local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Depois de enviar o trabalho de saudação, você pode exibir detalhes de envio de saudação. Selecione de detalhes do envio de saudação tooview **jobUrl** em Olá **saída** janela. Você também pode exibir o status de envio de trabalho de saudação do console de cmd hello. Digite **7** no console de cmd Olá se você quiser tooknow mais detalhes do trabalho.

   ![Ferramentas do Data Lake para Visual Studio Code saída de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Ferramentas do Data Lake para Visual Studio Code status do cmd de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Iniciar uma depuração local de trabalho do hello U-SQL  
Para o usuário pela primeira vez hello, você está Olá toodownload solicitadas publicitário: dependência de LocalRun baixar pacotes se eles não ainda estiverem instalados.
  
1. Selecione a paleta de comando Ctrl + Shift + P tooopen hello e, em seguida, digite **publicitário: Iniciar serviço de execução Local**. Olá cmd console será aberto. Certifique-se de que Olá **DataRoot** está definido.
3. Defina um ponto de interrupção no code-behind do C#.
4. No editor de script hello, selecione o console de comando Ctrl + Shift + P tooopen hello e, em seguida, digite **depuração Local** toostart seu serviço de depuração local.

![Ferramentas do Data Lake para Visual Studio Code resultado da depuração local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Próximas etapas
- Para usar as Ferramentas do Azure Data Lake para Visual Studio Code, confira [Usar as Ferramentas do Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- Para obter informações introdutórias sobre o Data Lake Analytics, veja [Tutorial: Introdução ao Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Para saber mais sobre as Ferramentas do Data Lake para Visual Studio, confira [Tutorial: Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Para obter informações sobre como desenvolver assemblies hello, consulte [assemblies desenvolver U-SQL para trabalhos de análise do Azure Data Lake](data-lake-analytics-u-sql-develop-assemblies.md).
