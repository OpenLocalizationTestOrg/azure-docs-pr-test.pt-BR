---
title: "Visão geral de desenvolvimento de aplicativo de banco de dados para o Banco de Dados do Azure para MySQL | Microsoft Docs"
description: "Apresenta considerações de design que um desenvolvedor deve seguir ao escrever o código de um aplicativo para se conectar ao Banco de Dados do Azure para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 350dd775e172120d806d1193877a34d94f4d3f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="8b583-103">Visão geral de desenvolvimento de aplicativo para o Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="8b583-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="8b583-104">Este artigo discute considerações de design que um desenvolvedor deve seguir ao escrever o código de um aplicativo para se conectar ao Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="8b583-104">This article discusses design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="8b583-105">Para ver um tutorial que mostra como criar um servidor, criar um firewall baseado em servidor, exibir propriedades do servidor, criar um banco de dados, conectar e consultar usando o Workbench e mysql.exe, confira [Criar seu primeiro banco de dados MySQL do Azure](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8b583-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="8b583-106">Linguagem e plataforma</span><span class="sxs-lookup"><span data-stu-id="8b583-106">Language and platform</span></span>
<span data-ttu-id="8b583-107">Há exemplos de código disponíveis para uma variedade de plataformas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="8b583-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="8b583-108">Encontre links para exemplos de código em: [Bibliotecas de conectividade usadas para se conectar ao Banco de Dados do Azure para MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="8b583-108">You can find links to the code samples at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="8b583-109">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="8b583-109">Tools</span></span>
<span data-ttu-id="8b583-110">O Banco de Dados do Azure para MySQL usa a versão de comunidade do MySQL, que é compatível com ferramentas de gerenciamento comuns do MySQL, como o Workbench, ou utilitários do MySQL, como o mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql) e outros.</span><span class="sxs-lookup"><span data-stu-id="8b583-110">Azure Database for MySQL uses the MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="8b583-111">Você também pode usar o Portal do Azure, a CLI do Azure e APIs REST para interagir com o serviço de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8b583-111">You can also use the Azure portal, Azure CLI, and REST APIs to interact with the database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="8b583-112">Limitações de recursos</span><span class="sxs-lookup"><span data-stu-id="8b583-112">Resource limitations</span></span>
<span data-ttu-id="8b583-113">O Banco de Dados MySQL do Azure gerencia os recursos disponíveis para um servidor usando dois mecanismos diferentes:</span><span class="sxs-lookup"><span data-stu-id="8b583-113">Azure MySQL Database manages the resources available to a server using two different mechanisms:</span></span> 
- <span data-ttu-id="8b583-114">Governança de recursos</span><span class="sxs-lookup"><span data-stu-id="8b583-114">Resources Governance</span></span> 
- <span data-ttu-id="8b583-115">Imposição de limites.</span><span class="sxs-lookup"><span data-stu-id="8b583-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="8b583-116">Segurança</span><span class="sxs-lookup"><span data-stu-id="8b583-116">Security</span></span>
<span data-ttu-id="8b583-117">O Banco de Dados MySQL do Azure fornece recursos para limitar o acesso, proteger os dados, configurar usuários e funções e monitorar atividades em um Banco de Dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b583-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="8b583-118">Autenticação</span><span class="sxs-lookup"><span data-stu-id="8b583-118">Authentication</span></span>
<span data-ttu-id="8b583-119">O Banco de Dados MySQL do Azure oferece suporte à autenticação de usuários e logons do servidor.</span><span class="sxs-lookup"><span data-stu-id="8b583-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="8b583-120">Resiliência</span><span class="sxs-lookup"><span data-stu-id="8b583-120">Resiliency</span></span>
<span data-ttu-id="8b583-121">Quando ocorre um erro transitório ao se conectar ao Banco de Dados MySQL, seu código deverá repetir a chamada.</span><span class="sxs-lookup"><span data-stu-id="8b583-121">When a transient error occurs while connecting to MySQL Database, your code should retry the call.</span></span> <span data-ttu-id="8b583-122">Recomendamos que a lógica de repetição use a lógica de retirada, de modo que ela não sobrecarregue o Banco de Dados SQL com vários clientes realizando novas tentativas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="8b583-122">We recommend the retry logic use back off logic, so that it does not overwhelm the SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="8b583-123">Exemplos de código: para obter exemplos de código que ilustram a lógica de repetição, confira os exemplos para o idioma de sua preferência em: [Bibliotecas de conexão usadas para se conectar ao Banco de Dados do Azure para MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="8b583-123">Code samples: For code samples that illustrate retry logic, see samples for the language of your choice at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="8b583-124">Gerenciando conexões</span><span class="sxs-lookup"><span data-stu-id="8b583-124">Managing Connections</span></span>
<span data-ttu-id="8b583-125">Conexões de banco de dados são um recurso limitado, portanto, recomendamos o uso adequado de conexões ao acessar o Banco de Dados MySQL para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="8b583-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database to achieve better performance.</span></span>
- <span data-ttu-id="8b583-126">Acesse o banco de dados usando o pooling de conexão ou conexões persistentes.</span><span class="sxs-lookup"><span data-stu-id="8b583-126">Access the database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="8b583-127">Acesse o banco de dados usando uma conexão de curta duração.</span><span class="sxs-lookup"><span data-stu-id="8b583-127">Access the database by using short connection life span.</span></span> 
- <span data-ttu-id="8b583-128">Use a lógica de repetição em seu aplicativo no ponto da tentativa de conexão, para detectar falhas causadas pelas conexões simultâneas atingirem o máximo permitido.</span><span class="sxs-lookup"><span data-stu-id="8b583-128">Use retry logic in your application at the point of the connection attempt, to catch failures due to concurrent connections have reached the maximum allowed.</span></span> <span data-ttu-id="8b583-129">Na lógica de repetição, defina um pequeno atraso e aguarde um período aleatório antes das tentativas de conexão adicionais.</span><span class="sxs-lookup"><span data-stu-id="8b583-129">In the retry logic, set a short delay, and then wait for a random time before the additional connection attempts.</span></span>