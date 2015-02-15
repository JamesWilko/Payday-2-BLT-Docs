
# Notifications Manager

The Notifications Manager allows you to show small notifications on the main menu. It is used by the Payday 2 BLT to show when updates are available.   
If more than one notification is added to the manager, they will automatically rotate through the available notifications. Players can also manually click through them.  

---

### Notification
Every notification is stored in a table in the `NotificationsManager`. They can be accessed via 
`GetNotifications`, or `GetCurrentNotification`. This is the data contained for each notification.  
`id` The unique identifier for this notification.  
`title` The display title for this notifiation.  
`message` The message which will be displayed alongside the title for this notification.  
`priority` How soon this notification will be shown on the UI.  
`callback` The function will be called when the notification on the UI is pressed.  
`read` A boolean indicating if this notification has been read or not.  


### NotificationsManager:GetNotifications()
Gets the ordered table of all notifications currently being displayed.  
`returns` An ordered table of all notifications being displayed by the notifications manager.  

	local notifs = NotificationsManager:GetNotifications()

	local num_notifs = #NotificationsManager:GetNotifications()


### NotificationsManager:GetCurrentNotification()
Gets the notification which is currently being shown.  
`returns` The table of the notification which is currently being shown.  

	local current_notif = NotificationsManager:GetCurrentNotification()


### NotificationsManager:GetCurrentNotificationIndex()
Gets the table index of the currently displayed notification.  
`returns` The index of the currently displayed notification from the notifications table.  

	local curr_index = NotificationsManager:GetCurrentNotificationIndex()


### NotificationsManager:AddNotification( id, title, message, priority, callback )
Adds a notification to the manager, and shows it on the notifications UI.  
`id` The unique identifier for this notification.  
`title` The title to use for this notification.  
`[message]` The message to be displayed alongside the notification. If set to nil or an empty string it will not be shown. Optional.  
`[priority]` The priority of this notification. Higher values will be shown sooner, acceptable values are `0` to `1000`. Optional.  
`[callback]` A function to run if the notification is clicked. Will do nothing when clicked if left as nil. Optional.  
`returns` Returns true if the notification was successfully added, false is it failed and could not be added.  

	local notif_id = "my_custom_notif"
	local title = "My Custom Notification"
	local message = "This is my custom notification, it will appear on the main menu."
	NotificationsManager:AddNotification( notif_id, title, message )


### NotificationsManager:UpdateNotification( id, title, message, priority, callback )
Updates the contents of a notification to the new values specified.  
`id` The unique identifier of the notification you wish to update.  
`[title]` The new title to use for the notification. If left nil it will not change the title. Optional.  
`[message]` The new message to use for the notification. If left nil it will not change the message. Optional.  
`[priority]` The new priority value for this notification. Will use the old value if left as nil. Optional.  
`[callback]` The new callback to use for this notification. Will use the old callback if left as nil. Optional.  
`returns` Returns true if the notification was successfully updated. Will return false if no notification with `id` could be found.  

	local notif_id = "my_custom_notif"
	local new_title = "My NEW Custom Notification"
	local new_prio = 25
	NotificationsManager:UpdateNotification( notif_id, new_title, nil, new_prio )


### NotificationsManager:RemoveNotification( id )
Removes the notification with the specified ID.  
`id` The identifier of the notification to be removed.  
`returns` Returns true if the notification was removed, false if no ID was specified.   

	NotificationsManager:RemoveNotification( "my_custom_notif" )


### NotificationsManager:ClearNotifications()
Removes all active notifications.  
	
	NotificationsManager:ClearNotifications()


### NotificationsManager:NotificationExists( id )
Checks if the notification with ID `id` exists and is being displayed.  
`id` The unique identifier of the notification to check.  
`returns` Returns true if the notification exists, false otherwise.  

	if not NotificationsManager:NotificationExists( "my_custom_notif" ) then
		create_my_notification()
	end


### NotificationsManager:MarkNotificationAsRead( id )
Marks the specified notification as being read. Unread notifications will have an exclamation point icon next to them. _This is not normally needed as notifications are automatically set as read once viewed._  
`id` The identifier of the notification to mark as read.  
`returns` Returns true if the notification was set as read, false if no notification could be found.  

	NotificationsManager:MarkNotificationAsRead( "my_custom_notif" )


### Hook: NotificationManagerOnNotificationsUpdated( self, notifications )
The hook which is called when the notifications table is updated.  
`self` The NotificationsManager class itself is passed as the first argument.  
`notifications` The table of notifications is passed as the second argument.  

	Hooks:Add("NotificationManagerOnNotificationsUpdated", "NotificationManagerOnNotificationsUpdated_Example", function(manager, notifications)
		log( "Received notifications: " .. manager:GetCurrentNotification().title )
	end)
