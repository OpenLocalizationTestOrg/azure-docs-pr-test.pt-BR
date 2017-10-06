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
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="26b0e-103">Configurar o Cofre de Chaves do Azure com a rotação de chaves e auditoria de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="26b0e-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="26b0e-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="26b0e-104">Introduction</span></span>
<span data-ttu-id="26b0e-105">Depois de criar seu Cofre de chaves, você será capaz de toostart usando esse cofre toostore suas chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="26b0e-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="26b0e-106">Os aplicativos desnecessários toopersist suas chaves ou segredos, mas em vez disso, irá solicitá-las do Cofre de chaves Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="26b0e-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="26b0e-107">Isso permite que você tooupdate chaves e segredos sem afetar o comportamento de saudação do seu aplicativo, que abre a uma gama de possibilidades em torno de sua chave e o gerenciamento de informações secretas.</span><span class="sxs-lookup"><span data-stu-id="26b0e-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="26b0e-108">Este artigo o orienta por meio de um exemplo de como usar o Azure Key Vault toostore um segredo, neste caso, uma chave de conta de armazenamento do Azure que é acessada por um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="26b0e-109">Ele também demonstra a implementação de uma rotação agendada dessa chave de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="26b0e-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="26b0e-110">Finalmente, ele apresenta uma demonstração de como toomonitor Olá logs de auditoria do Cofre de chaves e gerar alertas quando são feitas solicitações inesperadas.</span><span class="sxs-lookup"><span data-stu-id="26b0e-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="26b0e-111">Este tutorial não está tooexplain pretendido em detalhe Olá a configuração inicial do seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="26b0e-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="26b0e-112">Para obter essas informações, confira [Introdução ao Cofre da Chave do Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="26b0e-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="26b0e-113">Para obter instruções sobre a Interface de Linha de Comando de Plataforma Cruzada, confira [Gerenciar Cofre de Chaves usando a CLI](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="26b0e-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="26b0e-114">Configurar o Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="26b0e-114">Set up Key Vault</span></span>
<span data-ttu-id="26b0e-115">tooenable tooretrieve um aplicativo um segredo do Cofre de chaves, você deve primeiro criar segredo hello e carregá-lo tooyour cofre.</span><span class="sxs-lookup"><span data-stu-id="26b0e-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="26b0e-116">Isso pode ser feito iniciando uma sessão do PowerShell do Azure e entrar tooyour conta do Azure com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="26b0e-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="26b0e-117">Na janela de pop-up do navegador hello, insira seu nome de usuário da conta do Azure e a senha.</span><span class="sxs-lookup"><span data-stu-id="26b0e-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="26b0e-118">PowerShell obterá todas as assinaturas de saudação que estão associadas essa conta.</span><span class="sxs-lookup"><span data-stu-id="26b0e-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="26b0e-119">PowerShell usa Olá um primeiro por padrão.</span><span class="sxs-lookup"><span data-stu-id="26b0e-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="26b0e-120">Se você tiver várias assinaturas, você pode ter toospecify Olá que foi usado toocreate seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="26b0e-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="26b0e-121">Digite hello assinaturas de saudação toosee para sua conta a seguir:</span><span class="sxs-lookup"><span data-stu-id="26b0e-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="26b0e-122">assinatura de saudação toospecify associada com o Cofre de chaves Olá que fizerem logon, digite:</span><span class="sxs-lookup"><span data-stu-id="26b0e-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="26b0e-123">Como este artigo demonstra como armazenar uma chave de conta de armazenamento como um segredo, você deve obter essa chave de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="26b0e-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="26b0e-124">Depois de recuperar o segredo (nesse caso, sua chave de conta de armazenamento), você deve converter a cadeia de caracteres segura que tooa e, em seguida, criar um segredo com esse valor em seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="26b0e-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="26b0e-125">Em seguida, obter Olá URI segredo Olá criado por você.</span><span class="sxs-lookup"><span data-stu-id="26b0e-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="26b0e-126">Isso é usado em uma etapa posterior ao chamar hello Cofre de chaves tooretrieve seu segredo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="26b0e-127">Execute Olá comando PowerShell a seguir e anote o valor de ID de hello, que é o segredo Olá URI:</span><span class="sxs-lookup"><span data-stu-id="26b0e-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="26b0e-128">Configurar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="26b0e-128">Set up hello application</span></span>
<span data-ttu-id="26b0e-129">Agora que você tem um segredo armazenado, você pode usar código tooretrieve e usá-lo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="26b0e-130">Há algumas etapas e necessário tooachieve isso.</span><span class="sxs-lookup"><span data-stu-id="26b0e-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="26b0e-131">Hello primeiro e mais importante etapa é registrar seu aplicativo no Azure Active Directory e, em seguida, informando o Cofre de chaves suas informações de aplicativo para que ele pode permitir que solicitações de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="26b0e-132">Seu aplicativo deve ser criado em Olá mesmo locatário do Active Directory do Azure como seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="26b0e-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="26b0e-133">Abra a guia de aplicativos de saudação do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-133">Open hello applications tab of Azure Active Directory.</span></span>

![Abrir os aplicativos no Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="26b0e-135">Escolha **adicionar** tooadd tooyour um aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="26b0e-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![Escolha ADICIONAR](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="26b0e-137">Deixe o tipo de aplicativo hello como **aplicativo de WEB e/ou API WEB** e dê um nome de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Aplicativo hello nome](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="26b0e-139">Dê ao aplicativo uma **URL de logon** e um **URI de ID de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="26b0e-140">Eles podem ser qualquer coisa que você desejar para esta demonstração e podem ser alterados posteriormente, se necessário.</span><span class="sxs-lookup"><span data-stu-id="26b0e-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Fornecer os URIs necessários](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="26b0e-142">Depois que o aplicativo hello é adicionado tooAzure do Active Directory, você será levado à página de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="26b0e-143">Clique em Olá **configurar** guia e, em seguida, localize e copie Olá **ID do cliente** valor.</span><span class="sxs-lookup"><span data-stu-id="26b0e-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="26b0e-144">Anote a ID do cliente Olá para etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="26b0e-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="26b0e-145">Em seguida, gere uma chave para o aplicativo para que ele possa interagir com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="26b0e-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="26b0e-146">Você pode criá-lo em Olá **chaves** seção Olá **configuração** guia. Anote chave Olá recentemente gerado do seu aplicativo do Active Directory do Azure para uso em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="26b0e-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Chaves de aplicativo do Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="26b0e-148">Antes de estabelecer as chamadas do seu aplicativo em um cofre de chaves hello, você deve informar o Cofre de chaves Olá sobre seu aplicativo e suas permissões.</span><span class="sxs-lookup"><span data-stu-id="26b0e-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="26b0e-149">Olá comando a seguir obtém nome do cofre hello e ID do cliente de saudação do seu aplicativo do Active Directory do Azure e concede **obter** cofre da chave tooyour acesso para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="26b0e-150">Neste ponto, você está pronto toostart compilar seu aplicativo chama.</span><span class="sxs-lookup"><span data-stu-id="26b0e-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="26b0e-151">Em seu aplicativo, você deve instalar Olá NuGet pacotes necessário toointeract com o Cofre de chaves do Azure e o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="26b0e-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="26b0e-152">No console do Gerenciador de pacote do Visual Studio hello, digite Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="26b0e-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="26b0e-153">Na gravação da saudação deste artigo, a versão atual de saudação do pacote do Azure Active Directory Olá é 3.10.305231913, para que você pode ser a versão mais recente do tooconfirm hello e atualizar adequadamente.</span><span class="sxs-lookup"><span data-stu-id="26b0e-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="26b0e-154">No código do aplicativo, crie um método de saudação do toohold de classe para a autenticação do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="26b0e-155">Neste exemplo a classe é chamada **Utils**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="26b0e-156">Adicione o seguinte Olá usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="26b0e-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="26b0e-157">Em seguida, adicione Olá após o token JWT do método tooretrieve Olá do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="26b0e-158">Para fins de manutenção, convém toomove valores de cadeia de caracteres codificada de saudação em sua configuração de web ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

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

<span data-ttu-id="26b0e-159">Adicionar Olá código necessário toocall Cofre de chaves e recuperar seu valor secreto.</span><span class="sxs-lookup"><span data-stu-id="26b0e-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="26b0e-160">Primeiro você deve adicionar a seguinte hello usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="26b0e-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="26b0e-161">Adicionar tooinvoke chamadas de método hello Cofre de chaves e recuperar o segredo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="26b0e-162">Nesse método, você deve fornecer segredo Olá URI que você salvou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="26b0e-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="26b0e-163">Observe o uso de saudação do hello **GetToken** método da saudação **utilitários** classe criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="26b0e-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="26b0e-164">Quando você executar o aplicativo, você agora deve autenticar tooAzure do Active Directory e, em seguida, recuperar o valor de segredo do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="26b0e-165">Rotação de chaves usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="26b0e-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="26b0e-166">Há várias opções para implementar uma estratégia de rotação para valores armazenados como segredos do Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="26b0e-167">Os segredos podem ser rotacionados como parte de um processo manual, programaticamente usando chamadas à API ou por meio de um script de Automação.</span><span class="sxs-lookup"><span data-stu-id="26b0e-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="26b0e-168">Para fins de saudação deste artigo, você será usando o PowerShell Azure combinado com toochange de automação do Azure, uma chave de acesso da conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="26b0e-169">Em seguida, você atualizará um segredo do cofre de chaves com essa nova chave.</span><span class="sxs-lookup"><span data-stu-id="26b0e-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="26b0e-170">tooallow automação do Azure tooset secretos valores em seu Cofre de chaves, você deve obter ID de saudação do cliente para conexão Olá denominado AzureRunAsConnection, que foi criado quando você estabelecer sua instância de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="26b0e-171">Você pode localizar a ID selecionando **Ativos** da instância da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="26b0e-172">A partir daí, você deve escolher **conexões** e, em seguida, selecione Olá **AzureRunAsConnection** princípio de serviço.</span><span class="sxs-lookup"><span data-stu-id="26b0e-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="26b0e-173">Anote Olá **ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-173">Take note of hello **Application ID**.</span></span>

![ID do cliente da Automação do Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="26b0e-175">Em **Ativos**, escolha **Módulos**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="26b0e-176">De **módulos**, selecione **galeria**e, em seguida, procure e **importação** versões atualizadas dos cada Olá módulos a seguir:</span><span class="sxs-lookup"><span data-stu-id="26b0e-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="26b0e-177">A gravação da saudação deste artigo, hello mencionado anteriormente módulos necessários toobe atualizado apenas para Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="26b0e-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="26b0e-178">Se achar que o trabalho de automação está falhando, confirme se importou todos os módulos necessários e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="26b0e-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="26b0e-179">Depois de recuperar ID do aplicativo hello para sua conexão de automação do Azure, você deve informar o seu Cofre de chaves que esse aplicativo tenha acesso tooupdate segredos em seu cofre.</span><span class="sxs-lookup"><span data-stu-id="26b0e-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="26b0e-180">Isso pode ser feito com hello comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="26b0e-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="26b0e-181">Em seguida, selecione **Runbooks** na instância da Automação do Azure e selecione **Adicionar um Runbook**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="26b0e-182">Selecione **Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-182">Select **Quick Create**.</span></span> <span data-ttu-id="26b0e-183">Nome do seu runbook e selecione **PowerShell** como tipo de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="26b0e-184">Você tem Olá opção tooadd uma descrição.</span><span class="sxs-lookup"><span data-stu-id="26b0e-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="26b0e-185">Por fim, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-185">Finally, click **Create**.</span></span>

![Criar runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="26b0e-187">Saudação de colar o script do PowerShell no painel do editor de saudação para seu novo runbook a seguir:</span><span class="sxs-lookup"><span data-stu-id="26b0e-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

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

<span data-ttu-id="26b0e-188">No painel do editor de saudação, escolha **painel teste** tootest seu script.</span><span class="sxs-lookup"><span data-stu-id="26b0e-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="26b0e-189">Depois que o script hello está sendo executado sem erro, você pode selecionar **publicar**, e, em seguida, você pode aplicar uma agenda para Olá runbook no painel de configuração de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="26b0e-190">Pipeline de auditoria do Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="26b0e-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="26b0e-191">Quando você configura um cofre de chaves, você pode ativar a auditoria toocollect logs em solicitações de acesso feitas toohello Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="26b0e-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="26b0e-192">Esses logs são armazenados em uma conta de armazenamento do Azure designada e podem ser extraídos, monitorados e analisados.</span><span class="sxs-lookup"><span data-stu-id="26b0e-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="26b0e-193">Olá cenário a seguir usa funções do Azure, aplicativos lógicos do Azure e toocreate de logs de auditoria do Cofre de chaves toosend um pipeline um email quando um aplicativo que corresponde à ID do aplicativo de saudação do aplicativo web de saudação recupera segredos de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="26b0e-194">Primeiro, você deve habilitar o log no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="26b0e-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="26b0e-195">Isso pode ser feito por meio de saudação comandos do PowerShell a seguir (detalhes completos podem ser vistos no [registro de Cofre de chave](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="26b0e-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="26b0e-196">Depois que isso é habilitado, os logs de auditoria iniciar coleta em Olá designado a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="26b0e-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="26b0e-197">Esses logs contêm eventos sobre como e quando os cofres de chaves são acessados e por quem.</span><span class="sxs-lookup"><span data-stu-id="26b0e-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="26b0e-198">Você pode acessar suas informações de registro em log 10 minutos após a operação de Cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b0e-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="26b0e-199">Geralmente será mais rápido do que isso.</span><span class="sxs-lookup"><span data-stu-id="26b0e-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="26b0e-200">Olá próxima etapa é muito[criar uma fila do barramento de serviço do Azure](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="26b0e-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="26b0e-201">Esse é o local para o qual os logs de auditoria do cofre de chaves são enviados.</span><span class="sxs-lookup"><span data-stu-id="26b0e-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="26b0e-202">Quando mensagens de saudação do log de auditoria na fila hello, Olá lógica aplicativo seleciona-los e age sobre eles.</span><span class="sxs-lookup"><span data-stu-id="26b0e-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="26b0e-203">Crie um barramento de serviço com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="26b0e-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="26b0e-204">Criar um namespace de barramento de serviço (se você já tiver um que você deseja toouse para isso, ignorar tooStep 2).</span><span class="sxs-lookup"><span data-stu-id="26b0e-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="26b0e-205">Procure o barramento de serviço toohello Olá portal do Azure e selecione Olá namespace em que deseja toocreate fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b0e-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="26b0e-206">Selecione **novo** e escolha **barramento de serviço > fila** e insira os detalhes de saudação necessária.</span><span class="sxs-lookup"><span data-stu-id="26b0e-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="26b0e-207">Selecione informações de conexão do barramento do serviço Olá escolhendo Olá namespace e clicando em **informações de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="26b0e-208">Você precisará dessas informações para a próxima seção de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b0e-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="26b0e-209">Em seguida, [criar uma função do Azure](../azure-functions/functions-create-first-azure-function.md) toopoll logs de Cofre de chaves no hello conta de armazenamento e retirar os novos eventos.</span><span class="sxs-lookup"><span data-stu-id="26b0e-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="26b0e-210">Essa será uma função disparada em um cronograma.</span><span class="sxs-lookup"><span data-stu-id="26b0e-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="26b0e-211">toocreate uma função do Azure, escolha **Novo > função de aplicativo** em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="26b0e-212">Durante a criação, você pode usar um plano de hospedagem existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="26b0e-213">Você também pode optar pela hospedagem dinâmica.</span><span class="sxs-lookup"><span data-stu-id="26b0e-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="26b0e-214">Mais detalhes sobre opções de hospedagem de função podem ser encontrados em [como tooscale funções do Azure](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="26b0e-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="26b0e-215">Quando Olá função do Azure é criada, navegar tooit e escolha um timer de função e C\#.</span><span class="sxs-lookup"><span data-stu-id="26b0e-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="26b0e-216">Em seguida, clique em **Criar esta função**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-216">Then click **Create this function**.</span></span>

![Folha de Início das Funções do Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="26b0e-218">Em Olá **desenvolver** guia, substitua o código de run.csx Olá pela seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="26b0e-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

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
> <span data-ttu-id="26b0e-219">Faça tooreplace-se de que variáveis de saudação na Olá anterior conta de armazenamento do código toopoint tooyour onde Olá Cofre de chaves logs são gravados, criada anteriormente, o barramento de serviço hello e Olá logs de armazenamento de Cofre de chaves de toohello caminho específico.</span><span class="sxs-lookup"><span data-stu-id="26b0e-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="26b0e-220">função Hello pega hello mais recente arquivo de log da conta de armazenamento Olá onde Olá Cofre de chaves logs são gravados, captura os eventos mais recentes Olá desse arquivo, e envia-os tooa fila de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="26b0e-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="26b0e-221">Como um único arquivo pode ter vários eventos, você deve criar um arquivo de sync.txt função hello também analisa toodetermine Olá carimbo de data do último evento de saudação que foi recebido.</span><span class="sxs-lookup"><span data-stu-id="26b0e-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="26b0e-222">Isso garante que você não enviar Olá mesmo evento várias vezes.</span><span class="sxs-lookup"><span data-stu-id="26b0e-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="26b0e-223">Este arquivo sync.txt contém um carimbo de hora para o último evento de encontrado hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="26b0e-224">Olá, logs, quando carregado, tem toobe classificado com base em Olá timestamp tooensure eles serão ordenados corretamente.</span><span class="sxs-lookup"><span data-stu-id="26b0e-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="26b0e-225">Para esta função, podemos fazer referência a algumas bibliotecas adicionais que não estão disponíveis sem a necessidade de saudação em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b0e-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="26b0e-226">tooinclude isso, precisamos de funções do Azure toopull-los usando o NuGet.</span><span class="sxs-lookup"><span data-stu-id="26b0e-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="26b0e-227">Escolha Olá **exibir arquivos** opção.</span><span class="sxs-lookup"><span data-stu-id="26b0e-227">Choose hello **View Files** option.</span></span>

![Opção Exibir Arquivos](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="26b0e-229">Adicione um arquivo chamado project.json com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="26b0e-229">And add a file called project.json with following content:</span></span>

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
<span data-ttu-id="26b0e-230">Após a **salvar**, funções do Azure será baixado binários Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="26b0e-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="26b0e-231">Alternar toohello **integrar** guia e dar ao parâmetro de timer de saudação toouse um nome significativo em função hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="26b0e-232">Olá precede o código, ele espera que Olá timer toobe chamado *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="26b0e-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="26b0e-233">Especifique um [expressão CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) da seguinte maneira: 0 \* \* \* \* \* pelo temporizador hello que causarão Olá função toorun a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="26b0e-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="26b0e-234">Olá na mesma **integrar** guia, adicione uma entrada do tipo hello **armazenamento de BLOBs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="26b0e-235">Isso vai apontar toohello sync.txt arquivo que contém Olá carimbo de hora do último evento de saudação verificado pela função hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="26b0e-236">Isso estará disponível em função hello pelo nome do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="26b0e-237">Olá precede o código, Olá entrada de armazenamento de BLOBs do Azure espera que toobe de nome de parâmetro hello *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="26b0e-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="26b0e-238">Escolha Olá conta de armazenamento onde o arquivo de sync.txt Olá residirá (pode ser Olá mesmo ou outra conta de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="26b0e-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="26b0e-239">No campo de caminho hello, forneça o caminho de saudação onde o arquivo hello reside no formato Olá {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="26b0e-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="26b0e-240">Adicionar uma saída de tipo hello *armazenamento de BLOBs do Azure* saída.</span><span class="sxs-lookup"><span data-stu-id="26b0e-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="26b0e-241">Isso vai apontar toohello sync.txt arquivo definido na entrada hello.</span><span class="sxs-lookup"><span data-stu-id="26b0e-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="26b0e-242">Isso é usado pelo Olá função toowrite Olá carimbo de hora Olá último evento examinado.</span><span class="sxs-lookup"><span data-stu-id="26b0e-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="26b0e-243">o código anterior Hello espera este toobe parâmetro chamado *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="26b0e-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="26b0e-244">Neste ponto, a função hello está pronta.</span><span class="sxs-lookup"><span data-stu-id="26b0e-244">At this point, hello function is ready.</span></span> <span data-ttu-id="26b0e-245">Fazer toohello back se tooswitch **desenvolver** guia e salve o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b0e-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="26b0e-246">Verifique a janela de saída Olá para os erros de compilação e corrija-as adequadamente.</span><span class="sxs-lookup"><span data-stu-id="26b0e-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="26b0e-247">Se código Olá compila, código Olá deve agora ser verificando Olá Cofre de chaves logs a cada minuto, e enviar quaisquer novos eventos para Olá definido fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="26b0e-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="26b0e-248">Você deve ver as informações de log gravar toohello a janela de log sempre que a função hello é disparada.</span><span class="sxs-lookup"><span data-stu-id="26b0e-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="26b0e-249">Aplicativo lógico do Azure</span><span class="sxs-lookup"><span data-stu-id="26b0e-249">Azure logic app</span></span>
<span data-ttu-id="26b0e-250">Em seguida, você deve criar um aplicativo do Azure lógica que seleciona eventos Olá função hello está fazendo a fila do barramento de serviço toohello, analisa o conteúdo de saudação e envia um email com base em um critério de correspondência.</span><span class="sxs-lookup"><span data-stu-id="26b0e-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="26b0e-251">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) indo muito**Novo > aplicativo lógico**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="26b0e-252">Depois de criar o aplicativo lógico de saudação, navegar tooit e escolher **editar**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="26b0e-253">No editor de aplicativo da lógica de saudação, escolha **fila do barramento de serviço** e insira sua tooconnect de credenciais do barramento de serviço-toohello fila.</span><span class="sxs-lookup"><span data-stu-id="26b0e-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Barramento de Serviço de aplicativo lógico do Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="26b0e-255">Depois, escolha **Adicionar uma condição**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="26b0e-256">Na condição de saudação alternar toohello editor avançado e digite Olá código a seguir, substituindo APP_ID com hello APP_ID real de seu aplicativo web:</span><span class="sxs-lookup"><span data-stu-id="26b0e-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="26b0e-257">Essa expressão retorna essencialmente **false** se hello *appid* de saudação evento de entrada (que é o corpo de saudação da mensagem de saudação do barramento de serviço) não é Olá *appid* de saudação aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26b0e-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="26b0e-258">Agora, crie uma ação em **Se não, não faça nada**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-258">Now, create an action under **If no, do nothing**.</span></span>

![Escolher ação do aplicativo lógico do Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="26b0e-260">Para a ação de saudação, escolha **Office 365 - enviar email**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="26b0e-261">Preencha Olá campos toocreate toosend um email quando Olá definido a condição retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="26b0e-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="26b0e-262">Se você não tiver o Office 365, você pode examinar alternativas tooachieve Olá os mesmos resultados.</span><span class="sxs-lookup"><span data-stu-id="26b0e-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="26b0e-263">Neste ponto, você tem um pipeline de tooend final que procura os logs de auditoria do novo cofre de chaves a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="26b0e-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="26b0e-264">Ele envia novos logs encontrar tooa fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="26b0e-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="26b0e-265">aplicativo de lógica de saudação é disparado quando uma nova mensagem chega na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b0e-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="26b0e-266">Se hello *appid* dentro Olá eventos não correspondem Olá ID do aplicativo de saudação aplicativo de chamada, ele envia um email.</span><span class="sxs-lookup"><span data-stu-id="26b0e-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
