# Sublime PHPUnit

Convenient Sublime Text commands for running your PHPUnit tests. Scans up the directory tree to find the closest phpunit.xml file and runs phpunit from there. If it can't find one, it just runs phpunit from `/`.

## Installation


Installation is as simple as cloning the repository into your Sublime Text install's `Packages` folder:

```bash
git clone https://github.com/adamwathan/sublime-phpunit ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/sublime-phpunit
```

## Available Commands & Example Keybindings

You can find the commands in the command palette under "Sublime PHPUnit", or map any of these commands to whatever shortcuts you want:

Here's the full list of commands:

```
run_phpunit_test
run_phpunit_tests_in_dir
run_single_phpunit_test
run_last_phpunit_test
run_all_phpunit_tests
run_single_dusk_test
run_all_dusk_tests
run_dusk_tests_in_dir
run_pint_on_current_file
````

Here are some example keybindings:

```json
[
    { "keys": ["alt+t"], "command": "run_phpunit_test"},
    { "keys": ["super+alt+t"], "command": "run_single_phpunit_test"},
    { "keys": ["super+alt+l+t"], "command": "run_last_phpunit_test"},
    { "keys": ["super+shift+t"], "command": "run_phpunit_tests_in_dir"},
    { "keys": ["super+shift+ctrl+t"], "command": "run_all_phpunit_tests"},
]

```

## Using iTerm2 instead of Terminal.app

By default, this package uses macOS's built-in Terminal.app. If you want to use iTerm2, you can do so changing the terminal in your settings:

```
{
    "phpunit-sublime-terminal": "iTerm",
}
```

## Using fish shell

If you use [fish shell](https://fishshell.com/), specify this in your settings: 

```
{
    "phpunit-sublime-shell": "fish"
}
``` 

This will instruct Sublime PHPUnit to connect the commands using fish's `; and` instead of bash's `&&`.

## Docker Support

If your PHP project runs inside Docker, you can have all commands execute inside a container via `docker compose exec`. Add the `phpunit-sublime-docker-service` setting to your `.sublime-project` file:

```json
{
    "settings": {
        "phpunit-sublime-docker-service": "app"
    }
}
```

Where `app` is the name of your Docker Compose service. When this setting is present, commands will be wrapped like:

```
cd /path/to/project && docker compose exec -e XDEBUG_MODE=off app php vendor/bin/phpunit tests/Feature/SomeTest.php
```

The `cd` runs on the host so `docker compose` can find your `docker-compose.yml`. File paths are automatically converted to project-relative paths for the container.

When this setting is absent, all commands run locally as usual.

## Auto-focus Sublime Text After Running Tests

If you want Sublime Text to automatically regain focus after a test is triggered, enable the following setting:

```json
{
    "phpunit-sublime-autofocus-after-run": true
}
```
