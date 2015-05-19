# Add partner filter to partner ledger report.

add partner filter to the partner balance ledger report

you have one step to do after installing this module:

change the file:/addons/account/report/account_partner_ledger.py

add this two lines into def set_context(self, objects, data, ids, report_type=None) method:

if data['form'].get('partner_id',False): </br>
<t/>self.partner_ids = data['form']['partner_id']</br>
objects = obj_partner.browse(self.cr, SUPERUSER_ID, self.partner_ids)</br>
objects = sorted(objects, key=lambda x: (x.ref, x.name))</br>
return super(third_party_ledger, self).set_context(objects, data, self.partner_ids, report_type)
