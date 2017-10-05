---
title: "Criar aplicativos .NET HDInsight de autenticação não interativa – Azure | Microsoft Docs"
description: "Saiba como criar aplicativos .NET HDInsight de autenticação não interativa."
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
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="87cf4-103">Criar aplicativos .NET HDInsight de autenticação não interativa</span><span class="sxs-lookup"><span data-stu-id="87cf4-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="87cf4-104">Você pode executar seu aplicativo .NET do Azure HDInsight na própria identidade do aplicativo (não interativo) ou na identidade do usuário conectado do aplicativo (interativo).</span><span class="sxs-lookup"><span data-stu-id="87cf4-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="87cf4-105">Para obter um exemplo do aplicativo interativo, consulte [Conectar-se ao Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="87cf4-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="87cf4-106">Este artigo mostra como criar um aplicativo .NET de autenticação não interativa para se conectar ao Azure e gerenciar o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87cf4-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="87cf4-107">Em seu aplicativo .NET não interativo, você precisa:</span><span class="sxs-lookup"><span data-stu-id="87cf4-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="87cf4-108">Da sua ID de locatário da assinatura do Azure (também conhecida como ID de diretório).</span><span class="sxs-lookup"><span data-stu-id="87cf4-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="87cf4-109">Veja [Obter a ID de locatário](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="87cf4-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="87cf4-110">A ID de cliente do aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87cf4-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="87cf4-111">Consulte [Criar um aplicativo do Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) e [Obter uma ID de aplicativo](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="87cf4-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="87cf4-112">A chave secreta do aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87cf4-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="87cf4-113">Consulte [Obter chave de autenticação do aplicativo](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="87cf4-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87cf4-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="87cf4-114">Prerequisites</span></span>
* <span data-ttu-id="87cf4-115">Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87cf4-115">HDInsight cluster.</span></span> <span data-ttu-id="87cf4-116">Consulte [tutorial de introdução](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="87cf4-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="87cf4-117">Atribuir o aplicativo do Azure AD à função</span><span class="sxs-lookup"><span data-stu-id="87cf4-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="87cf4-118">Você deve atribuir o aplicativo a uma [função](../active-directory/role-based-access-built-in-roles.md) para conceder a ele permissões para executar ações.</span><span class="sxs-lookup"><span data-stu-id="87cf4-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="87cf4-119">Você pode definir o escopo no nível da assinatura, do grupo de recursos ou do recurso.</span><span class="sxs-lookup"><span data-stu-id="87cf4-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="87cf4-120">As permissões são herdadas de níveis inferiores do escopo (por exemplo, adicionar um aplicativo à função Leitor de um grupo de recursos significa que ele pode ler o grupo de recursos e todos os recursos que ele contiver).</span><span class="sxs-lookup"><span data-stu-id="87cf4-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="87cf4-121">Neste tutorial, você definirá o escopo no nível de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="87cf4-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="87cf4-122">Para obter mais informações, consulte [Usar atribuições de função para gerenciar o acesso aos recursos de assinatura do Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="87cf4-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="87cf4-123">**Adicionar a função de Proprietário ao aplicativo do Azure AD**</span><span class="sxs-lookup"><span data-stu-id="87cf4-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="87cf4-124">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87cf4-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="87cf4-125">Clique no **Grupo de Recursos** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="87cf4-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="87cf4-126">Clique no grupo de recursos que contém o cluster HDInsight, no qual você executará a consulta Hive posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="87cf4-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="87cf4-127">Se houver muitos grupos de recursos, você poderá usar o filtro.</span><span class="sxs-lookup"><span data-stu-id="87cf4-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="87cf4-128">Clique em **Controle de acesso (IAM)** no menu do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="87cf4-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="87cf4-129">Clique em **Adicionar** na folha **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="87cf4-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="87cf4-130">Siga as instruções para adicionar a função **Proprietário** ao aplicativo do Azure AD que você criou no último procedimento.</span><span class="sxs-lookup"><span data-stu-id="87cf4-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="87cf4-131">Ao concluir a tarefa com êxito, você deverá ver o aplicativo listado na folha Usuários com a função de Proprietário.</span><span class="sxs-lookup"><span data-stu-id="87cf4-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="87cf4-132">Desenvolver aplicativos do cliente HDInsight</span><span class="sxs-lookup"><span data-stu-id="87cf4-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="87cf4-133">Criar um aplicativo de console em C#</span><span class="sxs-lookup"><span data-stu-id="87cf4-133">Create a C# console application.</span></span>
2. <span data-ttu-id="87cf4-134">Adicione os seguintes pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="87cf4-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="87cf4-135">Use o seguinte exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="87cf4-135">Use the following code sample:</span></span>

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
                private static string secretKey = "<Enter the Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
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

## <a name="next-steps"></a><span data-ttu-id="87cf4-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87cf4-136">Next steps</span></span>
* [<span data-ttu-id="87cf4-137">Criar o aplicativo do Azure Active Directory e a entidade de serviço usando o portal</span><span class="sxs-lookup"><span data-stu-id="87cf4-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="87cf4-138">Autenticação de uma entidade de serviço com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="87cf4-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="87cf4-139">Controle de Acesso Baseado em Função do Azure</span><span class="sxs-lookup"><span data-stu-id="87cf4-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
