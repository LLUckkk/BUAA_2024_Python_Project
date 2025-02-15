本项目为buaa计算机学院2024年夏季学期Python程序设计课程大作业，由团队合作完成app的开发。

项目主题：任务管理app

技术栈：前端Pyqt，后端Python



**上传描述更新！**
**frontend/backend-(content)-author**

+ feat：提交新功能

+ fix：修复了bug

+ docs：只修改了文档

+ style：调整代码格式，未修改代码逻辑（比如修改空格、格式化、缺少分号等）

+ refactor：代码重构，既没修复bug也没有添加新功能

+ perf：性能优化，提高性能的代码更改

+ test：添加或修改代码测试

+ chore：对构建流程或辅助工具和依赖库（如文档生成等）的更改

> 毫不动摇地追随组长大人的步伐

# frontend

# backend

## database.py

### 数据库

使用阿里云数据库，可通过外网链接访问。

```python
host='rm-cn-g6z3tw7xl00052co.rwlb.rds.aliyuncs.com'
port=3306
user='buaa_python_2024'
passwd='DCJBzxhy2024'
database='python_todo'
```

#### 命名规范

> 表名：[对象单数<u>  </u>]对象复数
> 
> 列名：表名单数[<u>  </u><属性前缀>]<u>  </u>属性单数
> 
> 方法名：动词<u>  </u>列名/表名[<u>  </u>动词后缀]

### 密码机制

数据库中存储的是经过哈希加密后的密码以及加密所使用的盐。

- 生成密码时，将随机生成盐对输入的密码进行加密，再将二者存储到数据库中

- 检测密码正确与否时，将从数据库中获取盐对输入的密码进行加密，再与数据库中的密码进行比对

### `get_constant(file_name, constant_name)`

用于从数据库中获得常量的值，参数为 **文件名** 和 **常量名**，返回值均为 **字符串类型**。下面的代码可以获得发送方邮箱地址。

```python
send_by = get_constant(file_name, 'send_by')
```

把一些参数常量放在数据库，是为了不用修改代码就可以直接改变程序的运行状况。

### `add_user(user_name, user_email, user_password)`

用于向数据库中新增用户，参数为 **用户名**、**用户邮箱（需要保证唯一）** 和 **用户密码**，返回值为 **True** 或 **False** 代表操作是否成功。

### `delete_user(user_email)`

用于删除数据库中的指定用户，参数为 **用户邮箱（需要保证唯一）**，返回值为 **True** 或 **False** 代表操作是否成功。

### `reset_password(user_email, user_password)`

用于重置数据库中指定用户的密码，参数为 **用户邮箱（需要保证唯一）** 和 **新的用户密码**，返回值为 **True** 或 **False** 代表操作是否成功。

### `is_user_password_correct(user_email, user_password)`

用于检查指定用户的密码是否正确，参数为 **用户邮箱（需要保证唯一）** 和 **输入的用户密码**，返回值为 **True** 或 **False** 代表密码是否正确。

### `reset_name(user_email, user_name)`

用于重置用户名，参数为 用户邮箱 **用户邮箱（需要保证唯一）** 和 **新的用户名**，返回值为 **True** 或 **False** 代表操作是否成功。

### `is_user_email_exist(user_email)`

用于检测数据库中是否存在指定的邮箱，参数为 **用户邮箱（需要保证唯一）** ，返回值为 **True** 或 **False** 代表邮箱是否存在。

## send_email_code.py

### `is_valid_email(email)`

用于检测邮箱地址格式，是否合法，参数为**邮箱地址** 和 **输入的用户密码**，返回值为 **True** 或 **False** 代表格式是否正确。注：仅检查格式是否正确，不检查是否真实有效。

### `send_email_code(send_to)`

用于向指定邮箱发送验证码，参数为 **接收方邮箱地址**，发送成功将返回 **验证码（字符串类型）**，发送失败将返回 **False**。验证码为随机生成的六位大小写字母、数字的组合。下面的代码可以向`2892278592@qq.com` 发送并返回验证码。

```python
email_code=send_email_code('2892278592@qq.com')
```

使用 QQ 邮箱发送验证码，相关服务信息默认如下（可在数据库中修改，发送前会先更新）：

```python
send_by = '2892278592@qq.com'
email_password = 'kwniejavvatkdgcf'
mail_host = 'smtp.qq.com'
send_port = 465
```

## daily_sentence.py

### `get_sentence()`

用于随机产生每日一句格言，内容涵盖文学、影视、诗词、哲学等方面，返回值为 **格言内容（字符串类型）与出处的元组**。下面的代码可以获得一句格言及出处。

```python
sentenct=get_sentence()    # ('人生如逆旅，我亦是行人。', '临江仙·送钱穆父')
```
