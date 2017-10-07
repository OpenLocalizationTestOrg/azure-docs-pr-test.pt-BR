---
title: trabalhos aaaDebug U-SQL | Microsoft Docs
description: "Saiba como toodebug um U-SQL falha vértice usando o Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Depurar um código C# definido pelo usuário em trabalhos com falha do U-SQL

U-SQL fornece um modelo de extensibilidade usando c#, portanto você pode escrever sua funcionalidade de tooadd código como um extrator personalizado ou Redutor. mais, consulte toolearn [guia de programação de U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). Na prática, qualquer código pode precisar de depuração e sistemas de Big Data podem fornecer apenas informações limitadas de depuração em tempo de execução como arquivos de log.

Azure Data Lake Tools para Visual Studio fornece um recurso chamado **Falha na depuração de vértice**, que permite que você clonar um trabalho com falha do computador local do hello nuvem tooyour para depuração. clone local Olá captura o ambiente de nuvem inteira hello, incluindo quaisquer dados de entrada e o código do usuário.

Olá vídeo a seguir demonstra falha vértice depurar no Azure Data Lake Tools para Visual Studio.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> O Visual Studio requer Olá após duas atualizações, se eles não ainda estiverem instalados: [Microsoft Visual C++ 2015 Redistributable atualização 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) e [Universal em tempo de execução do C para Windows](https://www.microsoft.com/download/details.aspx?id=50410).

## <a name="download-failed-vertex-toolocal-machine"></a>Falha no download do vértice toolocal máquina

Quando você abre um trabalho com falha no Azure Data Lake Tools para Visual Studio, verá uma barra amarela de alerta com mensagens de erro detalhadas na guia erro de saudação.

1. Clique em **baixar** toodownload todos Olá necessários recursos e fluxos de entrada. Se o download de saudação não for concluída, clique em **novamente**.

2. Clique em **abrir** após o download de saudação toogenerate um ambiente de depuração local. Uma nova instância do Visual Studio com uma solução de depuração é criada e aberta automaticamente.

![Vértice para download do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

Os trabalhos podem incluir arquivos de origem code-behind ou assemblies registrados e esses dois tipos têm diferentes cenários de depuração.

- [Depurar um trabalho com falha com code-behind](#debug-job-failed-with-code-behind)
- [Depurar um trabalho com falha com assemblies](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>Depurar um trabalho com falha com code-behind

Se um trabalho de U-SQL falha e o trabalho de saudação inclui o código do usuário (geralmente denominado `Script.usql.cs` em um projeto de U-SQL), que o código-fonte é importado para Olá depuração solução.  Lá você pode usar Olá Olá Visual Studio depuração ferramentas (Observação, variáveis, etc.) tootroubleshoot problema.

> [!NOTE]
> Antes de depurar, ser toocheck se **exceções do Common Language Runtime** na janela de configurações de exceção de saudação (**Ctrl + Alt + E**).

![Configuração do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. Pressione **F5** toorun código de code-behind de saudação. Ele será executado até que seja interrompido por uma exceção.

2. Olá abrir `ADLTool_Codebehind.usql.cs` arquivo e defina pontos de interrupção, em seguida, pressione **F5** código de saudação toodebug passo a passo.

    ![Exceção de depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>Depurar trabalho em falha com assemblies

Se você usar assemblies registrados em seu script U-SQL, o sistema de saudação não é possível obter código-fonte Olá automaticamente. Nesse caso, adicione manualmente fonte código arquivos toohello solução os assemblies da saudação.

### <a name="configure-hello-solution"></a>Configurar a solução de saudação

1. Clique com botão direito **solução 'VertexDebug' > Adicionar > projeto existente...**  toofind Olá código-fonte dos assemblies e adicione Olá projeto toohello solução de depuração.

    ![Adicionar projeto de depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Clique com botão direito **LocalVertexHost > propriedades** em Olá Olá solução e cópia **Working Directory** caminho.

3. Clique com botão direito **projeto de código de origem do assembly > propriedades**, selecione Olá **criar** guia à esquerda e, em seguida, cole o caminho de saudação copiado como **saída > caminho de saída**.

    ![Definir caminho pdb da depuração do U-SQL do Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. Pressione **Ctrl+Alt+E** e marque **Exceções de Common Language Runtime** na janela Configurações de exceção.

### <a name="start-debug"></a>Iniciar depuração

1. Clique com botão direito **projeto de código de origem do assembly > recriar** toohello de arquivos. PDB de toooutput `LocalVertexHost` diretório de trabalho.

2. Pressione **F5** e projeto Olá será executado até que ele seja interrompido por uma exceção. Você pode ver Olá mensagem de aviso, você pode ignorar com segurança a seguir. Pode demorar até a tela de depuração de toohello tooa tooget minutos.

    ![Aviso do visual studio para depuração do U-SQL no Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. Abra o seu código-fonte e definir pontos de interrupção, em seguida, pressione **F5** código de saudação toodebug passo a passo.

Você também pode usar Olá Visual Studio depuração ferramentas (Observação, variáveis, etc.) tootroubleshoot Olá problema.

> [!NOTE]
> Recompile o projeto de código de origem do assembly hello cada vez depois de modificar arquivos. PDB do hello código toogenerate atualizado.

Após a depuração, se o projeto de saudação for concluído com êxito Olá a janela de saída mostra Olá a seguinte mensagem:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Depuração do U-SQL do Azure Data Lake Analytics bem sucedida](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Envie novamente o trabalho de saudação

Depois de concluir a depuração, reenvie o trabalho com falha hello.

1. Para trabalhos com as soluções de lógica, copie seu código c# em um arquivo de origem do code-behind de saudação (geralmente `Script.usql.cs`).
2. Para trabalhos com assemblies, registre Olá atualizado. dll assemblies no banco de dados ADLA:
    1. No Gerenciador de servidores ou Cloud Explorer, expanda Olá **conta ADLA > bancos de dados** nó.
    2. Clique com botão direito **Assemblies** e registrar seus novos assemblies. dll com o banco de dados do hello ADLA: ![depuração da análise Azure Data Lake U-SQL registrar o assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. Reenvie o trabalho.

## <a name="next-steps"></a>Próximas etapas

- [Guia de programação do U-SQL](data-lake-analytics-u-sql-programmability-guide.md)
- [Desenvolver operadores do U-SQL definidos pelo usuário para trabalhos do Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
