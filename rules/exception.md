# 异常处理

1. **【强制】** 异常不要用来做流程控制，条件控制，因为异常的处理效率比条件分支低。

2. **【强制】** 对大段代码进行`try - catch`，这是不负责任的表现。`catch`时请分清稳定代码和非稳定代码，稳定代码指的是无论如何不会出错的代码。对于非稳定代码的`catch`尽可能进行区分异常类型，再做对应的异常处理。

3. **【强制】** 捕获异常是为了处理它，不要捕获了却什么都不处理而抛弃之，如果不想处理它，请将该异常抛给它的调用者。最外层的业务使用者，必须处理异常，将其转化为用户可以理解的内容。

4. **【强制】** 有`try`块放到了事务代码中，`catch`异常后，如果需要回滚事务，一定要注意手动回滚事务。

5. **【推荐】** 在代码中使用“抛异常”还是“返回错误码”，对于公司外的`http/api`开放接口必须使用“错误码”; 而应用内部推荐异常抛出; 跨应用间`RPC`调用优先考虑使用`Result`方式，封装`isSuccess`、“错误码”、“错误简短信息”。

   **<font color='#937c27'>说明：</font>** 关于`RPC`方法返回方式使用`Result`方式的理由:

	> 1) 使用抛异常返回方式，调用方如果没有捕获到就会产生运行时错误。
	> 2) 如果不加栈信息，只是`new`自定义异常，加入自己的理解的`error message`，对于调用端解决问题的帮助不会太多。 如果加了栈信息，在频繁调用出错的情况下，数据序列化和传输的性能损耗也是问题。
