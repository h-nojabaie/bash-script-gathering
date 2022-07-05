#### Environment Variables

- Local variable

  A local environment variable is one that is set during a shell session and is erased when the shell is closed.

  ```bash
  export GLOBAL="this is global variable"
  echo $MY_VARIABLE
  ```

- Global variables 

  A global environment variable is one that is set upon initialization of a shell and can be used across all your shells.

  ```bash
  # write this in ~./profile
  export GLOBAL_VARIABLE="some value"
  ```

- To see all of the environment variables in your current environment.

  ```bash
  env
  ```

  

#### Shell Variables

Similar to Environment variables but not accessible in other script.

```bash
MY_SHELL_VARIABLE="some value"
```



#### PATH Variable

The most important global environment variable that you must set is the `PATH` variable. This is the variable that tells the bash shell where to find different executable files and scripts.

```bash
echo $PATH
# /usr/local/sbin:/usr/local/bin:/usr/sbin:
```

To add some path to PATH:

```bash
# for the end of the PATH
export PATH=$PATH:<some path>
# for the start of the PATH
export PATH=<some path>:$PATH
```

