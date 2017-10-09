<span data-ttu-id="c9639-101">filas de toobegin usando o barramento de serviço no Azure, você deve primeiro criar um namespace com um nome que seja exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="c9639-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="c9639-102">Um namespace fornece um contêiner de escopo para endereçar recursos do barramento de serviço dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9639-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="c9639-103">toocreate um namespace:</span><span class="sxs-lookup"><span data-stu-id="c9639-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="c9639-104">Faça logon no toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="c9639-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="c9639-105">No painel de navegação à esquerda de saudação do portal de saudação, clique em **novo**, em seguida, clique em **integração corporativa**e, em seguida, clique em **barramento de serviço**.</span><span class="sxs-lookup"><span data-stu-id="c9639-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="c9639-106">Em Olá **criar namespace** caixa de diálogo, digite um nome de namespace.</span><span class="sxs-lookup"><span data-stu-id="c9639-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="c9639-107">sistema de saudação imediatamente verifica toosee se Olá nome está disponível.</span><span class="sxs-lookup"><span data-stu-id="c9639-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="c9639-108">Depois de fazer o nome do namespace Olá-se de que está disponível, escolha Olá preço (Basic, Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="c9639-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="c9639-109">Em Olá **assinatura** campo, escolha uma assinatura do Azure no qual namespace de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9639-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="c9639-110">Em Olá **grupo de recursos** campo, escolha um grupo de recursos existente no qual Olá namespace ao vivo ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="c9639-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="c9639-111">Em **local**, escolha o país de saudação ou região em que o namespace deve ser hospedado.</span><span class="sxs-lookup"><span data-stu-id="c9639-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Criar um namespace][create-namespace]
8. <span data-ttu-id="c9639-113">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c9639-113">Click **Create**.</span></span> <span data-ttu-id="c9639-114">sistema de saudação agora cria seu namespace e permite que ele.</span><span class="sxs-lookup"><span data-stu-id="c9639-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="c9639-115">Você pode ter toowait vários minutos como recursos de provisões de sistema Olá para sua conta.</span><span class="sxs-lookup"><span data-stu-id="c9639-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="c9639-116">Obter credenciais de gerenciamento Olá</span><span class="sxs-lookup"><span data-stu-id="c9639-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="c9639-117">Na lista de saudação de namespaces, clique Olá recém-criada em nome do namespace.</span><span class="sxs-lookup"><span data-stu-id="c9639-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="c9639-118">Na folha de namespace hello, clique em **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="c9639-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="c9639-119">Em Olá **políticas de acesso compartilhado** folha, clique em **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="c9639-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![informações de conexão][connection-info]
4. <span data-ttu-id="c9639-121">Em Olá **política: RootManageSharedAccessKey** folha, clique o botão de cópia de Olá Avançar muito**chave primária cadeia de caracteres de Conexão**, toocopy Olá conexão cadeia tooyour na área de transferência para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="c9639-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="c9639-122">Cole esse valor no Bloco de notas ou em outro local temporário.</span><span class="sxs-lookup"><span data-stu-id="c9639-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="c9639-124">Etapa anterior Olá repetida, copiar e colar o valor de saudação do **chave primária** tooa o local temporário para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="c9639-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
