---
title: aplicativos de aaaConnect tooAzure banco de dados MySQL | Microsoft Docs
description: "Este documento contém cadeias de conexão Olá atualmente com suporte para aplicativos tooconnect com o banco de dados MySQL, incluindo ADO.NET (c#), JDBC, Node. js, ODBC, PHP, Python e Ruby."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a><span data-ttu-id="f66b1-103">Como tooconnect aplicativos tooAzure banco de dados para MySQL</span><span class="sxs-lookup"><span data-stu-id="f66b1-103">How tooconnect applications tooAzure Database for MySQL</span></span>
<span data-ttu-id="f66b1-104">Este documento lista os tipos de cadeia de caracteres de conexão de saudação que são suportados pelo banco de dados do Azure para MySQL, junto com os modelos e exemplos.</span><span class="sxs-lookup"><span data-stu-id="f66b1-104">This document lists hello connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="f66b1-105">Você pode ter parâmetros e configurações diferentes na cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="f66b1-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="f66b1-106">certificado de saudação tooobtain, consulte [como tooconfigure SSL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f66b1-106">tooobtain hello certificate, see [How tooconfigure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="f66b1-107">{your_host} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="f66b1-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="f66b1-108">Formato {your_user}@{servername} = userID para realizar a autenticação corretamente.</span><span class="sxs-lookup"><span data-stu-id="f66b1-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="f66b1-109">Usar apenas o userID Olá fará com que Olá toofail de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f66b1-109">Using just hello userID will cause hello authentication toofail.</span></span>

## <a name="adonet"></a><span data-ttu-id="f66b1-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="f66b1-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="f66b1-111">Neste exemplo, o nome do servidor de saudação é `myserver4demo`, nome do banco de dados é `wpdb`, nome de usuário é `WPAdmin`, e a senha é `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="f66b1-111">In this example, hello server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="f66b1-112">Em seguida, a cadeia de caracteres de conexão de saudação deve ser:</span><span class="sxs-lookup"><span data-stu-id="f66b1-112">Then, hello connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="f66b1-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="f66b1-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="f66b1-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="f66b1-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="f66b1-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="f66b1-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="f66b1-116">PHP</span><span class="sxs-lookup"><span data-stu-id="f66b1-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="f66b1-117">Python</span><span class="sxs-lookup"><span data-stu-id="f66b1-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="f66b1-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="f66b1-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a><span data-ttu-id="f66b1-119">Obter os detalhes de cadeia de caracteres de conexão Olá do hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f66b1-119">Get hello connection string details from hello Azure portal</span></span>
<span data-ttu-id="f66b1-120">Em Olá [portal do Azure](https://portal.azure.com), vá tooyour banco de dados do Azure para o MySQL server e, em seguida, clique em **cadeias de caracteres de Conexão** tooget sua cadeia de lista para sua instância: ![painel de cadeias de caracteres de Conexão Olá no Olá Portal do Azure](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="f66b1-120">In hello [Azure portal](https://portal.azure.com), go tooyour Azure Database for MySQL server, and then click **Connection strings** tooget your string list for your instance: ![hello Connection strings pane in hello Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="f66b1-121">cadeia de caracteres Hello fornece detalhes como o driver hello, server e outros parâmetros de conexão de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f66b1-121">hello string provides details such as hello driver, server, and other database connection parameters.</span></span> <span data-ttu-id="f66b1-122">Modifique esses exemplos usando seus próprios parâmetros, como o nome do banco de dados, a senha e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f66b1-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="f66b1-123">Você pode usar este servidor de toohello de tooconnect de cadeia de caracteres do seu código e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f66b1-123">You can then use this string tooconnect toohello server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f66b1-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f66b1-124">Next steps</span></span>
- <span data-ttu-id="f66b1-125">Para obter mais informações sobre bibliotecas de conexões, consulte [Conceitos – Bibliotecas de conexões](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="f66b1-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
