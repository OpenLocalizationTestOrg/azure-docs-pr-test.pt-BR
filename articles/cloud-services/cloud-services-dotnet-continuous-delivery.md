---
title: "Serviços de entrega de aaaContinuous para a nuvem com o TFS no Azure | Microsoft Docs"
description: "Saiba como aplicativos de nuvem tooset a entrega contínua para o Azure. Exemplos de código para instruções de linha de comando do MSBuild e scripts do PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Fornecimento contínuo de serviços de nuvem no Azure
Olá processo descrito neste artigo mostra como tooset a entrega contínua para aplicativos de nuvem do Azure. Esse processo permite que você crie automaticamente os pacotes e implantar Olá pacote tooAzure após cada check-in do código. Olá, processo de compilação do pacote descrito neste artigo é equivalente toohello **pacote** comando no Visual Studio e as etapas de publicação são equivalente toohello **publicar** comando no Visual Studio.
Olá artigo abrange Olá métodos você usaria toocreate um servidor de compilação com instruções de linha de comando do MSBuild e scripts do Windows PowerShell e ele também demonstra como configurar o Visual Studio Team Foundation Server - definições Team Build toooptionally comandos de MSBuild Olá toouse e scripts do PowerShell. processo de saudação é personalizável para seu ambiente de compilação e ambientes de destino do Azure.

Você também pode usar o Visual Studio Team Services, uma versão do TFS que é hospedado no Azure, toodo isso mais facilmente. 

Antes de começar, você deve publicar seu aplicativo do Visual Studio.
Isso garantirá que todos os recursos de saudação estão disponíveis e inicializado quando você tenta tooautomate processo de publicação de saudação.

## <a name="1-configure-hello-build-server"></a>1: configurar Olá servidor de compilação
Antes de criar um pacote do Azure usando o MSBuild, você deve instalar o software Olá necessárias e as ferramentas no servidor de compilação de saudação.

O Visual Studio não é necessário toobe instalado no servidor de compilação de saudação. Se você quiser toouse Team Foundation Build Service toomanage seu servidor de compilação, siga as instruções de Olá Olá [Team Foundation Build Service] [ Team Foundation Build Service] documentação.

