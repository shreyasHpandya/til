# Circular Import Problems

In python circular imports are generally fine. But there are a few cases one needs to watch out for.
In order to understand where this might be a problem one should understand how python import works.

To quote from [this](http://stackoverflow.com/questions/744373/circular-or-cyclic-imports-in-python)
StackOverflow post

>Imports are pretty straightforward really. Just remember the following:
>
>'import' and 'from xxx import yyy' are executable statements. They execute when the running program reaches that line.
>
>If a module is not in sys.modules, then an import creates the new module entry in sys.modules and then executes the code in the module. It does not return control to the calling module until the execution has completed.
>
>If a module does exist in sys.modules then an import simply returns that module whether or not it has completed executing. That is the reason why cyclic imports may return modules which appear to be partly empty.
>
>Finally, the executing script runs in a module named __main__, importing the script under its own name will create a new module unrelated to __main__.
>
>Take that lot together and you shouldn't get any surprises when importing modules.

That being said; cyclic imports are going to create problems in following scenarios

* trying to access an atribute of module (which is in cyclic dependency) in main block
* trying to import attribute like `from module import foo`
* trying to import attribute like `import module.foo`

I am sure there are more cases that can be problematic but these are the most obvious ones
