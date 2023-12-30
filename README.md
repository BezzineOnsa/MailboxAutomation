# Mailbox Automation

This Spring Boot project provides a robust and asynchronous solution for receiving and processing emails using the JavaMail and Spring Integration frameworks. 

## Configuration

The application's behavior and settings can be configured through the `application.yml` file. Key configuration parameters include:

### Log Level Configuration

Adjust the log levels for different packages to control the verbosity of logging.

```yaml
logging:
  level:
    root: INFO
    com.bezzine: DEBUG
    org.springframework.integration: DEBUG
```

### Mail Configuration

Configure the IMAP mail server settings, including SSL, host, port, username, and password.

```yaml
mail:
  imap:
    ssl: true
    host: imap.gmail.com
    port: 993
    username: your-email%40gmail.com
    password: your-password
```

### Task Execution Configuration

Fine-tune the task execution settings, such as thread pool size and scheduling.

```yaml
spring:
  task:
    execution:
      thread-name-prefix: autohost-task-
      pool:
        core-size: 2
        max-size: 200
        queue-capacity: 10000
    scheduling:
      thread-name-prefix: mail-receiver-
      pool:
        size: 2
```

## Code Structure

### `ReceiveMailServiceImpl` Class

The `ReceiveMailServiceImpl` class implements the `ReceiveMailService` interface and provides the core functionality for handling received emails.

Key methods include:

#### `handleReceivedMail`

Processes the received email, extracts information, and triggers further actions.

#### `fetchMessagesInFolder`

Fetches details of messages in the specified mail folder.

#### `copyMailToDownloadedFolder`

Copies the processed email to a "downloaded" folder.

#### `extractMail`

Extracts information from the MIME message, displays content, and downloads attachments.

#### `showMailContent`

Logs basic information about the email content.

#### `downloadAttachmentFiles`

Downloads attachment files and saves them to a specified folder.

### `MailReceiverConfiguration` Class

The `MailReceiverConfiguration` class configures the Spring Integration components for receiving emails.

Key methods include:

#### `receive`

Invoked when a new email is received, delegates the handling to the `ReceiveMailService`.

#### `defaultChannel`

Configures the default message channel for email reception.

#### `mailMessageSource`

Configures the mail receiving message source with a specified `MailReceiver`.

#### `imapMailReceiver`

Configures the IMAP mail receiver with the necessary properties.

### `AsyncConfiguration` Class

The `AsyncConfiguration` class configures asynchronous task execution using Spring's `ThreadPoolTaskExecutor`.

## Dependencies

The project relies on several dependencies, including Spring Boot, Spring Integration, Spring Mail, and other utility libraries. Notable dependencies include:

- `spring-boot-starter-data-jpa`
- `spring-boot-starter-web`
- `spring-boot-starter-mail`
- `spring-integration-mail`
- `commons-io`
- `commons-lang3`
- `commons-email`

## Building and Running the Application

To build and run the application, use the provided Maven configuration. The main class to execute is `MailboxAutomationApplication`.

```bash
./mvnw spring-boot:run
```

## Notes

- This application is built with Spring Boot 3.2.1 and Java 17.
- Ensure that the necessary dependencies are available and configured in the `pom.xml` file.
- 
