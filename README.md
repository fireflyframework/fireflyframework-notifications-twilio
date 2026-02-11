# Firefly Framework - Notifications - Twilio

[![CI](https://github.com/fireflyframework/fireflyframework-notifications-twilio/actions/workflows/ci.yml/badge.svg)](https://github.com/fireflyframework/fireflyframework-notifications-twilio/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-21%2B-orange.svg)](https://openjdk.org)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-green.svg)](https://spring.io/projects/spring-boot)

> Twilio SMS adapter for Firefly Notifications.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Overview

Firefly Framework Notifications Twilio implements the `SMSProvider` interface from the Firefly Notifications core module using Twilio as the delivery provider. It provides `TwilioSMSProvider` which handles SMS delivery through the Twilio API.

The module includes auto-configuration for seamless activation when included on the classpath alongside the notifications core module. Configuration properties allow customizing API credentials and provider-specific settings.

## Features

- `SMSProvider` implementation using Twilio
- Spring Boot auto-configuration for seamless activation
- Configurable API credentials via application properties
- Standalone provider library (include alongside fireflyframework-notifications)

## Requirements

- Java 21+
- Spring Boot 3.x
- Maven 3.9+
- Twilio account and API credentials

## Installation

```xml
<dependency>
    <groupId>org.fireflyframework</groupId>
    <artifactId>fireflyframework-notifications-twilio</artifactId>
    <version>26.02.01</version>
</dependency>
```

## Quick Start

```xml
<dependencies>
    <dependency>
        <groupId>org.fireflyframework</groupId>
        <artifactId>fireflyframework-notifications</artifactId>
    </dependency>
    <dependency>
        <groupId>org.fireflyframework</groupId>
        <artifactId>fireflyframework-notifications-twilio</artifactId>
    </dependency>
</dependencies>
```

## Configuration

```yaml
firefly:
  notifications:
    twilio:
      account-sid: ACxxxxxxxxxx
      auth-token: your-auth-token
      from-number: +1234567890
```

## Documentation

No additional documentation available for this project.

## Contributing

Contributions are welcome. Please read the [CONTRIBUTING.md](CONTRIBUTING.md) guide for details on our code of conduct, development process, and how to submit pull requests.

## License

Copyright 2024-2026 Firefly Software Solutions Inc.

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.
