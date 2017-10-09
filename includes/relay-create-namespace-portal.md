1. <span data-ttu-id="a5d16-101">Faça logon no toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a5d16-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a5d16-102">No painel de navegação à esquerda de saudação do portal de saudação, clique em **novo**, em seguida, clique em **integração corporativa**e, em seguida, clique em **retransmissão**.</span><span class="sxs-lookup"><span data-stu-id="a5d16-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="a5d16-103">Em Olá **criar namespace** caixa de diálogo, digite um nome de namespace.</span><span class="sxs-lookup"><span data-stu-id="a5d16-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="a5d16-104">sistema de saudação imediatamente verifica toosee se Olá nome está disponível.</span><span class="sxs-lookup"><span data-stu-id="a5d16-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="a5d16-105">Em Olá **assinatura** campo, escolha uma assinatura do Azure no qual namespace de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="a5d16-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="a5d16-106">Em Olá  **[grupo de recursos](../articles/azure-resource-manager/resource-group-portal.md)**  campo, escolha um grupo de recursos existente no qual Olá namespace ao vivo ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="a5d16-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="a5d16-107">Em **local**, escolha o país de saudação ou região em que o namespace deve ser hospedado.</span><span class="sxs-lookup"><span data-stu-id="a5d16-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Criar um namespace][create-namespace]
7. <span data-ttu-id="a5d16-109">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a5d16-109">Click **Create**.</span></span> <span data-ttu-id="a5d16-110">sistema de saudação agora cria seu namespace e permite que ele.</span><span class="sxs-lookup"><span data-stu-id="a5d16-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="a5d16-111">Depois de alguns minutos, Olá sistema Provisione recursos para sua conta.</span><span class="sxs-lookup"><span data-stu-id="a5d16-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="a5d16-112">Obter credenciais de gerenciamento Olá</span><span class="sxs-lookup"><span data-stu-id="a5d16-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="a5d16-113">Na lista de saudação de namespaces, clique Olá recém-criada em nome do namespace.</span><span class="sxs-lookup"><span data-stu-id="a5d16-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="a5d16-114">Na folha de namespace hello, clique em **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="a5d16-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="a5d16-115">Em Olá **políticas de acesso compartilhado** folha, clique em **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="a5d16-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![informações de conexão][connection-info]
4. <span data-ttu-id="a5d16-117">Em Olá **política: RootManageSharedAccessKey** folha, clique o botão de cópia de Olá Avançar muito**chave primária cadeia de caracteres de Conexão**, toocopy Olá conexão cadeia tooyour na área de transferência para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="a5d16-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="a5d16-118">Cole esse valor no Bloco de notas ou em outro local temporário.</span><span class="sxs-lookup"><span data-stu-id="a5d16-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="a5d16-120">Etapa anterior Olá repetida, copiar e colar o valor de saudação do **chave primária** tooa o local temporário para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="a5d16-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
