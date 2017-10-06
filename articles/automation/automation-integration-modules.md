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
# <a name="azure-automation-integration-modules"></a>Módulos de integração de automação do Azure
PowerShell é a tecnologia fundamental Olá atrás de automação do Azure. Desde que a automação do Azure se baseia no PowerShell, módulos do PowerShell são toohello chave extensibilidade de automação do Azure. Neste artigo, vamos orientará especificidades de saudação do uso da automação do Azure de módulos do PowerShell, chamado tooas "Módulos de integração" e práticas recomendadas para criar seu próprio toomake de módulos do PowerShell se que estão funcionando como módulos de integração em Automação do Azure. 

## <a name="what-is-a-powershell-module"></a>O que é um módulo do PowerShell?
Um módulo do PowerShell é um grupo de cmdlets do PowerShell como **Get-Date** ou **Copy-Item**, que pode ser usado do console do PowerShell hello, scripts, fluxos de trabalho, runbooks e recursos de DSC do PowerShell, como WindowsFeature ou arquivo, que pode ser usado em configurações DSC do PowerShell. Toda a funcionalidade de saudação do PowerShell é exposta por meio de cmdlets e recursos de DSC, e cada recurso de DSC/cmdlet é apoiado por um módulo do PowerShell, muitas das quais fornecidas com o PowerShell em si. Por exemplo, Olá **Get-Date** cmdlet faz parte da saudação módulo do PowerShell Utility, e **Copy-Item** cmdlet faz parte da saudação módulo PowerShell Management e Olá recurso DSC pacote faz parte da saudação módulo PSDesiredStateConfiguration PowerShell. Esses dois módulos são fornecidos com o PowerShell. Mas muitos módulos do PowerShell não são fornecidos como parte do PowerShell e, em vez disso, são distribuídos com produtos de terceiros ou primeiro como o System Center 2012 Configuration Manager ou pela comunidade de PowerShell grande Olá em locais como Galeria do PowerShell.  módulos de saudação são úteis porque eles simplificar tarefas complexas por meio da funcionalidade encapsulada.  Saiba mais sobre [Módulos do PowerShell no MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx). 

## <a name="what-is-an-azure-automation-integration-module"></a>O que é um Módulo de Integração da Automação do Azure?
Um Módulo de Integração não é muito diferente de um módulo do PowerShell. Seu simplesmente um módulo do PowerShell que contém, opcionalmente, um arquivo adicional - um arquivo de metadados especificando um toobe de tipo de conexão de automação do Azure usado com os cmdlets do módulo Olá em runbooks. Opcional de arquivo ou não, esses módulos podem ser importados para a automação do Azure toomake seus cmdlets disponíveis para usar em runbooks e seus recursos de DSC disponíveis para uso nas configurações de DSC de PowerShell. Em segundo plano hello, a automação do Azure armazena esses módulos e no trabalho de runbook e o tempo de execução do trabalho de compilação de DSC, carrega-os em áreas restritas de automação do Azure Olá onde os runbooks são executados e configurações DSC são compiladas.  Qualquer recurso de DSC em módulos é colocado automaticamente no servidor de pull de DSC de automação Olá, para que eles podem ser extraídos por máquinas tentar tooapply configurações de DSC.  

Que enviamos um número de módulos do PowerShell do Azure sem a necessidade de saudação na automação do Azure para você toouse para que você pode começar a usar a automação do gerenciamento do Azure imediatamente, mas você pode importar os módulos do PowerShell para qualquer sistema, serviço ou ferramenta que você deseja toointegrate com. 

> [!NOTE]
> Determinados módulos são fornecidos como "módulos global" serviço de automação de saudação. Esses módulos globais são tooyou disponível quando você criar uma conta de automação e podemos atualizar, às vezes, que envia-os automaticamente tooyour conta de automação. Se não quiser que elas toobe atualizado automaticamente, você sempre pode importar Olá mesmo módulo por conta própria, e que terá precedência sobre a versão do módulo global Olá desse módulo fornecida no serviço de saudação. 

formato de saudação em que você importar um pacote do módulo de integração é um arquivo compactado com hello mesmo nome como módulo hello e uma extensão. zip. Ele contém o módulo do Windows PowerShell hello e quaisquer arquivos de suporte, incluindo um arquivo de manifesto (. psd1) se o módulo de saudação tem um.

Se o módulo de saudação deve conter um tipo de conexão de automação do Azure, ele também deve conter um arquivo com nome hello `<ModuleName>-Automation.json` que especifica as propriedades de tipo de conexão hello. Isso é um arquivo json colocado na pasta de módulo de saudação do seu arquivo. zip compactado e contém campos de saudação do "conexão", que é necessário tooconnect toohello sistema ou o módulo de saudação do serviço representa. Com isso, um tipo de conexão será criado na Automação do Azure. Usando esse arquivo, você pode definir nomes de campo hello, tipos, e se os campos de saudação devem ser criptografados e / ou opcionais para o tipo de conexão de saudação do módulo de saudação. a seguir Olá é um modelo em formato de arquivo hello json:

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

