---
title: Conectar-se aos Azure Analysis Services | Microsoft Docs
description: Saiba como se conectar e obter dados de um servidor do Azure Analysis Services.
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
ms.openlocfilehash: deb3ef28d20decef01826450bd6091f87dd069de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-an-azure-analysis-services-server"></a><span data-ttu-id="b22cf-103">Conectar-se a um servidor do Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b22cf-103">Connect to an Azure Analysis Services server</span></span>

<span data-ttu-id="b22cf-104">Este artigo descreve como conectar-se a um servidor usando aplicativos de gerenciamento e modelagem de dados como o SQL Server Management Studio (SSMS) ou SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="b22cf-104">This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="b22cf-105">Ou, com aplicativos de relatório de cliente como o Microsoft Excel, Power BI Desktop ou aplicativos personalizados.</span><span class="sxs-lookup"><span data-stu-id="b22cf-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="b22cf-106">Conexões ao Azure Analysis Services usam HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b22cf-106">Connections to Azure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="b22cf-107">Bibliotecas de cliente</span><span class="sxs-lookup"><span data-stu-id="b22cf-107">Client libraries</span></span>
[<span data-ttu-id="b22cf-108">Obter as bibliotecas de Cliente mais recentes</span><span class="sxs-lookup"><span data-stu-id="b22cf-108">Get the latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="b22cf-109">Todas as conexões a um servidor, independentemente do tipo, exigem bibliotecas de cliente OLEDB, ADOMD.NET e AMO atualizadas para a conexão e interface com um servidor do Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b22cf-109">All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server.</span></span> <span data-ttu-id="b22cf-110">Para SSMS, SSDT, Excel 2016 e Power BI, as bibliotecas de cliente mais recentes são instaladas ou atualizadas com lançamentos mensais.</span><span class="sxs-lookup"><span data-stu-id="b22cf-110">For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="b22cf-111">No entanto, em alguns casos, é possível que um aplicativo não tenha a mais recente.</span><span class="sxs-lookup"><span data-stu-id="b22cf-111">However, in some cases, it's possible an application may not have the latest.</span></span> <span data-ttu-id="b22cf-112">Por exemplo, quando políticas atrasam atualizações ou, as atualizações do Office 365 estão no Canal Adiado.</span><span class="sxs-lookup"><span data-stu-id="b22cf-112">For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="b22cf-113">Nome do servidor</span><span class="sxs-lookup"><span data-stu-id="b22cf-113">Server name</span></span>

<span data-ttu-id="b22cf-114">Quando você cria um servidor do Azure Analysis Services, é necessário especificar um nome exclusivo e a região na qual o servidor será criado.</span><span class="sxs-lookup"><span data-stu-id="b22cf-114">When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created.</span></span> <span data-ttu-id="b22cf-115">Ao especificar o nome do servidor em uma conexão, o esquema de nomenclatura do servidor será:</span><span class="sxs-lookup"><span data-stu-id="b22cf-115">When specifying the server name in a connection, the server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="b22cf-116">Quando o protocolo for a cadeia de caracteres **asazure**, a região será o URI de onde o servidor foi criado (por exemplo, westus.asazure.windows.net) e servername será o nome do seu servidor exclusivo dentro da região.</span><span class="sxs-lookup"><span data-stu-id="b22cf-116">Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.</span></span>

### <a name="get-the-server-name"></a><span data-ttu-id="b22cf-117">Obter o nome do servidor</span><span class="sxs-lookup"><span data-stu-id="b22cf-117">Get the server name</span></span>
<span data-ttu-id="b22cf-118">No **Portal do Azure** > servidor > **Visão geral** > **Nome do servidor**, copie todo o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="b22cf-118">In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name.</span></span> <span data-ttu-id="b22cf-119">Se outros usuários em sua organização também forem se conectar a esse servidor, compartilhe o nome do servidor com eles.</span><span class="sxs-lookup"><span data-stu-id="b22cf-119">If other users in your organization are connecting to this server too, you can share this server name with them.</span></span> <span data-ttu-id="b22cf-120">Ao especificar um nome de servidor, todo o caminho deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="b22cf-120">When specifying a server name, the entire path must be used.</span></span>

![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="b22cf-122">Cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="b22cf-122">Connection string</span></span>

<span data-ttu-id="b22cf-123">Ao conectar-se ao Azure Analysis Services usando o Modelo de objeto de tabela, use os seguintes formatos de cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="b22cf-123">When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="b22cf-124">Autenticação integrada do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b22cf-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="b22cf-125">A autenticação integrada seleciona o cache de credencial do Azure Active Directory, se estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="b22cf-125">Integrated authentication picks up the Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="b22cf-126">Caso contrário, a janela de logon do Azure será exibida.</span><span class="sxs-lookup"><span data-stu-id="b22cf-126">If not, the Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="b22cf-127">Autenticação do Azure Active Directory com nome de usuário e senha</span><span class="sxs-lookup"><span data-stu-id="b22cf-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="b22cf-128">Autenticação do Windows (segurança integrada)</span><span class="sxs-lookup"><span data-stu-id="b22cf-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="b22cf-129">Use a conta do Windows executando o processo atual.</span><span class="sxs-lookup"><span data-stu-id="b22cf-129">Use the Windows account running the current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="b22cf-130">Conectar usando um arquivo .odc</span><span class="sxs-lookup"><span data-stu-id="b22cf-130">Connect using an .odc file</span></span>
<span data-ttu-id="b22cf-131">Com versões mais antigas do Excel, os usuários podem se conectar a um servidor do Azure Analysis Service usando um arquivo Office Data Connectionn (.odc).</span><span class="sxs-lookup"><span data-stu-id="b22cf-131">With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="b22cf-132">Para obter mais informações, consulte [Criar um arquivo Office Data Connection (.odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="b22cf-132">To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b22cf-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b22cf-133">Next steps</span></span>
<span data-ttu-id="b22cf-134">[Conectar com Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="b22cf-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="b22cf-135">[Conectar com Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="b22cf-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="b22cf-136">Gerenciar seu serviço</span><span class="sxs-lookup"><span data-stu-id="b22cf-136">Manage your server</span></span>](analysis-services-manage.md)   

