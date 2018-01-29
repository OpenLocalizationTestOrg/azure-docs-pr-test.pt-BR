## <a name="set-up-the-development-environment"></a>Configurar o ambiente de desenvolvimento

Esta seção orienta a configuração do ambiente de desenvolvimento. Ela inclui a criação de um aplicativo ASP.NET MVC, a adição de uma conexão de serviços conectados, a adição de um controlador e a especificação das diretivas de namespace necessárias.

### <a name="create-an-aspnet-mvc-app-project"></a>Criar um projeto de aplicativo ASP.NET MVC

1. Abra o Visual Studio.

1. No menu principal, selecione **Arquivo** > **Novo** > **Projeto**.

1. Na caixa de diálogo **Novo Projeto**, selecione **Web** > **Aplicativo Web ASP.NET (.NET Framework)**. No campo **Nome**, especifique **StorageAspNet**. Selecione **OK**.

    ![A captura de tela da caixa de diálogo Novo Projeto](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. Na caixa de diálogo **Novo Aplicativo Web ASP.NET**, selecione **MVC** e, a seguir, selecione **OK**.

    ![Captura de tela da caixa de diálogo Novo Aplicativo Web ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

### <a name="use-connected-services-to-connect-to-an-azure-storage-account"></a>Usar Serviços Conectados para se conectar a uma conta de armazenamento do Azure

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nome do projeto.

2. No menu de contexto, selecione **Adicionar** > **Serviços Conectados**.

1. Na caixa de diálogo **Serviços Conectados**, selecione **Armazenamento na Nuvem com Armazenamento do Microsoft Azure** e, a seguir, selecione **Configurar**.

    ![Tela de captura da caixa de diálogo Serviços Conectados](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. Na caixa de diálogo **Armazenamento do Microsoft Azure**, selecione a conta do Armazenamento do Azure a ser usada para este tutorial. Para criar uma nova conta do Armazenamento do Azure, selecione **Criar uma Nova Conta de Armazenamento** e preencha o formulário. Depois de selecionar uma conta de armazenamento existente ou criar uma nova, selecione **Adicionar**. O Visual Studio instalará o pacote NuGet para o Armazenamento do Microsoft Azure e uma cadeia de conexão de armazenamento para **Web.config**.

> [!TIP]
> Para saber como criar uma conta de armazenamento com o [portal do Azure](https://portal.azure.com), consulte [Criar uma conta de armazenamento](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account).
>
> Você também pode criar uma conta de armazenamento usando o [Azure PowerShell](../articles/storage/common/storage-powershell-guide-full.md), a [CLI do Azure](../articles/storage/common/storage-azure-cli.md) ou o [Azure Cloud Shell](../articles/cloud-shell/overview.md).

