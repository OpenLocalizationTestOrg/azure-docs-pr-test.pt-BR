---
title: "aaaSet o Cofre de chaves do Azure com a rotação de chaves de ponta a ponta e auditoria | Microsoft Docs"
description: "Use este tootoohelp de como você configurar com monitoramento logs de Cofre de chave e rotação de chaves."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>Configurar o Cofre de Chaves do Azure com a rotação de chaves e auditoria de ponta a ponta
## <a name="introduction"></a>Introdução
Depois de criar seu Cofre de chaves, você será capaz de toostart usando esse cofre toostore suas chaves e segredos. Os aplicativos desnecessários toopersist suas chaves ou segredos, mas em vez disso, irá solicitá-las do Cofre de chaves Olá conforme necessário. Isso permite que você tooupdate chaves e segredos sem afetar o comportamento de saudação do seu aplicativo, que abre a uma gama de possibilidades em torno de sua chave e o gerenciamento de informações secretas.

Este artigo o orienta por meio de um exemplo de como usar o Azure Key Vault toostore um segredo, neste caso, uma chave de conta de armazenamento do Azure que é acessada por um aplicativo. Ele também demonstra a implementação de uma rotação agendada dessa chave de conta de armazenamento. Finalmente, ele apresenta uma demonstração de como toomonitor Olá logs de auditoria do Cofre de chaves e gerar alertas quando são feitas solicitações inesperadas.

> [!NOTE]
> Este tutorial não está tooexplain pretendido em detalhe Olá a configuração inicial do seu Cofre de chaves. Para obter essas informações, confira [Introdução ao Cofre da Chave do Azure](key-vault-get-started.md). Para obter instruções sobre a Interface de Linha de Comando de Plataforma Cruzada, confira [Gerenciar Cofre de Chaves usando a CLI](key-vault-manage-with-cli2.md).
>
>

## <a name="set-up-key-vault"></a>Configurar o Cofre de Chaves
tooenable tooretrieve um aplicativo um segredo do Cofre de chaves, você deve primeiro criar segredo hello e carregá-lo tooyour cofre. Isso pode ser feito iniciando uma sessão do PowerShell do Azure e entrar tooyour conta do Azure com hello comando a seguir:

```powershell
Login-AzureRmAccount
```

Na janela de pop-up do navegador hello, insira seu nome de usuário da conta do Azure e a senha. PowerShell obterá todas as assinaturas de saudação que estão associadas essa conta. PowerShell usa Olá um primeiro por padrão.

Se você tiver várias assinaturas, você pode ter toospecify Olá que foi usado toocreate seu Cofre de chaves. Digite hello assinaturas de saudação toosee para sua conta a seguir:

```powershell
Get-AzureRmSubscription
```

assinatura de saudação toospecify associada com o Cofre de chaves Olá que fizerem logon, digite:

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

Como este artigo demonstra como armazenar uma chave de conta de armazenamento como um segredo, você deve obter essa chave de conta de armazenamento.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

Depois de recuperar o segredo (nesse caso, sua chave de conta de armazenamento), você deve converter a cadeia de caracteres segura que tooa e, em seguida, criar um segredo com esse valor em seu Cofre de chaves.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
Em seguida, obter Olá URI segredo Olá criado por você. Isso é usado em uma etapa posterior ao chamar hello Cofre de chaves tooretrieve seu segredo. Execute Olá comando PowerShell a seguir e anote o valor de ID de hello, que é o segredo Olá URI:

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Configurar o aplicativo hello
Agora que você tem um segredo armazenado, você pode usar código tooretrieve e usá-lo. Há algumas etapas e necessário tooachieve isso. Hello primeiro e mais importante etapa é registrar seu aplicativo no Azure Active Directory e, em seguida, informando o Cofre de chaves suas informações de aplicativo para que ele pode permitir que solicitações de seu aplicativo.

> [!NOTE]
> Seu aplicativo deve ser criado em Olá mesmo locatário do Active Directory do Azure como seu Cofre de chaves.
>
>

Abra a guia de aplicativos de saudação do Active Directory do Azure.

