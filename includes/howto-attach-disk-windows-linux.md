


## <a name="attach-an-empty-disk"></a>Anexar um disco vazio
Anexar um disco vazio é tooadd uma maneira simples que dados de um disco, porque o Azure cria o arquivo. vhd de saudação para você e o armazena na conta de armazenamento hello.

1. Clique em **máquinas virtuais (clássicas)**, e, em seguida, selecione Olá VM apropriado.

2. No menu de configurações de saudação, clique em **discos**.

   ![Anexar um novo disco vazio](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Na barra de comandos de saudação, clique em **anexar novos**.  
    Olá **anexar novo disco** caixa de diálogo é exibida.

    ![Anexar um novo disco](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Preencha Olá informações a seguir:
    - Em **nome de arquivo**, aceite o nome padrão de saudação ou digite um outro para o arquivo. vhd de saudação. disco de dados Olá usa um nome gerado automaticamente, mesmo se você digitar outro nome para o arquivo. vhd de saudação.
    - Selecione Olá **tipo** saudação do disco de dados. Todas as máquinas virtuais oferecem suporte a discos padrão. Muitas máquinas virtuais também oferecem suporte a discos premium.
    - Selecione Olá **tamanho (GB)** saudação do disco de dados.
    - Para **Cache de Host**, escolha nenhum ou Somente Leitura.
    - Clique em toofinish Okey.

4. Depois que o disco de dados Olá é criado e anexado, ele é listado na seção de discos de saudação do hello VM.

   ![Disco de dados novo e vazio anexado com êxito](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> Depois de adicionar um disco de dados, você precisa toolog em toohello VM e inicializar disco Olá para que ele possa ser usado.

## <a name="how-to-attach-an-existing-disk"></a>Como: anexar um disco existente
Anexar um disco existente exige que você tenha um .vhd disponível em uma conta de armazenamento. Saudação de uso [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) conta de armazenamento toohello de arquivo. vhd de saudação tooupload de cmdlet. Depois de criar e carregar o arquivo. vhd de saudação, você pode anexar tooa VM.

1. Clique em **máquinas virtuais (clássicas)**, e, em seguida, selecione Olá máquina virtual apropriado.

2. No menu de configurações de saudação, clique em **discos**.

3. Na barra de comandos de saudação, clique em **anexar existente**.

    ![Anexar disco de dados](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. Clique em **Local**. exibem contas de armazenamento disponível Hello. Em seguida, selecione uma conta de armazenamento apropriada daquelas listadas.

    ![Fornecer conta de armazenamento de disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. A **Conta de armazenamento** contém um ou mais contêineres que contêm unidades de disco (vhds). Selecione o contêiner apropriado Olá daqueles listados.

    ![Fornecer o contêiner de virtual-machines-windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. Olá **vhds** painel lista de unidades de disco Olá mantidas no contêiner de saudação. Clique em um dos discos hello e, em seguida, clique em Selecionar.

    ![Fornecer a imagem de disco para virtual-machines-windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. Olá **anexar o disco existente** painel exibe novamente, com o local de saudação que contém a conta de armazenamento hello, contêiner e máquina virtual do disco rígido (vhd) selecionado tooadd toohello.

  Definir **cache de Host** toonone ou leitura somente, em seguida, clique em Okey.

    ![Disco de dados anexado com êxito](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
