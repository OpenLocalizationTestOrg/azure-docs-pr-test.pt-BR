1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. Iniciando na parte superior esquerda do hello, clique em **Novo > computação > Windows Server 2016 Datacenter**.

    ![Navegue toohello imagens de VM do Azure no portal de saudação](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. Na Olá Datacenter do Windows Server 2016, selecione o modelo de implantação clássico hello. Clique em Criar.

    ![Captura de tela que mostra imagens de VM do Azure Olá disponíveis no portal de saudação](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. Folha de Noções básicas

folha de Noções básicas de saudação solicita informações administrativas para a máquina virtual de saudação.

1. Insira um **nome** para a máquina virtual de saudação. No exemplo hello, _HeroVM_ é Olá nome da máquina virtual de saudação. nome de saudação deve ser de 1 a 15 caracteres e não pode conter caracteres especiais.

2. Insira um **nome de usuário** e um forte **senha** que são usada toocreate uma conta local Olá VM. Olá conta local é usada toosign em tooand gerenciar Olá VM. No exemplo hello, _azureuser_ é o nome de usuário de saudação.

 Olá senha deve ter 8 123 caracteres e atender aos três das quatro seguintes requisitos de complexidade Olá: caractere minúscula, caractere um maiusculo, um número e um caractere especial. Veja mais sobre os [requisitos de nome de usuário e senha](../articles/virtual-machines/windows/faq.md).

3. Olá **assinatura** é opcional. Uma configuração comum é "Pré-pago".

4. Selecione uma existente **grupo de recursos** ou nome de saudação do tipo para um novo. No exemplo hello, _HeroVMRG_ é nome Olá Olá do grupo de recursos.

5. Selecione um datacenter do Azure **local** onde você deseja Olá toorun VM. No exemplo hello, **Leste dos EUA** é Olá local.

6. Quando terminar, clique em **próximo** toocontinue toohello próxima folha.

    ![Captura de tela que mostra as configurações de saudação na folha de Noções básicas de saudação para configurar uma VM do Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. Folha Tamanho

folha de tamanho de saudação identifica os detalhes de configuração de saudação de saudação VM e lista as várias opções que incluem o sistema operacional, o número de processadores, o tipo de armazenamento de disco e custos estimados de uso mensal.  

Escolha um tamanho de VM e, em seguida, clique em **selecione** toocontinue. Neste exemplo, _DS1_\__V2 padrão_ é o tamanho da VM hello.

  ![Captura de tela da folha de tamanho de saudação que mostra Olá tamanhos de VM do Azure que você pode selecionar](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. Folha de configurações

folha de configurações de saudação solicitações de opções de armazenamento e rede. Você pode aceitar as configurações padrão de saudação. O Azure cria entradas apropriadas quando necessário.

Se você selecionou um tamanho de máquina virtual que dá suporte a isso, poderá experimentar o Armazenamento Premium do Azure, selecionando Premium (SSD) em Tipo de disco.

Quando terminar de fazer as alterações, clique em **OK**.

## <a name="4-summary-blade"></a>4. Folha de Resumo

folha de resumo de saudação lista configurações de Olá especificadas em folhas de saudação anterior. Clique em **Okey** quando estiver pronto toomake imagem de saudação.

 ![Relatório de resumo de folha fornecendo configurações especificadas da máquina virtual de saudação](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Após a criação de máquina virtual de hello, portal Olá lista Olá nova máquina virtual em **todos os recursos**e exibe um bloco de máquina virtual de saudação no painel de saudação. Olá correspondente nuvem serviço e conta de armazenamento também são criadas e listadas. Máquina virtual de saudação e o serviço de nuvem são iniciados automaticamente e seu status é listado como **executando**.

 ![Configurar o agente de VM e hello pontos de extremidade da máquina virtual de saudação](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
