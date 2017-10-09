---
title: aaaUsing ambientes de teste e Scripts do Windows PowerShell tooPublish tooDev | Microsoft Docs
description: Saiba como toouse do Windows PowerShell scripts de ambientes de teste e toodevelopment toopublish Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>Usando o Windows PowerShell scripts de ambientes de teste e toodev toopublish
Quando você cria um aplicativo web no Visual Studio, você pode gerar um script do Windows PowerShell que você pode usar a publicação Olá tooautomate posterior do seu site tooAzure como um aplicativo Web no serviço de aplicativo do Azure ou uma máquina virtual. Você pode editar e estender seus requisitos de script do Windows PowerShell de saudação em toosuit de editor do Visual Studio hello ou integrar o script hello compilação existente, teste e scripts de publicação.

Usando esses scripts, você pode provisionar versões personalizadas (também conhecidas como ambientes de desenvolvimento e teste) do seu site para uso temporário. Por exemplo, você pode configurar uma versão específica do seu site em uma máquina virtual do Azure ou em Olá slot toorun um site de preparo um conjunto de testes, reproduzir um bug, testar uma correção de bug, avaliação de uma alteração proposta ou configurar um ambiente personalizado para uma demonstração ou apresentação. Depois de criar um script que publique seu projeto, você pode recriar ambientes idênticos executando novamente o script hello conforme necessário, ou executar o script hello com sua própria compilação do seu toocreate de aplicativo web um ambiente personalizado para teste.

## <a name="what-you-need"></a>O que você precisa
* SDK 2.3 do Azure ou posterior. Para saber mais, consulte [Downloads do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384) .

Scripts de Olá Olá SDK do Azure toogenerate não é necessário para projetos web. Esse recurso é para projetos Web, não as funções Web nos serviços de nuvem.

* Azure PowerShell 0.7.4 ou posterior. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou posterior.

