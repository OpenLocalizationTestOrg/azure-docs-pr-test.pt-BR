---
title: "aaaCreate um módulo de integração de automação do Azure | Microsoft Docs"
description: "Tutorial que orienta você através do uso de criação, teste e exemplo hello módulos de integração na automação do Azure."
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
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="1d327-103">Módulos de integração de automação do Azure</span><span class="sxs-lookup"><span data-stu-id="1d327-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="1d327-104">PowerShell é a tecnologia fundamental Olá atrás de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d327-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="1d327-105">Desde que a automação do Azure se baseia no PowerShell, módulos do PowerShell são toohello chave extensibilidade de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d327-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="1d327-106">Neste artigo, vamos orientará especificidades de saudação do uso da automação do Azure de módulos do PowerShell, chamado tooas "Módulos de integração" e práticas recomendadas para criar seu próprio toomake de módulos do PowerShell se que estão funcionando como módulos de integração em Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d327-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="1d327-107">O que é um módulo do PowerShell?</span><span class="sxs-lookup"><span data-stu-id="1d327-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="1d327-108">Um módulo do PowerShell é um grupo de cmdlets do PowerShell como **Get-Date** ou **Copy-Item**, que pode ser usado do console do PowerShell hello, scripts, fluxos de trabalho, runbooks e recursos de DSC do PowerShell, como WindowsFeature ou arquivo, que pode ser usado em configurações DSC do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d327-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="1d327-109">Toda a funcionalidade de saudação do PowerShell é exposta por meio de cmdlets e recursos de DSC, e cada recurso de DSC/cmdlet é apoiado por um módulo do PowerShell, muitas das quais fornecidas com o PowerShell em si.</span><span class="sxs-lookup"><span data-stu-id="1d327-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="1d327-110">Por exemplo, Olá **Get-Date** cmdlet faz parte da saudação módulo do PowerShell Utility, e **Copy-Item** cmdlet faz parte da saudação módulo PowerShell Management e Olá recurso DSC pacote faz parte da saudação módulo PSDesiredStateConfiguration PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d327-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="1d327-111">Esses dois módulos são fornecidos com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d327-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="1d327-112">Mas muitos módulos do PowerShell não são fornecidos como parte do PowerShell e, em vez disso, são distribuídos com produtos de terceiros ou primeiro como o System Center 2012 Configuration Manager ou pela comunidade de PowerShell grande Olá em locais como Galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d327-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="1d327-113">módulos de saudação são úteis porque eles simplificar tarefas complexas por meio da funcionalidade encapsulada.</span><span class="sxs-lookup"><span data-stu-id="1d327-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="1d327-114">Saiba mais sobre [Módulos do PowerShell no MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d327-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="1d327-115">O que é um Módulo de Integração da Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="1d327-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="1d327-116">Um Módulo de Integração não é muito diferente de um módulo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d327-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="1d327-117">Seu simplesmente um módulo do PowerShell que contém, opcionalmente, um arquivo adicional - um arquivo de metadados especificando um toobe de tipo de conexão de automação do Azure usado com os cmdlets do módulo Olá em runbooks.</span><span class="sxs-lookup"><span data-stu-id="1d327-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="1d327-118">Opcional de arquivo ou não, esses módulos podem ser importados para a automação do Azure toomake seus cmdlets disponíveis para usar em runbooks e seus recursos de DSC disponíveis para uso nas configurações de DSC de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d327-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="1d327-119">Em segundo plano hello, a automação do Azure armazena esses módulos e no trabalho de runbook e o tempo de execução do trabalho de compilação de DSC, carrega-os em áreas restritas de automação do Azure Olá onde os runbooks são executados e configurações DSC são compiladas.</span><span class="sxs-lookup"><span data-stu-id="1d327-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="1d327-120">Qualquer recurso de DSC em módulos é colocado automaticamente no servidor de pull de DSC de automação Olá, para que eles podem ser extraídos por máquinas tentar tooapply configurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="1d327-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="1d327-121">Que enviamos um número de módulos do PowerShell do Azure sem a necessidade de saudação na automação do Azure para você toouse para que você pode começar a usar a automação do gerenciamento do Azure imediatamente, mas você pode importar os módulos do PowerShell para qualquer sistema, serviço ou ferramenta que você deseja toointegrate com.</span><span class="sxs-lookup"><span data-stu-id="1d327-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="1d327-122">Determinados módulos são fornecidos como "módulos global" serviço de automação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d327-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="1d327-123">Esses módulos globais são tooyou disponível quando você criar uma conta de automação e podemos atualizar, às vezes, que envia-os automaticamente tooyour conta de automação.</span><span class="sxs-lookup"><span data-stu-id="1d327-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="1d327-124">Se não quiser que elas toobe atualizado automaticamente, você sempre pode importar Olá mesmo módulo por conta própria, e que terá precedência sobre a versão do módulo global Olá desse módulo fornecida no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d327-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="1d327-125">formato de saudação em que você importar um pacote do módulo de integração é um arquivo compactado com hello mesmo nome como módulo hello e uma extensão. zip.</span><span class="sxs-lookup"><span data-stu-id="1d327-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="1d327-126">Ele contém o módulo do Windows PowerShell hello e quaisquer arquivos de suporte, incluindo um arquivo de manifesto (. psd1) se o módulo de saudação tem um.</span><span class="sxs-lookup"><span data-stu-id="1d327-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="1d327-127">Se o módulo de saudação deve conter um tipo de conexão de automação do Azure, ele também deve conter um arquivo com nome hello `<ModuleName>-Automation.json` que especifica as propriedades de tipo de conexão hello.</span><span class="sxs-lookup"><span data-stu-id="1d327-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="1d327-128">Isso é um arquivo json colocado na pasta de módulo de saudação do seu arquivo. zip compactado e contém campos de saudação do "conexão", que é necessário tooconnect toohello sistema ou o módulo de saudação do serviço representa.</span><span class="sxs-lookup"><span data-stu-id="1d327-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="1d327-129">Com isso, um tipo de conexão será criado na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d327-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="1d327-130">Usando esse arquivo, você pode definir nomes de campo hello, tipos, e se os campos de saudação devem ser criptografados e / ou opcionais para o tipo de conexão de saudação do módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d327-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="1d327-131">a seguir Olá é um modelo em formato de arquivo hello json:</span><span class="sxs-lookup"><span data-stu-id="1d327-131">hello following is a template in hello json file format:</span></span>

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

<span data-ttu-id="1d327-132">Se você tiver implantado o Service Management Automation e criar pacotes de módulos de integração para seus runbooks de automação, isso deve ser tooyou muito familiar.</span><span class="sxs-lookup"><span data-stu-id="1d327-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="1d327-133">Práticas recomendadas de criação</span><span class="sxs-lookup"><span data-stu-id="1d327-133">Authoring Best Practices</span></span>
<span data-ttu-id="1d327-134">Embora os módulos de integração são essencialmente os módulos do PowerShell, se ainda há inúmeras coisas, recomendamos que você considere durante a criação de um módulo do PowerShell, toomake-la mais útil na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d327-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="1d327-135">Algumas delas são específicas de automação do Azure e algumas delas são úteis toomake apenas seus módulos funcionam bem no fluxo de trabalho do PowerShell, independentemente se você estiver usando a automação.</span><span class="sxs-lookup"><span data-stu-id="1d327-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="1d327-136">Incluir uma sinopse, descrição e URI de ajuda para cada cmdlet no módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d327-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="1d327-137">No PowerShell, você pode definir algumas informações de ajuda para cmdlets tooallow Olá usuário tooreceive Ajuda em usá-los com hello **Get-Help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d327-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="1d327-138">Por exemplo, veja como você pode definir uma sinopse e um URI de ajuda para um módulo do PowerShell escrito em um arquivo .psm1.</span><span class="sxs-lookup"><span data-stu-id="1d327-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="1d327-139">Fornecer essas informações não mostrará apenas ajuda usando Olá **Get-Help** Olá de cmdlet no console do PowerShell, ele também irá expor essa funcionalidade ajuda na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d327-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="1d327-140">Por exemplo, ao inserir atividades durante a criação de runbooks.</span><span class="sxs-lookup"><span data-stu-id="1d327-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="1d327-141">Clicar em "Exibir ajuda detalhada" será URI de ajuda Olá aberto em outra guia do hello navegador da web estiver usando tooaccess automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d327-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="1d327-142">![Ajuda do Módulo de Integração](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="1d327-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="1d327-143">Se o módulo de saudação é executado em um sistema remoto,</span><span class="sxs-lookup"><span data-stu-id="1d327-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="1d327-144">a.</span><span class="sxs-lookup"><span data-stu-id="1d327-144">a.</span></span> <span data-ttu-id="1d327-145">Ela deve conter um arquivo de metadados do módulo de integração que define Olá informações necessárias tooconnect toothat sistema remoto, que significa que o tipo de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d327-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="1d327-146">b.</span><span class="sxs-lookup"><span data-stu-id="1d327-146">b.</span></span> <span data-ttu-id="1d327-147">Cada cmdlet no módulo Olá deve ser capaz de tootake em um objeto de conexão (uma instância desse tipo de conexão) como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1d327-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="1d327-148">Cmdlets no módulo de saudação se tornam mais fácil toouse na automação do Azure se você permitir passando um objeto com campos de saudação do tipo de conexão hello como um cmdlet de toohello do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1d327-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="1d327-149">Esse modo como os usuários não tem parâmetros de toomap de parâmetros correspondentes do cmdlet do hello conexão ativo toohello cada vez que eles chamam de um cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d327-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="1d327-150">Com base no exemplo de runbook hello acima, ele usa um ativo de conexão do Twilio chamado CorpTwilio tooaccess Twilio e retornar todos os números de telefone de saudação na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d327-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="1d327-151">Observe como ele é mapear os campos de saudação parâmetros de toohello de conexão de saudação do cmdlet de Olá?</span><span class="sxs-lookup"><span data-stu-id="1d327-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="1d327-152">Uma maneira mais fácil e melhor tooapproach isso está passando diretamente Olá conexão objeto toohello cmdlet-</span><span class="sxs-lookup"><span data-stu-id="1d327-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="1d327-153">Você pode habilitar o comportamento de seus cmdlets assim, permitindo que eles tooaccept um objeto de conexão diretamente como um parâmetro, em vez de apenas os campos de conexão para os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1d327-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="1d327-154">Geralmente, você desejará um conjunto de parâmetros para cada um, para que um usuário não usando a automação do Azure possa chamar seus cmdlets sem construir tooact uma tabela de hash como objeto de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d327-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="1d327-155">Conjunto de parâmetros **SpecifyConnectionFields** abaixo é usado toopass propriedades de campo de conexão Olá uma.</span><span class="sxs-lookup"><span data-stu-id="1d327-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="1d327-156">**UseConnectionObject** permite que você passe Olá diretamente por meio da conexão.</span><span class="sxs-lookup"><span data-stu-id="1d327-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="1d327-157">Como você pode ver, Olá cmdlet Send-TwilioSMS Olá [Twilio PowerShell módulo](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) permite a passagem de qualquer forma:</span><span class="sxs-lookup"><span data-stu-id="1d327-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="1d327-158">Defina o tipo de saída para todos os cmdlets no módulo hello.</span><span class="sxs-lookup"><span data-stu-id="1d327-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="1d327-159">Definição de um tipo de saída para um cmdlet permite que o IntelliSense de tempo de design toohelp determinar Olá propriedades do cmdlet hello, para uso durante a criação de saída.</span><span class="sxs-lookup"><span data-stu-id="1d327-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="1d327-160">É especialmente útil durante a automação runbook gráficas de criação, onde o conhecimento do tempo de design é experiência do usuário fácil tooan chave com o módulo.</span><span class="sxs-lookup"><span data-stu-id="1d327-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="1d327-161">![Tipo de saída do runbook gráfico](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="1d327-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="1d327-162">Isso é semelhante toohello funcionalidade de "tipo em frente" de um cmdlet de saída no ISE do PowerShell sem a necessidade de toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="1d327-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="1d327-163">![IntelliSense POSH](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="1d327-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="1d327-164">Cmdlets no módulo Olá não deveria receber os tipos de objeto complexo para parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1d327-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="1d327-165">O Fluxo de Trabalho do PowerShell é diferente do PowerShell, pois armazena tipos complexos no formato desserializado.</span><span class="sxs-lookup"><span data-stu-id="1d327-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="1d327-166">Tipos primitivos permanecerá como primitivos, mas tipos complexos são convertidos tootheir desserializado versões, que são basicamente os recipientes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="1d327-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="1d327-167">Por exemplo, se você usou Olá **Get-Process** cmdlet em um runbook (ou um fluxo de trabalho do PowerShell para essa finalidade), ele deve retornar um objeto do tipo [Deserialized.System.Diagnostic.Process], não Olá esperado [ Tipo de Diagnostic].</span><span class="sxs-lookup"><span data-stu-id="1d327-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="1d327-168">Esse tipo tem todos os Olá mesmas propriedades como Olá tipo não é desserializado, mas nenhum dos métodos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d327-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="1d327-169">E se você tentar toopass esse valor como um parâmetro tooa cmdlet, onde Olá cmdlet espera um valor de [Diagnostic] para esse parâmetro, você receberá Olá erro a seguir: *não é possível processar a transformação de argumento no parâmetro 'processo' . Erro: "não é possível converter o valor do hello"Process (CcmExec)"do tipo"Deserialized.System.Diagnostics.Process"tootype"Process".*</span><span class="sxs-lookup"><span data-stu-id="1d327-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="1d327-170">Isso ocorre porque há que uma incompatibilidade de tipo entre hello esperado tipo [Diagnostic] e hello [Deserialized.System.Diagnostic.Process] tipo fornecido.</span><span class="sxs-lookup"><span data-stu-id="1d327-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="1d327-171">modo de saudação alternativa para esse problema é tooensure Olá cmdlets do módulo não têm tipos complexos para parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1d327-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="1d327-172">Aqui está a saudação errada toodo-lo.</span><span class="sxs-lookup"><span data-stu-id="1d327-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="1d327-173">E aqui está a saudação de certa forma, considerando em um primitivo que pode ser usado internamente pelo cmdlet Olá toograb Olá objeto complexo e usá-lo.</span><span class="sxs-lookup"><span data-stu-id="1d327-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="1d327-174">Como executar cmdlets no contexto de saudação do PowerShell, não PowerShell fluxo de trabalho, dentro de cmdlet Olá $process torna-se o tipo correto de [Diagnostic] Olá.</span><span class="sxs-lookup"><span data-stu-id="1d327-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="1d327-175">Ativos de Conexão em runbooks são tabelas de hash, que são um tipo complexo, e ainda essas tabelas de hash parecerem toobe toobe capaz passado para cmdlets para seus – o parâmetro de Conexão perfeitamente, com exceção de nenhuma conversão.</span><span class="sxs-lookup"><span data-stu-id="1d327-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="1d327-176">Tecnicamente, alguns tipos de PowerShell são capaz de toocast corretamente em sua forma de tootheir desserializado formato serializado e, portanto, podem ser passados para cmdlets para aceitar o tipo de não desserializado Olá de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="1d327-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="1d327-177">A tabela de hash é um deles.</span><span class="sxs-lookup"><span data-stu-id="1d327-177">Hashtable is one of these.</span></span> <span data-ttu-id="1d327-178">É possível toobe de tipos definidos de um autor módulo implementado de forma que eles corretamente podem desserializar também, mas há alguns tooconsider vantagens e desvantagens.</span><span class="sxs-lookup"><span data-stu-id="1d327-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="1d327-179">Olá tipo necessidades toohave um construtor padrão, têm todas suas propriedades públicas e ter um PSTypeConverter.</span><span class="sxs-lookup"><span data-stu-id="1d327-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="1d327-180">No entanto, para tipos já definidos pelo autor do módulo que Olá não possui, há não muito "corrigir"-los, Olá, portanto, os tipos complexos de tooavoid de recomendação para parâmetros todos juntos.</span><span class="sxs-lookup"><span data-stu-id="1d327-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="1d327-181">Criação de runbook Dica: se por alguma razão, seus cmdlets necessário tootake um complexo de parâmetro de tipo, ou você estiver usando outra pessoa módulo que requer um parâmetro de tipo complexo, a solução alternativa de saudação em runbooks de fluxo de trabalho do PowerShell e fluxos de trabalho do PowerShell no local PowerShell, é toowrap Olá cmdlet que gera o tipo complexo hello e Olá cmdlet que consome o tipo complexo de saudação em Olá mesma atividade InlineScript.</span><span class="sxs-lookup"><span data-stu-id="1d327-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="1d327-182">Como InlineScript seu conteúdo é executado como o PowerShell em vez de fluxo de trabalho do PowerShell, cmdlet Olá geração de tipo complexo Olá pode produzir esse tipo correto, não Olá desserializar o tipo complexo.</span><span class="sxs-lookup"><span data-stu-id="1d327-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="1d327-183">Faça com que todos os cmdlets no módulo Olá sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="1d327-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="1d327-184">Fluxo de trabalho do PowerShell é executado a cada cmdlet chamado no fluxo de trabalho de saudação em uma sessão diferente.</span><span class="sxs-lookup"><span data-stu-id="1d327-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="1d327-185">Isso significa que todos os cmdlets que dependem do estado de sessão criadas / modificadas por outros cmdlets em Olá mesmo módulo não funcionará em runbooks de fluxo de trabalho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d327-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="1d327-186">Aqui está um exemplo do que não toodo.</span><span class="sxs-lookup"><span data-stu-id="1d327-186">Here is an example of what not toodo.</span></span>
   
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
6. <span data-ttu-id="1d327-187">módulo Olá deve estar totalmente contido em um pacote capaz de Xcopy.</span><span class="sxs-lookup"><span data-stu-id="1d327-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="1d327-188">Como módulos de automação do Azure são as áreas restritas de automação distribuída toohello quando precisar de runbooks tooexecute, eles precisam toowork independentemente do host Olá em que estiverem sendo executados.</span><span class="sxs-lookup"><span data-stu-id="1d327-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="1d327-189">Isso significa que você deve ser capaz de tooZip o pacote do módulo hello, movê-la tooany outro host com hello igual ou mais recente versão do PowerShell, e ainda funcionar normalmente quando importados para o ambiente do PowerShell do host.</span><span class="sxs-lookup"><span data-stu-id="1d327-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="1d327-190">Para que toohappen, módulo Olá deve não dependem de todos os arquivos fora da pasta de módulo hello (Olá pasta obtém compactada ao importar para a automação do Azure), ou em quaisquer configurações de registro exclusivo em um host, como aquelas definidas por Olá instalar de um produto.</span><span class="sxs-lookup"><span data-stu-id="1d327-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="1d327-191">Se não for efetivada essa prática recomendada, o módulo de saudação não poderá ser usado na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d327-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1d327-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d327-192">Next steps</span></span>

* <span data-ttu-id="1d327-193">tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="1d327-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="1d327-194">toolearn mais sobre como criar módulos do PowerShell, consulte [escrevendo um módulo do Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="1d327-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

