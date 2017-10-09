* Em **adicionar vCenter**, especifique um nome amigável para o servidor de host ou vCenter vSphere hello e em seguida, especifique o endereço IP hello ou FQDN do servidor de saudação. Deixe a porta hello como 443, a menos que os servidores do VMware são toolisten configurada para solicitações em uma porta diferente. Selecione a conta Olá tooconnect toohello VMware vCenter ou vSphere ESXi server. Clique em **OK**.

    ![VMware](./media/site-recovery-add-vcenter/vmware-server.png)

   > [!NOTE]
   > Se você estiver adicionando Olá VMware vCenter server ou VMware vSphere host com uma conta que não tem privilégios de administrador no servidor de host ou vCenter Olá, certifique-se de que conta Olá tem esses privilégios habilitados: Datacenter, o repositório de dados, pasta, Host, rede , Recursos, a máquina Virtual e o vSphere distribuído do comutador. Além disso, Olá VMware vCenter server precisa de exibições de armazenamento Olá privilégio habilitado.
