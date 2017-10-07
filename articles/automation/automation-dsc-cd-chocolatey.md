---
title: "aaaAzure implantação contínua de DSC de automação com Chocolatey | Microsoft Docs"
description: "Implantação contínua de DevOps usando DSC de Automação do Azure e o gerenciador de pacotes Chocolatey.  Exemplo com modelo ARM JSON completo e fonte do PowerShell."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>Exemplo de uso: Implantação contínua tooVirtual máquinas usando DSC de automação e Chocolatey
Em um mundo de DevOps há muitos tooassist ferramentas com vários pontos no pipeline de integração contínua hello.  Configuração de estado do Azure Automation desejado (DSC) é um opções de toohello de adição de novos bem-vindo que utilizam a equipes de DevOps.  Este artigo demonstra a configuração da CD (Implantação Contínua) para um computador com Windows.  Você pode estender facilmente Olá técnica tooinclude tantos computadores Windows conforme necessário na função hello (um site da web, por exemplo) e de lá tooadditional funções também.

![Implantação contínua para VMs do IaaS](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>Em um alto nível
Há bem pouco acontecendo aqui, mas, felizmente, é possível dividir tudo em dois processos principais: 

* Escrevendo código e testá-lo, em seguida, criar e publicar pacotes de instalação para as versões principais e secundárias do sistema de saudação. 
* Criar e gerenciar máquinas virtuais que irão instalar e executar o código de saudação em pacotes de saudação.  

Depois que esses dois principais processos estão em vigor, é um pacote de saudação etapa curto tooautomatically atualização em execução em uma VM específica como novas versões são criadas e implantadas.

## <a name="component-overview"></a>Visão geral do componente
Os gerentes do pacote como [apt get](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) são bastante conhecidos no Linux Olá, mundo, mas não tanto no mundo do Windows hello.  [Chocolatey](https://chocolatey.org/) é tal uma coisa e de Scott Hanselman [blog](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) em Olá tópico é uma ótima introdução.  Resumindo, Chocolatey permite tooinstall pacotes de um repositório central de pacotes em um sistema do Windows usando a linha de comando hello.  Você pode criar e gerenciar seu próprio repositório, e o Chocolatey pode instalar pacotes de qualquer repositório que você designar.

Estado de configuração desejado (DSC) ([visão geral](https://technet.microsoft.com/library/dn249912.aspx)) é uma ferramenta do PowerShell que permite que você toodeclare Olá configuração para uma máquina.  Por exemplo, você pode dizer: "Quero o Chocolatey instalado, quero o IIS instalado, quero a porta 80 aberta, quero a versão 1.0.0 de meu site instalada".  Olá DSC Gerenciador de configurações Local (LCM) implementa essa configuração. Um Servidor de recepção da DSC mantém um repositório de configurações para seus computadores. Olá LCM em cada computador verifica no toosee periodicamente se sua configuração corresponde à configuração armazenada hello. Ele pode relatar o status ou tentativa de máquina de saudação toobring no alinhamento com a configuração armazenada hello. Você pode editar Olá configuração armazenada em Olá pull server toocause uma máquina ou conjunto de máquinas toocome alinhada com a configuração de saudação alterada.

Automação do Azure é um serviço gerenciado no Microsoft Azure que permite que você tooautomate várias tarefas usando runbooks, nós, credenciais, recursos e ativos como variáveis globais e agendas. DSC de automação do Azure estende essa automação ferramentas do recurso tooinclude DSC do PowerShell.  Confira uma excelente [visão geral](automation-dsc-overview.md).

Um Recurso DSC é um módulo de código que tem recursos específicos, como gerenciar redes, o Active Directory ou o SQL Server.  Olá Chocolatey recurso de DSC sabe como tooaccess um servidor do NuGet (entre outros), baixe os pacotes, pacotes de instalação e assim por diante.  Há muitos outros recursos de DSC em Olá [Galeria do PowerShell](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title).  Esses módulos são instalados no Servidor de Recepção da DSC de Automação do Azure (por você) para que possam ser usados por suas configurações.

Os modelos do Resource Manager fornecem uma maneira declarativa de gerar sua infraestrutura (itens como redes, sub-redes, roteamento e segurança de rede, balanceadores de carga, NICs, VMs e assim por diante).  Aqui está uma [artigo](../azure-resource-manager/resource-manager-deployment-model.md) que compara Olá modelo de implantação do Gerenciador de recursos (declarativo) com hello Azure Service Management (ASM ou clássico) implantação de modelo (obrigatória) e discute o recurso de núcleo Olá provedores, computação, armazenamento e rede.

Um recurso importante de um modelo do Gerenciador de recursos é sua capacidade tooinstall uma extensão de VM na VM de saudação conforme ela é provisionada.  Uma extensão de VM tem recursos específicos, como executar um script personalizado, instalar software antivírus ou executar um script de configuração de DSC.  Há muitos outros tipos de extensões de VM.

## <a name="quick-trip-around-hello-diagram"></a>Processamento rápido em torno do diagrama de saudação
Iniciando na parte superior do hello, você escreve seu código, compilar e testar e criar um pacote de instalação.  O Chocolatey pode manipular vários tipos de pacotes de instalação, como MSI, MSU e ZIP.  E você tem toda a capacidade de instalação real do PowerShell toodo Olá Olá se recursos nativos do Chocolatey não são bastante o tooit.  Coloque o pacote de saudação em algum lugar acessível – um repositório de pacotes.  Este exemplo de uso usa uma pasta pública em uma conta de armazenamento de blob do Azure, mas pode estar em qualquer outro lugar.  O Chocolatey funciona nativamente com servidores do NuGet e alguns outras para o gerenciamento de metadados de pacote.  [Este artigo](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) descreve opções de saudação.  Este exemplo de uso usa o NuGet.  Um Nuspec consiste em metadados sobre seus pacotes.  saudação Nuspec é "compilado" do NuPkg e armazenado em um servidor do NuGet.  Quando sua configuração solicita um pacote por nome e faz referência a um servidor do NuGet, Olá Chocolatey recurso de DSC (agora em Olá VM) captura pacote hello e instala para você.  Você também pode solicitar uma versão específica de um pacote.

Olá inferior esquerdo parte imagem hello, há um modelo do Azure Resource Manager (ARM).  Neste exemplo de uso, Olá extensão de VM registra Olá VM com hello o servidor de Pull de DSC do Azure Automation (isto é, um servidor de pull) como um nó.  Olá configuração é armazenada no servidor de pull de saudação.  Na verdade, ela é armazenada duas vezes: uma vez como texto sem formatação e uma vez compilada como um arquivo MOF (para aqueles que os conhecem.)  No portal de saudação Olá MOF é uma configuração de nó"" (como toosimply contrário "configuração").  Sua saudação artefato associado a um nó para que nó Olá saiba sua configuração.  Os detalhes abaixo mostram como tooassign Olá nó de toohello de configuração do nó.

Presume-se já estiver fazendo bit Olá na parte superior do hello, ou a maioria dos-lo.  Criando nuspec hello, compilação e armazená-los em um servidor do NuGet são uma coisa pequena.  E você já está gerenciando VMs.  Levar Olá próxima etapa toocontinuous implantação requer a configuração de servidor de pull de saudação (uma vez), registrar os nós com ele (uma vez) e criar e armazenar a configuração de saudação existe (inicialmente).  Como os pacotes são atualizados e implantados toohello repositório, atualize hello configuração e configuração de nó no servidor de pull da saudação (repetir conforme necessário).

Se você não estiver começando com um modelo do ARM, isso também está OK.  Há PowerShell cmdlets projetados toohelp registrar suas VMs com o servidor de pull hello e Olá resto. Para obter mais detalhes, confira este artigo: [Integrando máquinas para o gerenciamento pelo DSC de Automação do Azure](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>Etapa 1: Configuração de conta de automação e de servidor de pull Olá
Em uma linha de comando do PowerShell (Adicionar AzureRmAccount) autenticada: (pode levar alguns minutos enquanto o servidor de recepção de saudação é configurado)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

Você pode colocar sua conta de automação em qualquer Olá regiões (também conhecido como local) a seguir: Leste dos EUA 2, Centro Sul dos EUA, nós Gov Virgínia, Europa Ocidental, Sudeste da Ásia, Leste do Japão, Índia Central e Sudeste da Austrália, Canadá Central, Norte da Europa.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>Etapa 2: Extensão de VM ajustes toohello modelo do ARM
Detalhes de registro VM (usando a extensão de VM de DSC do PowerShell Olá) fornecido neste [modelo de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver).  Esta etapa registra sua nova VM com o servidor de pull Olá na lista de saudação de nós de DSC.  Parte do registro está especificando Olá configuração toobe aplicada toohello nós.  Essa configuração de nó ainda não tiver tooexist no servidor de pull hello, portanto é Okey etapa 4 é onde isso é feito para Olá primeira vez.  Mas aqui na etapa 2 você precisa toohave nome hello decidiu nó de saudação e nome de saudação da configuração de saudação.  Neste exemplo de uso, o nó de saudação é 'isvbox' e Olá configuração 'ISVBoxConfig'.  Portanto, nome de configuração de nó hello (toobe especificado em DeploymentTemplate.json) é 'ISVBoxConfig.isvbox'.  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>Etapa 3: Adicionando necessário servidor de pull de DSC recursos toohello
Olá Galeria do PowerShell é instrumentado tooinstall recursos de DSC em sua conta de automação do Azure.  Navegue toohello recurso desejado e clique botão de "Implantar tooAzure automação" hello.

![Exemplo da Galeria do PowerShell](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

Outra técnica adicionado recentemente toohello Portal do Azure permite que você toopull em novos módulos ou módulos de atualização existente. Clique em recursos da conta de automação de hello, bloco de ativos de saudação e, finalmente, bloco de módulos de saudação.  ícone de procurar Galeria Olá permite toosee lista Olá módulos Galeria hello, fazer drill down nos detalhes e, por fim, importar para a conta de automação. Isso é uma ótima maneira tookeep seus módulos backup toodate de tootime de tempo. Além disso, o recurso de importação Olá verifica as dependências com outros tooensure módulos que nada obtém fora de sincronia.

Ou, não há abordagem manual hello.  estrutura de pastas de saudação de um módulo de integração para um computador com o Windows PowerShell é um pouco diferente da estrutura de pastas de saudação esperada pelo Olá automação do Azure.  Isso exige que você faça alguns ajustes.  Mas não é difícil, e isso é feito apenas uma vez por recurso (a menos que você deseja tooupgrade-lo no futuro.)  Para saber mais sobre como criar Módulos de Integração do PowerShell, confira este artigo: [Criando Módulos de Integração para a Automação do Azure](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/)

* Instale o módulo de saudação que são necessários em sua estação de trabalho, da seguinte maneira:
  * Instale o [Windows Management Framework, v5](http://aka.ms/wmf5latest) (não é necessário para o Windows 10)
  * `Install-Module –Name MODULE-NAME`< — captura Olá módulo a partir da saudação Galeria do PowerShell 
* Pasta de módulo de saudação de cópia de `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` pasta temp tooa 
* Excluir amostras e documentação da pasta principal Olá 
* Pasta principal do ZIP hello, nomear o arquivo ZIP de saudação exatamente Olá mesmo como pasta Olá 
* Coloque o arquivo ZIP de saudação em um local acessível de HTTP, como o armazenamento de blob em uma conta de armazenamento do Azure.
* Execute este PowerShell:
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

exemplo Hello incluído executa estas etapas para cChoco e xNetworking. Consulte Olá [notas](#notes) para tratamento especial para cChoco.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>Etapa 4: Adicionando um servidor de pull Olá nó configuração toohello
Não há nada especial sobre Olá primeira vez que você importar sua configuração para a compilação e o servidor de pull de saudação.  Importação subsequentes/compila todos da saudação mesma aparência configuração exatamente Olá mesmo.  Cada vez que o pacote de atualização e precisa toopush-tooproduction você executar essa etapa depois de verificar o arquivo de configuração de saudação está correto – incluindo Olá nova versão do pacote.  Aqui está o arquivo de configuração de saudação e do PowerShell:

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

New-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

Esses resultados de etapas em uma nova configuração de nó nomeado "ISVBoxConfig.isvbox" que está sendo colocado no servidor de pull de saudação.  nome de configuração de nó de saudação é compilado como "configurationName.nodeName".

## <a name="step-5-creating-and-maintaining-package-metadata"></a>Etapa 5: criar e manter metadados de pacote
Para cada pacote que você colocar em um repositório de pacotes de saudação, é necessário um nuspec que descreve a ele.  Esse nuspec deve ser compilado e armazenado em seu servidor do NuGet. Este processo é descrito [aqui](http://docs.nuget.org/create/creating-and-publishing-a-package).  Você pode usar MyGet.org como um servidor do NuGet.  Eles vendem este serviço, mas há uma SKU inicial que é gratuita.  Em NuGet.org, você encontrará instruções sobre como instalar seu próprio servidor do NuGet para seus pacotes privados.

## <a name="step-6-tying-it-all-together"></a>Etapa 6: reunir tudo isso
Cada vez que uma versão passa o controle de qualidade e for aprovada para implantação, Olá pacote é criado, nuspec nupkg e atualizados implantado toohello NuGet server.  Além disso, a configuração de saudação (etapa 4 acima) deve ser tooagree atualizada com novo número de versão hello.  Ele deve ser enviado do servidor de pull toohello e compilado.  A partir desse ponto em diante, é máquinas virtuais toohello que dependem dessa atualização da configuração toopull hello e instalá-lo.  Cada uma dessas atualizações é simples - apenas uma ou duas linhas do PowerShell.  No caso de saudação do Visual Studio Team Services, algumas delas são encapsuladas em tarefas de compilação que podem ser encadeadas em uma compilação.  Este [artigo](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery) fornece mais detalhes.  Isso [repositório GitHub](https://github.com/Microsoft/vso-agent-tasks) detalhes Olá várias tarefas de build disponíveis.

## <a name="notes"></a>Observações
Este exemplo de uso inicia com uma máquina virtual de uma imagem do Windows Server 2012 R2 genérica de saudação Galeria do Azure.  Você pode iniciar a partir de qualquer imagem armazenada e, em seguida, ajustar a partir daí com configuração de DSC hello.  No entanto, a alteração de configuração é baked em uma imagem é muito mais difícil do que a atualização dinâmica de configuração de saudação usando DSC.

Você não tem toouse um modelo do ARM e toouse de extensão VM Olá essa técnica com suas VMs.  E suas VMs não tem toobe toobe do Azure sob gerenciamento do CD.  Tudo o que é necessário é que Chocolatey ser instalado e hello LCM configurado no hello VM para que ele saiba onde hello servidor de pull é.  

É claro que, quando você atualiza um pacote em uma VM que está em produção, é necessário tootake VM da rotação enquanto Olá atualização está instalada.  A maneira de fazer isso varia muito.  Por exemplo, com uma VM por trás de um Balanceador de Carga do Azure, você pode adicionar uma Sonda Personalizada.  Ao atualizar Olá VM, ter ponto de extremidade de investigação de saudação retornar um 400.  Olá ajuste necessário toocause essa alteração pode ser dentro de sua configuração, que pode Olá tooswitch ajuste-o novamente tooreturning uma resposta 200 após a conclusão da atualização de saudação.

O código-fonte completo deste exemplo de uso está [neste projeto do Visual Studio](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) no GitHub.

## <a name="related-articles"></a>Artigos relacionados
* [Visão geral da DSC da Automação do Azure](automation-dsc-overview.md)
* [cmdlets da DSC de Automação do Azure](https://msdn.microsoft.com/library/mt244122.aspx)
* [Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure](automation-dsc-onboarding.md)

