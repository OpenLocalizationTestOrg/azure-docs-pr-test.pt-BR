
<br>

> [!NOTE]
> <span data-ttu-id="1b788-101">Se você recebeu um nome de usuário e uma senha de um administrador, há boas chances de que você já tenha uma ID corporativa ou de estudante (às vezes também chamada de *ID organizacional*).</span><span class="sxs-lookup"><span data-stu-id="1b788-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="1b788-102">Nesse caso, você pode começar a usar sua conta do Azure imediatamente para acessar recursos do Azure que a exigem.</span><span class="sxs-lookup"><span data-stu-id="1b788-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span></span> <span data-ttu-id="1b788-103">Se não for possível usar esses recursos, talvez você precise retornar a este artigo para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="1b788-103">If you find that you cannot use those resources, you may need to return to this article for help.</span></span> <span data-ttu-id="1b788-104">Para saber mais, confira [Contas que você pode usar para entrar](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) e [Qual é a relação de uma assinatura do Azure como Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="1b788-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="1b788-105">As etapas são simples.</span><span class="sxs-lookup"><span data-stu-id="1b788-105">The steps are simple.</span></span> <span data-ttu-id="1b788-106">Você precisa localizar sua identidade de conexão no portal clássico do Azure, descobrir o domínio padrão do Active Directory do Azure e adicionar um novo usuário a ele como um coadministrador do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b788-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a><span data-ttu-id="1b788-107">Localize seu diretório padrão no portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="1b788-107">Locate your default directory in the Azure classic portal</span></span>
<span data-ttu-id="1b788-108">Comece fazendo logon no [Portal clássico do Azure](https://manage.windowsazure.com) com a identidade de sua conta pessoal da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b788-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="1b788-109">Quando estiver conectado, role para baixo no painel azul do lado esquerdo e clique em **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="1b788-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="1b788-111">Vamos começar localizando algumas informações sobre sua identidade no Azure.</span><span class="sxs-lookup"><span data-stu-id="1b788-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="1b788-112">Algo semelhante ao que se segue será exibido no painel principal, mostrando que você tem um diretório padrão.</span><span class="sxs-lookup"><span data-stu-id="1b788-112">You should see something like the following in the main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="1b788-113">Vamos descobrir mais algumas informações sobre ele.</span><span class="sxs-lookup"><span data-stu-id="1b788-113">Let's find out some more information about it.</span></span> <span data-ttu-id="1b788-114">Clique na linha de diretório padrão, que mostra as propriedades do diretório padrão.</span><span class="sxs-lookup"><span data-stu-id="1b788-114">Click the default directory row, which brings you into the default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="1b788-115">Para exibir o nome de domínio padrão, clique em **DOMÍNIOS**.</span><span class="sxs-lookup"><span data-stu-id="1b788-115">To view the default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="1b788-116">Aqui você pode ver que quando a conta do Azure foi criada, o Active Directory do Azure criou um domínio padrão pessoal que é um valor hash (um número gerado por meio de uma cadeia de texto) da sua ID pessoal usado como um subdomínio de onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="1b788-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span></span> <span data-ttu-id="1b788-117">Esse é o domínio ao qual você adicionará um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="1b788-117">That's the domain to which you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-the-default-domain"></a><span data-ttu-id="1b788-118">Criando um novo usuário no domínio padrão</span><span class="sxs-lookup"><span data-stu-id="1b788-118">Creating a new user in the default domain</span></span>
<span data-ttu-id="1b788-119">Clique em **USUÁRIOS** e procure a sua conta pessoal única.</span><span class="sxs-lookup"><span data-stu-id="1b788-119">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="1b788-120">Na coluna **ORIGINADO DE**, você deverá ver que é uma **conta da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="1b788-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="1b788-121">Queremos criar um usuário no seu domínio padrão .onmicrosoft.com do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b788-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="1b788-122">Seguiremos [estas instruções](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) nas próximas etapas, mas usando um exemplo específico.</span><span class="sxs-lookup"><span data-stu-id="1b788-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span></span>

<span data-ttu-id="1b788-123">No fim da página, clique em **+ADICIONAR USUÁRIO**.</span><span class="sxs-lookup"><span data-stu-id="1b788-123">At the bottom of the page, click **+ADD USER**.</span></span> <span data-ttu-id="1b788-124">Na página que aparece, digite o novo nome de usuário e defina o **Tipo de Usuário** como um **Novo usuário em sua organização**.</span><span class="sxs-lookup"><span data-stu-id="1b788-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="1b788-125">Neste exemplo, o novo nome de usuário é `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="1b788-125">In this example, the new user name is `ahmet`.</span></span> <span data-ttu-id="1b788-126">Selecione o domínio padrão descoberto anteriormente como o domínio para o endereço de email do ahmet.</span><span class="sxs-lookup"><span data-stu-id="1b788-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span></span> <span data-ttu-id="1b788-127">Clique na seta para avançar quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="1b788-127">Click the next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="1b788-128">Adicione mais detalhes para Ahmet, mas certifique-se de selecionar o valor apropriado de **FUNÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="1b788-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span></span> <span data-ttu-id="1b788-129">É fácil usar o **Administrador Global** para garantir que tudo esteja funcionando, mas, se possível, use uma função com menos privilégios.</span><span class="sxs-lookup"><span data-stu-id="1b788-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="1b788-130">Este exemplo usa a função **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="1b788-130">This example uses the **User** role.</span></span> <span data-ttu-id="1b788-131">(Saiba mais em [Permissões de administrador por função](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Não habilite a autenticação multifator, a menos que queira usá-la para cada log em operação.</span><span class="sxs-lookup"><span data-stu-id="1b788-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span></span> <span data-ttu-id="1b788-132">Clique na seta para avançar quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="1b788-132">Click the next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="1b788-133">Clique no botão **criar** para gerar e exibir uma senha temporária para Ahmet.</span><span class="sxs-lookup"><span data-stu-id="1b788-133">Click the **create** button to generate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="1b788-134">Copie o endereço de email do nome de usuário ou use **ENVIAR SENHA EM EMAIL**.</span><span class="sxs-lookup"><span data-stu-id="1b788-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="1b788-135">Você precisará das informações para fazer logon em breve.</span><span class="sxs-lookup"><span data-stu-id="1b788-135">You'll need the information to log on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="1b788-136">Agora você deve ver o novo usuário, **Ahmet o desenvolvedor**, originado do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b788-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="1b788-137">Você criou a nova identidade corporativa ou de estudante com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b788-137">You've created the new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="1b788-138">No entanto, essa identidade ainda não tem permissões para usar os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b788-138">However, this identity does not yet have permissions to use Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="1b788-139">Se você usar **ENVIAR SENHA EM EMAIL**, o tipo de email a seguir será enviado.</span><span class="sxs-lookup"><span data-stu-id="1b788-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="1b788-140">Adicionando direitos de coadministrador do Azure para assinaturas</span><span class="sxs-lookup"><span data-stu-id="1b788-140">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="1b788-141">Agora você precisa adicionar o novo usuário como um coadministrador de sua assinatura para que o novo usuário possa entrar no Portal de Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1b788-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span></span> <span data-ttu-id="1b788-142">Para fazer isso, no painel inferior esquerdo, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="1b788-142">To do this, in the lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="1b788-143">Na área de configurações principais, clique em **ADMINISTRADORES** na parte superior, e você deverá ver apenas a identidade de sua conta pessoal da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b788-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="1b788-144">Na parte inferior da página, clique em **+ ADICIONAR** para especificar um coadministrador.</span><span class="sxs-lookup"><span data-stu-id="1b788-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span></span> <span data-ttu-id="1b788-145">Aqui, insira o endereço de email do novo usuário criado, incluindo o domínio padrão.</span><span class="sxs-lookup"><span data-stu-id="1b788-145">Here, enter the email address of the new user you had created, including your default domain.</span></span> <span data-ttu-id="1b788-146">Conforme mostrado na seguinte captura de tela, uma marca de seleção verde é exibida ao lado do usuário para o diretório padrão.</span><span class="sxs-lookup"><span data-stu-id="1b788-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span></span> <span data-ttu-id="1b788-147">Lembre-se de selecionar todas as assinaturas que deseja que este usuário seja capaz de administrar.</span><span class="sxs-lookup"><span data-stu-id="1b788-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="1b788-148">Quando tiver terminado, você deverá ver dois usuários, incluindo sua nova identidade de coadministrador.</span><span class="sxs-lookup"><span data-stu-id="1b788-148">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="1b788-149">Faça logoff no portal.</span><span class="sxs-lookup"><span data-stu-id="1b788-149">Log out of the portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a><span data-ttu-id="1b788-150">Fazendo logon e alterando a senha do novo usuário</span><span class="sxs-lookup"><span data-stu-id="1b788-150">Logging in and changing the new user's password</span></span>
<span data-ttu-id="1b788-151">Faça logon como o novo usuário criado.</span><span class="sxs-lookup"><span data-stu-id="1b788-151">Log in as the new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="1b788-152">Será solicitado que você crie uma nova senha imediatamente.</span><span class="sxs-lookup"><span data-stu-id="1b788-152">You will immediately be prompted to create a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="1b788-153">Uma mensagem de que você foi bem-sucedido deverá ser exibida, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1b788-153">You should be rewarded with success that looks like the following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="1b788-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b788-154">Next steps</span></span>
<span data-ttu-id="1b788-155">Agora você pode usar sua nova identidade do Active Directory do Azure para usar os [Modelos de grupo de recursos do Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1b788-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
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
