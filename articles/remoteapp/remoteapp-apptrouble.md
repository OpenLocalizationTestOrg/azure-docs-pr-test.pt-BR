---
title: "Solucionar problemas do Azure RemoteApp - falhas de conexão e inicialização do aplicativo | Microsoft Docs"
description: "Saiba como solucionar problemas com a inicialização e a conexão a aplicativos no Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fc9d538991adce7fc13e9654b9a7c6d113d03fde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a><span data-ttu-id="a51a2-103">Solucionar problemas do Azure RemoteApp - falhas de conexão e inicialização do aplicativo</span><span class="sxs-lookup"><span data-stu-id="a51a2-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a51a2-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="a51a2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a51a2-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a51a2-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a51a2-106">Aplicativos hospedados no Azure RemoteApp podem falhar ao inicializar por alguns motivos diferentes.</span><span class="sxs-lookup"><span data-stu-id="a51a2-106">Applications hosted in Azure RemoteApp can fail to launch for a few different reasons.</span></span> <span data-ttu-id="a51a2-107">Este artigo descreve vários motivos e mensagens de erro que os usuários podem receber quando tentam inicializar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a51a2-107">This article describes various reasons and error messages users might receive when trying to launch applications.</span></span> <span data-ttu-id="a51a2-108">Ele também fala sobre falhas de conexão.</span><span class="sxs-lookup"><span data-stu-id="a51a2-108">It also talks about connection failures.</span></span> <span data-ttu-id="a51a2-109">(Mas o artigo não descreve problemas ao entrar no cliente do Azure RemoteApp).</span><span class="sxs-lookup"><span data-stu-id="a51a2-109">(But this article does not describe issues when signing into the Azure RemoteApp client.)</span></span>  

<span data-ttu-id="a51a2-110">Continue lendo para obter informações sobre mensagens de erro comuns devido a falhas de conexão e inicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a51a2-110">Read on for information about common error messages due to app launch and connection failures.</span></span>

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a><span data-ttu-id="a51a2-111">Estamos configurando para você... Tente novamente em 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a51a2-111">We're getting you set up... Try again in 10 minutes.</span></span>
<span data-ttu-id="a51a2-112">Este erro significa que o Azure RemoteApp está ampliando sua capacidade para atender às necessidades de seus usuários.</span><span class="sxs-lookup"><span data-stu-id="a51a2-112">This error means Azure RemoteApp is scaling up to meet the capacity need of your users.</span></span> <span data-ttu-id="a51a2-113">Em segundo plano, mais instâncias de VM do Azure RemoteApp estão sendo criadas para atender às necessidades de capacidade de seus usuários.</span><span class="sxs-lookup"><span data-stu-id="a51a2-113">In the background more Azure RemoteApp VM instances are being created to handle the capacity needs of your users.</span></span> <span data-ttu-id="a51a2-114">Normalmente, isso leva cerca de cinco, mas pode levar até 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a51a2-114">Typically this takes around five minutes but can take up to 10 minutes.</span></span> <span data-ttu-id="a51a2-115">Às vezes, isso não acontece rápido o suficiente e os recursos são necessários imediatamente.</span><span class="sxs-lookup"><span data-stu-id="a51a2-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span></span> <span data-ttu-id="a51a2-116">Por exemplo, um cenário às 9h em que vários usuários precisam usar seu aplicativo no Azure RemoteAppn ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a51a2-116">For example a 9 AM scenario where many users need to use your app in Azure RemoteAppn at the same time.</span></span> <span data-ttu-id="a51a2-117">Se isso ocorrer, poderemos habilitar o **modo de capacidade** no back-end.</span><span class="sxs-lookup"><span data-stu-id="a51a2-117">If this happens to you we can enable **capacity mode** on the back end.</span></span> <span data-ttu-id="a51a2-118">Para fazer isso, abra um tíquete de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="a51a2-118">To do this open an Azure Support ticket.</span></span> <span data-ttu-id="a51a2-119">Certifique-se de incluir sua ID de assinatura na solicitação.</span><span class="sxs-lookup"><span data-stu-id="a51a2-119">Be certain to include your subscription ID in the request.</span></span>  

