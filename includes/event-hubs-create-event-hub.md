## <a name="create-an-event-hub"></a>Erstellen eines Ereignis-Hubs
1. Melden Sie sich beim [Azure-Portal][Azure-Portal] an, und klicken Sie oben links auf dem Bildschirm auf **Neu**.
2. Klicken Sie auf **Internet der Dinge**, und klicken Sie dann auf **Event Hubs**.
   
    ![](./media/event-hubs-create-event-hub/create-event-hub9.png)
3. Geben Sie auf dem Blatt **Namespace erstellen** einen Namen für den Namespace ein. Das System überprüft sofort, ob dieser Name verfügbar ist.
   
    ![](./media/event-hubs-create-event-hub/create-event-hub1.png)
4. Ist der Name verfügbar, wählen Sie den Tarif („Basic“ oder „Standard“) aus. Wählen Sie außerdem ein Azure-Abonnement, eine Ressourcengruppe und einen Standort, an dem die Ressource erstellt werden soll. 
5. Klicken Sie auf **Erstellen** , um den Namespace zu erstellen.
6. Klicken Sie in der Liste der Event Hubs-Namespaces auf den neu erstellten Namespace.      
   
    ![](./media/event-hubs-create-event-hub/create-event-hub2.png)
7. Klicken Sie auf dem Blatt mit den Namespaces auf **Event Hubs**.
   
    ![](./media/event-hubs-create-event-hub/create-event-hub3.png)
8. Klicken Sie oben auf dem Blatt auf **Event Hub hinzufügen**.
   
    ![](./media/event-hubs-create-event-hub/create-event-hub4.png)
9. Geben Sie einen Namen für den Event Hub ein, und klicken Sie auf **Erstellen**.
   
    ![](./media/event-hubs-create-event-hub/create-event-hub5.png)
10. Klicken Sie in der Liste der Event Hubs auf den Namen des neu erstellten Event Hubs. 
    
     ![](./media/event-hubs-create-event-hub/create-event-hub6.png)
11. Klicken Sie auf dem Blatt mit Namespaces (nicht auf dem Blatt für den bestimmten Event Hub) auf **Shared access policies** (Richtlinien für gemeinsamen Zugriff), und klicken Sie dann auf **RootManageSharedAccessKey**.
    
     ![](./media/event-hubs-create-event-hub/create-event-hub7.png)
12. Klicken Sie auf die Kopierschaltfläche, um die Verbindungszeichenfolge **RootManageSharedAccessKey** in die Zwischenablage zu kopieren. Speichern Sie diese Verbindungszeichenfolge für die spätere Verwendung in diesem Tutorial.
    
     ![](./media/event-hubs-create-event-hub/create-event-hub8.png)

Ihr Event Hub wird jetzt erstellt, und Sie verfügen über die zum Senden und Empfangen von Ereignissen erforderlichen Verbindungszeichenfolgen.

[Azure-Portal]: https://portal.azure.com/

<!--HONumber=Nov16_HO4-->