## <a name="additional-tools"></a>Ferramentas adicionais
Estão disponíveis ferramentas e recursos adicionais para trabalhar com o PowerShell no Visual Studio para desenvolvimento do Azure. Consulte [Ferramentas do PowerShell para Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Saudação de gerar scripts de publicação
Você pode gerar Olá publicar scripts para uma máquina virtual que hospede seu site quando você cria um projeto novo seguindo [estas instruções](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Você também pode [gerar scripts de publicação para aplicativos Web no Serviço de Aplicativo do Azure](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Scripts gerados pelo Visual Studio
O Visual Studio gera uma pasta de nível de solução chamada **PublishScripts** que contém dois arquivos do Windows PowerShell, um script de publicação para sua máquina virtual ou site e um módulo que contém funções que você pode usar em Olá scripts. O Visual Studio também gera um arquivo no formato JSON Olá que especifica os detalhes de saudação do projeto Olá que você está implantando.

### <a name="windows-powershell-publish-script"></a>Script de publicação do Windows PowerShell
saudação de script de publicação contém específico publicar etapas para implantar o site tooa ou máquina virtual. O Visual Studio fornece sintaxe colorida para o desenvolvimento do Windows PowerShell. Ajuda para funções hello está disponível e pode editar funções Olá Olá script toosuit livremente seus requisitos de alteração.

### <a name="windows-powershell-module"></a>Módulo do Windows PowerShell
Olá módulo que o Visual Studio gera contém funções hello do Windows PowerShell usa script de publicação. Essas são funções do PowerShell do Azure e não são toobe pretendido modificado. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.

### <a name="json-configuration-file"></a>Arquivo de configuração JSON
arquivo JSON de saudação é criado no hello **configurações** pasta e contém dados de configuração que especificam exatamente quais tooAzure de toodeploy de recursos. nome de saudação do arquivo de saudação que o Visual Studio gera é projeto-nome-WAWS-dev se você tiver criado um site ou o nome do projeto-VM-dev se você tiver criado uma máquina virtual. Aqui está um exemplo de um arquivo de configuração JSON é gerado quando você cria um site. A maioria dos valores de saudação são auto-explicativos. nome do site Olá é gerado pelo Azure, portanto não pode coincidir com o nome do projeto.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
Quando você cria uma máquina virtual, o arquivo de configuração JSON Olá parece a seguir toohello semelhante. Observe que um serviço de nuvem é criado como um contêiner para a máquina virtual de saudação. máquina virtual de saudação contém extremidades Olá para o acesso à web via HTTP e HTTPS, bem como pontos de extremidade de implantação da Web, que permite que você publique o site de toohello do seu computador local, a área de trabalho remota e o Windows PowerShell.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Você pode editar Olá JSON configuração toochange o que acontece quando você executar Olá publicar scripts. Olá `cloudService` e `virtualMachine` seções são necessárias, mas você pode excluir Olá `databases` seção se você não precisar dele. Propriedades de saudação vazias no arquivo de configuração do saudação padrão que o Visual Studio gera são opcionais. aqueles que possuem valores no arquivo de configuração padrão de saudação são necessários.

Se você tiver um site que tem vários ambientes de implantação (conhecidos como slots) em vez de um único site de produção no Azure, você pode incluir o nome do slot de saudação em nome de saudação do site Olá no arquivo de configuração JSON hello. Por exemplo, se você tiver um site chamado **mysite** e um slot para ele nomeado **teste** e Olá URI é mysite test.cloudapp.net, mas Olá nome correto toouse no arquivo de configuração de saudação MySite (Test) . Você pode fazer isso apenas se o site da Web hello e slots já existem na sua assinatura. Se não existirem, criar site Olá executando o script hello sem especificar o slot hello, criar slot Olá Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), e depois execute o script de saudação com o nome do site modificado hello. Para obter mais informações sobre os slots de implantação para aplicativos Web, consulte [Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Como toorun Olá publicar scripts
Se você nunca executou um script do Windows PowerShell antes, você deve primeiro definir Olá execução política tooenable scripts toorun. Isso é uma segurança recurso tooprevent que os usuários executem scripts do Windows PowerShell se eles forem vulnerável toomalware ou vírus que envolvem a execução de scripts.

### <a name="run-hello-script"></a>Execute o script hello
1. Crie pacote de implantação da Web Olá para o seu projeto. Um pacote de implantação da Web é um arquivo compactado (arquivo. zip) que contêm arquivos que você deseja toocopy tooyour site ou máquina virtual. Você pode criar pacotes de implantação na Web no Visual Studio para qualquer aplicativo Web.

![Criar pacote de implantação na Web](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Consulte [Como criar um pacote de implantação na Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). Você também pode automatizar a criação de saudação do seu pacote de implantação da Web, conforme descrito na seção de saudação **personalizando e estendendo Olá publicam scripts** mais adiante neste tópico.

1. Em **Solution Explorer**, abra o menu de contexto de saudação de script hello e, em seguida, escolha **abrir com o PowerShell ISE**.
2. Se isso for Olá primeira vez que você executar scripts do Windows PowerShell neste computador, abra uma janela de prompt de comando com privilégios de administrador e Olá tipo comando a seguir:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Entre tooAzure usando o comando a seguir de saudação.

    ```powershell
    Add-AzureAccount
    ```

    Quando solicitado, forneça seu nome de usuário e senha.

    Observe que, quando você automatizar o script hello, esse método para fornecer as credenciais do Azure não funcionará. Em vez disso, você deve usar credenciais de tooprovide de arquivo hello. publishsettings. Uma vez, você use Olá comando **Get-AzurePublishSettingsFile** Olá toodownload do Azure e depois usar **AzurePublishSettingsFile importação** tooimport arquivo de saudação. Para obter instruções detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

4. (Opcional) Se você quiser toocreate Azure recursos como Olá virtual machine, banco de dados e site sem publicar seu aplicativo web, usam Olá **publicar WebApplication.ps1** com hello **-configuração** argumento definido toohello arquivo de configuração de JSON. Esta linha de comando usa Olá toodetermine de arquivo de configuração de JSON que toocreate de recursos. Porque ele usa as configurações padrão de saudação para outros argumentos de linha de comando, cria recursos hello, mas não publica seu aplicativo da web. Hello – opção detalhada fornece mais informações sobre o que está acontecendo.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Saudação de uso **WebApplication.ps1 publicar** conforme mostrado em uma saudação script de saudação tooinvoke exemplos a seguir de comando e publicar seu aplicativo web. Se você precisar toooverride as configurações padrão de saudação para qualquer Olá outros argumentos, como nome da assinatura Olá, nome do pacote, as credenciais de máquina virtual ou credenciais do servidor de banco de dados de publicação, você pode especificar esses parâmetros. Saudação de uso **– Verbose** opção toosee obter mais informações sobre o progresso de saudação Olá processo de publicação.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Se você estiver criando uma máquina virtual, comando Olá Olá seguinte aparência. Este exemplo também mostra como toospecify Olá credenciais para vários bancos de dados. Para Olá máquinas virtuais que esses scripts criam, Olá certificado SSL não é de uma autoridade raiz confiável. Portanto, você precisa Olá toouse **– AllowUntrusted** opção.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    script Hello pode criar bancos de dados, mas não criará os servidores de banco de dados. Se você quiser toocreate um servidor de banco de dados, você pode usar o hello **New-AzureSqlDatabaseServer** função hello módulo do Azure.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Personalizando e estendendo Olá publicam scripts
Você pode personalizar Olá publicar script e o arquivo de configuração JSON. Olá funções no módulo do Windows PowerShell Olá **AzureWebAppPublishModule.psm1** não são toobe pretendido modificado. Se você apenas deseja toospecify um banco de dados diferente ou alterar algumas das propriedades de saudação da máquina virtual de hello, edite o arquivo de configuração de JSON de hello. Se desejar tooextend Olá funcionalidades de saudação script tooautomate compilar e testar seu projeto, você pode implementar stubs de função em **WebApplication.ps1 publicar**.

tooautomate compilar seu projeto, adicione o código que chama o MSBuild muito`New-WebDeployPackage` conforme mostrado neste exemplo de código. Olá caminho toohello comando MSBuild é diferente dependendo da versão de saudação do Visual Studio que você instalou. caminho correto do tooget hello, você pode usar a função hello **Get-MSBuildCmd**, conforme mostrado neste exemplo.

### <a name="tooautomate-building-your-project"></a>tooautomate compilar seu projeto
1. Adicionar Olá `$ProjectFile` parâmetro na seção de parâmetro global hello.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copiar a função hello `Get-MSBuildCmd` em seu arquivo de script.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Substituir `New-WebDeployPackage` com hello seguinte código e substitua os espaços reservados de saudação na construção de linha hello `$msbuildCmd`. Esse código é para o Visual Studio 2015. Se você estiver usando o Visual Studio 2013, alterar Olá **VisualStudioVersion** propriedade abaixo muito`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild seu aplicativo web, use MsBuild.exe. Para obter ajuda, consulte a Referência de linha de comando de MSBuild em: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Iniciar a execução do comando de compilação Olá

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Chamar hello `New-WebDeployPackage` função antes desta linha: `$Config = Read-ConfigFile $Configuration` para aplicativos web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` para máquinas virtuais.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Invocar o script hello personalizado da linha de comando usando passando Olá `$Project` argumento, como saudação de linha de comando de exemplo a seguir.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    tooautomate de teste do seu aplicativo, adicione o código muito`Test-WebApplication`. Ser toouncomment-se de que as linhas de saudação em **WebApplication.ps1 publicar** onde essas funções são chamadas. Se você não fornecer uma implementação, você pode criar manualmente o seu projeto com o Visual Studio e execução Olá publique script toopublish tooAzure.

## <a name="publishing-function-summary"></a>Resumo da função de publicação
tooget ajuda para funções que você pode usar no prompt de comando do Windows PowerShell hello, use o comando de saudação `Get-Help function-name`. Ajuda de saudação inclui exemplos e a Ajuda do parâmetro. Olá mesmo texto de ajuda também está nos arquivos de origem do script hello, **AzureWebAppPublishModule.psm1** e **WebApplication.ps1 publicar**. Ajuda e o script hello está localizadas em seu idioma do Visual Studio.

**AzureWebAppPublishModule**

| Nome da função | Descrição |
| --- | --- |
| Add-AzureSQLDatabase |Cria um novo banco de dados SQL do Azure. |
| Add-AzureSQLDatabases |Cria bancos de dados SQL do Azure dos valores hello no arquivo de configuração do JSON Olá Visual Studio gera. |
| Add-AzureVM |Cria uma máquina virtual do Azure e retorna a que URL de saudação do hello implantado a VM. Olá função configura pré-requisitos hello e, em seguida, Olá chamadas **New-AzureVM** função (módulo do Azure) toocreate uma nova máquina virtual. |
| Add-AzureVMEndpoints |Adiciona a nova máquina de virtual tooa de pontos de extremidade de entrada e retorna Olá máquina de virtual com o novo ponto de extremidade de saudação. |
| Add-AzureVMStorage |Cria uma nova conta de armazenamento do Azure na assinatura atual hello. nome de saudação da conta Olá começa com "devtest" seguido por uma cadeia de caracteres alfanumérica exclusiva. função Hello retorna o nome de Olá Olá novo da conta de armazenamento. Você deve especificar um local ou um grupo de afinidade para a nova conta de armazenamento hello. |
| Add-AzureWebsite |Cria um site com o local e o nome especificado da saudação. Esta função chama Olá **AzureWebsite novo** função hello módulo do Azure. Se a assinatura de saudação já não inclui um site com o nome especificado Olá, esta função cria site hello e retorna um objeto de site. Caso contrário, retornará `$null`. |
| Assinatura de backup |Salva Olá assinatura atual do Azure no hello `$Script:originalSubscription` variável no escopo do script. Esta função salva a assinatura atual do Azure da saudação (conforme obtidas pelo `Get-AzureSubscription -Current`) e a conta de armazenamento e assinatura Olá alterada por esse script (armazenado na variável Olá `$UserSpecifiedSubscription`) e sua conta de armazenamento, no escopo do script. Salvando valores hello, você pode usar uma função, como `Restore-Subscription`, toorestore Olá original atual assinatura e armazenamento toocurrent status da conta se o status atual da saudação foi alterado. |
| Find-AzureVM |Obtém Olá especificado a máquina virtual do Azure. |
| Format-DevTestMessageWithTime |Precede a mensagem de saudação data e hora tooa. Essa função é projetada para mensagens gravadas toohello fluxos de erro e Verbose. |
| Get-AzureSQLDatabaseConnectionString |Monta um conexão cadeia de caracteres tooconnect tooan Azure banco de dados SQL. |
| Get-AzureVMStorage |Retorna Olá nome da conta de armazenamento primeiro Olá com padrão de nome hello "devtest*" (maiusculas e minúsculas) no grupo local ou de afinidade especificado hello. Se hello "devtest*" conta de armazenamento não corresponde à localização hello ou grupo de afinidade, hello função o ignora. Você deve especificar um local ou um grupo de afinidades. |
| Get-MSDeployCmd |Retorna uma ferramenta do comando toorun Olá MsDeploy.exe. |
| New-AzureVMEnvironment |Encontra ou cria uma máquina virtual na assinatura de saudação que corresponde a valores hello no arquivo de configuração JSON hello. |
| Publish-WebPackage |Usa o MsDeploy.exe e um web publicar o pacote. Site tooa de recursos toodeploy de arquivo zip. Essa função não gera nenhuma saída. Se Olá chamada tooMSDeploy.exe falhar, a função hello gera uma exceção. tooget mais detalhado de saída, use Olá **-Verbose** opção. |
| Publish-WebPackageToVM |Verifica os valores de parâmetro hello e, em seguida, chama Olá **publicar WebPackage** função. |
| Read-ConfigFile |Valida o arquivo de configuração do hello JSON e retorna uma tabela de hash de valores selecionados. |
| Restore-Subscription |Redefine Olá atual assinatura toohello assinatura original. |
| Test-AzureModule |Retorna `$true` se a versão do módulo do Azure Olá instalada for 0.7.4 ou posterior. Retorna `$false` se o módulo de saudação não está instalado ou é uma versão anterior. Essa função não tem parâmetros. |
| Test-AzureModuleVersion |Retorna `$true` se a versão de saudação do hello módulo do Azure for 0.7.4 ou posterior. Retorna `$false` se o módulo de saudação não está instalado ou é uma versão anterior. Essa função não tem parâmetros. |
| Test-HttpsUrl |Converte o objeto do hello entrado URL tooa System. URI. Retorna `$True` se Olá URL for absoluta e seu esquema é https. Retorna `$false` se Olá URL for relativa, seu esquema não é HTTPS ou cadeia de caracteres de entrada hello não pode ser convertido tooa URL. |
| Test-Member |Retorna `$true` se uma propriedade ou método é um membro de objeto hello. Caso contrário, retorna `$false`. |
| Write-ErrorWithTime |Grava uma mensagem de erro prefixada com hello hora atual. Esta função chama Olá **DevTestMessageWithTime formato** tempo de saudação do função tooprepend antes de gravar o fluxo de erro de toohello de mensagem de saudação. |
| Write-HostWithTime |Grava um programa de host toohello mensagem (**Write-Host**) prefixados com hello hora atual. efeito de saudação de escrever um programa de host toohello varia. A maioria dos programas que hospedam o Windows PowerShell gravar a essas mensagens de saída de toostandard. |
| Write-VerboseWithTime |Grava uma mensagem detalhada prefixada com hello hora atual. Porque chama **Write-Verbose**, mensagem de saudação exibe apenas quando Olá script é executado com hello **detalhado** parâmetro ou quando Olá **VerbosePreference** preferência é Definir muito**continuar**. |

**Publish-WebApplication**

| Nome da função | Descrição |
| --- | --- |
| New-AzureWebApplicationEnvironment |Cria recursos do Azure, como um site ou uma máquina virtual. |
| New-WebDeployPackage |Essa função não está implementada. Você pode adicionar comandos toobuild essa função seu projeto. |
| Publish-AzureWebApplication |Publica uma tooAzure de aplicativo web. |
| Publish-WebApplication |Cria e implanta aplicativos Web, máquinas virtuais, bancos de dados SQL e contas de armazenamento para um projeto Web do Visual Studio. |
| Test-WebApplication |Essa função não está implementada. Você pode adicionar comandos tootest essa função seu aplicativo. |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre os scripts do PowerShell lendo [scripts com o Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) e ver outros scripts de PowerShell do Azure em Olá [Script Center](https://azure.microsoft.com/documentation/scripts/).
