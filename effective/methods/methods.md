1. 方法存在接受者，接受者的类型可以为 指针或者值，两者的区别在于

   1. 值方法可以通过指针和值调用
   2. 指针方法只能通过指针调用

   之所以会有这条规则是因为指针方法可以修改接受者，而通过值调用它们会导致方法接收到值的副本，因此任何修改都将会被丢弃。

