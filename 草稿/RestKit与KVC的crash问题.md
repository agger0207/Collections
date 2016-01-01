Restkit与KVC的crash 问题

https://github.com/RestKit/RestKit/issues/1680


Since there is no way to verify a key-path prior to invoking valueForKeyPath: the only choice would be to wrap the KVC access in try/catch and then try to continue mapping. As @segiddins rightly points out, this has potentially unpredictable side-effects on the mapping process. It’s also potentially introduces a large performance penalty in any app that makes changes and doesn’t notice the log messages as mapping could be generating and rescuing any number of NSException instances (which are expensive to construct).

To my mind, this is programmer error and should immediately fail fast and hard so that you know about the problem and can address it.

那么最好是我们的Model类加一个！！