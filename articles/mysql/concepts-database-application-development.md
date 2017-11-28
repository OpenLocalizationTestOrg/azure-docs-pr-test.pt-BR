---
title: "Visão geral de desenvolvimento de aplicativo aaaDatabase banco de dados do Azure para MySQL | Microsoft Docs"
description: "Apresenta considerações de design que um desenvolvedor deve seguir ao escrever aplicativos código tooconnect tooAzure banco de dados para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="ddfec-103">Visão geral de desenvolvimento de aplicativo para o Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="ddfec-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="ddfec-104">Este artigo aborda considerações de design que um desenvolvedor deve seguir ao escrever aplicativos código tooconnect tooAzure banco de dados para MySQL</span><span class="sxs-lookup"><span data-stu-id="ddfec-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="ddfec-105">Para um tutorial mostrando você como toocreate um servidor, criar um firewall baseado em servidor, exibir propriedades de servidor, cria banco de dados, se conectar e consulta usando o workbench e mysql.exe, consulte [criar seu primeiro banco de dados MySQL do Azure](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ddfec-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="ddfec-106">Linguagem e plataforma</span><span class="sxs-lookup"><span data-stu-id="ddfec-106">Language and platform</span></span>
<span data-ttu-id="ddfec-107">Há exemplos de código disponíveis para uma variedade de plataformas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="ddfec-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="ddfec-108">Você pode encontrar links toohello exemplos de código em: [bibliotecas de conectividade usados tooconnect tooAzure banco de dados para MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ddfec-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="ddfec-109">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="ddfec-109">Tools</span></span>
<span data-ttu-id="ddfec-110">Banco de dados do Azure para MySQL usa a versão de comunidade MySQL hello, compatível com as ferramentas de gerenciamento comuns MySQL como utilitários Workbench ou MySQL como mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)e outros.</span><span class="sxs-lookup"><span data-stu-id="ddfec-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="ddfec-111">Você também pode usar o hello portal do Azure, CLI do Azure e toointeract de APIs REST com o serviço de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddfec-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="ddfec-112">Limitações de recursos</span><span class="sxs-lookup"><span data-stu-id="ddfec-112">Resource limitations</span></span>
<span data-ttu-id="ddfec-113">Banco de dados MySQL Azure gerencia Olá recursos disponíveis tooa server usando dois mecanismos diferentes:</span><span class="sxs-lookup"><span data-stu-id="ddfec-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="ddfec-114">Governança de recursos</span><span class="sxs-lookup"><span data-stu-id="ddfec-114">Resources Governance</span></span> 
- <span data-ttu-id="ddfec-115">Imposição de limites.</span><span class="sxs-lookup"><span data-stu-id="ddfec-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="ddfec-116">Segurança</span><span class="sxs-lookup"><span data-stu-id="ddfec-116">Security</span></span>
<span data-ttu-id="ddfec-117">O Banco de Dados MySQL do Azure fornece recursos para limitar o acesso, proteger os dados, configurar usuários e funções e monitorar atividades em um Banco de Dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="ddfec-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="ddfec-118">Autenticação</span><span class="sxs-lookup"><span data-stu-id="ddfec-118">Authentication</span></span>
<span data-ttu-id="ddfec-119">O Banco de Dados MySQL do Azure oferece suporte à autenticação de usuários e logons do servidor.</span><span class="sxs-lookup"><span data-stu-id="ddfec-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="ddfec-120">Resiliência</span><span class="sxs-lookup"><span data-stu-id="ddfec-120">Resiliency</span></span>
<span data-ttu-id="ddfec-121">Quando ocorre um erro temporário durante a conexão tooMySQL banco de dados, seu código deverá repetir a chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddfec-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="ddfec-122">Recomendamos o uso de lógica de repetição Olá a lógica, para que não sobrecarregue Olá banco de dados SQL com vários clientes simultaneamente repetir.</span><span class="sxs-lookup"><span data-stu-id="ddfec-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="ddfec-123">Exemplos de código: para exemplos de código que ilustram a lógica de repetição, consulte exemplos para o idioma de saudação de sua preferência em: [bibliotecas de conectividade usados tooconnect tooAzure banco de dados para MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ddfec-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="ddfec-124">Gerenciando conexões</span><span class="sxs-lookup"><span data-stu-id="ddfec-124">Managing Connections</span></span>
<span data-ttu-id="ddfec-125">Conexões de banco de dados são um recurso limitado, portanto, é recomendável uso adequado de conexões ao acessar o banco de dados MySQL tooachieve melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="ddfec-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="ddfec-126">Banco de dados Access hello usando conexões persistentes ou pool de conexão.</span><span class="sxs-lookup"><span data-stu-id="ddfec-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="ddfec-127">Banco de dados Access hello usando conexão curto tempo de vida útil.</span><span class="sxs-lookup"><span data-stu-id="ddfec-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="ddfec-128">Use a lógica de repetição em seu aplicativo no ponto de saudação da tentativa de conexão hello, toocatch falhas devido a conexões tooconcurrent atingiu o máximo de saudação permitido.</span><span class="sxs-lookup"><span data-stu-id="ddfec-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="ddfec-129">Em Olá lógica de repetição, defina um pequeno atraso e aguarde um tempo aleatório antes de tentativas de conexão adicionais hello.</span><span class="sxs-lookup"><span data-stu-id="ddfec-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
