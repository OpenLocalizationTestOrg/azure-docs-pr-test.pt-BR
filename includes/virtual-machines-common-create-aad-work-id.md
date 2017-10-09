
<br>

> [!NOTE]
> <span data-ttu-id="4105b-101">Se você recebeu um nome de usuário e uma senha de um administrador, há boas chances de que você já tenha uma ID corporativa ou de estudante (às vezes também chamada de *ID organizacional*).</span><span class="sxs-lookup"><span data-stu-id="4105b-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="4105b-102">Nesse caso, você pode iniciar imediatamente toouse tooaccess sua conta do Azure recursos do Azure que precisam de uma.</span><span class="sxs-lookup"><span data-stu-id="4105b-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="4105b-103">Se você achar que não é possível usar esses recursos, talvez seja necessário tooreturn toothis artigo para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="4105b-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="4105b-104">Para obter mais informações, consulte [contas que você pode usar para entrar no](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) e [assinatura como um Azure está relacionada tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="4105b-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="4105b-105">etapas de saudação são simples.</span><span class="sxs-lookup"><span data-stu-id="4105b-105">hello steps are simple.</span></span> <span data-ttu-id="4105b-106">Você precisa toolocate seu assinado em identidade no portal clássico do Azure do hello, descobrir seu domínio do Active Directory do Azure padrão e adicionar um novo tooit de usuário como um coadministrador do Azure.</span><span class="sxs-lookup"><span data-stu-id="4105b-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="4105b-107">Localize o diretório padrão em Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4105b-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="4105b-108">Iniciar o registro em log em toohello [portal clássico do Azure](https://manage.windowsazure.com) com sua identidade de conta Microsoft pessoal.</span><span class="sxs-lookup"><span data-stu-id="4105b-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="4105b-109">Depois que você está conectado, role para baixo painel Olá azul Olá lado esquerdo e clique em **do ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="4105b-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="4105b-111">Vamos começar localizando algumas informações sobre sua identidade no Azure.</span><span class="sxs-lookup"><span data-stu-id="4105b-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="4105b-112">Você deve ver algo como Olá a seguir no painel principal hello, mostrando o que você tenha um diretório padrão.</span><span class="sxs-lookup"><span data-stu-id="4105b-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="4105b-113">Vamos descobrir mais algumas informações sobre ele.</span><span class="sxs-lookup"><span data-stu-id="4105b-113">Let's find out some more information about it.</span></span> <span data-ttu-id="4105b-114">Clique em saudação padrão directory linha, que traz em Propriedades do diretório padrão hello.</span><span class="sxs-lookup"><span data-stu-id="4105b-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="4105b-115">nome de domínio padrão do hello tooview, clique em **domínios**.</span><span class="sxs-lookup"><span data-stu-id="4105b-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="4105b-116">Aqui, você deve ser capaz de toosee quando foi criado Olá conta do Azure, Active Directory do Azure criado um domínio padrão pessoais que é um valor de hash (um número gerado a partir de uma cadeia de caracteres de texto) da sua ID pessoal usado como um subdomínio do c o m. Isso é Olá domínio toowhich agora, você adicionará um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="4105b-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="4105b-117">Criar um novo usuário no domínio do saudação padrão</span><span class="sxs-lookup"><span data-stu-id="4105b-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="4105b-118">Clique em **USUÁRIOS** e procure a sua conta pessoal única.</span><span class="sxs-lookup"><span data-stu-id="4105b-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="4105b-119">Você verá no hello **ORIGINADO de** coluna que é um **conta da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="4105b-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="4105b-120">Queremos que um usuário no padrão de toocreate. c o m domínio de Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="4105b-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="4105b-121">Vamos toofollow [estas instruções](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) em Olá próximas etapas, mas usar um exemplo específico.</span><span class="sxs-lookup"><span data-stu-id="4105b-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="4105b-122">Final Olá Olá página, clique em **+ adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="4105b-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="4105b-123">Na página de saudação que aparece, digite o novo nome de usuário hello e fazer Olá **tipo de usuário** um **novo usuário na sua organização**.</span><span class="sxs-lookup"><span data-stu-id="4105b-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="4105b-124">Neste exemplo, o novo nome de usuário Olá é `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="4105b-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="4105b-125">Selecione o domínio de padrão de saudação descobertos anteriormente como domínio de saudação para do ahmet endereço de email.</span><span class="sxs-lookup"><span data-stu-id="4105b-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="4105b-126">Clique em seta para Avançar a hello quando terminar.</span><span class="sxs-lookup"><span data-stu-id="4105b-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="4105b-127">Adicione mais detalhes para Ahmet, mas tornar se Olá de tooselect apropriados **função** valor.</span><span class="sxs-lookup"><span data-stu-id="4105b-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="4105b-128">É fácil toouse **Administrador Global** toomake se as coisas estão funcionando, mas se você pode usar uma função menor, que é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="4105b-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="4105b-129">Este exemplo usa Olá **usuário** função.</span><span class="sxs-lookup"><span data-stu-id="4105b-129">This example uses hello **User** role.</span></span> <span data-ttu-id="4105b-130">(Saiba mais em [Permissões de administrador por função](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Não habilite a autenticação multifator, a menos que você deseja toouse a autenticação multifator para cada log em operação.</span><span class="sxs-lookup"><span data-stu-id="4105b-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="4105b-131">Quando terminar, clique em seta Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="4105b-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="4105b-132">Clique em Olá **criar** botão toogenerate e exibir uma senha temporária para Ahmet.</span><span class="sxs-lookup"><span data-stu-id="4105b-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="4105b-133">Copie o endereço de email de nome de usuário hello, ou use **enviar senha no EMAIL**.</span><span class="sxs-lookup"><span data-stu-id="4105b-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="4105b-134">Você precisará Olá informações toolog em breve.</span><span class="sxs-lookup"><span data-stu-id="4105b-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="4105b-135">Agora você deve ver o novo usuário de hello, **Ahmet Olá desenvolvedor**, originários do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="4105b-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="4105b-136">Você criou novos trabalhos de saudação ou identidade de escola com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="4105b-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="4105b-137">No entanto, essa identidade ainda não tiver permissões toouse Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="4105b-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="4105b-138">Se você usar **enviar senha no EMAIL**, Olá após o tipo de email é enviada.</span><span class="sxs-lookup"><span data-stu-id="4105b-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="4105b-139">Adicionando direitos de coadministrador do Azure para assinaturas</span><span class="sxs-lookup"><span data-stu-id="4105b-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="4105b-140">Agora você precisa de tooadd Olá novo usuário como coadministrador da assinatura para que o novo usuário de saudação pode entrar no Portal de gerenciamento de toohello.</span><span class="sxs-lookup"><span data-stu-id="4105b-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="4105b-141">toodo isso, no painel inferior esquerdo de saudação clique **configurações**.</span><span class="sxs-lookup"><span data-stu-id="4105b-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="4105b-142">Na área de configurações principal hello, clique em **administradores** em Olá superior e você verá somente sua identidade pessoal da conta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4105b-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="4105b-143">Final Olá Olá página, clique em **+ adicionar** toospecify um coadministrador.</span><span class="sxs-lookup"><span data-stu-id="4105b-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="4105b-144">Aqui, insira o endereço de email de saudação do novo usuário de saudação criado, incluindo o domínio padrão.</span><span class="sxs-lookup"><span data-stu-id="4105b-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="4105b-145">Conforme mostrado na seguinte captura de tela de hello, uma marca de seleção verde é exibida próximo usuário toohello para o diretório padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4105b-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="4105b-146">Lembre-se de tooselect todas as assinaturas de saudação que deseja que este tooadminister capaz de toobe do usuário.</span><span class="sxs-lookup"><span data-stu-id="4105b-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="4105b-147">Quando tiver terminado, você deverá ver dois usuários, incluindo sua nova identidade de coadministrador.</span><span class="sxs-lookup"><span data-stu-id="4105b-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="4105b-148">Faça logoff do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="4105b-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="4105b-149">Logon e alterar a senha de saudação do novo usuário</span><span class="sxs-lookup"><span data-stu-id="4105b-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="4105b-150">Faça logon como usuário novo Olá que você criou.</span><span class="sxs-lookup"><span data-stu-id="4105b-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="4105b-151">Você será solicitada toocreate uma nova senha imediatamente.</span><span class="sxs-lookup"><span data-stu-id="4105b-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="4105b-152">Você deve ser premiado com êxito semelhante ao seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="4105b-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="4105b-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4105b-153">Next steps</span></span>
<span data-ttu-id="4105b-154">Agora você pode usar o novo toouse de identidade do Active Directory do Azure [modelos de grupo de recursos do Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4105b-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
