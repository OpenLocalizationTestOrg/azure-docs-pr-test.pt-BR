---
title: "Active Directory B2C: Residência de dados e disponibilidade de região | Microsoft Docs"
description: "Um tópico sobre os tipos de locatários do Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="16db4-103">Azure Active Directory B2C: Residência de dados e disponibilidade de região</span><span class="sxs-lookup"><span data-stu-id="16db4-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="16db4-104">Residência de dados e disponibilidade de região são dois conceitos muito diferentes que se aplicam a B2C do Azure AD diferentemente do restante do Azure.</span><span class="sxs-lookup"><span data-stu-id="16db4-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="16db4-105">Este artigo irá explicar as diferenças entre esses dois conceitos e comparar como são aplicáveis para B2C do Azure AD versus Azure.</span><span class="sxs-lookup"><span data-stu-id="16db4-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="16db4-106">Resumo</span><span class="sxs-lookup"><span data-stu-id="16db4-106">Summary</span></span>
<span data-ttu-id="16db4-107">B2C do Azure AD está **disponível em todo o mundo** com a opção para **residência de dados nos Estados Unidos ou Europa**.</span><span class="sxs-lookup"><span data-stu-id="16db4-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="16db4-108">Conceitos</span><span class="sxs-lookup"><span data-stu-id="16db4-108">Concepts</span></span>
* <span data-ttu-id="16db4-109">**Disponibilidade da região** refere-se onde um serviço está disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="16db4-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="16db4-110">**Residência dados** refere-se ao armazenamento de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="16db4-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="16db4-111">Disponibilidade de região</span><span class="sxs-lookup"><span data-stu-id="16db4-111">Region availability</span></span>
<span data-ttu-id="16db4-112">B2C do Azure AD está disponível em todo o mundo por meio da nuvem pública do Azure.</span><span class="sxs-lookup"><span data-stu-id="16db4-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="16db4-113">Isso difere do modelo da maioria dos demais serviços do Azure, que une disponibilidade com residência de dados.</span><span class="sxs-lookup"><span data-stu-id="16db4-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="16db4-114">É possível visualizar exemplos disso na página [Produtos Disponíveis por Região](https://azure.microsoft.com/regions/services/) e [Calculadora de preços B2C do Active Directory](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="16db4-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="16db4-115">Residência de dadosResidência de dados</span><span class="sxs-lookup"><span data-stu-id="16db4-115">Data residency</span></span>
<span data-ttu-id="16db4-116">B2C do Azure AD armazena dados do usuário nos Estados Unidos ou na Europa.</span><span class="sxs-lookup"><span data-stu-id="16db4-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="16db4-117">Residência de dados é determinada com base em qual país/região é selecionada ao [criar um locatário B2C do Azure AD](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16db4-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Captura de tela de um locatário de visualização](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="16db4-119">Os dados residem nos Estados Unidos para os seguintes países/regiões:</span><span class="sxs-lookup"><span data-stu-id="16db4-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="16db4-120">Estados Unidos, Canadá, Costa Rica, República Dominicana, El Salvador, Guatemala, México, Panamá, Porto Rico e Trinidad e Tobago</span><span class="sxs-lookup"><span data-stu-id="16db4-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="16db4-121">Os dados residem na Europa para os seguintes países/regiões:</span><span class="sxs-lookup"><span data-stu-id="16db4-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="16db4-122">África do Sul, Alemanha, Arábia Saudita, Argélia, Áustria, Azerbaidjão, Barein, Bélgica, Bielorrússia, Bulgária, Cazaquistão, Chipre, Croácia, Dinamarca, Egito, Emirados Árabes Unidos, Eslováquia, Eslovênia, Espanha, Estônia, Finlândia, França, Grécia, Hungria, Irlanda, Islândia, Israel, Itália, Jordânia, Kuwait, Letônia, Líbano, Liechtenstein, Lituânia, Luxemburgo, Macedônia FYRO, Malta, Marrocos, Montenegro, Nigéria, Noruega, Omã, Países Baixos, Paquistão, Polônia, Portugal, Qatar, Quênia, Reino Unido, República Checa, Romênia, Rússia, Sérvia, Suécia, Suíça, Tunísia, Turquia, Ucrânia.</span><span class="sxs-lookup"><span data-stu-id="16db4-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="16db4-123">Os demais países/regiões estão no processo de serem adicionados à lista.</span><span class="sxs-lookup"><span data-stu-id="16db4-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="16db4-124">Por enquanto, ainda é possível utilizar B2C do Azure AD, escolhendo qualquer um dos países/regiões acima.</span><span class="sxs-lookup"><span data-stu-id="16db4-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="16db4-125">Afeganistão, Argentina, Austrália, Brasil, Chile, Colômbia, Equador, RAE de Hong Kong, Índia, Indonésia, Iraque, Japão, Coreia, Malásia, Nova Zelândia, Paraguai, Peru, Filipinas, Cingapura, Sri Lanka, Taiwan, Tailândia, Uruguai e Venezuela.</span><span class="sxs-lookup"><span data-stu-id="16db4-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="16db4-126">Locatário de visualização</span><span class="sxs-lookup"><span data-stu-id="16db4-126">Preview tenant</span></span>
<span data-ttu-id="16db4-127">Se você criou um locatário do B2C durante o período de visualização do Azure AD B2C, é provável que seu **Tipo de locatário** seja **Locatário de visualização**.</span><span class="sxs-lookup"><span data-stu-id="16db4-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="16db4-128">Se esse for o caso, você DEVERÁ usar o locatário somente para fins de teste e desenvolvimento e NÃO para aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="16db4-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16db4-129">Não há um caminho de migração de um locatário do B2C de visualização para um locatário do B2C de produção-escala.</span><span class="sxs-lookup"><span data-stu-id="16db4-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="16db4-130">Observe que há problemas conhecidos quando você exclui um locatário B2C de visualização e recria um locatário B2C de escala de produção com o mesmo nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="16db4-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="16db4-131">Você precisa criar um locatário B2C de escala de produção com um nome de domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="16db4-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![Captura de tela de um locatário de visualização](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
