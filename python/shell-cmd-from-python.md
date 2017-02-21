There are infinitely many ways to execute shell commands from python so to resolve the dilemma once and for all keep following points in mind

* `os.system` and `os.popen*` are old school. subprocess.Popen replaces them all
* most obvious use case is `subprocess.check_output` which executes the command and wait and raises `CalledProcessError` if fails else returns output
* if you dont want to raise exception on non zero exit code use `subprocess.call`
* to use pipe supply shell=True `subprocess.call('ls -al | grep 'foo', shell=True)`. Shell=True is not secure so be careful and use more secure way of using pipe. Check docs

eg

    try:
        output = subprocess.check_output(['ls','-al'])
    except subprocess.CalledProcessError as e:
        print e.returncode, e.output
