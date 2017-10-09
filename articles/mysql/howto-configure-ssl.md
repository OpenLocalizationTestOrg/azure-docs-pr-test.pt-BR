---
title: "aaaConfigure SSL conectividade toosecurely tooAzure banco de dados de conexão para MySQL | Microsoft Docs"
description: "Instruções sobre como tooproperly configura o banco de dados do Azure para aplicativos associados toocorrectly e MySQL usam conexões SSL"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>Configurar o SSL de conectividade em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL
Banco de dados do Azure para MySQL dá suporte à conexão seu banco de dados MySQL tooclient para aplicativos de servidor usando o protocolo (SSL). Impor conexões SSL entre o servidor de banco de dados e aplicativos cliente ajuda a proteger contra ataques "man no meio hello" criptografando o fluxo de dados de saudação entre o servidor de saudação e seu aplicativo.

## <a name="step-1-obtain-ssl-certificate"></a>Etapa 1: obter um certificado SSL
Baixar Olá certificado necessário toocommunicate por SSL com o banco de dados do Azure para o MySQL server de [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) e salvar tooyour de arquivo de certificado de saudação local unidade (com este tutorial, usamos c:\ssl).
**Para o Microsoft Internet Explorer e Microsoft Edge:** após a conclusão do download hello, renomear Olá tooBaltimoreCyberTrustRoot.crt.pem de certificado.

## <a name="step-2-bind-ssl"></a>Etapa 2: associar o SSL
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>Conectando tooserver usando Olá MySQL Workbench sobre SSL
Configure o MySQL Workbench tooconnect com segurança por SSL. Navegue toohello **SSL** guia Olá MySQL Workbench em Olá caixa de diálogo de Conexão nova instalação. Insira o local do arquivo de saudação do hello **BaltimoreCyberTrustRoot.crt.pem** em Olá **arquivo de autoridade de certificação SSL:** campo.
![salvar bloco personalizado](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>Conectando tooserver usando Olá MySQL CLI sobre SSL
Usando a interface de linha de comando do MySQL hello, execute Olá comando a seguir:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>Etapa 3: impor conexões SSL no Azure 
### <a name="using-azure-portal"></a>Usando o Portal do Azure
Usando Olá portal do Azure, visite o banco de dados do Azure para MySQL server e clique em **segurança de Conexão**. Use tooenable de botão de alternância de saudação ou desabilite Olá **conexão SSL impor** configuração. Em seguida, clique em **Salvar**. A Microsoft recomenda habilitar tooalways **conexão SSL impor** configuração de segurança aprimorada.
![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Usando a CLI do Azure
Você pode habilitar ou desabilitar Olá **ssl imposição** parâmetro usando valores Enabled ou Disabled respectivamente em CLI do Azure.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Etapa 4: verificar a conexão SSL
Executar Olá mysql **status** tooverify de comando que você está conectado tooyour MySQL server usando o SSL:
```dos
mysql> status
```
Confirme a conexão de saudação é criptografado, revisando a saída de hello. Ela deverá mostrar: **SSL: a criptografia em uso é AES256-SHA** 

## <a name="sample-code"></a>Exemplo de código
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>Próximas etapas
Analise as várias opções de conectividade do aplicativo em [Bibliotecas de conexão para o Banco de Dados do Azure para MySQL](concepts-connection-libraries.md)
