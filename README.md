# Objective

To make logging setup in python reusable and extensible. I have been replicating this setup quite a few times across many projects I worked. Hence the repo.

# How to use?

Currently you can include it as a git submodule. Later, I will release this in PYPI.
```
git submodule add https://github.com/chaconinc/DbConnector
```

Include *our requirements* to *your requirements*. For instance, we rely on PyYAML to load logging configurations.

```
vim /path/to/your/requirements.txt
-r py_logging_setup/requirements.txt
```

Then whichever file you want to log stuff in your application, do,
```
from py_logging_setup.main import setup_logging
# for default logging setup which logs to the console. default level=INFO, default logger=console, default config file=logging.yaml.
setup_logging()
LOGGER = logging.getLogger('console')
LOGGER.info("Hello World!")
# output in your console.
>> 2020-05-20 12:16:31,767 - console - INFO - Hello World!

# read config from another file.
export LOGGING_YAML_CONFIG=/path/to/logging.yaml
setup_logging(config_env_key='LOGGING_YAML_CONFIG')
```
