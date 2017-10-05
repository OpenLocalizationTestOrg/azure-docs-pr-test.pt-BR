---
title: "Práticas recomendadas do RemoteApp do Azure | Microsoft Docs"
description: "Práticas recomendadas para configurar e usar o RemoteApp do Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ab9c2dafc622e9b6f3bcd2767218cdc03e844847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="55c8f-103">Práticas recomendadas para configurar e usar o RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="55c8f-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="55c8f-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="55c8f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="55c8f-105">Leia o [comunicado](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="55c8f-105">Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="55c8f-106">As informações a seguir podem ajudá-lo a configurar e usar o RemoteApp do Azure de forma produtiva.</span><span class="sxs-lookup"><span data-stu-id="55c8f-106">The following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="55c8f-107">Conectividade</span><span class="sxs-lookup"><span data-stu-id="55c8f-107">Connectivity</span></span>
* <span data-ttu-id="55c8f-108">Sempre use a versão mais recente do cliente.</span><span class="sxs-lookup"><span data-stu-id="55c8f-108">Always use the latest client version.</span></span> <span data-ttu-id="55c8f-109">Usar clientes mais antigos pode resultar em problemas de conectividade e outras experiências degradadas.</span><span class="sxs-lookup"><span data-stu-id="55c8f-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="55c8f-110">A habilitação de atualizações automáticas do aplicativo para o dispositivo irá garantir que o cliente mais recente esteja sempre instalado.</span><span class="sxs-lookup"><span data-stu-id="55c8f-110">Enabling automatic application updates for your device will ensure that the latest client is always installed.</span></span>
* <span data-ttu-id="55c8f-111">Sempre use a conexão de internet mais estável e confiável disponível para você.</span><span class="sxs-lookup"><span data-stu-id="55c8f-111">Always use the most stable and reliable internet connection available to you.</span></span>  
* <span data-ttu-id="55c8f-112">Use apenas conexões de proxy suportadas para desempenho ideal de conectividade.</span><span class="sxs-lookup"><span data-stu-id="55c8f-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="55c8f-113">Não há suporte para o proxy SOCKS.</span><span class="sxs-lookup"><span data-stu-id="55c8f-113">The SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="55c8f-114">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="55c8f-114">Applications</span></span>
* <span data-ttu-id="55c8f-115">Salve e feche os aplicativos do RemoteApp ao terminar com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55c8f-115">Save and close RemoteApp applications when you are done with the application.</span></span> <span data-ttu-id="55c8f-116">O não fechamento do aplicativo pode resultar em perda de dados.</span><span class="sxs-lookup"><span data-stu-id="55c8f-116">Not closing the application might result in data loss.</span></span>
* <span data-ttu-id="55c8f-117">Valide aplicativos personalizados antes de usá-los no RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="55c8f-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="55c8f-118">Isso inclui garantir que eles funcionam em uma plataforma de várias sessões e não consomem recursos desnecessários, como memória e CPU que podem enfraquecer outro usuário na mesma coleção.</span><span class="sxs-lookup"><span data-stu-id="55c8f-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection.</span></span> <span data-ttu-id="55c8f-119">Para obter informações, baixe e analise as [Práticas recomendadas de compatibilidade de aplicativos para os serviços de área de trabalho remota](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="55c8f-119">For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="55c8f-120">Configuração e gerenciamento</span><span class="sxs-lookup"><span data-stu-id="55c8f-120">Configuration and management</span></span>
* <span data-ttu-id="55c8f-121">Mantenha suas imagens de modelo atualizadas, instale atualizações de software e outras correções críticas, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="55c8f-121">Keep your template images up to date, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="55c8f-122">Isso garante que, como o RemoteApp do Azure se redimensiona automaticamente para atender sua capacidade, cada instância é corrigida.</span><span class="sxs-lookup"><span data-stu-id="55c8f-122">This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="55c8f-123">Verifique se a sua implantação de serviços de Federação do Active Directory (AD FS) está segura e confiável.</span><span class="sxs-lookup"><span data-stu-id="55c8f-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="55c8f-124">Caso contrário, as autenticações do cliente podem falhar, impedindo que os usuários acessem o RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="55c8f-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="55c8f-125">Configure imagens de modelo com aplicativos instalados, funções ou recursos que estão sem monitoramento do estado.</span><span class="sxs-lookup"><span data-stu-id="55c8f-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="55c8f-126">Elas não devem confiar em todas as instâncias das máquinas virtuais em um serviço do RemoteApp estando em um estado persistente.</span><span class="sxs-lookup"><span data-stu-id="55c8f-126">They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="55c8f-127">Armazene todos os dados do usuário em perfis de usuário ou outros locais de armazenamento externos para o serviço, como compartilhamentos de arquivo local ou OneDrive.</span><span class="sxs-lookup"><span data-stu-id="55c8f-127">Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="55c8f-128">Armazene dados compartilhados em locais de armazenamento externos para o serviço, como compartilhamentos de arquivo local ou OneDrive.</span><span class="sxs-lookup"><span data-stu-id="55c8f-128">Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="55c8f-129">Configure quaisquer configurações gerais do sistema na imagem do modelo em vez de em máquinas virtuais individuais em um serviço.</span><span class="sxs-lookup"><span data-stu-id="55c8f-129">Configure any system-wide settings in the template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="55c8f-130">Desabilite atualizações automáticas de software para aplicativos publicados - em vez disso, aplique-as manualmente à imagem do modelo e teste-as antes da implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="55c8f-130">Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.</span></span>

