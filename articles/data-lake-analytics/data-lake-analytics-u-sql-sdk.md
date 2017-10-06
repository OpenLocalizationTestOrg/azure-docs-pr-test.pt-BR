---
title: local aaaScale U-SQL execute e teste com o SDK do SQL Azure Data Lake U | Microsoft Docs
description: "Saiba como trabalhos tooscale U-SQL de SDK do Azure Data Lake U-SQL de toouse locais executar e testam com linha de comando e interfaces de programação na sua estação de trabalho local."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Escalar a execução e o teste locais do U-SQL com o SDK do U-SQL do Azure Data Lake

Ao desenvolver o script U-SQL, é comum toorun e teste U-SQL script localmente antes de enviar-toocloud. O Azure Data Lake fornece um pacote NuGet chamado SDK do U-SQL do Azure Data Lake para este cenário, por meio do qual é possível escalar a execução e o teste locais do U-SQL com facilidade. Também é possível toointegrate este U-SQL de teste com a compilação de saudação do CI (integração contínua) sistema tooautomate e teste.

Se você se preocupa como toomanually local executar e depurar o script U-SQL com ferramentas de interface gráfica do usuário, em seguida, você pode usar o Azure Data Lake Tools para Visual Studio para que. Saiba mais [aqui](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="install-azure-data-lake-u-sql-sdk"></a>Instalar o SDK do U-SQL do Azure Data Lake

Você pode obter o SDK do Azure Data Lake U-SQL de saudação [aqui](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) em Nuget.org. E antes de usá-lo, você precisa toomake-se de que ter dependências da seguinte maneira.

### <a name="dependencies"></a>Dependências

Olá Data Lake U-SQL SDK requer Olá dependências a seguir:

- [Microsoft .NET Framework 4.6 ou mais recente](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 e SDK do Windows 10.0.10240.0 ou mais novo (que é chamado CppSDK neste artigo). Há duas maneiras tooget CppSDK:

    - Instalar o [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou). Você terá uma pasta \Windows Kits\10 na pasta de arquivos de programa do hello – por exemplo, C:\Program Files (x86) \Windows Kits\10\. Você também encontrará a versão do SDK do Windows 10 Olá em \Windows Kits\10\Lib. Se você não vir essas pastas, reinstalar o Visual Studio e se tooselect Olá SDK do Windows 10 durante a instalação de saudação. Se você tiver instalado com o Visual Studio, compilador local do hello U-SQL encontrará automaticamente.

    ![SDK para Windows 10 da execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - Instalar [Ferramentas do Data Lake para Visual Studio](http://aka.ms/adltoolsvs). Você pode encontrar hello predefinida de arquivos do Visual C++ e o SDK do Windows em C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK. Nesse caso, compilador local do hello U-SQL não é possível localizar as dependências de saudação automaticamente. Você precisa de caminho de CppSDK de saudação toospecify para ele. Você pode copiar Olá arquivos tooanother local ou usá-la como está.

## <a name="understand-basic-concepts"></a>Entender os conceitos básicos

### <a name="data-root"></a>Raiz de dados

pasta de dados raiz Olá é "armazenamento local" para a conta de computação local hello. É a conta do repositório Azure Data Lake toohello equivalente de uma conta da análise Data Lake. Pasta raiz de dados diferentes alternando tooa é como alternar tooa conta de armazenamento diferente. Se você quiser tooaccess normalmente compartilhado dados com pastas raiz de dados diferentes, você deve usar caminhos absolutos em seus scripts. Criar links simbólicos do sistema de arquivo (por exemplo, **mklink** em NTFS) em Olá raiz de dados pasta toopoint toohello dados compartilhados.

pasta de dados raiz Olá é usada para:

- Armazenar metadados locais, incluindo bancos de dados, tabelas, TVFs (funções com valor de tabela) e assemblies.
- Pesquise hello de entrada e os caminhos de saída que são definidos como caminhos relativos no U-SQL. Usar caminhos relativos torna mais fácil toodeploy seu tooAzure de projetos de U-SQL.

### <a name="file-path-in-u-sql"></a>Caminho de arquivo no U-SQL

Você pode usar um caminho relativo e um caminho absoluto local em scripts U-SQL. caminho relativo da saudação é relativo toohello caminho da pasta raiz de dados especificado. É recomendável que você use "/" como Olá toomake do separador de caminho seus scripts compatíveis com do lado do servidor de saudação. A seguir, alguns exemplos de caminhos relativos e os respectivos caminhos absolutos equivalentes. Nestes exemplos, C:\LocalRunDataRoot é a pasta raiz de dados de saudação.

|Caminho relativo|Caminho absoluto|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>Diretório de trabalho

Ao executar o script hello U-SQL localmente, um diretório de trabalho é criado durante a compilação em diretório de execução atual. Além disso saídas de compilação toohello hello necessários arquivos de tempo de execução para execução local será diretório de trabalho toothis copiado de sombra. saudação de pasta de raiz do diretório de trabalho é chamada de "ScopeWorkDir" e arquivos Olá Olá diretório de trabalho são os seguintes:

|Diretório/arquivo|Diretório/arquivo|Diretório/arquivo|Definição|Descrição|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |Cadeia de caracteres de hash da versão do tempo de execução|Cópia de sombra dos arquivos de tempo de execução necessários para execução local|
| |Script_66AE4909AA0ED06C| |Nome do script + cadeia de caracteres de hash do caminho do script|Saídas da compilação e log das etapas de execução|
| | |\_script\_.abr|Saída do compilador|Arquivo de álgebra|
| | |\_ScopeCodeGen\_.*|Saída do compilador|Código gerenciado gerado|
| | |\_ScopeCodeGenEngine\_.*|Saída do compilador|Código nativo gerado|
| | |assemblies referenciados|Referência de assembly|Arquivos de assembly referenciado|
| | |deployed_resources|Implantação de recursos|Arquivos da implantação de recursos|
| | |xxxxxxxx.xxx[1..n]\_\*.*|Log de execução|Log das etapas de execução|


## <a name="use-hello-sdk-from-hello-command-line"></a>Use Olá SDK da linha de comando Olá

### <a name="command-line-interface-of-hello-helper-application"></a>Interface de linha de comando do aplicativo de auxiliar hello

No SDK directory\build\runtime, LocalRunHelper.exe é aplicativo de linha de comando auxiliar hello que fornece interfaces funções toomost de saudação usada execução local. Observe que ambos Olá comando e opções de argumento Olá diferenciam maiusculas de minúsculas. tooinvoke-lo:

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

Execute LocalRunHelper.exe sem argumentos ou com hello **ajuda** alternar tooshow informações de ajuda de saudação:

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

Informações de Ajuda no hello:

-  **Comando** fornece Olá nome do comando.  
-  **Required Argument** lista argumentos que devem ser fornecidos.  
-  **Optional Argument** lista argumentos que são opcionais e com valores padrão.  Argumentos opcionais de boolianos não tem parâmetros e suas aparências significam o valor padrão de tootheir negativo.

### <a name="return-value-and-logging"></a>Valor de retorno e registro em log

aplicativo de auxiliar Hello retorna **0** para êxito e **-1** falha. Por padrão, o auxiliar de saudação envia todas as console atual toohello de mensagens. No entanto, a maioria dos comandos de saudação suporte Olá **- MessageOut caminho_para_arquivo_log** argumento opcional que redireciona hello gera o arquivo de log tooa.

### <a name="environment-variable-configuring"></a>Configurando variáveis de ambiente

A execução local do U-SQL precisa de uma raiz de dados especificada como a conta de armazenamento local, bem como um caminho do CppSDK especificado para as dependências. Você pode ambos os argumento de conjunto de saudação na variável de ambiente de linha de comando ou definidas para eles.

- Saudação de conjunto **SCOPE_CPP_SDK** variável de ambiente.

    Se você obtiver o Microsoft Visual C++ e hello SDK do Windows ao instalar o Data Lake Tools para Visual Studio, verifique se Olá pasta a seguir:

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    Definir uma nova variável de ambiente chamada **SCOPE_CPP_SDK** toopoint toothis directory. Ou copie Olá pasta toohello outro local e especificar **SCOPE_CPP_SDK** que.

    Variável de ambiente do adição toosetting hello, você pode especificar Olá **- CppSDK** argumento quando você estiver usando a linha de comando hello. Esse argumento substitui a variável de ambiente CppSDK padrão.

- Saudação de conjunto **LOCALRUN_DATAROOT** variável de ambiente.

    Definir uma nova variável de ambiente chamada **LOCALRUN_DATAROOT** que aponte toohello raiz de dados.

    Variável de ambiente do adição toosetting hello, você pode especificar Olá **- DataRoot** argumento com caminho de dados raiz hello quando você estiver usando uma linha de comando. Esse argumento substitui a variável de ambiente de raiz de dados padrão. É necessário tooadd essa linha de comando tooevery argumento que estiver em execução para que você pode substituir uma variável de ambiente de dados raiz saudação padrão para todas as operações.

### <a name="sdk-command-line-usage-samples"></a>Amostras de uso da linha de comando do SDK

#### <a name="compile-and-run"></a>Compilar e executar

Olá **execute** comando é usado toocompile Olá script e, em seguida, executar resultados compilados. Seus argumentos de linha de comando são uma combinação dos argumentos de **compile** e **execute**.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

Olá, a seguir é argumentos opcionais para **executar**:


|Argumento|Valor padrão|Descrição|
|--------|-------------|-----------|
|-CodeBehind|Falso|script Hello possui código. cs|
|-CppSDK| |Diretório do CppSDK|
|-DataRoot| Variável de ambiente DataRoot|DataRoot para execução local, padrão muito variável de ambiente 'LOCALRUN_DATAROOT'|
|-MessageOut| |Mensagens de despejo no arquivo tooa do console|
|-Parallel|1|Executar Olá plano com hello especificado paralelismo|
|-References| |Lista de assemblies de referência tooextra caminhos ou arquivos de dados de code-behind, separada por ';'|
|-UdoRedirect|Falso|Gerar configuração de redirecionamento de assembly UDO|
|-UseDatabase|mestre|Toouse de banco de dados para o código por trás de registro de assembly temporário|
|-Verbose|Falso|Mostrar saídas detalhadas do tempo de execução|
|-WorkDir|Diretório atual|Diretório para uso do compilador e saídas|
|-RunScopeCEP|0|ScopeCEP modo toouse|
|-ScopeCEPTempPath|temp|Toouse caminho temporário para o fluxo de dados|
|-OptFlags| |Lista separada por vírgula de sinalizadores do otimizador|


Aqui está um exemplo:

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

Além de combinar **compilar** e **executar**, você pode compilar e executar executáveis Olá compilado separadamente.

#### <a name="compile-a-u-sql-script"></a>Compilar um script U-SQL

Olá **compilar** comando é usado toocompile um U-SQL script tooexecutables.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

Olá, a seguir é argumentos opcionais para **compilar**:


|Argumento|Descrição|
|--------|-----------|
| -CodeBehind [valor padrão 'False']|script Hello possui código. cs|
| -CppSDK [valor padrão '']|Diretório do CppSDK|
| -DataRoot [valor padrão “variável de ambiente DataRoot”]|DataRoot para execução local, padrão muito variável de ambiente 'LOCALRUN_DATAROOT'|
| -MessageOut [valor padrão '']|Mensagens de despejo no arquivo tooa do console|
| -References [valor padrão '']|Lista de assemblies de referência tooextra caminhos ou arquivos de dados de code-behind, separada por ';'|
| -Shallow [valor padrão 'False']|Compilação superficial|
| -UdoRedirect [valor padrão 'False']|Gerar configuração de redirecionamento de assembly UDO|
| -UseDatabase [valor padrão 'master']|Toouse de banco de dados para o código por trás de registro de assembly temporário|
| -WorkDir [valor padrão “Diretório Atual”]|Diretório para uso do compilador e saídas|
| -RunScopeCEP [valor padrão “0”]|ScopeCEP modo toouse|
| -ScopeCEPTempPath [valor padrão “temp”]|Toouse caminho temporário para o fluxo de dados|
| -OptFlags [valor padrão '']|Lista separada por vírgula de sinalizadores do otimizador|


Veja alguns exemplos de uso.

Compilar um script U-SQL:

    LocalRunHelper compile -Script d:\test\test1.usql

Compilar um script U-SQL e defina a pasta de dados raiz hello. Observe que isto substituirá a variável de ambiente do conjunto de saudação.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

Compilar um script U-SQL e definir um diretório de trabalho, o assembly de referência e o banco de dados:

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>Executar resultados compilados

Olá **execute** comando é usado tooexecute compilado resultados.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

Olá, a seguir é argumentos opcionais para **executar**:

|Argumento|Descrição|
|--------|-----------|
|-DataRoot [valor padrão '']|Raiz de dados para a execução de metadados. O padrão é toohello **LOCALRUN_DATAROOT** variável de ambiente.|
|-MessageOut [valor padrão '']|Despeje mensagens no arquivo de tooa Olá console.|
|-Parallel [valor padrão '1']|Etapas de execução local do indicador toorun Olá gerado com hello especificado o nível de paralelismo.|
|-Verbose [valor padrão 'False']|Indicador tooshow detalhadas saídas do tempo de execução.|

Aqui está um exemplo de uso:

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>Usar Olá SDK com interfaces de programação

interfaces de programação de saudação estão localizado em Olá LocalRunHelper.exe. Você pode usá-los toointegrate funcionalidade de saudação do hello SDK U-SQL e Olá c# test framework tooscale seu teste de local de script U-SQL. Neste artigo, eu usarei a saudação padrão c# unidade teste projeto tooshow como toouse essas interfaces tootest seu script U-SQL.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>Etapa 1: Criar o projeto de teste de unidade do C# e a configuração

- Crie um projeto de teste de unidade do C# por meio de Arquivo > Novo > Projeto > Visual C# > Teste > Projeto de Teste de Unidade.
- Adicione LocalRunHelper.exe como uma referência para o projeto de saudação. Olá LocalRunHelper.exe está localizado em \build\runtime\LocalRunHelper.exe no pacote do Nuget.

    ![SDK do U-SQL do Azure Data Lake – Adicionar referência](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- SDK de U-SQL **somente** suporte x64 ambiente, verifique se tooset compilação plataforma destino como x64. É possível definir isso por meio de Propriedade do Projeto > Build > Destino da plataforma.

    ![SDK do U-SQL do Azure Data Lake – Configurar projeto do x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- Verifique se tooset seu ambiente de teste como x64. No Visual Studio, é possível defini-lo por meio de Teste > Configurações de Teste > Arquitetura do Processador Padrão > x64.

    ![SDK do U-SQL do Azure Data Lake – Configurar ambiente de teste x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- Verifique se toocopy todos os arquivos de dependência no diretório de trabalho do NugetPackage\build\runtime\ tooproject que é geralmente em ProjectFolder\bin\x64\Debug.

### <a name="step-2-create-u-sql-script-test-case"></a>Etapa 2: Criar um caso de teste do script U-SQL

Abaixo está o código de exemplo hello para teste de script U-SQL. Para testar, você precisa tooprepare scripts, arquivos de entrada e saída esperada.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>Interfaces de programação em LocalRunHelper.exe

LocalRunHelper.exe fornece Olá interfaces de programação para compilação de local de U-SQL, execute, interfaces de saudação etc. são listadas a seguir.

**Construtor**

public LocalRunHelper([System.IO.TextWriter messageOutput = null])

|.|Tipo|Descrição|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|para mensagens de saída, definir toonull toouse Console|

**Propriedades**

|Propriedade|Tipo|Descrição|
|--------|----|-----------|
|AlgebraPath|string|Olá caminho tooalgebra arquivo (arquivo álgebra é um dos resultados da compilação Olá)|
|CodeBehindReferences|string|Se o script hello tem adicional code-behind referências, especificar caminhos de Olá separados por ';'|
|CppSdkDir|string|Diretório do CppSDK|
|CurrentDir|string|Diretório atual|
|DataRoot|string|Caminho da raiz de dados|
|DebuggerMailPath|string|Olá caminho toodebugger falhas|
|GenerateUdoRedirect|bool|Se quisermos carregamento do assembly toogenerate redirecionamento Substituir configuração|
|HasCodeBehind|bool|Se o script hello tem code-behind|
|InputDir|string|Diretório dos dados de entrada|
|MessagePath|string|Caminho do arquivo de despejo da mensagem|
|OutputDir|string|Diretório dos dados de saída|
|Paralelismo|int|Álgebra de saudação do paralelismo toorun|
|ParentPid|int|PID do pai Olá nas quais Olá serviço monitora tooexit, conjunto too0 ou tooignore negativo|
|ResultPath|string|Caminho do arquivo de despejo do resultado|
|RuntimeDir|string|Diretório do tempo de execução|
|ScriptPath|string|Onde toofind Olá script|
|Shallow|bool|Compilação superficial ou não|
|TempDir|string|Diretório temporário|
|UseDataBase|string|Especifique a saudação toouse de banco de dados para o código por trás de registro do assembly temporário, mestre por padrão|
|WorkDir|string|Diretório de trabalho preferencial|


**Método**

|Método|Descrição|Retorno|.|
|------|-----------|------|---------|
|public bool DoCompile()|Olá U-SQL script de compilação|Verdadeiro se tiver êxito| |
|public bool DoExec()|Execute o resultado de saudação compilado|Verdadeiro se tiver êxito| |
|public bool DoRun()|Executar script hello U-SQL (compilar + executar)|Verdadeiro se tiver êxito| |
|public bool IsValidRuntimeDir(string path)|Verifique se Olá dado caminho é caminho válido do tempo de execução|Verdadeiro para válido|caminho de saudação do diretório de tempo de execução|


## <a name="faq-about-common-issue"></a>Perguntas frequentes sobre um problema comum

### <a name="error-1"></a>Erro 1:
E_CSC_SYSTEM_INTERNAL: Erro interno. Não foi possível carregar o arquivo ou o assembly “ScopeEngineManaged.dll” ou uma de suas dependências. módulo especificado Olá não pôde ser encontrado.

Verifique o seguinte hello:

- Verifique se você tem o ambiente x64. plataforma de destino de compilação Hello e ambiente de teste de saudação deve ser x64, consulte muito**etapa 1: configuração e projeto de teste de unidade criar c#** acima.
- Verifique se que você copiou todos os arquivos de dependência no diretório de trabalho do NugetPackage\build\runtime\ tooproject.


## <a name="next-steps"></a>Próximas etapas

* toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).
* toolog informações de diagnóstico, consulte [acessar logs de diagnóstico para análise do Azure Data Lake](data-lake-analytics-diagnostic-logs.md).
* toosee uma consulta mais complexa, consulte [analisar logs de site usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* detalhes do trabalho tooview, consulte [navegador de trabalho de uso e a exibição de trabalho de trabalhos da análise Azure Data Lake](data-lake-analytics-data-lake-tools-view-jobs.md).
* exibição de execuções de vértice de saudação toouse, consulte [Olá Use exibição de execuções de vértice no Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
