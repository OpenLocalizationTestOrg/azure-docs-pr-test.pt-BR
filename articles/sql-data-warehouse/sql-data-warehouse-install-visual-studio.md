---
title: Instalar o Visual Studio e o SSDT para o SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: f7023b78c241a7bc8014276cd0bfa455165b42cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="5190a-103">Instalar o Visual Studio e o SSDT para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5190a-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="5190a-104">Para desenvolver aplicativos para o SQL Data Warehouse, recomendamos o uso da versão mais recente do Visual Studio com a versão mais recente do SSDT (SQL Server Data Tools).</span><span class="sxs-lookup"><span data-stu-id="5190a-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="5190a-105">Também há suporte para o Visual Studio 2013 Atualização 5 com SSDT a fim de permitir a compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="5190a-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="5190a-106">O uso do Visual Studio com SSDT permite o uso do Pesquisador de Objetos do SQL Server para explorar visualmente tabelas, exibições, procedimentos armazenados e muitos outros objetos em seu SQL Data Warehouse, além da execução de consultas.</span><span class="sxs-lookup"><span data-stu-id="5190a-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="5190a-107">O SQL Data Warehouse ainda não dá suporte aos Projetos do Banco de Dados do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5190a-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="5190a-108">Este recurso será adicionado em uma futura versão.</span><span class="sxs-lookup"><span data-stu-id="5190a-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="5190a-109">Etapa 1: instalar o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5190a-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="5190a-110">Siga estes links para baixar e instalar o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5190a-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="5190a-111">Se você já tiver o Visual Studio 2013 ou posterior instalado, pule para a Etapa 2 e instale o SSDT.</span><span class="sxs-lookup"><span data-stu-id="5190a-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="5190a-112">[Baixar o Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="5190a-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="5190a-113">Siga o guia [Instalação do Visual Studio][Installing Visual Studio] no MSDN e escolha as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="5190a-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="5190a-114">Etapa 2: Instalar o SSDT</span><span class="sxs-lookup"><span data-stu-id="5190a-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="5190a-115">Para instalar o SSDT para o Visual Studio, simplesmente procure uma atualização do SSDT dentro do Visual Studio seguindo estas etapas.</span><span class="sxs-lookup"><span data-stu-id="5190a-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="5190a-116">No Visual Studio, clique em **Ferramentas** / **Extensões e Atualizações…**</span><span class="sxs-lookup"><span data-stu-id="5190a-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="5190a-117"> / **Atualizações**</span><span class="sxs-lookup"><span data-stu-id="5190a-117"> / **Updates**</span></span>
2. <span data-ttu-id="5190a-118">Selecione **Atualizações do Produto**, em seguida, procure **Atualização do Microsoft SQL Server para as ferramentas do banco de dados**</span><span class="sxs-lookup"><span data-stu-id="5190a-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="5190a-119">Se nenhuma atualização for encontrada, você já terá a versão mais recente instalada.</span><span class="sxs-lookup"><span data-stu-id="5190a-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="5190a-120">Para confirmar se o SSDT está instalado, clique em **Ajuda** / **Sobre o Microsoft Visual Studio** e procure o SQL Server Data Tools na lista.</span><span class="sxs-lookup"><span data-stu-id="5190a-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="5190a-121">A versão mais recente do SSDT é 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="5190a-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="5190a-122">Se a opção de instalação não estiver disponível no Visual Studio, uma alternativa é visitar a página de [Download do SSDT][SSDT Download] para baixar e instalar o SSDT manualmente.</span><span class="sxs-lookup"><span data-stu-id="5190a-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5190a-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5190a-123">Next steps</span></span>
<span data-ttu-id="5190a-124">Agora que você tem a versão mais recente do SSDT, está pronto para se [conectar][connect] ao seu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5190a-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
<span data-ttu-id="5190a-125">[Baixar o Visual Studio]: https://www.visualstudio.com/downloads/</span><span class="sxs-lookup"><span data-stu-id="5190a-125">[Download Visual Studio]: https://www.visualstudio.com/downloads/</span></span>
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
