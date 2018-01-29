---
title: "Autenticação do usuário final: SDK do .NET com o Data Lake Store usando o Azure Active Directory | Microsoft Docs"
description: "Saiba como obter a autenticação do usuário final com o Data Lake Store usando o Azure Active Directory com o SDK do .NET"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/09/2018
ms.author: nitinme
ms.openlocfilehash: ea71743e775da8cfd85ecbd20e9c5981a198e05c
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
# <a name="end-user-authentication-with-data-lake-store-using-net-sdk"></a>Autenticação do usuário final com o Data Lake Store usando o SDK do .NET
> [!div class="op_single_selector"]
> * [Usando o Java](data-lake-store-end-user-authenticate-java-sdk.md)
> * [Usar o SDK .NET](data-lake-store-end-user-authenticate-net-sdk.md)
> * [Usando o Python](data-lake-store-end-user-authenticate-python.md)
> * [Usar a API REST](data-lake-store-end-user-authenticate-rest-api.md)
> 
>  

Neste artigo, você aprenderá como usar o SDK do .NET para fazer a autenticação do usuário final com o Azure Data Lake Store. Para saber sobre autenticação serviço a serviço com o Data Lake Store usando o SDK do .NET, consulte [Autenticação serviço a serviço com Data Lake Store usando o SDK do .NET](data-lake-store-service-to-service-authenticate-net-sdk.md).

## <a name="prerequisites"></a>Pré-requisitos
* **Visual Studio 2013, 2015 ou 2017**. As instruções abaixo usam o Visual Studio 2017.

* **Uma assinatura do Azure**. Consulte [Obter a avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Criar um aplicativo "Nativo" do Azure Active Directory**. Você deve ter concluído as etapas em [Autenticação do usuário final com o Data Lake Store usando o Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>Criar um aplicativo .NET
1. Abra o Visual Studio e crie um aplicativo de console.
2. No menu **Arquivo**, clique em **Novo** e em **Projeto**.
3. Em **Novo Projeto**, digite ou selecione os seguintes valores:

   | Propriedade | Valor |
   | --- | --- |
   | Categoria |Modelos/Visual C#/Windows |
   | Modelo |Aplicativo de console |
   | NOME |CreateADLApplication |

4. Clique em **OK** para criar o projeto.

5. Adicione os pacotes NuGet ao seu projeto.

   1. Clique com o botão direito do mouse no nome do projeto no Gerenciador de Soluções e clique em **Gerenciar Pacotes NuGet**.
   2. Na guia **Gerenciador de Pacotes NuGet**, verifique se a **Origem do pacote** está definida como **nuget.org** e se a caixa de seleção **Incluir pré-lançamento** está marcada.
   3. Procure e instale os seguintes pacotes NuGet:

      * `Microsoft.Azure.Management.DataLake.Store` - este tutorial usa a versão 2.1.3-preview.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - este tutorial usa a versão v2.2.12.

        ![Adicionar uma origem de NuGet](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Criar uma nova conta do Azure Data Lake")
   4. Feche o **Gerenciador de Pacotes NuGet**.

6. Abrir **Program.cs**
7. Libere o uso de instruções com as linhas a seguir:

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Collections.Generic;
            
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;
    using Microsoft.Azure.Management.DataLake.Store;
    using Microsoft.Azure.Management.DataLake.Store.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    ```     

## <a name="end-user-authentication"></a>Autenticação do usuário final
Adicione este trecho no aplicativo cliente do .NET. Substitua os valores de espaço reservado pelos valores recuperados de um aplicativo nativo do Azure AD (listado como pré-requisito). Este trecho de código permite autenticar seu aplicativo **interativamente** com Data Lake Store, o que significa que você será solicitado a inserir suas credenciais do Azure.

Para facilitar o uso, o trecho a seguir usa valores padrão para a ID do cliente e o URI de redirecionamento que são válidos com qualquer assinatura do Azure. No trecho a seguir, você só precisa fornecer o valor da sua ID de locatário. Você pode recuperar a ID de locatário usando as instruções fornecidas em [Obter a ID de locatário](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
    
- Substitua a função Main() pelo código a seguir:

    ```csharp
    private static void Main(string[] args)
    {
        //User login via interactive popup
        string TENANT = "<AAD-directory-domain>";
        string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
        System.Uri ARM_TOKEN_AUDIENCE = new System.Uri(@"https://management.core.windows.net/");
        System.Uri ADL_TOKEN_AUDIENCE = new System.Uri(@"https://datalake.azure.net/");
        string MY_DOCUMENTS = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);
        string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");
        var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
        var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
        var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
    }
    ```

Algumas informações importantes sobre o trecho de código anterior:

* O trecho de código anterior usa funções auxiliares `GetTokenCache` e `GetCreds_User_Popup`. O código para essas funções auxiliares está disponível [aqui no Github](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options#gettokencache).
* Para ajudá-lo a concluir o tutorial mais rapidamente, o trecho de código usa uma ID de cliente de aplicativo nativa disponível por padrão a todas as assinaturas do Azure. Portanto, você pode **usar o trecho de código como está em seu aplicativo**.
* No entanto, se você quiser usar sua própria ID de cliente de aplicativo e o domínio do Azure AD, crie um aplicativo nativo Azure AD e use a ID de locatário do Azure AD, a ID de cliente e o URI de redirecionamento para o aplicativo que você criou. Veja [Criar um aplicativo do Active Directory para autenticação do usuário final no Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) para obter instruções.

  
## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu a usar a autenticação do usuário final para autenticar no Azure Data Lake Store com o SDK do .NET. Agora você pode examinar os seguintes artigos que discorrem sobre como usar o SDK do .NET para trabalhar com o Azure Data Lake Store.

* [Operações de gerenciamento de conta no Data Lake Store usando o SDK do .NET](data-lake-store-get-started-net-sdk.md)
* [Operações de dados no Data Lake Store usando o SDK do .NET](data-lake-store-data-operations-net-sdk.md)

