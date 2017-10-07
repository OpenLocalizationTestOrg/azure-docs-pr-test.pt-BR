---
title: "aaaUse proativo de toodo de captura de pacote de rede de monitoramento com alertas e funções do Azure | Microsoft Docs"
description: Este artigo descreve como toocreate um alerta acionado captura de pacote com o observador de rede do Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Usar a captura de pacotes para fazer um monitoramento de rede proativo com alertas e o Azure Functions

Captura de pacote do Inspetor de rede cria sessões de captura de tráfego tootrack dentro e fora de máquinas virtuais. Olá captura arquivo pode ter um filtro que é definido tootrack Olá somente o tráfego que você deseja toomonitor. Esses dados, em seguida, são armazenados em um blob de armazenamento ou localmente no computador de convidado hello.

Esse recurso pode ser iniciado remotamente a partir de outros cenários de automação como o Azure Functions. Fornece de captura de pacote em que Hello capturas de pró-ativo toorun de recurso com base definido anomalias na rede. Outros usos incluem a coleta de estatísticas de rede, obtenção de informações sobre as invasões de rede, depuração de comunicações cliente-servidor e muito mais.

Os recursos implantados no Azure estão em execução 24/7. Você e sua equipe ativamente não é possível monitorar o status de saudação de todos os recursos 24/7. Por exemplo, o que acontecerá se ocorrer um problema às 2:00 da manhã?

Usando o observador de rede, alertas e funções de em Olá ecossistema do Azure, você pode responder proativamente com problemas de toosolve de dados e ferramentas de saudação em sua rede.

![Cenário][scenario]

## <a name="prerequisites"></a>Pré-requisitos

