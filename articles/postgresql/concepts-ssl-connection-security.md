---
title: Configurar a conectividade SSL no Banco de Dados do Azure para PostgreSQL | Microsoft Docs
description: "Instruções e informações para configurar o Banco de Dados do Azure para PostgreSQL e aplicativos associados a fim de usar as conexões SSL adequadamente."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 685aa4c2f75b7c3260ca737f7c786157480b2d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="8ed51-103">Configurar a conectividade SSL no Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8ed51-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="8ed51-104">O Banco de dados do Azure para PostgreSQL prefere conectar-se seus aplicativos cliente ao serviço PostgreSQL usando o protocolo SSL.</span><span class="sxs-lookup"><span data-stu-id="8ed51-104">Azure Database for PostgreSQL prefers connecting your client applications to the PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="8ed51-105">Impor conexões SSL entre seu servidor de banco de dados e os aplicativos cliente ajuda a proteger contra ataques de "intermediários" criptografando o fluxo de dados entre o servidor e seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed51-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

<span data-ttu-id="8ed51-106">Por padrão, o serviço de banco de dados do PostgreSQL é configurado para exigir conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="8ed51-106">By default, the PostgreSQL database service is configured to require SSL connection.</span></span> <span data-ttu-id="8ed51-107">Como opção, você pode desabilitar a exigência de SSL para conectar ao seu serviço de banco de dados, se seu aplicativo cliente não oferecer suporte à conectividade SSL.</span><span class="sxs-lookup"><span data-stu-id="8ed51-107">Optionally, you can disable requiring SSL for connecting to your database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="8ed51-108">Impor conexões SSL</span><span class="sxs-lookup"><span data-stu-id="8ed51-108">Enforcing SSL connections</span></span>
<span data-ttu-id="8ed51-109">Para todos os Bancos de Dados do Azure para servidores PostgreSQL provisionados com o Portal e a CLI do Azure, a imposição de conexões SSL está habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="8ed51-109">For all Azure Database for PostgreSQL servers provisioned through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="8ed51-110">Da mesma forma, cadeias de conexão previamente definidas nas configurações de "Cadeias de Conexão" em seu servidor no Portal do Azure incluem os parâmetros necessários para linguagens comuns a fim de se conectar ao seu servidor de banco de dados usando SSL.</span><span class="sxs-lookup"><span data-stu-id="8ed51-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="8ed51-111">O parâmetro SSL varia de acordo com o conector, por exemplo "ssl=true" ou "sslmode=require" ou "sslmode=required" e outras variações.</span><span class="sxs-lookup"><span data-stu-id="8ed51-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="8ed51-112">Configurar a imposição de SSL</span><span class="sxs-lookup"><span data-stu-id="8ed51-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="8ed51-113">Como opção, você pode desabilitar a imposição da conectividade SSL.</span><span class="sxs-lookup"><span data-stu-id="8ed51-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="8ed51-114">O Microsoft Azure recomenda sempre habilitar a configuração **Impor conexão SSL** para melhorar a segurança.</span><span class="sxs-lookup"><span data-stu-id="8ed51-114">Microsoft Azure recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="8ed51-115">Usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8ed51-115">Using the Azure portal</span></span>
<span data-ttu-id="8ed51-116">Visite seu servidor de Banco de Dados do Azure para PostgreSQL e clique em **Segurança de conexão**.</span><span class="sxs-lookup"><span data-stu-id="8ed51-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="8ed51-117">Use o botão de alternância para habilitar ou desabilitar a configuração **Impor conexão SSL**.</span><span class="sxs-lookup"><span data-stu-id="8ed51-117">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="8ed51-118">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8ed51-118">Then click **Save**.</span></span> 

