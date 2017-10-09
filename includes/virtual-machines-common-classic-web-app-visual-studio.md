

Ao criar um projeto de aplicativo Web para o Azure, você pode provisionar uma máquina virtual no Azure. Você pode configurar a máquina virtual de saudação com software adicional ou usar a máquina virtual de saudação para fins de diagnósticos e depuração.

toocreate uma máquina virtual quando você criar um aplicativo web, siga estas etapas:

1. No Visual Studio, clique em **arquivo** > **novo** > **projeto** > **Web**e, em seguida, escolha **Aplicativo Web ASP.NET** (em Olá **Visual C#** ou **Visual Basic** nós).
2. Em Olá **novo projeto ASP.NET** caixa de diálogo, o tipo de saudação selecione do aplicativo web desejado e, em hello Azure seção da caixa de diálogo de saudação (no canto do hello inferior direito), certifique-se de que Olá **Host na nuvem Olá**caixa de seleção estiver marcada (esta caixa de seleção rotulada **criar recursos remotos** em algumas instalações).
   
    ![][0]
3. Neste exemplo, na lista suspensa, Olá em Microsoft Azure, escolha **Máquina Virtual (v1)**e, em seguida, clique em Olá **Okey** botão.
4. Entrar tooAzure se você for solicitado. Olá **criar Máquina Virtual** caixa de diálogo é exibida.
   
    ![][2]
5. Em Olá **nome DNS** , digite um nome para a máquina virtual de saudação. nome DNS Olá deve ser exclusivo no Azure. Se o nome hello inserido não estiver disponível, um ponto de exclamação vermelho será exibido.
6. Em Olá **imagem** , escolha a imagem Olá deseja toobase Olá VM na. Você pode escolher qualquer uma das imagens de máquina virtual do Azure padrão hello ou a imagem que você carregou tooAzure.
7. Deixe Olá **habilitar o IIS e a implantação da Web** caixa de seleção, a menos que você planejar tooinstall um servidor web diferente. Você não será capaz de toopublish do Visual Studio se você desabilitar a implantação da Web. Você pode adicionar o IIS e a implantação da Web tooany de imagens do Windows Server Olá empacotado, incluindo imagens personalizadas.
8. Em Olá **tamanho** , escolha o tamanho de saudação da máquina virtual de saudação.
9. Especifique Olá credenciais de entrada para esta máquina virtual. Anote-los, porque eles são necessários tooaccess Olá máquina por meio da área de trabalho remota.
10. Em Olá **local** , escolha a máquina virtual do hello região toohost hello.
11. Clique em Olá **Okey** toostart botão criando uma máquina virtual de saudação. Você pode acompanhar o progresso de saudação da operação de saudação da saudação **saída** janela.
    
    ![][3]
12. Quando a máquina virtual de saudação é provisionada, scripts publicados são criados em um **PublishScripts** nó em sua solução. Olá publicados script será executado e provisiona uma máquina virtual no Azure. Olá **saída** janela mostra o status de saudação. script Hello executa Olá ações tooset máquina virtual de saudação a seguir:
    
    * Cria a máquina de virtual de saudação se ele ainda não existir.
    * Cria uma conta de armazenamento com um nome que começa com `devtest`, mas somente se já houver tal uma conta de armazenamento na região especificada hello.
    * Cria um serviço de nuvem como um contêiner para a máquina virtual de saudação e cria uma função web do aplicativo da web hello.
    * Configura a implantação da Web na máquina virtual de saudação.
    * Configura o IIS e ASP.NET na máquina virtual de saudação.
    
    ![][4]
13. (Opcional) Você pode se conectar a máquina virtual da nova toohello. Em **Server Explorer**, expanda Olá **máquinas virtuais** nó, escolha o nó Olá Olá máquina de virtual criado por você e em seu menu de atalho, escolha **conecte-se à área de trabalho remota**. Como alternativa, na **Cloud Explorer** você pode escolher **abrir no Portal de** Olá menu de atalho e conectar-se a máquina de virtual toohello existe.
    
    ![][5]

## <a name="next-steps"></a>Próximas etapas
Se você quiser toocustomize Olá publicados scripts que você criou, ler informações mais detalhadas em [ambientes de teste e usando Scripts do Windows PowerShell tooPublish tooDev](http://msdn.microsoft.com/library/dn642480.aspx).

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
