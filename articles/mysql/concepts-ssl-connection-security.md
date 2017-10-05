---
title: Conectividade SSL para Banco de Dados do Azure para MySQL | Microsoft Docs
description: "Informações para configurar o Banco de Dados do Azure para MySQL e aplicativos associados a fim de usar as conexões SSL adequadamente"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b03b3a2dbfad92cc0cfa84777b38ddff90452cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="ec8ba-103">Conectividade SSL no Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="ec8ba-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="ec8ba-104">O Banco de Dados do Azure para MySQL dá suporte à conexão de seu servidor de banco de dados com aplicativos cliente usando o protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="ec8ba-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="ec8ba-105">Impor conexões SSL entre seu servidor de banco de dados e os aplicativos cliente ajuda a proteger contra ataques de "intermediários" criptografando o fluxo de dados entre o servidor e seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ec8ba-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="ec8ba-106">Configurações padrão</span><span class="sxs-lookup"><span data-stu-id="ec8ba-106">Default settings</span></span>
<span data-ttu-id="ec8ba-107">Por padrão, o serviço de banco de dados deve ser configurado para exigir conexões SSL ao se conectar ao MySQL.</span><span class="sxs-lookup"><span data-stu-id="ec8ba-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="ec8ba-108">Recomendamos evitar desabilitar a opção SSL sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="ec8ba-108">It is recommended avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="ec8ba-109">Ao provisionar um novo servidor de Banco de Dados do Azure para MySQL por meio do Portal e CLI do Azure, a imposição de conexões SSL está habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="ec8ba-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="ec8ba-110">Da mesma forma, cadeias de conexão previamente definidas nas configurações de "Cadeias de Conexão" em seu servidor no Portal do Azure incluem os parâmetros necessários para linguagens comuns a fim de se conectar ao seu servidor de banco de dados usando SSL.</span><span class="sxs-lookup"><span data-stu-id="ec8ba-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="ec8ba-111">O parâmetro SSL varia de acordo com o conector, por exemplo "ssl=true" ou "sslmode=require" ou "sslmode=required" e outras variações.</span><span class="sxs-lookup"><span data-stu-id="ec8ba-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="ec8ba-112">Para saber como habilitar ou desabilitar a conexão SSL durante o desenvolvimento de aplicativos, confira [Como configurar o SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ec8ba-112">To learn how to enable or disable SSL connection when developing application, please refer to [How to configure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec8ba-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ec8ba-113">Next steps</span></span>
[<span data-ttu-id="ec8ba-114">Bibliotecas de conexão para o Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="ec8ba-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
