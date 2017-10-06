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
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>Configurar a conectividade SSL no Banco de Dados do Azure para PostgreSQL
Banco de dados do Azure para PostgreSQL prefere conectando seu aplicativos de cliente toohello PostgreSQL serviço usando o protocolo (SSL). Impor conexões SSL entre o servidor de banco de dados e aplicativos cliente ajuda a proteger contra ataques "man no meio hello" criptografando o fluxo de dados de saudação entre o servidor de saudação e seu aplicativo.

Por padrão, a saudação serviço de banco de dados PostgreSQL é configurado toorequire SSL conexão. Opcionalmente, você pode desabilitar exigir SSL para conectar-se o serviço de banco de dados tooyour se seu aplicativo cliente não oferece suporte a conectividade SSL. 

## <a name="enforcing-ssl-connections"></a>Impor conexões SSL
Para todos os banco de dados para servidores PostgreSQL provisionados com hello portal do Azure e a CLI, imposição de conexões SSL está habilitada por padrão. 

Da mesma forma, cadeias de caracteres de conexão previamente definidas nas configurações de "Cadeias de caracteres de Conexão" hello em seu servidor no portal do Azure de saudação incluem parâmetros de saudação necessária para comuns idiomas tooconnect tooyour servidor usando SSL. Hello parâmetro SSL varia de acordo com o conector hello, por exemplo "ssl = true" ou "sslmode = exigem" ou "sslmode = necessária" e outras variações.

## <a name="configure-enforcement-of-ssl"></a>Configurar a imposição de SSL
Como opção, você pode desabilitar a imposição da conectividade SSL. Microsoft Azure recomenda habilitar tooalways **conexão SSL impor** configuração de segurança aprimorada.

### <a name="using-hello-azure-portal"></a>Usando Olá portal do Azure
Visite seu servidor de Banco de Dados do Azure para PostgreSQL e clique em **Segurança de conexão**. Use tooenable de botão de alternância de saudação ou desabilite Olá **conexão SSL impor** configuração. Em seguida, clique em **Salvar**. 

