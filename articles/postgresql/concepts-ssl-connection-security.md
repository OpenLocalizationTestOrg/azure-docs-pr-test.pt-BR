---
title: conectividade SSL aaaConfigure no banco de dados do Azure para PostgreSQL | Microsoft Docs
description: "Instruções e informações tooconfigure banco de dados do Azure para PostgreSQL e aplicativos associados tooproperly usam conexões SSL."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="d02b2-103">Configurar a conectividade SSL no Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d02b2-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="d02b2-104">Banco de dados do Azure para PostgreSQL prefere conectando seu aplicativos de cliente toohello PostgreSQL serviço usando o protocolo (SSL).</span><span class="sxs-lookup"><span data-stu-id="d02b2-104">Azure Database for PostgreSQL prefers connecting your client applications toohello PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="d02b2-105">Impor conexões SSL entre o servidor de banco de dados e aplicativos cliente ajuda a proteger contra ataques "man no meio hello" criptografando o fluxo de dados de saudação entre o servidor de saudação e seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d02b2-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

<span data-ttu-id="d02b2-106">Por padrão, a saudação serviço de banco de dados PostgreSQL é configurado toorequire SSL conexão.</span><span class="sxs-lookup"><span data-stu-id="d02b2-106">By default, hello PostgreSQL database service is configured toorequire SSL connection.</span></span> <span data-ttu-id="d02b2-107">Opcionalmente, você pode desabilitar exigir SSL para conectar-se o serviço de banco de dados tooyour se seu aplicativo cliente não oferece suporte a conectividade SSL.</span><span class="sxs-lookup"><span data-stu-id="d02b2-107">Optionally, you can disable requiring SSL for connecting tooyour database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="d02b2-108">Impor conexões SSL</span><span class="sxs-lookup"><span data-stu-id="d02b2-108">Enforcing SSL connections</span></span>
<span data-ttu-id="d02b2-109">Para todos os banco de dados para servidores PostgreSQL provisionados com hello portal do Azure e a CLI, imposição de conexões SSL está habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="d02b2-109">For all Azure Database for PostgreSQL servers provisioned through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="d02b2-110">Da mesma forma, cadeias de caracteres de conexão previamente definidas nas configurações de "Cadeias de caracteres de Conexão" hello em seu servidor no portal do Azure de saudação incluem parâmetros de saudação necessária para comuns idiomas tooconnect tooyour servidor usando SSL.</span><span class="sxs-lookup"><span data-stu-id="d02b2-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="d02b2-111">Hello parâmetro SSL varia de acordo com o conector hello, por exemplo "ssl = true" ou "sslmode = exigem" ou "sslmode = necessária" e outras variações.</span><span class="sxs-lookup"><span data-stu-id="d02b2-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="d02b2-112">Configurar a imposição de SSL</span><span class="sxs-lookup"><span data-stu-id="d02b2-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="d02b2-113">Como opção, você pode desabilitar a imposição da conectividade SSL.</span><span class="sxs-lookup"><span data-stu-id="d02b2-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="d02b2-114">Microsoft Azure recomenda habilitar tooalways **conexão SSL impor** configuração de segurança aprimorada.</span><span class="sxs-lookup"><span data-stu-id="d02b2-114">Microsoft Azure recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="d02b2-115">Usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d02b2-115">Using hello Azure portal</span></span>
<span data-ttu-id="d02b2-116">Visite seu servidor de Banco de Dados do Azure para PostgreSQL e clique em **Segurança de conexão**.</span><span class="sxs-lookup"><span data-stu-id="d02b2-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="d02b2-117">Use tooenable de botão de alternância de saudação ou desabilite Olá **conexão SSL impor** configuração.</span><span class="sxs-lookup"><span data-stu-id="d02b2-117">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="d02b2-118">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d02b2-118">Then click **Save**.</span></span> 

