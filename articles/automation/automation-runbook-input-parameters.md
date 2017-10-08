---
title: "parâmetros de entrada aaaRunbook | Microsoft Docs"
description: "Parâmetros de entrada do runbook aumentam a flexibilidade de saudação de runbooks, permitindo-lhe toopass dados tooa runbook quando ele for iniciado. Este artigo descreve os diferentes cenários em que os parâmetros de entrada são usados em runbooks."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Parâmetros de entrada do Runbook
Parâmetros de entrada do runbook aumentam a flexibilidade de saudação de runbooks, permitindo-lhe toopass dados tooit quando ele for iniciado. Olá permitem Olá runbook ações toobe direcionado para ambientes e cenários específicos. Neste artigo, vamos orientá-lo quanto aos diferentes cenários em que os parâmetros de entrada são usados em runbooks.

## <a name="configure-input-parameters"></a>Como configurar parâmetros de entrada
Parâmetros de entrada podem ser configurados no PowerShell, no Fluxo de Trabalho do PowerShell e em runbooks gráficos. Um runbook pode ter vários parâmetros com tipos de dados diferentes, ou não ter nenhum parâmetro. Os parâmetros de entrada podem ser obrigatório ou opcionais, e você pode atribuir um valor padrão para parâmetros opcionais. Você pode atribuir valores toohello parâmetros de entrada para um runbook quando você iniciá-lo por meio de um dos métodos disponíveis hello. Esses métodos incluem iniciando um runbook do portal de saudação ou um serviço da web. Você também pode iniciá-lo como um runbook filho, que é chamado de embutido em outro runbook.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>Como configurar parâmetros de entrada no PowerShell e em runbooks do Fluxo de Trabalho do PowerShell
PowerShell e [runbooks do fluxo de trabalho do PowerShell](automation-first-runbook-textual.md) na automação do Azure oferecem suporte a parâmetros de entrada que são definidos por meio de saudação atributos a seguir.  

| **Propriedade** | **Descrição** |
|:--- |:--- |
| Tipo |Obrigatório. tipo de dados Olá esperado para o valor do parâmetro hello. Qualquer tipo .NET é válido. |
| Nome |Obrigatório. nome de saudação do parâmetro hello. Isso deve ser exclusivo dentro de runbook Olá e pode conter apenas letras, números ou caracteres de sublinhado. Deve começar com uma letra. |
| Obrigatório |Opcional. Especifica se deve ser fornecido um valor para o parâmetro hello. Se você definir esta opção muito**$true**, em seguida, um valor deve ser fornecido quando Olá runbook for iniciado. Se você definir esta opção muito**$false**, em seguida, um valor é opcional. |
| Valor padrão |Opcional.  Especifica um valor que será usado para o parâmetro hello se um valor não for passado quando Olá runbook for iniciado. Um valor padrão pode ser definido para qualquer parâmetro e fará automaticamente parâmetro hello opcional independentemente Olá configuração obrigatória. |

O Windows PowerShell dá suporte a mais atributos de parâmetros de entrada do que aqueles listados aqui, como validação, aliases e conjuntos de parâmetros. No entanto, automação do Azure atualmente suporta apenas Olá parâmetros de entrada listados acima.

Uma definição de parâmetro no fluxo de trabalho do PowerShell runbooks tem Olá seguindo o formato geral, onde vários parâmetros são separados por vírgulas.

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> Quando você está definindo parâmetros, se você não especificar Olá **obrigatório** atributo, em seguida, por padrão, o parâmetro hello é considerado opcional. Além disso, se você definir um valor padrão para um parâmetro em runbooks de fluxo de trabalho do PowerShell, ele será tratado pelo PowerShell como um parâmetro opcional, independentemente de saudação **obrigatório** valor do atributo.
> 
> 

Por exemplo, vamos configurar parâmetros de entrada hello para um runbook de fluxo de trabalho do PowerShell que gera os detalhes sobre as máquinas virtuais, uma única VM ou todas as máquinas virtuais dentro de um grupo de recursos. Este runbook tem dois parâmetros, conforme mostrado no hello captura de tela a seguir: nome de saudação da máquina virtual e o nome de Olá Olá do grupo de recursos.