Se você tiver implantado o Service Management Automation e criar pacotes de módulos de integração para seus runbooks de automação, isso deve ser tooyou muito familiar. 

## <a name="authoring-best-practices"></a>Práticas recomendadas de criação
Embora os módulos de integração são essencialmente os módulos do PowerShell, se ainda há inúmeras coisas, recomendamos que você considere durante a criação de um módulo do PowerShell, toomake-la mais útil na automação do Azure. Algumas delas são específicas de automação do Azure e algumas delas são úteis toomake apenas seus módulos funcionam bem no fluxo de trabalho do PowerShell, independentemente se você estiver usando a automação. 

1. Incluir uma sinopse, descrição e URI de ajuda para cada cmdlet no módulo de saudação. No PowerShell, você pode definir algumas informações de ajuda para cmdlets tooallow Olá usuário tooreceive Ajuda em usá-los com hello **Get-Help** cmdlet. Por exemplo, veja como você pode definir uma sinopse e um URI de ajuda para um módulo do PowerShell escrito em um arquivo .psm1.<br>  
   
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
   <br> Fornecer essas informações não mostrará apenas ajuda usando Olá **Get-Help** Olá de cmdlet no console do PowerShell, ele também irá expor essa funcionalidade ajuda na automação do Azure.  Por exemplo, ao inserir atividades durante a criação de runbooks. Clicar em "Exibir ajuda detalhada" será URI de ajuda Olá aberto em outra guia do hello navegador da web estiver usando tooaccess automação do Azure.<br>![Ajuda do Módulo de Integração](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. Se o módulo de saudação é executado em um sistema remoto,

    a. Ela deve conter um arquivo de metadados do módulo de integração que define Olá informações necessárias tooconnect toothat sistema remoto, que significa que o tipo de conexão de saudação.  
    b. Cada cmdlet no módulo Olá deve ser capaz de tootake em um objeto de conexão (uma instância desse tipo de conexão) como um parâmetro.  

    Cmdlets no módulo de saudação se tornam mais fácil toouse na automação do Azure se você permitir passando um objeto com campos de saudação do tipo de conexão hello como um cmdlet de toohello do parâmetro. Esse modo como os usuários não tem parâmetros de toomap de parâmetros correspondentes do cmdlet do hello conexão ativo toohello cada vez que eles chamam de um cmdlet. Com base no exemplo de runbook hello acima, ele usa um ativo de conexão do Twilio chamado CorpTwilio tooaccess Twilio e retornar todos os números de telefone de saudação na conta de saudação.  Observe como ele é mapear os campos de saudação parâmetros de toohello de conexão de saudação do cmdlet de Olá?<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    Uma maneira mais fácil e melhor tooapproach isso está passando diretamente Olá conexão objeto toohello cmdlet-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    Você pode habilitar o comportamento de seus cmdlets assim, permitindo que eles tooaccept um objeto de conexão diretamente como um parâmetro, em vez de apenas os campos de conexão para os parâmetros. Geralmente, você desejará um conjunto de parâmetros para cada um, para que um usuário não usando a automação do Azure possa chamar seus cmdlets sem construir tooact uma tabela de hash como objeto de conexão de saudação. Conjunto de parâmetros **SpecifyConnectionFields** abaixo é usado toopass propriedades de campo de conexão Olá uma. **UseConnectionObject** permite que você passe Olá diretamente por meio da conexão. Como você pode ver, Olá cmdlet Send-TwilioSMS Olá [Twilio PowerShell módulo](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) permite a passagem de qualquer forma: 
   
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
3. Defina o tipo de saída para todos os cmdlets no módulo hello. Definição de um tipo de saída para um cmdlet permite que o IntelliSense de tempo de design toohelp determinar Olá propriedades do cmdlet hello, para uso durante a criação de saída. É especialmente útil durante a automação runbook gráficas de criação, onde o conhecimento do tempo de design é experiência do usuário fácil tooan chave com o módulo.<br><br> ![Tipo de saída do runbook gráfico](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> Isso é semelhante toohello funcionalidade de "tipo em frente" de um cmdlet de saída no ISE do PowerShell sem a necessidade de toorun-lo.<br><br> ![IntelliSense POSH](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. Cmdlets no módulo Olá não deveria receber os tipos de objeto complexo para parâmetros. O Fluxo de Trabalho do PowerShell é diferente do PowerShell, pois armazena tipos complexos no formato desserializado. Tipos primitivos permanecerá como primitivos, mas tipos complexos são convertidos tootheir desserializado versões, que são basicamente os recipientes de propriedade. Por exemplo, se você usou Olá **Get-Process** cmdlet em um runbook (ou um fluxo de trabalho do PowerShell para essa finalidade), ele deve retornar um objeto do tipo [Deserialized.System.Diagnostic.Process], não Olá esperado [ Tipo de Diagnostic]. Esse tipo tem todos os Olá mesmas propriedades como Olá tipo não é desserializado, mas nenhum dos métodos de saudação. E se você tentar toopass esse valor como um parâmetro tooa cmdlet, onde Olá cmdlet espera um valor de [Diagnostic] para esse parâmetro, você receberá Olá erro a seguir: *não é possível processar a transformação de argumento no parâmetro 'processo' . Erro: "não é possível converter o valor do hello"Process (CcmExec)"do tipo"Deserialized.System.Diagnostics.Process"tootype"Process".*   Isso ocorre porque há que uma incompatibilidade de tipo entre hello esperado tipo [Diagnostic] e hello [Deserialized.System.Diagnostic.Process] tipo fornecido. modo de saudação alternativa para esse problema é tooensure Olá cmdlets do módulo não têm tipos complexos para parâmetros. Aqui está a saudação errada toodo-lo.
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    E aqui está a saudação de certa forma, considerando em um primitivo que pode ser usado internamente pelo cmdlet Olá toograb Olá objeto complexo e usá-lo. Como executar cmdlets no contexto de saudação do PowerShell, não PowerShell fluxo de trabalho, dentro de cmdlet Olá $process torna-se o tipo correto de [Diagnostic] Olá.  
   
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
   Ativos de Conexão em runbooks são tabelas de hash, que são um tipo complexo, e ainda essas tabelas de hash parecerem toobe toobe capaz passado para cmdlets para seus – o parâmetro de Conexão perfeitamente, com exceção de nenhuma conversão. Tecnicamente, alguns tipos de PowerShell são capaz de toocast corretamente em sua forma de tootheir desserializado formato serializado e, portanto, podem ser passados para cmdlets para aceitar o tipo de não desserializado Olá de parâmetros. A tabela de hash é um deles. É possível toobe de tipos definidos de um autor módulo implementado de forma que eles corretamente podem desserializar também, mas há alguns tooconsider vantagens e desvantagens. Olá tipo necessidades toohave um construtor padrão, têm todas suas propriedades públicas e ter um PSTypeConverter. No entanto, para tipos já definidos pelo autor do módulo que Olá não possui, há não muito "corrigir"-los, Olá, portanto, os tipos complexos de tooavoid de recomendação para parâmetros todos juntos. Criação de runbook Dica: se por alguma razão, seus cmdlets necessário tootake um complexo de parâmetro de tipo, ou você estiver usando outra pessoa módulo que requer um parâmetro de tipo complexo, a solução alternativa de saudação em runbooks de fluxo de trabalho do PowerShell e fluxos de trabalho do PowerShell no local PowerShell, é toowrap Olá cmdlet que gera o tipo complexo hello e Olá cmdlet que consome o tipo complexo de saudação em Olá mesma atividade InlineScript. Como InlineScript seu conteúdo é executado como o PowerShell em vez de fluxo de trabalho do PowerShell, cmdlet Olá geração de tipo complexo Olá pode produzir esse tipo correto, não Olá desserializar o tipo complexo.
5. Faça com que todos os cmdlets no módulo Olá sem monitoração de estado. Fluxo de trabalho do PowerShell é executado a cada cmdlet chamado no fluxo de trabalho de saudação em uma sessão diferente. Isso significa que todos os cmdlets que dependem do estado de sessão criadas / modificadas por outros cmdlets em Olá mesmo módulo não funcionará em runbooks de fluxo de trabalho do PowerShell.  Aqui está um exemplo do que não toodo.
   
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
6. módulo Olá deve estar totalmente contido em um pacote capaz de Xcopy. Como módulos de automação do Azure são as áreas restritas de automação distribuída toohello quando precisar de runbooks tooexecute, eles precisam toowork independentemente do host Olá em que estiverem sendo executados. Isso significa que você deve ser capaz de tooZip o pacote do módulo hello, movê-la tooany outro host com hello igual ou mais recente versão do PowerShell, e ainda funcionar normalmente quando importados para o ambiente do PowerShell do host. Para que toohappen, módulo Olá deve não dependem de todos os arquivos fora da pasta de módulo hello (Olá pasta obtém compactada ao importar para a automação do Azure), ou em quaisquer configurações de registro exclusivo em um host, como aquelas definidas por Olá instalar de um produto. Se não for efetivada essa prática recomendada, o módulo de saudação não poderá ser usado na automação do Azure.  

## <a name="next-steps"></a>Próximas etapas

* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)
* toolearn mais sobre como criar módulos do PowerShell, consulte [escrevendo um módulo do Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

