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
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="5200a-103">Conectar-se o servidor de serviços de análise do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="5200a-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="5200a-104">Este artigo descreve tooa conectando o servidor usando a modelagem de dados e aplicativos de gerenciamento como o SQL Server Management Studio (SSMS) ou SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="5200a-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="5200a-105">Ou, com aplicativos de relatório de cliente como o Microsoft Excel, Power BI Desktop ou aplicativos personalizados.</span><span class="sxs-lookup"><span data-stu-id="5200a-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="5200a-106">Conexões tooAzure Analysis Services usar HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5200a-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="5200a-107">Bibliotecas de cliente</span><span class="sxs-lookup"><span data-stu-id="5200a-107">Client libraries</span></span>
[<span data-ttu-id="5200a-108">Obter Olá bibliotecas de cliente mais recentes</span><span class="sxs-lookup"><span data-stu-id="5200a-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="5200a-109">Todas as conexões tooa server, independentemente do tipo, requer atualizado AMO, ADOMD.NET e OLEDB bibliotecas tooconnect tooand interface de cliente com um servidor do Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5200a-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="5200a-110">Para SSMS, o SSDT, o Excel 2016 e o Power BI, bibliotecas de cliente mais recentes Olá são instaladas ou atualizadas com as versões mensais.</span><span class="sxs-lookup"><span data-stu-id="5200a-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="5200a-111">No entanto, em alguns casos, é possível que um aplicativo pode não ter hello mais recente.</span><span class="sxs-lookup"><span data-stu-id="5200a-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="5200a-112">Por exemplo, quando atualizações de atraso de políticas ou atualizações do Office 365 estão em Olá canal adiado.</span><span class="sxs-lookup"><span data-stu-id="5200a-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="5200a-113">Nome do servidor</span><span class="sxs-lookup"><span data-stu-id="5200a-113">Server name</span></span>

<span data-ttu-id="5200a-114">Quando você cria um servidor do Analysis Services no Azure, você pode especificar uma região de nome e hello exclusiva, onde o servidor de saudação é toobe criado.</span><span class="sxs-lookup"><span data-stu-id="5200a-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="5200a-115">Ao especificar o nome do servidor de saudação em uma conexão, o esquema de nomenclatura de servidor de saudação é:</span><span class="sxs-lookup"><span data-stu-id="5200a-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="5200a-116">Em que o protocolo é cadeia de caracteres **asazure**, região é hello Uri em que o servidor de saudação foi criado (por exemplo, westus.asazure.windows.net) e servername é o nome de saudação do servidor exclusivo dentro da região de saudação.</span><span class="sxs-lookup"><span data-stu-id="5200a-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="5200a-117">Obter o nome do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="5200a-117">Get hello server name</span></span>
<span data-ttu-id="5200a-118">Em **portal do Azure** > servidor > **visão geral** > **nome do servidor**, nome de todo o servidor de saudação de cópia.</span><span class="sxs-lookup"><span data-stu-id="5200a-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="5200a-119">Se outros usuários na sua organização estiver se conectando a servidor toothis demais, você pode compartilhar este nome de servidor com eles.</span><span class="sxs-lookup"><span data-stu-id="5200a-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="5200a-120">Ao especificar um nome de servidor, o caminho inteiro Olá deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="5200a-120">When specifying a server name, hello entire path must be used.</span></span>

![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="5200a-122">Cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="5200a-122">Connection string</span></span>

<span data-ttu-id="5200a-123">Ao conectar-se tooAzure Analysis Services usando Olá modelo de objeto Tabular, Olá use formatos de cadeia de caracteres de conexão a seguir:</span><span class="sxs-lookup"><span data-stu-id="5200a-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="5200a-124">Autenticação integrada do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5200a-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="5200a-125">A autenticação integrada pega Olá cache de credenciais do Active Directory do Azure se disponível.</span><span class="sxs-lookup"><span data-stu-id="5200a-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="5200a-126">Caso contrário, a janela de logon do Azure Olá é mostrada.</span><span class="sxs-lookup"><span data-stu-id="5200a-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="5200a-127">Autenticação do Azure Active Directory com nome de usuário e senha</span><span class="sxs-lookup"><span data-stu-id="5200a-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="5200a-128">Autenticação do Windows (segurança integrada)</span><span class="sxs-lookup"><span data-stu-id="5200a-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="5200a-129">Use conta do Windows hello executando o processo atual hello.</span><span class="sxs-lookup"><span data-stu-id="5200a-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="5200a-130">Conectar usando um arquivo .odc</span><span class="sxs-lookup"><span data-stu-id="5200a-130">Connect using an .odc file</span></span>
<span data-ttu-id="5200a-131">Com versões anteriores do Excel, usuários podem se conectar tooan servidor de serviços de análise do Azure usando um arquivo de Conexão de dados do Office (. odc).</span><span class="sxs-lookup"><span data-stu-id="5200a-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="5200a-132">mais, consulte toolearn [criar um arquivo de Conexão de dados do Office (. odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="5200a-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5200a-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5200a-133">Next steps</span></span>
<span data-ttu-id="5200a-134">[Conectar com Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="5200a-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="5200a-135">[Conectar com Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="5200a-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="5200a-136">Gerenciar seu serviço</span><span class="sxs-lookup"><span data-stu-id="5200a-136">Manage your server</span></span>](analysis-services-manage.md)   

