---
title: "Operações do Synchronization Service Manager do Azure AD Connect | Microsoft Docs"
description: "Entenda como usar a guia Operações no Synchronization Service Manager para o Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1475e4fcd11eb008badba49665f4af6029a1697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-sync-service-manager-operations-tab"></a><span data-ttu-id="52797-103">Usando a guia Operações do Synchronization Service Manager</span><span class="sxs-lookup"><span data-stu-id="52797-103">Using the Sync Service Manager Operations tab</span></span>

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="52797-105">A guia Operações mostra os resultados das operações mais recentes.</span><span class="sxs-lookup"><span data-stu-id="52797-105">The operations tab shows the results from the most recent operations.</span></span> <span data-ttu-id="52797-106">Essa guia é o segredo para entender e solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="52797-106">This tab is key to understand and troubleshoot issues.</span></span>

## <a name="understand-the-information-visible-in-the-operations-tab"></a><span data-ttu-id="52797-107">Entender as informações visíveis na guia Operações</span><span class="sxs-lookup"><span data-stu-id="52797-107">Understand the information visible in the operations tab</span></span>
<span data-ttu-id="52797-108">A metade superior mostra todas as execuções em ordem cronológica.</span><span class="sxs-lookup"><span data-stu-id="52797-108">The top half shows all runs in chronological order.</span></span> <span data-ttu-id="52797-109">Por padrão, as operações de log mantêm informações sobre os últimos sete dias, mas essa configuração pode ser alterada com o [agendador](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="52797-109">By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="52797-110">Você deseja procurar qualquer execução que não mostre um status bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="52797-110">You want to look for any run that does not show a success status.</span></span> <span data-ttu-id="52797-111">É possível alterar a classificação clicando nos cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="52797-111">You can change the sorting by clicking the headers.</span></span>

<span data-ttu-id="52797-112">A coluna **Status** traz as informações mais importantes e mostra o problema mais grave de uma execução.</span><span class="sxs-lookup"><span data-stu-id="52797-112">The **Status** column is the most important information and shows the most severe problem for a run.</span></span> <span data-ttu-id="52797-113">Aqui está um resumo rápido dos status mais comuns em ordem de prioridade para investigação (em que * indica várias cadeias de caracteres de erro possíveis).</span><span class="sxs-lookup"><span data-stu-id="52797-113">Here is a quick summary of the most common statuses in order of priority to investigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="52797-114">Status</span><span class="sxs-lookup"><span data-stu-id="52797-114">Status</span></span> | <span data-ttu-id="52797-115">Comentário</span><span class="sxs-lookup"><span data-stu-id="52797-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="52797-116">stopped-*</span><span class="sxs-lookup"><span data-stu-id="52797-116">stopped-*</span></span> |<span data-ttu-id="52797-117">Não foi possível concluir a execução.</span><span class="sxs-lookup"><span data-stu-id="52797-117">The run could not complete.</span></span> <span data-ttu-id="52797-118">Por exemplo, se o sistema remoto está inoperante e não pode ser contatado.</span><span class="sxs-lookup"><span data-stu-id="52797-118">For example, if the remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="52797-119">stopped-error-limit</span><span class="sxs-lookup"><span data-stu-id="52797-119">stopped-error-limit</span></span> |<span data-ttu-id="52797-120">Há mais de 5.000 erros.</span><span class="sxs-lookup"><span data-stu-id="52797-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="52797-121">A execução foi interrompida automaticamente devido ao grande número de erros.</span><span class="sxs-lookup"><span data-stu-id="52797-121">The run was automatically stopped due to the large number of errors.</span></span> |
| <span data-ttu-id="52797-122">completed-\*-errors</span><span class="sxs-lookup"><span data-stu-id="52797-122">completed-\*-errors</span></span> |<span data-ttu-id="52797-123">A execução foi concluída, mas há erros (menos de 5.000) que devem ser investigados.</span><span class="sxs-lookup"><span data-stu-id="52797-123">The run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="52797-124">completed-\*-warnings</span><span class="sxs-lookup"><span data-stu-id="52797-124">completed-\*-warnings</span></span> |<span data-ttu-id="52797-125">A execução foi concluída, mas alguns dados não estão no estado esperado.</span><span class="sxs-lookup"><span data-stu-id="52797-125">The run completed, but some data is not in the expected state.</span></span> <span data-ttu-id="52797-126">Se houver erros, geralmente, essa mensagem indicará apenas um sintoma.</span><span class="sxs-lookup"><span data-stu-id="52797-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="52797-127">Até que tenha resolvido os erros, você não deverá investigar os avisos.</span><span class="sxs-lookup"><span data-stu-id="52797-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="52797-128">sucesso</span><span class="sxs-lookup"><span data-stu-id="52797-128">success</span></span> |<span data-ttu-id="52797-129">Nenhum problema.</span><span class="sxs-lookup"><span data-stu-id="52797-129">No issues.</span></span> |

<span data-ttu-id="52797-130">Quando você seleciona uma linha, a parte inferior é atualizada para mostrar os detalhes dessa execução.</span><span class="sxs-lookup"><span data-stu-id="52797-130">When you select a row, the bottom updates to show the details of that run.</span></span> <span data-ttu-id="52797-131">À extrema esquerda da parte inferior, talvez você veja uma lista indicando **Etapa nº**.</span><span class="sxs-lookup"><span data-stu-id="52797-131">To the far left of the bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="52797-132">Essa lista só será exibida se você tiver vários domínios na floresta, em que cada domínio é representado por uma etapa.</span><span class="sxs-lookup"><span data-stu-id="52797-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="52797-133">O nome de domínio pode ser encontrado sob o título **Partição**.</span><span class="sxs-lookup"><span data-stu-id="52797-133">The domain name can be found under the heading **Partition**.</span></span> <span data-ttu-id="52797-134">Em **Estatísticas de Sincronização**, é possível encontrar mais informações sobre o número de alterações que foram processadas.</span><span class="sxs-lookup"><span data-stu-id="52797-134">Under **Synchronization Statistics**, you can find more information about the number of changes that were processed.</span></span> <span data-ttu-id="52797-135">É possível clicar nos links para obter uma lista dos objetos alterados.</span><span class="sxs-lookup"><span data-stu-id="52797-135">You can click the links to get a list of the changed objects.</span></span> <span data-ttu-id="52797-136">Se você tiver objetos com erros, eles aparecerão em **erros de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="52797-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="52797-137">Para obter mais informações, consulte [Solução de problemas de um objeto que não está sincronizando](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span><span class="sxs-lookup"><span data-stu-id="52797-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="52797-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52797-138">Next steps</span></span>
<span data-ttu-id="52797-139">Saiba mais sobre a configuração de [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="52797-139">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="52797-140">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="52797-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
