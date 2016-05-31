## php-cli-lock

A simple class for process locking for things suck as cron jobs, etc.  The class can also
be easily dropped into CodeIgniter as a library and used for CLI processes that
utilize the CLI functionality of a Controller as outlined here:

http://www.codeigniter.com/userguide3/general/cli.html

### Example standalone usage:
* Include/require the class
```
require 'Cli_lock.php';
```
* Instantiate and initialize an object with the name of the lock to use
```
$cli_lock = new Cli_lock('example');
```
* Attempt to set the lock.  If successful do your processing, if not do whatever you want to do when there is already an instance running.
```
if($cli_lock->setLock()) {
    // Lock set, do your processing
    echo "Yay I can run";
    
    // When done clear your lock file
    $cli_lock->clearLock();
} else {
    // Failed to set lock, is another process running or failed?
    // Probably output or log a message at least
    echo "Oh no another instance is running.  Don't do anything"
}
```

### Example CodeIgniter Usage
* Download the file into your application/libraries directory
* Load the library in your controller as needed
```
$this->load->library('cli_lock');
```
* Initialize and attempt to lock your process.
```
$this->cli_lock->init('example');
if($this->cli_lock->setLock()) {
    // Lock set, do your processing
    echo "Yay I can run";
    
    // When done clear your lock file
    $this->cli_lock->clearLock();
} else {
    // Failed to set lock, is another process running or failed?
    // Probably output or log a message at least
    echo "Oh no another instance is running.  Don't do anything"
}
```
