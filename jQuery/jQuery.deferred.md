# jQuery.Deferred()
`jQuery.Deferred()`工厂函数创建一个`deferred`对象。    

`jQuery.Deferred`方法能传递一个可选的函数，仅在方法返回和传入了一个新的`deferred`对象，作为`this`对象同时也是这个函数的第一个参数被调用；使用`deferred.then()`能附带多个回调。    

一个Deferred对象起初是`pending`状态，使用`deferred.then()`,`deferred.always()`,`deferred.done()`或`deferred.fail()`添加的任何回调将被加入队列，在之后会被执行。调用`deferred.resolve()`或`deferred.resolveWith()`将Deferred过渡到`resolved`状态，并且立即执行所有之前设置的`doneCallbacks`.调用`deferred.reject()`或`deferred.rejectWith()`将Deferred过渡到`rejected`状态，并且立即执行之前设置过的所有`failCallbacks`.一旦deferred对象进入了resolved或rejected状态，就会保持那个状态不变。回调仍然能继续添加到resolved或rejected的Deferred对象，它们会立即执行。    

### 使用jQuery Deferred增强回调    

在js中，调用一个能接收可选的回调的函数非常普遍；例如，在早期的jQuery 1.5版本，像`jQuery.ajax()`异步处理,接收在不远的未来被调用的回调，在ajax请求成功、失败和完成之后。    
`jQuery.Deferred`引进了几种管理和调用回调的增强方式。特别的，`jQuery.Deferred()`提供灵活的方式去提供多个回调，并且这些回调能被调用，不管原来的回调分发是否已经触发了。jQuery Deferred基于[CommonJS Promises/A](http://wiki.commonjs.org/wiki/Promises/A)设计。    

用于理解Deferred的一个模型，就是想象它是一个可链式调用函数的包装。`deferred.then()`、`deferred.always()`、`deferred.done()`和`deferred.fail()`方法指定了被调用的函数，并且`deferred.resolve(args)`或`deferred.reject(arts)`方法使用你提供的参数“调用”函数。一旦Deferred被resolved或rejected，它的状态就保持不变了。`deferred.resolve()`的第二个调用，被忽略了。如果更多的函数通过`deferred.then()`添加，例如，在Deferred被resolved后，它们会使用之前提供的参数被立即调用。    
  在大多数情况下，一个jQuery API能返回一个Deferred或promise兼容的对象，例如`jQuery.ajax()`或`jQuery.when()`，你将只需要使用`deferred.then()`，`deferred.doan()`和`deferred.fail()`方法，去添加回调到Deferred的队列里。API调用的内部或者创建Deferred的代码，同一时间点，将在deferred对象上调用`deferred.resolve()`或`deferred.reject()`，对应的回调也会运行。
