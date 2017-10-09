---
title: aaaEnable criptografia transparente de dados para o Stretch Database - Azure | Microsoft Docs
description: Habilitar TDE (Transparent Data Encryption) para SQL Server Stretch Database no Azure
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="fd5a5-103">Habilitar TDE (Transparent Data Encryption) para Stretch Database no Azure</span><span class="sxs-lookup"><span data-stu-id="fd5a5-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd5a5-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fd5a5-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="fd5a5-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="fd5a5-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="fd5a5-106">Criptografia de dados transparente (TDE) ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia de banco de dados hello, backups associados e arquivos de log de transações em repouso sem exigir alterações toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd5a5-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="fd5a5-107">Ela criptografa o armazenamento de saudação de um banco de dados inteiro usando uma chave de criptografia de banco de dados de saudação de chamada de chave simétrica.</span><span class="sxs-lookup"><span data-stu-id="fd5a5-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="fd5a5-108">chave de criptografia de banco de dados de saudação é protegida por um certificado de servidor interno.</span><span class="sxs-lookup"><span data-stu-id="fd5a5-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="fd5a5-109">certificado de saudação do servidor interno é exclusivo para cada servidor do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd5a5-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="fd5a5-110">A Microsoft alterna automaticamente esses certificados pelo menos a cada 90 dias.</span><span class="sxs-lookup"><span data-stu-id="fd5a5-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="fd5a5-111">Para obter uma descrição geral da TDE, consulte [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="fd5a5-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="fd5a5-112">Habilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="fd5a5-112">Enabling Encryption</span></span>
<span data-ttu-id="fd5a5-113">tooenable TDE para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd5a5-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="fd5a5-114">Banco de dados aberto Olá no hello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="fd5a5-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="fd5a5-115">Na folha de banco de dados de saudação, clique em Olá **configurações** botão</span><span class="sxs-lookup"><span data-stu-id="fd5a5-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="fd5a5-116">Selecione Olá **criptografia transparente de dados** opção![][1]</span><span class="sxs-lookup"><span data-stu-id="fd5a5-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="fd5a5-117">Selecione Olá **na** configuração e, em seguida, selecione **salvar**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="fd5a5-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="fd5a5-118">Desabilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="fd5a5-118">Disabling Encryption</span></span>
<span data-ttu-id="fd5a5-119">toodisable TDE para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd5a5-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="fd5a5-120">Banco de dados aberto Olá no hello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="fd5a5-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="fd5a5-121">Na folha de banco de dados de saudação, clique em Olá **configurações** botão</span><span class="sxs-lookup"><span data-stu-id="fd5a5-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="fd5a5-122">Selecione Olá **criptografia transparente de dados** opção</span><span class="sxs-lookup"><span data-stu-id="fd5a5-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="fd5a5-123">Selecione Olá **Off** configuração e, em seguida, selecione **salvar**</span><span class="sxs-lookup"><span data-stu-id="fd5a5-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
