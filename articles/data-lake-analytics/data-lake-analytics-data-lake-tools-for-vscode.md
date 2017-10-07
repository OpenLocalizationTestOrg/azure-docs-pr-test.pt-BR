---
title: 'Ferramentas do Azure Data Lake: Usar as Ferramentas do Azure Data Lake para Visual Studio Code | Microsoft Docs'
description: 'Saiba como toouse Azure Data Lake Tools para Visual Studio Code toocreate, testar e executar scripts U-SQL. '
Keywords: "O VScode, ferramentas do Azure Data Lake, execução, depuração Local, locais de depuração, visualizar o arquivo de armazenamento, Local carregar toostorage caminho"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Usar as Ferramentas do Azure Data Lake para Visual Studio Code

Saiba como toouse Azure Data Lake Tools para o código do Visual Studio (VS código) toocreate, testar e executar scripts U-SQL. também são abordadas informações Olá Olá vídeo a seguir:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Pré-requisitos

Data Lake Tools pode ser instalado em plataformas de saudação aceitas pelo código do VS. plataformas de saudação com suporte incluem Windows, Linux e MacOS. plataformas diferentes Olá têm Olá pré-requisitos a seguir:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp). Adicione Olá java.exe caminho toohello ambiente variável caminho do sistema. Para obter instruções de configuração, consulte [como definir ou alterar a variável de sistema Path Olá?]( https://www.java.com/download/help/path.xml). caminho de saudação é tooC:\Program Files\Java\jdk1.8.0_77\jre\bin semelhante.
    - [Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).
    
- Linux (é recomendável o Ubuntu 14.04 LTS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). tooinstall Olá código, digite Olá comando a seguir:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - pacotes de deb Olá tooupdate de origem, digite Olá comandos a seguir:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall Mono, digite Olá comando a seguir:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Não há suporte para o Mono 4.6. Desinstale totalmente a versão 4.6 antes de instalar a versão 4.2.x.  

        - [Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp). Para obter instruções sobre instalação, consulte Olá [instruções de instalação do Linux de 64 bits para Java]( https://java.com/en/download/help/linux_x64_install.xml) página.
        - [Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp). Para obter instruções sobre instalação, consulte Olá [instruções de instalação do Linux de 64 bits para Java](https://java.com/en/download/help/mac_install.xml) página.
    - [Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Instalar as Ferramentas do Data Lake

Depois de instalar os pré-requisitos do hello, você pode instalar o Data Lake Tools para o código do VS.

**tooinstall Data Lake Tools**

1. Abra o Visual Studio Code.
2. Selecione Ctrl + P e, em seguida, digite Olá comando a seguir:
```
ext install usql-vscode-ext
```
Você pode ver uma lista de extensões de código do Visual Studio. Por exemplo, as **Ferramentas do Azure Data Lake**.

3. Selecione **instalar** Avançar muito**ferramentas do Azure Data Lake**. Depois de alguns segundos, Olá **instalar** botão alterações muito**recarregar**.
4. Selecione **recarregar** tooactivate extensão de saudação.
5. Selecione **Okey** tooconfirm. Você pode ver o Azure Data Lake Tools no hello **extensões** painel.
    ![Painel de Extensões das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Ativar Ferramentas do Azure Data Lake
Crie um novo arquivo .usql ou abra existente .usql tooactivate Olá extensão de arquivo. 

## <a name="connect-tooazure"></a>Conecte-se tooAzure

Antes de compilar e executar scripts U-SQL na análise Data Lake, você deve conectar tooyour conta do Azure.

**tooconnect tooAzure**

1.  Selecione Ctrl + Shift + P tooopen Olá comando paleta. 
2.  Digite **ADL: Logon**. informações de logon de saudação aparecem no hello **saída** painel.

    ![Paleta de comandos das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informações de logon do dispositivo das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Selecione Ctrl + clique na URL de logon Olá: https://aka.ms/devicelogin tooopen Olá logon página da Web. Insira o código de saudação **G567LX42V** na caixa de texto de saudação e selecione **continuar**.

   ![Ferramentas do Data Lake para Visual Studio Code colar código de logon](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Siga Olá instruções toosign do hello página da Web. Quando você estiver conectado, o nome da sua conta do Azure aparece na barra de status de Olá no canto inferior esquerdo Olá Olá **código VS** janela. 

    > [!NOTE] 
    > Se sua conta tiver a autenticação por dois fatores habilitada, recomendamos o uso da autenticação por telefone em vez de usar um PIN.

toosign, digite o comando Olá **publicitário: Logout**.

## <a name="list-your-data-lake-analytics-accounts"></a>Listar suas contas do Data Lake Analytics

conexão de saudação tootest, obtenha uma lista de suas contas da análise Data Lake.

**contas de análise Data Lake Olá toolist em sua assinatura do Azure**

1. Selecione Ctrl + Shift + P tooopen Olá comando paleta.
2. Insira **ADL: List Accounts**. contas de saudação aparecem no hello **saída** painel.

## <a name="open-hello-sample-script"></a>Script de exemplo hello aberto
Abra a paleta de comando hello (Ctrl + Shift + P) e digite **publicitário: abrir o Script de exemplo**. Isso abre outra instância deste exemplo. Você também pode editar, configurar e enviar o script nessa instância.

## <a name="work-with-u-sql"></a>Trabalhar com o U-SQL

Você precisa abrir um arquivo U-SQL ou uma pasta toowork com U-SQL.

**tooopen uma pasta para o seu projeto U-SQL**

1. No código do Visual Studio, selecione Olá **arquivo** menu e, em seguida, selecione **Abrir pasta**.
2. Especifique uma pasta e selecione **Selecionar Pasta**.
3. Selecione Olá **arquivo** menu e, em seguida, selecione **novo**. Um arquivo sem título 1 é adicionado toohello projeto.
4. Digite hello código a seguir no arquivo hello sem título 1:

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    script Hello cria um arquivo de departments.csv com alguns dados incluídos na pasta de /output hello.

5. Salve o arquivo hello como **myUSQL.usql** em Olá aberto na pasta. Um arquivo de configuração adltools_settings.json também é adicionado toohello projeto.
4. Abrir e configurar adltools_settings.json com hello propriedades a seguir:

    - Conta: uma conta do Data Lake Analytics na sua assinatura do Azure.
    - Banco de dados: um banco de dados em sua conta. saudação padrão é **mestre**.
    - Esquema: um esquema em seu banco de dados. saudação padrão é **dbo**.
    - Configurações opcionais:
        - Prioridade: intervalo de prioridade de saudação é de 1 too1000 com 1 prioridade mais alta hello. valor padrão de saudação é **1000**.
        - Paralelismo: intervalo de paralelismo de saudação é de 1 too150. valor padrão de saudação é permitido em sua conta da análise Azure Data Lake máximo de paralelismo do hello. 
        
        > [!NOTE] 
        > Se as configurações de saudação são inválidas, são usados valores padrão de saudação.

    ![Arquivo de configuração das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Uma conta da análise Data Lake é de computação necessária toocompile e executar trabalhos de U-SQL. Você deve configurar a conta de computador Olá antes de compilar e executar trabalhos de U-SQL.
    
Após salva configuração hello, informações de conta, o banco de dados e o esquema de saudação aparecem na barra de status de saudação no canto inferior esquerdo de saudação do arquivo correspondente de .usql hello. 
 
 
Tooopening em comparação com um arquivo, quando você abrir uma pasta que você pode:

- Usar um arquivo code-behind. No modo de arquivo único hello, não é suportado por trás do código.
- Usar um arquivo de configuração. Quando você abrir uma pasta, scripts Olá Olá pasta de trabalho compartilham um único arquivo de configuração.


Olá script U-SQL compila remotamente por meio de saudação serviço de análise Data Lake. Quando você emitir Olá **compilar** o comando, a conta de análise Data Lake tooyour de saudação script U-SQL é enviada. Posteriormente, o código do Visual Studio recebe o resultado da compilação hello. Devido a compilação remota de toohello, código do Visual Studio requer que você listar informações Olá tooconnect tooyour análise Data Lake conta no arquivo de configuração de saudação.

**toocompile um U-SQL script**

1. Selecione Ctrl + Shift + P tooopen Olá comando paleta. 
2. Insira **ADL: Compilar Script**. Olá compilação os resultados aparecem na Olá **saída** janela. Você pode também um arquivo de script e, em seguida, selecione **publicitário: Script de compilação** trabalho toocompile um U-SQL. o resultado da compilação Olá aparece no hello **saída** painel.
 

**toosubmit um U-SQL script**

1. Selecione Ctrl + Shift + P tooopen Olá comando paleta. 
2. Insira **ADL: Enviar Trabalho**.  Também é possível clicar com o botão direito do mouse em um arquivo de script e, depois, selecionar **ADL: Enviar Trabalho**. 

Depois que você enviar um trabalho de U-SQL, logs de envio de saudação são exibidos na Olá **saída** janela no código VS. Se o envio de saudação for bem-sucedida, Olá trabalho URL também é exibida. Você pode abrir Olá trabalho URL em um status de trabalho em tempo real da web navegador tootrack hello.

saída de hello tooenable de detalhes do trabalho Olá, definir **jobInformationOutputPath** em Olá **vs código para hello u-sql_settings.json** arquivo.
 
## <a name="use-a-code-behind-file"></a>Usar um arquivo code-behind

Um arquivo code-behind é um arquivo em C# associado a um único script U-SQL. Você pode definir um script dedicado tooUDO UDA, UDT e UDF no arquivo de code-behind hello. Olá UDO, UDA, UDT e UDF podem ser usados diretamente no script hello sem registrar o assembly hello primeiro. Hello arquivo code-behind é colocado em Olá mesma pasta do seu arquivo de script U-SQL emparelhamento. Se o script hello é denominado xxx.usql, Olá lógica é nomeada como xxx.usql.cs. Se você excluir manualmente o arquivo de code-behind hello, recurso de lógica de saudação está desabilitado para seu script U-SQL associado. Para saber mais sobre como escrever código do cliente para script U-SQL, veja [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (Escrevendo e usado código personalizado em U-SQL — Funções Definidas pelo Usuário).

toosupport por trás do código, você deve abrir uma pasta de trabalho. 

**toogenerate um arquivo code-behind**

1. Abra um arquivo de origem. 
2. Selecione Ctrl + Shift + P tooopen Olá comando paleta.
3. Insira **ADL: Gerar Code-Behind**. Um arquivo code-behind é criado no hello mesma pasta. 

Também é possível clicar com o botão direito em um arquivo de script e, depois, selecionar **ADL: Gerar Code Behind**. 

toocompile e enviar um script U-SQL com um arquivo code-behind é Olá mesmo que o arquivo de script com hello autônomo U-SQL.

Olá duas capturas de tela a seguir mostra um arquivo code-behind e seu arquivo de script U-SQL associado:
 
![Code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Arquivo de script code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Usar assemblies

Para obter informações sobre como desenvolver assemblies, confira [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics).

Você pode usar assemblies de código personalizado do Data Lake Tools tooregister no catálogo de análise Data Lake hello.

**tooregister um assembly**

Você pode registrar o assembly hello por meio de saudação **publicitário: registrar Assembly de** ou **publicitário: registrar o Assembly por meio da configuração** comandos.

**tooregister por meio de saudação publicitário: comando registrar Assembly**
1.  Selecione Ctrl + Shift + P tooopen Olá comando paleta.
2.  Digite **ADL: Registrar Assembly**. 
3.  Especifica caminho do local do assembly hello. 
4.  Selecione uma conta do Data Lake Analytics.
5.  Selecione um banco de dados.

Resultados: portal de saudação é aberto em um navegador e exibe o processo de registro do assembly hello.  

Saudação de tootrigger outra maneira conveniente **publicitário: registrar Assembly de** comando é o DLL de saudação tooright clique no Explorador de arquivos. 

**tooregister embora Olá publicitário: registrar o Assembly através do comando de configuração**
1.  Selecione Ctrl + Shift + P tooopen Olá comando paleta.
2.  Digite **ADL: Registrar Assembly através da Configuração**. 
3.  Especifica caminho do local do assembly hello. 
4.  arquivo JSON de saudação é exibido. Revise e edite as dependências de assembly hello e parâmetros de recursos, se necessário. As instruções são exibidas no hello **saída** janela. tooproceed toohello registro do assembly, salve o arquivo JSON de saudação (Ctrl + S).

![Code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- As dependências de assembly: Azure Data Lake Tools este detecta automaticamente se Olá DLL tem todas as dependências. dependências de saudação são exibidas no arquivo JSON de saudação depois que eles são detectados. 
>- Recursos: Você pode carregar os recursos DLL (por exemplo,. txt,. PNG e. csv) como parte do registro do assembly hello. 

Saudação de tootrigger outra maneira **publicitário: registrar o Assembly por meio da configuração** comando é o DLL de saudação tooright clique no Explorador de arquivos. 

Olá código U-SQL a seguir demonstra como toocall um assembly. No exemplo hello, nome do assembly hello é *teste*.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>Acessar o catálogo do hello análise Data Lake

Depois que você se conectou tooAzure, você pode usar o hello catálogo de saudação U-SQL tooaccess as etapas a seguir.

**metadados de análise do Azure Data Lake Olá tooaccess**

1.  Pressione CTRL+SHIFT+P e insira **ADL: Listar Tabelas**.
2.  Selecione uma das contas de análise Data Lake hello.
3.  Selecione um dos bancos de dados de análise Data Lake hello.
4.  Selecione um dos esquemas de saudação. Você pode ver a lista de saudação de tabelas.

## <a name="view-data-lake-analytics-jobs"></a>Exibir trabalhos do Data Lake Analytics

**trabalhos de análise Data Lake tooview**
1.  Abra a paleta de comando hello (Ctrl + Shift + P) e selecione **publicitário: Mostrar trabalho**. 
2.  Selecione uma conta do Data Lake Analytics ou local. 
3.  Aguarde para lista de trabalhos Olá Olá conta tooappear.
4.  Selecione um trabalho na lista de trabalhos, Data Lake Tools abre detalhes do trabalho Olá no hello portal do Azure e exibe o arquivo de JobInfo Olá no código VS.

![Tipos de objeto do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Integração do Armazenamento do Azure Data Lake

Você pode usar comandos relacionados ao Armazenamento do Azure Data Lake:
 - Procure por meio de recursos de armazenamento do Azure Data Lake hello. 
 - Arquivo de armazenamento do Azure Data Lake Olá visualização.  
 - Saudação de carregar arquivo de tooAzure Data Lake armazenamento diretamente no código VS. 

### <a name="list-hello-storage-path"></a>Caminho de armazenamento de saudação de lista 
Você pode listar o caminho de armazenamento Olá por meio de paleta do comando hello ou com o botão direito.

**caminho de armazenamento toolist Olá a paleta de comando Olá**

1.  Abra a paleta de comando hello (Ctrl + Shift + P) e digite **publicitário: caminho de armazenamento de lista**.

    ![Listar caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Selecione sua maneira preferida para listar o caminho de armazenamento de saudação. Esta passagem usa **Inserir um caminho** como exemplo.

    ![Data Lake Tools para Visual Studio Code caminho de armazenamento Olá toolist unidirecional](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- Código VS mantém caminho de saudação visitou por último em cada conta da análise Data Lake. Por exemplo: /tt/ss.
    >- Navegador do caminho raiz: caminho de raiz de lista de saudação da sua conta da análise Data Lake selecionada ou um caminho local.
    >- Inserir um caminho: lista um caminho especificado de sua conta do Data Lake Analytics selecionada, ou um caminho local.
    
3. Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.

    ![Ferramentas do Data Lake para Visual Studio Code selecionar mais](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Selecione **mais** toolist mais análise Data Lake contas e, em seguida, selecione uma conta da análise Data Lake.

    ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Insira um caminho de armazenamento do Azure. Por exemplo, /output.

    ![Inserir caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Resultados: paleta de comando Olá lista informações de caminho de saudação com base nas suas entradas.

    ![Listar resultados do caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Uma maneira mais conveniente de caminho relativo do toolist Olá é por meio de saudação clique o menu de contexto.

**caminho de armazenamento de saudação toolist por meio de clique**

1.  Clique com botão direito Olá tooselect de cadeia de caracteres de caminho **caminho de armazenamento de lista**.

       ![Menu de contexto acessado com o botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. caminho relativo do selecionado Olá aparece na paleta de comando Olá.

   ![Caminho relativo selecionado das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Resultados: paleta de comando Olá lista Olá pastas e arquivos caminho atual hello.

       ![Data Lake Tools para lista de código do Visual Studio do caminho atual Olá](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>Arquivo de armazenamento de saudação de visualização
Você pode visualizar o arquivo de armazenamento Olá por meio de paleta do comando hello ou com o botão direito.

**arquivo de armazenamento de saudação toopreview por meio da paleta de comando Olá**

1.  Abra a paleta de comando hello (Ctrl + Shift + P) e digite **publicitário: arquivo de armazenamento de visualização**.

       ![Visualizar arquivo de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.

       ![Listar conta das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Selecione **mais** toolist mais análise Data Lake contas e, em seguida, selecione uma conta da análise Data Lake.

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Insira um caminho ou arquivo de armazenamento do Azure. Por exemplo: /output/SearchLog.txt.

       ![Inserir caminho e arquivo de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Resultados: paleta de comando Olá lista informações de caminho de saudação com base nas suas entradas.

       ![Ferramentas do Data Lake para Visual Studio Code Resultado da visualização do arquivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**caminho de armazenamento de saudação toolist por meio de clique**

1.  toopreview um arquivo, clique o caminho do arquivo hello.

   ![Menu de contexto acessado com o botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Resultados: Código VS exibe os resultados de visualização de saudação do arquivo hello.

       ![Ferramentas do Data Lake para Visual Studio Code Resultado da visualização do arquivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Carregar um arquivo 

Você pode carregar arquivos digitando comandos Olá **publicitário: Carregue o arquivo** ou **publicitário: Carregue o arquivo por meio da configuração**.

**arquivos tooupload embora Olá publicitário: comando carregar arquivo**
1. Selecione Ctrl + Shift + P tooopen Olá comando paleta ou com o botão direito editor de script hello e, em seguida, digite **carregar arquivo**.
2.  Olá tooupload de arquivo, insira um caminho local.

    ![Inserir caminho local das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Selecione uma das maneiras de saudação do caminho de armazenamento de saudação de listagem. Esta passagem usa **Inserir um caminho** como exemplo.

    ![Listar caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- Código VS mantém caminho de saudação visitou por último em cada conta da análise Data Lake. Por exemplo: /tt/ss.
    >- Navegador do caminho raiz: caminho de raiz de lista de saudação da sua conta da análise Data Lake selecionada ou um caminho local.
    >- Inserir um caminho: lista um caminho especificado de sua conta do Data Lake Analytics selecionada, ou um caminho local.

4. Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.

    ![Armazenamento acionado pelo botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Insira um caminho de armazenamento do Azure. Por exemplo: /output.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Encontre o caminho de seu armazenamento do Azure. Selecione **Escolher pasta atual**.

    ![Selecionar uma pasta das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Resultados: Olá **saída** janela exibe o status de carregamento de arquivo hello.

       ![Status de upload das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**arquivos tooupload embora Olá publicitário: Carregue o arquivo por meio do comando de configuração**
1.  Selecione Ctrl + Shift + P tooopen Olá comando paleta ou com o botão direito editor de script hello e, em seguida, digite **carregar o arquivo por meio da configuração**.
2.  O VS Code exibe um arquivo JSON. Você pode inserir os caminhos de arquivo e carregar vários arquivos no hello simultaneamente. As instruções são exibidas no hello **saída** janela. tooproceed tooupload Olá arquivo, salve (Ctrl + S) Olá JSON.

       ![Inserir arquivo das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Resultados: Olá **saída** janela exibe o status de carregamento de arquivo hello.

       ![Status de upload das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Outro tooupload de maneira toostorage um arquivo é por meio de saudação de atalho no caminho completo do arquivo hello ou um caminho relativo do arquivo hello no editor de script hello. Insira o caminho do arquivo local hello e, em seguida, selecione a conta de saudação. Olá **saída** janela exibe o status de carregamento de saudação. 

### <a name="open-azure-storage-explorer"></a>Abra o Gerenciador de Armazenamento do Azure
Você pode abrir **Azure Storage Explorer** digitando o comando Olá **publicitário: Abra o Web Azure Storage Explorer** ou selecionando-o no menu de contexto do botão direito do mouse hello.

**tooopen Azure Storage Explorer**

1. Selecione Ctrl + Shift + P tooopen Olá comando paleta.
2. Digite **abra Web Azure Storage Explorer** ou com o botão direito em um caminho relativo ou um caminho completo de saudação no editor de script hello e, em seguida, selecione **abra Web Azure Storage Explorer**.
3. Selecione uma conta do Data Lake Analytics.

Ferramentas do data Lake abre caminho de armazenamento do Azure Olá no Olá portal do Azure. Você pode encontrar hello caminho e visualização Olá arquivo da web hello.

### <a name="local-run-and-local-debug-for-windows-users"></a>Depuração local e execução local para usuários do Windows
Local de U-SQL execute testes de seus dados locais e valida o script localmente, antes que seu código seja publicado tooData análise Lake. Olá depuração local recurso permite que você toocomplete Olá tarefas a seguir antes de seu código é enviada análise tooData Lake: 
- Depure o code-behind em C#. 
- Percorrer o código de saudação. 
- Valide o script localmente.

Para obter instruções sobre a execução e a depuração local, confira [Execução local do U-SQL e depuração local com o Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Recursos adicionais

Data Lake Tools para código VS dá suporte a saudação recursos a seguir:

-   Preenchimento automático de IntelliSense: as sugestões são exibidas em janelas pop-up ao redor dos itens, como palavras-chave, métodos e variáveis. Ícones diferentes representam tipos diferentes de objetos de saudação:

    - Tipo de dados de Scala
    - Tipos de dados complexos
    - UDTs Internos
    - Coleções e classes .Net
    - Expressões em C#
    - UDFs, UDOs e UDAAGs internos de C# 
    - Funções em U-SQL
    - Função de Janelas do U-SQL
 
    ![Tipos de objeto do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   IntelliSense preenchimento automático nos metadados da análise Data Lake: Data Lake Tools baixa informações de metadados de análise Data Lake Olá localmente. recurso IntelliSense de saudação preenche automaticamente os objetos, inclusive Olá banco de dados, esquema, tabela, exibição, função com valor de tabela, procedimentos e c# assemblies, Olá análise Data Lake metadados.
 
    ![Metadados do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   Marcador de erro do IntelliSense: Data Lake Tools sublinha Olá edição erros para U-SQL e c#. 
-   Destaques de sintaxe: Data Lake Tools usa os itens de toodifferentiate de cores diferentes, como variáveis, palavras-chave, tipo de dados e funções. 

    ![Destaques da sintaxe das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Próximas etapas

- Para saber mais sobre a execução local do U-SQL e sobre a depuração local com o Visual Studio Code, consulte [Execução local do U-SQL e depuração local com o Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).
- Para obter informações introdutórias sobre o Data Lake Analytics, veja [Tutorial: Introdução ao Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Para saber mais sobre as Ferramentas do Data Lake para Visual Studio, confira [Tutorial: Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Para obter informações sobre como desenvolver assemblies, confira [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics).



