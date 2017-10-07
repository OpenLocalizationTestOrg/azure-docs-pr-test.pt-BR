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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Criar aplicativos .NET HDInsight de autenticação não interativa
Você pode executar seu aplicativo .NET do Azure HDInsight na identidade do aplicativo (não interativo) ou com identidade de saudação do hello assinado no usuário do aplicativo hello (interativo). Para obter um exemplo de aplicativo interativo do hello, consulte [conectar tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). Este artigo mostra como toocreate autenticação não interativo .NET aplicativo tooconnect tooAzure e gerenciar o HDInsight.

Em seu aplicativo .NET não interativo, você precisa:

* Da sua ID de locatário da assinatura do Azure (também conhecida como ID de diretório). Veja [Obter a ID de locatário](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* ID do cliente de aplicativo do Active Directory do Azure Hello. Consulte [Criar um aplicativo do Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) e [Obter uma ID de aplicativo](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* chave secreta do aplicativo do Active Directory do Azure de saudação. Consulte [Obter chave de autenticação do aplicativo](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>Pré-requisitos
* Cluster HDInsight. Consulte [tutorial de introdução](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-toorole"></a>Atribuir toorole de aplicativo do AD do Azure
Você deve atribuir Olá aplicativo tooa [função](../active-directory/role-based-access-built-in-roles.md) toogrant ela permissões para executar ações. Você pode definir o escopo de saudação no nível de saudação de assinatura de saudação, o grupo de recursos ou o recurso. permissões de saudação são herdadas toolower níveis de escopo (por exemplo, adicionando que uma função de leitor de toohello de aplicativo para um grupo de recursos significa que ela pode ler o grupo de recursos de saudação e os recursos que ele contém). Neste tutorial, você definirá o escopo de saudação no nível do grupo de recursos de saudação. Para obter mais informações, consulte [usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](../active-directory/role-based-access-control-configure.md)

**Olá tooadd aplicativo do proprietário função toohello AD do Azure**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **grupo de recursos** no painel esquerdo do hello.
3. Clique em grupo de recursos de saudação que contém o cluster do HDInsight Olá onde você executa a consulta de Hive posteriormente neste tutorial. Se houver muitos grupos de recursos, você pode usar o filtro de saudação.
4. Clique em **(IAM) do controle de acesso** Olá recursos no menu de grupo.
5. Clique em **adicionar** de saudação **usuários** folha.
6. Siga saudação do hello instrução tooadd **proprietário** função toohello aplicativo AD do Azure que você criou no procedimento de última hello. Quando concluir com êxito, você deverá ver o aplicativo hello listado na folha do hello usuários com função de proprietário de saudação.

## <a name="develop-hdinsight-client-application"></a>Desenvolver aplicativos do cliente HDInsight

1. Criar um aplicativo de console em C#
2. Adicione Olá pacotes do Nuget a seguir:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Use Olá exemplo de código a seguir:

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

## <a name="next-steps"></a>Próximas etapas
* [Criar o aplicativo do Azure Active Directory e a entidade de serviço usando o portal](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Autenticação de uma entidade de serviço com o Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Controle de Acesso Baseado em Função do Azure](../active-directory/role-based-access-control-configure.md)
