---
title: "aaaPorts além 1433 para o banco de dados SQL | Microsoft Docs"
description: "Conexões de cliente do ADO.NET tooAzure banco de dados SQL, às vezes, ignoram proxy hello e interagem diretamente com o banco de dados de saudação. Outras portas diferentes da 1433 se tornam importantes."
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
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="9cdc0-104">Portas além da 1433 para ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="9cdc0-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="9cdc0-105">Este tópico descreve o comportamento de conexão de banco de dados do Azure SQL Olá para clientes que usam o ADO.NET 4.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9cdc0-106">Para obter informações sobre a arquitetura de conectividade, confira [Arquitetura de conectividade de Banco de Dados SQL do Azure](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="9cdc0-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="9cdc0-107">Fora versus dentro</span><span class="sxs-lookup"><span data-stu-id="9cdc0-107">Outside vs inside</span></span>
<span data-ttu-id="9cdc0-108">Para conexões tooAzure banco de dados SQL, deve primeiro pedimos que se seu programa cliente executa *fora* ou *dentro* limites de nuvem do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="9cdc0-109">subseções Olá discutem dois cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="9cdc0-110">*Fora:* o cliente é executado em seu computador desktop</span><span class="sxs-lookup"><span data-stu-id="9cdc0-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="9cdc0-111">A porta 1433 é Olá somente a porta que deve ser aberta no computador desktop que hospede o aplicativo de cliente do banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="9cdc0-112">*Dentro:* o cliente é executado no Azure</span><span class="sxs-lookup"><span data-stu-id="9cdc0-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="9cdc0-113">Quando o cliente é executado dentro do limite de nuvem do Azure hello, ele usa o que podemos chamar um *direta de rota* toointeract com o servidor de banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="9cdc0-114">Depois que uma conexão é estabelecida, outras interações entre o cliente hello e banco de dados não envolvem nenhum proxy de middleware.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="9cdc0-115">sequência de saudação é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9cdc0-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="9cdc0-116">ADO.NET 4.5 (ou posterior) inicia uma breve interação com hello nuvem do Azure e recebe um número de porta dinamicamente identificado.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="9cdc0-117">número da porta Olá dinamicamente identificado está no intervalo de saudação de 11.000 a 11.999 ou 14.000 a 14.999.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="9cdc0-118">ADO.NET, em seguida, conecta-se servidor de banco de dados SQL toohello diretamente, com nenhum middleware entre.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="9cdc0-119">As consultas são enviadas diretamente toohello banco de dados e os resultados são retornados diretamente toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="9cdc0-120">Verifique se essa porta Olá intervalos de 11.000 a 11.999 e 14.000 a 14.999 do computador cliente do Azure ficam disponíveis para ADO.NET 4.5 interações de cliente com o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="9cdc0-121">Em particular, as portas no intervalo de saudação devem estar livres de quaisquer outros bloqueadores de saída.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="9cdc0-122">Na sua VM do Azure, Olá **Firewall do Windows com segurança avançada** controles Olá configurações de porta.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="9cdc0-123">Você pode usar o hello [interface de usuário do firewall](http://msdn.microsoft.com/library/cc646023.aspx) tooadd uma regra para que você especificar Olá **TCP** como o protocolo junto com um intervalo de portas com sintaxe Olá **11.000 a 11.999**.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="9cdc0-124">Esclarecimentos da versão</span><span class="sxs-lookup"><span data-stu-id="9cdc0-124">Version clarifications</span></span>
<span data-ttu-id="9cdc0-125">Esta seção explica monikers Olá que fazem referência tooproduct versões.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="9cdc0-126">Ela também lista alguns emparelhamentos de versões entre produtos.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="9cdc0-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="9cdc0-127">ADO.NET</span></span>
* <span data-ttu-id="9cdc0-128">ADO.NET 4.0 oferece suporte a protocolo de saudação 7.3 TDS, mas não 7.4.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="9cdc0-129">ADO.NET 4.5 e posterior oferece suporte ao protocolo de saudação TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="9cdc0-130">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="9cdc0-130">Related links</span></span>
* <span data-ttu-id="9cdc0-131">O ADO.NET 4.6 foi lançado em 20 de julho de 2015.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="9cdc0-132">Um comunicado do blog da equipe do .NET hello está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cdc0-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="9cdc0-133">O ADO.NET 4.5 foi lançado em 15 de agosto de 2012.</span><span class="sxs-lookup"><span data-stu-id="9cdc0-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="9cdc0-134">Um comunicado do blog da equipe do .NET hello está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cdc0-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="9cdc0-135">Uma postagem no blog sobre o ADO.NET 4.5.1 está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cdc0-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="9cdc0-136">Lista de versões do protocolo TDS</span><span class="sxs-lookup"><span data-stu-id="9cdc0-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="9cdc0-137">Visão geral do desenvolvimento de Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="9cdc0-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="9cdc0-138">Firewall do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="9cdc0-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="9cdc0-139">Como definir as configurações de firewall no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="9cdc0-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

