---
title: "Notas de versão do Catálogo de Dados do Azure | Microsoft Docs"
description: "Notas de versão do Catálogo de Dados do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: d3db9bee0558cac5fb4f5b8fb4ab67a35ce0f141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="11742-103">Notas de versão do Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="11742-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="11742-104">Notas da versão de 20 de novembro de 2015 do Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="11742-104">Notes for the November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="11742-105">Abrindo fontes no Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="11742-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="11742-106">Ao usar a opção "Abrir no Power BI Desktop" no portal do **Catálogo de Dados do Azure** , os usuários podem encontrar um de dois problemas no aplicativo Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="11742-106">When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:</span></span>

* <span data-ttu-id="11742-107">Será exibida uma caixa de diálogo com o título "Não é possível abrir o documento"</span><span class="sxs-lookup"><span data-stu-id="11742-107">A dialog box with the title "Unable to Open Document" is displayed</span></span>
* <span data-ttu-id="11742-108">O Power BI Desktop abre, mas o arquivo parece estar vazio</span><span class="sxs-lookup"><span data-stu-id="11742-108">The Power BI Desktop application opens, but the file appears to be empty</span></span>

<span data-ttu-id="11742-109">Para cada situação, o problema pode ser resolvido ao baixar e instalar a versão mais recente do Power BI Desktop em [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="11742-109">For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="11742-110">Notas da versão de 13 de novembro de 2015 do Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="11742-110">Notes for the November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-teradata"></a><span data-ttu-id="11742-111">Registrando e conectando ao Teradata</span><span class="sxs-lookup"><span data-stu-id="11742-111">Registering and connecting to Teradata</span></span>
<span data-ttu-id="11742-112">Ao se conectar a fontes de dados Teradata, os usuários devem ter instalado o driver ODBC correto do Teradata que coincida com o número de bits (32 bits ou 64 bits) do software que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="11742-112">When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

<span data-ttu-id="11742-113">A partir dessa data de lançamento do ADC, o [driver ODBC do Teradata para windows (versão 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) mais recente é compatível com o Office 2013, mas não com o Office 2016.</span><span class="sxs-lookup"><span data-stu-id="11742-113">As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="11742-114">Notas da versão de 13 de julho de 2015 do Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="11742-114">Notes for the July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-oracle-database"></a><span data-ttu-id="11742-115">Registrando e conectando-se ao Banco de Dados do Oracle</span><span class="sxs-lookup"><span data-stu-id="11742-115">Registering and connecting to Oracle Database</span></span>
<span data-ttu-id="11742-116">Ao conectar-se às fontes de dados do banco de dados Oracle, os usuários devem ter instalado os drivers corretos do Oracle que correspondem ao número de bits (32 bits ou 64 bits) do software que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="11742-116">When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

* <span data-ttu-id="11742-117">Ao registrar fontes de dados Oracle em um computador executando o Windows de 32 bits, os drivers do Oracle de 32 bits serão usados</span><span class="sxs-lookup"><span data-stu-id="11742-117">When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="11742-118">Ao registrar fontes de dados Oracle em um computador executando o Windows de 64 bits, os drivers do Oracle de 64 bits serão usados</span><span class="sxs-lookup"><span data-stu-id="11742-118">When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="11742-119">Ao conectar-se às fontes de dados Oracle usando o Excel em um computador executando a versão de 32 bits do Microsoft Office, inclusive no Windows de 64 bits, os drivers do Oracle de 32 bits serão usados</span><span class="sxs-lookup"><span data-stu-id="11742-119">When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="11742-120">Ao conectar-se às fontes de dados Oracle usando o Excel em um computador executando a versão de 64 bits do Microsoft Office, os drivers do Oracle de 64 bits serão usados</span><span class="sxs-lookup"><span data-stu-id="11742-120">When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a><span data-ttu-id="11742-121">Registro e conexão ao SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="11742-121">Registering and connecting to SQL Server Reporting Services</span></span>
<span data-ttu-id="11742-122">Atualmente, o suporte para as fontes de dados do SSRS (SQL Server Reporting Services) está limitado somente a servidores do Modo Nativo.</span><span class="sxs-lookup"><span data-stu-id="11742-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only.</span></span> <span data-ttu-id="11742-123">O suporte para o SSRS no modo SharePoint será adicionado em uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="11742-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="11742-124">Abrindo ativos de dados no Excel</span><span class="sxs-lookup"><span data-stu-id="11742-124">Opening data assets in Excel</span></span>
<span data-ttu-id="11742-125">Ao abrir os ativos de dados no Microsoft Excel, no portal do **Catálogo de Dados do Azure**, os usuários poderão ver uma caixa de diálogo **Aviso de Segurança do Microsoft Excel**.</span><span class="sxs-lookup"><span data-stu-id="11742-125">When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="11742-126">Esse é um comportamento padrão e esperado, e os usuários podem selecionar **Habilitar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="11742-126">This is standard, expected behavior, and users can select **Enable** to continue.</span></span>

<span data-ttu-id="11742-127">Para obter mais informações, veja [Habilitar ou desabilitar alertas de segurança sobre links e arquivos de sites suspeitos](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="11742-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="11742-128">Registro da fonte de dados e configuração de proxy e política</span><span class="sxs-lookup"><span data-stu-id="11742-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="11742-129">Os usuários podem encontrar uma situação em que podem acessar o portal do Catálogo de Dados do Azure, mas quando tentam fazer logon na ferramenta de registro da fonte de dados encontram uma mensagem de erro que impede o logon.</span><span class="sxs-lookup"><span data-stu-id="11742-129">Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="11742-130">Há duas causas possíveis para esse comportamento de problema:</span><span class="sxs-lookup"><span data-stu-id="11742-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="11742-131">**Causa 1: configuração dos Serviços de Federação do Active Directory** A ferramenta de registro de fonte de dados usa a Autenticação de formulários para validar logons de usuário no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="11742-131">**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="11742-132">Para um logon bem-sucedido, a autenticação de formulários deve ser habilitada na Política de Autenticação Global por um administrador do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="11742-132">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="11742-133">Em algumas situações, esse comportamento de erro pode ocorrer apenas quando o usuário está na rede da empresa, ou quando está se conectando de fora da rede da empresa.</span><span class="sxs-lookup"><span data-stu-id="11742-133">In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network.</span></span> <span data-ttu-id="11742-134">A Política de Autenticação Global permite que os métodos de autenticação sejam habilitados separadamente para conexões intranet e extranet.</span><span class="sxs-lookup"><span data-stu-id="11742-134">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="11742-135">Erros de logon poderão ocorrer se a autenticação de formulários não estiver habilitada para a rede por meio da qual o usuário está se conectando.</span><span class="sxs-lookup"><span data-stu-id="11742-135">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

<span data-ttu-id="11742-136">Para obter mais informações, consulte [Configurando políticas de autenticação](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="11742-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="11742-137">**Causa 2: configuração de proxy da rede** Se a rede corporativa usar um servidor proxy, a ferramenta de registro não poderá se conectar ao Active Directory do Azure por meio do proxy.</span><span class="sxs-lookup"><span data-stu-id="11742-137">**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy.</span></span> <span data-ttu-id="11742-138">Os usuários podem garantir a ferramenta de registro editando o arquivo de configuração da ferramenta, adicionando esta seção ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="11742-138">Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="11742-139">Para localizar o arquivo RegistrationTool.exe.config, inicie a ferramenta de registro e, em seguida, abra o utilitário Gerenciador de Tarefas do Windows.</span><span class="sxs-lookup"><span data-stu-id="11742-139">To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility.</span></span> <span data-ttu-id="11742-140">Na guia Detalhes do Gerenciador de tarefas, clique com o botão direito em RegistrationTool.exe e escolha Abrir local do arquivo no menu pop-up.</span><span class="sxs-lookup"><span data-stu-id="11742-140">On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.</span></span>
