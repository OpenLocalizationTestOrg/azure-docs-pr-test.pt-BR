---
title: "Autenticação no Data Lake Store usando o Azure Active Directory | Microsoft Docs"
description: Saiba como se autenticar com o Data Lake Store usando o Azure Active Directory
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/09/2018
ms.author: nitinme
ms.openlocfilehash: 7e6e37c0f5c8447b0e6d147a297b460d323b8894
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="authentication-with-data-lake-store-using-azure-active-directory"></a>Autenticação com o Data Lake Store usando o Azure Active Directory

O Azure Data Lake Store usa o Azure Active Directory para autenticação. Antes de criar um aplicativo que funciona com o Azure Data Lake Store, você deve decidir como deseja autenticar seu aplicativo no Azure AD (Azure Active Directory). 

## <a name="authentication-options"></a>Opções de autenticação

* **Autenticação do usuário final** – as credenciais de um usuário final do Azure são usadas para se autenticar com o Data Lake Store. O aplicativo criado para funcionar com o Data Lake Store solicita essas credenciais de usuário. Como resultado, esse mecanismo de autenticação é *interativo* e o aplicativo é executado no contexto do usuário conectado. Para obter mais informações e instruções, consulte [Autenticação de usuário final para o Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md).

* **Autenticação serviço a serviço** – Use essa opção se desejar que um aplicativo faça sua própria autenticação com o Data Lake Store. Nesses casos, você cria um aplicativo do Azure AD (Active Directory) e usa a chave do aplicativo do Azure AD para se autenticar com o Data Lake Store. Como resultado, esse mecanismo de autenticação *não é interativo*. Para obter mais informações e instruções, consulte [Autenticação serviço a serviço para o Data Lake Store](data-lake-store-service-to-service-authenticate-using-active-directory.md).

A tabela a seguir ilustra como os mecanismos de autenticação de usuário final e serviço a serviço têm suporte no Data Lake Store. Veja como ler a tabela.

* O símbolo ✔ * indica que a opção de autenticação tem suporte e fornece um link para um artigo que demonstra como usar essa opção de autenticação. 
* O símbolo ✔ indica que a opção de autenticação tem suporte. 
* As células vazias indicam que a opção de autenticação não tem suporte.


|Use essa opção de autenticação com...                   |.NET         |Java     |PowerShell |CLI 2.0 | Python   |REST     |
|:---------------------------------------------|:------------|:--------|:----------|:-------------|:---------|:--------|
|Usuário final (sem MFA **)                        |   ✔ |    ✔    |    ✔      |       ✔      |    **[✔ *](data-lake-store-end-user-authenticate-python.md#end-user-authentication-without-multi-factor-authentication)**(preterido)     |    **[✔*](data-lake-store-end-user-authenticate-rest-api.md)**    |
|Usuário final (com MFA)                           |    **[✔*](data-lake-store-end-user-authenticate-net-sdk.md)**        |    **[✔*](data-lake-store-end-user-authenticate-java-sdk.md)**     |    ✔      |       **[✔*](data-lake-store-get-started-cli-2.0.md)**      |    **[✔*](data-lake-store-end-user-authenticate-python.md#end-user-authentication-with-multi-factor-authentication)**     |    ✔    |
|Serviço a serviço (usando a chave de cliente)         |    **[✔*](data-lake-store-service-to-service-authenticate-net-sdk.md#service-to-service-authentication-with-client-secret)** |    **[✔*](data-lake-store-service-to-service-authenticate-java.md)**    |    ✔      |       ✔      |    **[✔*](data-lake-store-service-to-service-authenticate-python.md#service-to-service-authentication-with-client-secret-for-account-management)**     |    **[✔*](data-lake-store-service-to-service-authenticate-rest-api.md)**    |
|Serviço a serviço (usando o certificado do cliente) |    **[✔*](data-lake-store-service-to-service-authenticate-net-sdk.md#service-to-service-authentication-with-certificate)**        |    ✔    |    ✔      |       ✔      |    ✔     |    ✔    |

<i>* Clique no símbolo <b>✔\*</b>. Ele é um link.</i><br>
<i>** MFA significa autenticação multifator</i>

Consulte [Cenários de autenticação do Azure Active Directory](../active-directory/develop/active-directory-authentication-scenarios.md) para obter mais informações sobre como usar o Azure Active Directory para autenticação.

## <a name="next-steps"></a>Próximas etapas

* [Autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md)
* [Autenticação serviço a serviço](data-lake-store-service-to-service-authenticate-using-active-directory.md)


