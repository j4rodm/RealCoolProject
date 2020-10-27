# RealCoolProject #

## Future header ##

future body

### Future Subheader ###

Intense code

```js
// Find groups that have Ticket Queue Notifications turned on
var group_gr = new GlideRecord('sys_user_group');
group_gr.addEncodedQuery('u_ticket_queue_active=true^u_ticket_queue_threshold>=0^u_ticket_queue_usersISNOTEMPTY^ORu_ticket_queue_groupsISNOTEMPTY');
group_gr.query();
while (group_gr.next()){
	var notify = [];
	notify.push(group_gr.getValue('u_ticket_queue_users'));
	notify.push(group_gr.getValue('u_ticket_queue_groups'));

	var case_gr = new GlideRecord('sn_customerservice_case');
	case_gr.addEncodedQuery('active=true^u_requires_fulfiller_action=true^assignment_group='+group_gr.getUniqueValue());
	case_gr.query();
	if (case_gr.getRowCount() >= group_gr.getValue('u_ticket_queue_threshold')){
		gs.eventQueue('ticket_queue_notifications.threshold_met', group_gr, notify.join(','), case_gr.getRowCount());
	}
}
```
