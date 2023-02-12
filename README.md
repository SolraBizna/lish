
This is Lish, the Liso Shell. It shows off many of the features of the Liso crate. It's also useful in its own right, primarily for wrapping around game servers (such as _Vintage Story_ servers) that are very chattery and have only basic console IO. I really don't recommend setting it as your primary shell—for one thing, it can't handle interactive TUI applications like text editors—but if you really want to, knock yourself out.

# Installation

If you have a Rust environment installed, you can install Lish with `cargo install lish`. If not, the easiest way to get Lish is to [install a Rust environment](https://www.rust-lang.org/learn/get-started) and then… `cargo install lish`.

# Invocation

If invoked with no arguments, Lish will simply start the main prompt. If invoked with one or more arguments, each argument is treated as a separate command to run. For example:

```sh
lish 'start_vs_server.sh' 'java -jar minecraft_server.jar'
```

Commands specified on the command line are treated exactly like they entered at the main prompt, including name specification. **Each argument is an entire command line, you must use quotes or backslashes if you want to have a command line that contains a space or other symbols.** You may need to perform multiple levels of backslash escaping to get everything to work how you want.

# Main Prompt

The main prompt allows you to spawn new commands.

At the main prompt, the following builtin commands are available:

- `cd [DIR...]`: Change working directory
- `exit [STATUS]`: Exit Lish, or enter Batch Mode
- `help`: This help
- `unsetenv <VARNAME...>`: Blank environment variables
- `setenv <VARNAME=VALUE...>`: Set environment variables
- `jobs`: Show all running jobs

Anything you enter at the main prompt will either be one of these builtin commands, or will be sent to the operating system for execution as a job. Lish will switch to newly-started jobs automatically. You can return to the main prompt with control-X.

# Jobs

You can start jobs at the main prompt, or by supplying jobs on Lish's command line. Jobs will normally be named according to their first element. You can specify a custom name, that does not get included in the actual command to execute, by specifying it, followed by a colon, at the start of the command line:

```sh
public: start_server.sh ~/public_server
private: start_server.sh ~/private_server
esperanto: LANG=eo start_server.sh ~/esperanto_server
```

(Custom names cannot contain spaces or backslash escapes. If you want to run a command whose name would otherwise count as a custom name, you can put a single space before it.)

Use control-X to switch between running jobs, or to return to the main prompt (if present) to start additional jobs. If you're on a UNIX (such as BSD or Linux), you can press control-C to terminate the currently-selected job.

# Batch Mode

If you specify commands on the command line, Lish will start in Batch Mode instead of Interactive Mode. In this mode, Lish will exit with status `0` if all jobs completed successfully, or a non-zero status if any failed. You can, instead, request that the main prompt be started by passing `-i` as an argument, in which case, Lish will operate normally.

You can also enter Batch Mode by typing `exit` with no parameters at the main prompt.

# Exiting

You can exit by entering `exit` or typing control-C at the main prompt. If there is no main prompt, Lish will exit automatically when all jobs have terminated.

# Legalese

Lish is copyright 2022-2023, Solra Bizna, and licensed under either of:

 * Apache License, Version 2.0
   ([LICENSE-APACHE](LICENSE-APACHE) or
   <http://www.apache.org/licenses/LICENSE-2.0>)
 * MIT license
   ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.

Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion in the Liso crate by you, as defined
in the Apache-2.0 license, shall be dual licensed as above, without any
additional terms or conditions.
