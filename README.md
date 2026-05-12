# Zoho-CRM-Quote-Approval-Automation
Built a complete automation flow in Zoho CRM for Quote Approval and automatic Work Order creation. The process includes automated email notifications with approval links, customer approval/cancellation actions, automatic Quote Stage updates (Draft → Approved), and instant Work Order creation after approval.


``
void automation.CreateWorkOrder(Int idd)
{
resp = zoho.crm.getRecordById("Quotes",idd);
info resp;
owner = ifnull(resp.getJSON("Owner"),"");
ownerid = ifnull(owner.getJSON("id"),"");
subject = ifnull(resp.getJSON("Subject"),"");
contact = resp.getJSON("Contact_Name");
if(contact != null)
{
	contactid = contact.getJSON("id");
	info contactid;
}
resp2 = zoho.crm.getRecordById("Contacts",contactid);
info resp2;
email = resp2.getJSON("Email");
info email;
account = resp.getJSON("Account_Name");
if(account != null)
{
	accountid = account.getJSON("id");
	info accountid;
}
deal = resp.getJSON("Deal_Name");
if(deal != null)
{
	dealid = deal.getJSON("id");
	info dealid;
}
mapp = Map();
mapp.put("Owner",ownerid);
mapp.put("Contact",contactid);
mapp.put("Account",accountid);
mapp.put("Deal_Name",dealid);
mapp.put("Quote",idd);
mapp.put("Name",subject);
mapp.put("Email",email);
mapp.put("Status","Created");
resp2 = zoho.crm.createRecord("Work_Orders",mapp,{"trigger":{"workflow"}});
info resp2;
}

``
