---
title: "<span data-ttu-id=\"c297a-101\">Criar um Módulo de Integração da Automação do Azure | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"c297a-101\">Create an Azure Automation Integration Module | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"c297a-102\">Tutorial que explica a criação, os testes e o uso de exemplo dos módulos de integração na Automação do Azure.</span><span class=\"sxs-lookup\"><span data-stu-id=\"c297a-102\">Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.</span></span>"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: aeb06276a52e5472667ae0a741fb3007a91910fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="c297a-103">Módulos de integração de automação do Azure</span><span class="sxs-lookup"><span data-stu-id="c297a-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="c297a-104">O PowerShell é a tecnologia fundamental por trás da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c297a-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="c297a-105">Como a Automação do Azure foi desenvolvida sobre o PowerShell, os módulos do PowerShell são fundamentais para a extensibilidade da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c297a-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="c297a-106">Neste artigo, orientaremos você pelas questões específicas da utilização de módulos do PowerShell pela Automação do Azure, chamados de “Módulos de Integração”, e as práticas recomendadas para a criação de seus próprios módulos do PowerShell para ter certeza de que eles funcionam como Módulos de Integração dentro da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c297a-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="c297a-107">O que é um módulo do PowerShell?</span><span class="sxs-lookup"><span data-stu-id="c297a-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="c297a-108">Um módulo do PowerShell é um grupo de cmdlets do PowerShell, como **Get-Date** ou **Copy-Item**, que pode ser usado no console do PowerShell, em scripts, fluxos de trabalho, runbooks e em recursos de DSC do PowerShell, como WindowsFeature ou File, que podem ser usados por meio das configurações de DSC do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c297a-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="c297a-109">Toda a funcionalidade do PowerShell é exposta por meio de cmdlets e recursos de DSC, e todo cmdlet/recurso de DSC tem o suporte de um módulo do PowerShell, muitos deles acompanham o próprio PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c297a-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="c297a-110">Por exemplo, o cmdlet **Get-Date** faz parte do módulo Microsoft.PowerShell.Utility do PowerShell, e o cmdlet **Copy-Item** faz parte do módulo Microsoft.PowerShell.Management do PowerShell, e o recurso Package DSC faz parte do módulo PSDesiredStateConfiguration do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c297a-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="c297a-111">Esses dois módulos são fornecidos com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c297a-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="c297a-112">Porém, muitos módulos do PowerShell não acompanham o PowerShell, mas são distribuídos com produtos internos ou de terceiros, como o System Center 2012 Configuration Manager, ou pela vasta comunidade do PowerShell, em locais como a Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c297a-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="c297a-113">Os módulos são úteis porque simplificam tarefas complexas por meio de funcionalidade encapsulada.</span><span class="sxs-lookup"><span data-stu-id="c297a-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="c297a-114">Saiba mais sobre [Módulos do PowerShell no MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c297a-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="c297a-115">O que é um Módulo de Integração da Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="c297a-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="c297a-116">Um Módulo de Integração não é muito diferente de um módulo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c297a-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="c297a-117">É simplesmente um módulo do PowerShell que contém, opcionalmente, um arquivo adicional: um arquivo de metadados que especifica um tipo de conexão de Automação do Azure a ser usado com os cmdlets do módulo em runbooks.</span><span class="sxs-lookup"><span data-stu-id="c297a-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="c297a-118">Com o arquivo opcional ou não, esses módulos do PowerShell podem ser importados na Automação do Azure a fim de disponibilizar seus cmdlets para uso dentro de runbooks, e disponibilizar os recursos de DSC para utilização em configurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="c297a-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="c297a-119">Nos bastidores, a Automação do Azure armazena esses módulos, e no momento da execução do trabalho do runbook e do trabalho de compilação do DSC os carrega nas áreas restritas da Automação do Azure, onde os runbooks são executados e as configurações de DSC são compiladas.</span><span class="sxs-lookup"><span data-stu-id="c297a-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="c297a-120">Quaisquer recursos de DSC em módulos também são colocados automaticamente no servidor de recepção do DSC de Automação, de modo que eles possam ser obtidos por máquinas que tentarem aplicar configurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="c297a-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="c297a-121">Fornecemos diversos módulos do Azure PowerShell na Automação do Azure para que você possa começar a automatizar o gerenciamento do Azure imediatamente, mas você pode importar os módulos do PowerShell para qualquer sistema, serviço ou ferramenta com o qual deseja realizar a integração.</span><span class="sxs-lookup"><span data-stu-id="c297a-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="c297a-122">Determinados módulos são fornecidos como "módulos globais" no serviço de Automação.</span><span class="sxs-lookup"><span data-stu-id="c297a-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="c297a-123">Esses módulos globais estão disponíveis quando você cria uma conta de automação, e os atualizamos às vezes, o que os envia automaticamente à sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="c297a-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="c297a-124">Se não quiser que eles sejam atualizados automaticamente, você sempre poderá importar o mesmo módulo por conta própria, e ele terá precedência sobre a versão de módulo global desse módulo que fornecemos no serviço.</span><span class="sxs-lookup"><span data-stu-id="c297a-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="c297a-125">O formato no qual você importa um pacote do Módulo de Integração é um arquivo compactado com o mesmo nome que o módulo e com uma extensão .zip.</span><span class="sxs-lookup"><span data-stu-id="c297a-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="c297a-126">Ele contém o módulo do Windows PowerShell e quaisquer arquivos de suporte, incluindo um arquivo de manifesto (.psd1), se o módulo tiver um.</span><span class="sxs-lookup"><span data-stu-id="c297a-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="c297a-127">Se o módulo precisar conter um tipo de conexão da Automação do Azure, também deverá conter um arquivo com o nome `<ModuleName>-Automation.json` que especifica as propriedades do tipo de conexão.</span><span class="sxs-lookup"><span data-stu-id="c297a-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="c297a-128">Esse é um arquivo json colocando dentro da pasta do módulo de seu arquivo .zip compactado, e contém os campos de uma “conexão” necessária para conectar ao sistema ou serviço representado pelo módulo.</span><span class="sxs-lookup"><span data-stu-id="c297a-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="c297a-129">Com isso, um tipo de conexão será criado na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c297a-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="c297a-130">Com esse arquivo você pode definir os nomes de campo, os tipos e se os campos devem ser criptografados e/ou opcionais, para o tipo de conexão do módulo.</span><span class="sxs-lookup"><span data-stu-id="c297a-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="c297a-131">Veja a seguir um modelo no formato de arquivo json:</span><span class="sxs-lookup"><span data-stu-id="c297a-131">The following is a template in the json file format:</span></span>

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

