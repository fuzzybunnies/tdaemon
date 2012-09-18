## Test Daemon

The test daemon watches the content of files in a directory and if any of them
changes (the content is edited), it runs the tests.

### Installation

Put the tdaemon somewhere where it's executable.

### Basic Usage

Simply run this:

    $ python /path/to/tdaemon.py

The daemon starts watching the current directory and subdirectories. As soon as
one file changes, the daemon runs ``nosetests`` and you may watch the result.

### Advanced usage

#### Change the scanned path

If you want to run the daemon from another directory than your current
directory, just run:

    $ tdaemon.py /path/to/your/project


#### Change the test program

For example, try out ``py.test``:

    $ tdaemon.py --test-program=py

``Nosetests`` is the default test program, but you may use others.

The available test programs are:

* [nosetests](http://somethingaboutorange.com/mrl/projects/nose/) (keyword is `nose` or `nosetests`)
* [django](http://docs.djangoproject.com/en/dev/topics/testing/) (keyword is `django`)
* [py.test](http://codespeak.net/py/dist/test.html) (keyword is `py`)
* [symfony](http://www.symfony-project.org/) (keyword is `symfony`)
* [jelix](http://jelix.org/) (keyword is `jelix`)
* [phpunit](http://www.phpunit.de/manual/current/en/index.html) (keyword is `phpunit`)
* [sphinx](http://sphinx.pocoo.org/) (keyword is `sphinx`)

Bear in mind that if you want to use one of these program, you **must** install
them on your system.

*Note* : When you're using django, the path to the project must be the path where
`manage.py` lives.

#### Add parameters to your test program

Most test programs allow you to test using specifig arguments, to test a small
part of your project, or using a specific setting. If you want to append
specific arguments to your command line, use the ``--custom-args`` parameter
like this::

    $ tdaemon.py --custom-args="myapp.MyTestClass" --test-program=django

The above command will execute the following command in the current directory:

    $ ./manage.py myapp.MyTestClass

Please refer to the test program manual / documentation to find out which
additional argument you may use here.

**WARNING**: Please note that every time you're going to use this option, it
will require your confirmation. You are being warned that any command that
would break your system, erase some important data, etc. is
**YOUR PLAIN FAULT!**. Not mine. So BE CAREFUL. Please.

#### The max filesize

The ``tdaemon`` first checks the total filesize you want to scan. If the total
file size exceeds his quota (which is 25MB by default), the program asks you if
you still want to go on with this. You may be informed that scanning large
directories may take some time, and thus alter the daemon performances.

You can change this quota by using the ``--size-max`` argument. For example:

    $ tdaemon --size-max=100

With this argument, the programm will only ask for your permission to proceed
with a total archive of more than 100MB.