![Estamos configurando para você](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-to-your-applications-please-re-launch-your-application"></a><span data-ttu-id="a51a2-121">Não foi possível se reconectar automaticamente aos seus aplicativos, inicialize novamente seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="a51a2-121">Could not auto-reconnect to your applications, please re-launch your application</span></span>
<span data-ttu-id="a51a2-122">Esta mensagem de erro normalmente é vista se estava usando o Azure RemoteApp, colocou seu computador em suspensão por mais de 4 horas e, em seguida, ativou o computador e o cliente do Azure RemoteApp tentou se reconectar automaticamente e o tempo limite foi excedido.</span><span class="sxs-lookup"><span data-stu-id="a51a2-122">This error message is often seen if you were using Azure RemoteApp and then put your PC to sleep longer than 4 hours and then woke your PC up and the Azure RemoteApp client attempt to auto reconnect and timeout was exceeded.</span></span>  <span data-ttu-id="a51a2-123">Instrua os usuários a navegar de volta para o aplicativo e tentar abri-lo no cliente do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a51a2-123">Instruct users to navigate back to the application and attempt to open it from the Azure RemoteApp client.</span></span>

![Não foi possível reconectar automaticamente aos seus aplicativos](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-the-temp-profile"></a><span data-ttu-id="a51a2-125">Problemas com o perfil temporário</span><span class="sxs-lookup"><span data-stu-id="a51a2-125">Problems with the temp profile</span></span>
<span data-ttu-id="a51a2-126">Este erro ocorre quando seu perfil de usuário (disco de perfil do usuário) não foi montado e o usuário recebeu um perfil temporário.</span><span class="sxs-lookup"><span data-stu-id="a51a2-126">This error occurs when your user profile (User Profile Disk) failed to mount and the user received a temporary profile.</span></span>  <span data-ttu-id="a51a2-127">Os administradores devem navegar para a coleção no portal do Azure e ir até a guia **Sessões** e tentar **Fazer logoff** do usuário.</span><span class="sxs-lookup"><span data-stu-id="a51a2-127">Administrators should navigate to the collection in the Azure portal and then go to the **Sessions** tab and attempt to **Log Off** the user.</span></span> <span data-ttu-id="a51a2-128">Isso forçará o logoff completo da sessão de usuário - em seguida, peça que o usuário tente inicializar um aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="a51a2-128">This will force a full log off of the user session - then have the user attempt to launch an app again.</span></span> <span data-ttu-id="a51a2-129">Se não funcionar, entre em contato com o suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="a51a2-129">If that fails contact Azure support.</span></span>

## <a name="azure-remoteapp-has-stopped-working"></a><span data-ttu-id="a51a2-130">O Azure RemoteApp parou de funcionar</span><span class="sxs-lookup"><span data-stu-id="a51a2-130">Azure RemoteApp has stopped working</span></span>
<span data-ttu-id="a51a2-131">Esta mensagem de erro significa que o cliente do Azure RemoteApp está tendo um problema e precisa ser reiniciado.</span><span class="sxs-lookup"><span data-stu-id="a51a2-131">This error message means the Azure RemoteApp client is having an issue and needs to be restarted.</span></span> <span data-ttu-id="a51a2-132">Instrua os usuários a fechar: selecione **Fechar programa** e reinicie o cliente do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a51a2-132">Instruct users to close: select **Close program** and then launch the Azure RemoteApp client again.</span></span>  <span data-ttu-id="a51a2-133">Se o problema persistir, abra um tíquete de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="a51a2-133">If the issue continues open and Azure Support ticket.</span></span>

![O Azure RemoteApp parou de funcionar](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-the-connection-or-contact-your-system-administrator"></a><span data-ttu-id="a51a2-135">Ocorreu um erro enquanto a Conexão de Área de Trabalho Remota estava acessando este recurso.</span><span class="sxs-lookup"><span data-stu-id="a51a2-135">An error occurred while Remote Desktop Connection was accessing this resource.</span></span> <span data-ttu-id="a51a2-136">Tente conectar novamente ou entre em contato com o administrador do sistema</span><span class="sxs-lookup"><span data-stu-id="a51a2-136">Retry the connection or contact your system administrator</span></span>
<span data-ttu-id="a51a2-137">Esta é uma mensagem de erro genérica — entre em contato com o suporte do Azure para que possamos investigar.</span><span class="sxs-lookup"><span data-stu-id="a51a2-137">This is a generic error message - contact Azure support so we can investigate.</span></span> 

![Mensagem genérica do Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

