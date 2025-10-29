# lib-notifications-twilio

Twilio SMS adapter for Firefly Notifications.

## Install
```xml path=null start=null
<dependency>
  <groupId>com.firefly</groupId>
  <artifactId>lib-notifications-twilio</artifactId>
  <version>1.0.0-SNAPSHOT</version>
</dependency>
```

## Configuration (application.yml)
```yaml path=null start=null
twilio:
  config:
    accountSid: ${TWILIO_ACCOUNT_SID}
    authToken: ${TWILIO_AUTH_TOKEN}
    phoneNumber: "+1XXXXXXXXXX"
```

## Usage
Inject `SMSService` from `lib-notifications-core`; this adapter provides the implementation via Spring.