![Segurança de Conexão - Desabilitar a imposição de SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

Você pode confirmar configuração saudação exibindo Olá **visão geral** Olá de toosee página **SSL impor status** indicador.

### <a name="using-azure-cli"></a>Usando a CLI do Azure
Você pode habilitar ou desabilitar Olá **ssl imposição** usando o parâmetro `Enabled` ou `Disabled` valores respectivamente em CLI do Azure.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>Verificar se o seu aplicativo ou sua estrutura oferece suporte a conexões SSL
Muitas estruturas de aplicativo comuns que usam PostgreSQL para serviços de banco de dados, como Drupal e Django, não habilitam o SSL por padrão durante a instalação. Habilitando a conectividade SSL deve ser feito após a instalação ou por meio do aplicativo de toohello específica de comandos CLI. Se seu servidor PostgreSQL é impor conexões SSL e o aplicativo hello associado não está configurado corretamente, o aplicativo hello pode falhar servidor de banco de dados de tooyour tooconnect. Consulte toolearn de documentação do seu aplicativo como tooenable as conexões SSL.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>Aplicativos que exigem a verificação de certificado para conectividade SSL
Em alguns casos, os aplicativos exigem um arquivo de certificado local gerado a partir de um tooconnect de arquivo (. cer) de certificado de autoridade de certificação (CA) confiável com segurança. Consulte Olá seguir etapas tooobtain hello. cer arquivo, decodificar certificado hello e associá-lo tooyour aplicativo.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Baixar o arquivo de certificado de saudação do hello autoridade de certificação (CA) 
Olá certificado necessário toocommunicate por SSL com o banco de dados do Azure para PostgreSQL server está localizado [aqui](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt). Baixe o arquivo do certificado Olá localmente.

### <a name="download-and-install-openssl-on-your-machine"></a>Baixar e instalar o OpenSSL em seu computador 
arquivo de certificado Olá toodecode necessário para seu aplicativo tooconnect com segurança tooyour servidor de banco de dados, você precisa tooinstall OpenSSL no computador local.

#### <a name="for-linux-os-x-or-unix"></a>Para Linux, OS X ou Unix
bibliotecas do OpenSSL Olá são fornecidas no código-fonte diretamente da saudação [OpenSSL Software Foundation](http://www.openssl.org). Olá instruções a seguir orientam você na saudação de etapas necessárias tooinstall OpenSSL em seu computador Linux. Este artigo usa comandos conhecidos toowork no Ubuntu 12.04 e superior.

Abra uma sessão de terminal e instale o OpenSSL
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Extraia os arquivos de saudação do pacote de download de saudação
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Insira o diretório de saudação onde os arquivos de saudação foram extraídos. Por padrão, deve ser da seguinte maneira.

```bash
cd openssl-1.1.0e
```
Configure o OpenSSL executando o comando a seguir de saudação. Se desejar Olá arquivos em uma pasta diferente de /usr/local/openssl, verifique toochange se Olá a seguir conforme apropriado.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
Agora que o OpenSSL está configurado corretamente, você precisa toocompile-tooconvert seu certificado. toocompile, execute Olá comando a seguir:

```bash
make
```
Após a compilação for concluída, você está pronto tooinstall OpenSSL como um executável executando Olá comando a seguir:
```bash
make install
```
tooconfirm que você instalou o OpenSSL com êxito em seu sistema, comando Olá execução a seguir e verifique toomake-se de obter Olá mesma saída.

```bash
/usr/local/openssl/bin/openssl version
```
Se for bem-sucedido você verá a seguinte mensagem de saudação.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Para Windows
Instalar o OpenSSL em um PC Windows pode ser feito em Olá maneiras a seguir:
1. **(Recomendado)**  Usando funcionalidade interna de Bash para Windows hello no Windows 10 e acima, o OpenSSL está instalado por padrão. Instruções sobre como tooenable funcionalidade Bash para Windows no Windows 10 pode ser encontrado [aqui](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).
2. Por meio de download de um aplicativo Win32/64 fornecido pela comunidade de saudação. Enquanto Olá OpenSSL Software Foundation não fornecer nem endossa qualquer instaladores específicos do Windows, eles fornecem uma lista de instaladores disponíveis [aqui](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>Decodificar o arquivo de certificado
Olá baixado da autoridade de certificação raiz arquivo está em formato criptografado. Use o arquivo de certificado do OpenSSL toodecode hello. toodo assim, execute este comando OpenSSL:

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>Conexão tooAzure banco de dados PostgreSQL com autenticação de certificado SSL
Agora que você tenha com êxito decodificado seu certificado, você pode agora conectar tooyour servidor de banco de dados com segurança por SSL. verificação de certificado do servidor tooallow, certificado Olá deve ser colocado em Olá arquivo ~/.postgresql/root.crt no diretório base do usuário hello. (No arquivo do Microsoft Windows hello é denominada % APPDATA%\postgresql\root.crt.). a seguir Olá fornece instruções para conectar tooAzure banco de dados para PostgreSQL.

> [!NOTE]
> Atualmente, há um problema conhecido se você usar "sslmode = verificar-full" em seu serviço de toohello de conexão, a conexão Olá falhará com hello erro a seguir: _certificado do servidor para "&lt;região&gt;. Control.Database.Windows.NET"(e 7 outros nomes) não coincide com o nome de host"&lt;servername&gt;. postgres.database.azure.com "._
> Se "sslmode = completo verificar" é necessário, use a convenção de nomenclatura de servidor de saudação  **&lt;servername&gt;. t** como seu nome de host de cadeia de caracteres de conexão. Planejamos tooremove esta limitação no hello futuras. Conexões usando outros [modos SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) devem continuar a convenção de nomenclatura Olá preferido host toouse  **&lt;servername&gt;. postgres.database.azure.com**.

#### <a name="using-psql-command-line-utility"></a>Usar o utilitário de linha de comando psql
saudação de exemplo a seguir mostra como toosuccessfully conectar tooyour PostgreSQL servidor usando o utilitário de linha de comando do hello psql. Saudação de uso `root.crt` arquivo criado e hello `sslmode=verify-ca` ou `sslmode=verify-full` opção.

Usando a interface de linha de comando do hello PostgreSQL, execute Olá comando a seguir:
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
Se for bem-sucedido, você receberá Olá saída a seguir:
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

#### <a name="using-pgadmin-gui-tool"></a>Usando a ferramenta GUI de pgAdmin
Configurar pgAdmin 4 tooconnect com segurança por SSL requer Olá tooset `SSL mode = Verify-CA` ou `SSL mode = Verify-Full` da seguinte maneira:

![Captura de tela de pgAdmin - conexão - modo SSL Require](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>Próximas etapas
Analise as várias opções de conectividade do aplicativo em [Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL](concepts-connection-libraries.md)
