# Block

That’s correct. Since the block doesn’t capture any variables in its closure, it doesn’t need any state set up at runtime. it gets compiled as an NSGlobalBlock. It’s neither on the stack nor the heap, but part of the code segment, like any C function. This works both with and without ARC.

注意：不访问外部变量的是全局的block


而block在ARC与MRC下最大的区别就是没有了栈block.

http://blog.parse.com/learn/engineering/objective-c-blocks-quiz/
http://blog.devtang.com/blog/2013/07/28/a-look-inside-blocks/