---
title: "Guia de solução de problemas de Gerenciador de armazenamento aaaAzure | Microsoft Docs"
description: "Visão geral do recurso de depuração de dois de saudação do Azure"
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
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="76296-103">Guia de solução de problemas do Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="76296-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="76296-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="76296-104">Introduction</span></span>

<span data-ttu-id="76296-105">Gerenciador de armazenamento do Microsoft Azure (visualização) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Windows e Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="76296-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="76296-106">Olá aplicativo pode se conectar a contas toStorage hospedadas no Azure, Sovereign nuvens e pilha do Azure.</span><span class="sxs-lookup"><span data-stu-id="76296-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="76296-107">Este guia resume as soluções de problemas comuns encontrados no Gerenciador de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76296-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="76296-108">Problemas de entrada</span><span class="sxs-lookup"><span data-stu-id="76296-108">Sign in issues</span></span>

<span data-ttu-id="76296-109">Somente contas do AAD (Azure Active Directory) têm suporte.</span><span class="sxs-lookup"><span data-stu-id="76296-109">Only Azure Active Directory (AAD) accounts are supported.</span></span> <span data-ttu-id="76296-110">Se você usar uma conta do AD FS, espera-se que a assinatura no tooStorage que Explorer não funcionará.</span><span class="sxs-lookup"><span data-stu-id="76296-110">If you use an ADFS account, it’s expected that signing in tooStorage Explorer would not work.</span></span> <span data-ttu-id="76296-111">Antes de continuar, tente reiniciar o aplicativo e veja se os problemas de saudação podem ser corrigidos.</span><span class="sxs-lookup"><span data-stu-id="76296-111">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="76296-112">Erro: Certificado autoassinado na cadeia confiável</span><span class="sxs-lookup"><span data-stu-id="76296-112">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="76296-113">Há várias razões por que você pode encontrar esse erro, e dois motivos de hello mais comuns são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="76296-113">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="76296-114">Olá aplicativo está conectado por meio de um "proxy transparente", que significa que um servidor (como o servidor da sua empresa) é interceptar o tráfego HTTPS, descriptografá-los e, em seguida, criptografar usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="76296-114">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="76296-115">Você está executando um aplicativo, como software antivírus, que está injetando um certificado SSL autoassinado em mensagens de saudação do HTTPS que você receber.</span><span class="sxs-lookup"><span data-stu-id="76296-115">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="76296-116">Quando o Gerenciador de armazenamento encontra um dos problemas hello, pode não saber se a mensagem de saudação recebida do HTTPS foi violada.</span><span class="sxs-lookup"><span data-stu-id="76296-116">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="76296-117">Se você tiver uma cópia do certificado autoassinado hello, você pode deixar o Gerenciador de armazenamento deve confiar nele.</span><span class="sxs-lookup"><span data-stu-id="76296-117">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="76296-118">Se você não tiver certeza de que está injetando certificado hello, siga estas etapas toofind-lo:</span><span class="sxs-lookup"><span data-stu-id="76296-118">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="76296-119">Instalar o Open SSL</span><span class="sxs-lookup"><span data-stu-id="76296-119">Install Open SSL</span></span>

    - <span data-ttu-id="76296-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (qualquer uma das versões de luz Olá deve ser suficiente)</span><span class="sxs-lookup"><span data-stu-id="76296-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="76296-121">Mac e Linux: deve estar incluído com o sistema operacional</span><span class="sxs-lookup"><span data-stu-id="76296-121">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="76296-122">Executar Open SSL</span><span class="sxs-lookup"><span data-stu-id="76296-122">Run Open SSL</span></span>

    - <span data-ttu-id="76296-123">Windows: Abra o diretório de instalação de saudação, clique em **/bin/**e, em seguida, clique duas vezes em **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="76296-123">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="76296-124">Mac e Linux: execute **openssl** de um terminal.</span><span class="sxs-lookup"><span data-stu-id="76296-124">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="76296-125">Execute s_client -showcerts -connect microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="76296-125">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="76296-126">Procurar certificados autoassinados.</span><span class="sxs-lookup"><span data-stu-id="76296-126">Look for self-signed certificates.</span></span> <span data-ttu-id="76296-127">Se você não tiver certeza de que são autoassinado, procure em qualquer lugar assunto hello ("s") e emissor ("i") são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="76296-127">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="76296-128">Quando localizar todos os certificados autoassinados, para cada um, copie e cole-tudo a partir e incluindo **---iniciar certificado---** muito**---concluir certificado---** tooa novo arquivo de. cer.</span><span class="sxs-lookup"><span data-stu-id="76296-128">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="76296-129">Abra o Gerenciador de armazenamento, clique em **editar** > **certificados SSL** > **importar certificados**e, em seguida, use Olá arquivo seletor toofind, selecione, e abra hello. cer que você criou.</span><span class="sxs-lookup"><span data-stu-id="76296-129">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="76296-130">Se você não encontrar todos os certificados autoassinados usando Olá acima etapas, entre em contato conosco por meio da ferramenta de comentários Olá para obter mais ajuda.</span><span class="sxs-lookup"><span data-stu-id="76296-130">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="76296-131">Não é possível tooretrieve assinaturas</span><span class="sxs-lookup"><span data-stu-id="76296-131">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="76296-132">Se você não é possível tooretrieve suas assinaturas depois que você entre com êxito, siga essas etapas tootroubleshoot esse problema:</span><span class="sxs-lookup"><span data-stu-id="76296-132">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="76296-133">Verifique se sua conta tem acesso toohello assinaturas ao entrar em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="76296-133">Verify that your account has access toohello subscriptions by signing into hello Azure portal.</span></span>

- <span data-ttu-id="76296-134">Certifique-se de que você entrou usando o ambiente correto de saudação (do Azure, do Azure na China, Alemanha do Azure, Azure US Government ou personalizado do Azure/ambiente pilha).</span><span class="sxs-lookup"><span data-stu-id="76296-134">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="76296-135">Se você estiver atrás de um proxy, certifique-se de que você tenha configurado proxy de Gerenciador de armazenamento Olá corretamente.</span><span class="sxs-lookup"><span data-stu-id="76296-135">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="76296-136">Tente remover e lendo a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="76296-136">Try removing and readding hello account.</span></span>

- <span data-ttu-id="76296-137">Tente excluir Olá seguintes arquivos do diretório raiz (ou seja, C:\Users\ContosoUser) e, em seguida, adicionar novamente conta hello:</span><span class="sxs-lookup"><span data-stu-id="76296-137">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="76296-138">.adalcache</span><span class="sxs-lookup"><span data-stu-id="76296-138">.adalcache</span></span>

    - <span data-ttu-id="76296-139">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="76296-139">.devaccounts</span></span>

    - <span data-ttu-id="76296-140">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="76296-140">.extaccounts</span></span>

- <span data-ttu-id="76296-141">Console de ferramentas de desenvolvedor inspecionar hello (pressionando F12) quando você está tentando entrar para as mensagens de erro:</span><span class="sxs-lookup"><span data-stu-id="76296-141">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![ferramentas de desenvolvedor](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="76296-143">Página de autenticação não é possível toosee Olá</span><span class="sxs-lookup"><span data-stu-id="76296-143">Unable toosee hello authentication page</span></span>

<span data-ttu-id="76296-144">Se você página de autenticação Olá toosee não é possível, siga essas etapas tootroubleshoot esse problema:</span><span class="sxs-lookup"><span data-stu-id="76296-144">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="76296-145">Dependendo da velocidade da saudação de sua conexão, ele pode levar algum tempo para tooload de página de entrada hello, aguarde pelo menos um minuto antes de fechar a caixa de diálogo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="76296-145">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="76296-146">Se você estiver atrás de um proxy, certifique-se de que você tenha configurado proxy de Gerenciador de armazenamento Olá corretamente.</span><span class="sxs-lookup"><span data-stu-id="76296-146">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="76296-147">Exibir o console do desenvolvedor hello, pressionando a tecla F12 de saudação.</span><span class="sxs-lookup"><span data-stu-id="76296-147">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="76296-148">Assista a respostas de saudação do console do desenvolvedor hello e ver se você pode encontrar qualquer dica de por que a autenticação não está funcionando.</span><span class="sxs-lookup"><span data-stu-id="76296-148">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="76296-149">Não é possível remover a conta</span><span class="sxs-lookup"><span data-stu-id="76296-149">Cannot remove account</span></span>

<span data-ttu-id="76296-150">Se você não é possível tooremove uma conta, ou se Olá reautenticar link não faz nada, siga essas etapas tootroubleshoot esse problema:</span><span class="sxs-lookup"><span data-stu-id="76296-150">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="76296-151">Tente excluir Olá seguintes arquivos do diretório raiz e, em seguida, lendo conta hello:</span><span class="sxs-lookup"><span data-stu-id="76296-151">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="76296-152">.adalcache</span><span class="sxs-lookup"><span data-stu-id="76296-152">.adalcache</span></span>

    - <span data-ttu-id="76296-153">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="76296-153">.devaccounts</span></span>

    - <span data-ttu-id="76296-154">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="76296-154">.extaccounts</span></span>

- <span data-ttu-id="76296-155">Se você quiser tooremove SAS anexado recursos de armazenamento, exclua Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="76296-155">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="76296-156">Pasta %AppData%/StorageExplorer para Windows</span><span class="sxs-lookup"><span data-stu-id="76296-156">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="76296-157">/Usuários/<seu_nome>/Library/Applicaiton SUpport/StorageExplorer para Mac</span><span class="sxs-lookup"><span data-stu-id="76296-157">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="76296-158">~/.config/StorageExplorer para Linux</span><span class="sxs-lookup"><span data-stu-id="76296-158">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="76296-159">Você terá tooreenter todas as suas credenciais se você excluir esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="76296-159">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="76296-160">Problemas de proxy</span><span class="sxs-lookup"><span data-stu-id="76296-160">Proxy issues</span></span>

<span data-ttu-id="76296-161">Primeiro, certifique-se de que Olá segue as informações inseridas estão corretas:</span><span class="sxs-lookup"><span data-stu-id="76296-161">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="76296-162">Olá URL do proxy e a porta número</span><span class="sxs-lookup"><span data-stu-id="76296-162">hello proxy URL and port number</span></span>

- <span data-ttu-id="76296-163">Nome de usuário e senha, se exigido pelo proxy Olá</span><span class="sxs-lookup"><span data-stu-id="76296-163">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="76296-164">Soluções comuns</span><span class="sxs-lookup"><span data-stu-id="76296-164">Common solutions</span></span>

<span data-ttu-id="76296-165">Se você ainda estiver tendo problemas, siga estas etapas tootroubleshoot-los:</span><span class="sxs-lookup"><span data-stu-id="76296-165">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="76296-166">Se você puder se conectar toohello Internet sem usar o proxy, verifique se o Gerenciador de armazenamento funciona sem as configurações de proxy habilitadas.</span><span class="sxs-lookup"><span data-stu-id="76296-166">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="76296-167">Se esse for o caso de Olá, pode haver um problema com as configurações de proxy.</span><span class="sxs-lookup"><span data-stu-id="76296-167">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="76296-168">Trabalhar com seus problemas de saudação do proxy administrador tooidentify.</span><span class="sxs-lookup"><span data-stu-id="76296-168">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="76296-169">Verifique se outros aplicativos usando o servidor de proxy Olá funcionam conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="76296-169">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="76296-170">Verifique se que você pode conectar o portal do Microsoft Azure toohello usando seu navegador da web</span><span class="sxs-lookup"><span data-stu-id="76296-170">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="76296-171">Verifique se que você pode receber respostas de seus pontos de extremidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="76296-171">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="76296-172">Insira uma das suas URLs de ponto de extremidade em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="76296-172">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="76296-173">Se você puder se conectar, deverá receber um InvalidQueryParameterValue ou resposta XML semelhante.</span><span class="sxs-lookup"><span data-stu-id="76296-173">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="76296-174">Se outra pessoa também estiver usando o Gerenciador de Armazenamento com o servidor proxy, verifique se eles podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="76296-174">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="76296-175">Se eles possam se conectar, você pode ter toocontact seu administrador do servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="76296-175">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="76296-176">Ferramentas para diagnosticar problemas</span><span class="sxs-lookup"><span data-stu-id="76296-176">Tools for diagnosing issues</span></span>

<span data-ttu-id="76296-177">Se você tem ferramentas de rede, como o Fiddler para Windows, você pode ser capaz de toodiagnose problemas de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="76296-177">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="76296-178">Se você tiver toowork por meio do proxy, você pode ter tooconfigure seu tooconnect ferramenta rede por meio do proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="76296-178">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="76296-179">Verifique o número da porta Olá usada pela ferramenta de sua rede.</span><span class="sxs-lookup"><span data-stu-id="76296-179">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="76296-180">Digite a URL de host local de saudação e Olá número da porta da ferramenta de rede como configurações de proxy no Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76296-180">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="76296-181">Se isso for feito corretamente, a sua rede ferramenta inicia o log de solicitações de rede feitas pelos pontos de extremidade toomanagement e o serviço do Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76296-181">If this is done correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="76296-182">Por exemplo, digite https://cawablobgrs.blob.core.windows.net/ para seu ponto de extremidade de blob em um navegador e você receberá uma resposta semelhante Olá seguinte, o que sugere Olá recurso existir, embora você não pode acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="76296-182">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![exemplo de código](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="76296-184">Entre em contato com o administrador do servidor proxy</span><span class="sxs-lookup"><span data-stu-id="76296-184">Contact proxy server admin</span></span>

<span data-ttu-id="76296-185">Se as configurações de proxy estão corretas, você poderá ter toocontact seu administrador do servidor proxy, e</span><span class="sxs-lookup"><span data-stu-id="76296-185">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="76296-186">Verifique se o proxy não bloqueia o tráfego tooAzure gerenciamento ou o recurso de pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="76296-186">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="76296-187">Verifique se o protocolo de autenticação de saudação usado pelo servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="76296-187">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="76296-188">No momento, o Gerenciador de Armazenamento não dá suporte a proxies NTLM.</span><span class="sxs-lookup"><span data-stu-id="76296-188">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="76296-189">Mensagem de erro "Não é possível tooRetrieve filhos"</span><span class="sxs-lookup"><span data-stu-id="76296-189">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="76296-190">Se você estiver conectado tooAzure através de um proxy, verificar se as configurações de proxy estão corretas.</span><span class="sxs-lookup"><span data-stu-id="76296-190">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="76296-191">Se você foi concedido acesso tooa recursos proprietário de saudação da saudação assinatura ou conta, verifique se você leu ou lista de permissões para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="76296-191">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="76296-192">Problemas com a URL SAS</span><span class="sxs-lookup"><span data-stu-id="76296-192">Issues with SAS URL</span></span>
<span data-ttu-id="76296-193">Se você estiver se conectando tooa serviço usando uma URL SAS e apresentando este erro:</span><span class="sxs-lookup"><span data-stu-id="76296-193">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="76296-194">Verifique se Olá URL contém as permissões necessárias Olá tooread ou lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="76296-194">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="76296-195">Verifique se esse Olá que URL não expirou.</span><span class="sxs-lookup"><span data-stu-id="76296-195">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="76296-196">Se Olá URL SAS é baseado em uma política de acesso, verifique se a política de acesso Olá não foi revogada.</span><span class="sxs-lookup"><span data-stu-id="76296-196">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76296-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="76296-197">Next steps</span></span>

<span data-ttu-id="76296-198">Se nenhuma das soluções de saudação funcionar para você, enviar seu problema por meio da ferramenta de comentários do hello com seu email e como muitos detalhes sobre o problema Olá incluídos como você podem, para que possamos contatá-lo para corrigir o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="76296-198">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="76296-199">toodo, clique **ajuda** menu e clique **enviar comentários**.</span><span class="sxs-lookup"><span data-stu-id="76296-199">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Comentários](./media/storage-explorer-troubleshooting/4022503_en_1.png)
