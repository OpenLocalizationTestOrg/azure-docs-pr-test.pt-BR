---
title: aaaConnect tooAzure Analysis Services | Microsoft Docs
description: Saiba como tooconnect tooand obter dados de um servidor do Analysis Services no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Conectar-se o servidor de serviços de análise do Azure tooan

Este artigo descreve tooa conectando o servidor usando a modelagem de dados e aplicativos de gerenciamento como o SQL Server Management Studio (SSMS) ou SQL Server Data Tools (SSDT). Ou, com aplicativos de relatório de cliente como o Microsoft Excel, Power BI Desktop ou aplicativos personalizados. Conexões tooAzure Analysis Services usar HTTPS.

## <a name="client-libraries"></a>Bibliotecas de cliente
[Obter Olá bibliotecas de cliente mais recentes](analysis-services-data-providers.md)

Todas as conexões tooa server, independentemente do tipo, requer atualizado AMO, ADOMD.NET e OLEDB bibliotecas tooconnect tooand interface de cliente com um servidor do Analysis Services. Para SSMS, o SSDT, o Excel 2016 e o Power BI, bibliotecas de cliente mais recentes Olá são instaladas ou atualizadas com as versões mensais. No entanto, em alguns casos, é possível que um aplicativo pode não ter hello mais recente. Por exemplo, quando atualizações de atraso de políticas ou atualizações do Office 365 estão em Olá canal adiado.

## <a name="server-name"></a>Nome do servidor

Quando você cria um servidor do Analysis Services no Azure, você pode especificar uma região de nome e hello exclusiva, onde o servidor de saudação é toobe criado. Ao especificar o nome do servidor de saudação em uma conexão, o esquema de nomenclatura de servidor de saudação é:

```
<protocol>://<region>/<servername>
```
 Em que o protocolo é cadeia de caracteres **asazure**, região é hello Uri em que o servidor de saudação foi criado (por exemplo, westus.asazure.windows.net) e servername é o nome de saudação do servidor exclusivo dentro da região de saudação.

### <a name="get-hello-server-name"></a>Obter o nome do servidor de saudação
Em **portal do Azure** > servidor > **visão geral** > **nome do servidor**, nome de todo o servidor de saudação de cópia. Se outros usuários na sua organização estiver se conectando a servidor toothis demais, você pode compartilhar este nome de servidor com eles. Ao especificar um nome de servidor, o caminho inteiro Olá deve ser usado.

![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Cadeia de conexão

Ao conectar-se tooAzure Analysis Services usando Olá modelo de objeto Tabular, Olá use formatos de cadeia de caracteres de conexão a seguir:

###### <a name="integrated-azure-active-directory-authentication"></a>Autenticação integrada do Azure Active Directory
A autenticação integrada pega Olá cache de credenciais do Active Directory do Azure se disponível. Caso contrário, a janela de logon do Azure Olá é mostrada.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Autenticação do Azure Active Directory com nome de usuário e senha

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Autenticação do Windows (segurança integrada)
Use conta do Windows hello executando o processo atual hello.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Conectar usando um arquivo .odc
Com versões anteriores do Excel, usuários podem se conectar tooan servidor de serviços de análise do Azure usando um arquivo de Conexão de dados do Office (. odc). mais, consulte toolearn [criar um arquivo de Conexão de dados do Office (. odc)](analysis-services-odc.md).


## <a name="next-steps"></a>Próximas etapas
[Conectar com Excel](analysis-services-connect-excel.md)    
[Conectar com Power BI](analysis-services-connect-pbi.md)   
[Gerenciar seu serviço](analysis-services-manage.md)   

