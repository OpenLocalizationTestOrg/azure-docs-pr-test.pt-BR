
<br>

> [!NOTE]
> Se você recebeu um nome de usuário e uma senha de um administrador, há boas chances de que você já tenha uma ID corporativa ou de estudante (às vezes também chamada de *ID organizacional*). Nesse caso, você pode iniciar imediatamente toouse tooaccess sua conta do Azure recursos do Azure que precisam de uma. Se você achar que não é possível usar esses recursos, talvez seja necessário tooreturn toothis artigo para obter ajuda. Para obter mais informações, consulte [contas que você pode usar para entrar no](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) e [assinatura como um Azure está relacionada tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

etapas de saudação são simples. Você precisa toolocate seu assinado em identidade no portal clássico do Azure do hello, descobrir seu domínio do Active Directory do Azure padrão e adicionar um novo tooit de usuário como um coadministrador do Azure.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>Localize o diretório padrão em Olá portal clássico do Azure
Iniciar o registro em log em toohello [portal clássico do Azure](https://manage.windowsazure.com) com sua identidade de conta Microsoft pessoal. Depois que você está conectado, role para baixo painel Olá azul Olá lado esquerdo e clique em **do ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Vamos começar localizando algumas informações sobre sua identidade no Azure. Você deve ver algo como Olá a seguir no painel principal hello, mostrando o que você tenha um diretório padrão.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

Vamos descobrir mais algumas informações sobre ele. Clique em saudação padrão directory linha, que traz em Propriedades do diretório padrão hello.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

nome de domínio padrão do hello tooview, clique em **domínios**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Aqui, você deve ser capaz de toosee quando foi criado Olá conta do Azure, Active Directory do Azure criado um domínio padrão pessoais que é um valor de hash (um número gerado a partir de uma cadeia de caracteres de texto) da sua ID pessoal usado como um subdomínio do c o m. Isso é Olá domínio toowhich agora, você adicionará um novo usuário.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Criar um novo usuário no domínio do saudação padrão
Clique em **USUÁRIOS** e procure a sua conta pessoal única. Você verá no hello **ORIGINADO de** coluna que é um **conta da Microsoft**. Queremos que um usuário no padrão de toocreate. c o m domínio de Active Directory do Azure.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

Vamos toofollow [estas instruções](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) em Olá próximas etapas, mas usar um exemplo específico.

Final Olá Olá página, clique em **+ adicionar usuário**. Na página de saudação que aparece, digite o novo nome de usuário hello e fazer Olá **tipo de usuário** um **novo usuário na sua organização**. Neste exemplo, o novo nome de usuário Olá é `ahmet`. Selecione o domínio de padrão de saudação descobertos anteriormente como domínio de saudação para do ahmet endereço de email. Clique em seta para Avançar a hello quando terminar.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Adicione mais detalhes para Ahmet, mas tornar se Olá de tooselect apropriados **função** valor. É fácil toouse **Administrador Global** toomake se as coisas estão funcionando, mas se você pode usar uma função menor, que é uma boa ideia. Este exemplo usa Olá **usuário** função. (Saiba mais em [Permissões de administrador por função](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Não habilite a autenticação multifator, a menos que você deseja toouse a autenticação multifator para cada log em operação. Quando terminar, clique em seta Avançar hello.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Clique em Olá **criar** botão toogenerate e exibir uma senha temporária para Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Copie o endereço de email de nome de usuário hello, ou use **enviar senha no EMAIL**. Você precisará Olá informações toolog em breve.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Agora você deve ver o novo usuário de hello, **Ahmet Olá desenvolvedor**, originários do Active Directory do Azure. Você criou novos trabalhos de saudação ou identidade de escola com o Active Directory do Azure. No entanto, essa identidade ainda não tiver permissões toouse Azure recursos.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Se você usar **enviar senha no EMAIL**, Olá após o tipo de email é enviada.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Adicionando direitos de coadministrador do Azure para assinaturas
Agora você precisa de tooadd Olá novo usuário como coadministrador da assinatura para que o novo usuário de saudação pode entrar no Portal de gerenciamento de toohello. toodo isso, no painel inferior esquerdo de saudação clique **configurações**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Na área de configurações principal hello, clique em **administradores** em Olá superior e você verá somente sua identidade pessoal da conta Microsoft. Final Olá Olá página, clique em **+ adicionar** toospecify um coadministrador. Aqui, insira o endereço de email de saudação do novo usuário de saudação criado, incluindo o domínio padrão. Conforme mostrado na seguinte captura de tela de hello, uma marca de seleção verde é exibida próximo usuário toohello para o diretório padrão de saudação. Lembre-se de tooselect todas as assinaturas de saudação que deseja que este tooadminister capaz de toobe do usuário.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

Quando tiver terminado, você deverá ver dois usuários, incluindo sua nova identidade de coadministrador. Faça logoff do portal de saudação.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Logon e alterar a senha de saudação do novo usuário
Faça logon como usuário novo Olá que você criou.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Você será solicitada toocreate uma nova senha imediatamente.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Você deve ser premiado com êxito semelhante ao seguinte hello.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Próximas etapas
Agora você pode usar o novo toouse de identidade do Active Directory do Azure [modelos de grupo de recursos do Azure](../articles/xplat-cli-azure-resource-manager.md).

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