![Fluxo de trabalho do PowerShell de automação](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

Nesta definição de parâmetro, Olá parâmetros **$VMName** e **$resourceGroupName** são parâmetros simples do tipo cadeia de caracteres. No entanto, o PowerShell e os runbooks do Fluxo de Trabalho do PowerShell dão suporte a todos os tipos simples e complexos, como **objeto** ou **PSCredential** para parâmetros de entrada.

Se seu runbook tem um parâmetro de entrada de tipo de objeto, em seguida, use uma tabela de hash com (nome, valor) do PowerShell pares toopass em um valor. Por exemplo, se você tiver Olá parâmetro em um runbook a seguir:

     [Parameter (Mandatory = $true)]
     [object] $FullName

Em seguida, você pode passar Olá parâmetro toohello de valor a seguir:

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>Como configurar parâmetros de entrada em runbooks gráficos
muito[configurar um runbook gráfico](automation-first-runbook-graphical.md) com parâmetros de entrada, vamos criar um runbook gráfico que gera os detalhes sobre as máquinas virtuais, ou uma única VM ou todas as máquinas virtuais dentro de um grupo de recursos. A configuração de um runbook consiste em duas atividades principais, conforme descrito abaixo.

[**Autenticar Runbooks com a conta executar como do Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate com o Azure.

[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget propriedades de saudação de uma máquina virtual.

Você pode usar o hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) nomes de hello atividade toooutput de máquinas virtuais. Hello atividade **Get-AzureRmVm** aceita dois parâmetros, hello **nome da máquina virtual** e hello **nome do grupo de recursos**. Como esses parâmetros podem exigir valores diferentes cada vez que iniciar o runbook hello, você pode adicionar parâmetros de entrada tooyour runbook. Aqui estão os parâmetros de entrada hello etapas tooadd:

1. Selecione Olá runbook gráfico de saudação **Runbooks** folha e depois clique em [ **editar** ](automation-graphical-authoring-intro.md) -lo.
2. No editor de runbook hello, clique em **de entrada e saída** tooopen Olá **de entrada e saída** folha.
   
    ![Runbook gráfico de automação](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. Olá **de entrada e saída** folha exibe uma lista de parâmetros de entrada que são definidos para o runbook hello. Nesta folha, você pode adicionar um novo parâmetro de entrada ou Editar configuração de saudação de um parâmetro de entrada existente. tooadd um novo parâmetro hello runbook, clique em **Adicionar entrada** tooopen Olá **parâmetro de entrada do Runbook** folha. Lá, você pode configurar Olá parâmetros a seguir:
   
   | **Propriedade** | **Descrição** |
   |:--- |:--- |
   | Nome |Obrigatório.  nome de saudação do parâmetro hello. Isso deve ser exclusivo dentro de runbook Olá e pode conter apenas letras, números ou caracteres de sublinhado. Deve começar com uma letra. |
   | Descrição |Opcional. Descrição sobre a finalidade de saudação do parâmetro de entrada. |
   | Tipo |Opcional. tipo de dados de saudação esperada para o valor do parâmetro hello. Os tipos de parâmetro com suporte são **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** e **Object**. Se um tipo de dados não estiver selecionado, o padrão é muito**cadeia de caracteres**. |
   | Obrigatório |Opcional. Especifica se deve ser fornecido um valor para o parâmetro hello. Se você escolher **Sim**, em seguida, um valor deve ser fornecido quando Olá runbook for iniciado. Se você escolher **sem**, em seguida, um valor não é necessário quando Olá runbook for iniciado, e um valor padrão pode ser definido. |
   | Valor Padrão |Opcional. Especifica um valor que será usado para o parâmetro hello se um valor não for passado quando Olá runbook for iniciado. Um valor padrão pode ser definido para um parâmetro que não é obrigatório. tooset um valor padrão, escolha **personalizado**. Esse valor é usado, a menos que outro valor seja fornecido quando Olá runbook for iniciado. Escolha **nenhum** se você não quiser tooprovide qualquer valor padrão. |
   
    ![Como adicionar nova entrada](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. Crie dois parâmetros com hello seguintes propriedades que serão usadas pelo Olá **AzureRmVm Get** atividade:
   
   * **Parameter1:**
     
     * Nome - VMName
     * Tipo - String
     * Obrigatório - Não
   * **Parameter2:**
     
     * Nome - resourceGroupName
     * Tipo - String
     * Obrigatório - Não
     * Valor padrão - Personalizado
     * O valor padrão personalizado - \<nome saudação do grupo de recursos que contém máquinas virtuais de hello >
5. Depois de adicionar parâmetros de saudação, clique em **Okey**.  Agora você pode exibi-las no hello **entrada e saída blade**. Clique em **OK** novamente e clique em **Salvar** e **Publicar** o runbook.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Atribuir valores de parâmetros de tooinput em runbooks
Você pode passar valores tooinput parâmetros em runbooks em Olá cenários a seguir.

### <a name="start-a-runbook-and-assign-parameters"></a>Iniciar um runbook e atribuir parâmetros
Um runbook pode ser iniciado de várias maneiras: por meio de saudação portal do Azure, com um webhook, com os cmdlets do PowerShell, com hello API REST ou com hello SDK. A seguir, discutiremos diferentes métodos para iniciar um runbook e atribuir parâmetros.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Iniciar um runbook publicado usando Olá portal do Azure e atribuir os parâmetros
Quando você [iniciar runbook Olá](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), Olá **iniciar Runbook** folha é aberto e você pode configurar valores de parâmetros de saudação que você acabou de criar.

![Começar a usar o portal de saudação](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

Em rótulo Olá abaixo da caixa de entrada hello, você pode ver atributos Olá que foram definidos para o parâmetro hello. Os atributos incluem obrigatório ou opcional, tipo e valor padrão. No hello ajuda balão próxima toohello nome de parâmetro, você pode ver todas as informações de chave Olá necessário toomake decisões sobre valores de entrada de parâmetro. Essas informações incluem se um parâmetro é obrigatório ou opcional. Ele também inclui Olá tipo e valor padrão (se houver) e outras observações úteis.

![Balão de ajuda](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> Parâmetros do tipo String dão suporte a valores de Cadeia de Caracteres **Vazia** .  Inserir **[EmptyString]** no parâmetro de entrada hello caixa passará um parâmetro de toohello de cadeia de caracteres vazia. Além disso, parâmetros do tipo de cadeia de caracteres não dão suporte à passagem de valores **Nulos** . Se não passar qualquer parâmetro de cadeia de caracteres do valor toohello, em seguida, PowerShell interpretará como nulo.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>Como iniciar um runbook publicado usando cmdlets do PowerShell e atribuir parâmetros
* **Cmdlets do Azure Resource Manager:** você pode iniciar um runbook de Automação criado em um grupo de recursos usando [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).
  
  **Exemplo:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Cmdlets de gerenciamento de serviços do azure:** você pode iniciar um runbook de automação criado em um grupo de recursos padrão usando [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)
  
  **Exemplo:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> Quando você inicia um runbook usando cmdlets do PowerShell, um parâmetro padrão, **MicrosoftApplicationManagementStartedBy** é criado com o valor de saudação **PowerShell**. Você pode exibir esse parâmetro no hello **detalhes do trabalho** folha.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>Como uniciar um runbook usando o SDK e atribuir parâmetros
* **Método do Gerenciador de recursos do Azure:** pode iniciar um runbook usando Olá SDK de uma linguagem de programação. Abaixo está um trecho de código em C# para iniciar um runbook em sua conta de Automação. Você pode exibir todos os códigos de saudação em nosso [repositório GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Método de gerenciamento de serviços do Azure:** pode iniciar um runbook usando Olá SDK de uma linguagem de programação. Abaixo está um trecho de código em C# para iniciar um runbook em sua conta de Automação. Você pode exibir todos os códigos de saudação em nosso [repositório GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart esse método, crie uma saudação do dicionário toostore parâmetros de runbook, **VMName** e **resourceGroupName**e seus valores. Em seguida, inicie o runbook de hello. Abaixo está o trecho de Olá c# código para chamar o método hello definida acima.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Iniciar um runbook usando a API REST de saudação e atribuir os parâmetros
Um trabalho de runbook pode ser criado e iniciado com hello API de REST de automação do Azure usando Olá **colocar** URI de solicitação do método com hello a seguir.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

No URI de solicitação hello, substitua Olá parâmetros a seguir:

* **subscription-id:** a ID de sua assinatura do Azure.  
* **nome do serviço de nuvem:** nome Olá Olá nuvem toowhich Olá de solicitação do serviço deve ser enviada.  
* **nome da conta de automação:** Olá sua conta de automação que está hospedada dentro de saudação especificado de serviço de nuvem.  
* **id do trabalho:** hello GUID para o trabalho de saudação. GUIDs no PowerShell podem ser criados usando Olá **[GUID]::NewGuid(). ToString ()** comando.

No trabalho de runbook do toohello ordem toopass parâmetros, use o corpo da solicitação hello. Ele usa Olá duas propriedades fornecidas no formato JSON a seguir:

* **Nome do Runbook:** Obrigatório. Olá nome do runbook Olá Olá toostart de trabalho.  
* **Parâmetros do Runbook:** Opcional. Um dicionário de lista de parâmetros de saudação (nome, valor) Formatar onde nome deve ser do tipo cadeia de caracteres e o valor pode ser qualquer valor JSON válido.

Se você quiser Olá toostart **Get-AzureVMTextual** runbook criado anteriormente com **VMName** e **resourceGroupName** como parâmetros, use Olá seguindo o formato JSON para o corpo da solicitação hello.

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

Um código de status HTTP 201 será retornado se o trabalho de saudação é criado com êxito. Para obter mais informações sobre cabeçalhos de resposta e o corpo da resposta hello, consulte o artigo toohello sobre como muito[criar um trabalho de runbook usando Olá API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Testar um runbook e atribuir parâmetros
Quando você [teste Olá versão de rascunho do runbook](automation-testing-runbook.md) usando a opção de teste hello, Olá **teste** folha é aberto e você pode configurar valores de parâmetros de saudação que você acabou de criar.

![Como testar e atribuir parâmetros](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>Vincula um runbook tooa de agenda e atribuir os parâmetros
Você pode [vincular um agendamento](automation-schedules.md) tooyour runbook para esse runbook Olá inicia em um momento específico. Você atribui parâmetros de entrada quando você criar agenda de saudação e Olá runbook usará esses valores quando ele for iniciado por agendamento Olá. Você não pode salvar a agenda de saudação até que todos os valores de parâmetro obrigatório são fornecidos.

![Como agendar e atribuir parâmetros](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Criar um webhook de um runbook e atribuir parâmetros
Você pode criar um [webhook](automation-webhooks.md) para seu runbook e configurar parâmetros de entrada do runbook. Você não pode salvar o webhook Olá até que todos os valores de parâmetro obrigatório são fornecidos.

![Como criar o webhook e atribuir parâmetros](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

Quando você executar um runbook usando um webhook, Olá predefinidos de parâmetro de entrada  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  é enviada, juntamente com os parâmetros de entrada hello que você definiu. Você pode clicar em Olá tooexpand **WebhookData** parâmetro para obter mais detalhes.

![Parâmetro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre a entrada e a saída do runbook, consulte [Automação do Azure: entrada do runbook, saída e runbooks aninhados](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).
* Para obter detalhes sobre as diferentes maneiras toostart um runbook, consulte [iniciando um runbook](automation-starting-a-runbook.md).
* tooedit um runbook textual, consulte muito[edição textual runbooks](automation-edit-textual-runbook.md).
* tooedit um runbook gráfico, consulte muito[criação gráfica na automação do Azure](automation-graphical-authoring-intro.md).