1. No servidor de compilação hello, instalar Olá [do .NET Framework 4.5.2][.NET Framework 4.5.2], que inclui o MSBuild.
2. Instalar hello mais recente [ferramentas de criação do Azure para .NET](https://azure.microsoft.com/develop/net/).
3. Instalar Olá [bibliotecas do Azure para .NET](http://go.microsoft.com/fwlink/?LinkId=623519).
4. Copie o arquivo de WebApplication de saudação de um toohello de instalação do Visual Studio criar o servidor.

   Em um computador com Visual Studio instalado, esse arquivo está localizado no diretório Olá c:\\arquivos de programa (x86)\\MSBuild\\Microsoft\\VisualStudio\\v 14.0\\aplicativos daWeb. Você deve copiá-lo toohello mesmo diretório no servidor de compilação de saudação.
5. Instalar Olá [ferramentas do Azure para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).

## <a name="2-build-a-package-using-msbuild-commands"></a>2: Compilar um Pacote usando comandos MSBuild
Esta seção descreve como tooconstruct um MSBuild comando que cria um pacote do Azure. Execute esta etapa no hello tooverify de servidor de compilação que tudo está configurado corretamente e que o comando de MSBuild Olá o que você deseja toodo. Você pode adicionar essa linha de comando tooexisting criar scripts no servidor de compilação hello, ou você pode usar saudação de linha de comando em uma definição de compilação do TFS, conforme descrito na próxima seção, Olá. Para obter mais informações sobre parâmetros de linha de comando e sobre o MSBuild, consulte [Referência de linha de comando do MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).

1. Se o Visual Studio está instalado no servidor de compilação hello, localize e selecione **Prompt de comando do Visual Studio** em Olá **ferramentas do Visual Studio** pasta no Windows.

   Se o Visual Studio não está instalado no servidor de compilação Olá, abra um prompt de comando e verifique se MSBuild.exe está acessível no caminho. MSBuild é instalado com a saudação do .NET Framework em Olá caminho % WINDIR %\\Microsoft.NET\\Framework\\*versão*. Por exemplo, para adicionar a variável de ambiente MSBuild.exe toohello caminho quando você tiver o .NET Framework 4 instalado, digite hello comando no prompt de comando Olá a seguir:

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. No prompt de comando hello, navegue toohello pasta que contém o arquivo de projeto do Azure que você deseja toobuild.
3. Executar o MSBuild com hello /target: opção como no exemplo a seguir de saudação de publicação:

       MSBuild /target:Publish

   Essa opção pode ser abreviada como /t:Publish. opção de /t:Publish Olá no MSBuild não deve ser confundida com comandos de publicação Olá disponíveis no Visual Studio quando você tiver hello que Azure SDK instalado. Olá /t: opção de publicação somente compilações Olá pacotes do Azure. Não implanta pacotes de saudação assim como os comandos do hello publicar no Visual Studio.

   Opcionalmente, você pode especificar o nome do projeto hello como um parâmetro de MSBuild. Se não for especificado, o diretório atual da saudação é usado. Para saber mais sobre as opções da linha de comando, veja [Referência da linha de comando do MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).
4. Localize a saída de hello. Por padrão, este comando cria um diretório na relação toohello pasta raiz do projeto Olá, como *ProjectDir*\\bin\\*configuração* \\ App.Publish\\. Quando você compila um projeto do Azure, você deve gerar dois arquivos, o próprio arquivo de pacote hello e Olá que acompanha o arquivo de configuração:

   * Project.cspkg
   * ServiceConfiguration.*TargetProfile*.cscfg

   Por padrão, cada projeto do Azure inclui um arquivo de configuração de serviço (arquivo .cscfg) para compilações locais (depuração) e outro para compilações de nuvem (de preparo ou produção), mas você pode adicionar ou remover arquivos de configuração de serviço conforme necessário. Quando você criar um pacote do Visual Studio, você será solicitado que tooinclude de arquivo de configuração de serviço junto com o pacote de saudação.
5. Especifique o arquivo de configuração do serviço de saudação. Quando você criar um pacote usando o MSBuild, o arquivo de configuração do serviço local hello está incluído por padrão. tooinclude um arquivo de configuração de serviço diferentes, defina a propriedade TargetProfile do comando de MSBuild hello, como no exemplo a seguir de saudação:

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. Especifique o local de saudação para saída de hello. Definir o caminho de saudação usando o /p: publishdir =*diretório* \\ opção, incluindo Olá separador de barra invertida, como no exemplo a seguir de saudação à direita:

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   Depois de criada e testada uma MSBuild apropriado toobuild de linha de comando seus projetos e combiná-los em um pacote do Azure, você pode adicionar scripts de compilação de tooyour essa linha de comando. Se seu servidor de compilação usar scripts personalizados, esse processo dependerá das especificidades de seu processo de compilação personalizado. Se você estiver usando o TFS como um ambiente de compilação, você pode seguir instruções Olá Olá próxima etapa tooadd Olá pacote do Azure compilação tooyour processo de compilação.

## <a name="3-build-a-package-using-tfs-team-build"></a>3: Compilar um Pacote usando o TFS Team Build
Se você tiver Team Foundation Server (TFS) configurado como um controlador de compilação e hello criar servidor configurado como um computador de compilação do TFS, opcionalmente, você pode configurar uma compilação automatizada para seu pacote do Azure. Para obter informações sobre como tooset backup e usar o Team Foundation server como um sistema de compilação, consulte [seu sistema de compilação em expansão][Scale out your build system]. Em particular, o procedimento a seguir supõe que você configurou seu servidor de compilação conforme descrito em [implantar e configurar um servidor de compilação][Deploy and configure a build server], e que você tenha criado um projeto de equipe criado uma nuvem projeto de serviço no projeto de equipe hello.

tooconfigure TFS toobuild Azure pacotes, executar Olá etapas a seguir:

1. No Visual Studio no computador de desenvolvimento, no menu de exibição hello, escolha **Team Explorer**, ou escolha Ctrl +\\, Ctrl + M. Na janela do Team Explorer, expanda Olá **cria** nó ou escolha Olá **cria** página e selecione **nova definição de compilação**.

   ![Opção Nova Definição de Compilação][0]
2. Escolha Olá **gatilho** guia e, em seguida, especifique a saudação desejado condições para quando você quiser Olá toobe pacote criado. Por exemplo, especificar **integração contínua** ocorre de pacote de saudação toobuild sempre que o check-in de controle de uma origem.
3. Escolha Olá **configurações de fonte de** guia e certifique-se de sua pasta de projeto está listada na Olá **pasta de controle de origem** coluna, e o status de saudação é **Active**.
4. Escolha Olá **padrões de compilação** guia e no controlador de compilação, verifique o nome de saudação do servidor de compilação de saudação.  Além disso, escolha a opção de saudação **seguinte de toohello de saída de compilação de cópia Remover pasta** e especifique o local de destino Olá desejado.
5. Escolha Olá **processo** guia. Na guia do processo hello, escolher o modelo de padrão de saudação, em **criar**, escolha o projeto de saudação se não ainda estiver selecionada e expanda Olá **avançado** seção Olá **Build**seção da grade de saudação.
6. Escolha **argumentos de MSBuild**e defina os argumentos de linha de comando do MSBuild apropriados Olá conforme descrito na etapa 2 acima. Por exemplo, digite **/t: publicar /p: publishdir =\\\\myserver\\descarta\\**  toobuild um pacote de saudação do pacote e copiar arquivos de local de toohello \\ \\myserver\\descarta\\:

   ![Argumentos do MSBuild][2]

   > [!NOTE]
   > Copiando Olá arquivos tooa compartilhamento público torna mais fácil toomanually implantar pacotes de saudação do seu computador de desenvolvimento.
7. Testar o sucesso de saudação da etapa de compilação verificando-se em um projeto de tooyour de alteração ou enfileirar uma nova compilação. tooqueue a uma nova compilação no Team Explorer, clique com botão direito **todas as definições de compilação,** e, em seguida, escolha **enfileirar nova compilação**.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4: Publicar um Pacote usando um Script do PowerShell
Esta seção descreve como tooconstruct um script do Windows PowerShell que publicará o pacote de aplicativos de nuvem Olá saída tooAzure usando parâmetros opcionais. Esse script pode ser chamado após a etapa de compilação de saudação na sua automação de compilação personalizada. Ele também pode ser chamado das atividades do fluxo de trabalho do Modelo de processo no Visual Studio TFS Team Build.

1. Instalar Olá [cmdlets do PowerShell do Azure] [ Azure PowerShell cmdlets] (v0.6.1 ou superior).
   Durante a fase de instalação do cmdlet hello, escolha tooinstall como um snap-in. Observe que esta versão com suporte oficialmente substitui a versão mais antiga do hello oferecido por meio do CodePlex, embora as versões anteriores do hello foram numeradas 2.x.x.
2. Inicie o PowerShell do Azure usando o menu de início de saudação ou página inicial. Se você iniciar dessa forma, Olá cmdlets do PowerShell do Azure será carregado.
3. No prompt do PowerShell hello, verifique se Olá cmdlets do PowerShell são carregados digitando o comando parcial Olá `Get-Azure` e, em seguida, pressionar Olá a tecla Tab para conclusão de instrução.

   Se você pressionar a tecla Tab de saudação repetidamente, você verá vários comandos do PowerShell do Azure.
4. Verifique se que você pode conectar tooyour assinatura do Azure importando as informações de assinatura de arquivo. publishsettings de saudação.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   Em seguida, insira o comando Olá

   `Get-AzureSubscription`

   Isso mostra informações sobre sua assinatura. Verifique se tudo está correto.
5. Salvar modelo de script hello fornecido no final da saudação deste artigo para a pasta de scripts, como c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.
6. Examine a seção de parâmetros de saudação do script hello. Adicione ou modifique os valores padrão. Esses valores podem ser substituídos sempre passando parâmetros explícitos.
7. Certifique-se de serviço de nuvem válido e não contas de armazenamento criadas na sua assinatura que pode ser afetada por Olá script de publicação. A conta de armazenamento (armazenamento de blob) será usado tooupload e armazenar temporariamente o arquivo de pacote e a configuração de implantação de saudação durante a implantação está sendo criada.

   * toocreate um novo serviço de nuvem, você pode chamar esse script ou Olá [portal do Azure](https://portal.azure.com). nome do serviço de nuvem Olá será usado como um prefixo em um nome de domínio totalmente qualificado e, portanto, ele deve ser exclusivo.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * toocreate uma nova conta de armazenamento, você pode chamar esse script ou Olá [portal do Azure](https://portal.azure.com). o nome de conta de armazenamento Olá será usado como um prefixo em um nome de domínio totalmente qualificado e, portanto, ele deve ser exclusivo. Você pode tentar usar Olá mesmo nome do serviço de nuvem.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Chamar o script hello diretamente do PowerShell do Azure ou conectar este toooccur de automação de compilação do script tooyour host após a compilação do pacote de saudação.

   > [!IMPORTANT]
   > script Hello serão sempre excluir ou substituir as implantações existentes por padrão, se eles são detectados. Isso é necessário para habilitar o fornecimento contínuo de automação onde não é possível nenhum aviso ao usuário.
   >
   >

   **Cenário de exemplo 1:** toohello implantação contínua preparação do ambiente de serviço:

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   Isso é normalmente seguido pela verificação da execução de teste e uma troca de VIP. permuta de VIP de saudação pode ser feita por meio de saudação [portal do Azure](https://portal.azure.com) ou usando o cmdlet Olá Move-implantação.

   **Cenário de exemplo 2:** ambiente de produção toohello implantação contínua de um serviço de teste dedicados

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **Área de trabalho remota:**

   Se a área de trabalho remota está habilitada no seu projeto do Azure, você precisará tooperform etapas única adicionais Olá tooensure que certificado de serviço de nuvem correto é carregado tooall serviços de nuvem direcionados por esse script.

   Localize valores de impressão digital do certificado Olá esperados por suas funções. Os valores de impressão digital são visíveis na seção de certificados de saudação do arquivo de configuração de nuvem (ou seja, ServiceConfiguration). Também é visível na caixa de diálogo de configuração da área de trabalho remota de saudação no Visual Studio quando você Mostrar opções e exibir hello selecionado certificado.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   Carregar certificados de área de trabalho remota como uma etapa de configuração única usando Olá cmdlet script a seguir:

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   Por exemplo:

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   Como alternativa, você pode exportar arquivo de certificado PFX Olá com chave privada e carregar certificados tooeach serviço de destino nuvem usando o [portal do Azure](https://portal.azure.com).

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **Atualizar implantação vs. Excluir Implantação -\> Nova Implantação**

   Olá script por padrão executará uma implantação de atualização ($enableDeploymentUpgrade = 1) quando nenhum parâmetro é passado ou o valor 1 é passado explicitamente. Para instâncias únicas isso tem a vantagem de levar menos tempo do que uma implantação completa. Para instâncias que exigem alta disponibilidade, que isso também tem a vantagem de saudação de deixar algumas instâncias em execução enquanto outros são atualizadas (percorrer seu domínio de atualização), além de seu VIP não será excluído.

   Implantação de atualização pode ser desabilitada no script hello ($enableDeploymentUpgrade = 0) ou passando *- enableDeploymentUpgrade 0* como um parâmetro, que altera a exclusão do script comportamento toofirst qualquer implantação existente e, em seguida, criar um nova implantação.

   > [!IMPORTANT]
   > script Hello serão sempre excluir ou substituir as implantações existentes por padrão, se eles são detectados. Isso é necessário para habilitar o fornecimento contínuo de automação onde é possível sem nenhum aviso ao usuário/operador.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5: Publicar um Pacote usando o TFS Team Build
Esta etapa opcional conecta o TFS Team Build toohello script criado na etapa 4, que manipula a publicação de tooAzure de compilação do pacote de saudação. Isso envolve a modificação Olá usada por sua definição de compilação para que ele executa uma atividade de publicação no final de saudação do fluxo de trabalho de saudação do modelo de processo. Hello atividade publicar executará o comando PowerShell passando parâmetros de compilação de saudação. Saída de hello MSBuild tem como alvo e script de publicação será conectada na saída de compilação padrão hello.

1. Editar saudação definição de compilação responsável por contínua implantar.
2. Selecione Olá **processo** guia.
3. Execute [estas instruções](http://msdn.microsoft.com/library/dd647551.aspx) tooadd um projeto de atividade para hello criar modelo de processo, baixe o modelo padrão de saudação, adicioná-lo ao projeto Olá e check-in. Dê um novo nome, como AzureBuildProcessTemplate de modelo de processo de compilação de saudação.
4. Retornar toohello **processo** guia e usar **Mostrar detalhes** tooshow uma lista de modelos de processo de compilação disponível. Escolha Olá **New...**  botão e, em seguida, navegue toohello projeto recém-adicionado e check-in. Localize o modelo Olá recém-criado e escolha **Okey**.
5. Abra Olá selecionada do modelo de processo para edição. Você pode abrir diretamente no designer de fluxo de trabalho de saudação ou no hello toowork de editor de XML com hello XAML.
6. Adicione Olá lista de argumentos novos a seguir como itens separados de linha na guia de argumentos de saudação do designer de fluxo de trabalho de saudação. Todos os argumentos devem ter direção =In e digite =String. Esses serão usados tooflow parâmetros da definição de compilação Olá no fluxo de trabalho hello, quais Olá de toocall usado get, em seguida, o script de publicação.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista de argumentos][3]

   Olá que correspondente XAML tem esta aparência:

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. Adicione uma nova sequência de final de saudação do executar no agente:

   1. Comece adicionando um toocheck de atividade de instrução If para um arquivo de script válida. Defina o valor de toothis de condição de saudação:

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. Em Olá caso de Olá instrução If, adicione uma nova atividade de sequência. Publicar too'Start de nome de exibição do conjunto de saudação '
   3. Com hello início publicar sequência ainda selecionada, adicione a seguinte lista de novas variáveis como itens separados de linha na guia variáveis de designer de fluxo de trabalho de saudação. Todas as variáveis devem ter um tipo de Variável =String e Escopo=Início da publicação. Esses serão usados tooflow parâmetros da definição de compilação Olá no fluxo de trabalho, quais Olá de toocall usado get, em seguida, o script de publicação.

      * SubscriptionDataFilePath, do tipo String
      * PublishScriptFilePath, do tipo String

        ![Novas variáveis][4]
   4. Se você estiver usando o TFS 2012 ou anterior, adicionar uma atividade de ConvertWorkspaceItem no início de saudação do hello nova sequência. Se você estiver usando o TFS 2013 ou posterior, adicione uma atividade de GetLocalPath no início de saudação da nova sequência de saudação. Para um ConvertWorkspaceItem, definir propriedades de saudação da seguinte maneira: direção = ServerToLocal, DisplayName = 'Converter a publicação de nome de arquivo de script', entrada = 'PublishScriptLocation', resultado = 'PublishScriptFilePath', espaço de trabalho = 'Espaço de trabalho'. Para uma atividade de GetLocalPath, defina Olá propriedade IncomingPath too'PublishScriptLocation', e Olá too'PublishScriptFilePath de resultado '. Este toohello de caminho hello atividade converte publicar script a partir de locais do servidor TFS (se aplicável) tooa caminho de disco local padrão.
   5. Se você estiver usando o TFS 2012 ou anterior, adicione outra atividade de ConvertWorkspaceItem final Olá Olá nova sequência. Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'. Se estiver usando o TFS 2013 ou posterior, adicione outra atividade GetLocalPath. IncomingPath='SubscriptionDataFileLocation' e Result='SubscriptionDataFilePath.'
   6. Adicionar uma atividade de InvokeProcess final Olá Olá nova sequência.
      Essa chamadas de atividade PowerShell.exe com argumentos Olá passado por Olá definição de compilação.

      + Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)
      + DisplayName = Execute publish script
      + FileName = "PowerShell" (incluir aspas Olá)
      + OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)
   7. Em Olá **tratar saída padrão** seção o InvokeProcess de texto, defina too'data de valor de caixa de texto de saudação '. Este é um dados de saída padrão de saudação toostore variável.
   8. Adicionar uma atividade WriteBuildMessage logo abaixo Olá **tratar saída padrão** seção. Definir Olá importância = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' e mensagem de saudação = 'data'. Isso garante que a saída padrão de saudação do script será gravada toohello saída da compilação.
   9. Em Olá **tratar a saída de erro** seção o InvokeProcess de texto, defina too'data de valor de caixa de texto de saudação '. Este é um toostore variável de dados de erro padrão de saudação.
   10. Adicionar uma atividade WriteBuildError logo abaixo Olá **tratar a saída de erro** seção. Defina a mensagem de saudação = 'data'. Isso garante que erros de padrão de saudação do script hello serão gravados toohello saída de erro de compilação.
   11. Corrija quaisquer erros, indicados por sinais de exclamação azuis. Passe o mouse sobre o pontos de exclamação tooget uma dica sobre o erro de saudação. Salve fluxo de trabalho de saudação para limpar os erros.

   resultado final Olá Olá publicar atividades terá esta aparência no designer de saudação do fluxo de trabalho:

   ![Atividades do fluxo de trabalho][5]

   resultado final Olá Olá publicar atividades terá esta aparência em XAML de fluxo de trabalho:

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. Salve fluxo de trabalho modelo processo de compilação de saudação e Check-In deste arquivo.
9. Editar definição de compilação da saudação (fechá-lo se ele já estiver aberto) e selecione hello **novo** botão se você ainda não ver Olá novo modelo na lista de saudação de modelos de processo.
10. Defina valores de propriedade de parâmetro de saudação em Olá Misc seção da seguinte maneira:

    1. CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Esse valor é derivado de: ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Esse valor é derivado de: ($PublishDir)($ProjectName).cspkg*
    3. PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = 'mycloudservicename' *a nome de serviço de nuvem apropriado de saudação de uso aqui*
    5. Ambiente = 'Teste'
    6. StorageAccountName = 'mystorageaccountname' *a nome de conta de armazenamento apropriado de saudação de uso aqui*
    7. SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'
    8. SubscriptionName = 'padrão'

    ![Valores de propriedade do parâmetro][6]
11. Salve alterações de saudação toohello definição de compilação.
12. Fila tooexecute uma compilação ambos Olá compilação do pacote e publicação. Se você tiver um gatilho definido tooContinuous integração, você executará esse comportamento em cada check-in.

### <a name="publishcloudserviceps1-script-template"></a>Modelo de script PublishCloudService.ps1
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>Próximas etapas
depuração remota tooenable ao usar a entrega contínua, consulte [habilitar a depuração remota ao usar a entrega contínua toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
