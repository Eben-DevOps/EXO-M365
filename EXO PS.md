Here are some of the most commonly performed tasks in **Exchange Online PowerShell**:

### 1. **Managing Mailboxes**

#### a. **Get a List of All Mailboxes**
```powershell
Get-Mailbox
```
This retrieves all mailboxes in your organization.

#### b. **Create a New Mailbox**
```powershell
New-Mailbox -UserPrincipalName john.doe@yourdomain.com -Alias johndoe -FirstName John -LastName Doe -Password (ConvertTo-SecureString "Password123" -AsPlainText -Force)
```
Creates a new mailbox for a user.

#### c. **Set or Change Mailbox Properties**
```powershell
Set-Mailbox -Identity "john.doe@yourdomain.com" -DisplayName "John Doe" -EmailAddresses "SMTP:johndoe@yourdomain.com"
```
Modify properties of an existing mailbox, such as display name or email addresses.

#### d. **Enable or Disable Mailbox Features**
```powershell
Set-CasMailbox -Identity "john.doe@yourdomain.com" -OWAEnabled $false -PopEnabled $false -ImapEnabled $false
```
This disables OWA, POP, and IMAP for a user mailbox.

#### e. **Remove a Mailbox**
```powershell
Remove-Mailbox -Identity "john.doe@yourdomain.com"
```
Deletes a mailbox from Exchange Online.

### 2. **Managing Distribution Groups**

#### a. **Get a List of Distribution Groups**
```powershell
Get-DistributionGroup
```
Retrieves all distribution groups.

#### b. **Create a New Distribution Group**
```powershell
New-DistributionGroup -Name "Marketing Team" -PrimarySmtpAddress marketing@yourdomain.com -Alias "MarketingTeam"
```
Creates a new distribution group.

#### c. **Add Members to a Distribution Group**
```powershell
Add-DistributionGroupMember -Identity "Marketing Team" -Member "john.doe@yourdomain.com"
```
Adds a member to a distribution group.

#### d. **Remove Members from a Distribution Group**
```powershell
Remove-DistributionGroupMember -Identity "Marketing Team" -Member "john.doe@yourdomain.com"
```
Removes a member from a distribution group.

### 3. **Mail Flow and Message Trace**

#### a. **Get Mail Flow Rules (Transport Rules)**
```powershell
Get-TransportRule
```
Retrieve all mail flow rules that govern how messages are handled and routed.

#### b. **Create a New Mail Flow Rule**
```powershell
New-TransportRule -Name "Block External Email" -FromScope NotInOrganization -SentTo "blockemail@yourdomain.com" -RejectMessageReasonText "External emails are not allowed."
```
Creates a rule that blocks external email to a specific user.

#### c. **Run a Message Trace**
```powershell
Get-MessageTrace -Sender "john.doe@yourdomain.com" -StartDate "09/01/2024" -EndDate "09/05/2024"
```
Trace messages sent from a user within a specified date range.

#### d. **Get Detailed Message Trace**
```powershell
Get-MessageTraceDetail -MessageTraceId "trace-id"
```
Provides detailed information about the path a message took.

### 4. **Managing Retention Policies**

#### a. **Get a List of Retention Policies**
```powershell
Get-RetentionCompliancePolicy
```
Retrieves all retention policies.

#### b. **Assign a Retention Policy to a Mailbox**
```powershell
Set-Mailbox -Identity "john.doe@yourdomain.com" -RetentionPolicy "Default MRM Policy"
```
Assigns a retention policy to a user mailbox.

#### c. **Create a New Retention Policy**
```powershell
New-RetentionCompliancePolicy -Name "HR Retention Policy" -RetentionDuration 365 -RetentionAction PermanentlyDelete
```
Creates a new retention policy that deletes items after 365 days.

### 5. **Shared Mailboxes**

#### a. **Create a Shared Mailbox**
```powershell
New-Mailbox -Shared -Name "Support" -PrimarySmtpAddress support@yourdomain.com
```
Creates a new shared mailbox.

#### b. **Add Permissions to a Shared Mailbox**
```powershell
Add-MailboxPermission -Identity "support@yourdomain.com" -User "john.doe@yourdomain.com" -AccessRights FullAccess -AutoMapping $true
```
Gives a user full access to a shared mailbox.

#### c. **Send As Permissions for a Shared Mailbox**
```powershell
Add-RecipientPermission -Identity "support@yourdomain.com" -Trustee "john.doe@yourdomain.com" -AccessRights SendAs
```
Allows a user to send email as the shared mailbox.

### 6. **Mailbox Auditing**

#### a. **Enable Mailbox Auditing for a Single Mailbox**
```powershell
Set-Mailbox -Identity "john.doe@yourdomain.com" -AuditEnabled $true
```
Enables mailbox auditing to track actions such as mailbox access and email deletions.

#### b. **Search Mailbox Audit Logs**
```powershell
Search-MailboxAuditLog -Mailboxes "john.doe@yourdomain.com" -StartDate "2024-01-01" -EndDate "2024-01-31" -Operations SendOnBehalf, MoveToDeletedItems
```
Retrieve audit logs for specific mailbox actions.

### 7. **Managing Forwarding and Redirection**

#### a. **Set Email Forwarding for a User**
```powershell
Set-Mailbox -Identity "john.doe@yourdomain.com" -ForwardingSMTPAddress "forwardto@yourdomain.com" -DeliverToMailboxAndForward $true
```
Sets up forwarding for a mailbox, with an option to keep a copy of the email in the original mailbox.

#### b. **Remove Email Forwarding**
```powershell
Set-Mailbox -Identity "john.doe@yourdomain.com" -ForwardingSMTPAddress $null
```
Removes email forwarding.

### 8. **Managing Calendar Permissions**

#### a. **Get Calendar Permissions for a Mailbox**
```powershell
Get-MailboxFolderPermission -Identity "john.doe@yourdomain.com:\Calendar"
```
Retrieve the list of users who have permissions to access a user’s calendar.

#### b. **Add Calendar Permissions for a User**
```powershell
Add-MailboxFolderPermission -Identity "john.doe@yourdomain.com:\Calendar" -User "mary.smith@yourdomain.com" -AccessRights Editor
```
Grants a user **Editor** access to another user's calendar.

### 9. **Mailbox Storage and Quota Management**

#### a. **Check Mailbox Quota Usage**
```powershell
Get-MailboxStatistics -Identity "john.doe@yourdomain.com" | Select-Object DisplayName, TotalItemSize
```
Check how much storage a mailbox is using.

#### b. **Set Mailbox Storage Quota**
```powershell
Set-Mailbox -Identity "john.doe@yourdomain.com" -IssueWarningQuota 90GB -ProhibitSendQuota 95GB -ProhibitSendReceiveQuota 100GB
```
Set storage quotas for a mailbox, including warning and send/receive limits.

### 10. **Managing Litigation Hold**

#### a. **Enable Litigation Hold for a Mailbox**
```powershell
Set-Mailbox -Identity "john.doe@yourdomain.com" -LitigationHoldEnabled $true -LitigationHoldDuration 365
```
Places a mailbox on litigation hold, which preserves mailbox content for a specified period.

#### b. **Disable Litigation Hold**
```powershell
Set-Mailbox -Identity "john.doe@yourdomain.com" -LitigationHoldEnabled $false
```
Removes litigation hold from a mailbox.

---

These tasks cover a wide range of administrative responsibilities in **Exchange Online**, from managing mailboxes and distribution groups to configuring mail flow rules and auditing mailbox activity.
