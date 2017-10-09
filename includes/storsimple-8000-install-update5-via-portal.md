<!--author=alkohli last changed: 08/04/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall uma atualização do hello portal do Azure

1. Na página de serviço do StorSimple hello, selecione seu dispositivo.

    ![Selecionar dispositivo](./media/storsimple-8000-install-update5-via-portal/update1.png)

2. Navegue muito**configurações do dispositivo** > **atualizações de dispositivo**.

    ![Clique em Atualizações de dispositivo](./media/storsimple-8000-install-update5-via-portal/update2.png)

2. Uma notificação será exibida se houver novas atualizações disponíveis. Como alternativa, no hello **atualizações de dispositivo** folha, clique em **verificar atualizações**. Um trabalho é criado tooscan atualizações disponíveis. Você será notificado quando Olá for concluído com êxito.

    ![Clique em Atualizações de dispositivo](./media/storsimple-8000-install-update5-via-portal/update3.png)

3. É recomendável que você revise as notas de versão de saudação antes de aplicar uma atualização em seu dispositivo. tooapply atualizações, clique em **instalar atualizações**. Em Olá **confirmar atualizações regulares** folha, examine Olá pré-requisitos toocomplete antes de aplicar as atualizações. Selecione Olá tooindicate de caixa de seleção que você tooupdate pronto do hello dispositivo e, em seguida, clique em **instalar**.

    ![Clique em Atualizações de dispositivo](./media/storsimple-8000-install-update5-via-portal/update4.png)

6. Um conjunto de verificações de pré-requisito é iniciado. Essas verificações incluem:
   
   * **Verificações de integridade do controlador** tooverify que ambos Olá controladores de dispositivo estiverem íntegros e online.
   * **Verificações de integridade do componente de hardware** tooverify que todos os Olá componentes de hardware no seu dispositivo StorSimple estão íntegros.
   * **DATA 0 verifica** tooverify que DATA 0 está habilitado no seu dispositivo. Se essa interface não estiver habilitada, você deverá habilitá-la e repetir a ação.

    atualização de saudação é baixada e instalada somente se todas as verificações de saudação são concluídas com êxito. Você será notificado quando Olá verificações estão em andamento. Se Olá prechecks falharem, você será fornecido com motivos Olá da falha. Resolver esses problemas e, em seguida, repita a operação de saudação. Se você não pode resolver esses problemas sozinho, talvez seja necessário toocontact Microsoft Support.

7. Depois de saudação prechecks são concluídos com êxito, um trabalho de atualização é criado. Você será notificado quando o trabalho de atualização de saudação é criado com êxito.
   
    ![Criação do trabalho de atualização](./media/storsimple-8000-install-update5-via-portal/update6.png)
   
    atualização de saudação é então aplicada em seu dispositivo.

9. atualização de saudação leva alguns toocomplete de horas. Selecione o trabalho de atualização de saudação e clique em **detalhes** tooview detalhes de saudação do trabalho Olá a qualquer momento.

    ![Criação do trabalho de atualização](./media/storsimple-8000-install-update5-via-portal/update8.png)

     Você também pode monitorar o progresso de saudação do trabalho de atualização de saudação do **configurações do dispositivo > trabalhos**. Em Olá **trabalhos** folha, você pode ver Olá progresso da atualização.

     ![Criação do trabalho de atualização](./media/storsimple-8000-install-update5-via-portal/update7.png)

10. Após a conclusão do trabalho hello, navegar toohello **configurações do dispositivo > atualizações de dispositivo**. versão do software Olá agora deve ser atualizada.

