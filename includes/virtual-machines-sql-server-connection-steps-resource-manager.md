### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="9be24-101">Configurar um rótulo de DNS para o endereço IP público</span><span class="sxs-lookup"><span data-stu-id="9be24-101">Configure a DNS Label for the public IP address</span></span>

<span data-ttu-id="9be24-102">Para conectar o Mecanismo de Banco de Dados do SQL Server na Internet, considere criar um Rótulo DNS para seu endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="9be24-102">To connect to the SQL Server Database Engine from the Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="9be24-103">Você pode conectar pelo endereço IP, mas o rótulo DNS cria um Registro A que é mais fácil de identificar e abstrai o endereço IP público subjacente.</span><span class="sxs-lookup"><span data-stu-id="9be24-103">You can connect by IP address, but the DNS Label creates an A Record that is easier to identify and abstracts the underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="9be24-104">Rótulos de DNS não são obrigatórios se você planeja se conectar somente à instância do SQL Server na mesma Rede Virtual ou apenas localmente.</span><span class="sxs-lookup"><span data-stu-id="9be24-104">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>

<span data-ttu-id="9be24-105">Para criar um rótulo de DNS, primeiro selecione **Máquinas Virtuais** no portal.</span><span class="sxs-lookup"><span data-stu-id="9be24-105">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="9be24-106">Selecione sua VM do SQL Server para exibir suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="9be24-106">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="9be24-107">Na visão geral da máquina virtual, selecione seu **Endereço IP público**.</span><span class="sxs-lookup"><span data-stu-id="9be24-107">In the virtual machine overview, select your **Public IP address**.</span></span>

    ![endereço ip público](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="9be24-109">Nas propriedades de seu Endereço IP Público, expanda **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="9be24-109">In the properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="9be24-110">Insira um nome para o rótulo de DNS.</span><span class="sxs-lookup"><span data-stu-id="9be24-110">Enter a DNS Label name.</span></span> <span data-ttu-id="9be24-111">Esse nome é um registro A que pode ser usado para se conectar à sua VM do SQL Server por nome em vez de por endereço IP diretamente.</span><span class="sxs-lookup"><span data-stu-id="9be24-111">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="9be24-112">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9be24-112">Click the **Save** button.</span></span>

    ![rótulo de dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="9be24-114">Conectar-se ao Mecanismo de Banco de Dados de outro computador</span><span class="sxs-lookup"><span data-stu-id="9be24-114">Connect to the Database Engine from another computer</span></span>

1. <span data-ttu-id="9be24-115">Em um computador conectado à Internet, abra o SSMS (SQL Server Management Studio).</span><span class="sxs-lookup"><span data-stu-id="9be24-115">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="9be24-116">Se você não tiver o SQL Server Management Studio, poderá baixá-lo [aqui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="9be24-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="9be24-117">Na caixa de diálogo **Conectar ao Servidor** ou **Conectar ao Mecanismo de Banco de Dados**, edite o valor **Nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="9be24-117">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="9be24-118">Insira o endereço IP ou o nome DNS completo da máquina virtual (determinado na tarefa anterior).</span><span class="sxs-lookup"><span data-stu-id="9be24-118">Enter the IP address or full DNS name of the virtual machine (determined in the previous task).</span></span> <span data-ttu-id="9be24-119">Você também pode adicionar uma vírgula e fornecer a porta TCP do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9be24-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="9be24-120">Por exemplo: `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="9be24-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="9be24-121">Na caixa **Autenticação**, selecione **Autenticação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="9be24-121">In the **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="9be24-122">Na caixa **Login** , digite o nome de um login válido do SQL.</span><span class="sxs-lookup"><span data-stu-id="9be24-122">In the **Login** box, type the name of a valid SQL login.</span></span>

1. <span data-ttu-id="9be24-123">Na caixa **Senha** , digite a senha de login.</span><span class="sxs-lookup"><span data-stu-id="9be24-123">In the **Password** box, type the password of the login.</span></span>

1. <span data-ttu-id="9be24-124">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="9be24-124">Click **Connect**.</span></span>

    ![conexão ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)