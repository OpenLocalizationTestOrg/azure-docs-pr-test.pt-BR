---
title: "aaaRules de nomeação de entidades do Azure Data Factory | Microsoft Docs"
description: Descreve as regras de nomenclatura para entidades de Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="eff7b-103">Azure Data Factory - regras de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="eff7b-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="eff7b-104">Olá, a tabela a seguir fornece as regras de nomenclatura para artefatos de fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="eff7b-104">hello following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="eff7b-105">Nome</span><span class="sxs-lookup"><span data-stu-id="eff7b-105">Name</span></span> | <span data-ttu-id="eff7b-106">Exclusividade do nome</span><span class="sxs-lookup"><span data-stu-id="eff7b-106">Name Uniqueness</span></span> | <span data-ttu-id="eff7b-107">Verificações de validação</span><span class="sxs-lookup"><span data-stu-id="eff7b-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="eff7b-108">Data Factory</span><span class="sxs-lookup"><span data-stu-id="eff7b-108">Data Factory</span></span> |<span data-ttu-id="eff7b-109">Exclusivo em todo o Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eff7b-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="eff7b-110">Os nomes diferenciam maiusculas de minúsculas, isto é, `MyDF` e `mydf` consulte toohello mesma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="eff7b-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer toohello same data factory.</span></span> |<ul><li><span data-ttu-id="eff7b-111">Cada fábrica de dados é tooexactly associado uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="eff7b-111">Each data factory is tied tooexactly one Azure subscription.</span></span></li><li><span data-ttu-id="eff7b-112">Nomes de objeto devem começar com uma letra ou um número e podem conter apenas letras, números e caracteres de traço (-) hello.</span><span class="sxs-lookup"><span data-stu-id="eff7b-112">Object names must start with a letter or a number, and can contain only letters, numbers, and hello dash (-) character.</span></span></li><li><span data-ttu-id="eff7b-113">Cada caractere traço (-) deve ser imediatamente precedido e seguido por uma letra ou um número.</span><span class="sxs-lookup"><span data-stu-id="eff7b-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="eff7b-114">Não há permissão para traços consecutivos em nomes de contêiner.</span><span class="sxs-lookup"><span data-stu-id="eff7b-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="eff7b-115">O nome pode ter de 3 a 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="eff7b-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="eff7b-116">Serviços/tabelas/pipelines vinculados</span><span class="sxs-lookup"><span data-stu-id="eff7b-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="eff7b-117">Exclusivo em um mesmo data factory.</span><span class="sxs-lookup"><span data-stu-id="eff7b-117">Unique with in a data factory.</span></span> <span data-ttu-id="eff7b-118">Os nomes não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="eff7b-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="eff7b-119">Número máximo de caracteres em um nome de tabela: 260.</span><span class="sxs-lookup"><span data-stu-id="eff7b-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="eff7b-120">Os nomes de objetos devem começar com uma letra, um número ou um sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="eff7b-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="eff7b-121">Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="eff7b-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="eff7b-122">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="eff7b-122">Resource Group</span></span> |<span data-ttu-id="eff7b-123">Exclusivo em todo o Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eff7b-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="eff7b-124">Os nomes não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="eff7b-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="eff7b-125">Número máximo de caracteres: 1000.</span><span class="sxs-lookup"><span data-stu-id="eff7b-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="eff7b-126">Nome pode conter letras, dígitos e Olá seguintes caracteres: "-", "_",","e"."</span><span class="sxs-lookup"><span data-stu-id="eff7b-126">Name can contain letters, digits, and hello following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

