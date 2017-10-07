---
ms.assetid: 
title: "mundos de segurança do Cofre de chaves aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="bc29d-102">Universos de segurança e limites geográficos do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bc29d-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="bc29d-103">O Azure Key Vault é um serviço multilocatário e usa um pool de HSMs (Módulos de Segurança de Hardware) em cada localização do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc29d-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="bc29d-104">Todos os HSMs nos locais do Azure da saudação mesma região geográfica compartilham Olá mesmo limite de criptografia (Thales mundo de segurança).</span><span class="sxs-lookup"><span data-stu-id="bc29d-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="bc29d-105">Por exemplo, EUA Leste e Oeste dos EUA compartilhar Olá mundo de segurança mesmo porque elas pertencem a localização geográfica de toohello dos EUA.</span><span class="sxs-lookup"><span data-stu-id="bc29d-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="bc29d-106">Da mesma forma, todos os locais do Azure no compartilhamento Japão Olá mundo de segurança mesmo e todos os locais do Azure na Austrália, Índia e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="bc29d-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="bc29d-107">Comportamento de backup e restauração</span><span class="sxs-lookup"><span data-stu-id="bc29d-107">Backup and restore behavior</span></span>

<span data-ttu-id="bc29d-108">Um backup feito de uma chave de um cofre de chaves em um local do Azure pode ser restaurados tooa Cofre de chaves em outro local do Azure, desde que essas duas condições forem verdadeiras:</span><span class="sxs-lookup"><span data-stu-id="bc29d-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="bc29d-109">Ambos hello Azure locais pertencem toohello mesmo local geográfico</span><span class="sxs-lookup"><span data-stu-id="bc29d-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="bc29d-110">Cofre de chave Olá pertencer toohello mesma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="bc29d-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="bc29d-111">Por exemplo, um backup feito por uma determinada assinatura de uma chave em um cofre de chaves no Oeste da Índia, só pode ser restaurado tooanother Cofre de chaves em Olá mesma assinatura e localização geográfica; Oeste da Índia, Índia Central ou Sul da Índia.</span><span class="sxs-lookup"><span data-stu-id="bc29d-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="bc29d-112">Regiões e produtos</span><span class="sxs-lookup"><span data-stu-id="bc29d-112">Regions and products</span></span>

- [<span data-ttu-id="bc29d-113">Regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="bc29d-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="bc29d-114">Produtos da Microsoft por região</span><span class="sxs-lookup"><span data-stu-id="bc29d-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="bc29d-115">Regiões são mapeadas toosecurity mundos, mostrados como títulos principais nas tabelas de saudação:</span><span class="sxs-lookup"><span data-stu-id="bc29d-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="bc29d-116">Em produtos Olá pelo artigo da região, por exemplo, Olá **Américas** guia contém Leste EUA, centro dos EUA, oeste dos EUA todos os mapeamento toohello Américas região.</span><span class="sxs-lookup"><span data-stu-id="bc29d-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="bc29d-117">Uma exceção é que US DOD LESTE e US DOD CENTRAL têm seus próprios mundos de segurança.</span><span class="sxs-lookup"><span data-stu-id="bc29d-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="bc29d-118">Da mesma forma, em Olá **Europa** guia, Norte da Europa e Europa Ocidental são mapeados toohello região da Europa.</span><span class="sxs-lookup"><span data-stu-id="bc29d-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="bc29d-119">Olá mesmo também ocorre em Olá **Ásia-Pacífico** guia.</span><span class="sxs-lookup"><span data-stu-id="bc29d-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



