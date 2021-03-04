async --await无法在请求出现错误的时候捕捉到错误，await只能拿到promise的resolve的状态。

可使用try()catch{},

或者：

export handlerPromise = (promise) => promise.then(data => [null,data]).catch(err => [err]);

使用：

let [err,data] = await handlerPromise();

if(err) return;