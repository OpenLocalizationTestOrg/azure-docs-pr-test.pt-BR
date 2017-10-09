---
title: "Active Directory B2C: Residência de dados e disponibilidade de região | Microsoft Docs"
description: "Um tópico em tipos de saudação de locatários do Azure Active Directory B2C"
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
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="c06f6-103">Azure Active Directory B2C: Residência de dados e disponibilidade de região</span><span class="sxs-lookup"><span data-stu-id="c06f6-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="c06f6-104">Disponibilidade de região e residência de dados são dois conceitos muito diferentes que se aplicam diferentemente tooAzure AD B2C do restante de saudação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c06f6-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="c06f6-105">Este artigo explicam Olá diferenças entre esses dois conceitos e comparar como elas se aplicam a tooAzure versus B2C do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c06f6-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="c06f6-106">Resumo</span><span class="sxs-lookup"><span data-stu-id="c06f6-106">Summary</span></span>
<span data-ttu-id="c06f6-107">B2C do Azure AD é **disponível em todo o mundo** com a opção Olá para **residência de dados nos Estados Unidos ou Europa**.</span><span class="sxs-lookup"><span data-stu-id="c06f6-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="c06f6-108">Conceitos</span><span class="sxs-lookup"><span data-stu-id="c06f6-108">Concepts</span></span>
* <span data-ttu-id="c06f6-109">**Disponibilidade de região** refere-se toowhere um serviço está disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="c06f6-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="c06f6-110">**Residência dados** refere-se o usuário toowhere os dados são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c06f6-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="c06f6-111">Disponibilidade de região</span><span class="sxs-lookup"><span data-stu-id="c06f6-111">Region availability</span></span>
<span data-ttu-id="c06f6-112">B2C do AD do Azure está disponível em todo o mundo via Olá nuvem pública do Azure.</span><span class="sxs-lookup"><span data-stu-id="c06f6-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="c06f6-113">Isso difere do modelo de saudação siga a maioria dos outros serviços do Azure que acumula a disponibilidade com residência de dados.</span><span class="sxs-lookup"><span data-stu-id="c06f6-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="c06f6-114">Você pode ver exemplos de ambos os Azure [produtos disponíveis por região](https://azure.microsoft.com/regions/services/) página e hello [Calculadora de preços B2C do Active Directory](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="c06f6-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="c06f6-115">Residência de dadosResidência de dados</span><span class="sxs-lookup"><span data-stu-id="c06f6-115">Data residency</span></span>
<span data-ttu-id="c06f6-116">B2C do Azure AD armazena dados do usuário nos Estados Unidos ou na Europa.</span><span class="sxs-lookup"><span data-stu-id="c06f6-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="c06f6-117">Residência de dados é determinada com base em qual país/região é selecionada ao [criar um locatário B2C do Azure AD](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c06f6-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Captura de tela de um locatário de visualização](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="c06f6-119">Os dados residem no hello dos Estados Unidos para Olá países/regiões a seguir:</span><span class="sxs-lookup"><span data-stu-id="c06f6-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="c06f6-120">Estados Unidos, Canadá, Costa Rica, República Dominicana, El Salvador, Guatemala, México, Panamá, Porto Rico e Trinidad e Tobago</span><span class="sxs-lookup"><span data-stu-id="c06f6-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="c06f6-121">Dados residem na Europa para Olá países/regiões a seguir:</span><span class="sxs-lookup"><span data-stu-id="c06f6-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="c06f6-122">África do Sul, Alemanha, Arábia Saudita, Argélia, Áustria, Azerbaidjão, Barein, Bélgica, Bielorrússia, Bulgária, Cazaquistão, Chipre, Croácia, Dinamarca, Egito, Emirados Árabes Unidos, Eslováquia, Eslovênia, Espanha, Estônia, Finlândia, França, Grécia, Hungria, Irlanda, Islândia, Israel, Itália, Jordânia, Kuwait, Letônia, Líbano, Liechtenstein, Lituânia, Luxemburgo, Macedônia FYRO, Malta, Marrocos, Montenegro, Nigéria, Noruega, Omã, Países Baixos, Paquistão, Polônia, Portugal, Qatar, Quênia, Reino Unido, República Checa, Romênia, Rússia, Sérvia, Suécia, Suíça, Tunísia, Turquia, Ucrânia.</span><span class="sxs-lookup"><span data-stu-id="c06f6-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="c06f6-123">Olá restantes países/regiões estão no processo de saudação do que está sendo adicionado toohello lista.</span><span class="sxs-lookup"><span data-stu-id="c06f6-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="c06f6-124">Por enquanto, você ainda pode usar o Azure AD B2C selecionando qualquer um dos países/regiões de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="c06f6-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="c06f6-125">Afeganistão, Argentina, Austrália, Brasil, Chile, Colômbia, Equador, RAE de Hong Kong, Índia, Indonésia, Iraque, Japão, Coreia, Malásia, Nova Zelândia, Paraguai, Peru, Filipinas, Cingapura, Sri Lanka, Taiwan, Tailândia, Uruguai e Venezuela.</span><span class="sxs-lookup"><span data-stu-id="c06f6-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="c06f6-126">Locatário de visualização</span><span class="sxs-lookup"><span data-stu-id="c06f6-126">Preview tenant</span></span>
<span data-ttu-id="c06f6-127">Se você criou um locatário do B2C durante o período de visualização do Azure AD B2C, é provável que seu **Tipo de locatário** seja **Locatário de visualização**.</span><span class="sxs-lookup"><span data-stu-id="c06f6-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="c06f6-128">Se esse for o caso de Olá, você deve usar o seu locatário somente para fins de teste e desenvolvimento e não para aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="c06f6-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c06f6-129">Não há nenhum caminho de migração de uma visualização locatário B2C do B2C locatário tooa escala de produção.</span><span class="sxs-lookup"><span data-stu-id="c06f6-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="c06f6-130">Observe que existem problemas conhecidos quando você exclui um locatário de visualização B2C e crie novamente uma escala de produção B2C locatário com hello o mesmo nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="c06f6-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="c06f6-131">Você tem toocreate um locatário B2C de escala de produção com um nome de domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="c06f6-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![Captura de tela de um locatário de visualização](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
