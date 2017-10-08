---
title: "Instalando aaaProblem Olá conector de agente de Proxy de aplicativo | Microsoft Docs"
description: "Como tootroubleshoot problemas que você pode Olá de face ao instalar o conector do agente de Proxy de aplicativo"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="06fc8-103">Problema ao instalar o conector do agente de Proxy de aplicativo de saudação</span><span class="sxs-lookup"><span data-stu-id="06fc8-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="06fc8-104">Conector de Proxy de aplicativo Microsoft AAD é um componente de domínio interno que usa conectividade de saudação tooestablish conexões de saída do domínio interno do toohello Olá nuvem ponto de extremidade disponível.</span><span class="sxs-lookup"><span data-stu-id="06fc8-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="06fc8-105">Áreas de problemas gerais com a instalação do conector</span><span class="sxs-lookup"><span data-stu-id="06fc8-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="06fc8-106">Quando ocorre falha na instalação de saudação de um conector, causa Olá é normalmente uma saudação áreas a seguir:</span><span class="sxs-lookup"><span data-stu-id="06fc8-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="06fc8-107">**Conectividade** – toocomplete uma instalação bem sucedida, Olá tooregister de necessidades novo conector e estabelecer as propriedades de confiança futuras.</span><span class="sxs-lookup"><span data-stu-id="06fc8-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="06fc8-108">Isso é feito por meio da conexão toohello serviço de nuvem do Proxy de aplicativo do AAD.</span><span class="sxs-lookup"><span data-stu-id="06fc8-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="06fc8-109">**Estabelecimento de confiança** – novo conector de saudação cria um certificado autoassinado e registra o serviço de nuvem toohello.</span><span class="sxs-lookup"><span data-stu-id="06fc8-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="06fc8-110">**Autenticação de Olá administrador** – durante a instalação, a saudação usuário deve fornecer credenciais de administrador de instalação do conector toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="06fc8-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="06fc8-111">Verifique se o serviço de Proxy de aplicativo de nuvem toohello conectividade e página de Login da Microsoft</span><span class="sxs-lookup"><span data-stu-id="06fc8-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="06fc8-112">**Objetivo:** verificar máquina Olá conector pode conectar-se o ponto de extremidade de registro de Proxy de aplicativo AAD toohello, bem como a página de logon do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06fc8-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="06fc8-113">Abra uma página da web a seguir de toohello navegador e acesse: <https://aadap-portcheck.connectorporttest.msappproxy.net> , verifique se essa conectividade de saudação tooCentral dos EUA e data centers do Leste dos EUA com portas 9090 e 9091 está funcionando.</span><span class="sxs-lookup"><span data-stu-id="06fc8-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="06fc8-114">Se qualquer uma dessas portas não for bem-sucedida (não tem uma marca de seleção verde), verifique se esse Olá Firewall ou proxy de back-end tem \*. msappproxy.net com portas 9090 e 9091 definidos corretamente.</span><span class="sxs-lookup"><span data-stu-id="06fc8-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="06fc8-115">Abra um navegador (guia separada) e vá toohello página da web a seguir: <https://login.microsoftonline.com>, certifique-se de que você pode fazer logon toothat página.</span><span class="sxs-lookup"><span data-stu-id="06fc8-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="06fc8-116">Verifique se os componentes do computador e de back-end oferecem suporte para certificados de confiança de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="06fc8-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="06fc8-117">**Objetivo:** verificar se o computador do conector hello, proxy de back-end e firewall podem suportam certificado Olá criado pelo conector Olá para futuras de confiança.</span><span class="sxs-lookup"><span data-stu-id="06fc8-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="06fc8-118">conector de saudação tenta toocreate um certificado de SHA512 com suporte do TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="06fc8-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="06fc8-119">Se a máquina hello ou firewall de back-end hello e proxy não oferece suporte a TLS 1.2, instalação de saudação falhar.</span><span class="sxs-lookup"><span data-stu-id="06fc8-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="06fc8-120">**problema de saudação tooresolve:**</span><span class="sxs-lookup"><span data-stu-id="06fc8-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="06fc8-121">Verifique se a máquina Olá dá suporte a TLS 1.2 – as versões de todas as janelas após 2012 R2 devem oferecer suporte a TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="06fc8-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="06fc8-122">Se o computador do conector é de uma versão do 2012 R2 ou anterior, certifique-se de que Olá seguintes KBs estão instalados na máquina de saudação: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="06fc8-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="06fc8-123">Contate seu administrador de rede e tooverify que firewall e proxy de back-end de saudação não bloqueiam SHA512 para tráfego de saída.</span><span class="sxs-lookup"><span data-stu-id="06fc8-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="06fc8-124">Verifique se administrador é usado tooinstall Olá conector</span><span class="sxs-lookup"><span data-stu-id="06fc8-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="06fc8-125">**Objetivo:** Verifique se esse usuário Olá que tenta conector de saudação tooinstall é um administrador com as credenciais corretas.</span><span class="sxs-lookup"><span data-stu-id="06fc8-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="06fc8-126">No momento, o usuário de saudação deve ser um administrador global para Olá toosucceed de instalação.</span><span class="sxs-lookup"><span data-stu-id="06fc8-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="06fc8-127">**credenciais de saudação do tooverify estão corretas:**</span><span class="sxs-lookup"><span data-stu-id="06fc8-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="06fc8-128">Conecte-se muito<https://login.microsoftonline.com> e use Olá as mesmas credenciais.</span><span class="sxs-lookup"><span data-stu-id="06fc8-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="06fc8-129">Certifique-se de saudação logon for bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="06fc8-129">Make sure hello login is successful.</span></span> <span data-ttu-id="06fc8-130">Você pode verificar a função de usuário Olá indo muito**Active Directory do Azure**  - &gt; **usuários e grupos**  - &gt; **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="06fc8-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="06fc8-131">Selecione sua conta de usuário, em seguida, "função de diretório" no menu resultante hello.</span><span class="sxs-lookup"><span data-stu-id="06fc8-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="06fc8-132">Verifique se a função hello selecionado é "Administrador Global".</span><span class="sxs-lookup"><span data-stu-id="06fc8-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="06fc8-133">Se você não é possível tooaccess qualquer Olá páginas ao longo dessas etapas, você não for um administrador global.</span><span class="sxs-lookup"><span data-stu-id="06fc8-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06fc8-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06fc8-134">Next steps</span></span>
[<span data-ttu-id="06fc8-135">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="06fc8-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