* versão mais recente de saudação do [Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Uma instância existente do Observador de Rede. Se você ainda não tiver um, [crie uma instância do Observador de Rede](network-watcher-create.md).
* Uma máquina virtual existente no hello mesma região do observador de rede com hello [extensão Windows](../virtual-machines/windows/extensions-nwa.md) ou [extensão da máquina virtual Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Cenário

Neste exemplo, a VM estiver enviando mais segmentos TCP que o usual e desejar toobe alertado. Os segmentos TCP são usados como um exemplo aqui, e você pode utilizar qualquer condição de alerta.

Quando você for alertado, você deseja tooreceive toounderstand de dados de nível de pacote por comunicação aumentou. Em seguida, você pode adotar medidas comunicação de tooregular tooreturn Olá máquina virtual.

Este cenário pressupõe que você tem uma instância existente do Observador de Rede e um grupo de recursos com uma máquina virtual válida.

Olá lista a seguir é uma visão geral de fluxo de trabalho Olá ocorre:

1. Um alerta é disparado em sua VM.
1. alerta de saudação chama a função do Azure por meio de um webhook.
1. A função do Azure processa alerta hello e inicia uma sessão de captura de pacote do observador de rede.
1. captura de pacote de saudação é executado em Olá VM e o tráfego de coleta.
1. Olá arquivo de captura de pacote é carregado tooa conta de armazenamento para diagnóstico e análise.

tooautomate esse processo, podemos criar e conecte-se um alerta em nosso tootrigger VM quando Olá incidente. Também criamos uma função toocall em observador de rede.

Este cenário Olá a seguir:

* Cria uma função do Azure que inicia uma captura de pacotes.
* Cria uma regra de alerta em uma máquina virtual e configura Olá toocall da regra de alerta Olá função do Azure.

## <a name="create-an-azure-function"></a>Criar uma função do Azure

Olá primeira etapa é toocreate um alerta de saudação do tooprocess de função do Azure e criar uma captura de pacote.

1. Em Olá [portal do Azure](https://portal.azure.com), selecione **novo** > **de computação** > **aplicativo função**.

    ![Criar um aplicativo de funções][1-1]

2. Em Olá **aplicativo função** folha, digite Olá valores a seguir e, em seguida, selecione **Okey** toocreate Olá aplicativo:

    |**Configuração** | **Valor** | **Detalhes** |
    |---|---|---|
    |**Nome do aplicativo**|PacketCaptureExample|nome de saudação do aplicativo de função hello.|
    |**Assinatura**|[Sua assinatura] Olá assinatura para qual aplicativo de função toocreate hello.||
    |**Grupo de recursos**|PacketCaptureRG|Olá recurso grupo toocontain Olá função app.|
    |**Plano de hospedagem**|Plano de consumo| tipo de saudação do plano de seu aplicativo usa de função. As opções são planos de consumo ou planos do serviço de aplicativo do Azure. |
    |**Localidade**|Centro dos EUA| região de saudação em qual aplicativo de função toocreate hello.|
    |**Conta de armazenamento**|{gerado automaticamente}| conta de armazenamento de saudação que precisa de funções do Azure para armazenamento de uso geral.|

3. Em Olá **PacketCaptureExample função aplicativos** folha, selecione **funções** > **função personalizada**  >  **+**.

4. Selecione **HttpTrigger Powershell**e, em seguida, digite Olá restantes informações. Por fim, toocreate função hello, selecione **criar**.

    |**Configuração** | **Valor** | **Detalhes** |
    |---|---|---|
    |**Cenário**|Experimental|Tipo de cenário|
    |**Nomeie sua função**|AlertPacketCapturePowerShell|Nome da função hello|
    |**Nível de autorização**|Função|Nível de autorização para a função hello|

![Exemplo de funções][functions1]

> [!NOTE]
> modelo de PowerShell Olá é experimental e não tem suporte completo.

As personalizações são necessárias para este exemplo e são explicadas em Olá etapas a seguir.

### <a name="add-modules"></a>Adicionar módulos

toouse cmdlets do PowerShell do Inspetor de rede, carregar o aplicativo hello mais recente do PowerShell módulo toohello função.

1. Em seu computador local com hello mais recentes do Azure PowerShell módulos instalados, execute Olá comando PowerShell a seguir:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    Isso proporciona exemplo hello caminho local dos seus módulos do PowerShell do Azure. Essas pastas são usadas em uma etapa posterior. módulos de saudação que são usados neste cenário são:

    * AzureRM.Network

    * AzureRM.profile

    * AzureRM.Resources

    ![Pastas do PowerShell][functions5]

1. Selecione **configurações do aplicativo de função** > **vá tooApp Editor serviço**.

    ![Configurações do aplicativo de funções][functions2]

1. Saudação de atalho **AlertPacketCapturePowershell** pasta e, em seguida, crie uma pasta chamada **azuremodules**. 

4. Crie uma subpasta para cada módulo de que você precisa.

    ![Pastas e subpastas][functions3]

    * AzureRM.Network

    * AzureRM.profile

    * AzureRM.Resources

1. Saudação de atalho **AzureRM.Network** subpasta e, em seguida, selecione **carregar arquivos**. 

6. Vá tooyour Azure módulos. No local de saudação **AzureRM.Network** pasta, selecione todos os arquivos de saudação na pasta hello. Depois, selecione **OK**. 

7. Repita essas etapas para **AzureRM.Profile** e **AzureRM.Resources**.

    ![Carregar arquivos][functions6]

1. Depois de concluir, cada pasta deve ter arquivos de módulo do PowerShell Olá em sua máquina local.

    ![Arquivos do PowerShell][functions7]

### <a name="authentication"></a>Autenticação

cmdlets do PowerShell Olá toouse, você deverá se autenticar. Configurar a autenticação no aplicativo de função hello. autenticação tooconfigure, você deve configurar variáveis de ambiente e carregar um aplicativo de função de toohello do arquivo de chave criptografada.

> [!NOTE]
> Este cenário fornece apenas um exemplo de como a autenticação tooimplement com funções do Azure. Existem outra maneiras toodo isso.

#### <a name="encrypted-credentials"></a>Credenciais criptografadas

saudação de script do PowerShell a seguir cria um arquivo de chave chamado **PassEncryptKey.key**. Ele também fornece uma versão criptografada da senha de saudação que é fornecida. Essa senha é hello mesma senha que é definida para o aplicativo do Active Directory do Azure hello que é usado para autenticação.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

Olá Editor de aplicativo do serviço de aplicativo de função hello, cria uma pasta chamada **chaves** em **AlertPacketCapturePowerShell**. Em seguida, carregar Olá **PassEncryptKey.key** arquivo criado no exemplo anterior de PowerShell hello.

![Chave de funções][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Recuperar valores de variáveis de ambiente

requisito de final de saudação é tooset variáveis de ambiente de saudação são valores de saudação tooaccess necessário para autenticação. Olá lista a seguir mostra as variáveis de ambiente de saudação que são criadas:

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

ID do cliente Olá é hello ID de um aplicativo no Azure Active Directory.

1. Se você ainda não tiver um aplicativo toouse, execute um aplicativo para Olá toocreate de exemplo a seguir.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > senha de saudação que você usa ao criar o aplicativo hello deveria ser Olá mesma senha que você criou anteriormente ao salvar o arquivo de chave de saudação.

1. No portal do Azure de Olá, selecione **assinaturas**. Selecione Olá assinatura toouse e, em seguida, selecione **(IAM) do controle de acesso**.

    ![IAM de funções][functions9]

1. Escolha Olá conta toouse e, em seguida, selecione **propriedades**. Copiar Olá ID do aplicativo.

    ![ID do Aplicativo de funções][functions10]

#### <a name="azuretenant"></a>AzureTenant

Obter ID de locatário Olá executando Olá PowerShell de exemplo a seguir:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

valor de Olá Olá AzureCredPassword da variável de ambiente é o valor de saudação obtido executando Olá PowerShell de exemplo a seguir. Este exemplo é Olá mesmo que é mostrada na saudação anterior **credenciais criptografadas** seção. Olá valor que é necessário Olá de saída de hello `$Encryptedpassword` variável.  Isso é Olá serviço principal senha criptografada usando o script do PowerShell hello.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Variáveis de ambiente de saudação do repositório

1. Vá toohello função app. Selecione **Configurações do aplicativo de função** > **Definir configurações de aplicativo**.

    ![Definir configurações de aplicativo][functions11]

1. Adicionar variáveis de ambiente hello e suas configurações de aplicativo toohello valores e, em seguida, selecione **salvar**.

    ![Configurações do aplicativo][functions12]

### <a name="add-powershell-toohello-function"></a>Adicionar a função do PowerShell toohello

Agora é hora toomake chamadas em observador de rede de dentro de Olá função do Azure. Dependendo dos requisitos de hello, implementação Olá dessa função pode variar. No entanto, o fluxo geral de saudação do código de saudação é o seguinte:

1. Processar os parâmetros de entrada.
2. Pacote existente de consulta de captura tooverify limites e resolver conflitos de nome.
3. Criar uma captura de pacotes com os devidos parâmetros.
4. Pesquisar a captura de pacotes periodicamente até concluir.
5. Notifica o usuário Olá que a sessão de captura de pacote de saudação foi concluída.

Olá, exemplo a seguir é código do PowerShell que pode ser usado na função de saudação. Há valores que precisam toobe substituído para **subscriptionId**, **resourceGroupName**, e **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Recuperar a URL de função hello 
1. Depois de criar sua função, configure a URL do hello toocall alerta associado à função hello. tooget esse valor, copiar Olá função URL de seu aplicativo de função.

    ![Localizando Olá função URL][functions13]

2. Copie URL de função Olá para seu aplicativo de função.

    ![Copiar URL da função de saudação][2]

Se você precisar de propriedades personalizadas na carga de saudação de solicitação POST webhook hello, consulte muito[configurar um webhook em um alerta de métrica do Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Configurar um alerta em uma VM

Alertas podem ser configurados toonotify indivíduos quando uma métrica específica exceder um limite atribuído tooit. Neste exemplo, alerta hello está em Olá segmentos TCP que são enviados, mas Olá alerta pode ser acionado para muitas outras métricas. Neste exemplo, um alerta é configurado toocall uma função de saudação do webhook toocall.

### <a name="create-hello-alert-rule"></a>Criar regra de alerta de saudação

Vá tooan máquina de virtual existente e, em seguida, adicione uma regra de alerta. Mais documentação detalhada sobre como configurar alertas pode ser encontrada em [Criar alertas do Monitor do Azure para serviços do Azure - Portal do Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). Digite Olá Olá valores a seguir **regra de alerta** folha e, em seguida, selecione **Okey**.

  |**Configuração** | **Valor** | **Detalhes** |
  |---|---|---|
  |**Nome**|TCP_Segments_Sent_Exceeded|Nome da regra de alerta de saudação.|
  |**Descrição**|Segmentos TCP enviados limite excedido|Descrição de saudação de regra de alerta de saudação.||
  |**Métrica**|Segmentos TCP enviados| alerta de saudação do Hello métrica toouse tootrigger. |
  |**Condição**|Maior que| Olá condição toouse ao avaliar a métrica de saudação.|
  |**Limite**|100| valor de saudação da métrica de saudação que dispara um alerta de saudação. Esse valor deve ser definido como tooa o valor válido para o seu ambiente.|
  |**Período**|Sobre Olá últimos cinco minutos| Determina o período de saudação na qual toolook para o limite de saudação na métrica hello.|
  |**Webhook**|[URL do webhook do aplicativo de funções]| URL do webhook saudação do aplicativo de função hello criado nas etapas anteriores hello.|

> [!NOTE]
> métrica de segmentos TCP Olá não está habilitada por padrão. Saiba mais sobre como as métricas adicionais de tooenable visitando [habilitar o monitoramento e diagnóstico](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Examine os resultados de saudação

Depois de critérios de saudação para gatilhos alerta hello, uma captura de pacote é criada. Vá tooNetwork Inspetor e, em seguida, selecione **captura de pacote**. Nessa página, você pode selecionar Olá captura arquivo link toodownload Olá pacote captura de pacote.

![Exibir a captura de pacotes][functions14]

Se o arquivo de captura Olá é armazenado localmente, você pode recuperá-lo ao entrar na máquina virtual de toohello.

Para obter instruções sobre como baixar os arquivos das contas de armazenamento do Azure, veja [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Outra ferramenta que você pode usar é o [Gerenciador de armazenamento](http://storageexplorer.com/).

Depois que a captura for baixada, você poderá exibi-la usando qualquer ferramenta que possa ler um arquivo **.cap**. Estes são links tootwo dessas ferramentas:

- [Analisador de Mensagens da Microsoft](https://technet.microsoft.com/library/jj649776.aspx)
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>Próximas etapas

Saiba como tooview seu pacote captura visitando [análise de captura de pacote com o Wireshark](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
