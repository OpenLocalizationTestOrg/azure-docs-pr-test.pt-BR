---
title: aaaSSL conectividade de banco de dados do Azure para MySQL | Microsoft Docs
description: "Informações para configurar o banco de dados do Azure para aplicativos associados tooproperly e MySQL usar conexões SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="b9b03-103">Conectividade SSL no Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="b9b03-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="b9b03-104">Banco de dados do Azure para MySQL dá suporte à conexão seus aplicativos de tooclient do servidor de banco de dados usando o protocolo (SSL).</span><span class="sxs-lookup"><span data-stu-id="b9b03-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="b9b03-105">Impor conexões SSL entre o servidor de banco de dados e aplicativos cliente ajuda a proteger contra ataques "man no meio hello" criptografando o fluxo de dados de saudação entre o servidor de saudação e seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b9b03-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="b9b03-106">Configurações padrão</span><span class="sxs-lookup"><span data-stu-id="b9b03-106">Default settings</span></span>
<span data-ttu-id="b9b03-107">Por padrão, o serviço de banco de dados de saudação deve ser toorequire configurado as conexões SSL ao conectar-se tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="b9b03-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="b9b03-108">É recomendável evitar que a opção de SSL Olá sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="b9b03-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="b9b03-109">Ao provisionar um novo banco de dados do Azure para o MySQL server por meio de saudação portal do Azure e a CLI, imposição de conexões SSL está habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="b9b03-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="b9b03-110">Da mesma forma, cadeias de caracteres de conexão previamente definidas nas configurações de "Cadeias de caracteres de Conexão" hello em seu servidor no portal do Azure de saudação incluem parâmetros de saudação necessária para comuns idiomas tooconnect tooyour servidor usando SSL.</span><span class="sxs-lookup"><span data-stu-id="b9b03-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="b9b03-111">Hello parâmetro SSL varia de acordo com o conector hello, por exemplo "ssl = true" ou "sslmode = exigem" ou "sslmode = necessária" e outras variações.</span><span class="sxs-lookup"><span data-stu-id="b9b03-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="b9b03-112">toolearn como tooenable ou desabilitar conexão SSL durante o desenvolvimento de aplicativo, consulte muito[como tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b9b03-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9b03-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9b03-113">Next steps</span></span>
[<span data-ttu-id="b9b03-114">Bibliotecas de conexão para o Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="b9b03-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
