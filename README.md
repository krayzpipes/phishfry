# PhishFry Remediation Library and Command Line Tool
PhishFry is a python library and command line tool for removing and restoring emails in exchange and office365.

## Installation
Clone the repo and run the setup script.
```bash
git@github.com:IntegralDefense/phishfry.git
cd phishfry
./setup.sh
```

Add credentials for one or more exchange accounts with impersonation rights to the config.ini file.
###### Example config.ini file:
```
[account1]
user=admin@example1.com
pass=123456

[account2]
user=admin@example2.com
pass=123456
```

## Command Line Tool
```bash
# display usage information
./phishfry.py -h

# Deletes message with message_id=<message_id> from the test@example.com mailbox
./phishfry.py delete test@example.com "<message_id>"

# Restores message with message_id="<message_id>" to the test@example.com mailbox
./phishfry.py restore test@example.com "<message_id>"
```

## Library
```python
import EWS

# create an EWS session
session = EWS.Session("admin@example1.com", "123456")

# resolve all mailboxes that an address delivers to
mailboxes = session.Resolve("user@example.com")

# delete a message from all mailboxes
for address in mailboxes:
	try:
		mailboxes[address].Delete("<message_id>")
	except Exception as e:
		print(e)

# restore a message to all mailboxes
for address in mailboxes:
	try:
		session.Restore("<message_id>")
	except Exception as e:
		print(e)
```
