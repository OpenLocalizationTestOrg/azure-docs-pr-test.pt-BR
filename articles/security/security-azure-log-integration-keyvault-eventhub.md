---
title: logs de aaaIntegrate do Cofre de chaves do Azure usando os Hubs de eventos | Microsoft Docs
description: "Tutorial que fornece as etapas necessárias de saudação toomake Cofre de chaves logs disponível tooa SIEM usando a integração de Log do Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Tutorial de integração de log do Azure: processar eventos do Azure Key Vault usando Hubs de Eventos

Você pode usar a integração do Azure Log tooretrieve registrado eventos e torná-los disponíveis tooyour segurança informações e eventos (SIEM) sistema de gerenciamento de. Este tutorial mostra um exemplo de como a integração do Azure Log pode ser usado tooprocess logs adquiridas por meio de Hubs de eventos do Azure.
 
Use este tutorial tooget familiarizado com como o trabalho de integração de Log do Azure e Hubs de eventos juntos seguindo Olá etapas de exemplo e entender como cada etapa dá suporte à solução de saudação. Em seguida, você pode executar o que você aprendeu aqui toocreate toosupport suas próprias etapas requisitos exclusivos da sua empresa.

>[!WARNING]
etapas de saudação e os comandos neste tutorial não são toobe pretendido copiados e colados. Elas são apenas exemplos. Não use comandos do PowerShell hello "como está" em seu ambiente dinâmico. Você deve personalizá-los com base em seu ambiente exclusivo.


Este tutorial orienta você pelo processo de saudação de colocar o hub de eventos de tooan conectado de atividade de Cofre de chaves do Azure e torná-lo disponível como JSON arquivos tooyour SIEM sistema. Você pode configurar os arquivos JSON de saudação do SIEM sistema tooprocess.

>[!NOTE]
>A maioria das etapas neste tutorial Olá envolve configurar cofres de chaves, contas de armazenamento e hubs de eventos. as etapas específicas de integração do Azure Log Olá são final Olá deste tutorial. Não execute estas etapas em um ambiente de produção. Elas servem apenas para um ambiente de laboratório. Você deve personalizar as etapas de saudação antes de usá-los em produção.

As informações fornecidas ao longo de ajuda de maneira Olá que entender motivos Olá atrás de cada etapa. Artigos de tooother links fornecem mais detalhes sobre determinados tópicos.

Para obter mais informações sobre os serviços de saudação mencionadas neste tutorial, consulte: 

