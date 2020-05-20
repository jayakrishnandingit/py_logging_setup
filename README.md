# Objective

To make logging setup in python reusable and extensible. I have been replicating this setup quite a few times across many projects I worked. Hence the repo.

# How to use?

Currently you can include it as a git submodule. Later, I will release this in PYPI.
```
git submodule add git@github.com:jayakrishnandingit/py_logging_setup.git
```

Include *our requirements* to *your requirements*. For instance, we rely on PyYAML to load logging configurations.

```
vim /path/to/your/requirements.txt
-r py_logging_setup/requirements.txt
```

Then whichever file you want to log stuff in your application, do,
```
from py_logging_setup import setup_logging
# for default logging setup which logs to the console with default level INFO.
setup_logging()
LOGGER = logging.getLogger('console')
LOGGER.info("Hello World!")
# output in your console.
>> 2020-05-20 12:16:31,767 - console - INFO - Hello World!
```

## Define a config file to suit your needs.
```
# /path/to/your/logging.yaml
version: 1
disable_existing_loggers: false
formatters:
    simple:
        format: "%(asctime)s - %(name)s - %(levelname)s - %(message)s"
handlers:
    console:
        class: logging.StreamHandler
        level: DEBUG
        formatter: simple
        stream: ext://sys.stdout
    error:
        class: logging.handlers.RotatingFileHandler
        level: WARNING
        formatter: simple
        filename: error.log
        maxBytes: 1048576  # 1 MB
loggers:
    mymodule:
        level: INFO
        handlers: [console, error]
        propagate: yes

```
Set the logging yaml file path as an environment variable.
```
export LOGGING_YAML_CONFIG=/path/to/logging.yaml
```
Now pass the env variable key during the setup.
```
setup_logging(config_env_key='LOGGING_YAML_CONFIG')
```
