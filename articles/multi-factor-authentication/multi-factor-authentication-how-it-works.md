---
title: aaaAzure multi-Factor Authentication - como ele funciona
description: "Autenticação multifator do Azure ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple. Ele fornece segurança adicional, exigindo uma segunda forma de autenticação e fornece autenticação forte por meio de uma variedade de opções de verificação fácil."
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="df0de-104">Como funciona o Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="df0de-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="df0de-105">segurança de saudação de verificação em duas etapas é sua abordagem em camadas.</span><span class="sxs-lookup"><span data-stu-id="df0de-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="df0de-106">O comprometimento de vários fatores de autenticação apresenta um desafio significativo para os invasores.</span><span class="sxs-lookup"><span data-stu-id="df0de-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="df0de-107">Mesmo se um invasor toolearn Olá a senha de usuário, é inútil sem também ter posse do dispositivo confiável hello.</span><span class="sxs-lookup"><span data-stu-id="df0de-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Prova](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="df0de-109">Autenticação multifator do Azure ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple.</span><span class="sxs-lookup"><span data-stu-id="df0de-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="df0de-110">Ele fornece segurança adicional, exigindo uma segunda forma de autenticação e fornece autenticação forte por meio de uma variedade de opções de verificação fácil.</span><span class="sxs-lookup"><span data-stu-id="df0de-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="df0de-111">Métodos disponíveis para verificação em duas etapas</span><span class="sxs-lookup"><span data-stu-id="df0de-111">Methods available for two-step verification</span></span>
<span data-ttu-id="df0de-112">Quando um usuário entra, uma verificação adicional é enviada toohello usuário.</span><span class="sxs-lookup"><span data-stu-id="df0de-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="df0de-113">Olá seguem uma lista de métodos que podem ser usados para essa verificação de segundo.</span><span class="sxs-lookup"><span data-stu-id="df0de-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="df0de-114">Método de verificação</span><span class="sxs-lookup"><span data-stu-id="df0de-114">Verification Method</span></span> | <span data-ttu-id="df0de-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="df0de-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="df0de-116">chamada telefônica</span><span class="sxs-lookup"><span data-stu-id="df0de-116">Phone call</span></span> |<span data-ttu-id="df0de-117">Uma chamada é feita de telefone registrado tooa do usuário.</span><span class="sxs-lookup"><span data-stu-id="df0de-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="df0de-118">usuário Olá insere um PIN, se necessário, em seguida, pressiona a tecla # de saudação.</span><span class="sxs-lookup"><span data-stu-id="df0de-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="df0de-119">mensagem de texto</span><span class="sxs-lookup"><span data-stu-id="df0de-119">Text message</span></span> |<span data-ttu-id="df0de-120">Uma mensagem de texto é enviada celular do usuário tooa com um código de seis dígitos.</span><span class="sxs-lookup"><span data-stu-id="df0de-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="df0de-121">usuário Olá insere esse código na página de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="df0de-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="df0de-122">Notificação de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="df0de-122">Mobile app notification</span></span> |<span data-ttu-id="df0de-123">Uma solicitação de verificação é enviada Smartphone do usuário tooa.</span><span class="sxs-lookup"><span data-stu-id="df0de-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="df0de-124">Olá usuário digita um PIN, se necessário, em seguida, seleciona **verificar** no aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="df0de-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="df0de-125">Código de verificação do aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="df0de-125">Mobile app verification code</span></span> |<span data-ttu-id="df0de-126">aplicativo móvel Hello, que está em execução no Smartphone do usuário, exibe um código de verificação que muda a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="df0de-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="df0de-127">usuário Olá localiza o código mais recente hello e insere-o na página de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="df0de-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="df0de-128">Tokens OATH de terceiros</span><span class="sxs-lookup"><span data-stu-id="df0de-128">Third-party OATH tokens</span></span> | <span data-ttu-id="df0de-129">Servidor de autenticação multifator do Azure pode ser configurado tooaccept métodos de verificação de terceiros.</span><span class="sxs-lookup"><span data-stu-id="df0de-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="df0de-130">O Azure Multi-Factor Authentication fornece métodos de verificação selecionável para a nuvem e o servidor.</span><span class="sxs-lookup"><span data-stu-id="df0de-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="df0de-131">É possível escolher quais métodos estarão disponíveis para os usuários: chamada telefônica, texto, notificação no aplicativo ou códigos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df0de-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="df0de-132">Para obter mais informações, consulte os [métodos de verificação selecionáveis](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="df0de-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="df0de-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df0de-133">Next steps</span></span>

- <span data-ttu-id="df0de-134">Leia sobre Olá diferente [versões e os métodos de consumo para autenticação multifator do Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="df0de-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="df0de-135">Escolha se toodeploy Azure MFA [na nuvem de saudação ou no local](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="df0de-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="df0de-136">Leia as respostas para as [Perguntas frequentes](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="df0de-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>