- [Cofre da Chave do Azure](../key-vault/key-vault-whatis.md)
- [Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Integração de log do Azure](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>Configuração inicial

Antes de concluir as etapas de saudação neste artigo, você precisa seguir hello:

1. Uma assinatura do Azure e uma conta nessa assinatura com direitos de administrador. Se você não tem uma assinatura, você pode criar um [conta gratuita](https://azure.microsoft.com/free/).
 
2. Um sistema com toohello de acesso à internet que atenda aos requisitos de saudação para a integração do Azure Log de instalação. sistema Olá pode estar em um serviço de nuvem ou hospedado no local.

3. [Integração de log do Azure](https://www.microsoft.com/download/details.aspx?id=53324) instalada. tooinstall-lo:

   a. Use a área de trabalho remota tooconnect toohello sistema mencionado na etapa 2.   
   b. Copie o sistema de toohello de instalador de integração do Azure Log hello. Você pode [baixar arquivos de instalação Olá](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Iniciar o instalador hello e aceite Olá Microsoft Software License Terms.   
   d. Se você fornecerá informações de telemetria, deixe a caixa de seleção hello. Se você preferir enviar não tooMicrosoft de informações de uso, desmarque a caixa de seleção de saudação.
   
   Para obter mais informações sobre a integração do Log do Azure e como tooinstall, consulte [integração de Log do Azure com o log de diagnóstico do Azure e o encaminhamento de eventos do Windows](security-azure-log-integration-get-started.md).

4. versão mais recente do PowerShell Hello.
 
   Se você tem o Windows Server 2016 instalado, você tem, no mínimo, o PowerShell 5.0. Se estiver usando outra versão do Windows Server, pode ser que você tenha uma versão anterior do PowerShell instalada. Você pode verificar a versão de hello inserindo ```get-host``` em uma janela do PowerShell. Se você não tiver o PowerShell 5.0 instalado, você poderá [baixá-lo](https://www.microsoft.com/download/details.aspx?id=50395).

   Depois de ter pelo menos PowerShell 5.0, você pode continuar a versão mais recente do tooinstall hello:
   
   a. Em uma janela do PowerShell, digite Olá ```Install-Module Azure``` comando. Conclua as etapas de instalação hello.    
   b. Digite hello ```Install-Module AzureRM``` comando. Conclua as etapas de instalação hello.

   Para obter mais informações, consulte [Instalar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Criar elementos de suporte da infraestrutura

1. Abra uma janela do PowerShell com privilégios elevados e vá muito**C:\Program Files\Microsoft Azure Log integração**.
2. Importe Olá AzLog cmdlets executando o script hello LoadAzLogModule.ps1. Digite hello `.\LoadAzLogModule.ps1` comando. (Olá aviso ". \" nesse comando.) Você deverá ver algo assim:</br>

   ![Lista de módulos carregados](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Digite hello `Login-AzureRmAccount` comando. Na janela de logon hello, insira as informações de credencial de Olá para assinatura de saudação que você usará para este tutorial.

   >[!NOTE]
   >Se isso for Olá pela primeira vez que você estiver fazendo o logon em tooAzure desta máquina, você verá uma mensagem sobre a permissão de dados de uso do Microsoft toocollect do PowerShell. É recomendável que você habilite a coleta de dados porque ele será usado tooimprove PowerShell do Azure.

4. Após a autenticação bem-sucedida, você está conectado e ver informações Olá Olá captura de tela a seguir. Anote o nome da assinatura Olá ID e a assinatura, porque eles são necessários toocomplete etapas mais tarde.

   ![Janela do PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Crie variáveis toostore valores que serão usados posteriormente. Insira cada Olá PowerShell linhas a seguir. Talvez seja necessário tooadjust Olá valores toomatch seu ambiente.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (O nome da sua assinatura pode ser diferente. Você poderá ver isso como parte da saída de saudação do comando anterior hello.)
    - ```$location = 'West US'```(Essa variável será local de saudação toopass usado onde recursos devem ser criados. Você pode alterar essa variável toobe qualquer local de sua escolha.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(Olá nome pode ser qualquer, mas ele deve conter apenas letras minúsculas e números).
    - ``` $storageName = $name```(Essa variável será usada para o nome de conta de armazenamento hello.)
    - ```$rgname = $name ```(Essa variável será usada para o nome do grupo de recursos hello.)
    - ``` $eventHubNameSpaceName = $name```(Esse é o nome de saudação do namespace de hub de eventos de saudação).
6. Especifique a assinatura de saudação que você estará trabalhando com:
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Crie um grupo de recursos:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Se você inserir `$rg` neste ponto, você deve ver a saída de tela de toothis semelhante:

   ![Saída após a criação de um grupo de recursos](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Crie uma conta de armazenamento que será usado tookeep rastrear informações de estado:
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Crie um namespace de hub de eventos de saudação. Isso é necessário toocreate um hub de eventos.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Obter Olá ID da regra que será usado com o provedor de insights hello:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Obter todos os possíveis locais do Azure e adicione a variável de tooa de nomes de saudação que pode ser usado em uma etapa posterior:
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Se você inserir `$locations` neste ponto, você verá nomes de local de saudação sem informações adicionais de saudação retornadas por Get-AzureRmLocation.
12. Criar um perfil de log do Azure Resource Manager: 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Para obter mais informações sobre Olá perfil de registro do Azure, consulte [visão geral da saudação Log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> Você pode obter uma mensagem de erro ao tentar toocreate um perfil de registro. Em seguida, você pode revisar documentação Olá para Get-AzureRmLogProfile e remover AzureRmLogProfile. Se você executar Get-AzureRmLogProfile, você pode ver informações sobre o perfil do log de saudação. Você pode excluir o perfil de log existente da saudação inserindo Olá ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` comando.
>
>![Erro de perfil do Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Criar um cofre de chave

1. Crie Cofre de chaves de saudação:

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Configure o log para o Cofre de chaves hello:

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Gerar atividade de log

Solicitações necessário toobe enviado tooKey atividade de log de toogenerate do cofre. Ações como geração de chaves, armazenamento de segredos ou leitura de segredos do Key Vault criarão entradas de log.

1. Exibir chaves de armazenamento atual da saudação:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Gerar uma nova **key2**:
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Exibir chaves Olá novamente e veja que **key2** contém um valor diferente:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Definir e ler um segredo toogenerate entradas de log adicionais:
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Segredo retornado](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Configurar a integração de log do Azure

Agora que você configurou o hub de eventos do hello elementos necessários toohave registro de Cofre de chaves tooan todos, é necessário tooconfigure integração do Azure Log:

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Execute o comando de AzLog de saudação para cada hub de eventos:

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

Após um minuto ou de execução Olá dois últimos comandos, você deve ver os arquivos JSON que está sendo gerados. Você pode confirmar que monitoramento Olá diretório **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Próximas etapas

- [Perguntas frequentes sobre a integração de log do Azure](security-azure-log-integration-faq.md)
- [Introdução à integração de log do Azure](security-azure-log-integration-get-started.md)
- [Integrar logs de recursos do Azure nos seus sistemas SIEM](security-azure-log-integration-overview.md)
