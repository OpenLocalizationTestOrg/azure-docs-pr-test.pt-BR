1. Iniciar hello Azure Site Recovery UnifiedSetup.exe
2. Em **antes de começar a**, selecione **adicionar tooscale de servidores de processo adicional implantação**.

  ![Adicionar servidor de processo](./media/site-recovery-add-process-server/ps-page-1.png)

3. Em **detalhes do servidor de configuração**, especifique o endereço IP de saudação do hello servidor de configuração e Olá frase secreta.

  ![Adicionar servidor de processo 2](./media/site-recovery-add-process-server/ps-page-2.png)
4. Em **configurações de Internet**, especifique como Olá tooAzure recuperação de Site se conecta de provedor em execução no hello servidor de configuração pela Olá da Internet.

  ![Adicionar servidor de processo 3](./media/site-recovery-add-process-server/ps-page-3.png)

   * Se você desejar tooconnect com o proxy de saudação que está configurado na máquina hello, selecione **conectar-se com as configurações de proxy existentes**.
   * Se você desejar Olá provedor tooconnect diretamente, selecione **conectar-se diretamente sem um proxy**.
   * Se o proxy existente Olá requer autenticação, ou se você quiser toouse um proxy personalizado para a conexão do provedor de saudação, selecione **conectar-se com as configurações de proxy personalizadas**.

     * Se você usar um proxy personalizado, você precisa de credenciais, porta e endereço de saudação toospecify.
     * Se você estiver usando um proxy, você deve já ter permissão urls de serviço toohello de acesso.

5. Em **verificação de pré-requisitos**, um toomake seleção-se de que a instalação pode executar a instalação é executada. Se aparecer um aviso sobre Olá **verificação da sincronização de horário Global**, verifique se esse tempo de saudação no relógio do sistema de saudação (**data e hora** configurações) Olá mesmo como o fuso horário hello.

     ![Adicionar servidor de processo 4](./media/site-recovery-add-process-server/ps-page-4.png)

6. Em **detalhes do ambiente**, selecione se você vai tooreplicate VMware VMs. Se a resposta for positiva, a instalação verificará se o PowerCLI 6.0 está instalado.

     ![Adicionar servidor de processo 5](./media/site-recovery-add-process-server/ps-page-5.png)

7. Em **local de instalação**, selecione onde você deseja tooinstall binários de saudação e armazena o cache de saudação. unidade de saudação que você selecionar deve ter pelo menos 5 GB de espaço em disco disponível, mas é recomendável uma unidade de cache com pelo menos de 600 GB de espaço livre.
     ![Adicionar servidor de processo 5](./media/site-recovery-add-process-server/ps-page-6.png)

8. Em **seleção de rede**, especifique o ouvinte de saudação (adaptador de rede e porta SSL) no qual envia de servidor de configuração de saudação e recebe dados de replicação. Porta 9443 é saudação padrão usado para enviar e receber tráfego de replicação, mas você pode modificar este toosuit de número de porta requisitos do ambiente. Adição toohello porta 9443 também é abrir a porta 443, que é usada por um operações de replicação de tooorchestrate de servidor web. Não use a porta 443 para enviar ou receber tráfego de replicação.

     ![Adicionar servidor de processo 6](./media/site-recovery-add-process-server/ps-page-7.png)
9. Em **resumo**, revise as informações de saudação e clique em **instalar**. Após a conclusão da instalação, uma frase secreta é gerada. Você precisará dela quando habilitar a replicação, portanto copie-a e guarde-a em um local seguro.

     ![Adicionar servidor de processo 7](./media/site-recovery-add-process-server/ps-page-8.png)
