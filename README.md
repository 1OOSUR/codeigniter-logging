A CodeIgniter Logging Library
===================
Just a simple library that allows for multiple logs in CodeIgniter, rather than just the single log provided as standard.

Usage
-----
Just place the libraries/Logging.php file in your application's libraries directory and load it like a normal library:

>
>   $this->load->library('logging')
>

Loggers are configured via a logging.php file in the config directory, for example:

`
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
`