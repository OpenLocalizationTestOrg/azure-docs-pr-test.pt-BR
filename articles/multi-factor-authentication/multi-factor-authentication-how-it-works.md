---
title: Azure Multi-Factor Authentication - Como funciona
description: "O Azure Multi-Factor Authentication ajuda a proteger o acesso a dados e aplicativos enquanto atende à demanda dos usuários para um processo de logon simples. Ele fornece segurança adicional, exigindo uma segunda forma de autenticação e fornece autenticação forte por meio de uma variedade de opções de verificação fácil."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="074a3-104">Como funciona o Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="074a3-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="074a3-105">A segurança da verificação em duas etapas baseia-se na sua abordagem em camadas.</span><span class="sxs-lookup"><span data-stu-id="074a3-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="074a3-106">O comprometimento de vários fatores de autenticação apresenta um desafio significativo para os invasores.</span><span class="sxs-lookup"><span data-stu-id="074a3-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="074a3-107">Mesmo que um invasor consiga saber a senha do usuário, isso será inútil se ele também não tiver posse do dispositivo confiável.</span><span class="sxs-lookup"><span data-stu-id="074a3-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Prova](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="074a3-109">O Azure Multi-Factor Authentication ajuda a proteger o acesso a dados e aplicativos enquanto atende à demanda dos usuários para um processo de logon simples.</span><span class="sxs-lookup"><span data-stu-id="074a3-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="074a3-110">Ele fornece segurança adicional, exigindo uma segunda forma de autenticação e fornece autenticação forte por meio de uma variedade de opções de verificação fácil.</span><span class="sxs-lookup"><span data-stu-id="074a3-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="074a3-111">Métodos disponíveis para verificação em duas etapas</span><span class="sxs-lookup"><span data-stu-id="074a3-111">Methods available for two-step verification</span></span>
<span data-ttu-id="074a3-112">Quando um usuário entra, uma verificação adicional é enviada ao usuário.</span><span class="sxs-lookup"><span data-stu-id="074a3-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="074a3-113">Veja a seguir uma lista de métodos que podem ser usados para essa segunda verificação.</span><span class="sxs-lookup"><span data-stu-id="074a3-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="074a3-114">Método de verificação</span><span class="sxs-lookup"><span data-stu-id="074a3-114">Verification Method</span></span> | <span data-ttu-id="074a3-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="074a3-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="074a3-116">chamada telefônica</span><span class="sxs-lookup"><span data-stu-id="074a3-116">Phone call</span></span> |<span data-ttu-id="074a3-117">É feita uma chamada para o telefone registrado de um usuário.</span><span class="sxs-lookup"><span data-stu-id="074a3-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="074a3-118">O usuário insere um PIN, se necessário e, em seguida, pressiona a tecla #.</span><span class="sxs-lookup"><span data-stu-id="074a3-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="074a3-119">mensagem de texto</span><span class="sxs-lookup"><span data-stu-id="074a3-119">Text message</span></span> |<span data-ttu-id="074a3-120">Uma mensagem de texto é enviada para o celular de um usuário com um código de seis dígitos.</span><span class="sxs-lookup"><span data-stu-id="074a3-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="074a3-121">O usuário insere esse código na página de entrada.</span><span class="sxs-lookup"><span data-stu-id="074a3-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="074a3-122">Notificação de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="074a3-122">Mobile app notification</span></span> |<span data-ttu-id="074a3-123">Uma solicitação de verificação é enviada para o smartphone de um usuário.</span><span class="sxs-lookup"><span data-stu-id="074a3-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="074a3-124">O usuário insere um PIN, se necessário e, em seguida, seleciona **Confirmar** no aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="074a3-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="074a3-125">Código de verificação do aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="074a3-125">Mobile app verification code</span></span> |<span data-ttu-id="074a3-126">O aplicativo móvel, executado no smartphone de um usuário, exibe um código de verificação que muda a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="074a3-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="074a3-127">O usuário localiza o código mais recente e o insere na página de entrada.</span><span class="sxs-lookup"><span data-stu-id="074a3-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="074a3-128">Tokens OATH de terceiros</span><span class="sxs-lookup"><span data-stu-id="074a3-128">Third-party OATH tokens</span></span> | <span data-ttu-id="074a3-129">O Servidor de Autenticação Multifator do Azure pode ser configurado para aceitar métodos de verificação de terceiros.</span><span class="sxs-lookup"><span data-stu-id="074a3-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="074a3-130">O Azure Multi-Factor Authentication fornece métodos de verificação selecionável para a nuvem e o servidor.</span><span class="sxs-lookup"><span data-stu-id="074a3-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="074a3-131">É possível escolher quais métodos estarão disponíveis para os usuários: chamada telefônica, texto, notificação no aplicativo ou códigos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="074a3-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="074a3-132">Para obter mais informações, consulte os [métodos de verificação selecionáveis](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="074a3-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="074a3-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="074a3-133">Next steps</span></span>

- <span data-ttu-id="074a3-134">Leia sobre os diferentes [métodos de consumo e versões para a Autenticação Multifator do Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="074a3-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="074a3-135">Escolha se deseja implantar o Azure MFA [na nuvem ou no local](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="074a3-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="074a3-136">Leia as respostas para as [Perguntas frequentes](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="074a3-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>