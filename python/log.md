Python中将打印输出导向日志文件

a. 利用sys.stdout将print行导向到你定义的日志文件中，例如：

import sys

# make a copy of original stdout route
stdout_backup = sys.stdout
# define the log file that receives your log info
log_file = open("message.log", "w")
# redirect print output to log file
sys.stdout = log_file

print "Now all print info will be written to message.log"
# any command line that you will execute
...

log_file.close()
# restore the output to initial pattern
sys.stdout = stdout_backup

print "Now this will be presented on screen"
b. 利用logging模块（规范化日志输出，推荐！！）
由于logging模块的功能比较多，下面就放一些文档里介绍的简单的例子，更详细具体的用法请戳这里

需求	最好的实现方式
故障调查或者状态监测	logging.info()或logging.debug()(后者常用于针对性检测诊断的目的)
特定运行事件发出警告	logging.warning()
报告错误抑制不出发异常（常见于长时间运行的服务器进程的错误处理程序）	logging.error(), logging.exception()或者logging.critical()
而以下是根据事件的严重性程度而应采取的logging函数的建议：

程度	使用场景
DEBUG	获得诊断问题是具体的信息
INFO	确认程序是否按正常工作
WARNING	在程序还正常运行时获取发生的意外的信息，这可能会在之后引发异常（例如磁盘空间不足）
ERROR	获取程序某些功能无法正常调用这类严重异常的信息
CRITICAL	获取程序无法继续运行的这类最严重异常信息
默认的等级是WARNING，也就是说logging函数在没有特别配置的前提下只追踪比WARNING程度更严重的异常。

下面就用一些例子来具体说明如何用logging函数记录日志信息：

# this is a simple example
import logging
# define the log file, file mode and logging level
logging.basicConfig(filename='example.log', filemode="w", level=logging.DEBUG)
logging.debug('This message should go to the log file')
logging.info('So should this')
logging.warning('And this, too')
查看example.log文件可以看到以下信息：

DEBUG:root:This message should go to the log file
INFO:root:So should this
WARNING:root:And this, too
从多个文件记录日志

# myapp.py
import logging
import mylib

def main():
    logging.basicConfig(filename='myapp.log', level=logging.INFO)
    logging.info('Started')
    mylib.do_something()
    logging.info('Finished')

if __name__ == '__main__':
    main()
# mylib.py
import logging

def do_something():
    logging.info('Doing something')
输出的信息为

INFO:root:Started
INFO:root:Doing something
INFO:root:Finished
改变默认输出信息的格式

import logging
# output format: output time - logging level - log messages
logging.basicConfig(format='%(asctime)s - %(levelname)s - %(message)s')
logging.warning('This message will appear in python console.')
在python console中直接打印以下输出：

2016-8-2 2:59:11, 510 - WARNING - This message will appear in python console
logging高级用法
可以通过构建logger或者读取logging config文件对logging函数进行任意配置。

构建logger法
import logging

# create logger
logger = logging.getLogger('simple_example')
logger.setLevel(logging.DEBUG)

# create console handler and set level to debug
ch = logging.StreamHandler()
ch.setLevel(logging.DEBUG)

# create formatter
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# add formatter to ch
ch.setFormatter(formatter)

# add ch to logger
logger.addHandler(ch)

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warn('warn message')
logger.error('error message')
logger.critical('critical message')
以上程序结果会输出到python console中：

$ python simple_logging_module.py
2005-03-19 15:10:26,618 - simple_example - DEBUG - debug message
2005-03-19 15:10:26,620 - simple_example - INFO - info message
2005-03-19 15:10:26,695 - simple_example - WARNING - warn message
2005-03-19 15:10:26,697 - simple_example - ERROR - error message
2005-03-19 15:10:26,773 - simple_example - CRITICAL - critical message
读取配置文件法
import logging
import logging.config

logging.config.fileConfig('logging.conf')

# create logger
logger = logging.getLogger('simpleExample')

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warn('warn message')
logger.error('error message')
logger.critical('critical message')
其中logging.conf文件格式为：(其实就是将前一种方法的各项配置参数写到logging.conf文件中)

[loggers]
keys=root,simpleExample

[handlers]
keys=consoleHandler

[formatters]
keys=simpleFormatter

[logger_root]
level=DEBUG
handlers=consoleHandler

[logger_simpleExample]
level=DEBUG
handlers=consoleHandler
qualname=simpleExample
propagate=0

[handler_consoleHandler]
class=StreamHandler
level=DEBUG
formatter=simpleFormatter
args=(sys.stdout,)

[formatter_simpleFormatter]
format=%(asctime)s - %(name)s - %(levelname)s - %(message)s
datefmt= '%m/%d/%Y %I:%M:%S %p'
与前面一样，上述文件输出结果为：

$ python simple_logging_config.py
2005-03-19 15:38:55,977 - simpleExample - DEBUG - debug message
2005-03-19 15:38:55,979 - simpleExample - INFO - info message
2005-03-19 15:38:56,054 - simpleExample - WARNING - warn message
2005-03-19 15:38:56,055 - simpleExample - ERROR - error message
2005-03-19 15:38:56,130 - simpleExample - CRITICAL - critical message
参考：stackoverflow: redirect prints to log file

