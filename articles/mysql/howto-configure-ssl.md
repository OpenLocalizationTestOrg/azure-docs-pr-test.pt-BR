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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="88a96-103">Configurar o SSL de conectividade em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL</span><span class="sxs-lookup"><span data-stu-id="88a96-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="88a96-104">Banco de dados do Azure para MySQL dá suporte à conexão seu banco de dados MySQL tooclient para aplicativos de servidor usando o protocolo (SSL).</span><span class="sxs-lookup"><span data-stu-id="88a96-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="88a96-105">Impor conexões SSL entre o servidor de banco de dados e aplicativos cliente ajuda a proteger contra ataques "man no meio hello" criptografando o fluxo de dados de saudação entre o servidor de saudação e seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88a96-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="88a96-106">Etapa 1: obter um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="88a96-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="88a96-107">Baixar Olá certificado necessário toocommunicate por SSL com o banco de dados do Azure para o MySQL server de [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) e salvar tooyour de arquivo de certificado de saudação local unidade (com este tutorial, usamos c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="88a96-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="88a96-108">**Para o Microsoft Internet Explorer e Microsoft Edge:** após a conclusão do download hello, renomear Olá tooBaltimoreCyberTrustRoot.crt.pem de certificado.</span><span class="sxs-lookup"><span data-stu-id="88a96-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="88a96-109">Etapa 2: associar o SSL</span><span class="sxs-lookup"><span data-stu-id="88a96-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="88a96-110">Conectando tooserver usando Olá MySQL Workbench sobre SSL</span><span class="sxs-lookup"><span data-stu-id="88a96-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="88a96-111">Configure o MySQL Workbench tooconnect com segurança por SSL.</span><span class="sxs-lookup"><span data-stu-id="88a96-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="88a96-112">Navegue toohello **SSL** guia Olá MySQL Workbench em Olá caixa de diálogo de Conexão nova instalação.</span><span class="sxs-lookup"><span data-stu-id="88a96-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="88a96-113">Insira o local do arquivo de saudação do hello **BaltimoreCyberTrustRoot.crt.pem** em Olá **arquivo de autoridade de certificação SSL:** campo.</span><span class="sxs-lookup"><span data-stu-id="88a96-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="88a96-114">![salvar bloco personalizado](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="88a96-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="88a96-115">Conectando tooserver usando Olá MySQL CLI sobre SSL</span><span class="sxs-lookup"><span data-stu-id="88a96-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="88a96-116">Usando a interface de linha de comando do MySQL hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="88a96-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="88a96-117">Etapa 3: impor conexões SSL no Azure</span><span class="sxs-lookup"><span data-stu-id="88a96-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="88a96-118">Usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="88a96-118">Using Azure portal</span></span>
<span data-ttu-id="88a96-119">Usando Olá portal do Azure, visite o banco de dados do Azure para MySQL server e clique em **segurança de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="88a96-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="88a96-120">Use tooenable de botão de alternância de saudação ou desabilite Olá **conexão SSL impor** configuração.</span><span class="sxs-lookup"><span data-stu-id="88a96-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="88a96-121">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="88a96-121">Then click **Save**.</span></span> <span data-ttu-id="88a96-122">A Microsoft recomenda habilitar tooalways **conexão SSL impor** configuração de segurança aprimorada.</span><span class="sxs-lookup"><span data-stu-id="88a96-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="88a96-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="88a96-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="88a96-124">Usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="88a96-124">Using Azure CLI</span></span>
<span data-ttu-id="88a96-125">Você pode habilitar ou desabilitar Olá **ssl imposição** parâmetro usando valores Enabled ou Disabled respectivamente em CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="88a96-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="88a96-126">Etapa 4: verificar a conexão SSL</span><span class="sxs-lookup"><span data-stu-id="88a96-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="88a96-127">Executar Olá mysql **status** tooverify de comando que você está conectado tooyour MySQL server usando o SSL:</span><span class="sxs-lookup"><span data-stu-id="88a96-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="88a96-128">Confirme a conexão de saudação é criptografado, revisando a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="88a96-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="88a96-129">Ela deverá mostrar: **SSL: a criptografia em uso é AES256-SHA**</span><span class="sxs-lookup"><span data-stu-id="88a96-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="88a96-130">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="88a96-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="88a96-131">PHP</span><span class="sxs-lookup"><span data-stu-id="88a96-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="88a96-132">Python</span><span class="sxs-lookup"><span data-stu-id="88a96-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="88a96-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88a96-133">Next steps</span></span>
<span data-ttu-id="88a96-134">Analise as várias opções de conectividade do aplicativo em [Bibliotecas de conexão para o Banco de Dados do Azure para MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="88a96-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
