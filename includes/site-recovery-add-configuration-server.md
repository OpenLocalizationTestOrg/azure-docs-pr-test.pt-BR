1. Execute o arquivo de instalação do Unified instalação de saudação.
2. Em **antes de começar**, selecione **instalar o servidor de configuração de saudação e servidor de processo**.

    ![Antes de começar](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. Em **licença para Software de terceiros**, clique em **aceito** toodownload e instalar o MySQL.

    ![Software de terceiros](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. Em **registro**, selecione chave de registro de saudação baixado do cofre hello.

    ![Registro](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. Em **configurações de Internet**, especifique como Olá tooAzure recuperação de Site se conecta de provedor em execução no servidor de configuração de saudação pela Olá da Internet.

   a. Se você desejar tooconnect com o proxy de saudação que está configurado na máquina hello, selecione **conectar tooAzure recuperação de Site usando um servidor proxy**.

   b. Se você desejar Olá provedor tooconnect diretamente, selecione **se conectar diretamente tooAzure recuperação de Site sem um servidor proxy**.

   c. Se o proxy existente Olá requer autenticação, ou se você quiser toouse um proxy personalizado para a conexão do provedor de saudação, selecione **conectar-se com as configurações de proxy personalizadas**.

     * Se você usar um proxy personalizado, você precisa de credenciais, porta e endereço de saudação toospecify.
     * Se você estiver usando um proxy, você deve ter já Olá URLs permitidas descritos em [pré-requisitos](#prerequisites).

     ![Firewall](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. Em **verificação de pré-requisitos**, um toomake seleção-se de que a instalação pode executar a instalação é executada. Se aparecer um aviso sobre Olá **verificação da sincronização de horário Global**, verifique se esse tempo de saudação no relógio do sistema de saudação (**data e hora** configurações) Olá mesmo como o fuso horário hello.

    ![Pré-requisitos](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. Em **configuração MySQL**, criar credenciais para fazer logon na instância do servidor MySQL toohello que está instalada.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. Em **detalhes do ambiente**, selecione se você vai tooreplicate VMware VMs. Se a resposta for positiva, a Instalação verificará se o PowerCLI 6.0 está instalado.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. Em **local de instalação**, selecione onde você deseja tooinstall binários de saudação e armazena o cache de saudação. unidade de saudação que você selecionar deve ter pelo menos 5 GB de espaço em disco disponível, mas é recomendável uma unidade de cache com pelo menos de 600 GB de espaço livre.

    ![Local de instalação](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. Em **seleção de rede**, especifique o ouvinte de saudação (adaptador de rede e porta SSL) no qual servidor de configuração Olá envia e recebe dados de replicação. Porta 9443 é saudação padrão usado para enviar e receber tráfego de replicação, mas você pode modificar este toosuit de número de porta requisitos do ambiente. Adição toohello porta 9443 também é abrir a porta 443, que é usada por um operações de replicação de tooorchestrate de servidor web. Não use a porta 443 para enviar ou receber tráfego de replicação.

    ![Seleção da Rede](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. Em **resumo**, revise as informações de saudação e clique em **instalar**. Após a conclusão da instalação, uma frase secreta é gerada. Você precisará dela quando habilitar a replicação, portanto copie-a e guarde-a em um local seguro.

    ![Resumo](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Após a conclusão do registro, o servidor de saudação é exibido em Olá **configurações** > **servidores** folha no cofre hello.
