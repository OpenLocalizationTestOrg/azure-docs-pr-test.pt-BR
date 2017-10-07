---
title: "práticas recomendadas do RemoteApp aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="24455-103">Práticas recomendadas para configurar e usar o RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="24455-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="24455-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="24455-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="24455-105">Saudação de leitura [comunicado](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="24455-105">Read hello [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="24455-106">Olá informações a seguir pode ajudá-lo a configurar e usar o Azure RemoteApp produtiva.</span><span class="sxs-lookup"><span data-stu-id="24455-106">hello following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="24455-107">Conectividade</span><span class="sxs-lookup"><span data-stu-id="24455-107">Connectivity</span></span>
* <span data-ttu-id="24455-108">Sempre use a versão mais recente do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="24455-108">Always use hello latest client version.</span></span> <span data-ttu-id="24455-109">Usar clientes mais antigos pode resultar em problemas de conectividade e outras experiências degradadas.</span><span class="sxs-lookup"><span data-stu-id="24455-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="24455-110">Habilitar atualizações de aplicação automática para seu dispositivo garantirá o que cliente mais recente Olá é sempre instalado.</span><span class="sxs-lookup"><span data-stu-id="24455-110">Enabling automatic application updates for your device will ensure that hello latest client is always installed.</span></span>
* <span data-ttu-id="24455-111">Sempre use hello mais estável e confiável internet conexão disponível tooyou.</span><span class="sxs-lookup"><span data-stu-id="24455-111">Always use hello most stable and reliable internet connection available tooyou.</span></span>  
* <span data-ttu-id="24455-112">Use apenas conexões de proxy suportadas para desempenho ideal de conectividade.</span><span class="sxs-lookup"><span data-stu-id="24455-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="24455-113">Não há suporte para o proxy de meias para Hello.</span><span class="sxs-lookup"><span data-stu-id="24455-113">hello SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="24455-114">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="24455-114">Applications</span></span>
* <span data-ttu-id="24455-115">Salve e feche os aplicativos RemoteApp quando tiver terminado com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="24455-115">Save and close RemoteApp applications when you are done with hello application.</span></span> <span data-ttu-id="24455-116">Não fechar o aplicativo hello pode resultar em perda de dados.</span><span class="sxs-lookup"><span data-stu-id="24455-116">Not closing hello application might result in data loss.</span></span>
* <span data-ttu-id="24455-117">Valide aplicativos personalizados antes de usá-los no RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="24455-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="24455-118">Isso inclui garantir que eles funcionam em uma plataforma de várias sessões e não consomem recursos desnecessários, como memória e CPU que pode enfraquecer o outro usuário Olá mesma coleção.</span><span class="sxs-lookup"><span data-stu-id="24455-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in hello same collection.</span></span> <span data-ttu-id="24455-119">Para obter informações, baixe e leia Olá [práticas recomendadas de compatibilidade de aplicativos para os serviços de área de trabalho remota](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="24455-119">For information, download and review hello [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="24455-120">Configuração e gerenciamento</span><span class="sxs-lookup"><span data-stu-id="24455-120">Configuration and management</span></span>
* <span data-ttu-id="24455-121">Manter suas imagens de modelo para cima toodate, instalar atualizações de software e outras correções críticas, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="24455-121">Keep your template images up toodate, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="24455-122">Isso garante que, como o Azure RemoteApp autoescalas toomeet sua capacidade, cada instância é corrigida.</span><span class="sxs-lookup"><span data-stu-id="24455-122">This ensures that as Azure RemoteApp auto-scales toomeet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="24455-123">Verifique se a sua implantação de serviços de Federação do Active Directory (AD FS) está segura e confiável.</span><span class="sxs-lookup"><span data-stu-id="24455-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="24455-124">Caso contrário, as autenticações do cliente podem falhar, impedindo que os usuários acessem o RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="24455-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="24455-125">Configure imagens de modelo com aplicativos instalados, funções ou recursos que estão sem monitoramento do estado.</span><span class="sxs-lookup"><span data-stu-id="24455-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="24455-126">Eles não devem confiar em todas as instâncias de máquinas virtuais de saudação em um serviço do RemoteApp está em um estado persistente.</span><span class="sxs-lookup"><span data-stu-id="24455-126">They should not rely on any instances of hello virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="24455-127">Armazene todos os dados de usuário em perfis de usuário ou de outro serviço de toohello externo de locais de armazenamento, como local compartilhamentos de arquivos ou OneDrive.</span><span class="sxs-lookup"><span data-stu-id="24455-127">Store all user data in user profiles or other storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="24455-128">Armazene dados compartilhados no serviço de toohello externo de locais de armazenamento, como local compartilhamentos de arquivos ou OneDrive.</span><span class="sxs-lookup"><span data-stu-id="24455-128">Store shared data in storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="24455-129">Defina as configurações de todo o sistema na imagem de modelo de saudação em vez de em máquinas virtuais individuais em um serviço.</span><span class="sxs-lookup"><span data-stu-id="24455-129">Configure any system-wide settings in hello template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="24455-130">Desativar atualizações automáticas de software para aplicativos publicados - em vez disso, aplicá-las manualmente toohello imagem de modelo e testá-las antes de implantar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="24455-130">Disable automatic software updates for published applications - instead apply them manually toohello template image and test them before you deploy  from hello template.</span></span>

