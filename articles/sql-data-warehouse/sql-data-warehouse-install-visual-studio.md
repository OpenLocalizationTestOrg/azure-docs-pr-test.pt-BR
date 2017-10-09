---
title: aaaInstall Visual Studio e SSDT para SQL Data Warehouse | Microsoft Docs
description: Instalar o Visual Studio e o SSDT (Ferramentas de Desenvolvimento do SQL Server) para o SQL Data Warehouse do Azure
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="d2809-103">Instalar o Visual Studio e o SSDT para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d2809-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="d2809-104">toodevelop aplicativos para o SQL Data Warehouse, é recomendável usar a versão mais recente de saudação do Visual Studio com a versão mais recente de saudação do SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="d2809-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="d2809-105">Também há suporte para o Visual Studio 2013 Atualização 5 com SSDT a fim de permitir a compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="d2809-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="d2809-106">Usando o Visual Studio com o SSDT permitirá toouse Olá Pesquisador de objetos do SQL Server toovisually explorar as tabelas, exibições, procedimentos armazenados e muito mais objetos no SQL Data Warehouse, bem como executar consultas.</span><span class="sxs-lookup"><span data-stu-id="d2809-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="d2809-107">O SQL Data Warehouse ainda não dá suporte aos Projetos do Banco de Dados do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2809-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="d2809-108">Este recurso será adicionado em uma futura versão.</span><span class="sxs-lookup"><span data-stu-id="d2809-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="d2809-109">Etapa 1: instalar o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2809-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="d2809-110">Siga essas toodownload links e instalar o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2809-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="d2809-111">Se você já tiver o Visual Studio 2013 ou posterior instalado, você pode ignorar tooStep 2, instale o SSDT.</span><span class="sxs-lookup"><span data-stu-id="d2809-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="d2809-112">[Baixar o Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="d2809-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="d2809-113">Siga Olá [instalar o Visual Studio] [ Installing Visual Studio] guia no MSDN e escolha as configurações padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2809-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="d2809-114">Etapa 2: Instalar o SSDT</span><span class="sxs-lookup"><span data-stu-id="d2809-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="d2809-115">Basta marcar tooinstall SSDT para Visual Studio para uma atualização do SSDT de dentro do Visual Studio seguindo estas etapas.</span><span class="sxs-lookup"><span data-stu-id="d2809-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="d2809-116">No Visual Studio, clique em **Ferramentas** / **Extensões e Atualizações…**</span><span class="sxs-lookup"><span data-stu-id="d2809-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="d2809-117"> / **Atualizações**</span><span class="sxs-lookup"><span data-stu-id="d2809-117"> / **Updates**</span></span>
2. <span data-ttu-id="d2809-118">Selecione **Atualizações do Produto**, em seguida, procure **Atualização do Microsoft SQL Server para as ferramentas do banco de dados**</span><span class="sxs-lookup"><span data-stu-id="d2809-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="d2809-119">Se uma atualização não for encontrada, você deve ter versão mais recente do hello instalada.</span><span class="sxs-lookup"><span data-stu-id="d2809-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="d2809-120">tooconfirm SSDT está instalado, clique em **ajuda** / **sobre o Microsoft Visual Studio** e procure por ferramentas de dados do SQL Server na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2809-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="d2809-121">versão mais recente de saudação do SSDT é 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="d2809-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="d2809-122">Se Olá opção tooinstall não está disponível no Visual Studio, como alternativa você pode visitar Olá [de Download do SSDT] [ SSDT Download] página toodownload e instalar o SSDT manualmente.</span><span class="sxs-lookup"><span data-stu-id="d2809-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2809-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2809-123">Next steps</span></span>
<span data-ttu-id="d2809-124">Agora que você tem a versão mais recente de saudação do SSDT, você está pronto muito[conectar] [ connect] tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d2809-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Baixar o Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