![Segurança de Conexão - Desabilitar a imposição de SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="8ed51-120">Você pode confirmar a configuração exibindo a página **Visão geral** para ver o indicador **Status de imposição de SSL**.</span><span class="sxs-lookup"><span data-stu-id="8ed51-120">You can confirm the setting by viewing the **Overview** page to see the **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="8ed51-121">Usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8ed51-121">Using Azure CLI</span></span>
<span data-ttu-id="8ed51-122">Você pode habilitar ou desabilitar o parâmetro **ssl-enforcement** usando os valores `Enabled` ou `Disabled` respectivamente na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed51-122">You can enable or disable the **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="8ed51-123">Verificar se o seu aplicativo ou sua estrutura oferece suporte a conexões SSL</span><span class="sxs-lookup"><span data-stu-id="8ed51-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="8ed51-124">Muitas estruturas de aplicativo comuns que usam PostgreSQL para serviços de banco de dados, como Drupal e Django, não habilitam o SSL por padrão durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="8ed51-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="8ed51-125">A habilitação da conectividade SSL deve ser feita após a instalação ou por meio de comandos da CLI específicos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed51-125">Enabling SSL connectivity must be done after installation or through CLI commands specific to the application.</span></span> <span data-ttu-id="8ed51-126">Se o seu servidor PostgreSQL estiver impondo conexões SSL, e o aplicativo associado não estiver configurado corretamente, a conexão do aplicativo ao seu servidor de banco de dados poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="8ed51-126">If your PostgreSQL server is enforcing SSL connections and the associated application is not configured properly, the application may fail to connect to your database server.</span></span> <span data-ttu-id="8ed51-127">Confira a documentação de seu aplicativo para saber como habilitar conexões SSL.</span><span class="sxs-lookup"><span data-stu-id="8ed51-127">Consult your application's documentation to learn how to enable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="8ed51-128">Aplicativos que exigem a verificação de certificado para conectividade SSL</span><span class="sxs-lookup"><span data-stu-id="8ed51-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="8ed51-129">Em alguns casos, os aplicativos exigem um arquivo de certificado local gerado de um arquivo de certificado (.cer) de uma Autoridade de Certificação (CA) confiável para se conectar com segurança.</span><span class="sxs-lookup"><span data-stu-id="8ed51-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) to connect securely.</span></span> <span data-ttu-id="8ed51-130">Veja as etapas a seguir para obter o arquivo .cer, decodificar o certificado e vinculá-lo ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ed51-130">See the following steps to obtain the .cer file, decode the certificate and bind it to your application.</span></span>

### <a name="download-the-certificate-file-from-the-certificate-authority-ca"></a><span data-ttu-id="8ed51-131">Baixar o arquivo de certificado da Autoridade de Certificação (CA)</span><span class="sxs-lookup"><span data-stu-id="8ed51-131">Download the certificate file from the Certificate Authority (CA)</span></span> 
<span data-ttu-id="8ed51-132">O certificado necessário para se comunicar por SSL com o servidor de Banco de Dados do Azure para PostgreSQL está [aqui](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="8ed51-132">The certificate needed to communicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="8ed51-133">Baixar o arquivo de certificado localmente.</span><span class="sxs-lookup"><span data-stu-id="8ed51-133">Download the certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="8ed51-134">Baixar e instalar o OpenSSL em seu computador</span><span class="sxs-lookup"><span data-stu-id="8ed51-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="8ed51-135">Para decodificar o arquivo de certificado exigido para conectar seu aplicativo com segurança ao servidor de banco de dados, instale o OpenSSL em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="8ed51-135">To decode the certificate file needed for your application to connect securely to your database server, you need to install OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="8ed51-136">Para Linux, OS X ou Unix</span><span class="sxs-lookup"><span data-stu-id="8ed51-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="8ed51-137">As bibliotecas OpenSSL são fornecidas diretamente no código-fonte a partir da [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="8ed51-137">The OpenSSL libraries are provided in source code directly from the [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="8ed51-138">As instruções a seguir orientarão você pelas etapas necessárias de instalação do OpenSSL no computador com Linux.</span><span class="sxs-lookup"><span data-stu-id="8ed51-138">The following instructions guide you through the steps necessary to install OpenSSL on your Linux PC.</span></span> <span data-ttu-id="8ed51-139">Este artigo usa comandos comprovadamente funcionais no Ubuntu 12.04 e superior.</span><span class="sxs-lookup"><span data-stu-id="8ed51-139">This article uses commands known to work on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="8ed51-140">Abra uma sessão de terminal e instale o OpenSSL</span><span class="sxs-lookup"><span data-stu-id="8ed51-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="8ed51-141">Extraia os arquivos do pacote baixado</span><span class="sxs-lookup"><span data-stu-id="8ed51-141">Extract the files from the download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="8ed51-142">Entre no diretório onde os arquivos foram extraídos.</span><span class="sxs-lookup"><span data-stu-id="8ed51-142">Enter the directory where the files were extracted.</span></span> <span data-ttu-id="8ed51-143">Por padrão, deve ser da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="8ed51-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="8ed51-144">Configure o OpenSSL executando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ed51-144">Configure OpenSSL by executing the following command.</span></span> <span data-ttu-id="8ed51-145">Se você quiser os arquivos em uma pasta diferente de /usr/local/openssl, altere o seguinte conforme for apropriado.</span><span class="sxs-lookup"><span data-stu-id="8ed51-145">If you want the files in a folder different than /usr/local/openssl, make sure to change the following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="8ed51-146">Agora que o OpenSSL está configurado corretamente, você precisa compilá-lo para converter seu certificado.</span><span class="sxs-lookup"><span data-stu-id="8ed51-146">Now that OpenSSL is configured properly, you need to compile it to convert your certificate.</span></span> <span data-ttu-id="8ed51-147">Para compilar, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8ed51-147">To compile, run the following command:</span></span>

```bash
make
```
<span data-ttu-id="8ed51-148">Após a conclusão da compilação, você estará pronto para instalar o OpenSSL como um executável, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8ed51-148">Once compiling is complete, you're ready to install OpenSSL as an executable by running the following command:</span></span>
```bash
make install
```
<span data-ttu-id="8ed51-149">Para confirmar a instalação bem-sucedida do OpenSSL em seu sistema, execute o comando a seguir e verifique se você obtém o mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="8ed51-149">To confirm that you've successfully installed OpenSSL on your system, run the following command and check to make sure you get the same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="8ed51-150">Se for bem-sucedida, você verá a seguinte mensagem.</span><span class="sxs-lookup"><span data-stu-id="8ed51-150">If successful you should see the following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="8ed51-151">Para Windows</span><span class="sxs-lookup"><span data-stu-id="8ed51-151">For Windows</span></span>
<span data-ttu-id="8ed51-152">A instalação do OpenSSL em um PC com Windows pode ser feita destas maneiras:</span><span class="sxs-lookup"><span data-stu-id="8ed51-152">Installing OpenSSL on a Windows PC can be done in the following ways:</span></span>
1. <span data-ttu-id="8ed51-153">**(Recomendado)** Usando a funcionalidade interna Bash para Windows no Windows 10 e superior, o OpenSSL é instalado por padrão.</span><span class="sxs-lookup"><span data-stu-id="8ed51-153">**(Recommended)** Using the built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="8ed51-154">As instruções sobre como habilitar a funcionalidade Bash para Windows no Windows 10 podem ser encontradas [aqui](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="8ed51-154">Instructions on how to enable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="8ed51-155">Por meio do download de um aplicativo Win32/64 fornecido pela comunidade.</span><span class="sxs-lookup"><span data-stu-id="8ed51-155">Through downloading a Win32/64 application provided by the community.</span></span> <span data-ttu-id="8ed51-156">Embora a OpenSSL Software Foundation não forneça, nem endosse, qualquer instalador específico do Windows, ela fornece uma lista dos instaladores disponíveis [aqui](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="8ed51-156">While the OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="8ed51-157">Decodificar o arquivo de certificado</span><span class="sxs-lookup"><span data-stu-id="8ed51-157">Decode your certificate file</span></span>
<span data-ttu-id="8ed51-158">O arquivo de CA Raiz baixado está em formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="8ed51-158">The downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="8ed51-159">Use o OpenSSL para decodificar o arquivo de certificado.</span><span class="sxs-lookup"><span data-stu-id="8ed51-159">Use OpenSSL to decode the certificate file.</span></span> <span data-ttu-id="8ed51-160">Para fazer isso, execute este comando OpenSSL:</span><span class="sxs-lookup"><span data-stu-id="8ed51-160">To do so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-to-azure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="8ed51-161">Conectar-se ao Banco de Dados do Azure para PostgreSQL com autenticação de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="8ed51-161">Connecting to Azure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="8ed51-162">Agora que você decodificou o certificado, pode conectar-se ao seu servidor de banco de dados com segurança por SSL.</span><span class="sxs-lookup"><span data-stu-id="8ed51-162">Now that you have successfully decoded your certificate, you can now connect to your database server securely over SSL.</span></span> <span data-ttu-id="8ed51-163">Para permitir a verificação do certificado do servidor, o certificado deve ser colocado no arquivo ~/.postgresql/root.crt, no diretório base do usuário.</span><span class="sxs-lookup"><span data-stu-id="8ed51-163">To allow server certificate verification, the certificate must be placed in the file ~/.postgresql/root.crt in the user's home directory.</span></span> <span data-ttu-id="8ed51-164">(No Microsoft Windows, o arquivo é chamado % APPDATA%\postgresql\root.crt.).</span><span class="sxs-lookup"><span data-stu-id="8ed51-164">(On Microsoft Windows the file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="8ed51-165">Veja a seguir instruções para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8ed51-165">The following provides instructions for connecting to Azure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed51-166">Atualmente, há um problema conhecido em que, se você usar "sslmode=verify-full" em sua conexão ao serviço, a conexão falhará com o seguinte erro: _o certificado do servidor para "&lt;region&gt;.control.database.windows.net" (e outros 7 nomes) não corresponde ao nome de host "&lt;servername&gt;.postgres.database.azure.com"._</span><span class="sxs-lookup"><span data-stu-id="8ed51-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection to the service, the connection will fail with the following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="8ed51-167">Se "sslmode=verify-full" for obrigatório, use a convenção de nomenclatura do servidor **&lt;servername&gt;.database.windows.net** como nome de host da cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="8ed51-167">If "sslmode=verify-full" is required, please use the server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="8ed51-168">Planejamos remover esta limitação no futuro.</span><span class="sxs-lookup"><span data-stu-id="8ed51-168">We plan to remove this limitation in the future.</span></span> <span data-ttu-id="8ed51-169">Conexões que usam outros [modos SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) devem continuar usando a convenção de nomenclatura de host preferenciais  **&lt;servername&gt;.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="8ed51-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue to use the preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="8ed51-170">Usar o utilitário de linha de comando psql</span><span class="sxs-lookup"><span data-stu-id="8ed51-170">Using psql command-line utility</span></span>
<span data-ttu-id="8ed51-171">O exemplo a seguir mostra como conectar-se ao servidor PostgreSQL usando o utilitário de linha de comando psql.</span><span class="sxs-lookup"><span data-stu-id="8ed51-171">The following example shows you how to successfully connect to your PostgreSQL server using the psql command-line utility.</span></span> <span data-ttu-id="8ed51-172">Use o arquivo `root.crt` criado e a opção `sslmode=verify-ca` ou `sslmode=verify-full`.</span><span class="sxs-lookup"><span data-stu-id="8ed51-172">Use the `root.crt` file created and the `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="8ed51-173">Usando a interface de linha de comando do PostgreSQL, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8ed51-173">Using the PostgreSQL command-line interface, execute the following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="8ed51-174">Se tiver êxito, você receberá o seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="8ed51-174">If successful, you receive the following output:</span></span>
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

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="8ed51-175">Usando a ferramenta GUI de pgAdmin</span><span class="sxs-lookup"><span data-stu-id="8ed51-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="8ed51-176">A configuração de pgAdmin 4 para se conectar com segurança via SSL exige que você defina `SSL mode = Verify-CA` ou `SSL mode = Verify-Full` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8ed51-176">Configuring pgAdmin 4 to connect securely over SSL requires you to set the `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Captura de tela de pgAdmin - conexão - modo SSL Require](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="8ed51-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ed51-178">Next steps</span></span>
<span data-ttu-id="8ed51-179">Analise as várias opções de conectividade do aplicativo em [Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="8ed51-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