<span data-ttu-id="c297a-132">Se você tiver implantado a Service Management Automation e criado pacotes do Módulo de Integração para seus runbooks de automação, tudo isso será bastante familiar para você.</span><span class="sxs-lookup"><span data-stu-id="c297a-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="c297a-133">Práticas recomendadas de criação</span><span class="sxs-lookup"><span data-stu-id="c297a-133">Authoring Best Practices</span></span>
<span data-ttu-id="c297a-134">Embora os módulos de integração sejam essencialmente os módulos do PowerShell, ainda há uma série de itens a considerar durante a criação de um módulo do PowerShell, para torná-lo mais útil na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c297a-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="c297a-135">Algumas deles são específicas à Automação do Azure, e outras são úteis apenas para fazer seus módulos funcionarem bem no Fluxo de Trabalho do PowerShell, independentemente de você usar ou não a Automação.</span><span class="sxs-lookup"><span data-stu-id="c297a-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="c297a-136">Incluem uma sinopse, uma descrição e um URI de ajuda para cada cmdlet no módulo.</span><span class="sxs-lookup"><span data-stu-id="c297a-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="c297a-137">No PowerShell, você pode usar o cmdlet **Get-Help** para definir certas informações de ajuda com relação aos cmdlets para que o usuário receba ajuda sobre como usá-los.</span><span class="sxs-lookup"><span data-stu-id="c297a-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="c297a-138">Por exemplo, veja como você pode definir uma sinopse e um URI de ajuda para um módulo do PowerShell escrito em um arquivo .psm1.</span><span class="sxs-lookup"><span data-stu-id="c297a-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> <span data-ttu-id="c297a-139">Fornecer essas informações não apenas mostrará esta Ajuda usando o cmdlet **Get-Help** no console do PowerShell, mas também exporá essa funcionalidade de ajuda na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c297a-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="c297a-140">Por exemplo, ao inserir atividades durante a criação de runbooks.</span><span class="sxs-lookup"><span data-stu-id="c297a-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="c297a-141">Clicar em "Exibir ajuda detalhada" abrirá o URI de ajuda em outra guia do navegador da Web que você está usando para acessar a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c297a-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="c297a-142">![Ajuda do Módulo de Integração](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="c297a-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="c297a-143">Se o módulo for executado em um sistema remoto,</span><span class="sxs-lookup"><span data-stu-id="c297a-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="c297a-144">a.</span><span class="sxs-lookup"><span data-stu-id="c297a-144">a.</span></span> <span data-ttu-id="c297a-145">Ele deverá conter um arquivo de metadados do Módulo de Integração que define as informações necessárias para se conectar a esse sistema remoto, ou seja, tipo de conexão.</span><span class="sxs-lookup"><span data-stu-id="c297a-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="c297a-146">b.</span><span class="sxs-lookup"><span data-stu-id="c297a-146">b.</span></span> <span data-ttu-id="c297a-147">Cada cmdlet no módulo deve ser capaz de receber um objeto de conexão (uma instância desse tipo de conexão) como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c297a-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="c297a-148">Fica mais fácil usar os cmdlets no módulo na Automação do Azure se você permitir a passagem de um objeto com os campos do tipo de conexão como um parâmetro para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c297a-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="c297a-149">Dessa forma, os usuários não precisam mapear parâmetros do ativo de conexão para os parâmetros correspondentes do cmdlet sempre que eles chamarem um cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c297a-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="c297a-150">Com base no exemplo de runbook acima, ele usa um ativo de conexão Twilio chamado CorpTwilio para acessar o Twilio e retornar todos os números de telefone na conta.</span><span class="sxs-lookup"><span data-stu-id="c297a-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="c297a-151">Você observou como ele está mapeando os campos da conexão para os parâmetros do cmdlet?</span><span class="sxs-lookup"><span data-stu-id="c297a-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="c297a-152">Uma maneira mais fácil e adequada de abordar isso é passando diretamente o objeto de conexão para o cmdlet -</span><span class="sxs-lookup"><span data-stu-id="c297a-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="c297a-153">Você pode habilitar um comportamento como esse para seus cmdlets permitindo que eles aceitem um objeto de conexão diretamente como um parâmetro, em vez de apenas campos de conexão para parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c297a-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="c297a-154">Normalmente, convém ter um conjunto de parâmetros para cada um, para que um usuário que não esteja usando a Automação do Azure possa chamar seus cmdlets sem construir uma tabela de hash para agir como o objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="c297a-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="c297a-155">O conjunto de parâmetros **SpecifyConnectionFields** abaixo é usado para passar as propriedades do campo de conexão, individualmente.</span><span class="sxs-lookup"><span data-stu-id="c297a-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="c297a-156">**UseConnectionObject** permite que você passe a conexão diretamente.</span><span class="sxs-lookup"><span data-stu-id="c297a-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="c297a-157">Como você pode ver, o cmdlet Send-TwilioSMS no [módulo Twilio do PowerShell](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) permite a passagem de qualquer uma das formas:</span><span class="sxs-lookup"><span data-stu-id="c297a-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. <span data-ttu-id="c297a-158">Defina o tipo de saída para todos os cmdlets no módulo.</span><span class="sxs-lookup"><span data-stu-id="c297a-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="c297a-159">A definição de um tipo de saída para um cmdlet permite o IntelliSense no tempo de criação para ajudar você a determinar as propriedades de saída do cmdlet, para uso durante a criação.</span><span class="sxs-lookup"><span data-stu-id="c297a-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="c297a-160">É especialmente útil durante a criação gráfica do runbook da Automação, quando o conhecimento do tempo de criação é fundamental para uma experiência de usuário facilitada com o seu módulo.</span><span class="sxs-lookup"><span data-stu-id="c297a-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="c297a-161">![Tipo de saída do runbook gráfico](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="c297a-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="c297a-162">Isso é semelhante à funcionalidade "preenchimento automático" da saída de um cmdlet no ISE do PowerShell sem precisar executá-lo.</span><span class="sxs-lookup"><span data-stu-id="c297a-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="c297a-163">![IntelliSense POSH](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="c297a-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="c297a-164">Os cmdlets no módulo não devem usar tipos de objeto complexos como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c297a-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="c297a-165">O Fluxo de Trabalho do PowerShell é diferente do PowerShell, pois armazena tipos complexos no formato desserializado.</span><span class="sxs-lookup"><span data-stu-id="c297a-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="c297a-166">Tipos primitivos permanecerão primitivos, mas tipos complexos serão convertidos em suas versões desserializadas, que são essencialmente pacotes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="c297a-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="c297a-167">Por exemplo, se você tiver usado o cmdlet **Get-Process** em um runbook (ou um Fluxo de Trabalho do PowerShell para esse fim), ele retornará um objeto do tipo [Deserialized.System.Diagnostic.Process] não o tipo [System.Diagnostic.Process] esperado.</span><span class="sxs-lookup"><span data-stu-id="c297a-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="c297a-168">Esse tipo tem as mesmas propriedades que o tipo não desserializado, mas nenhum dos métodos.</span><span class="sxs-lookup"><span data-stu-id="c297a-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="c297a-169">Se tentar passar esse valor como um parâmetro para um cmdlet, quando o cmdlet espera um valor [System.Diagnostic.Process] para esse parâmetro, você receberá o seguinte erro: *Não é possível processar a transformação do argumento no parâmetro 'process'. Erro: "Não é possível converter o valor "System.Diagnostics.Process (CcmExec)" do tipo "Deserialized.System.Diagnostics.Process" para o tipo "System.Diagnostics.Process".*</span><span class="sxs-lookup"><span data-stu-id="c297a-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="c297a-170">Isso ocorre porque há uma incompatibilidade de tipo entre o tipo [System.Diagnostic.Process] esperado e o tipo [Deserialized.System.Diagnostic.Process] fornecido.</span><span class="sxs-lookup"><span data-stu-id="c297a-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="c297a-171">A solução alternativa a esse problema é garantir que os cmdlets de seu módulo não usem tipos complexos como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c297a-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="c297a-172">Está é a maneira errada de fazer isso.</span><span class="sxs-lookup"><span data-stu-id="c297a-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="c297a-173">Esta é a maneira certa, usando um primitivo que pode ser usado internamente pelo cmdlet para obter o objeto complexo e usá-lo.</span><span class="sxs-lookup"><span data-stu-id="c297a-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="c297a-174">Como os cmdlets são executadas no contexto do PowerShell, não no Fluxo de Trabalho do PowerShell, dentro do cmdlet $process torna-se o tipo correto de [System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="c297a-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   <span data-ttu-id="c297a-175">Ativos de conexão em runbooks são tabelas de hash, que são um tipo complexo. Ainda assim, parece que essas tabelas de hash podem ser passadas para os cmdlets para seu parâmetro –Connection perfeitamente, sem qualquer exceção de conversão.</span><span class="sxs-lookup"><span data-stu-id="c297a-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="c297a-176">Tecnicamente, alguns tipos de PowerShell podem ser convertidos apropriadamente de sua forma serializada para a forma desserializada e, assim, podem ser passados para os cmdlets para os parâmetros que aceitam o tipo não desserializado.</span><span class="sxs-lookup"><span data-stu-id="c297a-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="c297a-177">A tabela de hash é um deles.</span><span class="sxs-lookup"><span data-stu-id="c297a-177">Hashtable is one of these.</span></span> <span data-ttu-id="c297a-178">É possível implementar os tipos definidos de um autor de módulo de uma forma que possam desserializar corretamente também, mas há algumas compensações a considerar.</span><span class="sxs-lookup"><span data-stu-id="c297a-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="c297a-179">O tipo deve ter um construtor padrão, ter todas as suas propriedades públicas e ter um PSTypeConverter.</span><span class="sxs-lookup"><span data-stu-id="c297a-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="c297a-180">No entanto, para os tipos já definidos que não são de propriedade do autor do módulo, não é possível "corrigi-los". Por esse motivo existe a recomendação para evitar tipos complexos para parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c297a-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="c297a-181">Dica de criação de runbook: se, por alguma razão, seus cmdlets precisarem aceitar um parâmetro de tipo complexo, ou se você estiver usando o módulo de outra pessoa que exige um parâmetro de tipo complexo, a solução nos runbooks de Fluxo de Trabalho do PowerShell, e em Fluxos de Trabalho do PowerShell no PowerShell local, é encapsular o cmdlet que gera o tipo complexo e o cmdlet que consome o tipo complexo na mesma atividade InlineScript.</span><span class="sxs-lookup"><span data-stu-id="c297a-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="c297a-182">Como a InlineScript executa seu conteúdo como PowerShell e não como um Fluxo de Trabalho do PowerShell, o cmdlet que gera o tipo complexo produziria esse tipo correto, não o tipo complexo desserializado.</span><span class="sxs-lookup"><span data-stu-id="c297a-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="c297a-183">Torne todos os cmdlets no módulo cmdlets sem estado.</span><span class="sxs-lookup"><span data-stu-id="c297a-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="c297a-184">O Fluxo de Trabalho do PowerShell executa cada cmdlet chamado no fluxo de trabalho em uma sessão diferente.</span><span class="sxs-lookup"><span data-stu-id="c297a-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="c297a-185">Isso significa que todos os cmdlets que dependem do estado da sessão criado/modificada por outros cmdlets no mesmo módulo não funcionarão em runbooks do Fluxo de Trabalho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c297a-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="c297a-186">Veja um exemplo do que não fazer:</span><span class="sxs-lookup"><span data-stu-id="c297a-186">Here is an example of what not to do.</span></span>
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. <span data-ttu-id="c297a-187">O módulo deve estar totalmente contido em um pacote capacitado para Xcopy.</span><span class="sxs-lookup"><span data-stu-id="c297a-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="c297a-188">Como os módulos da Automação do Azure são distribuídos para as áreas restritas da Automação quando os runbooks precisam ser executados, eles precisam trabalhar independentemente do host no qual estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="c297a-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="c297a-189">Isso significa que você deve ser capaz de compactar o pacote do módulo, movê-lo para qualquer outro host com a mesma versão do PowerShell ou mais recente, e fazê-lo funcionar normalmente quando importado para o ambiente do PowerShell desse host.</span><span class="sxs-lookup"><span data-stu-id="c297a-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="c297a-190">Para que isso aconteça, o módulo não deve depender de quaisquer arquivos fora da pasta do módulo (a pasta que é compactada ao importar na Automação do Azure), ou de qualquer configuração de registro exclusiva em um host, como aquelas definidas pela instalação de um produto.</span><span class="sxs-lookup"><span data-stu-id="c297a-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="c297a-191">Se essa prática recomendada não for seguida, o módulo não poderá ser usado na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c297a-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c297a-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c297a-192">Next steps</span></span>

* <span data-ttu-id="c297a-193">Para começar a usar runbooks de fluxo de trabalho do PowerShell, veja [Meu primeiro runbook de Fluxo de Trabalho do PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="c297a-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="c297a-194">Para saber mais sobre como criar os Módulos do PowerShell, consulte [Escrevendo um Módulo do Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="c297a-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

