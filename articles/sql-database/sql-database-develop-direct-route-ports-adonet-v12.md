---
title: "Portas além de 1433 para o Banco de Dados SQL | Microsoft Docs"
description: "Às vezes, as conexões de cliente do ADO.NET para o Banco de Dados SQL do Azure ignoram o proxy e interagem diretamente com o banco de dados. Outras portas diferentes da 1433 se tornam importantes."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: d47ee8c794d1e231507dae6bb4aa88bf19ce6418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="74f19-104">Portas além da 1433 para ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="74f19-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="74f19-105">Este tópico descreve o comportamento de conexão do Banco de Dados SQL do Azure para clientes que usam ADO.NET 4.5 ou uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="74f19-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="74f19-106">Para obter informações sobre a arquitetura de conectividade, confira [Arquitetura de conectividade de Banco de Dados SQL do Azure](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="74f19-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="74f19-107">Fora versus dentro</span><span class="sxs-lookup"><span data-stu-id="74f19-107">Outside vs inside</span></span>
<span data-ttu-id="74f19-108">Para conexões com o Banco de Dados SQL do Azure, devemos perguntar primeiro se o programa cliente é executado *fora* ou *dentro* do limite de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="74f19-108">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="74f19-109">As subseções discutem dois cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="74f19-109">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="74f19-110">*Fora:* o cliente é executado em seu computador desktop</span><span class="sxs-lookup"><span data-stu-id="74f19-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="74f19-111">A porta 1433 é a única porta que deve estar aberta no computador desktop que hospeda o aplicativo cliente do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="74f19-111">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="74f19-112">*Dentro:* o cliente é executado no Azure</span><span class="sxs-lookup"><span data-stu-id="74f19-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="74f19-113">Quando o cliente é executado dentro do limite de nuvem do Azure, ele usa o que podemos chamar de *rota direta* para interagir com o servidor de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="74f19-113">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="74f19-114">Após o estabelecimento de uma conexão, as próximas interações entre o cliente e o banco de dados não envolvem um proxy de middleware.</span><span class="sxs-lookup"><span data-stu-id="74f19-114">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="74f19-115">Esta é a sequência:</span><span class="sxs-lookup"><span data-stu-id="74f19-115">The sequence is as follows:</span></span>

1. <span data-ttu-id="74f19-116">O ADO.NET 4.5 (ou posterior) inicia uma breve interação com a nuvem do Azure e recebe um número de porta identificado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="74f19-116">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="74f19-117">O número da porta identificado dinamicamente está no intervalo de 11000-11999 ou 14000-14999.</span><span class="sxs-lookup"><span data-stu-id="74f19-117">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="74f19-118">O ADO.NET conecta-se ao servidor de Banco de Dados SQL diretamente, sem um middleware entre os dois.</span><span class="sxs-lookup"><span data-stu-id="74f19-118">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="74f19-119">As consultas são enviadas diretamente ao banco de dados, e os resultados são retornados diretamente ao cliente.</span><span class="sxs-lookup"><span data-stu-id="74f19-119">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="74f19-120">Verifique se os intervalos de portas de 11000-11999 e 14000-14999 no computador cliente do Azure estão disponíveis para interações de cliente ADO.NET 4.5 com o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="74f19-120">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="74f19-121">Em particular, as portas no intervalo devem estar livres de outros bloqueadores de saída.</span><span class="sxs-lookup"><span data-stu-id="74f19-121">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="74f19-122">Em sua VM do Azure, o **Firewall do Windows com Segurança Avançada** controla as configurações de porta.</span><span class="sxs-lookup"><span data-stu-id="74f19-122">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="74f19-123">Você pode usar a [interface de usuário do firewall](http://msdn.microsoft.com/library/cc646023.aspx) a fim de adicionar uma regra para a qual você especifica o protocolo **TCP** junto com um intervalo de portas com a sintaxe **11000 a 11999**.</span><span class="sxs-lookup"><span data-stu-id="74f19-123">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="74f19-124">Esclarecimentos da versão</span><span class="sxs-lookup"><span data-stu-id="74f19-124">Version clarifications</span></span>
<span data-ttu-id="74f19-125">Esta seção explica os identificadores que se referem a versões do produto.</span><span class="sxs-lookup"><span data-stu-id="74f19-125">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="74f19-126">Ela também lista alguns emparelhamentos de versões entre produtos.</span><span class="sxs-lookup"><span data-stu-id="74f19-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="74f19-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="74f19-127">ADO.NET</span></span>
* <span data-ttu-id="74f19-128">O ADO.NET 4.0 dá suporte ao protocolo TDS 7.3, mas não ao 7.4.</span><span class="sxs-lookup"><span data-stu-id="74f19-128">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="74f19-129">O ADO.NET 4.5 e posterior dá suporte ao protocolo TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="74f19-129">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="74f19-130">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="74f19-130">Related links</span></span>
* <span data-ttu-id="74f19-131">O ADO.NET 4.6 foi lançado em 20 de julho de 2015.</span><span class="sxs-lookup"><span data-stu-id="74f19-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="74f19-132">Um comunicado do blog da equipe do .NET está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="74f19-132">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="74f19-133">O ADO.NET 4.5 foi lançado em 15 de agosto de 2012.</span><span class="sxs-lookup"><span data-stu-id="74f19-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="74f19-134">Um comunicado do blog da equipe do .NET está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="74f19-134">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="74f19-135">Uma postagem no blog sobre o ADO.NET 4.5.1 está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="74f19-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="74f19-136">Lista de versões do protocolo TDS</span><span class="sxs-lookup"><span data-stu-id="74f19-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="74f19-137">Visão geral do desenvolvimento de Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="74f19-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="74f19-138">Firewall do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="74f19-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="74f19-139">Como definir as configurações de firewall no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="74f19-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

