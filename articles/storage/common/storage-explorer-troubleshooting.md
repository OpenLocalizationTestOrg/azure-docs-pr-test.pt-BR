---
title: "Guia de solução de problemas do Gerenciador de Armazenamento do Azure | Microsoft Docs"
description: "Visão geral dos dois recursos de depuração do Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 470b2d87ffdc4769bb2963df7dea646901469e00
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="a205a-103">Guia de solução de problemas do Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a205a-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="a205a-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="a205a-104">Introduction</span></span>

<span data-ttu-id="a205a-105">O Gerenciador de Armazenamento do Microsoft Azure (Preview) é um aplicativo autônomo que permite que você trabalhe facilmente com dados do Armazenamento do Azure no Windows, no macOS e no Linux.</span><span class="sxs-lookup"><span data-stu-id="a205a-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="a205a-106">O aplicativo pode se conectar a contas de Armazenamento hospedadas no Azure, em nuvens independentes e no Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a205a-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="a205a-107">Este guia resume as soluções de problemas comuns encontrados no Gerenciador de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a205a-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="a205a-108">Problemas de entrada</span><span class="sxs-lookup"><span data-stu-id="a205a-108">Sign in issues</span></span>

<span data-ttu-id="a205a-109">Antes de continuar, tente reiniciar o aplicativo e verifique se os problemas podem ser corrigidos.</span><span class="sxs-lookup"><span data-stu-id="a205a-109">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="a205a-110">Erro: Certificado autoassinado na cadeia confiável</span><span class="sxs-lookup"><span data-stu-id="a205a-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="a205a-111">Você pode encontrar esse erro por vários motivos, os dois mais comuns são estes:</span><span class="sxs-lookup"><span data-stu-id="a205a-111">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="a205a-112">O aplicativo está conectado por meio de um "proxy transparente", o que significa que um servidor (como o servidor de sua empresa) está interceptando o tráfego HTTPS, descriptografando-o e, em seguida, criptografando usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="a205a-112">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="a205a-113">Você está executando um aplicativo, como um software antivírus, que está injetando um certificado SSL autoassinado para as mensagens HTTPS recebidas.</span><span class="sxs-lookup"><span data-stu-id="a205a-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="a205a-114">Quando o Gerenciador de Armazenamento encontra um dos problemas, ele não consegue mais saber se a mensagem HTTPS recebida foi violada.</span><span class="sxs-lookup"><span data-stu-id="a205a-114">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="a205a-115">Se você tiver uma cópia do certificado autoassinado, poderá permitir que o Gerenciador de Armazenamento confie nele.</span><span class="sxs-lookup"><span data-stu-id="a205a-115">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="a205a-116">Se você não tiver certeza de quem está injetando o certificado, execute estas etapas para encontrá-lo:</span><span class="sxs-lookup"><span data-stu-id="a205a-116">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="a205a-117">Instalar o Open SSL</span><span class="sxs-lookup"><span data-stu-id="a205a-117">Install Open SSL</span></span>

    - <span data-ttu-id="a205a-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (qualquer uma das versões leves deve ser suficiente)</span><span class="sxs-lookup"><span data-stu-id="a205a-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="a205a-119">Mac e Linux: deve estar incluído com o sistema operacional</span><span class="sxs-lookup"><span data-stu-id="a205a-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="a205a-120">Executar Open SSL</span><span class="sxs-lookup"><span data-stu-id="a205a-120">Run Open SSL</span></span>

    - <span data-ttu-id="a205a-121">Windows: abra o diretório de instalação, clique em **/bin/** e clique duas vezes em **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="a205a-121">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="a205a-122">Mac e Linux: execute **openssl** de um terminal.</span><span class="sxs-lookup"><span data-stu-id="a205a-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="a205a-123">Execute s_client -showcerts -connect microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="a205a-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="a205a-124">Procurar certificados autoassinados.</span><span class="sxs-lookup"><span data-stu-id="a205a-124">Look for self-signed certificates.</span></span> <span data-ttu-id="a205a-125">Se você não tiver certeza quais são autoassinados, procure onde o assunto ("s") e o emissor ("i") são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="a205a-125">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="a205a-126">Depois de encontrar os certificados autoassinados, para cada um deles, copie e cole tudo a partir, e incluindo, **---BEGIN CERTIFICATE---** até **---END CERTIFICATE---** em um novo arquivo .cer.</span><span class="sxs-lookup"><span data-stu-id="a205a-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="a205a-127">Abra o Gerenciador de Armazenamento, clique em **Editar** > **Certificados SSL** > **Importar Certificados** e, depois, use o seletor de arquivo para localizar, selecionar e abrir os arquivos .cer que você criou.</span><span class="sxs-lookup"><span data-stu-id="a205a-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="a205a-128">Se você não conseguir encontrar um certificado autoassinado usando as etapas acima, entre em contato conosco por meio da ferramenta de comentários para obter mais ajuda.</span><span class="sxs-lookup"><span data-stu-id="a205a-128">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="a205a-129">Não é possível recuperar as assinaturas</span><span class="sxs-lookup"><span data-stu-id="a205a-129">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="a205a-130">Se não for possível recuperar as assinaturas após a entrada bem-sucedida, execute estas etapas para solucionar esse problema:</span><span class="sxs-lookup"><span data-stu-id="a205a-130">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="a205a-131">Verifique se sua conta tem acesso às assinaturas entrando no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a205a-131">Verify that your account has access to the subscriptions by signing into the Azure Portal.</span></span>

- <span data-ttu-id="a205a-132">Verifique se você entrou usando o ambiente certo (Azure, Azure China, Azure Alemanha, Azure US Government nos ou Ambiente Personalizado/Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="a205a-132">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="a205a-133">Se você estiver atrás de um proxy, verifique se você configurou o proxy do Gerenciador de Armazenamento apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="a205a-133">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="a205a-134">Tente remover e readicionar a conta.</span><span class="sxs-lookup"><span data-stu-id="a205a-134">Try removing and readding the account.</span></span>

- <span data-ttu-id="a205a-135">Tente excluir os seguintes arquivos do diretório raiz (ou seja, C:\Usuários\ContosoUser) e, depois, adicione novamente a conta:</span><span class="sxs-lookup"><span data-stu-id="a205a-135">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="a205a-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="a205a-136">.adalcache</span></span>

    - <span data-ttu-id="a205a-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="a205a-137">.devaccounts</span></span>

    - <span data-ttu-id="a205a-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="a205a-138">.extaccounts</span></span>

- <span data-ttu-id="a205a-139">Fique atento ao console de ferramentas de desenvolvedor (pressionando F12) enquanto estiver tentando entrar para ver se aparecem mensagens de erro:</span><span class="sxs-lookup"><span data-stu-id="a205a-139">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![ferramentas de desenvolvedor](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="a205a-141">Não é possível ver a página de autenticação</span><span class="sxs-lookup"><span data-stu-id="a205a-141">Unable to see the authentication page</span></span>

<span data-ttu-id="a205a-142">Se não for possível ver a página de autenticação, execute estas etapas para solucionar esse problema:</span><span class="sxs-lookup"><span data-stu-id="a205a-142">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="a205a-143">Dependendo da velocidade de sua conexão, talvez demore algum tempo para a página de entrada carregar. Aguarde pelo menos um minuto antes de fechar a caixa de diálogo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="a205a-143">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="a205a-144">Se você estiver atrás de um proxy, verifique se você configurou o proxy do Gerenciador de Armazenamento apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="a205a-144">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="a205a-145">Exiba o console do desenvolvedor pressionando a tecla F12.</span><span class="sxs-lookup"><span data-stu-id="a205a-145">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="a205a-146">Veja as respostas no console do desenvolvedor e tente encontrar alguma dica do motivo do não funcionamento da autenticação.</span><span class="sxs-lookup"><span data-stu-id="a205a-146">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="a205a-147">Não é possível remover a conta</span><span class="sxs-lookup"><span data-stu-id="a205a-147">Cannot remove account</span></span>

<span data-ttu-id="a205a-148">Se você estiver conseguindo remover uma conta, ou se o link de reautenticação não responder, execute estas etapas para solucionar esse problema:</span><span class="sxs-lookup"><span data-stu-id="a205a-148">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="a205a-149">Tente excluir os seguintes arquivos do diretório raiz e adicione novamente a conta:</span><span class="sxs-lookup"><span data-stu-id="a205a-149">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="a205a-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="a205a-150">.adalcache</span></span>

    - <span data-ttu-id="a205a-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="a205a-151">.devaccounts</span></span>

    - <span data-ttu-id="a205a-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="a205a-152">.extaccounts</span></span>

- <span data-ttu-id="a205a-153">Se você quiser remover SAS associado a recursos de Armazenamento, exclua os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="a205a-153">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="a205a-154">Pasta %AppData%/StorageExplorer para Windows</span><span class="sxs-lookup"><span data-stu-id="a205a-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="a205a-155">/Usuários/<seu_nome>/Library/Applicaiton SUpport/StorageExplorer para Mac</span><span class="sxs-lookup"><span data-stu-id="a205a-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="a205a-156">~/.config/StorageExplorer para Linux</span><span class="sxs-lookup"><span data-stu-id="a205a-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="a205a-157">Será necessário reinserir todas as suas credenciais se você excluir esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="a205a-157">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="a205a-158">Problemas de proxy</span><span class="sxs-lookup"><span data-stu-id="a205a-158">Proxy issues</span></span>

<span data-ttu-id="a205a-159">Primeiro, certifique-se de que as seguintes informações inseridas estejam corretas:</span><span class="sxs-lookup"><span data-stu-id="a205a-159">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="a205a-160">A URL do proxy e o número da porta</span><span class="sxs-lookup"><span data-stu-id="a205a-160">The proxy URL and port number</span></span>

- <span data-ttu-id="a205a-161">Nome de usuário e senha, caso seja solicitado pelo proxy</span><span class="sxs-lookup"><span data-stu-id="a205a-161">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="a205a-162">Soluções comuns</span><span class="sxs-lookup"><span data-stu-id="a205a-162">Common solutions</span></span>

<span data-ttu-id="a205a-163">Se você ainda estiver enfrentando problemas, execute estas etapas para solucioná-los:</span><span class="sxs-lookup"><span data-stu-id="a205a-163">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="a205a-164">Se você puder se conectar à Internet sem usar o proxy, verifique se o Gerenciador de Armazenamento funciona sem as configurações de proxy habilitadas.</span><span class="sxs-lookup"><span data-stu-id="a205a-164">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="a205a-165">Se esse for o caso, talvez haja um problema com as configurações de proxy.</span><span class="sxs-lookup"><span data-stu-id="a205a-165">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="a205a-166">Trabalhe com seu administrador de proxy para identificar os problemas.</span><span class="sxs-lookup"><span data-stu-id="a205a-166">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="a205a-167">Verifique se outros aplicativos estão usando o servidor proxy conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="a205a-167">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="a205a-168">Verifique se você pode se conectar ao Portal do Microsoft Azure usando seu navegador da Web</span><span class="sxs-lookup"><span data-stu-id="a205a-168">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="a205a-169">Verifique se que você pode receber respostas de seus pontos de extremidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="a205a-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="a205a-170">Insira uma das suas URLs de ponto de extremidade em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="a205a-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="a205a-171">Se você puder se conectar, deverá receber um InvalidQueryParameterValue ou resposta XML semelhante.</span><span class="sxs-lookup"><span data-stu-id="a205a-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="a205a-172">Se outra pessoa também estiver usando o Gerenciador de Armazenamento com o servidor proxy, verifique se eles podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="a205a-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="a205a-173">Se eles puderem se conectar, talvez seja necessário entrar em contato com o administrador de seu servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="a205a-173">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="a205a-174">Ferramentas para diagnosticar problemas</span><span class="sxs-lookup"><span data-stu-id="a205a-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="a205a-175">Se você tiver ferramentas de rede, como o Fiddler para Windows, poderá diagnosticar os problemas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a205a-175">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="a205a-176">Se você tiver que trabalhar por meio do proxy, será necessário configurar a ferramenta de rede para se conectar por meio do proxy.</span><span class="sxs-lookup"><span data-stu-id="a205a-176">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="a205a-177">Verifique o número da porta usado por sua ferramenta de rede.</span><span class="sxs-lookup"><span data-stu-id="a205a-177">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="a205a-178">Insira a URL do host local e o número de porta da ferramenta de rede como configurações de proxy no Gerenciador de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a205a-178">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="a205a-179">Se isso for feito corretamente, a ferramenta de rede passará a registrar solicitações de rede feitas pelo Gerenciador de Armazenamento para pontos de extremidade de serviço e de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="a205a-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="a205a-180">Por exemplo, insira https://cawablobgrs.blob.core.windows.net/ do ponto de extremidade de blob em um navegador e você receberá uma resposta semelhante à seguinte, que sugere que o recurso existe, embora não seja possível acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="a205a-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![exemplo de código](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="a205a-182">Entre em contato com o administrador do servidor proxy</span><span class="sxs-lookup"><span data-stu-id="a205a-182">Contact proxy server admin</span></span>

<span data-ttu-id="a205a-183">Se as configurações de proxy estiverem corretas, talvez seja necessário entrar em contato com seu administrador de servidor proxy e</span><span class="sxs-lookup"><span data-stu-id="a205a-183">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="a205a-184">Verifique se o seu proxy não bloqueia o tráfego nos pontos de extremidade de gerenciamento ou recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="a205a-184">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="a205a-185">Verifique o protocolo de autenticação usado por seu servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="a205a-185">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="a205a-186">No momento, o Gerenciador de Armazenamento não dá suporte a proxies NTLM.</span><span class="sxs-lookup"><span data-stu-id="a205a-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="a205a-187">Mensagem de erro "Não é Possível Recuperar Filhos"</span><span class="sxs-lookup"><span data-stu-id="a205a-187">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="a205a-188">Se você estiver conectado ao Azure por meio de um proxy, verifique se as configurações do proxy estão corretas.</span><span class="sxs-lookup"><span data-stu-id="a205a-188">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="a205a-189">Se você tiver recebido acesso a um recurso do proprietário da assinatura ou conta, verifique se você tem permissões de leitura ou de lista para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a205a-189">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="a205a-190">Problemas com a URL SAS</span><span class="sxs-lookup"><span data-stu-id="a205a-190">Issues with SAS URL</span></span>
<span data-ttu-id="a205a-191">Se você estiver se conectando a um serviço usando uma URL SAS e enfrentando este erro:</span><span class="sxs-lookup"><span data-stu-id="a205a-191">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="a205a-192">Verifique se a URL fornece as permissões necessárias para ler ou lista recursos.</span><span class="sxs-lookup"><span data-stu-id="a205a-192">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="a205a-193">Verifique se a URL não expirou.</span><span class="sxs-lookup"><span data-stu-id="a205a-193">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="a205a-194">Se a URL SAS tiver base em uma política de acesso, verifique se a política de acesso não foi revogada.</span><span class="sxs-lookup"><span data-stu-id="a205a-194">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a205a-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a205a-195">Next steps</span></span>

<span data-ttu-id="a205a-196">Se nenhuma das soluções funcionar para você, envie seu problema por meio da ferramenta de comentários com seu email e com o máximo de detalhes possível sobre o problema, para que possamos entrar em contato com você para corrigir o problema.</span><span class="sxs-lookup"><span data-stu-id="a205a-196">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="a205a-197">Para fazer isso, clique no menu **Ajuda** e clique em **Enviar Comentários**.</span><span class="sxs-lookup"><span data-stu-id="a205a-197">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Comentários](./media/storage-explorer-troubleshooting/4022503_en_1.png)
