# Logging Events

## Purpose of logging

There are 2 main goals in logging :

- **Diagnosis** : records events related to the operations of an application
- **Audit** : records events for business analysis.

The Python [`logging`](https://docs.python.org/3/library/logging.ht) library is a convenient way to do so. It has a number of advantages over printing :

- Easy to see **where** and **when** (even what line no.) a logging call is being made from.
- You can log to `files`, `sockets`, pretty much anything, all **at the same time**.
- You can differentiate your logging based on **severity levels**.
- If your project is meant to be **imported by other python tools**, it's bad practice for your package to print things to stdout, since the user likely won't know where the print messages are coming from. With logging, users of your package can choose whether they want to propogate logging messages from your tool or not.

For more details about logging, please see basic and advanced tutorials [here](https://docs.python.org/3/howto/logging.html)

## Severity Levels

| Level | When it’s used |
| --- | --- |
| `DEBUG` | Detailed information, typically of interest only when diagnosing problems. |
| `INFO` | Confirmation that things are working as expected. |
| `WARNING` | An indication that something unexpected happened, or indicative of some problem in the near future (e.g. ‘disk space low’). The software is still working as expected. |
| `ERROR` | Due to a more serious problem, the software has not been able to perform some function. |
| `CRITICAL` | A serious error, indicating that the program itself may be unable to continue running. |

## Logger configuration

There are 3 methods to configure a logger in Python :

- `INI` file :
    - Pros : change the config during the execution.
    - Cons : less control.
- Using a Python `Dict` or `JSON` formatted file :
    - Pros : change the config during the execution 
    - Cons : less control than with code.
- Directly with **code** : 
    - Pros : complete control on the configuration.
    - Cons : need to change source code.

## Examples

### INI File

```toml title="config.ini"
[loggers]
keys=root

[handlers]
keys=stream_handler

[formatters]
keys=formatter

[logger_root]
level=DEBUG
handlers=stream_handler

[handler_stream_handler]
class=StreamHandler
level=DEBUG
formatter=formatter
args=(sys.stderr,)

[formatter_formatter]
format=%(asctime)s %(name)-12s %(levelname)-8s %(message)s
```

Then use `logging.config.fileConfig()` in the code:

```python title="app.py"
import logging
from logging.config import fileConfig

fileConfig('config.ini')
logger = logging.getLogger()
logger.debug('often makes a very good meal of %s', 'visiting tourists')
```

### JSON

```python title="app.py"
import logging
from logging.config import dictConfig

logging_config = dict(
    version = 1,
    formatters = {
        'f': {'format':
              '%(asctime)s %(name)-12s %(levelname)-8s %(message)s'}
        },
    handlers = {
        'h': {'class': 'logging.StreamHandler',
              'formatter': 'f',
              'level': logging.DEBUG}
        },
    root = {
        'handlers': ['h'],
        'level': logging.DEBUG,
        },
)

dictConfig(logging_config)

logger = logging.getLogger()
logger.debug('often makes a very good meal of %s', 'visiting tourists')
```

### Code

```python title="app.py"
import logging

logger = logging.getLogger()
handler = logging.StreamHandler()
formatter = logging.Formatter('%(asctime)s %(name)-12s %(levelname)-8s %(message)s')
handler.setFormatter(formatter)
logger.addHandler(handler)
logger.setLevel(logging.DEBUG)

logger.debug('often makes a very good meal of %s', 'visiting tourists')
```

For simple configuration needs, we can use the `basicConfig()` function.

```python title="app.py"
import logging

logging.basicConfig(
    encoding="utf-8",
    level=INFO,
    format="[%(asctime)s] %(levelname)-7s %(module)-15s %(lineno)-5d : %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S",
    handlers=[
        RotatingFileHandler(            # saves logs to a new file once the size of the current logfile reach the maxBytes size
            filename,
            maxBytes=2 * 1024 * 1024,
            backupCount=5,
        ),
        logging.StreamHandler(),        # to display logs in the standard output (terminal)
    ],
)

logging.info("Opening file...")
...
logging.error("File doesn't exists")
```

## Log records format

For the above format

```python
"[%(asctime)s] %(levelname)-7s %(module)-15s %(lineno)-5d : %(message)s" 
```

The output file might look like this :

```log title="app.log"
[2023-12-06 11:19:53] DEBUG   db              25    : Creating database connection object...
[2023-12-06 11:19:53] DEBUG   db              37    : Connection object created successfully.
[2023-12-06 11:19:53] INFO    utils           84    : Database is up
[2023-12-06 11:19:53] DEBUG   db              42    : Database connection closed.
```

The log format can be customize through [LogRecords attributes](https://docs.python.org/3/library/logging.html#logrecord-attributes) to get a very descriptive insight from the log.