![Abrir os aplicativos no Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

Escolha **adicionar** tooadd tooyour um aplicativo do Azure Active Directory.

![Escolha ADICIONAR](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Deixe o tipo de aplicativo hello como **aplicativo de WEB e/ou API WEB** e dê um nome de seu aplicativo.

![Aplicativo hello nome](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

Dê ao aplicativo uma **URL de logon** e um **URI de ID de aplicativo**. Eles podem ser qualquer coisa que você desejar para esta demonstração e podem ser alterados posteriormente, se necessário.

![Fornecer os URIs necessários](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Depois que o aplicativo hello é adicionado tooAzure do Active Directory, você será levado à página de aplicativo hello. Clique em Olá **configurar** guia e, em seguida, localize e copie Olá **ID do cliente** valor. Anote a ID do cliente Olá para etapas posteriores.

Em seguida, gere uma chave para o aplicativo para que ele possa interagir com o Azure Active Directory. Você pode criá-lo em Olá **chaves** seção Olá **configuração** guia. Anote chave Olá recentemente gerado do seu aplicativo do Active Directory do Azure para uso em uma etapa posterior.

![Chaves de aplicativo do Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Antes de estabelecer as chamadas do seu aplicativo em um cofre de chaves hello, você deve informar o Cofre de chaves Olá sobre seu aplicativo e suas permissões. Olá comando a seguir obtém nome do cofre hello e ID do cliente de saudação do seu aplicativo do Active Directory do Azure e concede **obter** cofre da chave tooyour acesso para o aplicativo hello.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

Neste ponto, você está pronto toostart compilar seu aplicativo chama. Em seu aplicativo, você deve instalar Olá NuGet pacotes necessário toointeract com o Cofre de chaves do Azure e o Azure Active Directory. No console do Gerenciador de pacote do Visual Studio hello, digite Olá comandos a seguir. Na gravação da saudação deste artigo, a versão atual de saudação do pacote do Azure Active Directory Olá é 3.10.305231913, para que você pode ser a versão mais recente do tooconfirm hello e atualizar adequadamente.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

No código do aplicativo, crie um método de saudação do toohold de classe para a autenticação do Active Directory do Azure. Neste exemplo a classe é chamada **Utils**. Adicione o seguinte Olá usando a instrução:

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Em seguida, adicione Olá após o token JWT do método tooretrieve Olá do Active Directory do Azure. Para fins de manutenção, convém toomove valores de cadeia de caracteres codificada de saudação em sua configuração de web ou aplicativo.

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

Adicionar Olá código necessário toocall Cofre de chaves e recuperar seu valor secreto. Primeiro você deve adicionar a seguinte hello usando a instrução:

```csharp
using Microsoft.Azure.KeyVault;
```

Adicionar tooinvoke chamadas de método hello Cofre de chaves e recuperar o segredo. Nesse método, você deve fornecer segredo Olá URI que você salvou na etapa anterior. Observe o uso de saudação do hello **GetToken** método da saudação **utilitários** classe criada anteriormente.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

Quando você executar o aplicativo, você agora deve autenticar tooAzure do Active Directory e, em seguida, recuperar o valor de segredo do Cofre de chaves do Azure.

## <a name="key-rotation-using-azure-automation"></a>Rotação de chaves usando a Automação do Azure
Há várias opções para implementar uma estratégia de rotação para valores armazenados como segredos do Cofre de Chaves do Azure. Os segredos podem ser rotacionados como parte de um processo manual, programaticamente usando chamadas à API ou por meio de um script de Automação. Para fins de saudação deste artigo, você será usando o PowerShell Azure combinado com toochange de automação do Azure, uma chave de acesso da conta de armazenamento do Azure. Em seguida, você atualizará um segredo do cofre de chaves com essa nova chave.

tooallow automação do Azure tooset secretos valores em seu Cofre de chaves, você deve obter ID de saudação do cliente para conexão Olá denominado AzureRunAsConnection, que foi criado quando você estabelecer sua instância de automação do Azure. Você pode localizar a ID selecionando **Ativos** da instância da Automação do Azure. A partir daí, você deve escolher **conexões** e, em seguida, selecione Olá **AzureRunAsConnection** princípio de serviço. Anote Olá **ID do aplicativo**.

![ID do cliente da Automação do Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

Em **Ativos**, escolha **Módulos**. De **módulos**, selecione **galeria**e, em seguida, procure e **importação** versões atualizadas dos cada Olá módulos a seguir:

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> A gravação da saudação deste artigo, hello mencionado anteriormente módulos necessários toobe atualizado apenas para Olá script a seguir. Se achar que o trabalho de automação está falhando, confirme se importou todos os módulos necessários e suas dependências.
>
>

Depois de recuperar ID do aplicativo hello para sua conexão de automação do Azure, você deve informar o seu Cofre de chaves que esse aplicativo tenha acesso tooupdate segredos em seu cofre. Isso pode ser feito com hello comando PowerShell a seguir:

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

Em seguida, selecione **Runbooks** na instância da Automação do Azure e selecione **Adicionar um Runbook**. Selecione **Criação Rápida**. Nome do seu runbook e selecione **PowerShell** como tipo de runbook hello. Você tem Olá opção tooadd uma descrição. Por fim, clique em **Criar**.

![Criar runbook](./media/keyvault-keyrotation/Create_Runbook.png)

Saudação de colar o script do PowerShell no painel do editor de saudação para seu novo runbook a seguir:

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

No painel do editor de saudação, escolha **painel teste** tootest seu script. Depois que o script hello está sendo executado sem erro, você pode selecionar **publicar**, e, em seguida, você pode aplicar uma agenda para Olá runbook no painel de configuração de runbook hello.

## <a name="key-vault-auditing-pipeline"></a>Pipeline de auditoria do Cofre de Chaves
Quando você configura um cofre de chaves, você pode ativar a auditoria toocollect logs em solicitações de acesso feitas toohello Cofre de chaves. Esses logs são armazenados em uma conta de armazenamento do Azure designada e podem ser extraídos, monitorados e analisados. Olá cenário a seguir usa funções do Azure, aplicativos lógicos do Azure e toocreate de logs de auditoria do Cofre de chaves toosend um pipeline um email quando um aplicativo que corresponde à ID do aplicativo de saudação do aplicativo web de saudação recupera segredos de cofre hello.

Primeiro, você deve habilitar o log no cofre de chaves. Isso pode ser feito por meio de saudação comandos do PowerShell a seguir (detalhes completos podem ser vistos no [registro de Cofre de chave](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

Depois que isso é habilitado, os logs de auditoria iniciar coleta em Olá designado a conta de armazenamento. Esses logs contêm eventos sobre como e quando os cofres de chaves são acessados e por quem.

> [!NOTE]
> Você pode acessar suas informações de registro em log 10 minutos após a operação de Cofre de chaves de saudação. Geralmente será mais rápido do que isso.
>
>

Olá próxima etapa é muito[criar uma fila do barramento de serviço do Azure](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md). Esse é o local para o qual os logs de auditoria do cofre de chaves são enviados. Quando mensagens de saudação do log de auditoria na fila hello, Olá lógica aplicativo seleciona-los e age sobre eles. Crie um barramento de serviço com hello etapas a seguir:

1. Criar um namespace de barramento de serviço (se você já tiver um que você deseja toouse para isso, ignorar tooStep 2).
2. Procure o barramento de serviço toohello Olá portal do Azure e selecione Olá namespace em que deseja toocreate fila de saudação.
3. Selecione **novo** e escolha **barramento de serviço > fila** e insira os detalhes de saudação necessária.
4. Selecione informações de conexão do barramento do serviço Olá escolhendo Olá namespace e clicando em **informações de Conexão**. Você precisará dessas informações para a próxima seção de saudação.

Em seguida, [criar uma função do Azure](../azure-functions/functions-create-first-azure-function.md) toopoll logs de Cofre de chaves no hello conta de armazenamento e retirar os novos eventos. Essa será uma função disparada em um cronograma.

toocreate uma função do Azure, escolha **Novo > função de aplicativo** em Olá portal do Azure. Durante a criação, você pode usar um plano de hospedagem existente ou criar um novo. Você também pode optar pela hospedagem dinâmica. Mais detalhes sobre opções de hospedagem de função podem ser encontrados em [como tooscale funções do Azure](../azure-functions/functions-scale.md).

Quando Olá função do Azure é criada, navegar tooit e escolha um timer de função e C\#. Em seguida, clique em **Criar esta função**.

![Folha de Início das Funções do Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

Em Olá **desenvolver** guia, substitua o código de run.csx Olá pela seguinte hello:

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> Faça tooreplace-se de que variáveis de saudação na Olá anterior conta de armazenamento do código toopoint tooyour onde Olá Cofre de chaves logs são gravados, criada anteriormente, o barramento de serviço hello e Olá logs de armazenamento de Cofre de chaves de toohello caminho específico.
>
>

função Hello pega hello mais recente arquivo de log da conta de armazenamento Olá onde Olá Cofre de chaves logs são gravados, captura os eventos mais recentes Olá desse arquivo, e envia-os tooa fila de barramento de serviço. Como um único arquivo pode ter vários eventos, você deve criar um arquivo de sync.txt função hello também analisa toodetermine Olá carimbo de data do último evento de saudação que foi recebido. Isso garante que você não enviar Olá mesmo evento várias vezes. Este arquivo sync.txt contém um carimbo de hora para o último evento de encontrado hello. Olá, logs, quando carregado, tem toobe classificado com base em Olá timestamp tooensure eles serão ordenados corretamente.

Para esta função, podemos fazer referência a algumas bibliotecas adicionais que não estão disponíveis sem a necessidade de saudação em funções do Azure. tooinclude isso, precisamos de funções do Azure toopull-los usando o NuGet. Escolha Olá **exibir arquivos** opção.

![Opção Exibir Arquivos](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

Adicione um arquivo chamado project.json com o seguinte conteúdo:

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
Após a **salvar**, funções do Azure será baixado binários Olá necessário.

Alternar toohello **integrar** guia e dar ao parâmetro de timer de saudação toouse um nome significativo em função hello. Olá precede o código, ele espera que Olá timer toobe chamado *myTimer*. Especifique um [expressão CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) da seguinte maneira: 0 \* \* \* \* \* pelo temporizador hello que causarão Olá função toorun a cada minuto.

Olá na mesma **integrar** guia, adicione uma entrada do tipo hello **armazenamento de BLOBs do Azure**. Isso vai apontar toohello sync.txt arquivo que contém Olá carimbo de hora do último evento de saudação verificado pela função hello. Isso estará disponível em função hello pelo nome do parâmetro hello. Olá precede o código, Olá entrada de armazenamento de BLOBs do Azure espera que toobe de nome de parâmetro hello *inputBlob*. Escolha Olá conta de armazenamento onde o arquivo de sync.txt Olá residirá (pode ser Olá mesmo ou outra conta de armazenamento). No campo de caminho hello, forneça o caminho de saudação onde o arquivo hello reside no formato Olá {container-name}/path/to/sync.txt.

Adicionar uma saída de tipo hello *armazenamento de BLOBs do Azure* saída. Isso vai apontar toohello sync.txt arquivo definido na entrada hello. Isso é usado pelo Olá função toowrite Olá carimbo de hora Olá último evento examinado. o código anterior Hello espera este toobe parâmetro chamado *outputBlob*.

Neste ponto, a função hello está pronta. Fazer toohello back se tooswitch **desenvolver** guia e salve o código de saudação. Verifique a janela de saída Olá para os erros de compilação e corrija-as adequadamente. Se código Olá compila, código Olá deve agora ser verificando Olá Cofre de chaves logs a cada minuto, e enviar quaisquer novos eventos para Olá definido fila do barramento de serviço. Você deve ver as informações de log gravar toohello a janela de log sempre que a função hello é disparada.

### <a name="azure-logic-app"></a>Aplicativo lógico do Azure
Em seguida, você deve criar um aplicativo do Azure lógica que seleciona eventos Olá função hello está fazendo a fila do barramento de serviço toohello, analisa o conteúdo de saudação e envia um email com base em um critério de correspondência.

[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) indo muito**Novo > aplicativo lógico**.

Depois de criar o aplicativo lógico de saudação, navegar tooit e escolher **editar**. No editor de aplicativo da lógica de saudação, escolha **fila do barramento de serviço** e insira sua tooconnect de credenciais do barramento de serviço-toohello fila.

![Barramento de Serviço de aplicativo lógico do Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

Depois, escolha **Adicionar uma condição**. Na condição de saudação alternar toohello editor avançado e digite Olá código a seguir, substituindo APP_ID com hello APP_ID real de seu aplicativo web:

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

Essa expressão retorna essencialmente **false** se hello *appid* de saudação evento de entrada (que é o corpo de saudação da mensagem de saudação do barramento de serviço) não é Olá *appid* de saudação aplicativo.

Agora, crie uma ação em **Se não, não faça nada**.

![Escolher ação do aplicativo lógico do Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Para a ação de saudação, escolha **Office 365 - enviar email**. Preencha Olá campos toocreate toosend um email quando Olá definido a condição retorna **false**. Se você não tiver o Office 365, você pode examinar alternativas tooachieve Olá os mesmos resultados.

Neste ponto, você tem um pipeline de tooend final que procura os logs de auditoria do novo cofre de chaves a cada minuto. Ele envia novos logs encontrar tooa fila do barramento de serviço. aplicativo de lógica de saudação é disparado quando uma nova mensagem chega na fila de saudação. Se hello *appid* dentro Olá eventos não correspondem Olá ID do aplicativo de saudação aplicativo de chamada, ele envia um email.
