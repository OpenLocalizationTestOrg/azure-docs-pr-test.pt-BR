---
title: Habilitar TDE (Transparent Data Encryption) para Stretch Database - Azure | Microsoft Docs
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
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="aa7cb-103">Habilitar TDE (Transparent Data Encryption) para Stretch Database no Azure</span><span class="sxs-lookup"><span data-stu-id="aa7cb-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa7cb-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aa7cb-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="aa7cb-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="aa7cb-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="aa7cb-106">O TDE (Transparent Data Encryption) ajuda a proteger contra ameaças de atividades mal-intencionadas por meio da execução de criptografia e descriptografia em tempo real do banco de dados, de backups associados e de arquivos de log de transações em repouso, sem exigir mudanças no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aa7cb-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="aa7cb-107">A TDE criptografa o armazenamento de um banco de dados inteiro usando uma chave simétrica chamada de chave de criptografia de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="aa7cb-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="aa7cb-108">A chave de criptografia do banco de dados está protegida por um certificado do servidor interno.</span><span class="sxs-lookup"><span data-stu-id="aa7cb-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="aa7cb-109">O certificado do servidor interno é exclusivo para cada servidor do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa7cb-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="aa7cb-110">A Microsoft alterna automaticamente esses certificados pelo menos a cada 90 dias.</span><span class="sxs-lookup"><span data-stu-id="aa7cb-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="aa7cb-111">Para obter uma descrição geral da TDE, consulte [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="aa7cb-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="aa7cb-112">Habilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="aa7cb-112">Enabling Encryption</span></span>
<span data-ttu-id="aa7cb-113">Para habilitar a TDE para um banco de dados do Azure que armazena os dados migrados de um banco de dados do SQL Server habilitado para ampliação, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aa7cb-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="aa7cb-114">Abra o banco de dados no [Portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="aa7cb-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="aa7cb-115">Na folha do banco de dados, clique no botão **Configurações**</span><span class="sxs-lookup"><span data-stu-id="aa7cb-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="aa7cb-116">Selecione a opção **Transparent Data Encryption**![][1]</span><span class="sxs-lookup"><span data-stu-id="aa7cb-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="aa7cb-117">Selecione a configuração **Ativar** e, em seguida, selecione **Salvar**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="aa7cb-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="aa7cb-118">Desabilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="aa7cb-118">Disabling Encryption</span></span>
<span data-ttu-id="aa7cb-119">Para desabilitar a TDE para um banco de dados do Azure que armazena os dados migrados de um banco de dados do SQL Server habilitado para ampliação, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aa7cb-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="aa7cb-120">Abra o banco de dados no [Portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="aa7cb-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="aa7cb-121">Na folha do banco de dados, clique no botão **Configurações**</span><span class="sxs-lookup"><span data-stu-id="aa7cb-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="aa7cb-122">Selecione a opção **Transparent Data Encryption**</span><span class="sxs-lookup"><span data-stu-id="aa7cb-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="aa7cb-123">Selecione a configuração **Desativar** e, em seguida, selecione **Salvar**</span><span class="sxs-lookup"><span data-stu-id="aa7cb-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
<span data-ttu-id="aa7cb-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="aa7cb-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
