Quando você não precisa mais um disco de dados é anexado tooa VM, você pode facilmente desanexá-lo. Desanexar um disco remove o disco de saudação da máquina virtual de hello, mas não exclui o disco de saudação da saudação conta de armazenamento do Azure.

Se você quiser toouse Olá dados existentes ao disco Olá novamente, você poderá reanexar-toohello mesma máquina virtual ou outro.  

> [!NOTE]
> toodetach um disco do sistema operacional, é necessário primeiro toodelete Olá VM.
>

## <a name="find-hello-disk"></a>Localizar o disco Olá
Se você não souber o nome de saudação do hello disco ou deseja tooverify-lo antes de desconectá-lo, siga estas etapas.

1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. Clique em **máquinas virtuais**, e, em seguida, selecione Olá VM apropriado.

3. Clique em **discos** ao longo de saudação extremidade esquerda do painel de máquina virtual hello, em **configurações**.

 Painel de máquina virtual Olá lista Nome hello e tipo de todos os discos conectados. Por exemplo, esta tela mostra uma máquina virtual com um disco do sistema operacional (SO) e um disco de dados:

    ![Encontrar disco de dados](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a>Desanexar o disco Olá
1. De Olá portal do Azure, clique em **máquinas virtuais**e então clique Olá nome da máquina virtual Olá que possui o disco de dados Olá deseja toodetach.

2. Clique em **discos** ao longo de saudação extremidade esquerda do painel de máquina virtual hello, em **configurações**.

3. Clique em disco Olá toodetach desejado.

  ![Identificar Olá disco toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. Na barra de comandos de saudação, clique em **desanexar**.

  ![Localizar Olá comando detach](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. Na janela de confirmação de saudação, clique em **Sim** toodetach disco de saudação.

  ![Confirmar desanexando disco Olá](./media/howto-detach-disk-windows-linux/confirmdetach.png)

disco Olá permanece no armazenamento, mas não está mais anexado tooa virtual machine.
