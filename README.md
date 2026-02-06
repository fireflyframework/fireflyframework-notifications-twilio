# fireflyframework-notifications-twilio

Twilio SMS adapter for Firefly Notifications Library.

## Overview

This module is an **infrastructure adapter** in the hexagonal architecture that implements the `SMSProvider` port interface. It handles all Twilio-specific integration details, including API authentication, request formatting, and SMS delivery.

### Architecture Role

```
Application Layer (SMSService)
    ↓ depends on
Domain Layer (SMSProvider interface)
    ↑ implemented by
Infrastructure Layer (TwilioSMSProvider) ← THIS MODULE
    ↓ calls
Twilio REST API
```

This adapter can be replaced with other SMS providers (AWS SNS, Vonage) without changing your application code.

## Installation

Add these dependencies to your `pom.xml`:

```xml path=null start=null
<dependency>
  <groupId>org.fireflyframework</groupId>
  <artifactId>fireflyframework-notifications-core</artifactId>
  <version>1.0.0-SNAPSHOT</version>
</dependency>

<dependency>
  <groupId>org.fireflyframework</groupId>
  <artifactId>fireflyframework-notifications-twilio</artifactId>
  <version>1.0.0-SNAPSHOT</version>
</dependency>
```

## Configuration

Add the following to your `application.yml`:

```yaml path=null start=null
notifications:
  sms:
    provider: twilio  # Enables this adapter

twilio:
  config:
    account-sid: ${TWILIO_ACCOUNT_SID}
    auth-token: ${TWILIO_AUTH_TOKEN}
    phone-number: "+1234567890"  # Your Twilio phone number
```

### Getting Your Credentials

1. Sign up at [twilio.com](https://www.twilio.com)
2. Get your Account SID and Auth Token from the console dashboard
3. Purchase or verify a phone number
4. Set as environment variables:
   ```bash
   export TWILIO_ACCOUNT_SID="ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
   export TWILIO_AUTH_TOKEN="your-auth-token"
   ```

## Usage

Inject `SMSService` from the core library. Spring automatically wires this adapter:

```java path=null start=null
@Service
public class VerificationService {
    
    @Autowired
    private SMSService smsService;
    
    public void sendVerificationCode(String phoneNumber, String code) {
        SMSRequestDTO request = SMSRequestDTO.builder()
            .phoneNumber(phoneNumber)
            .message("Your verification code is: " + code)
            .build();
        
        smsService.sendSMS(request)
            .subscribe(response -> {
                if (response.isSuccess()) {
                    log.info("SMS sent: {}", response.getMessageId());
                } else {
                    log.error("Failed: {}", response.getError());
                }
            });
    }
}
```

## Features

- **International SMS** - Supports sending to any country Twilio serves
- **Synchronous API** - Returns response immediately
- **Error handling** - Validates phone numbers and handles API errors
- **Delivery tracking** - Returns Twilio message SID for status tracking

## Switching Providers

To switch from Twilio to another SMS provider:

1. Remove this dependency from `pom.xml`
2. Add alternative SMS adapter dependency
3. Update configuration to use different provider

**No code changes required** in your services—hexagonal architecture ensures provider independence!

## Implementation Details

This adapter:
- Implements `SMSProvider` interface from `fireflyframework-notifications-core`
- Uses Twilio Java SDK for API calls
- Transforms `SMSRequestDTO` to Twilio's `Message` format
- Handles authentication via Account SID and Auth Token
- Returns standardized `SMSResponseDTO`

## Troubleshooting

### Error: "No qualifying bean of type 'SMSProvider'"

- Ensure `notifications.sms.provider=twilio` is set
- Verify Twilio credentials are configured

### Error: "Invalid phone number"

- Phone numbers must be in E.164 format (e.g., +1234567890)
- Ensure the number includes country code

### Error: "Insufficient balance"

- Check your Twilio account balance
- Add funds or use trial credits for testing

## References

- [Twilio SMS API Documentation](https://www.twilio.com/docs/sms/api)
- [Firefly Notifications Architecture](../fireflyframework-notifications/ARCHITECTURE.md)
