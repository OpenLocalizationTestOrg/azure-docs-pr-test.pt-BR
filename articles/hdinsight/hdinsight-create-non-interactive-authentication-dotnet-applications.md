---
title: "Criar aplicativos .NET de autenticação não interativa no Azure HDInsight | Microsoft Docs"
description: "Saiba como criar aplicativos Microsoft .NET de autenticação não interativa no Azure HDInsight."
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
ms.date: 01/03/2018
ms.author: jgao
ms.openlocfilehash: b2b24747ce4ea8499c999c693f00fb09178d52b0
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2018
---
# <a name="create-a-non-interactive-authentication-net-hdinsight-application"></a>Criar um aplicativo .NET HDInsight de autenticação não interativa
É possível executar seu aplicativo Microsoft .NET do Azure HDInsight na própria identidade do aplicativo (não interativo) ou na identidade do usuário conectado do aplicativo (interativo). Este artigo mostra como criar um aplicativo .NET de autenticação não interativa para se conectar ao Azure e gerenciar o HDInsight. Para obter um exemplo de um aplicativo interativo, consulte [Conectar-se ao Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). 

Em seu aplicativo .NET não interativo, você precisa:

* Da sua ID de locatário da assinatura do Azure (também conhecida como *ID de diretório*). Veja [Obter a ID de locatário](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* Da ID de cliente do aplicativo do Azure AD (Azure Active Directory). Consulte [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) (Criar um aplicativo do Azure Active Directory) e [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) (Obter uma ID de aplicativo).
* Da chave secreta do aplicativo do Azure AD. Consulte [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) (Obter chave de autenticação do aplicativo).

## <a name="prerequisites"></a>pré-requisitos
* Um cluster HDInsight. Consulte o [tutorial de introdução](hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster).

## <a name="assign-a-role-to-the-azure-ad-application"></a>Atribuir uma função ao aplicativo do Azure AD
Atribua a seu aplicativo do Azure AD uma [função](../active-directory/role-based-access-built-in-roles.md), para lhe conceder permissões para executar ações. Você pode definir o escopo no nível da assinatura, do grupo de recursos ou do recurso. As permissão são herdadas para níveis inferiores do escopo. (Por exemplo, adicionar um aplicativo à função Leitor de um grupo de recursos significa que o aplicativo pode ler o grupo de recursos e todos os recursos nele.) Neste tutorial, você definirá o escopo no nível de grupo de recursos. Para obter mais informações, consulte [Usar atribuições de função para gerenciar o acesso aos recursos de assinatura do Azure](../active-directory/role-based-access-control-configure.md).

**Adicionar a função de Proprietário ao aplicativo do Azure AD**

1. Entre no [Portal do Azure](https://portal.azure.com).
2. No menu esquerdo, selecione **Grupo de recursos**.
3. Selecione o grupo de recursos que contém o cluster HDInsight, no qual você executará a consulta Hive posteriormente neste tutorial. Se você tiver um grande número de grupos de recursos, será possível usar o filtro para localizar o item desejado.
4. No menu do grupo de recursos, selecione **Controle de acesso (IAM)**.
5. Em **Usuários**, selecione **Adicionar**.
6. Siga as instruções para adicionar a função Proprietário ao seu aplicativo do Azure AD. Depois de adicionar a função com êxito, o aplicativo será listado em **Usuários**, com a função Proprietário. 

## <a name="develop-an-hdinsight-client-application"></a>Desenvolver um aplicativo cliente HDInsight

1. Criar um aplicativo de console em C#
2. Adicione os seguintes pacotes NuGet:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Execute o código a seguir:

    ```csharp
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
    
            private static Guid SubscriptionId = new Guid("<Enter your Azure subscription ID>");
            private static string tenantID = "<Enter your tenant ID (also called directory ID)>";
            private static string applicationID = "<Enter your application ID>";
            private static string secretKey = "<Enter the application secret key>";
    
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
    
            /// Get the access token for a service principal and provided key.          
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
    ```


## <a name="next-steps"></a>Próximas etapas
* [Criar uma entidade de serviço e um aplicativo do Azure Active Directory no Portal do Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).
* Saiba como [autenticar uma entidade de serviço com o Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).
* Saiba mais sobre o [Azure RBAC (Controle de Acesso Baseado em Função)](../active-directory/role-based-access-control-configure.md).
