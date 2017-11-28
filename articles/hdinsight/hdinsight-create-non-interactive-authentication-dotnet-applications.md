---
title: "autenticação não interativo de aaaCreate HDInsight .NET applciations - Azure | Microsoft Docs"
description: "Saiba como toocreate aplicativos de HDInsight .NET de autenticação não interativo."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="a1bcc-103">Criar aplicativos .NET HDInsight de autenticação não interativa</span><span class="sxs-lookup"><span data-stu-id="a1bcc-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="a1bcc-104">Você pode executar seu aplicativo .NET do Azure HDInsight na identidade do aplicativo (não interativo) ou com identidade de saudação do hello assinado no usuário do aplicativo hello (interativo).</span><span class="sxs-lookup"><span data-stu-id="a1bcc-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="a1bcc-105">Para obter um exemplo de aplicativo interativo do hello, consulte [conectar tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="a1bcc-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="a1bcc-106">Este artigo mostra como toocreate autenticação não interativo .NET aplicativo tooconnect tooAzure e gerenciar o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="a1bcc-107">Em seu aplicativo .NET não interativo, você precisa:</span><span class="sxs-lookup"><span data-stu-id="a1bcc-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="a1bcc-108">Da sua ID de locatário da assinatura do Azure (também conhecida como ID de diretório).</span><span class="sxs-lookup"><span data-stu-id="a1bcc-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="a1bcc-109">Veja [Obter a ID de locatário](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="a1bcc-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="a1bcc-110">ID do cliente de aplicativo do Active Directory do Azure Hello.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="a1bcc-111">Consulte [Criar um aplicativo do Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) e [Obter uma ID de aplicativo](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="a1bcc-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="a1bcc-112">chave secreta do aplicativo do Active Directory do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="a1bcc-113">Consulte [Obter chave de autenticação do aplicativo](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="a1bcc-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1bcc-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a1bcc-114">Prerequisites</span></span>
* <span data-ttu-id="a1bcc-115">Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-115">HDInsight cluster.</span></span> <span data-ttu-id="a1bcc-116">Consulte [tutorial de introdução](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="a1bcc-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="a1bcc-117">Atribuir toorole de aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a1bcc-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="a1bcc-118">Você deve atribuir Olá aplicativo tooa [função](../active-directory/role-based-access-built-in-roles.md) toogrant ela permissões para executar ações.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="a1bcc-119">Você pode definir o escopo de saudação no nível de saudação de assinatura de saudação, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="a1bcc-120">permissões de saudação são herdadas toolower níveis de escopo (por exemplo, adicionando que uma função de leitor de toohello de aplicativo para um grupo de recursos significa que ela pode ler o grupo de recursos de saudação e os recursos que ele contém).</span><span class="sxs-lookup"><span data-stu-id="a1bcc-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="a1bcc-121">Neste tutorial, você definirá o escopo de saudação no nível do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="a1bcc-122">Para obter mais informações, consulte [usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="a1bcc-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="a1bcc-123">**Olá tooadd aplicativo do proprietário função toohello AD do Azure**</span><span class="sxs-lookup"><span data-stu-id="a1bcc-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="a1bcc-124">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a1bcc-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a1bcc-125">Clique em **grupo de recursos** no painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="a1bcc-126">Clique em grupo de recursos de saudação que contém o cluster do HDInsight Olá onde você executa a consulta de Hive posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="a1bcc-127">Se houver muitos grupos de recursos, você pode usar o filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="a1bcc-128">Clique em **(IAM) do controle de acesso** Olá recursos no menu de grupo.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="a1bcc-129">Clique em **adicionar** de saudação **usuários** folha.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="a1bcc-130">Siga saudação do hello instrução tooadd **proprietário** função toohello aplicativo AD do Azure que você criou no procedimento de última hello.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="a1bcc-131">Quando concluir com êxito, você deverá ver o aplicativo hello listado na folha do hello usuários com função de proprietário de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1bcc-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="a1bcc-132">Desenvolver aplicativos do cliente HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1bcc-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="a1bcc-133">Criar um aplicativo de console em C#</span><span class="sxs-lookup"><span data-stu-id="a1bcc-133">Create a C# console application.</span></span>
2. <span data-ttu-id="a1bcc-134">Adicione Olá pacotes do Nuget a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1bcc-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="a1bcc-135">Use Olá exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1bcc-135">Use hello following code sample:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter hello Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a><span data-ttu-id="a1bcc-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1bcc-136">Next steps</span></span>
* [<span data-ttu-id="a1bcc-137">Criar o aplicativo do Azure Active Directory e a entidade de serviço usando o portal</span><span class="sxs-lookup"><span data-stu-id="a1bcc-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="a1bcc-138">Autenticação de uma entidade de serviço com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a1bcc-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="a1bcc-139">Controle de Acesso Baseado em Função do Azure</span><span class="sxs-lookup"><span data-stu-id="a1bcc-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
