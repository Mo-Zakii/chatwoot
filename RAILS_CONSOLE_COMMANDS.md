# Rails Console Commands for BAITK Chatwoot

## Enable Enterprise Features for Account

After deploying your container, run these commands via Rails console to enable enterprise features:

### Option 1: Using Docker Exec
```bash
docker exec -it <container_name> bundle exec rails console

# Then in Rails console:
account = Account.find(1)  # Replace 1 with your account ID
account.enable_features!('captain', 'saml', 'custom_branding', 'agent_capacity', 'audit_logs', 'disable_branding')
```

### Option 2: Using Coolify CLI (if available)
```bash
# Access Rails console through Coolify
bundle exec rails console

# Enable all enterprise features at once
account = Account.find(1)
account.enable_features!('captain_integration', 'saml', 'disable_branding', 'audit_logs', 'sla', 'custom_roles', 'companies')

# Verify features
account.all_features
```

## List of Enterprise Features (Correct Names)
- `captain_integration` - AI-powered Captain (premium)
- `saml` - SAML SSO (premium)
- `disable_branding` - Remove "Powered by Chatwoot" (premium)
- `audit_logs` - Audit logging (premium)
- `sla` - SLA management (premium)
- `custom_roles` - Custom role management (premium)
- `companies` - Companies feature (premium)
- `advanced_search` - Advanced search (premium, internal)
- `channel_voice` - Voice channel (premium)

## Check Current Features
```ruby
account = Account.find(1)
account.all_features
```

## Contact Import

Chatwoot has **built-in CSV import functionality**:

1. Go to **Contacts** in your dashboard
2. Click the **Import** button
3. Upload your CSV file with the following columns:
   - `name` (required)
   - `email`
   - `phone_number`
   - `identifier` (custom identifier)
   - `additional_attributes` (JSON object for custom fields)

### CSV Format Example:
```csv
name,email,phone_number,identifier
John Doe,john@example.com,+1234567890,CUST001
Jane Smith,jane@example.com,+0987654321,CUST002
```

You can also import via **API** or **Rails Console** for bulk operations.
