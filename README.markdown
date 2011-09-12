todo.txt-php is a PHP library to access todo.txt files, validate them
and handle saving them to file.

## Scope

The library will support PHP 5.3 (although should support 5.2+
if namespaces are removed and classes named like
`TodoTxt_Loader_LocalLoader` - not tested).

Parsing errors should be silent (and should resort to the offending text
being represented as is where possible). However other errors should
result in exceptions.

The following features are roadmapped:

*   Task manipulation via a model.
*   Parsing a task into a model from a text string.
*   Full unit-testing.
*   Ability to sort and filter the tasks.
*   Loading task files from a local text file and remotely from Dropbox.
*   Pushing modified lists back to their origin.
*   Supporting both 'standalone' and 'archive' lists - a single text
    file and a setup where archived tasks are moved to `done.txt`.

## Quickstart

Use the following autoloader (or add the directory to your existing 
autoloader):

    set_include_path(get_include_path() . PATH_SEPARATOR . "/path/to/TodoTxt/../");
    function __autoload($name) {
        require_once str_replace(array("\\", "_"), "/", $name) . ".php";
    }

Then the following code will load a list from a local text file:

    $loader = new TodoTxt\Loader\LocalLoader("~/Dropbox/todo/");
    //$loader = new TodoTxt\Loader\LocalLoader("~/todo.txt"); //standalone
    $list = $loader->pull();
    
    foreach ($list as $task) {
        print $task . "\n";
    }