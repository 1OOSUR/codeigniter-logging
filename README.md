A CodeIgniter Logging Library
===================
A simple library that allows for multiple logs in CodeIgniter, rather than just the single log provided as standard.

This comes in useful in many cases, for example debugging a particular application without all the standard CI debugging messages.

Usage
-----
Just place the libraries/Logging.php file in your application's libraries directory and load it like a normal library:

    $this->load->library('logging')

Loggers are configured via a logging.php file in the config directory, for example:

    $config = array(
        'simple' => array(
            'level' => 'INFO',
            'type' => 'file',
            'format' => "{message}",
            'file_path' => '' // Use the default application/logs directory
        ),
        'just_critical' => array(
            'level' => 'CRITICAL',
            'type' => 'file',
            'format' => "{date}: {message}",
            'file_path' => 'critical' // Will save log files to application/logs/critical
        )
    );

A particular logger can be selected using get_logger('name') which opens up five logging methods:

    $logger = $this->logging->get_logger('simple');
    $logger->debug('..');
    $logger->info('..');
    $logger->warning('..');
    $logger->error('..');
    $logger->critical('..');

Logger Configuration
--------------------

All loggers have the same four configuration options:

* **name** The key of the array element. In the example above, 'simple' and 'just_critical' are names.
* **level** The level of message the logger accepts. Works the same as the standard CodeIgniter logging, i.e. 'DEBUG', 'INFO', 'WARNING', 'ERROR', 'CRITICAL'. Each extra level is inclusive of the more restrictive levels below it, for example a logger with WARNING level will also log ERROR and CRITICAL errors.
* **type** Logger type. See the available types in the next section.
* **format** The format of log messages. Uses the same syntax as the [CodeIgniter template parser class](http://ellislab.com/codeigniter/user-guide/libraries/parser.html). Available template variables are message, level, date, logger_level, logger_name.

Types of Loggers
----------------

At the moment there are three types of loggers available:

* File (type => 'file')
* Email (type => 'email')
* Null (type => 'null')

### FileLogger

Mimics the default CodeIgniter logging functionality by writing log messages to file.
Log files are named uniquely using the logger's identifier.

Additional Configuration:
* **file_path**
The path under which to store log files. If empty, the CodeIgniter configured log path is used.
If **file_path** is relative, it is appended to the end of the CodeIgniter log path (e.g. application/logs/my_custom_log_folder). 
Use an absolute path in order to completely change where log files are written.

### EmailLogger

Sends each log message by email to a defined email address. Quite simply an interface to the CodeIgniter email library, so that needs to be configured appropriately for your environment.

Additional Configuration:
* **subject** Subject of the email
* **to** Email address to send to
* **from** Email address to send from (typically a noreply)

The formatted log message will form the body of the email.

### NullLogger

For testing purposes or dummy logging. Messages go nowhere.
