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
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="80644-103">Usando o Windows PowerShell scripts de ambientes de teste e toodev toopublish</span><span class="sxs-lookup"><span data-stu-id="80644-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="80644-104">Quando você cria um aplicativo web no Visual Studio, você pode gerar um script do Windows PowerShell que você pode usar a publicação Olá tooautomate posterior do seu site tooAzure como um aplicativo Web no serviço de aplicativo do Azure ou uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80644-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="80644-105">Você pode editar e estender seus requisitos de script do Windows PowerShell de saudação em toosuit de editor do Visual Studio hello ou integrar o script hello compilação existente, teste e scripts de publicação.</span><span class="sxs-lookup"><span data-stu-id="80644-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="80644-106">Usando esses scripts, você pode provisionar versões personalizadas (também conhecidas como ambientes de desenvolvimento e teste) do seu site para uso temporário.</span><span class="sxs-lookup"><span data-stu-id="80644-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="80644-107">Por exemplo, você pode configurar uma versão específica do seu site em uma máquina virtual do Azure ou em Olá slot toorun um site de preparo um conjunto de testes, reproduzir um bug, testar uma correção de bug, avaliação de uma alteração proposta ou configurar um ambiente personalizado para uma demonstração ou apresentação.</span><span class="sxs-lookup"><span data-stu-id="80644-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="80644-108">Depois de criar um script que publique seu projeto, você pode recriar ambientes idênticos executando novamente o script hello conforme necessário, ou executar o script hello com sua própria compilação do seu toocreate de aplicativo web um ambiente personalizado para teste.</span><span class="sxs-lookup"><span data-stu-id="80644-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="80644-109">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="80644-109">What you need</span></span>
* <span data-ttu-id="80644-110">SDK 2.3 do Azure ou posterior.</span><span class="sxs-lookup"><span data-stu-id="80644-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="80644-111">Para saber mais, consulte [Downloads do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384) .</span><span class="sxs-lookup"><span data-stu-id="80644-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="80644-112">Scripts de Olá Olá SDK do Azure toogenerate não é necessário para projetos web.</span><span class="sxs-lookup"><span data-stu-id="80644-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="80644-113">Esse recurso é para projetos Web, não as funções Web nos serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="80644-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="80644-114">Azure PowerShell 0.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="80644-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="80644-115">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="80644-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="80644-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="80644-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="80644-117">Ferramentas adicionais</span><span class="sxs-lookup"><span data-stu-id="80644-117">Additional tools</span></span>
<span data-ttu-id="80644-118">Estão disponíveis ferramentas e recursos adicionais para trabalhar com o PowerShell no Visual Studio para desenvolvimento do Azure.</span><span class="sxs-lookup"><span data-stu-id="80644-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="80644-119">Consulte [Ferramentas do PowerShell para Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="80644-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="80644-120">Saudação de gerar scripts de publicação</span><span class="sxs-lookup"><span data-stu-id="80644-120">Generating hello publish scripts</span></span>
<span data-ttu-id="80644-121">Você pode gerar Olá publicar scripts para uma máquina virtual que hospede seu site quando você cria um projeto novo seguindo [estas instruções](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80644-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="80644-122">Você também pode [gerar scripts de publicação para aplicativos Web no Serviço de Aplicativo do Azure](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="80644-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="80644-123">Scripts gerados pelo Visual Studio</span><span class="sxs-lookup"><span data-stu-id="80644-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="80644-124">O Visual Studio gera uma pasta de nível de solução chamada **PublishScripts** que contém dois arquivos do Windows PowerShell, um script de publicação para sua máquina virtual ou site e um módulo que contém funções que você pode usar em Olá scripts.</span><span class="sxs-lookup"><span data-stu-id="80644-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="80644-125">O Visual Studio também gera um arquivo no formato JSON Olá que especifica os detalhes de saudação do projeto Olá que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="80644-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="80644-126">Script de publicação do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="80644-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="80644-127">saudação de script de publicação contém específico publicar etapas para implantar o site tooa ou máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80644-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="80644-128">O Visual Studio fornece sintaxe colorida para o desenvolvimento do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80644-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="80644-129">Ajuda para funções hello está disponível e pode editar funções Olá Olá script toosuit livremente seus requisitos de alteração.</span><span class="sxs-lookup"><span data-stu-id="80644-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="80644-130">Módulo do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="80644-130">Windows PowerShell module</span></span>
<span data-ttu-id="80644-131">Olá módulo que o Visual Studio gera contém funções hello do Windows PowerShell usa script de publicação.</span><span class="sxs-lookup"><span data-stu-id="80644-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="80644-132">Essas são funções do PowerShell do Azure e não são toobe pretendido modificado.</span><span class="sxs-lookup"><span data-stu-id="80644-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="80644-133">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="80644-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="80644-134">Arquivo de configuração JSON</span><span class="sxs-lookup"><span data-stu-id="80644-134">JSON configuration file</span></span>
<span data-ttu-id="80644-135">arquivo JSON de saudação é criado no hello **configurações** pasta e contém dados de configuração que especificam exatamente quais tooAzure de toodeploy de recursos.</span><span class="sxs-lookup"><span data-stu-id="80644-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="80644-136">nome de saudação do arquivo de saudação que o Visual Studio gera é projeto-nome-WAWS-dev se você tiver criado um site ou o nome do projeto-VM-dev se você tiver criado uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80644-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="80644-137">Aqui está um exemplo de um arquivo de configuração JSON é gerado quando você cria um site.</span><span class="sxs-lookup"><span data-stu-id="80644-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="80644-138">A maioria dos valores de saudação são auto-explicativos.</span><span class="sxs-lookup"><span data-stu-id="80644-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="80644-139">nome do site Olá é gerado pelo Azure, portanto não pode coincidir com o nome do projeto.</span><span class="sxs-lookup"><span data-stu-id="80644-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="80644-140">Quando você cria uma máquina virtual, o arquivo de configuração JSON Olá parece a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="80644-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="80644-141">Observe que um serviço de nuvem é criado como um contêiner para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="80644-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="80644-142">máquina virtual de saudação contém extremidades Olá para o acesso à web via HTTP e HTTPS, bem como pontos de extremidade de implantação da Web, que permite que você publique o site de toohello do seu computador local, a área de trabalho remota e o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80644-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="80644-143">Você pode editar Olá JSON configuração toochange o que acontece quando você executar Olá publicar scripts.</span><span class="sxs-lookup"><span data-stu-id="80644-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="80644-144">Olá `cloudService` e `virtualMachine` seções são necessárias, mas você pode excluir Olá `databases` seção se você não precisar dele.</span><span class="sxs-lookup"><span data-stu-id="80644-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="80644-145">Propriedades de saudação vazias no arquivo de configuração do saudação padrão que o Visual Studio gera são opcionais. aqueles que possuem valores no arquivo de configuração padrão de saudação são necessários.</span><span class="sxs-lookup"><span data-stu-id="80644-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="80644-146">Se você tiver um site que tem vários ambientes de implantação (conhecidos como slots) em vez de um único site de produção no Azure, você pode incluir o nome do slot de saudação em nome de saudação do site Olá no arquivo de configuração JSON hello.</span><span class="sxs-lookup"><span data-stu-id="80644-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="80644-147">Por exemplo, se você tiver um site chamado **mysite** e um slot para ele nomeado **teste** e Olá URI é mysite test.cloudapp.net, mas Olá nome correto toouse no arquivo de configuração de saudação MySite (Test) .</span><span class="sxs-lookup"><span data-stu-id="80644-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="80644-148">Você pode fazer isso apenas se o site da Web hello e slots já existem na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="80644-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="80644-149">Se não existirem, criar site Olá executando o script hello sem especificar o slot hello, criar slot Olá Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), e depois execute o script de saudação com o nome do site modificado hello.</span><span class="sxs-lookup"><span data-stu-id="80644-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="80644-150">Para obter mais informações sobre os slots de implantação para aplicativos Web, consulte [Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="80644-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="80644-151">Como toorun Olá publicar scripts</span><span class="sxs-lookup"><span data-stu-id="80644-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="80644-152">Se você nunca executou um script do Windows PowerShell antes, você deve primeiro definir Olá execução política tooenable scripts toorun.</span><span class="sxs-lookup"><span data-stu-id="80644-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="80644-153">Isso é uma segurança recurso tooprevent que os usuários executem scripts do Windows PowerShell se eles forem vulnerável toomalware ou vírus que envolvem a execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="80644-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="80644-154">Execute o script hello</span><span class="sxs-lookup"><span data-stu-id="80644-154">Run hello script</span></span>
1. <span data-ttu-id="80644-155">Crie pacote de implantação da Web Olá para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="80644-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="80644-156">Um pacote de implantação da Web é um arquivo compactado (arquivo. zip) que contêm arquivos que você deseja toocopy tooyour site ou máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80644-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="80644-157">Você pode criar pacotes de implantação na Web no Visual Studio para qualquer aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="80644-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Criar pacote de implantação na Web](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="80644-159">Consulte [Como criar um pacote de implantação na Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="80644-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="80644-160">Você também pode automatizar a criação de saudação do seu pacote de implantação da Web, conforme descrito na seção de saudação **personalizando e estendendo Olá publicam scripts** mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="80644-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="80644-161">Em **Solution Explorer**, abra o menu de contexto de saudação de script hello e, em seguida, escolha **abrir com o PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="80644-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="80644-162">Se isso for Olá primeira vez que você executar scripts do Windows PowerShell neste computador, abra uma janela de prompt de comando com privilégios de administrador e Olá tipo comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="80644-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="80644-163">Entre tooAzure usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="80644-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="80644-164">Quando solicitado, forneça seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="80644-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="80644-165">Observe que, quando você automatizar o script hello, esse método para fornecer as credenciais do Azure não funcionará.</span><span class="sxs-lookup"><span data-stu-id="80644-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="80644-166">Em vez disso, você deve usar credenciais de tooprovide de arquivo hello. publishsettings.</span><span class="sxs-lookup"><span data-stu-id="80644-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="80644-167">Uma vez, você use Olá comando **Get-AzurePublishSettingsFile** Olá toodownload do Azure e depois usar **AzurePublishSettingsFile importação** tooimport arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="80644-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="80644-168">Para obter instruções detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80644-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="80644-169">(Opcional) Se você quiser toocreate Azure recursos como Olá virtual machine, banco de dados e site sem publicar seu aplicativo web, usam Olá **publicar WebApplication.ps1** com hello **-configuração** argumento definido toohello arquivo de configuração de JSON.</span><span class="sxs-lookup"><span data-stu-id="80644-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="80644-170">Esta linha de comando usa Olá toodetermine de arquivo de configuração de JSON que toocreate de recursos.</span><span class="sxs-lookup"><span data-stu-id="80644-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="80644-171">Porque ele usa as configurações padrão de saudação para outros argumentos de linha de comando, cria recursos hello, mas não publica seu aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="80644-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="80644-172">Hello – opção detalhada fornece mais informações sobre o que está acontecendo.</span><span class="sxs-lookup"><span data-stu-id="80644-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="80644-173">Saudação de uso **WebApplication.ps1 publicar** conforme mostrado em uma saudação script de saudação tooinvoke exemplos a seguir de comando e publicar seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="80644-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="80644-174">Se você precisar toooverride as configurações padrão de saudação para qualquer Olá outros argumentos, como nome da assinatura Olá, nome do pacote, as credenciais de máquina virtual ou credenciais do servidor de banco de dados de publicação, você pode especificar esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="80644-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="80644-175">Saudação de uso **– Verbose** opção toosee obter mais informações sobre o progresso de saudação Olá processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="80644-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="80644-176">Se você estiver criando uma máquina virtual, comando Olá Olá seguinte aparência.</span><span class="sxs-lookup"><span data-stu-id="80644-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="80644-177">Este exemplo também mostra como toospecify Olá credenciais para vários bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="80644-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="80644-178">Para Olá máquinas virtuais que esses scripts criam, Olá certificado SSL não é de uma autoridade raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="80644-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="80644-179">Portanto, você precisa Olá toouse **– AllowUntrusted** opção.</span><span class="sxs-lookup"><span data-stu-id="80644-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="80644-180">script Hello pode criar bancos de dados, mas não criará os servidores de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="80644-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="80644-181">Se você quiser toocreate um servidor de banco de dados, você pode usar o hello **New-AzureSqlDatabaseServer** função hello módulo do Azure.</span><span class="sxs-lookup"><span data-stu-id="80644-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="80644-182">Personalizando e estendendo Olá publicam scripts</span><span class="sxs-lookup"><span data-stu-id="80644-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="80644-183">Você pode personalizar Olá publicar script e o arquivo de configuração JSON.</span><span class="sxs-lookup"><span data-stu-id="80644-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="80644-184">Olá funções no módulo do Windows PowerShell Olá **AzureWebAppPublishModule.psm1** não são toobe pretendido modificado.</span><span class="sxs-lookup"><span data-stu-id="80644-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="80644-185">Se você apenas deseja toospecify um banco de dados diferente ou alterar algumas das propriedades de saudação da máquina virtual de hello, edite o arquivo de configuração de JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="80644-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="80644-186">Se desejar tooextend Olá funcionalidades de saudação script tooautomate compilar e testar seu projeto, você pode implementar stubs de função em **WebApplication.ps1 publicar**.</span><span class="sxs-lookup"><span data-stu-id="80644-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="80644-187">tooautomate compilar seu projeto, adicione o código que chama o MSBuild muito`New-WebDeployPackage` conforme mostrado neste exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="80644-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="80644-188">Olá caminho toohello comando MSBuild é diferente dependendo da versão de saudação do Visual Studio que você instalou.</span><span class="sxs-lookup"><span data-stu-id="80644-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="80644-189">caminho correto do tooget hello, você pode usar a função hello **Get-MSBuildCmd**, conforme mostrado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="80644-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="80644-190">tooautomate compilar seu projeto</span><span class="sxs-lookup"><span data-stu-id="80644-190">tooautomate building your project</span></span>
1. <span data-ttu-id="80644-191">Adicionar Olá `$ProjectFile` parâmetro na seção de parâmetro global hello.</span><span class="sxs-lookup"><span data-stu-id="80644-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="80644-192">Copiar a função hello `Get-MSBuildCmd` em seu arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="80644-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="80644-193">Substituir `New-WebDeployPackage` com hello seguinte código e substitua os espaços reservados de saudação na construção de linha hello `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="80644-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="80644-194">Esse código é para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="80644-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="80644-195">Se você estiver usando o Visual Studio 2013, alterar Olá **VisualStudioVersion** propriedade abaixo muito`12.0`.</span><span class="sxs-lookup"><span data-stu-id="80644-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="80644-196">toobuild seu aplicativo web, use MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="80644-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="80644-197">Para obter ajuda, consulte a Referência de linha de comando de MSBuild em: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="80644-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="80644-198">Iniciar a execução do comando de compilação Olá</span><span class="sxs-lookup"><span data-stu-id="80644-198">Start execution of hello build command</span></span>

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

1. <span data-ttu-id="80644-199">Chamar hello `New-WebDeployPackage` função antes desta linha: `$Config = Read-ConfigFile $Configuration` para aplicativos web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` para máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="80644-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="80644-200">Invocar o script hello personalizado da linha de comando usando passando Olá `$Project` argumento, como saudação de linha de comando de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="80644-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="80644-201">tooautomate de teste do seu aplicativo, adicione o código muito`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="80644-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="80644-202">Ser toouncomment-se de que as linhas de saudação em **WebApplication.ps1 publicar** onde essas funções são chamadas.</span><span class="sxs-lookup"><span data-stu-id="80644-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="80644-203">Se você não fornecer uma implementação, você pode criar manualmente o seu projeto com o Visual Studio e execução Olá publique script toopublish tooAzure.</span><span class="sxs-lookup"><span data-stu-id="80644-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="80644-204">Resumo da função de publicação</span><span class="sxs-lookup"><span data-stu-id="80644-204">Publishing function summary</span></span>
<span data-ttu-id="80644-205">tooget ajuda para funções que você pode usar no prompt de comando do Windows PowerShell hello, use o comando de saudação `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="80644-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="80644-206">Ajuda de saudação inclui exemplos e a Ajuda do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="80644-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="80644-207">Olá mesmo texto de ajuda também está nos arquivos de origem do script hello, **AzureWebAppPublishModule.psm1** e **WebApplication.ps1 publicar**.</span><span class="sxs-lookup"><span data-stu-id="80644-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="80644-208">Ajuda e o script hello está localizadas em seu idioma do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80644-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="80644-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="80644-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="80644-210">Nome da função</span><span class="sxs-lookup"><span data-stu-id="80644-210">Function name</span></span> | <span data-ttu-id="80644-211">Descrição</span><span class="sxs-lookup"><span data-stu-id="80644-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80644-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="80644-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="80644-213">Cria um novo banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="80644-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="80644-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="80644-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="80644-215">Cria bancos de dados SQL do Azure dos valores hello no arquivo de configuração do JSON Olá Visual Studio gera.</span><span class="sxs-lookup"><span data-stu-id="80644-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="80644-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="80644-216">Add-AzureVM</span></span> |<span data-ttu-id="80644-217">Cria uma máquina virtual do Azure e retorna a que URL de saudação do hello implantado a VM.</span><span class="sxs-lookup"><span data-stu-id="80644-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="80644-218">Olá função configura pré-requisitos hello e, em seguida, Olá chamadas **New-AzureVM** função (módulo do Azure) toocreate uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80644-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="80644-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="80644-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="80644-220">Adiciona a nova máquina de virtual tooa de pontos de extremidade de entrada e retorna Olá máquina de virtual com o novo ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="80644-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="80644-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="80644-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="80644-222">Cria uma nova conta de armazenamento do Azure na assinatura atual hello.</span><span class="sxs-lookup"><span data-stu-id="80644-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="80644-223">nome de saudação da conta Olá começa com "devtest" seguido por uma cadeia de caracteres alfanumérica exclusiva.</span><span class="sxs-lookup"><span data-stu-id="80644-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="80644-224">função Hello retorna o nome de Olá Olá novo da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="80644-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="80644-225">Você deve especificar um local ou um grupo de afinidade para a nova conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="80644-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="80644-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="80644-226">Add-AzureWebsite</span></span> |<span data-ttu-id="80644-227">Cria um site com o local e o nome especificado da saudação.</span><span class="sxs-lookup"><span data-stu-id="80644-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="80644-228">Esta função chama Olá **AzureWebsite novo** função hello módulo do Azure.</span><span class="sxs-lookup"><span data-stu-id="80644-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="80644-229">Se a assinatura de saudação já não inclui um site com o nome especificado Olá, esta função cria site hello e retorna um objeto de site.</span><span class="sxs-lookup"><span data-stu-id="80644-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="80644-230">Caso contrário, retornará `$null`.</span><span class="sxs-lookup"><span data-stu-id="80644-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="80644-231">Assinatura de backup</span><span class="sxs-lookup"><span data-stu-id="80644-231">Backup-Subscription</span></span> |<span data-ttu-id="80644-232">Salva Olá assinatura atual do Azure no hello `$Script:originalSubscription` variável no escopo do script. Esta função salva a assinatura atual do Azure da saudação (conforme obtidas pelo `Get-AzureSubscription -Current`) e a conta de armazenamento e assinatura Olá alterada por esse script (armazenado na variável Olá `$UserSpecifiedSubscription`) e sua conta de armazenamento, no escopo do script.</span><span class="sxs-lookup"><span data-stu-id="80644-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="80644-233">Salvando valores hello, você pode usar uma função, como `Restore-Subscription`, toorestore Olá original atual assinatura e armazenamento toocurrent status da conta se o status atual da saudação foi alterado.</span><span class="sxs-lookup"><span data-stu-id="80644-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="80644-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="80644-234">Find-AzureVM</span></span> |<span data-ttu-id="80644-235">Obtém Olá especificado a máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="80644-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="80644-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="80644-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="80644-237">Precede a mensagem de saudação data e hora tooa.</span><span class="sxs-lookup"><span data-stu-id="80644-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="80644-238">Essa função é projetada para mensagens gravadas toohello fluxos de erro e Verbose.</span><span class="sxs-lookup"><span data-stu-id="80644-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="80644-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="80644-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="80644-240">Monta um conexão cadeia de caracteres tooconnect tooan Azure banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="80644-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="80644-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="80644-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="80644-242">Retorna Olá nome da conta de armazenamento primeiro Olá com padrão de nome hello "devtest*" (maiusculas e minúsculas) no grupo local ou de afinidade especificado hello. Se hello "devtest*" conta de armazenamento não corresponde à localização hello ou grupo de afinidade, hello função o ignora.</span><span class="sxs-lookup"><span data-stu-id="80644-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="80644-243">Você deve especificar um local ou um grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="80644-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="80644-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="80644-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="80644-245">Retorna uma ferramenta do comando toorun Olá MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="80644-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="80644-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="80644-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="80644-247">Encontra ou cria uma máquina virtual na assinatura de saudação que corresponde a valores hello no arquivo de configuração JSON hello.</span><span class="sxs-lookup"><span data-stu-id="80644-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="80644-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="80644-248">Publish-WebPackage</span></span> |<span data-ttu-id="80644-249">Usa o MsDeploy.exe e um web publicar o pacote. Site tooa de recursos toodeploy de arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="80644-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="80644-250">Essa função não gera nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="80644-250">This function doesn't generate any output.</span></span> <span data-ttu-id="80644-251">Se Olá chamada tooMSDeploy.exe falhar, a função hello gera uma exceção.</span><span class="sxs-lookup"><span data-stu-id="80644-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="80644-252">tooget mais detalhado de saída, use Olá **-Verbose** opção.</span><span class="sxs-lookup"><span data-stu-id="80644-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="80644-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="80644-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="80644-254">Verifica os valores de parâmetro hello e, em seguida, chama Olá **publicar WebPackage** função.</span><span class="sxs-lookup"><span data-stu-id="80644-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="80644-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="80644-255">Read-ConfigFile</span></span> |<span data-ttu-id="80644-256">Valida o arquivo de configuração do hello JSON e retorna uma tabela de hash de valores selecionados.</span><span class="sxs-lookup"><span data-stu-id="80644-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="80644-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="80644-257">Restore-Subscription</span></span> |<span data-ttu-id="80644-258">Redefine Olá atual assinatura toohello assinatura original.</span><span class="sxs-lookup"><span data-stu-id="80644-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="80644-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="80644-259">Test-AzureModule</span></span> |<span data-ttu-id="80644-260">Retorna `$true` se a versão do módulo do Azure Olá instalada for 0.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="80644-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="80644-261">Retorna `$false` se o módulo de saudação não está instalado ou é uma versão anterior.</span><span class="sxs-lookup"><span data-stu-id="80644-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="80644-262">Essa função não tem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="80644-262">This function has no parameters.</span></span> |
| <span data-ttu-id="80644-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="80644-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="80644-264">Retorna `$true` se a versão de saudação do hello módulo do Azure for 0.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="80644-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="80644-265">Retorna `$false` se o módulo de saudação não está instalado ou é uma versão anterior.</span><span class="sxs-lookup"><span data-stu-id="80644-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="80644-266">Essa função não tem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="80644-266">This function has no parameters.</span></span> |
| <span data-ttu-id="80644-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="80644-267">Test-HttpsUrl</span></span> |<span data-ttu-id="80644-268">Converte o objeto do hello entrado URL tooa System. URI.</span><span class="sxs-lookup"><span data-stu-id="80644-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="80644-269">Retorna `$True` se Olá URL for absoluta e seu esquema é https.</span><span class="sxs-lookup"><span data-stu-id="80644-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="80644-270">Retorna `$false` se Olá URL for relativa, seu esquema não é HTTPS ou cadeia de caracteres de entrada hello não pode ser convertido tooa URL.</span><span class="sxs-lookup"><span data-stu-id="80644-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="80644-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="80644-271">Test-Member</span></span> |<span data-ttu-id="80644-272">Retorna `$true` se uma propriedade ou método é um membro de objeto hello.</span><span class="sxs-lookup"><span data-stu-id="80644-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="80644-273">Caso contrário, retorna `$false`.</span><span class="sxs-lookup"><span data-stu-id="80644-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="80644-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="80644-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="80644-275">Grava uma mensagem de erro prefixada com hello hora atual.</span><span class="sxs-lookup"><span data-stu-id="80644-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="80644-276">Esta função chama Olá **DevTestMessageWithTime formato** tempo de saudação do função tooprepend antes de gravar o fluxo de erro de toohello de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="80644-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="80644-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="80644-277">Write-HostWithTime</span></span> |<span data-ttu-id="80644-278">Grava um programa de host toohello mensagem (**Write-Host**) prefixados com hello hora atual.</span><span class="sxs-lookup"><span data-stu-id="80644-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="80644-279">efeito de saudação de escrever um programa de host toohello varia.</span><span class="sxs-lookup"><span data-stu-id="80644-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="80644-280">A maioria dos programas que hospedam o Windows PowerShell gravar a essas mensagens de saída de toostandard.</span><span class="sxs-lookup"><span data-stu-id="80644-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="80644-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="80644-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="80644-282">Grava uma mensagem detalhada prefixada com hello hora atual.</span><span class="sxs-lookup"><span data-stu-id="80644-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="80644-283">Porque chama **Write-Verbose**, mensagem de saudação exibe apenas quando Olá script é executado com hello **detalhado** parâmetro ou quando Olá **VerbosePreference** preferência é Definir muito**continuar**.</span><span class="sxs-lookup"><span data-stu-id="80644-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="80644-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="80644-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="80644-285">Nome da função</span><span class="sxs-lookup"><span data-stu-id="80644-285">Function name</span></span> | <span data-ttu-id="80644-286">Descrição</span><span class="sxs-lookup"><span data-stu-id="80644-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80644-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="80644-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="80644-288">Cria recursos do Azure, como um site ou uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80644-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="80644-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="80644-289">New-WebDeployPackage</span></span> |<span data-ttu-id="80644-290">Essa função não está implementada.</span><span class="sxs-lookup"><span data-stu-id="80644-290">This function isn't implemented.</span></span> <span data-ttu-id="80644-291">Você pode adicionar comandos toobuild essa função seu projeto.</span><span class="sxs-lookup"><span data-stu-id="80644-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="80644-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="80644-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="80644-293">Publica uma tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="80644-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="80644-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="80644-294">Publish-WebApplication</span></span> |<span data-ttu-id="80644-295">Cria e implanta aplicativos Web, máquinas virtuais, bancos de dados SQL e contas de armazenamento para um projeto Web do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80644-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="80644-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="80644-296">Test-WebApplication</span></span> |<span data-ttu-id="80644-297">Essa função não está implementada.</span><span class="sxs-lookup"><span data-stu-id="80644-297">This function isn't implemented.</span></span> <span data-ttu-id="80644-298">Você pode adicionar comandos tootest essa função seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80644-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80644-299">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80644-299">Next steps</span></span>
<span data-ttu-id="80644-300">Saiba mais sobre os scripts do PowerShell lendo [scripts com o Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) e ver outros scripts de PowerShell do Azure em Olá [Script Center](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="80644-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