![Segurança de Conexão - Desabilitar a imposição de SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="d02b2-120">Você pode confirmar configuração saudação exibindo Olá **visão geral** Olá de toosee página **SSL impor status** indicador.</span><span class="sxs-lookup"><span data-stu-id="d02b2-120">You can confirm hello setting by viewing hello **Overview** page toosee hello **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="d02b2-121">Usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d02b2-121">Using Azure CLI</span></span>
<span data-ttu-id="d02b2-122">Você pode habilitar ou desabilitar Olá **ssl imposição** usando o parâmetro `Enabled` ou `Disabled` valores respectivamente em CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d02b2-122">You can enable or disable hello **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="d02b2-123">Verificar se o seu aplicativo ou sua estrutura oferece suporte a conexões SSL</span><span class="sxs-lookup"><span data-stu-id="d02b2-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="d02b2-124">Muitas estruturas de aplicativo comuns que usam PostgreSQL para serviços de banco de dados, como Drupal e Django, não habilitam o SSL por padrão durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="d02b2-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="d02b2-125">Habilitando a conectividade SSL deve ser feito após a instalação ou por meio do aplicativo de toohello específica de comandos CLI.</span><span class="sxs-lookup"><span data-stu-id="d02b2-125">Enabling SSL connectivity must be done after installation or through CLI commands specific toohello application.</span></span> <span data-ttu-id="d02b2-126">Se seu servidor PostgreSQL é impor conexões SSL e o aplicativo hello associado não está configurado corretamente, o aplicativo hello pode falhar servidor de banco de dados de tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d02b2-126">If your PostgreSQL server is enforcing SSL connections and hello associated application is not configured properly, hello application may fail tooconnect tooyour database server.</span></span> <span data-ttu-id="d02b2-127">Consulte toolearn de documentação do seu aplicativo como tooenable as conexões SSL.</span><span class="sxs-lookup"><span data-stu-id="d02b2-127">Consult your application's documentation toolearn how tooenable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="d02b2-128">Aplicativos que exigem a verificação de certificado para conectividade SSL</span><span class="sxs-lookup"><span data-stu-id="d02b2-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="d02b2-129">Em alguns casos, os aplicativos exigem um arquivo de certificado local gerado a partir de um tooconnect de arquivo (. cer) de certificado de autoridade de certificação (CA) confiável com segurança.</span><span class="sxs-lookup"><span data-stu-id="d02b2-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) tooconnect securely.</span></span> <span data-ttu-id="d02b2-130">Consulte Olá seguir etapas tooobtain hello. cer arquivo, decodificar certificado hello e associá-lo tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d02b2-130">See hello following steps tooobtain hello .cer file, decode hello certificate and bind it tooyour application.</span></span>

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a><span data-ttu-id="d02b2-131">Baixar o arquivo de certificado de saudação do hello autoridade de certificação (CA)</span><span class="sxs-lookup"><span data-stu-id="d02b2-131">Download hello certificate file from hello Certificate Authority (CA)</span></span> 
<span data-ttu-id="d02b2-132">Olá certificado necessário toocommunicate por SSL com o banco de dados do Azure para PostgreSQL server está localizado [aqui](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="d02b2-132">hello certificate needed toocommunicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="d02b2-133">Baixe o arquivo do certificado Olá localmente.</span><span class="sxs-lookup"><span data-stu-id="d02b2-133">Download hello certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="d02b2-134">Baixar e instalar o OpenSSL em seu computador</span><span class="sxs-lookup"><span data-stu-id="d02b2-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="d02b2-135">arquivo de certificado Olá toodecode necessário para seu aplicativo tooconnect com segurança tooyour servidor de banco de dados, você precisa tooinstall OpenSSL no computador local.</span><span class="sxs-lookup"><span data-stu-id="d02b2-135">toodecode hello certificate file needed for your application tooconnect securely tooyour database server, you need tooinstall OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="d02b2-136">Para Linux, OS X ou Unix</span><span class="sxs-lookup"><span data-stu-id="d02b2-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="d02b2-137">bibliotecas do OpenSSL Olá são fornecidas no código-fonte diretamente da saudação [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="d02b2-137">hello OpenSSL libraries are provided in source code directly from hello [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="d02b2-138">Olá instruções a seguir orientam você na saudação de etapas necessárias tooinstall OpenSSL em seu computador Linux.</span><span class="sxs-lookup"><span data-stu-id="d02b2-138">hello following instructions guide you through hello steps necessary tooinstall OpenSSL on your Linux PC.</span></span> <span data-ttu-id="d02b2-139">Este artigo usa comandos conhecidos toowork no Ubuntu 12.04 e superior.</span><span class="sxs-lookup"><span data-stu-id="d02b2-139">This article uses commands known toowork on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="d02b2-140">Abra uma sessão de terminal e instale o OpenSSL</span><span class="sxs-lookup"><span data-stu-id="d02b2-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="d02b2-141">Extraia os arquivos de saudação do pacote de download de saudação</span><span class="sxs-lookup"><span data-stu-id="d02b2-141">Extract hello files from hello download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="d02b2-142">Insira o diretório de saudação onde os arquivos de saudação foram extraídos.</span><span class="sxs-lookup"><span data-stu-id="d02b2-142">Enter hello directory where hello files were extracted.</span></span> <span data-ttu-id="d02b2-143">Por padrão, deve ser da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="d02b2-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="d02b2-144">Configure o OpenSSL executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="d02b2-144">Configure OpenSSL by executing hello following command.</span></span> <span data-ttu-id="d02b2-145">Se desejar Olá arquivos em uma pasta diferente de /usr/local/openssl, verifique toochange se Olá a seguir conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="d02b2-145">If you want hello files in a folder different than /usr/local/openssl, make sure toochange hello following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="d02b2-146">Agora que o OpenSSL está configurado corretamente, você precisa toocompile-tooconvert seu certificado.</span><span class="sxs-lookup"><span data-stu-id="d02b2-146">Now that OpenSSL is configured properly, you need toocompile it tooconvert your certificate.</span></span> <span data-ttu-id="d02b2-147">toocompile, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d02b2-147">toocompile, run hello following command:</span></span>

```bash
make
```
<span data-ttu-id="d02b2-148">Após a compilação for concluída, você está pronto tooinstall OpenSSL como um executável executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d02b2-148">Once compiling is complete, you're ready tooinstall OpenSSL as an executable by running hello following command:</span></span>
```bash
make install
```
<span data-ttu-id="d02b2-149">tooconfirm que você instalou o OpenSSL com êxito em seu sistema, comando Olá execução a seguir e verifique toomake-se de obter Olá mesma saída.</span><span class="sxs-lookup"><span data-stu-id="d02b2-149">tooconfirm that you've successfully installed OpenSSL on your system, run hello following command and check toomake sure you get hello same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="d02b2-150">Se for bem-sucedido você verá a seguinte mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d02b2-150">If successful you should see hello following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="d02b2-151">Para Windows</span><span class="sxs-lookup"><span data-stu-id="d02b2-151">For Windows</span></span>
<span data-ttu-id="d02b2-152">Instalar o OpenSSL em um PC Windows pode ser feito em Olá maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="d02b2-152">Installing OpenSSL on a Windows PC can be done in hello following ways:</span></span>
1. <span data-ttu-id="d02b2-153">**(Recomendado)**  Usando funcionalidade interna de Bash para Windows hello no Windows 10 e acima, o OpenSSL está instalado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d02b2-153">**(Recommended)** Using hello built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="d02b2-154">Instruções sobre como tooenable funcionalidade Bash para Windows no Windows 10 pode ser encontrado [aqui](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="d02b2-154">Instructions on how tooenable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="d02b2-155">Por meio de download de um aplicativo Win32/64 fornecido pela comunidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="d02b2-155">Through downloading a Win32/64 application provided by hello community.</span></span> <span data-ttu-id="d02b2-156">Enquanto Olá OpenSSL Software Foundation não fornecer nem endossa qualquer instaladores específicos do Windows, eles fornecem uma lista de instaladores disponíveis [aqui](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="d02b2-156">While hello OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="d02b2-157">Decodificar o arquivo de certificado</span><span class="sxs-lookup"><span data-stu-id="d02b2-157">Decode your certificate file</span></span>
<span data-ttu-id="d02b2-158">Olá baixado da autoridade de certificação raiz arquivo está em formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="d02b2-158">hello downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="d02b2-159">Use o arquivo de certificado do OpenSSL toodecode hello.</span><span class="sxs-lookup"><span data-stu-id="d02b2-159">Use OpenSSL toodecode hello certificate file.</span></span> <span data-ttu-id="d02b2-160">toodo assim, execute este comando OpenSSL:</span><span class="sxs-lookup"><span data-stu-id="d02b2-160">toodo so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="d02b2-161">Conexão tooAzure banco de dados PostgreSQL com autenticação de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="d02b2-161">Connecting tooAzure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="d02b2-162">Agora que você tenha com êxito decodificado seu certificado, você pode agora conectar tooyour servidor de banco de dados com segurança por SSL.</span><span class="sxs-lookup"><span data-stu-id="d02b2-162">Now that you have successfully decoded your certificate, you can now connect tooyour database server securely over SSL.</span></span> <span data-ttu-id="d02b2-163">verificação de certificado do servidor tooallow, certificado Olá deve ser colocado em Olá arquivo ~/.postgresql/root.crt no diretório base do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="d02b2-163">tooallow server certificate verification, hello certificate must be placed in hello file ~/.postgresql/root.crt in hello user's home directory.</span></span> <span data-ttu-id="d02b2-164">(No arquivo do Microsoft Windows hello é denominada % APPDATA%\postgresql\root.crt.).</span><span class="sxs-lookup"><span data-stu-id="d02b2-164">(On Microsoft Windows hello file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="d02b2-165">a seguir Olá fornece instruções para conectar tooAzure banco de dados para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d02b2-165">hello following provides instructions for connecting tooAzure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="d02b2-166">Atualmente, há um problema conhecido se você usar "sslmode = verificar-full" em seu serviço de toohello de conexão, a conexão Olá falhará com hello erro a seguir: _certificado do servidor para "&lt;região&gt;. Control.Database.Windows.NET"(e 7 outros nomes) não coincide com o nome de host"&lt;servername&gt;. postgres.database.azure.com "._</span><span class="sxs-lookup"><span data-stu-id="d02b2-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection toohello service, hello connection will fail with hello following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="d02b2-167">Se "sslmode = completo verificar" é necessário, use a convenção de nomenclatura de servidor de saudação  **&lt;servername&gt;. t** como seu nome de host de cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="d02b2-167">If "sslmode=verify-full" is required, please use hello server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="d02b2-168">Planejamos tooremove esta limitação no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="d02b2-168">We plan tooremove this limitation in hello future.</span></span> <span data-ttu-id="d02b2-169">Conexões usando outros [modos SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) devem continuar a convenção de nomenclatura Olá preferido host toouse  **&lt;servername&gt;. postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="d02b2-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue toouse hello preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="d02b2-170">Usar o utilitário de linha de comando psql</span><span class="sxs-lookup"><span data-stu-id="d02b2-170">Using psql command-line utility</span></span>
<span data-ttu-id="d02b2-171">saudação de exemplo a seguir mostra como toosuccessfully conectar tooyour PostgreSQL servidor usando o utilitário de linha de comando do hello psql.</span><span class="sxs-lookup"><span data-stu-id="d02b2-171">hello following example shows you how toosuccessfully connect tooyour PostgreSQL server using hello psql command-line utility.</span></span> <span data-ttu-id="d02b2-172">Saudação de uso `root.crt` arquivo criado e hello `sslmode=verify-ca` ou `sslmode=verify-full` opção.</span><span class="sxs-lookup"><span data-stu-id="d02b2-172">Use hello `root.crt` file created and hello `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="d02b2-173">Usando a interface de linha de comando do hello PostgreSQL, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d02b2-173">Using hello PostgreSQL command-line interface, execute hello following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="d02b2-174">Se for bem-sucedido, você receberá Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="d02b2-174">If successful, you receive hello following output:</span></span>
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="d02b2-175">Usando a ferramenta GUI de pgAdmin</span><span class="sxs-lookup"><span data-stu-id="d02b2-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="d02b2-176">Configurar pgAdmin 4 tooconnect com segurança por SSL requer Olá tooset `SSL mode = Verify-CA` ou `SSL mode = Verify-Full` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d02b2-176">Configuring pgAdmin 4 tooconnect securely over SSL requires you tooset hello `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Captura de tela de pgAdmin - conexão - modo SSL Require](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="d02b2-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d02b2-178">Next steps</span></span>
<span data-ttu-id="d02b2-179">Analise as várias opções de conectividade do aplicativo em [Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="d02b2-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
