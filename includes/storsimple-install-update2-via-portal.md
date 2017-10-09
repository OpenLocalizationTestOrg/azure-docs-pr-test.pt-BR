<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall uma atualização do hello portal do Azure

1. Na página de serviço do StorSimple hello, selecione seu dispositivo. Navegue muito**dispositivos** > **manutenção**.
2. Final Olá Olá página, clique em **verificar atualizações**. Um trabalho é criado tooscan atualizações disponíveis. Você será notificado quando Olá for concluído com êxito.
3. Em Olá **atualizações de Software** seção Olá mesma página, novas atualizações de software Olá estão disponíveis. É recomendável que você revise as notas de versão de saudação antes de aplicar uma atualização em seu dispositivo.
4. Final Olá Olá página, clique em **instalar atualizações**e, em seguida, **Okey**.
5. Em Olá **instalar atualizações** caixa de diálogo, certifique-se de que você seguiu as recomendações de saudação e selecione **entendo Olá acima requisito e estou pronto tooupgrade meu dispositivo** e clique em Verificar Olá botão.
   
    ![Mensagem de confirmação](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. Um conjunto de verificações de pré-requisito é iniciado. Essas verificações incluem:
   
   * **Verificações de integridade do controlador** tooverify que ambos Olá controladores de dispositivo estiverem íntegros e online.
   * **Verificações de integridade do componente de hardware** tooverify que todos os Olá componentes de hardware no seu dispositivo StorSimple estão íntegros.
   * **DATA 0 verifica** tooverify que DATA 0 está habilitado no seu dispositivo. Se essa interface não estiver habilitada, você deverá habilitá-la e repetir a ação.
   * **DATA 2 e DATA 3 verificações** tooverify que as interfaces de rede DATA 2 e 3 de dados não estão habilitadas. Se essas interfaces são habilitadas, você deve desabilitar estas e tente tooupdate seu dispositivo. Essa verificação será realizada somente se você estiver atualizando de um dispositivo que está executando o software de disponibilidade geral. Os dispositivos que executam versões 0.1, 0.2 ou 0.3 não precisarão dessa verificação.
   * **Verificação do gateway** em qualquer dispositivo que executa um tooUpdate anterior da versão 1. Essa verificação é executada em todos os dispositivos de saudação executando o software de pré-atualização 1, mas não em dispositivos de saudação que têm um gateway configurado para uma interface de rede diferente de dados 0.
     
     atualização de saudação é aplicada se todas as verificações são concluídas com êxito. Você será notificado quando Olá verificações estão em andamento.
     
     ![Notificação de pré-verificação](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     a seguir Olá é um exemplo em que as verificações de saudação falharam. Você deve verificar que ambos os controladores de dispositivo Olá estiverem íntegros e online. Você também precisa toocheck integridade de Olá Olá dos componentes de hardware. Neste exemplo, os componentes do Controlador 0 e do Controlador 1 precisam de atenção. Se você não pode resolver esses problemas sozinho, talvez seja necessário toocontact Microsoft Support.
     
       ![Falha nas verificações](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Depois de verificações de saudação são concluídas com êxito, um trabalho de atualização é criado. Você será notificado quando o trabalho de atualização de saudação é criado com êxito.
   
    ![Criação do trabalho de atualização](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    atualização de saudação é então aplicada em seu dispositivo.
    
8. progresso de saudação toomonitor de trabalho de atualização de hello, clique em **Exibir trabalho**. Em Olá **trabalhos** página, você pode ver Olá progresso da atualização.
9. atualização de saudação leva alguns toocomplete de horas. Selecione o trabalho de atualização de saudação e clique em **detalhes** tooview detalhes de saudação do trabalho Olá a qualquer momento.
10. Após a conclusão do trabalho hello, navegar toohello **manutenção** página e role para baixo demais**atualizações de Software**.

