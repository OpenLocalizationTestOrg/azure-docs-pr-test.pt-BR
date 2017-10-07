---
title: aaaUsing PowerShell do Azure com o armazenamento do Azure | Microsoft Docs
description: "Saiba como toouse Olá cmdlets do PowerShell do Azure para armazenamento do Azure toocreate e gerenciar contas de armazenamento; trabalhar com tabelas, blobs, filas e arquivos; Configurar a análise de armazenamento de consulta e criar assinaturas de acesso compartilhado."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Usando o PowerShell do Azure com o Armazenamento do Azure
## <a name="overview"></a>Visão geral
PowerShell do Azure é um módulo que fornece toomanage de cmdlets do Azure por meio do Windows PowerShell. Ele é um shell de linha de comando baseado em tarefa e linguagem de script criado especialmente para administração do sistema. Com o PowerShell, você pode facilmente controlar e automatizar a administração de saudação de aplicativos e serviços do Azure. Por exemplo, você pode usar Olá cmdlets tooperform Olá mesmas tarefas que você pode executar por Olá [portal do Azure](https://portal.azure.com).

Neste guia, exploraremos como Olá toouse [Cmdlets de armazenamento do Azure](/powershell/module/azurerm.storage/#storage) tooperform uma variedade de tarefas de administração e desenvolvimento com o armazenamento do Azure.

Este guia pressupõe que você tenha usado anteriormente o [Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/) e o [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Guia de saudação fornece vários scripts toodemonstrate uso de saudação do PowerShell com o armazenamento do Azure. Você deve atualizar as variáveis de script hello com base na sua configuração antes de executar cada script.

a primeira seção Olá neste guia fornece uma visão geral rápida do PowerShell e de armazenamento do Azure. Para obter informações detalhadas e instruções, iniciar de saudação [pré-requisitos para usar o PowerShell do Azure com o armazenamento do Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Introdução ao Armazenamento do Azure e ao PowerShell em 5 minutos
Esta seção mostra como tooaccess armazenamento do Azure por meio do PowerShell em 5 minutos.

**Novo tooAzure:** obter uma assinatura Microsoft Azure e uma conta da Microsoft associada à assinatura. Para saber mais sobre as opções de compra do Azure, confira [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opções de compra](https://azure.microsoft.com/pricing/purchase-options/) e [Ofertas para membros](https://azure.microsoft.com/pricing/member-offers/) (para membros do MSDN, Microsoft Partner Network e BizSpark, entre outros programas da Microsoft).

Consulte [Atribuindo funções de administrador no Azure AD (Azure Active Directory)](https://msdn.microsoft.com/library/azure/hh531793.aspx) para obter mais informações sobre as assinaturas do Azure.

**Depois de criar uma assinatura e conta do Microsoft Azure:**

1. Baixe e instale o hello mais recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Iniciar Windows PowerShell script ambiente integrado (ISE): No computador local, vá toohello **iniciar** menu. Tipo **ferramentas administrativas** e clique em toorun-lo. Em Olá **ferramentas administrativas** janela, clique com botão direito **o Windows PowerShell ISE**, clique em **executar como administrador**.
3. Em **o Windows PowerShell ISE**, clique em **arquivo** > **novo** toocreate um novo arquivo de script.
4. Agora, vamos dar um script simples que mostra o básico tooaccess de comandos do PowerShell armazenamento do Azure. script Hello primeiro solicitará sua tooadd de credenciais de conta do Azure o ambiente do PowerShell do Azure conta toohello local. Em seguida, script hello definir saudação padrão assinatura do Azure e criar uma nova conta de armazenamento no Azure. Em seguida, script hello criará um novo contêiner nessa nova conta de armazenamento e carregar um contêiner de toothat de (blob) do arquivo de imagem existente. Depois que o script hello lista todos os blobs nesse contêiner, ele cria um novo diretório de destino no computador local e baixar o arquivo de imagem de saudação.
5. No hello seção de código a seguir, selecione o script hello entre Olá comentários **#begin** e **#end**. Pressione CTRL + C toocopy-toohello área de transferência.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. Em **o Windows PowerShell ISE**, pressione o script de saudação toocopy CTRL + V. Clique em **Arquivo** > **Salvar**. Em Olá **Salvar como** janela da caixa de diálogo, digite o nome de Olá Olá do arquivo de script, como "mystoragescript". Clique em **Salvar**.
7. Agora, você precisa de variáveis de script hello tooupdate com base em suas definições de configuração. Você deve atualizar Olá **$SubscriptionName** variável com sua própria assinatura. Você pode manter Olá outras variáveis como especificado no script hello ou atualizá-los como quiser.
   
   * **$SubscriptionName:** você deve atualizar essa variável com o nome de sua própria assinatura. Execute uma saudação após três maneiras toolocate Olá nome da sua assinatura:
     
    a. Em **o Windows PowerShell ISE**, clique em **arquivo** > **novo** toocreate um novo arquivo de script. A seguir Olá cópia toohello novo arquivo de script do script e clique em **depurar** > **executar**. Olá script a seguir será seu tooadd de credenciais de conta do Azure primeiro solicitar uma conta do Azure toohello PowerShell ambiente local e, em seguida, Mostrar todas as assinaturas de saudação que são conectados toohello sessão local do PowerShell. Anote uma saudação nome de assinatura de saudação que você deseja toouse ao seguir este tutorial:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. toolocate e copiar nome de sua assinatura no hello [portal do Azure](https://portal.azure.com), no hello menu Hub saudação à esquerda, clique em **assinaturas**. Copie o nome de saudação de assinatura que você deseja toouse durante a execução de scripts de saudação neste guia.
     
     ![Portal do Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. toolocate e copiar nome de sua assinatura no hello [Portal clássico do Azure](https://manage.windowsazure.com/), role para baixo e clique em **configurações** em Olá esquerda do portal de saudação. Clique em **assinaturas** toosee uma lista de suas assinaturas. Nome de saudação de cópia de assinatura que você deseja toouse durante a execução de scripts de saudação fornecidos neste guia.
     
     ![Portal clássico do Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** usar Olá considerando o nome do script hello ou digitar um novo nome para sua conta de armazenamento. **Importante:** nome Olá Olá da conta de armazenamento deve ser exclusivo no Azure. Ele também deve ter somente letras minúsculas!
   * **$Location:** usar Olá fornecido "US West" no script hello ou escolher outros locais do Azure, como Leste dos EUA, Norte da Europa e assim por diante.
   * **$ContainerName:** use Olá considerando o nome do script hello ou digite um novo nome para seu contêiner.
   * **$ImageToUpload:** inserir uma imagem de tooa caminho no computador local, como: "C:\Images\HelloWorld.png".
   * **$DestinationFolder:** Enter um arquivos de toostore de diretório local do caminho tooa baixado do armazenamento do Azure, como: "C:\DownloadImages".
8. Depois de atualizar as variáveis de script hello no arquivo de "mystoragescript.ps1" Olá, clique em **arquivo** > **salvar**. Em seguida, clique em **depurar** > **executar** ou pressione **F5** toorun script de saudação.  

Após a execução do script hello, você deve ter uma pasta de destino que inclui o arquivo de imagem Olá baixado. Olá captura de tela a seguir mostra um exemplo de saída:

![Baixar blobs](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Hello "Introdução ao armazenamento do Azure e do PowerShell em 5 minutos" forneceu uma rápida introdução sobre como toouse PowerShell do Azure com o armazenamento do Azure. Para obter informações detalhadas e instruções, recomendamos que você Olá tooread seções a seguir.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Pré-requisitos para usar o Azure PowerShell com o armazenamento do Azure
Você precisa de uma conta e assinatura toorun Olá cmdlets do Azure PowerShell fornecido neste guia, conforme descrito acima.

PowerShell do Azure é um módulo que fornece toomanage de cmdlets do Azure por meio do Windows PowerShell. Para obter informações sobre como instalar e configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). É recomendável baixar e instalar ou atualizar o módulo PowerShell do Azure mais recente de toohello antes de usar este guia.

Você pode executar cmdlets Olá Olá padrão do Windows PowerShell no console de ou Olá Windows PowerShell Integrated Scripting ISE (ambiente). Por exemplo, tooopen **o Windows PowerShell ISE**, vá toohello menu de início, digite ferramentas administrativas e clique em toorun-lo. Na janela de ferramentas administrativas hello, clique o ISE do Windows PowerShell, clique em Executar como administrador.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Como o armazenamento toomanage contas no Azure

Vejamos agora o gerenciamento de contas de armazenamento no Azure com o PowerShell

### <a name="how-tooset-a-default-azure-subscription"></a>Como tooset um padrão de assinatura do Azure
toomanage o armazenamento do Azure usando o PowerShell do Azure, você precisa tooauthenticate seu ambiente do cliente com o Azure por meio de autenticação do Azure Active Directory ou a autenticação baseada em certificado. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tutorial. Este guia usa a autenticação do Active Directory do Azure hello.

1. No ISE do Windows PowerShell, digite Olá tooadd de comando a seguir o ambiente do PowerShell do Azure conta toohello local:

    ```powershell
    Add-AzureAccount
    ```

2. Na janela de "Entrar tooMicrosoft Azure" Olá, digite Olá o endereço de email e senha associada à sua conta. Azure autentica e salva informações de credencial hello e, em seguida, fecha a janela de saudação.

3. Em seguida, execute Olá Olá tooview de comando Azure contas no ambiente do PowerShell local e verifique se sua conta está listada a seguir:
   
    ```powershell
    Get-AzureAccount
    ```
4. Em seguida, execute Olá tooview cmdlet a seguir todas as assinaturas de saudação que são conectados toohello sessão local do PowerShell e verificar se sua assinatura está listada:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset um padrão de assinatura do Azure, execute o cmdlet Select-AzureSubscription de saudação:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Verifique o nome de saudação de assinatura de padrão de saudação executando o cmdlet Get-AzureSubscription de saudação:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee todos os Olá cmdlets do PowerShell disponíveis para o armazenamento do Azure, execute:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>Como toocreate uma nova conta de armazenamento do Azure
toouse armazenamento do Azure, você precisará de uma conta de armazenamento. Depois de configurar sua assinatura do computador tooconnect tooyour, você pode criar uma nova conta de armazenamento do Azure.

1. Execute Olá Get-AzureLocation cmdlet toofind todos os locais de datacenters disponíveis hello:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Em seguida, execute uma nova conta de armazenamento toocreate de cmdlet New-AzureStorageAccount hello. Olá exemplo a seguir cria uma nova conta de armazenamento no data center de "US West" hello.
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> nome de saudação da sua conta de armazenamento deve ser exclusivo dentro do Azure e deve estar em minúscula. Para ver as convenções e restrições de nomenclatura, confira [Sobre as contas de armazenamento do Azure](storage-create-storage-account.md) e [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx) (Nomeando e referenciando contêineres, blobs e metadados).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>Como tooset uma conta de armazenamento do Azure padrão
Você pode ter várias contas de armazenamento na sua assinatura. Você pode escolher um deles e defini-lo como a conta de armazenamento saudação padrão para todos os Olá armazenamento comandos no hello mesma sessão do PowerShell. Isso permite que você comandos de armazenamento toorun saudação do Azure PowerShell sem especificar explicitamente o contexto de armazenamento hello.

1. tooset uma conta de armazenamento padrão para a sua assinatura, você pode executar o cmdlet de Set-AzureSubscription hello.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Em seguida, execute Olá Get-AzureSubscription cmdlet tooverify que a conta de armazenamento de saudação é associada à sua conta de assinatura padrão. Esse comando retorna propriedades de assinatura de saudação na assinatura atual do hello incluindo sua conta de armazenamento atual.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Como toolist todo o armazenamento do Azure contas em uma assinatura
Cada assinatura do Azure pode ter até too100 contas de armazenamento. Para obter informações mais atualizadas sobre os limites de hello, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md).

Execute Olá cmdlet toofind nome hello e status Olá de contas de armazenamento na assinatura atual Olá a seguir:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>Como toocreate um contexto de armazenamento do Azure
Contexto de armazenamento do Azure é um objeto de credenciais de armazenamento do PowerShell tooencapsulate hello. Usando um contexto de armazenamento durante a execução de qualquer cmdlet subsequente permite que você tooauthenticate sua solicitação sem especificar a conta de armazenamento hello e sua chave de acesso explicitamente. Você pode criar um contexto de armazenamento de várias maneiras, como usando a chave de acesso e do nome da conta de armazenamento, o token de SAS (assinatura de acesso compartilhado), cadeia de conexão ou anonimamente. Para obter mais informações, consulte [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Use um contexto de armazenamento uma saudação toocreate de três maneiras a seguir:

* Executar Olá [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind cmdlet chave de acesso de armazenamento primário Olá para sua conta de armazenamento do Azure. Em seguida, chame Olá [AzureStorageContext novo](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate um contexto de armazenamento:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Gerar um token de assinatura de acesso compartilhado para um contêiner de armazenamento do Azure e usá-lo toocreate um contexto de armazenamento:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Para saber mais, veja [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) e [Uso de SAS (Assinaturas de Acesso Compartilhado)](storage-dotnet-shared-access-signature-part-1.md).

* Em alguns casos, convém pontos de extremidade do serviço toospecify hello quando você cria um novo contexto de armazenamento. Isso pode ser necessário quando você registrou um nome de domínio personalizado para sua conta de armazenamento com o serviço Blob hello ou desejar toouse uma assinatura de acesso compartilhado para acessar recursos de armazenamento. Definir pontos de extremidade de serviço de saudação em uma cadeia de conexão e usá-lo toocreate um novo contexto de armazenamento conforme mostrado abaixo:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Para obter mais informações sobre como tooconfigure uma cadeia de caracteres de conexão de armazenamento, consulte [Configurando cadeias de caracteres de Conexão](storage-configure-connection-string.md).

Agora que você tiver configurado seu computador e aprendeu como toomanage assinaturas e contas de armazenamento usando o PowerShell do Azure, vá toohello próxima seção toolearn como toomanage Azure blobs e instantâneos de blob.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>Como tooretrieve e regenerar chaves de armazenamento do Azure
Uma conta de armazenamento do Azure é fornecida com duas chaves de conta. Você pode usar o hello tooretrieve cmdlet a seguir suas chaves.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Use Olá cmdlet tooretrieve uma chave específica a seguir. Os valores válidos são Primary e Secondary.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Se você quiser tooregenerate suas chaves, use Olá cmdlet a seguir. Os valores válidos para -KeyType são "Primary" e "Secundary"

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Como os blobs de toomanage do Azure
Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS. Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de armazenamento de BLOBs do Azure hello. Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs usando o .NET](storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Conceitos do serviço Blob).

### <a name="how-toocreate-a-container"></a>Como um contêiner de toocreate
Todos os blobs no armazenamento do Azure devem residir em um contêiner. Você pode criar um contêiner privado, usando o cmdlet New-AzureStorageContainer de saudação:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Há três níveis de acesso de leitura anônimo: **Desativado**, **Blob** e **Contêiner**. tooprevent anônimo acessar tooblobs, Olá permissão parâmetro muito**Off**. Por padrão, o novo contêiner de saudação é particular e pode ser acessado somente pelo proprietário da conta hello. público anônimo tooallow leitura tooblob acessar os recursos, mas não toocontainer metadados ou toohello a lista de blobs no contêiner Olá, defina o parâmetro de permissão de saudação muito**Blob**. público completo tooallow leitura tooblob acessar os recursos, os metadados de contêiner e lista de saudação de blobs no contêiner de saudação, defina o parâmetro de permissão de saudação muito**contêiner**. Para obter mais informações, consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>Como tooupload um blob em um contêiner
O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas. Para obter mais informações, confira [Compreendendo Blobs de blocos, Blobs de apêndice e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).

blobs tooupload tooa contêiner, você pode usar o hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet. Por padrão, esse comando carrega o blob de blocos de tooa Olá arquivos locais. tipo de saudação toospecify blob hello, você pode usar o parâmetro de - BlobType de saudação.

exemplo Hello executa Olá [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget cmdlet Olá todos os arquivos na pasta especificada hello e passa-los toohello próximo cmdlet usando o operador de pipeline hello. Olá [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet carrega o contêiner de tooyour Olá arquivos locais:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Como toodownload blobs de um contêiner
saudação de exemplo a seguir demonstra como toodownload blobs de um contêiner. exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso primário. Em seguida, o exemplo hello recupera uma referência de blob usando Olá [AzureStorageBlob Get](/powershell/module/azure.storage/get-azurestorageblob) cmdlet. Em seguida, o exemplo hello usa Olá [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobs do cmdlet toodownload na pasta de destino local hello.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Como toocopy blobs de um tooanother de contêiner de armazenamento
Você pode copiar blobs em regiões e contas de armazenamento de forma assíncrona. Olá exemplo a seguir demonstra como toocopy blobs de armazenamento de um contêiner tooanother em duas contas de armazenamento diferente. exemplo Hello primeiro define variáveis para contas de armazenamento de origem e de destino e, em seguida, cria um contexto de armazenamento para cada conta. Em seguida, o exemplo hello copia blobs do contêiner Olá fonte contêiner toohello destino usando Olá [AzureStorageBlobCopy início](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet. exemplo Hello pressupõe que contêineres e contas de armazenamento de origem e destino Olá já existem.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Observe que este exemplo executa uma cópia assíncrona. Você pode monitorar o status de saudação de cada cópia executando Olá [AzureStorageBlobCopyState Get](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>Como toocopy blobs de um local secundário
Você pode copiar blobs do local secundário de saudação de uma conta ativada por RA-GRS.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>Como toodelete um blob
toodelete um blob, primeiro obter uma referência de blob e, em seguida, chamar hello remover AzureStorageBlob cmdlet. saudação de exemplo a seguir exclui todos os blobs de saudação em um contêiner específico. exemplo Hello primeiro define variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento. Em seguida, o exemplo hello recupera uma referência de blob usando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá cmdlet e executa [AzureStorageBlob remover](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs de um contêiner no armazenamento do Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Como instantâneos de blob toomanage do Azure
O Azure permite criar um instantâneo de um blob. Um instantâneo é uma versão somente leitura de um blob capturada em um momento no tempo. Quando um instantâneo tiver sido criado, ele pode ser lido, copiado ou excluído, mas não modificado. Os instantâneos fornecem uma tooback de forma a um blob conforme ele aparece em um momento específico. Para obter mais informações, consulte [Criar um instantâneo de um blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>Como toocreate um instantâneo de blob
toocreate um instantâneo de um blob, primeiro obter uma referência de blob e, em seguida, chamar hello `ICloudBlob.CreateSnapshot` método nele. Olá exemplo a seguir define primeiramente variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento. Em seguida, o exemplo hello recupera uma referência de blob usando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá cmdlet e executa [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate um instantâneo.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>Como os instantâneos de toolist um blob
Você pode criar tantos snapshots quanto desejar para um blob. Você pode listar instantâneos Olá associados com o blob tootrack seus instantâneos atuais. Olá, exemplo a seguir usa uma saudação predefinida de blob e chama [AzureStorageBlob Get](/powershell/module/azure.storage/get-azurestorageblob) instantâneos de saudação do cmdlet toolist desse blob.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>Como toocopy um instantâneo de um blob
Você pode copiar um instantâneo de um instantâneo do blob toorestore hello. Para obter informações detalhadas e restrições, consulte [Criar um instantâneo de um Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx). Olá exemplo a seguir define primeiramente variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento. Em seguida, o exemplo hello define variáveis de nome de contêiner e blob hello. exemplo Hello recupera uma referência de blob usando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá cmdlet e executa [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate um instantâneo. Em seguida, o exemplo hello executa Olá [AzureStorageBlobCopy início](/powershell/module/azure.storage/start-azurestorageblobcopy) instantâneo de saudação do cmdlet toocopy de um blob usando o objeto de ICloudBlob Olá para o blob de origem hello. Se tooupdate variáveis de saudação basear-se em sua configuração de exemplo de hello em execução. Observe que Olá no exemplo a seguir supõe que Olá contêineres de origem e de destino e o blob de origem Olá já existe.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Agora que você aprendeu como toomanage Azure blobs e instantâneos com o Azure PowerShell de blob, vá toohello próxima seção toolearn como toomanage tabelas, filas e arquivos.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Como toomanage Azure tabelas e entidades de tabela
Serviço de armazenamento de tabela do Azure é um repositório de dados NoSQL, que você pode usar conjuntos de enorme toostore e consulta de dados estruturados e não relacionais. Olá principais componentes do serviço de saudação são tabelas, entidades e propriedades. Uma tabela é uma coleção de entidades. Uma entidade é um conjunto de propriedades. Cada entidade pode ter propriedades too252, que são todos os pares nome-valor. Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de armazenamento de tabela do Azure hello. Para obter informações detalhadas, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx) e [Introdução ao armazenamento de tabela do Azure usando o .NET](storage-dotnet-how-to-use-tables.md).

Olá subseções a seguir, você aprenderá como toomanage armazenamento de tabela do Azure do serviço usando o PowerShell do Azure. Olá cenários abordados incluem **criando**, **excluindo**, e **recuperar** **tabelas**, bem como **adicionando**, **consultando**, e **excluir entidades de tabela**.

### <a name="how-toocreate-a-table"></a>Como toocreate uma tabela
Cada tabela deve residir em uma conta de armazenamento do Azure. Olá exemplo a seguir demonstra como toocreate uma tabela no armazenamento do Azure. exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso. Em seguida, ele usa Olá [AzureStorageTable novo](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate uma tabela no armazenamento do Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>Como tooretrieve uma tabela
Você pode consultar e recuperar uma ou todas as tabelas em uma conta de armazenamento. Olá exemplo a seguir demonstra como tooretrieve usando uma determinada tabela Olá [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Se você chamar hello Get-AzureStorageTable cmdlet sem parâmetros, ele obtém todas as tabelas de armazenamento para uma conta de armazenamento.

### <a name="how-toodelete-a-table"></a>Como toodelete uma tabela
Você pode excluir uma tabela de uma conta de armazenamento usando Olá [AzureStorageTable remover](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Como toomanage tabela entidades
No momento, do PowerShell do Azure não fornece cmdlets toomanage de entidades de tabela diretamente. tooperform operações em entidades de tabela, você pode usar classes de saudação fornecidos em Olá [biblioteca de cliente de armazenamento do Azure para .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Como tooadd tabela entidades
tooadd uma tabela de tooa de entidade, primeiro crie um objeto que define as propriedades de entidade. Uma entidade pode ter até too255 propriedades, incluindo 3 Propriedades do sistema: **PartitionKey**, **RowKey**, e **Timestamp**. Você é responsável por inserir e atualizar valores de saudação do **PartitionKey** e **RowKey**. servidor Hello gerencia valor Olá **Timestamp**, que não pode ser modificado. Olá junto **PartitionKey** e **RowKey** identificam exclusivamente cada entidade dentro de uma tabela.

* **PartitionKey**: determina partição Olá Olá entidade será armazenada no.
* **RowKey**: identifica exclusivamente a entidade Olá na partição de saudação.

Você pode definir as propriedades personalizadas de too252 para uma entidade. Para obter mais informações, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Olá exemplo a seguir demonstra como tabela de tooa tooadd entidades. exemplo Hello mostra como tooretrieve Olá tabela employee e adicionar várias entidades para ele. Primeiro, ele estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso. Em seguida, ele recupera Olá tabela usando Olá [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Se não existir tabela hello, Olá [AzureStorageTable novo](/powershell/module/azure.storage/new-azurestoragetable) cmdlet é usado toocreate uma tabela no armazenamento do Azure. Em seguida, o exemplo hello define uma função personalizada toohello tabela a adicionar entidade tooadd entidades especificando a partição de cada entidade e a chave de linha. saudação de chamadas de função Hello Adicionar entidade [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet Olá [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate classe um objeto de entidade. Posteriormente, o exemplo hello chama Olá [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) método essa tooadd de objeto de entidade-tooa tabela.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Como tooquery tabela entidades
tooquery uma tabela, use Olá [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) classe. Olá exemplo a seguir supõe que você já tiver executado o script hello fornecido em hello como tooadd seção entidades deste guia. exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso. Em seguida, ele tenta tooretrieve tabela de "Funcionários" hello criado anteriormente usando Olá [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Olá chamada [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet Olá Microsoft.WindowsAzure.Storage.Table.TableQuery classe cria um novo objeto de consulta. exemplo Hello procura entidades Olá que têm uma coluna de 'ID' cujo valor é 1, conforme especificado em um filtro de cadeia de caracteres. Para obter informações detalhadas, consulte [Consultando tabelas e entidades](http://msdn.microsoft.com/library/azure/dd894031.aspx). Quando você executa essa consulta, ele retorna todas as entidades que correspondem aos critérios de filtro de saudação.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Como toodelete tabela entidades
Você pode excluir uma entidade usando suas chaves de partição e de linha. Olá exemplo a seguir supõe que você já tiver executado o script hello fornecido em hello como tooadd seção entidades deste guia. exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso. Em seguida, ele tenta tooretrieve tabela de "Funcionários" hello criado anteriormente usando Olá [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Se Olá tabela existir, o exemplo hello chama Olá [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve método uma entidade com base em seus valores de chave de partição e de linha. Em seguida, passe Olá entidade toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete de método.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Como toomanage Azure as filas e mensagens da fila
Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS. Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de armazenamento de fila do Azure hello. Para obter informações detalhadas, confira [Introdução ao Armazenamento de Filas do Azure usando o .NET](storage-dotnet-how-to-use-queues.md).

Esta seção mostrará como toomanage armazenamento de fila do Azure do serviço usando o PowerShell do Azure. Olá cenários abordados incluem **inserindo** e **excluindo** Enfileirar mensagens, bem como **criando**, **excluindo**e **recuperar filas**.

### <a name="how-toocreate-a-queue"></a>Como toocreate uma fila
Olá exemplo a seguir primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso. Em seguida, ele chama [AzureStorageQueue novo](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate uma fila denominada 'queuename'.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Para obter informações sobre convenções de nomenclatura do serviço Fila do Azure, consulte [Nomear filas e metadados](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>Como tooretrieve uma fila
Você pode consultar e recuperar uma lista de todas as filas de saudação em uma conta de armazenamento ou de uma fila específica. Olá exemplo a seguir demonstra como tooretrieve uma fila especificada usando Olá [AzureStorageQueue Get](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Se você chamar hello [AzureStorageQueue Get](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet sem parâmetros, ele obtém uma lista de todas as filas de saudação.

### <a name="how-toodelete-a-queue"></a>Como toodelete uma fila
toodelete uma fila e todas as mensagens de saudação contidos nele, chamada hello remover AzureStorageQueue cmdlet. saudação de exemplo a seguir mostra como toodelete uma fila especificada usando Olá cmdlet Remove-AzureStorageQueue.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>Como tooinsert uma mensagem em uma fila
tooinsert uma mensagem em uma fila existente, primeiro crie uma nova instância da saudação [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe. Em seguida, chame Olá [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método. Um CloudQueueMessage pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.

saudação de exemplo a seguir demonstra como tooadd tooa fila de mensagens. exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso. Em seguida, ele recupera fila especificada de saudação usando Olá [AzureStorageQueue Get](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet. Se a fila Olá existir, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet é usado toocreate uma instância do hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe. Posteriormente, o exemplo hello chama Olá [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método essa tooadd de objeto de mensagem-fila tooa. Aqui está o código que recupera uma fila e insere a mensagem de saudação 'MessageInfo':

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Como toode-fila em Olá próxima mensagem
Seu código remove uma mensagem de um fila em duas etapas. Quando você chama Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) método, você obter próxima mensagem de saudação em uma fila. Uma mensagem retornada de **GetMessage** se torna invisível tooany outro código de leitura de mensagens dessa fila. toofinish mensagem de saudação remover da fila hello, você também deve chamar hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) método. Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente. Seu código chama **DeleteMessage** logo depois que a mensagem de saudação foi processada.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>Como toomanage arquivo Azure compartilhamentos e arquivos
Armazenamento de arquivo do Azure oferece armazenamento compartilhado para aplicativos que usam protocolo SMB padrão de saudação. Serviços de nuvem e máquinas virtuais do Microsoft Azure podem compartilhar dados de arquivo entre componentes de aplicativos por meio de compartilhamentos montados e aplicativos locais podem acessar dados de arquivo em um compartilhamento via API de armazenamento do arquivo hello ou o Azure PowerShell.

Para obter mais informações sobre o armazenamento de Arquivos do Azure, confira [Introdução ao Armazenamento de Arquivos do Azure no Windows](storage-dotnet-how-to-use-files.md) e [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx) (API REST do serviço Arquivo).

## <a name="how-tooset-and-query-storage-analytics"></a>Como tooset e consulta de análise de armazenamento
Você pode usar [Azure Storage Analytics](storage-analytics.md) toocollect métricas para suas contas de armazenamento do Azure e dados de log sobre solicitações enviadas tooyour conta de armazenamento. Você pode usar a integridade do armazenamento métricas toomonitor saudação de uma conta de armazenamento e armazenamento toodiagnose de registro em log e solucionar problemas com sua conta de armazenamento. Você pode configurar o monitoramento usando Olá portal do Azure ou o Windows PowerShell ou programaticamente usando a biblioteca de cliente de armazenamento hello. O log de armazenamento ocorre no lado do servidor e permite que você toorecord detalhes de solicitações bem-sucedidas e com falhas na conta de armazenamento. Esses logs o habilitam toosee detalhes de leitura, gravação e operações de exclusão em relação a tabelas, filas e blobs bem como motivos Olá para solicitações com falha.

toolearn como tooenable e exibir dados de métricas de armazenamento usando o PowerShell, consulte [como tooenable as métricas de armazenamento usando o PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

toolearn como tooenable e recuperar o log de armazenamento de dados usando o PowerShell, consulte [como tooenable armazenamento de log usando o PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) e [localizar os dados de log do log de armazenamento](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Para obter informações detalhadas sobre o uso de métricas de armazenamento e tootroubleshoot problemas de armazenamento de log de armazenamento, consulte [monitorando, diagnosticando e Solucionando problemas de armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Como toomanage compartilhado (SAS) de assinatura de acesso e política de acesso armazenada
Assinaturas de acesso compartilhado são uma parte importante do modelo de segurança Olá para qualquer aplicativo usando o armazenamento do Azure. Eles são úteis para fornecer permissões limitadas tooyour armazenamento conta tooclients que não deve ter a chave da conta hello. Por padrão, somente o proprietário de Olá da conta de armazenamento Olá pode acessar blobs, tabelas e filas nessa conta. Se seu aplicativo ou serviço precisa toomake esses clientes tooother disponíveis de recursos sem compartilhar sua chave de acesso, você terá três opções:

* Defina o contêiner de toohello do contêiner permissões toopermit acesso de leitura anônimo e seus blobs. Isso não é permitido para tabelas ou filas.
* Use uma assinatura de acesso compartilhado que concede toocontainers de direitos de acesso restrito, blobs, filas e tabelas para um intervalo de tempo específico.
* Use uma política de acesso armazenada tooobtain um nível adicional de controle sobre assinaturas de acesso compartilhado para um contêiner ou seus blobs, para uma fila ou de uma tabela. Olá política de acesso armazenado permite que você toochange a hora de início hello, tempo de expiração ou permissões para uma assinatura, ou toorevoke-lo depois que ele tiver sido emitida.

Uma assinatura de acesso compartilhado pode estar em uma das duas formas:

* **SAS ad-hoc**: quando você cria um SAS ad hoc, a hora de início de saudação, o tempo de expiração e permissões para Olá SAS são especificadas em Olá URI SAS. Esse tipo de SAS pode ser criado em um contêiner, blob, tabela ou fila e não pode ser revogado.
* **SAS com a política de acesso armazenada**: uma política de acesso armazenada é definida em um contêiner de recursos um contêiner de blob, tabela ou fila - e você pode usá-lo toomanage restrições para uma ou mais assinaturas de acesso compartilhado. Quando você associa uma SAS com uma política de acesso armazenada, Olá SAS herda restrições Olá - Olá hora de início, hora de expiração e permissões - definidas para a política de acesso Olá armazenado. Esse tipo de SAS pode ser revogado.

Para obter mais informações, consulte [usando assinaturas (SAS de acesso compartilhado)](storage-dotnet-shared-access-signature-part-1.md) e [gerenciar o acesso de leitura anônimo toocontainers e blobs](storage-manage-access-to-resources.md).

Seções a seguir hello, você aprenderá como toocreate uma política de acesso armazenado e token de assinatura de acesso compartilhado para tabelas do Azure. O PowerShell do Azure fornece cmdlets semelhantes para contêineres, blobs e filas. scripts de saudação toorun nesta seção, faça o download Olá [Azure PowerShell versão 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) ou posterior.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>Como toocreate uma política com base em token de assinatura de acesso compartilhado
Use Olá AzureStorageTableStoredAccessPolicy novo cmdlet toocreate uma nova política de acesso armazenada. Em seguida, chame Olá [AzureStorageTableSASToken novo](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate um novo token de assinatura com base na política de acesso compartilhado para uma tabela de armazenamento do Azure.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Como toocreate um token de assinatura de acesso compartilhado (não revogável) ad hoc
Saudação de uso [AzureStorageTableSASToken novo](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate um novo ad hoc (não revogável) token SAS para uma tabela de armazenamento do Azure:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>Como toocreate uma política de acesso armazenada
Use Olá AzureStorageTableStoredAccessPolicy novo cmdlet toocreate uma nova política de acesso armazenadas para uma tabela de armazenamento do Azure:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>Como tooupdate uma política de acesso armazenada
Use Olá conjunto AzureStorageTableStoredAccessPolicy cmdlet tooupdate uma política de acesso armazenada existente para uma tabela de armazenamento do Azure:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>Como toodelete uma política de acesso armazenada
Use toodelete de cmdlet Olá AzureStorageTableStoredAccessPolicy remover uma política de acesso armazenada em uma tabela de armazenamento do Azure:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Como toouse o armazenamento do Azure para governo dos Estados Unidos e do Azure na China
Um ambiente do Azure é uma implantação independente do Microsoft Azure, como [Governo do Azure para o governo dos EUA](https://azure.microsoft.com/features/gov/), [AzureCloud para Azure global](https://portal.azure.com) e [AzureChinaCloud para o Azure operado pela 21Vianet](http://www.windowsazure.cn/) na China. Você pode implantar novos ambientes do Azure para o governo dos EUA e Azure China.

toouse armazenamento do Azure com AzureChinaCloud, é necessário toocreate um contexto de armazenamento que está associado a AzureChinaCloud. Siga essas tooget etapas é iniciado:

1. Executar Olá [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet Olá ambientes do Azure disponíveis:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Adicione uma conta do Azure na China tooWindows PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Crie um contexto de armazenamento para uma conta de AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse armazenamento do Azure com [dos EUA dos EUA](https://azure.microsoft.com/features/gov/), você deve definir um novo ambiente e, em seguida, criar um novo contexto de armazenamento com esse ambiente:

1. Executar Olá [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet Olá ambientes do Azure disponíveis:

    ```powershell
    Get-AzureEnvironment
    ```

2. Adicione uma conta de Azure US Government tooWindows PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Crie um contexto de armazenamento para uma conta do AzureUSGovernment:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Para obter mais informações, consulte:

* [Guia do Desenvolvedor do Microsoft Azure Government](../azure-government-developer-guide.md).
* [Visão geral das diferenças ao criar um aplicativo no serviço na China](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Próximas etapas
Neste guia, você aprendeu como toomanage armazenamento do Azure com o Azure PowerShell. Estes são alguns artigos e recursos relacionados para saber mais sobre eles.

* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Cmdlets do PowerShell do Armazenamento do Azure](/powershell/module/azurerm.storage/#storage)
* [Referência do Windows PowerShell](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
