### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="fa25a-101">Configurar um rótulo de DNS para o endereço IP público de Olá</span><span class="sxs-lookup"><span data-stu-id="fa25a-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="fa25a-102">tooconnect toohello o mecanismo de banco de dados do SQL Server de saudação à Internet, considere a criação de um rótulo de DNS para seu endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="fa25a-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="fa25a-103">Você pode se conectar por endereço IP, mas Olá rótulo DNS cria um registro que é mais fácil tooidentify e resumos Olá subjacente endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="fa25a-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="fa25a-104">Rótulos de DNS não são necessários se o plano tooonly conectar toohello do SQL Server da instância em Olá mesmo rede Virtual ou apenas localmente.</span><span class="sxs-lookup"><span data-stu-id="fa25a-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="fa25a-105">toocreate um rótulo de DNS, primeiro selecione **máquinas virtuais** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa25a-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="fa25a-106">Selecione seu toobring VM do SQL Server, suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="fa25a-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="fa25a-107">Na visão geral de máquina virtual hello, selecione seu **endereço IP público**.</span><span class="sxs-lookup"><span data-stu-id="fa25a-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![endereço ip público](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="fa25a-109">Nas propriedades de saudação de seu endereço IP público, expanda **configuração**.</span><span class="sxs-lookup"><span data-stu-id="fa25a-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="fa25a-110">Insira um nome para o rótulo de DNS.</span><span class="sxs-lookup"><span data-stu-id="fa25a-110">Enter a DNS Label name.</span></span> <span data-ttu-id="fa25a-111">Esse nome é um registro que podem ser usados tooconnect tooyour VM do SQL Server por nome em vez de por endereço IP diretamente.</span><span class="sxs-lookup"><span data-stu-id="fa25a-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="fa25a-112">Clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="fa25a-112">Click hello **Save** button.</span></span>

    ![rótulo de dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="fa25a-114">Conectar toohello mecanismo de banco de dados de outro computador</span><span class="sxs-lookup"><span data-stu-id="fa25a-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="fa25a-115">Em um computador conectado toohello internet, abra SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="fa25a-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="fa25a-116">Se você não tiver o SQL Server Management Studio, poderá baixá-lo [aqui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="fa25a-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="fa25a-117">Em Olá **conectar tooServer** ou **conectar tooDatabase mecanismo** caixa de diálogo, editar Olá **nome do servidor** valor.</span><span class="sxs-lookup"><span data-stu-id="fa25a-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="fa25a-118">Insira o endereço IP de saudação ou nome DNS completo da máquina virtual de saudação (determinado na tarefa anterior Olá).</span><span class="sxs-lookup"><span data-stu-id="fa25a-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="fa25a-119">Você também pode adicionar uma vírgula e fornecer a porta TCP do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa25a-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="fa25a-120">Por exemplo: `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="fa25a-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="fa25a-121">Em Olá **autenticação** selecione **autenticação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="fa25a-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="fa25a-122">Em Olá **Login** caixa, digite o nome de saudação de um logon SQL válido.</span><span class="sxs-lookup"><span data-stu-id="fa25a-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="fa25a-123">Em Olá **senha** caixa, digite a senha de logon Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="fa25a-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="fa25a-124">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="fa25a-124">Click **Connect**.</span></span>

    ![conexão ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)