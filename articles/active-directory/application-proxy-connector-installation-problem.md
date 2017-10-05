---
title: Problemas ao instalar o conector de agente do Application Proxy | Microsoft Docs
description: "Como solucionar problemas que você poderá enfrentar ao instalar o conector de agente do Application Proxy"
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
ms.openlocfilehash: 91b3f6f3c8339647f568a509e9efd8e1fffb13dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a><span data-ttu-id="3a368-103">Problema ao instalar o conector de agente de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="3a368-103">Problem installing the Application Proxy Agent Connector</span></span>

<span data-ttu-id="3a368-104">Conector do Application Proxy do Microsoft AAD é um componente de domínio interno que usa conexões de saída para estabelecer a conectividade do ponto de extremidade da nuvem disponível para o domínio interno.</span><span class="sxs-lookup"><span data-stu-id="3a368-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="3a368-105">Áreas de problemas gerais com a instalação do conector</span><span class="sxs-lookup"><span data-stu-id="3a368-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="3a368-106">Quando a instalação de um conector falhar, a causa raiz é geralmente uma das seguintes áreas:</span><span class="sxs-lookup"><span data-stu-id="3a368-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span></span>

1.  <span data-ttu-id="3a368-107">**Conectividade** – para concluir uma instalação bem-sucedida, o novo conector precisa registrar e estabelecer as propriedades de confiança futuras.</span><span class="sxs-lookup"><span data-stu-id="3a368-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span></span> <span data-ttu-id="3a368-108">Isso é feito ao conectar ao serviço de nuvem do Application Proxy do AAD.</span><span class="sxs-lookup"><span data-stu-id="3a368-108">This is done by connecting to the AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="3a368-109">**Estabelecimento de confiança** – o novo conector cria um certificado autoassinado e registra ao serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3a368-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span></span>

3.  <span data-ttu-id="3a368-110">**Autenticação do administrador** – durante a instalação, o usuário deve fornecer credenciais de administrador para concluir a instalação do conector.</span><span class="sxs-lookup"><span data-stu-id="3a368-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span></span>

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="3a368-111">Verifique a conectividade com o serviço de Application Proxy de nuvem e a página de Logon da Microsoft</span><span class="sxs-lookup"><span data-stu-id="3a368-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="3a368-112">**Objetivo:** Verifique se o computador do conector pode se conectar ao ponto de extremidade de registro do Application Proxy do AAD, bem como página de logon do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3a368-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="3a368-113">Abra um navegador e vá para a seguinte página da Web: <https://aadap-portcheck.connectorporttest.msappproxy.net> e verificar se a conectividade com data centers aos EUA Central e Leste dos EUA com portas 9090 e 9091 está funcionando.</span><span class="sxs-lookup"><span data-stu-id="3a368-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="3a368-114">Se qualquer uma dessas portas não for bem-sucedida (não tem uma marca de seleção verde), verifique se o proxy do Firewall ou back-end tem portas 9090 e 9091 de \*.msappproxy.net definidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="3a368-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="3a368-115">Abra um navegador (guia separada) e vá para a seguinte página da Web: <https://login.microsoftonline.com>, certifique-se de que você pode fazer logon nessa página.</span><span class="sxs-lookup"><span data-stu-id="3a368-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="3a368-116">Verifique se os componentes do computador e de back-end oferecem suporte para certificados de confiança de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="3a368-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="3a368-117">**Objetivo:** Verifique se que o computador do conector, o proxy de back-end e o firewall podem dar suporte ao certificado criado pelo conector para confiança futura.</span><span class="sxs-lookup"><span data-stu-id="3a368-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="3a368-118">O conector tenta criar um certificado SHA512 com suporte a TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="3a368-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="3a368-119">Se o computador ou o firewall back-end e o proxy não oferece suporte a TLS1.2, a instalação falha.</span><span class="sxs-lookup"><span data-stu-id="3a368-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span></span>
>
>

<span data-ttu-id="3a368-120">**Como resolver o problema:**</span><span class="sxs-lookup"><span data-stu-id="3a368-120">**To resolve the issue:**</span></span>

1.  <span data-ttu-id="3a368-121">Verifique se o computador dá suporte a TLS1.2 – todas as versões do Windows após 2012 R2 devem oferecer suporte a TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="3a368-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="3a368-122">Se seu computador de conector for de uma versão de 2012 R2 ou anterior, certifique-se de que os seguintes KBs estão instalados no computador: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="3a368-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="3a368-123">Entre em contato com seu administrador de rede e peça para verificar se o proxy de back-end e o firewall não bloqueiam SHA512 para tráfego de saída.</span><span class="sxs-lookup"><span data-stu-id="3a368-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-to-install-the-connector"></a><span data-ttu-id="3a368-124">Verifique se o administrador é usado para instalar o conector</span><span class="sxs-lookup"><span data-stu-id="3a368-124">Verify admin is used to install the connector</span></span>

<span data-ttu-id="3a368-125">**Objetivo:** Verifique se o usuário que tenta instalar o conector é um administrador com as credenciais corretas.</span><span class="sxs-lookup"><span data-stu-id="3a368-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span></span> <span data-ttu-id="3a368-126">Atualmente, o usuário deve ser um administrador global para que a instalação tenha êxito.</span><span class="sxs-lookup"><span data-stu-id="3a368-126">Currently, the user must be a global administrator for the installation to succeed.</span></span>

<span data-ttu-id="3a368-127">**Para verificar se as credenciais estão corretas:**</span><span class="sxs-lookup"><span data-stu-id="3a368-127">**To verify the credentials are correct:**</span></span>

<span data-ttu-id="3a368-128">Conecte ao <https://login.microsoftonline.com> e use as mesmas credenciais.</span><span class="sxs-lookup"><span data-stu-id="3a368-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span></span> <span data-ttu-id="3a368-129">Verifique se o logon foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="3a368-129">Make sure the login is successful.</span></span> <span data-ttu-id="3a368-130">Você pode verificar a função de usuário acessando **Azure Active Directory** -&gt;**Usuários e grupos** -&gt;**Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3a368-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="3a368-131">Selecione sua conta de usuário, em seguida, "função do Directory" no menu resultante.</span><span class="sxs-lookup"><span data-stu-id="3a368-131">Select your user account, then “Directory Role” in the resulting menu.</span></span> <span data-ttu-id="3a368-132">Verifique se a função selecionada é "Administrador Global".</span><span class="sxs-lookup"><span data-stu-id="3a368-132">Verify that the selected role is “Global administrator”.</span></span> <span data-ttu-id="3a368-133">Se não for possível acessar qualquer uma das páginas ao longo dessas etapas, você não será um administrador global.</span><span class="sxs-lookup"><span data-stu-id="3a368-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a368-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a368-134">Next steps</span></span>
[<span data-ttu-id="3a368-135">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a368-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
